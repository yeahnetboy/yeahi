# yeahi
enjoy the auto choose music by ai

base the MuseGAN
MuseGAN is a project on music generation. In a nutshell, we aim to generate polyphonic music of multiple tracks (instruments). The proposed models are able to generate music either from scratch, or by accompanying a track given a priori by the user.

We train the model with training data collected from Lakh Pianoroll Dataset to generate pop song phrases consisting of bass, drums, guitar, piano and strings tracks.

Sample results are available here.

Prerequisites
Below we assume the working directory is the repository root.

Install dependencies
Using pipenv (recommended)

Make sure pipenv is installed. (If not, simply run pip install pipenv.)

# Install the dependencies
pipenv install
# Activate the virtual environment
pipenv shell
Using pip

# Install the dependencies
pip install -r requirements.txt
Prepare training data
The training data is collected from Lakh Pianoroll Dataset (LPD), a new multitrack pianoroll dataset.

# Download the training data
./scripts/download_data.sh
# Store the training data to shared memory
./scripts/process_data.sh
You can also download the training data manually (train_x_lpd_5_phr.npz).

Scripts
We provide several shell scripts for easy managing the experiments. (See here for a detailed documentation.)

Below we assume the working directory is the repository root.

Train a new model
Run the following command to set up a new experiment with default settings.

# Set up a new experiment
./scripts/setup_exp.sh "./exp/my_experiment/" "Some notes on my experiment"
Modify the configuration and model parameter files for experimental settings.

You can either train the model:

# Train the model
./scripts/run_train.sh "./exp/my_experiment/" "0"
or run the experiment (training + inference + interpolation):

# Run the experiment
./scripts/run_exp.sh "./exp/my_experiment/" "0"
Use pretrained models
Download pretrained models

# Download the pretrained models
./scripts/download_models.sh
You can also download the pretrained models manually (pretrained_models.tar.gz).

You can either perform inference from a trained model:

# Run inference from a pretrained model
./scripts/run_inference.sh "./exp/default/" "0"
or perform interpolation from a trained model:

# Run interpolation from a pretrained model
./scripts/run_interpolation.sh "./exp/default/" "0"
Outputs
By default, samples will be generated alongside the training. You can disable this behavior by setting save_samples_steps to zero in the configuration file (config.yaml). The generated will be stored in the following three formats by default.

.npy: raw numpy arrays
.png: image files
.npz: multitrack pianoroll files that can be loaded by the Pypianoroll package
You can disable saving in a specific format by setting save_array_samples, save_image_samples and save_pianoroll_samples to False in the configuration file.

The generated pianorolls are stored in .npz format to save space and processing time. You can use the following code to write them into MIDI files.

from pypianoroll import Multitrack

m = Multitrack('./test.npz')
m.write('./test.mid')
Sample Results
Some sample results can be found in ./exp/ directory. More samples can be downloaded from the following links.

sample_results.tar.gz (54.7 MB): sample inference and interpolation results
training_samples.tar.gz (18.7 MB): sample generated results at different steps
Papers
Convolutional Generative Adversarial Networks with Binary Neurons for Polyphonic Music Generation
Hao-Wen Dong and Yi-Hsuan Yang
in Proceedings of the 19th International Society for Music Information Retrieval Conference (ISMIR), 2018.
[website] [arxiv] [paper] [slides(long)] [slides(short)] [poster] [code]

