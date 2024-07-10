# ProjectPneumonia

 This project aims to use Artificial Intelligence to identify a presence of pneumonia in an xray. This AI helps classify xray pictures into 2 categories : Normal,Pneumonia. This helps separate the cases of patients who may be infected with this disease.

Identification of X-ray of Pneumonia infected patient

[6](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/4480a308-23f0-48e5-8cba-d5a41264a2ab)


## The Algorithm

For this project , to create and train a model , we used resnet18 which is a special type of network using 18 layers and employing CNN, convolutional neural network. CNN has its downsides , notably the time it takes to train, however it is widely considered the best neural network for image detction.

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

When training a model, different indications are given and should not be neglected:
 - train loss: The margin of loss and error in the epoch ran
 - Time: time spent running an epoch
 - train accuracy: The overall sucess rate of the epoch run
 - val accuracy: Accuracy while running the model in the validation set , essentielly another dataset that serves as validation
 - val loss: The margin of loss and error when going through the validation set
 
### Observations

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/dce6f0f1-d161-46a1-b3d7-ec2091c73b2e)

As shown in the graph above accuracy improves over time however it does reach a limit point, often found in the 85-95%. However after a certain number of epochs a problem can occur called overfitting. 

Overfitting is the case where the AI model trains too many times to the point where it loses accuracy as it tends to focus on smaller insignificant and irrelevant details after processing the same images too many times.This damages significantly the accuracy of your model as seen below.

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/9cf3760d-9e56-45ca-a2a9-f2be6b0bf841)

Underfitting also exits and in opposition to overfitting consist of not training a model enough meaning it will be inaccurate and inconsistent.

A simple relation exits between loss and epochs, the more epochs are run, the more the amount of loss diminishes.

![image](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/391652b5-4127-421f-9776-f6ef18996a01)

## Running this project

1. Choose the dataset, and the images, personally recommend to use 4000 images per label
2. Unzip the file and name it project
3. sort the images into 3 sections: train,test,val , respect the following ratio of data train:80% test:10% val:10%
4. Each file should have 50/50 split between normal and pneumonia both in 2 separate folders like this: Project--> train-->Normal
5. Create the diffrent labels: Normal and pneumonia in a txt file in the ProjectPneumonia file
6. Import the ProjectPneumonia folder into VS code in this directory *jetson-inference/python/training/classification/data*
7. Open a new terminal in jetson-inference directory and run the docker with the following command './docker/run.sh' this starts running the docker container to allow you to go trhough images and train the model
8. In the docker naviguate to jetson-inference/python/training/classification
9. Enter the following code to start training the model 'python3 train.py --model-dir=models/ProjectPneumonia data/ProjectPneumonia --epochs=70' This will run 70 epochs which shoul be enough to train the model
10. Once done training, enter this command 'python3 onnx_export.py --model-dir=models/cat_dog' to run the onnx srcipt . Check in jetson-inference/python/training/classification/models/ProjectPneumonia a file resnet18.onnx should be present
11. Exit the docker with ctrl+D or exit command
12. Enter both these commands to set the dataset and the network 'NET=models/cat_dog' 'DATASET=data/cat_dog'
13. Finally, run this command to obtain results in the selected choice 'imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/Pneumonia/(selected image).jpeg testp1.jpg'

## Conclusion
Here are examples of x ray scans tested.

A normal patient: 

Accuracy 79.10% , this is good accuracy and the correct answer

![12](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/57cf2aa7-2b32-4820-bc38-ed8d958e34a6)

A sick patient: 

Accuracy 85% , very good accuracy and the correct answer

![14](https://github.com/yoyofuji/ProjectPneumonia/assets/174374607/a7d6b37e-37c4-46d7-b23d-30eb73e8c7c9)





[View a video explanation here](video link)
