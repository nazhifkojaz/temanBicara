# 🗣️ Teman Bicara

**A conversational AI companion for casual, day-to-day voice conversations**

Teman Bicara (Indonesian for "conversation partner") is an Conversational AI system that listens and responds to users like a human friend who are there to chat about casual topics, day-to-day life, or just to pass the time. It focuses on being the 'good listener' and engaging in light-hearted conversations and small talk, or even just being there to listen when you need to vent instead of providing factual information or task-oriented assistance.

## 🏗️ Architecture

```
User Speech    →   ASR  →   LLM  →   TTS  →   AI Voice Response
             (opt) ↓       ↑
               Conversation History
```

### Components

1. **ASR (Automatic Speech Recognition)**
   - The part that converts user speech to text.

2. **LLM (Large Language Model)**
   - Responsible for generating responses based on the transcribed text and conversation history.

3. **TTS (Text-to-Speech)**
   - Converts the LLM-generated response text back into speech.

4. **Backend**
   - API to handle communication between frontend and AI components
   - Manages conversation state and history

5. **Frontend**
   - User interface for voice interaction with the AI companion

## 🚀 Quick Start

### Prerequisites

- Python 3.11
- [uv](https://docs.astral.sh/uv/) (Fast Python package manager)
- CUDA-compatible GPU (optional, for faster inference)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd temanBicara
   ```

2. **Initialize virtual environment**
   ```bash
   # uv will create .venv and install dependencies
   uv sync
   ```

3. **Activate virtual environment**
   ```bash
   source .venv/bin/activate  # Linux/Mac
   # or
   .venv\Scripts\activate  # Windows
   ```

4. **Install PyTorch with CUDA support** (recommended for GPU)
   ```bash
   # For CUDA 12.6
   pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu126

   # For CPU-only (if no GPU)
   pip install torch torchaudio --index-url https://download.pytorch.org/whl/cpu
   ```

   > **Note:** PyTorch with CUDA is installed via pip due to dependency resolver compatibility. All other packages are managed by uv.

5. **Verify installation**
   ```bash
   python -c "import torch; print(f'PyTorch: {torch.__version__}'); print(f'CUDA available: {torch.cuda.is_available()}')"
   ```

### Development Setup

1. **Create data directory structure**
   ```bash
   mkdir -p data/{raw,processed,samples}
   mkdir -p data/raw/{train,test,validation}
   mkdir -p notebooks
   ```

2. **Start Jupyter for exploration**
   ```bash
   jupyter notebook notebooks/
   ```

### Project Structure

```
teman-bicara/
├── src/teman_bicara/    # Main package
│   ├── asr/             # ASR module (Phase 1)
│   ├── llm/             # LLM integration (Phase 2)
│   ├── tts/             # Text-to-speech (Phase 2)
│   ├── backend/         # API backend (Phase 3)
│   └── utils/           # Shared utilities
├── notebooks/           # Jupyter notebooks for exploration
├── tests/               # Unit tests
├── data/                # Data directory (gitignored)
│   ├── raw/             # Original audio files (private)
│   ├── processed/       # Preprocessed data
│   └── samples/         # Small sample files (can be in git)
└── pyproject.toml       # Project configuration
```

### Using Public Datasets

For ASR exploration without private data:

```python
from datasets import load_dataset

# Indonesian speech from Mozilla Common Voice
dataset = load_dataset("mozilla-foundation/common_voice_11_0", "id", split="train[:100]")

# Or Google's FLEURS dataset
dataset = load_dataset("google/fleurs", "id_id", split="train[:100]")
```


## 📊 Current Status

- [x] ASR exploration
- [ ] ASR module implementation
- [ ] LLM integration
- [ ] TTS module
- [ ] Pipeline
- [ ] Backend API
- [ ] Frontend UI
- [ ] Deployment

## 🛣️ Roadmap

### Phase 1: ASR (Current)
- Understanding ASR processes
- Experimenting with available ASR models
- Selecting suitable ASR model
- (if needed) Fine-tuning ASR model

### Phase 2: LLM & TTS
- Integrate LLM for conversation
- Implement TTS for voice responses
- Build end-to-end pipeline

### Phase 2.1: Conversation Memory
- Implement memory management

### Phase 3: Prototyping and Deployment
- Develop backend API
- Create web frontend
- Deploy MVP

### Phase 4: Enhancement
- Improve latency and performance
- Multi-language support
- Mobile app