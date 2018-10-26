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
    - Side facing
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

  
