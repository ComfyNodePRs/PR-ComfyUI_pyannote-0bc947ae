# ComfyUI Custom Nodes: Speaker Diarization and Whisper Integration

## Overview

This repository provides custom nodes for **ComfyUI** designed to process audio files, performing speaker diarization and integrating speaker data into whisper-transcribed segments. These nodes utilize the **PyAnnote** library for speaker identification and **pandas** for efficient data handling.

---

## Custom Nodes

### 1. **Speaker Diarization Node**

**Description:**  
Performs speaker diarization on an input audio file, identifying and segmenting speech by different speakers.

- **Category:** Audio Processing
- **Node Name:** `Speaker Diarization`

**Inputs:**
- **audio:** (`AUDIO`)  
  The audio data to process.
- **hf_token:** (`STRING`)  
  A Hugging Face authentication token for accessing the PyAnnote model.

**Outputs:**
- **speaker_segments:** (`List[Dict]`)  
  A list of dictionaries containing speaker segments with `start`, `end`, and `speaker` information.

**Usage Example:**  
After connecting an audio input, this node identifies where each speaker starts and ends in the audio file.

---

### 2. **Whisper Segments to Speaker Node**

**Description:**  
Adds speaker labels to segments generated by a Whisper speech-to-text model, aligning them based on time overlaps with diarized segments.

- **Category:** Audio Processing
- **Node Name:** `Whisper Segments to Speaker`

**Inputs:**
- **whisper_segments:** (`whisper_alignment`)  
  Transcription segments generated by Whisper, including `start` and `end` times.
- **speaker_segments:** (`speaker_segments`)  
  Output from the `Speaker Diarization Node`, providing time-aligned speaker information.

**Outputs:**
- **segments_alignment:** (`whisper_alignment`)  
  The original Whisper segments enriched with speaker labels.

**Usage Example:**  
Connect the output of the `Speaker Diarization Node` and Whisper-transcribed segments. This node will align speaker data, allowing for a detailed transcription with speaker differentiation.

---

## Dependencies

Ensure the following libraries are installed:
- **PyAnnote Audio:** For speaker diarization.
- **pandas:** For data manipulation.
- **numpy:** For numeric operations.
- **torchaudio:** For audio processing.
- **pydub:** For audio format handling.

Install dependencies using:
```bash
pip install pyannote.audio pandas numpy torchaudio pydub
```

---

## Integration with ComfyUI

1. **Place Node Files:**  
   Add the provided Python file to the custom nodes directory in your ComfyUI setup.

2. **Register the Nodes:**  
   ComfyUI automatically detects nodes from the `NODE_CLASS_MAPPINGS`. Ensure the structure includes:
   ```python
   NODE_CLASS_MAPPINGS = {
       "Speaker Diarization": SpeakerDiarizationNode,
       "Whisper Segments to Speaker": WhisperDiarizationNode
   }
   ```

3. **Node Interface:**  
   In the ComfyUI interface, locate the nodes under the **Audio Processing** category. Connect them as needed to process audio inputs and transcriptions.

---

## Configuration

### Hugging Face Token
To access the PyAnnote model, you need a Hugging Face token. Sign up or log in to Hugging Face and generate an access token from your account settings.

---

## License

This project is open-source. Refer to the LICENSE file for details.

---

## Contact

For issues or feature requests, please submit them via the repository's issue tracker.

--- 

Happy audio processing! 🎧
