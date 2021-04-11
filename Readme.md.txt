Hi,
I have tried multiple models but I have been unsuccesful in creating a model which works properly. 
If you run the project, the CNN implemented will return some good predictions along with bad predictions in the output list.
So I am describing my trials here, just in case.

First Trial:
Contour detection and HOG feature + SVM classifier 
I implemented a contour detection algorithm with opencv's "findcontours" function. The function was fed a canny edge detected image with some manual thresholds.
Then the detected contours were analysed for shapes. The contours which were ellipse(cv2.fitellipse) were shortlisted .
These ellipses were then given to the HOG feature extractor which gave features of shape 133.
Then these features were calssified using a pre-trained SVM classifier.

Problems:
The contour detection was poor due to variation in the UFO colors and their similarity with the background.
The classifier I used was LinearSVM which I think might have unable to classify the run time generated images(which were different from training images in orientation of numbers).
The training images were monotonous in position of the UFO and number. Improvement with transformation not tried.

Second Trial:
Sliding window and Neural net
I implemented a sliding window approach to extract small windows(80x80) of images from the parent "Frame.jpg"
These were given to the neural network to classify into 11 classes(one for each number(0-9) and one for background)

CNN architecture used here:
2 convolution layers(Both 3x3 kernels)
2 fully connected linear layers
Relu activation and dropout of 0.5

Problems:
CNN trained for 10 epochs has overfit the training images. Test accuracy didn't rise above 65%
I wasn't able to find a proper model to train for this task. 
To improve accuracy, I tried applying transformations(-15 to +15 rotation, -10 to +10 randomcrop, etc) to the training images, 
					 I tried with different dropouts
					 I tried increasing/decreasing number of layers/parameters
					 
I can get this method to work with some more time.


Another trial:
Contour detection and Neural net classifier
Same contour detection as in First Trial and tried some additional image aumentations like erode, histogram equalization and dilation.
Then the detected ellipses were fed to the CNN in Second Trial.

This trial failed because of contour detection which couldn't detect all the numbers in the image.
