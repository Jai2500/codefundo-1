# Drone Documentation

### Implementation of Recognition Model

- The current model for human recognition(which will be used to process images sent by the drone), on Azure, works at 64% precision and 41% Mean Average Precision(mAP). 
- It is implemented by training the model with images of people from previous natural disasters. It broadly classifies people based on their apparent size and orientation in the image as :-
  - Medium: 
    - Front facing
    - Back facing
    - Side facing
  - Small:
    - Front facing
    - Back facing
    - Side facing <br >
This allows the model to identify humans in the image whether they are near the drone or far away. 
- Maximum accuracy has been achieved when a person is facing the drone, while the model has lesser precision when the person is oriented with their back to the drone's camera.
- The model has been trained with 169 images from:
  - Kerala Floods (2018)
  - Japan Floods (2018)
  - South East European Floods (2018)
  - Maryland Floods (2018)
  - Quebec Floods (2017)
  - Alberta Floods (2013)
  - Thailand Floods (2010)
  - Hurricane Harvey Induced Flooding (2017)
- The model is also capable of recognizing make-shift rafts and damaged cars.

### Implementation of the Mapping System

- The mapping system is based on the Bing Maps API for Enterprices(provided by Azure), which uses the information from the drone and the Custom Vision model(Human Recognition Model), to provide a visual representation of people's locations on a map of the affected area.
- The file containing information supplied by the drone is of the GeoJson filetype, which is one of the best formats for processing geo-spatial data. 
- A simple HTML file is created that calls the Bing Maps API and uses its inbuilt tools to pinpoint people's locations on the map.
- An Ajax styled implementation will also be able to support real time tracking of the people in the affected regions.
- The above can be implemented very easily on Bings API by running the below code in a browser and dragging and dropping the GeoJson file onto the map shown on the browser
``` HTML
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8" />
    <script type='text/javascript'>
    var map;
    function GetMap() {
        map = new Microsoft.Maps.Map('#myMap', {
            zoom: 1
        });
        //Load the GeoJSON module.
        Microsoft.Maps.loadModule('Microsoft.Maps.GeoJson', function () {
            
        });
    }
    function handleFileSelect(evt) {
        
            var reader = new FileReader();
            reader.onload = function (e) {
                try {
                    var geoJsonText = e.target.result;
                    //Attempt to parse the file as GeoJSON and add the shapes to the map.
                    var shapes = Microsoft.Maps.GeoJson.read(geoJsonText);
                    map.entities.push(shapes);
                    
                    //Calculate the bounding box of the data in the single file. 
                    var bounds = Microsoft.Maps.LocationRect.fromShapes(shapes);
                    //If data is already loaded from another GeoJSON file, merge the bounding boxes together.
                    if (dataBounds) {
                        dataBounds = Microsoft.Maps.LocationRect.merge(dataBounds, bounds);
                    } else {
                        dataBounds = bounds;
                    }
                    //Update the map view to show the data.
                    map.setView({ bounds: dataBounds, padding: 50 });
                } catch (e) {
                    alert('Unable to read file as GeoJSON.');
                }
            };
    }
    </script>
    <script type='text/javascript' src='https://www.bing.com/api/maps/mapcontrol?callback=GetMap&key=[API KEY]' async defer></script>
</head>
<body>
    <div id="myMap" style="position:relative;width:800px;height:600px;"></div>

</body>
</html>
```

### Implementation of the Drone(Physically)


