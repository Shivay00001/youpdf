# YOU.PDF API Documentation

## Base URL
```
http://127.0.0.1:7860
```

## Authentication
Currently, the API does not require authentication. However, AI features require a valid HuggingFace API key.

---

## Core PDF Operations

### Merge PDFs
Combine multiple PDF files into a single PDF.

**Endpoint:** `POST /merge`

**Request:**
- Content-Type: `multipart/form-data`
- `files`: List of PDF files (multiple)

**Response:** `application/pdf`
- Merged PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/merge \
  -F "files=@file1.pdf" \
  -F "files=@file2.pdf" \
  -o merged.pdf
```

---

### Split PDF
Split a PDF by page ranges.

**Endpoint:** `POST /split`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `ranges`: Page ranges (e.g., "1-3,4-6,7-10")

**Response:** `application/json`
```json
{
  "job_id": "uuid-string"
}
```

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/split \
  -F "file=@document.pdf" \
  -F "ranges=1-3,4-6"
```

---

### Compress PDF
Reduce the file size of a PDF.

**Endpoint:** `POST /compress`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/pdf`
- Compressed PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/compress \
  -F "file=@large.pdf" \
  -o compressed.pdf
```

---

### Extract Pages
Extract specific pages from a PDF.

**Endpoint:** `POST /extract-pages`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `pages`: Page numbers (0-indexed, comma-separated, e.g., "0,2,5")

**Response:** `application/pdf`
- PDF with extracted pages

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/extract-pages \
  -F "file=@document.pdf" \
  -F "pages=0,2,5" \
  -o extracted.pdf
```

---

### Rotate Pages
Rotate PDF pages by specified angle.

**Endpoint:** `POST /rotate`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `angle`: Rotation angle (90, 180, 270)

**Response:** `application/pdf`
- Rotated PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/rotate \
  -F "file=@document.pdf" \
  -F "angle=90" \
  -o rotated.pdf
```

---

### Add Page Numbers
Add page numbers to a PDF.

**Endpoint:** `POST /page-numbers`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/pdf`
- PDF with page numbers

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/page-numbers \
  -F "file=@document.pdf" \
  -o numbered.pdf
```

---

### Reorder Pages
Reorder pages in a PDF.

**Endpoint:** `POST /reorder`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `order`: New page order (0-indexed, comma-separated, e.g., "2,0,1,3")

**Response:** `application/pdf`
- PDF with reordered pages

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/reorder \
  -F "file=@document.pdf" \
  -F "order=2,0,1,3" \
  -o reordered.pdf
```

---

### Remove Pages
Remove specific pages from a PDF.

**Endpoint:** `POST /remove-pages`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `pages`: Pages to remove (0-indexed, comma-separated)

**Response:** `application/pdf`
- PDF with pages removed

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/remove-pages \
  -F "file=@document.pdf" \
  -F "pages=1,3,5" \
  -o cleaned.pdf
```

---

### Resize Pages
Resize PDF pages by scale factor.

**Endpoint:** `POST /resize`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `scale`: Scale factor (e.g., 0.5 for 50%, 2.0 for 200%)

**Response:** `application/pdf`
- Resized PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/resize \
  -F "file=@document.pdf" \
  -F "scale=0.5" \
  -o resized.pdf
```

---

### Get Metadata
Get PDF metadata information.

**Endpoint:** `POST /metadata`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/json`
```json
{
  "/Title": "Document Title",
  "/Author": "Author Name",
  "/Subject": "Document Subject",
  "/Creator": "Application Name",
  "/Producer": "PDF Producer",
  "/CreationDate": "D:20240120000000Z"
}
```

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/metadata \
  -F "file=@document.pdf"
```

---

## Converters

### PDF to Images
Convert PDF pages to images.

**Endpoint:** `POST /pdf-to-images`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/json`
```json
{
  "images": ["/app/uploads/imgs_uuid/page_1.png", "/app/uploads/imgs_uuid/page_2.png"]
}
```

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/pdf-to-images \
  -F "file=@document.pdf"
```

---

### Images to PDF
Convert images to a single PDF.

**Endpoint:** `POST /images-to-pdf`

**Request:**
- Content-Type: `multipart/form-data`
- `files`: List of image files (multiple)

**Response:** `application/pdf`
- Generated PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/images-to-pdf \
  -F "files=@image1.jpg" \
  -F "files=@image2.png" \
  -o output.pdf
```

---

### Process PDF (Extract/Summarize/Translate)
General endpoint for various text processing operations.

