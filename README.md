# Persian Tacotron2

**Persian Tacotron2** is a customized implementation of Tacotron2, adapted for Persian text-to-speech (TTS) synthesis. Tacotron2 is a model that converts text into mel-spectrograms, which can then be synthesized into audio. This implementation builds upon [NVIDIA's Tacotron2](https://github.com/NVIDIA/tacotron2) with adjustments for Persian phoneme-based data.

---

## Modifications for Persian Language

To adapt Tacotron2 for Persian, the following changes were made:
1. **Data Preparation**: Persian data is organized into audio files and corresponding phoneme sequences (using phonemes avoids issues related to Persian script and vowel omissions).
2. **Cleaner Modification**: Edited `cleaner.py` in `tacotron2/text/` to handle Persian phonemes.
3. **Hyperparameter Adjustment**: Customized `hparams.py` in `tacotron2/` for Persian language data.
4. **Data File Creation**: Created a script to format data into text files for training.
5. **Testing Script**: Added a script for testing the model on specific phoneme sequences.

---

## How to Use

### Setup

1. **Clone the Repository**  
   ```bash
   git clone https://github.com/your_username/persian_tacotron.git
   cd persian_tacotron

2. **Install Requirements**
    ```
    pip install -r tacotron2/requirements.txt
    ```
3. **Prepare Your Data**
    * Place audio files in files/wavs
    * Add phoneme transcriptions in `files/phoneme_transcriptions.txt`
4. **Create Data Files**
   Run the data preparation script:
    ```
    python create_data_file.py
    ```
    This will generate text files in `files/text_files/`. Move these files to `tacotron2/filelists/` for training.
5. **Configure Hyperparameters**
   Modify hparams.py in `tacotron2/` to set parameters like epochs, iters_per_checkpoint, training_files, and validation_files paths.

### Training
1. **Start Training**
    Begin training with:
    ```
    python tacotron2/train.py --output_directory=outdir --log_directory=logdir
    ```
    Checkpoints are saved in `tacotron2/outdir/`. For instance, with 1000 audio files and a batch size of 16, each epoch will include approximately 1000/16 iterations. If you encounter memory issues, reduce the batch_size in hparams.py.

2. **Test the Model**

    Update `get_results.py` with the phoneme sequence you’d like to test (text = "YOUR_TEST_PHONEME").
    Run inference with the latest checkpoint. For example:
    ```
    python get_results.py 32000
    ```
    Outputs (mel-spectrograms and audio files) will be saved in results/.

### Results
Training the model on 2500 audio files for 400 epochs produced the following results:

<img src="https://github.com/majidAdibian77/persian_tacotron/blob/master/result/plots/output_test2_56000(1634039244.8246922).jpg" width="1500">
Click [here](https://github.com/majidAdibian77/persian_tacotron/tree/master/result/wavs/) for sample audio results.

   
