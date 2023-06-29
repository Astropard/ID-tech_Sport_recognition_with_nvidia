# ID-tech_Sport_recognition_with_nvidia

Using pretrained detection models the program will recognize a large amount of objects in a live video as well as certain sport activities.

![add image descrition here](direct image link here)

## The Algorithm

### Installing the pretrained models:
1. Connect by SSH into your Nano using PuTTy or on your dekstop with nvidia
2. Enter your password when prompted, and ensure that you are in a command line on your Nano.
3. Run this command to install cmake. <<sudo apt-get install git cmake>>
4. Clone the jetson-inference project using the commands below.
   <<git clone --recursive https://github.com/dusty-nv/jetson-inference>>
   <<cd jetson-inference>>
   <<git submodule update --init>>
5. In order to install the necessary python packages, run this command.  <<sudo apt-get install libpython3-dev python3-numpy>>
6.  Next, make a build directory to build your project into. Make sure you are in the jetson-inference directory before running these commands.  <<mkdir build>>
7.  Change directories into build and run make to build the project.
   <<cd build>>
   <<cmake ../>>
8. While configuring, you will see the downloader tool. You can access this tool at any time using commands, so for now, leave the selections as they are.
9. You will also see the PyTorch installer. You do not need to install PyTorch, so if there is a star in one of these installation options, use the spacebar to un-select it, and press Enter to continue.
10. Once this finishes loading you should see a space to run commands again. Make sure that you are still in the build directory and run these commands
    <<make>>
    <<sudo make install>>
    <<sudo ldconfig>>

### Setting up the docker: 
https://catalog.ngc.nvidia.com/orgs/nvidia/teams/dli/containers/dli-nano-ai
### Re-training with a new dataset:
1. Download a dataset, the command to download should have : 1.The download command(wget) 2.The download url 3.The name you want the file to have on you nano.
2. Unzip the file, to do so you may want to use different commands depending on the file. For a zip file you will use the unzip command
   run this code: <<sudo apt-get install unzip>> and then <<unzip filename>>
   for a gz.tar file run this command <<tar xvzf filename>>
3. From the jetson-inference folder, run <<./docker/run.sh>> to run the docker container.
4. From inside the Docker container, change directories so you are in jetson-inference/python/training/classification
5. Run the training script to re-train the network where the model-dir argument is where the model should be saved and where the data is.  You should immediately start to see output, but it will take a very long time to finish running.
   <<python3 train.py --model-dir=models/directoryname data/directoryname>> to control the number of epochs, workers, batchsize, etc add this on the same line <<--epochs=35>>
6.To interupt the training do Ctrl+C
7.Run the onnx export script. <<python3 onnx_export.py --model-dir=models/cat_dog>>

## Running this project
1. Open VScode
2. Run the imagenet, detectnet, etc commands with the name of the file you want to analyze and the name of the output file

[View a video explanation here](video link)
