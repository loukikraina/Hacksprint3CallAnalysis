# Call Analysis System

## Overview
This is a Flask-based web application that performs speaker diarization on audio calls, specifically designed to separate and analyze conversations between customers and call center agents. The system uses voice activity detection (VAD) and machine learning techniques to segment and classify speakers in audio recordings.

## Features
- Audio file upload and processing
- Voice Activity Detection (VAD) using webrtcvad
- Speaker diarization using Gaussian Mixture Models (GMM)
- MFCC (Mel-frequency cepstral coefficients) feature extraction
- Spectral clustering for speaker separation
- Web interface for easy interaction

## Technical Stack
- Flask (Web Framework)
- librosa (Audio Processing)
- webrtcvad (Voice Activity Detection)
- scikit-learn (Machine Learning)
- NumPy (Numerical Computing)
- Wave (Audio File Handling)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/CallAnalysis.git
cd CallAnalysis
```

2. Install the required dependencies:
```bash
pip install flask webrtcvad librosa scikit-learn numpy wave
```

## Usage

1. Start the Flask server:
```bash
python app.py
```

2. Access the web interface at `http://localhost:5000`

3. Upload an audio file (WAV format) for analysis

4. The system will:
   - Segment the audio into chunks
   - Perform voice activity detection
   - Extract MFCC features
   - Create a Universal Background Model (UBM)
   - Perform MAP adaptation
   - Classify speakers using spectral clustering

## File Structure
```
.
├── app.py              # Main Flask application
├── templates/
│   └── index.html     # Web interface template
├── static/            # Static files
└── output/           # Generated audio chunks
```

## Technical Details

### Audio Processing Pipeline
1. **Voice Activity Detection (VAD)**
   - Uses webrtcvad for detecting speech segments
   - Filters out non-voiced audio frames
   - Segments audio into chunks

2. **Feature Extraction**
   - Extracts MFCC features (13 coefficients)
   - Computes delta and second-order delta features
   - Concatenates features for robust representation

3. **Speaker Diarization**
   - Creates a Universal Background Model (UBM) using GMM
   - Performs MAP adaptation for speaker modeling
   - Uses spectral clustering for final speaker separation

### Parameters
- Sampling Rate: 8000 Hz
- MFCC Features: 13 coefficients
- FFT Window: 0.032 seconds
- Hop Length: 0.010 seconds
- GMM Components: 16
- Number of Speakers: 2 (Customer and Agent)

## Notes
- The system assumes binary speaker classification (customer and agent)
- By default, it assumes the call center agent speaks first
- Audio files must be in WAV format with specific requirements:
  - Single channel (mono)
  - 16-bit depth
  - Sampling rate: 8000, 16000, 32000, or 48000 Hz
