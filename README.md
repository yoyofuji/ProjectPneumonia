# ProjectPneumonia

 This project aims to use Artificial Intelligence to identify a presence of pneumonia in an xray. This AI helps classify xray pictures into 2 categories : Normal,Pneumonia. This helps separate the cases of patients who may be infected with this disease.

![Identification of X-ray of Pneumonia infected patient]![6](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/4480a308-23f0-48e5-8cba-d5a41264a2ab)


## The Algorithm

For this project , to create and train a model , we used resnet18 which is a special type of network using 18 layers and employing CNN. 

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/1bc243ca-7298-4caf-85f7-9e3a42a068cc)

To train the model , we used an already existing model, imagenet which is the key databse to image classiffication.
Through this model, we can create our own running our own data, for this , multiple factors are to take into consideration:

  1)Batchsize, this is the specification that indicates how many images are we training at once, for example, we could train 10 images at once which wouldve give 1 batch.By default it is 10
  
    '--batch-size=NumberOfBatchFiles'
    
  2)Workers, workers is the specification of the number of threads that will simultaneously train the model, just like in real life 5 workers working on something often leads to increase speed. 
    However to run multiple workers a certain level of hardware and infrastructure is needed. By default it is 1
    
    '--workers=NumberOfWorkers'
    
  3)Epochs, is the the number of times the model wiil go through every image inputed. When running 10 epochs, an image will be analysed and looked at 10 times in the training process. By default it is 35
  
    '--epochs=NumberOfEpochs'

    
The final line to train should be:

'python3 train.py --model-dir=models/(name_of_model) data/(name_of_file_with_data) --epochs=35 --batch-size=1 --workers=1'

When training a model, different idications are given and shouldnt be neglected.
 - Val loss:The margin of loss and error in the epoch ran
 - Val time:time spent running an epoch
 - Val accuracy:The overall accuracy of the epoch run
 
### Observations

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/dce6f0f1-d161-46a1-b3d7-ec2091c73b2e)

As shown in the graph above accuracy improves over time however it does reach a limit point, often found in the 85-95%. However after a certain number of epochs a problem can occur called overfitting. 

Overfitting is the case where the AI model trains too many times to the point where it loses accuracy as it tends to focus on smaller insignificant and irrelevant details. 

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/9cf3760d-9e56-45ca-a2a9-f2be6b0bf841)

A simple relation exits between loss and epochs, the more epochs are run, the more the amount of loss diminishes.

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/391652b5-4127-421f-9776-f6ef18996a01)

## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.

[View a video explanation here](video link)