**Endpoint:** `POST /process`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `action`: One of `extract`, `summarize`, `translate`, `keywords`, `qa`
- `lang`: Translation direction (for `translate` action): `en2hi`, `en2es`, etc.
- `question`: Question (for `qa` action)

**Response:** `text/plain`
- Processed text content

**Example (Extract):**
```bash
curl -X POST http://127.0.0.1:7860/process \
  -F "file=@document.pdf" \
  -F "action=extract" \
  -o text.txt
```

**Example (Summarize):**
```bash
curl -X POST http://127.0.0.1:7860/process \
  -F "file=@document.pdf" \
  -F "action=summarize" \
  -o summary.txt
```

**Example (Translate):**
```bash
curl -X POST http://127.0.0.1:7860/process \
  -F "file=@document.pdf" \
  -F "action=translate" \
  -F "lang=en2hi" \
  -o translated.txt
```

**Example (QA):**
```bash
curl -X POST http://127.0.0.1:7860/process \
  -F "file=@document.pdf" \
  -F "action=qa" \
  -F "question=What is this document about?" \
  -o answer.txt
```

---

### PDF to Word
Convert PDF to Word document.

**Endpoint:** `POST /pdf-to-word`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/vnd.openxmlformats-officedocument.wordprocessingml.document`
- Word document file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/pdf-to-word \
  -F "file=@document.pdf" \
  -o output.docx
```

---

### PDF to Excel
Extract tables from PDF to Excel.

**Endpoint:** `POST /pdf-to-excel`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
- Excel file with tables

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/pdf-to-excel \
  -F "file=@document.pdf" \
  -o output.xlsx
```

---

### HTML/Markdown to PDF
Convert HTML or Markdown content to PDF.

**Endpoint:** `POST /html-to-pdf`

**Request:**
- Content-Type: `multipart/form-data`
- `content`: HTML or Markdown text
- `type`: `html` or `markdown`

**Response:** `application/pdf`
- Generated PDF file

**Example (HTML):**
```bash
curl -X POST http://127.0.0.1:7860/html-to-pdf \
  -F "content=<h1>Hello World</h1>" \
  -F "type=html" \
  -o output.pdf
```

**Example (Markdown):**
```bash
curl -X POST http://127.0.0.1:7860/html-to-pdf \
  -F "content=# Hello World" \
  -F "type=markdown" \
  -o output.pdf
```

---

### Extract Tables
Extract tables from PDF as CSV.

**Endpoint:** `POST /extract-tables`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/zip`
- ZIP file containing CSV files for each table

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/extract-tables \
  -F "file=@document.pdf" \
  -o tables.zip
```

---

## AI & Text Processing

### OCR
Extract text from scanned PDFs using OCR.

**Endpoint:** `POST /ocr`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF or image file

**Response:** `text/plain`
- Extracted text content

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/ocr \
  -F "file=@scanned.pdf" \
  -o text.txt
```

---

## Security

### Protect PDF
Add password protection to PDF.

**Endpoint:** `POST /protect`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `password`: Password string

**Response:** `application/pdf`
- Password-protected PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/protect \
  -F "file=@document.pdf" \
  -F "password=secure123" \
  -o protected.pdf
```

---

### Unlock PDF
Remove password protection from PDF.

**Endpoint:** `POST /unlock`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `password`: Current password

**Response:** `application/pdf`
- Unlocked PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/unlock \
  -F "file=@protected.pdf" \
  -F "password=secure123" \
  -o unlocked.pdf
```

---

### Add Watermark
Add watermark to PDF.

**Endpoint:** `POST /watermark`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `watermark`: Watermark image or PDF file

**Response:** `application/pdf`
- Watermarked PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/watermark \
  -F "file=@document.pdf" \
  -F "watermark=@watermark.pdf" \
  -o watermarked.pdf
```

---

## Advanced Features

### Fill Form
Fill PDF form fields.

**Endpoint:** `POST /fill-form`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file with form fields
- `data`: JSON string of form data (e.g., '{"field1": "value1", "field2": "value2"}')

**Response:** `application/pdf`
- Filled PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/fill-form \
  -F "file=@form.pdf" \
  -F 'data={"name":"John Doe","email":"john@example.com"}' \
  -o filled.pdf
```

---

### Annotate
Add annotations to PDF.

**Endpoint:** `POST /annotate`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `annotations`: JSON string of annotations (e.g., '[{"page": 0, "x": 100, "y": 100, "text": "Note"}]')

