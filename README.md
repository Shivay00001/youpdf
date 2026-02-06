# YOU.PDF - Complete PDF Processing Solution

A fully functional PDF processing platform with web and mobile interfaces, offering 50+ features for document manipulation, AI-powered analysis, and security.

## Features

### Core PDF Operations
- Merge PDFs - Combine multiple files
- Split PDF - Extract page ranges
- Compress PDF - Reduce file size
- Extract Pages - Remove specific pages
- Rotate Pages - Adjust orientation
- Add Page Numbers - Number documents
- Reorder Pages - Rearrange pages
- Remove Pages - Delete unwanted pages
- Resize PDF - Scale/crop pages
- Edit Metadata - View/modify PDF info

### Converters
- PDF to Images - Convert pages to PNG/JPG
- Images to PDF - Create PDF from images
- PDF to Text - Extract text content
- PDF to Markdown - Convert to MD format
- HTML to PDF - Convert HTML content
- PDF to Word - Export to DOCX
- PDF to Excel - Extract tables to XLSX
- Extract Tables - Get table data as CSV

### AI & Text Processing
- Summarize - AI-powered document summaries
- Translate - Multi-language translation
- Extract Keywords - Identify key topics
- Chat with PDF - Q&A with document content
- OCR Scan - Extract text from images
- Generate Quiz - Create MCQs from content

### Security
- Protect PDF - Add password encryption
- Unlock PDF - Remove password protection
- Add Watermark - Overlay text/image
- Sign PDF - Digital signatures
- Redact Text - Black out sensitive info

### Advanced Features
- Fill Forms - Auto-fill PDF forms
- Annotate - Add comments and notes
- Compare PDFs - Find differences
- Repair PDF - Fix corrupted files
- Generate Certificates - Create professional certificates
- Generate QR Codes - Create QR code PDFs

## Installation

### Backend Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd youpdf
```

2. Create and activate virtual environment:
```bash
python -m venv .venv
# On Windows
.venv\Scripts\activate
# On Mac/Linux
source .venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Start the backend server:
```bash
python server.py
```

Or use the batch file (Windows):
```bash
start_backend.bat
```

The server will start on `http://127.0.0.1:7860`

### Web Interface

1. Open your browser and navigate to:
```
http://127.0.0.1:7860
```

2. Select a feature from the sidebar
3. Upload your files
4. Click "Process" to execute

### Mobile App (Flutter)

1. Navigate to the mobile_app directory:
```bash
cd mobile_app
```

2. Install Flutter dependencies:
```bash
flutter pub get
```

3. Run the app:
```bash
flutter run
```

## Configuration

### AI Features

For AI features (summarize, translate, QA), set your HuggingFace API key in `ai_utils.py`:
```python
# Replace with your actual API key
HF_API_KEY = "your_huggingface_api_key_here"
```

Or set it as an environment variable:
```bash
export HF_API_KEY="your_key_here"
```

### OCR

For OCR functionality, ensure Tesseract is installed:
- **Windows**: Download from [GitHub](https://github.com/UB-Mannheim/tesseract/wiki)
- **Mac**: `brew install tesseract`
- **Linux**: `sudo apt install tesseract-ocr`

### Server Configuration

Modify these in `server.py`:
```python
# Change port if needed
HOST = "0.0.0.0"
PORT = 7860

# Change upload directory
UPLOAD_DIR = "uploads"
```

## API Endpoints

### Core Operations
- `POST /merge` - Merge PDFs
- `POST /split` - Split PDF by ranges
- `POST /compress` - Compress PDF
- `POST /extract-pages` - Extract pages
- `POST /rotate` - Rotate pages
- `POST /page-numbers` - Add page numbers
- `POST /reorder` - Reorder pages
- `POST /remove-pages` - Remove pages
- `POST /resize` - Resize pages
- `POST /metadata` - Get metadata

### Converters
- `POST /pdf-to-images` - PDF to images
- `POST /images-to-pdf` - Images to PDF
- `POST /process?action=extract` - PDF to text
- `POST /pdf-to-word` - PDF to Word
- `POST /pdf-to-excel` - PDF to Excel
- `POST /html-to-pdf` - HTML/Markdown to PDF
- `POST /extract-tables` - Extract tables to CSV

### AI & Processing
- `POST /process?action=summarize` - Summarize PDF
- `POST /process?action=translate` - Translate PDF
- `POST /process?action=keywords` - Extract keywords
- `POST /process?action=qa` - QA with PDF
- `POST /ocr` - OCR processing

### Security
- `POST /protect` - Password protect PDF
- `POST /unlock` - Remove password
- `POST /watermark` - Add watermark

### Advanced
- `POST /fill-form` - Fill PDF forms
- `POST /annotate` - Add annotations
- `POST /redact` - Redact content
- `POST /generate-qr` - Generate QR code PDF
- `POST /generate-certificate` - Generate certificate
- `POST /compare` - Compare PDFs
- `POST /repair` - Repair PDF

## Project Structure

```
youpdf/
├── server.py              # FastAPI backend server
├── pdf_utils.py           # PDF processing utilities
├── ai_utils.py            # AI processing utilities
├── requirements.txt        # Python dependencies
├── start_backend.bat      # Windows startup script
├── templates/
│   └── index.html         # Web UI template
├── static/                # Static assets
├── mobile_app/
│   ├── lib/
│   │   ├── screens/       # Flutter screens
│   │   ├── services/      # API and local services
│   │   ├── data/          # Feature data
│   │   └── theme/         # App theme
│   └── pubspec.yaml       # Flutter dependencies
└── README.md              # This file
```

## Usage Examples

### Merge PDFs via API
```bash
curl -X POST http://127.0.0.1:7860/merge \
  -F "files=@file1.pdf" \
  -F "files=@file2.pdf" \
  -o merged.pdf
```

### Compress PDF via API
```bash
curl -X POST http://127.0.0.1:7860/compress \
  -F "file=@large.pdf" \
  -o compressed.pdf
```

### Summarize PDF via API
```bash
curl -X POST http://127.0.0.1:7860/process \
  -F "file=@document.pdf" \
  -F "action=summarize" \
  -o summary.txt
```

## Troubleshooting

### Port Already in Use
If port 7860 is busy, change it in `server.py`:
```python
if __name__ == "__main__":
    uvicorn.run("server:app", host="0.0.0.0", port=8000, reload=True)
```

### OCR Not Working
Ensure Tesseract is properly installed and in your PATH:
```bash
tesseract --version
```

### AI Features Not Working
Check your HuggingFace API key is set correctly and you have sufficient credits.

### Mobile App Connection Issues
Ensure the backend is running and the API base URL in `api_service.dart` matches:
```dart
static const String baseUrl = 'http://127.0.0.1:7860';
```

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues.

## License

This project is provided as-is for educational and commercial use.

## Support

For issues and questions, please open an issue on the repository.

## Acknowledgments

- FastAPI - Python web framework
- PyMuPDF - PDF processing
- ReportLab - PDF generation
- Flutter - Mobile framework
- Tailwind CSS - Web styling
- HuggingFace - AI models
