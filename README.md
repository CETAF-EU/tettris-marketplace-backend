# tettris-marketplace-backend

A Python FastAPI backend service for the CETAF Marketplace platform. This application handles researcher authentication via ORCID, manages profiles pictures files uploads, and serves static content for the marketplace.

## Purpose

This backend API powers the CETAF Marketplace (`https://marketplace.cetaf.org`), providing essential services for:
- Researcher identity verification through ORCID integration
- Secure file and image upload handling
- Static file serving for marketplace content
- Token-based API authentication

## Project Structure

### Core Files

**main.py** - FastAPI application containing:
- Static file serving for uploads (`/uploads` directory)
- ORCID authentication integration
- Secure file upload endpoints with token verification
- File size restrictions (2MB limit for profile pictures)
- CORS middleware configured for marketplace domains

**requirements.txt** - Python dependencies:
- `fastapi` - Modern web framework for building APIs
- `uvicorn[standard]` - ASGI server for running the application
- `httpx` - HTTP client for making requests to ORCID and other APIs
- `python-dotenv` - Environment variable management
- `python-multipart` - File upload handling

**dockerfile** - Container configuration:
- Based on Python 3.11-slim
- Installs dependencies and application code
- Configures environment variables (ORCID credentials, API tokens)
- Creates upload directory
- Runs FastAPI server on port 8000

**README.md** - Project documentation (this file)

## Setup

### Environment Variables

The application requires the following environment variables (set in `.env` file or Docker build args):
- `VITE_ORCID_CLIENT_ID` - ORCID OAuth client ID
- `VITE_ORCID_CLIENT_SECRET` - ORCID OAuth client secret
- `VITE_ORCID_REDIRECT_URI` - ORCID redirect URI
- `VITE_IMAGE_API` - API token for image service authentication

### Running Locally

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Create `.env` file with required environment variables

3. Run the server:
   ```bash
   uvicorn main:app --reload
   ```

### Running with Docker

Build and run the container with environment variables:
```bash
docker build \
  --build-arg VITE_ORCID_CLIENT_ID=your_client_id \
  --build-arg VITE_ORCID_CLIENT_SECRET=your_client_secret \
  --build-arg VITE_ORCID_REDIRECT_URI=your_redirect_uri \
  --build-arg VITE_IMAGE_API=your_api_token \
  -t tettris-marketplace-backend .

docker run -p 8000:8000 tettris-marketplace-backend
```

The API will be available at `http://localhost:8000`