**Response:** `application/pdf`
- Annotated PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/annotate \
  -F "file=@document.pdf" \
  -F 'annotations=[{"page":0,"x":100,"y":100,"text":"Important note"}]' \
  -o annotated.pdf
```

---

### Redact
Redact (black out) content from PDF.

**Endpoint:** `POST /redact`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file
- `redactions`: JSON string of redaction areas (e.g., '[{"page": 0, "x": 100, "y": 100, "width": 200, "height": 50}]')

**Response:** `application/pdf`
- Redacted PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/redact \
  -F "file=@document.pdf" \
  -F 'redactions=[{"page":0,"x":100,"y":100,"width":200,"height":50}]' \
  -o redacted.pdf
```

---

### Generate QR Code
Generate a QR code PDF.

**Endpoint:** `POST /generate-qr`

**Request:**
- Content-Type: `multipart/form-data`
- `text`: Text to encode in QR code
- `size`: QR code size in pixels (default: 200)

**Response:** `application/pdf`
- PDF with QR code

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/generate-qr \
  -F "text=https://example.com" \
  -F "size=300" \
  -o qrcode.pdf
```

---

### Generate Certificate
Generate a certificate PDF.

**Endpoint:** `POST /generate-certificate`

**Request:**
- Content-Type: `multipart/form-data`
- `data`: JSON string with certificate data (e.g., '{"name": "John Doe", "course": "Python", "date": "2024-01-20"}')

**Response:** `application/pdf`
- Generated certificate

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/generate-certificate \
  -F 'data={"name":"John Doe","course":"Python Programming","date":"2024-01-20"}' \
  -o certificate.pdf
```

---

### Compare PDFs
Compare two PDFs and find differences.

**Endpoint:** `POST /compare`

**Request:**
- Content-Type: `multipart/form-data`
- `file1`: First PDF file
- `file2`: Second PDF file

**Response:** `application/json`
```json
{
  "differences": [
    "Page count mismatch: 5 vs 4",
    "Page 1 content differs"
  ]
}
```

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/compare \
  -F "file1=@document1.pdf" \
  -F "file2=@document2.pdf"
```

---

### Repair PDF
Attempt to repair a corrupted PDF.

**Endpoint:** `POST /repair`

**Request:**
- Content-Type: `multipart/form-data`
- `file`: PDF file

**Response:** `application/pdf`
- Repaired PDF file

**Example:**
```bash
curl -X POST http://127.0.0.1:7860/repair \
  -F "file=@corrupted.pdf" \
  -o repaired.pdf
```

---

## Utility Endpoints

### Health Check
Check if the server is running.

**Endpoint:** `GET /health`

**Response:** `application/json`
```json
{
  "status": "ok",
  "uploads": 5
}
```

**Example:**
```bash
curl http://127.0.0.1:7860/health
```

---

### Job Status
Check the status of a background job.

**Endpoint:** `GET /job/{job_id}`

**Response:** `application/json`
```json
{
  "id": "uuid-string",
  "type": "split",
  "status": "done",
  "input_meta": "/app/uploads/file.pdf",
  "output_meta": "/app/uploads/split_uuid/split_1_2.pdf;/app/uploads/split_uuid/split_3_5.pdf",
  "created_at": 1705737600.0,
  "updated_at": 1705737605.0
}
```

**Example:**
```bash
curl http://127.0.0.1:7860/job/uuid-string
```

---

## Error Responses

All endpoints may return error responses:

```json
{
  "error": "Error message describing the issue"
}
```

Common HTTP status codes:
- `200`: Success
- `400`: Bad Request (invalid parameters)
- `404`: Not Found (job not found)
- `500`: Internal Server Error

---

## Rate Limiting

Rate limiting can be enabled via environment variables. When enabled, clients will receive a `429 Too Many Requests` response if they exceed the limit.

---

## Notes

1. **File Size Limits**: Default maximum file size is 100MB. Configure via `MAX_FILE_SIZE` environment variable.

2. **AI Features**: Summarize, translate, and QA endpoints require a valid HuggingFace API key.

3. **OCR**: Requires Tesseract to be installed on the server.

4. **Background Jobs**: Operations like `split` run asynchronously. Use the `/job/{job_id}` endpoint to check status.

5. **File Cleanup**: Uploaded files are stored in the `uploads` directory. Configure cleanup behavior via `KEEP_FILES` and `CLEANUP_INTERVAL` environment variables.
