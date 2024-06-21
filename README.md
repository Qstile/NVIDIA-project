# Aircaft flying and not flying

 Add a short description of the project here > 

CODE NEEDED FOR THIS PROGRAM![code  for invidia project](https://github.com/Qstile/NVIDIA-project/assets/172285930/158711c4-7a8d-4fc4-9e61-d1d6065733c4)


## The Algorithm

Model The way this works is that first, I chose to use Resnet-18, which is a pre-trained model. Resnet-18 is already on downloaded onto the jetson, but it is not made to recognize different locations of the aircraft, which is why it needs to be trained.

Data and training The data I found was from Jetphotos.com, specifically for data classification. I then categorized it myself, combining data from different sets. I had two categories: it was either in the air or on the ground. I then made three folders: test, train, and validation. In my training set, I had about 50 images per category, in the validation around 100, and in the test between 50 images. I also had a text file with all the labels, for when I trained the Resnet-18 model. The model was then trained using a pre-written Python file from the module, in order to train the network to recognize what these different items are. A lot of training had to be done to get correct values.

Once I trained the model, it was able to recognize the different locations of the aircraft it was presented with. I then exported the model in the ONNX format and saved it to the jetson.

Results Now that the model was trained, and could classify spots the plane was, I had to create a way to output the results. Once the data was set, I wrote a Python file to be able to output the data.



## Running this project

Training:

Make sure you have resnet-18 already downloaded onto your jetson.
All of the files in the GitHub should be downloaded onto the jetson, including all Python scripts that will be used.
Change directories into jetson-inference/python/training/classification/data
Download the data from the "garbage-data-main" folder, and download that onto the jetson by getting the download link and typing "get" and then the link.
unzip the file, by running "unzip", and then the link we just did get to.
Go to the jetson-inference folder and run: ./docker/run.sh
Go back to jetson-inference/python/training/classification
To train the data, run the following: python3 train.py--model-dir=models/garbage_classification data/garbage-data-main
Allow the resnet-18 model to train for at least 10 epochs, but the more training that is done, the better.
Exporting the model

Make sure the onnx_export.py file is on the jetson, if not do that first.
Stay in the jetson-inference/python/training/classification folder.
Run: python3 onnx_export.py --model-dir=models/garbage_classification.
There should be a model named resnet18.onnx in jetson-inference/python/training/classification/models/garbage_classification.
Outputting the data:

To see the overall accuracy of the trained model, go to the jetson-inference/python/training/classification, and type: python3 train.py -e --model-dir=models/final_project data/garbage-data-main.
You should be able to see the accuracy of the validation data.
In order to get a visual representation of the data, in your home terminal, type: imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/image.jpg name.jpg
The image should now be saved on your laptop, with the label of what it is.

[My project video description](https://youtu.be/x9TlX8DYVkw?si=fMsmfeztpdZKDq8V)
