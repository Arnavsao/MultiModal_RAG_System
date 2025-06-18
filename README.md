# Multimodal RAG System

This project implements a **Multimodal Retrieval-Augmented Generation (RAG) System** that processes video content to extract and index images, audio, and transcribed text, enabling advanced question answering and retrieval over multiple data modalities.

---

## Features

- **Video Downloading:** Fetches videos from YouTube using a URL.
- **Frame Extraction:** Extracts images from video frames at a specified interval.
- **Audio Extraction & Transcription:** Converts video audio to text using speech recognition and Whisper.
- **Multimodal Indexing:** Stores and indexes both text and images using LanceDB and LlamaIndex.
- **Retrieval & QA:** Answers user queries by retrieving relevant images and text from the indexed data.
- **Visualization:** Displays retrieved images and text in response to user queries.

---

## Installation

Install all required dependencies using the following commands:

pip install llama-index-vector-stores-lancedb
pip install llama-index-multi-modal-llms-openai
pip install llama-index-embeddings-clip
pip install git+https://github.com/openai/CLIP.git
pip install llama-index-readers-file
pip install llama_index
pip install -U openai-whisper
pip install lancedb moviepy pytube pydub SpeechRecognition ffmpeg-python soundfile torch torchvision matplotlib scikit-image ftfy regex tqdm


---

## Usage

1. **Set Up API Keys:**
   - Store your OpenAI API key in the environment or use Colab's `userdata`.

2. **Download Video:**
   - Set the `video_url` variable and download the video using the provided function.

3. **Extract Data:**
   - Extract frames, audio, and transcribe audio to text.

4. **Index Data:**
   - Use LanceDB and LlamaIndex to store and index the extracted images and text.

5. **Query the System:**
   - Use the retrieval engine to answer questions about the video content, retrieving both images and text as context.

6. **Visualize Results:**
   - Display retrieved images and text using the provided plotting functions.

---

## Project Structure

| File/Folder         | Description                                      |
|---------------------|--------------------------------------------------|
| `mixed_data/`       | Stores extracted images, audio, and text files   |
| `video_data/`       | Stores downloaded video files                    |
| `output_text.txt`   | Transcribed text from video audio                |
| `main.py`           | Main script with all processing and retrieval    |
| `README.md`         | Project documentation                            |

---

## Example Workflow

Download video and extract metadata
metadata_vid = download_video(video_url, output_video_path)

Extract frames and audio
video_to_images(filepath, output_folder)
video_to_audio(filepath, output_audio_path)

Transcribe audio to text
text_data = audio_to_text(output_audio_path)

Save text and clean up
with open(output_folder + "output_text.txt", "w") as file:
file.write(text_data)
os.remove(output_audio_path)

Index and retrieve
documents = SimpleDirectoryReader(output_folder).load_data()
index = MultiModalVectorStoreIndex.from_documents(documents, storage_context=storage_context)
retriever_engine = index.as_retriever(similarity_top_k=1, image_similarity_top_k=5)
img, text = retrieve(retriever_engine, query)
plot_images(img)



---

## Requirements

- Python 3.8+
- OpenAI API Key
- All packages listed in the installation section

---

## Acknowledgements

- [LlamaIndex](https://github.com/jerryjliu/llama_index)
- [LanceDB](https://github.com/lancedb/lancedb)
- [OpenAI Whisper](https://github.com/openai/whisper)
- [MoviePy](https://zulko.github.io/moviepy/)
- [PyTube](https://github.com/pytube/pytube)

---

## License

This project is for educational and research purposes only.

---

## Contact

For questions or contributions, please open an issue or submit a pull request.
To use:
Copy the above content and save it as a file named README.md in your project directory.
Let me know if you need a Python script, requirements file, or anything else!
