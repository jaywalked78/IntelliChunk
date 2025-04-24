# IntelliChunk

**Smart Semantic Processing for RAG Systems**

Adaptive content processor that intelligently chunks diverse data sources—screen recordings, articles, and structured documents—based on semantic meaning. Seamlessly integrates with Airtable, n8n workflows, and image servers to prepare optimized content for retrieval and AI-powered generation.

## System Architecture

IntelliChunk consists of three fully operational, independent tools that work together:

### 1. OCR Processing Tool

A comprehensive OCR system that:
- Processes screen recording frames to extract text
- Integrates directly with Airtable for storage and organization
- Works with n8n for automation workflows
- Handles batch processing of frame images

### 2. Semantic Chunker

A specialized text processing system that:
- Divides extracted text into semantic chunks for optimal retrieval
- Organizes chunks with proper metadata and references
- Prepares data for embedding generation
- Sends structured data via webhooks to other systems

### 3. Integration with Image Server

Seamlessly works with [Lightweight File Hosting Server](https://github.com/jaywalked78/Lightweight-File-Hosting-Server) to:
- Host frame images via HTTP endpoints
- Generate accessible URLs for frames
- Provide a consistent interface for image retrieval
- Enable visual reference alongside text content

These three components can operate independently but are designed to work together through the integration scripts provided in this repository.

## Overview

IntelliChunk processes diverse content to:
1. Extract meaningful text (using OCR for screen recordings)
2. Adaptively chunk text based on semantic meaning and content structure
3. Generate image URLs for visual content
4. Combine text chunks and image URLs into a unified dataset
5. Send processed data via webhooks to n8n or other systems

## Components

### 1. Text Chunker

The text chunker processes various content formats:
- Extracts meaningful text from raw data
- Intelligently chunks text based on content type
- Organizes chunks with metadata
- Sends processed data via webhook

### 2. Image Server Integration

Integrated with [Lightweight File Hosting Server](https://github.com/jaywalked78/Lightweight-File-Hosting-Server) to:
- Host frame images via HTTP
- Generate accessible URLs for each frame
- Combine image URLs with text data

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/jaywalked78/IntelliChunk.git
   cd IntelliChunk
   ```

2. Create a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure environment:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

5. Setup Image Server (optional but recommended):
   ```bash
   git clone https://github.com/jaywalked78/Lightweight-File-Hosting-Server.git ../Lightweight-File-Hosting-Server
   ```

## Usage

### Basic Usage

Process a folder of screen recording frames:

```bash
./run_processor_with_image_server.sh folder_name [test]
```

Arguments:
- `folder_name`: Name of the folder containing frame images
- `test` (optional): Run in test mode (doesn't send to webhook)

### Advanced Usage

Process a specific JSON file:

```bash
./run_processor_with_image_server.sh folder_name path/to/file.json
```

### n8n Integration

For automated workflows with n8n, see [n8n_integration.md](./n8n_integration.md).

## Input/Output

### Input

- JSON files containing OCR data from screen recording frames
- Text documents of various formats (articles, posts, etc.)
- Structured data with semantic content

### Output

1. **Text Processing Output**:
   - Chunked text data optimized for RAG systems
   - Webhook payload with structured content
   - Metadata for each chunk

2. **Image Server Output** (when applicable):
   - JSON file with image URLs
   - Format: `folder_name_YYYYMMDD_HHMMSS.json` (timestamped)
   - Symlink: `folder_name_latest.json` for easy access

## Configuration

Edit `.env` file to configure:
- Webhook URL for sending processed data
- Base directory for content
- Test mode settings
- Image server connection details

## Scripts

- `run_processor_with_image_server.sh`: Main script for integrated processing
- `process_json_files_v5.py`: Text processing and chunking
- `main.py`: API server for receiving processing requests

## Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add some amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a pull request

## License

This project is proprietary and not licensed for public use without explicit permission from the repository owner.

## Changelog

See [CHANGELOG.md](./CHANGELOG.md) for version history and updates. 