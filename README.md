# IntelliChunk

**Smart Semantic Processing for RAG Systems**

Adaptive content processor that intelligently chunks diverse data sources based on semantic meaning. Currently optimized for processing screen recording frame metadata, IntelliChunk is being expanded to handle articles, structured documents, social media content, and more. It seamlessly integrates with n8n workflows and image servers to prepare optimized content for retrieval and AI-powered generation.

## System Architecture

IntelliChunk focuses on semantic chunking and integration. For screen recording processing, it's designed to work alongside a dedicated OCR system:

### 1. Semantic Chunker (This Repository)

A specialized text processing system that:
- Takes input text (currently optimized for frame metadata)
- Divides text into semantic chunks for optimal retrieval
- Organizes chunks with proper metadata and references
- Prepares data for embedding generation
- Sends structured data via webhooks to other systems

### 2. Integration with Image Server (This Repository)

Seamlessly works with [Lightweight File Hosting Server](https://github.com/jaywalked78/Lightweight-File-Hosting-Server) to:
- Host visual content (like screen frames) via HTTP endpoints
- Generate accessible URLs for content
- Provide a consistent interface for media retrieval
- Enable visual reference alongside text content

### 3. OCR Processing Integration (External)

IntelliChunk integrates with external OCR systems for processing screen recordings. For a recommended OCR solution that works well with IntelliChunk, see [**Placeholder for OCR Repo Link - e.g., ScreenScraperOCR**].

## Overview

IntelliChunk processes diverse content to:
1. Receive input data (currently focused on frame metadata from screen recordings via JSON)
2. Adaptively chunk text based on semantic meaning and content structure
3. Generate image URLs for associated visual content (if applicable)
4. Combine text chunks and image URLs into a unified dataset
5. Send processed data via webhooks to n8n or other systems

*Future versions will directly handle various text formats like articles, blog posts, and social media feeds.*

## Components

### 1. Text Chunker

The text chunker processes input data:
- Extracts meaningful text from raw data (e.g., frame metadata JSON)
- Intelligently chunks text based on content type (expanding capabilities)
- Organizes chunks with metadata
- Sends processed data via webhook

### 2. Image Server Integration

Integrated with [Lightweight File Hosting Server](https://github.com/jaywalked78/Lightweight-File-Hosting-Server) to:
- Host image content via HTTP
- Generate accessible URLs for each image
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

6. Setup OCR Processor (Optional - for screen recordings):
   ```bash
   # Clone and set up the external OCR repository (e.g., ScreenScraperOCR)
   # Follow instructions in that repository
   ```

## Usage

### Basic Usage

Process a folder of screen recording frame metadata:

```bash
./run_processor_with_image_server.sh folder_name [test]
```

Arguments:
- `folder_name`: Name of the folder containing frame metadata JSON files
- `test` (optional): Run in test mode (doesn't send to webhook)

*Support for other content types coming soon.*

### Advanced Usage

Process a specific JSON file containing frame metadata:

```bash
./run_processor_with_image_server.sh folder_name path/to/file.json
```

### n8n Integration

For automated workflows with n8n, see [n8n_integration.md](./n8n_integration.md).

## Input/Output

### Input (Current)

- JSON files containing screen recording frame metadata (output from an OCR process)

### Input (Planned)

- Text documents (articles, posts, etc.)
- Structured data feeds
- Social media content

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
- Base directory for input content
- Test mode settings
- Image server connection details

## Scripts

- `run_processor_with_image_server.sh`: Main script for integrated processing (currently frame-focused)
- `process_json_files_v5.py`: Text processing and chunking logic
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