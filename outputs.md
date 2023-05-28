# REMARK 1

We have stored all the images and their labels into lists (data and labels).
We need to convert the list into numpy arrays for feeding to the model.

The shape of data is (39209, 30, 30, 3) which means that there are 39,209 images of size 30×30 pixels and the last 3 means the data contains colored images (RGB value).
With the sklearn package, we use the train_test_split() method to split training and testing data.
From the keras.utils package, we use to_categorical method to convert the labels present in y_train and t_test into one-hot encoding.

![op1](https://media.discordapp.net/attachments/1101944447740162058/1101944498566729728/op1.png?width=607&height=242)

## OUTPUT 1

# REMARK 2

To classify the images into their respective categories, we will build a CNN model (Convolutional Neural Network). CNN is best for image classification purposes.

The architecture of our model is:

2 Conv2D layer (filter=32, kernel_size=(5,5), activation=”relu”)
MaxPool2D layer ( pool_size=(2,2))
Dropout layer (rate=0.25)
2 Conv2D layer (filter=64, kernel_size=(3,3), activation=”relu”)
MaxPool2D layer ( pool_size=(2,2))
Dropout layer (rate=0.25)
Flatten layer to squeeze the layers into 1 dimension
Dense Fully connected layer (256 nodes, activation=”relu”)
Dropout layer (rate=0.5)
Dense layer (43 nodes, activation=”softmax”)
We compile the model with Adam optimizer which performs well and loss is “categorical_crossentropy” because we have multiple classes to categorise.

[Link to code segment - Training the model](https://github.com/Dunno-Ikigai/Traffic-sign-recognition/blob/e7243f2e637a6d8bb5833a223455d4ce9b36f01b/Traffic_signs.py#L48)

![op2](https://raw.githubusercontent.com/Dunno-Ikigai/Traffic-sign-recognition/main/Model%20Training%202.png)

## OUTPUT 2

# REMARK 3

After building the model architecture, we then train the model using model.fit(). I tried with batch size 32 and 64. Our model performed better with 64 batch size. And after 15 epochs the accuracy was stable.

[Link to code segment - Plotting accuracy graph](https://github.com/Dunno-Ikigai/Traffic-sign-recognition/blob/e7243f2e637a6d8bb5833a223455d4ce9b36f01b/Traffic_signs.py#LL70C1-L70C1)

![op3.1](https://raw.githubusercontent.com/Dunno-Ikigai/Traffic-sign-recognition/main/Accurracy%20plot.png)
![op3.2](https://raw.githubusercontent.com/Dunno-Ikigai/Traffic-sign-recognition/main/Loss%20plot.png)

## OUTPUT 3

# REMARK 4

Our dataset contains a test folder and in a test.csv file, we have the details related to the image path and their respective class labels. We extract the image path and labels using pandas. Then to predict the model, we have to resize our images to 30×30 pixels and make a numpy array containing all image data. From the sklearn.metrics, we imported the accuracy_score and observed how our model predicted the actual labels. We achieved a 95% accuracy in this model.

[Link to code segment - Testing accuracy on "test" dataset](https://github.com/Dunno-Ikigai/Traffic-sign-recognition/blob/e7243f2e637a6d8bb5833a223455d4ce9b36f01b/Traffic_signs.py#LL89C1-L89C1)

In the end, we are going to save the model that we have trained using the Keras model.save() function.

# REMARK 5

Now we are going to build a graphical user interface for our traffic signs classifier with Tkinter. Tkinter is a GUI toolkit in the standard python library. Make a new file in the project folder and copy the below code. Save it as gui.py and you can run the code by typing python gui.py in the command line.

In this file, we have first loaded the trained model ‘traffic_classifier.h5’ using Keras. And then we build the GUI for uploading the image and a button is used to classify which calls the classify() function. The classify() function is converting the image into the dimension of shape (1, 30, 30, 3). This is because to predict the traffic sign we have to provide the same dimension we have used when building the model. Then we predict the class, the model.predict_classes(image) returns us a number between (0-42) which represents the class it belongs to. We use the dictionary to get the information about the class. Here’s the code for the gui.py file.

[Link to code - GUI](https://github.com/Dunno-Ikigai/Traffic-sign-recognition/blob/main/GUI_traffsign.py)

FINAL WORKING OF THE FIRST VERSION OF OUR PROJECT: 

![op5](https://cdn.discordapp.com/attachments/1112393409227931720/1112397021106679828/traffic-sign-recognition-project.gif)

## OUTPUT 5




