# SSLearningPipeLine

# Operations


Create a working directory, ie

```
mkdir work
cd work
source /reg/g/psdm/etc/psconda.sh
```
on pslogin (outside internet machine):

```
git clone https://github.com/mmongia/SSLearningPipeLine.git
```
First 


```
cp -r /reg/g/psdm/tutorials/transferLearning .
```

In SSLearningPipeLine, in user_driver.py, in first line of main(), change outputdir to the address for the transferLearning folder under work.


Now in another terminal, 

```
ssh psana
source /reg/g/psdm/etc/psconda.sh
cd ./work/SSLearningPipeline
PYTHONPATH=../transferLearning/pylabelme python user_driver.py
```

notice that the script, user_driver.py, is telling sslearn to write the labeled files into your transferlearning directory.



# How to get error results

We first need to edit user_driver.py file. In the main function where the following lines of code are written 
```
    for idx in A:
        #break

```
edit it so that reads. 
```
    for idx in A:
        break
```

Run the code using
```
PYTHONPATH=../transferLearning/pylabelme python user_driver.py
```
and from code located in sslearningpipeline.py, a graph plotting the errors of the predicted boxes will be produced.
The graph should look similar to  below.



![alt text](https://github.com/mmongia/SSLearningPipeLine/blob/master/ErrorFromTransferLearning.JPG)





# How to label images
Make sure in the main function in user_driver.py that the code reads like the following


```
    for idx in A:
        #break
```

(comment out the break)

Now run the code using the following 

```
PYTHONPATH=../transferLearning/pylabelme python user_driver.py
```
You will see that many images come up one after another. These images are already labeled. Eventually there will come an image that has not been labeled and you will have a choice to label it or not.

![alt text](https://github.com/mmongia/SSLearningPipeLine/blob/master/Comment1.JPG)

You can click enter on the command prompt to label. You can type "n" and then click enter to move on. Make sure to label images that only have fingers on the top island. For the sake of this tutorial we have set up the code to worry about the top finger. Once you find an image that has a top finger and you click enter you will see something like the following 


![alt text](https://github.com/mmongia/SSLearningPipeLine/blob/master/Comment2.JPG)

In order to label click on the "create polygon" button and draw a line. This line will be the diagonal of rectangular box. Then there will be prompt to give a label to the rectangular box. For the sake of this tutorial always label it "0" as shown in the below image.


![alt text](https://github.com/mmongia/SSLearningPipeLine/blob/master/comment3.JPG)


You can keep doing this. If you want to exit from doing this just press ctrl+c.

# The role of certain variable and directories in this code


  vgg16 weights:
  
  These are very important. These weights are the weights of the VGGNET model which we past each image through to get codewords. These     codewords will be the our feature set for any machine learning ( as simple as linear regression) task we want to do.
  
  json directory:
    
  After labeling an image, the locations of the boxes drawn and their corresponding labels are stored in a json file. From the json       files of the labeled images we create machine learning models.
    
  codewords:
    
  Once again these codewords are generated by passing the images through the vgg net. 
  
  index list:
  
  This is just a predefined list of images that we will be looking at. From this list of indexes we can gather the images from the the     corresponding experiment's database.
  
  dark image:
    
  This is an image which represents what the camera sees when there is no action going on. It is important to subtract this from the       images so we can see the image that corresponds to the real action. This perhaps was a bit to figurative of an explanation.
