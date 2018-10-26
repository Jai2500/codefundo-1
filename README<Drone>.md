# Drone Documentation

### Implementation of Recognition Model

- The current model for human recognition(which will be used to process images sent by the drone), on Azure, works at 64% precision and 41% Mean Average Precision(mAP). 
- It is implemented by training the model with images of people from previous natural disasters. It broadly classifies people based on their apparent size in the image as :-
  - Medium: 
    - Front facing
    - Back facing
    - Side facing
  - Small
    - Front facing
    - Back facing
    - Side facing
