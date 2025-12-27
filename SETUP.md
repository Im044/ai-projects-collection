# Setup and Installation Guide

## Prerequisites

- Python 3.9 or higher
- Git
- Virtual environment manager (venv or conda)
- API keys for external services (OpenAI, HuggingFace, etc.)

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Im044/ai-projects-collection.git
cd ai-projects-collection
```

### 2. Set Up Virtual Environment

```bash
# Using venv
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Or using conda
conda create -n ai-projects python=3.9
conda activate ai-projects
```

## Individual Project Setup

### AI Chatbot with LLM

```bash
cd ../ai-chatbot-llm
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env and add your API keys

# Run the chatbot
python main.py
```

**Environment Variables:**
```
OPENAI_API_KEY=your_key_here
HUGGINGFACE_API_KEY=your_key_here
DATABASE_URL=postgresql://user:password@localhost/db
REDIS_URL=redis://localhost:6379
```

### AI Image Generator

```bash
cd ../ai-image-generator
pip install -r requirements.txt

# Download models (first time)
python -m scripts.download_models

# Run the API
uvicorn main:app --reload
```

### N8N Automation Workflows

```bash
cd ../n8n-automation-workflows

# Using Docker (recommended)
docker compose up

# Access N8N at http://localhost:5678
```

### FastAPI ML API

```bash
cd ../fastapi-ml-api
pip install -r requirements.txt

# Run the API
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Access API docs at http://localhost:8000/docs
```

## Docker Setup

For containerized deployment:

```bash
# Build individual images
docker build -t ai-chatbot:latest ./ai-chatbot-llm
docker build -t ai-image-generator:latest ./ai-image-generator
docker build -t fastapi-ml:latest ./fastapi-ml-api

# Or use docker-compose for all services
cd ai-agents-docker-automation
docker compose up
```

## Configuration

### API Keys

Obtain API keys from:
- OpenAI: https://platform.openai.com/api-keys
- HuggingFace: https://huggingface.co/settings/tokens
- Google Cloud: https://console.cloud.google.com/

### Database Setup

```bash
# PostgreSQL
psql -U postgres -c "CREATE DATABASE ai_projects;"

# Redis
redis-server
```

## Verification

Verify your installation:

```bash
# Test AI Chatbot
curl http://localhost:8001/chat -X POST -H "Content-Type: application/json" -d '{"message": "Hello"}'

# Test Image Generator
curl http://localhost:8002/generate -X POST -H "Content-Type: application/json" -d '{"prompt": "A sunset"}'

# Test ML API
curl http://localhost:8003/health
```

## Troubleshooting

### ImportError
```bash
pip install --upgrade pip
pip install -r requirements.txt --force-reinstall
```

### Database Connection Error
```bash
# Check PostgreSQL is running
sudo service postgresql status

# Check Redis is running
redis-cli ping
```

### CUDA/GPU Issues
```bash
# Install CPU version of PyTorch
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

## Development

```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
pytest

# Run linting
flake8 .
black .
```

## Performance Optimization

- Use GPU acceleration when available
- Enable caching with Redis
- Use batch processing for large datasets
- Monitor resource usage with prometheus

## Next Steps

1. Review individual project documentation
2. Set up your API keys
3. Configure database connections
4. Run integration tests
5. Deploy using Docker

## Support

For issues, refer to individual project README files or open an issue on GitHub.
