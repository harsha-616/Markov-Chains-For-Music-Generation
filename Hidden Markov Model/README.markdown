# Music Generation with Hidden Markov Model

This project implements a music generation system using a Hidden Markov Model (HMM) to create simple musical sequences based on classical music MIDI files. The application is built as a Jupyter Notebook and uses the `music21` Python library to process MIDI data and generate new music sequences. The input data is sourced from the GiantMIDI-Piano dataset, specifically using a subset of Franz Schubert's *Fantasie in C major* MIDI files.

## Project Overview

The goal of this project is to generate sparse, ambient-like melodies using an HMM. The system:

- Loads MIDI files from a specified directory.
- Extracts musical elements (notes, chords, rests) and organizes them by measure.
- Trains an HMM using observation sequences of musical types (`<NOTE>`, `<CHORD>`, `<REST>`).
- Generates a new musical sequence by predicting the most likely sequence of musical elements.
- Exports the generated sequence as a MIDI file.

This project is based on the *HackerNoon* guide "Music Generation Via A Hidden Markov Model - Part 1" by *Picture in the Noise*.

## Prerequisites

To run this project, you need:

- **Python 3.x** installed.
- **Jupyter Notebook** environment.
- **Git** installed for cloning the GiantMIDI-Piano repository.
- Intermediate knowledge of Python and machine learning concepts, particularly Hidden Markov Models (HMMs).
- A basic understanding of music theory is helpful but not required.

### Required Python Packages

Install the necessary Python packages using pip:

```bash
pip install numpy music21
```

## Setup Instructions

1. **Clone the GiantMIDI-Piano Repository**: Clone the GiantMIDI-Piano dataset repository to access sample MIDI files:

   ```bash
   git clone https://github.com/bytedance/GiantMIDI-Piano.git
   ```

2. **Create a Data Directory**: Create a directory (e.g., `midi-music`) to store the MIDI files used as input data. Copy the following MIDI files from `GiantMIDI-Piano/midis_for_evaluation/giantmidi-piano` to your data directory:

   - `Schubert_Fantasie_in_C_major_D760_lR43Ti4w5MM_cut_mov_1.mid`
   - `Schubert_Fantasie_in_C_major_D760_lR43Ti4w5MM_cut_mov_2.mid`
   - `Schubert_Fantasie_in_C_major_D760_lR43Ti4w5MM_cut_mov_3.mid`
   - `Schubert_Fantasie_in_C_major_D760_lR43Ti4w5MM_cut_mov_4.mid`

3. **Update the Notebook**: In the Jupyter Notebook, update the `DATA_DIR` constant in **Cell 2** to point to your data directory (e.g., `C:/midi-music`).

4. **Run the Notebook**: Open the Jupyter Notebook (`music_generation_hmm.ipynb`) and execute all cells in order. The notebook will:

   - Load and process the MIDI files.
   - Train the HMM using the specified observation sequence.
   - Generate a new musical sequence.
   - Export the result as a MIDI file (e.g., `hmm_music_exp_1_using_schubert_fantasie.mid`).

## Project Structure

- `music_generation_hmm.ipynb`: The main Jupyter Notebook containing the music generation code.
- `midi-music/`: Directory containing the input MIDI files (user-created).
- `README.md`: This file, providing an overview and instructions for the project.

## How It Works

The notebook is divided into three main parts:

1. **Loading and Processing MIDI Data**:

   - Uses `music21` to load MIDI files and extract musical elements (rests, notes, chords).
   - Organizes elements by measure and extracts properties like pitch and duration.

2. **Training the HMM**:

   - Defines observation sequences (`<NOTE>`, `<CHORD>`, `<REST>`) to train the HMM.
   - Calculates initial, transition, and emission probability matrices.
   - Uses the Viterbi algorithm to predict the most likely sequence of musical elements.

3. **Generating and Exporting Music**:

   - Converts the predicted sequence into a `music21` stream.
   - Exports the stream as a MIDI file for playback or further editing.

## Running Experiments

To run additional experiments:

1. Modify the `USE_OBS` constant in **Cell 2** to select a different observation sequence (`OBS1`, `OBS2`, `OBS3`, or `OBS4`).
2. Update the `FILENAME` in **Cell 23** to save the output to a new MIDI file.
3. Re-run the notebook from **Cell 16** onward to generate a new sequence.

## Expected Output

The generated MIDI file (e.g., `hmm_music_exp_1_using_schubert_fantasie.mid`) contains a sparse melody that may not sound as polished as modern AI-generated music (e.g., from Udio or Suno). However, it can produce interesting sequences suitable for inspiration or further composition. The output can be played using any MIDI-compatible software or imported into a MIDI editor like Signal Online MIDI Editor (covered in Part 2 of the guide).

## Limitations

- The generated music is basic and may not always sound musically coherent due to the simplicity of the HMM.
- The model is sensitive to the input observation sequence and dataset, which can lead to varying results.
- The project uses a small subset of the GiantMIDI-Piano dataset, limiting the diversity of the training data.