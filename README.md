# CS5330-proj5
___________________________________________________________________________________________________________________
## 👥 Team Members

1. **Yuyang Tian**
2. **Arun Mekkad**
___________________________________________________________________________________________________________________
## 💻 Environment

- **🖥️ Yuyang Tian**: macOS 10.13.1 + CLion
- **🐧 Arun Mekkad**: Ubuntu 22.04 LTS + VS Code
___________________________________________________________________________________________________________________
### 📂 File Structure
    ```
    Proj5/
    ├── data/                 # 📁 Data files
    |   ├── MNIST             # 🖼️ MNIST Samples
    |   ├── Handwritten       # 🖼️ Handwritten Samples
    ├── src/                  # 📁 Source files
    |   ├── examine.py
    |   ├── experiment.py 
    |   ├── live_digit_recognition.py 
    |   ├── plot.py 
    |   ├── test_greek.py 
    |   ├── test.py 
    |   ├── train_dcgan.py 
    |   ├── train_greek.py 
    |   ├── train.py 
    |   ├── visualize_gan.py 
    ├── trained_models        # 📁 Directory for saving trained models
    ├── README.md             # 📖 Project documentation
    ```
___________________________________________________________________________________________________________________

## 📌 Tasks

## 1.Build and train a network to recognize digits

* RUN `train.py` 

### TaskA

The MNIST dataset is loaded using `load_mnist_test_data`, and the first 6 digits are visualized by calling `plot_mnist_samples`. Both steps are executed in the `main` function.

### TaskB

The CNN architecture is implemented in the `MyCNNNetwork` class. All layers are defined in the `__init__` method, and the `forward` method specifies how the input flows through those layers.

### TaskC

Trains a deep learning model on MNIST digits dataset. The model will be trained for 5 epochs, with each batch of training data containing 64 samples (batch_size = 64)

### TaskD

Saves the trained model in trained_models folder. Create this folder before running the code.

* RUN `test.py`

### TaskE

Loads the pre-trained model from local path and tests the model using example dataset.

### TaskF

* RUN `test.py <handwritten_directory_path>`

Eg. test.py ../data/Handwritten

Adds all the images within the provided directory, pre-processes it, runs the test and visualizes the predictions.
-------------------------------------------------------------------------------------------------------------------

## 2. Examine the network ---

RUN `examine.py`

### TaskA

Plot the weighted filters from first convolutional layer

### TaskB

Visualize the weighted filter and first image from train dataset with applied filters
-------------------------------------------------------------------------------------------------------------------

## 3. Transfer Leaning on Greek Letters

RUN `train_greek.py`

Trains a deep learning model on greek_train dataset. The model will be trained for 20 epochs, with each batch of training data containing 5 samples (batch_size = 5)

RUN `test_greek.py`

Adds all the images within the provided directory, pre-processes it, runs the test and visualizes the predictions.
-------------------------------------------------------------------------------------------------------------------

## 4. Design your own experiment

RUN `experiment.py`

Evaluates multiple CNN models with different hyperparameter combinations on the FashionMNIST dataset, saving the test accuracy and training time for each configuration to a CSV file. The process of generating different variations (136) of the model took around 1.5 hours on GPU device (GeForce 4060 RTX)
-------------------------------------------------------------------------------------------------------------------

## Extension

### 1.  More greek letters recognition

### Train/ Test with Extension Flags

You can now pass `--extension` to both **`train_greek.py`** and **`test_greek.py`**:

- **Added Lambda & Theta:**
   These images were introduced in both training and testing sets. The total number of Greek letters in training set dynamically sets the size of the final fully connected layer.
- **Training (`train_greek.py`)**
  - **No extension flag**: Trains on `data/greek_train_3` and tests on `data/greek_test_3`.
    - A alternative test dataset `data/greek_test_3(2)` is provided to play around
    -  The default 3-class model is stored as `../trained_models/greek_trained_model.pth`.
  - **`--extension` flag**: Trains on `data/greek_train_5` and tests on `data/greek_test_5` (because we’ve added lambda and theta).
  - Automatically detects the number of letters and configures the model’s final layer.
  - Saves as `../trained_models/greek_trained_{num_classes}.pth`.
- **Testing (`test_greek.py`)**
  - **No extension flag**: Loads the default model from `../trained_models/greek_trained_model.pth`.
    - Performs letter recognition on the `test_greek_3` folder and visualizes the results.
  - **`--extension` flag**: Loads `../trained_models/greek_trained_{num_classes}.pth`.
    - Performs letter recognition on the `test_greek_5` folder and visualizes the results.

### 2. DC-GAN

Please refer to [Pytorch Tutorials](https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html#results) for more information on how DC-GAN works under the hood.

* **Training** with `train_dc_gan.py`

  This script trains DC-GAN networks based on the `data/celeba_10k` folder, which contains 10,000 images from the [Large-scale CelebFaces Attributes (CelebA) Dataset](https://mmlab.ie.cuhk.edu.hk/projects/CelebA.html). Each image is associated with a celebrity ID (some celebrities have multiple images). The original CelebA dataset has over 200K images; for assignment purposes, it’s downsampled to 10K.

  The generator model is saved as `../trained_models/gan_models_generator.pth` and the discriminator is saved as `../trained_models/gan_models_discriminator.pth`

  **Note**: Training can take about 40 minutes on a CPU, so if you prefer, you can skip retraining and just load the existing model for generating images.

* **Generating and Visualizing with `visualize_gan.py`**
   This script loads the trained DC-GAN model and displays a batch of generated images. It points to the model path from the training script, then visualizes images created by the trained generator.

* The result images was saved to `outputs` dir for reference

### 3. Live Digit Recognition

RUN `live_digit_recognition.py`

Creates a GUI using Tkinter for live handwritten digit recognition. Users can draw digits on a canvas, and upon clicking **Recognize**, the application preprocesses the drawn image and uses a pre-trained MNIST model to predict the digit. The predicted digit is then displayed on the screen.