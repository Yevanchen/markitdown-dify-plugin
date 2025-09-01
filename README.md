# MarkItDown Dify Plugin

A powerful document conversion plugin for Dify based on MarkItDown 0.0.2a1, designed to convert various file formats into Markdown with high accuracy and reliability.

## Overview

This plugin serves as an excellent alternative to traditional document extraction nodes, offering robust file conversion capabilities within the Dify ecosystem. It leverages MarkItDown's plugin-based architecture to provide seamless conversion of multiple file formats to Markdown.

## Supported File Formats

- **PDF**
- **PowerPoint**
- **Word**
- **Excel**
- **Images**（EXIF metadata, OCR）
- **Audio**（EXIF metadata, speech transcription）
- **HTML**
- **Text-based formats**
- **ZIP archives**
- **YouTube URLs**
- **EPUBs**
- ...and more!


## Usage in Dify

### Parameters

The plugin accepts the following parameters in the Dify interface:

```yaml
files:
  type: files
  required: false
  description: "Array of files to be converted to Markdown"
```

### Response Format

The plugin provides three types of response formats for maximum flexibility:

1. **JSON Response** (New)
   ```json
   {
     "status": "success|error",
     "total_files": 2,
     "successful_conversions": 2,
     "results": [
       {
         "filename": "example1.pdf",
         "original_format": "pdf",
         "markdown_content": "# Content...",
         "status": "success"
       },
       {
         "filename": "example2.docx",
         "original_format": "docx",
         "markdown_content": "# Content...",
         "status": "success"
       }
     ]
   }
   ```

   Error response example:
   ```json
   {
     "filename": "failed.pdf",
     "original_format": "pdf",
     "error": "Error message",
     "status": "error"
   }
   ```

2. **Blob Response**
   - Returns raw markdown content as a blob
   - Includes mime_type metadata: "text/markdown"
   - Useful for direct content processing

3. **Text Response** (Legacy)
   - Single File:
   ```
   [Markdown content of the file]
   ```

   - Multiple Files:
   ```
   ==================================================
   File 1: example1.pdf
   ==================================================

   [Markdown content of file 1]

   ==================================================
   File 2: example2.docx
   ==================================================

   [Markdown content of file 2]
   ```

### Example Usage in Prompts

```
Please convert the attached files to Markdown format.
{@markitdown files=["document.pdf", "presentation.pptx"]}
```

## Features

- **Batch Processing**: Process multiple files in a single request
- **Clear File Separation**: When processing multiple files, content is clearly separated with headers and dividers
- **Format Preservation**: Maintains important formatting elements in the Markdown output
- **Error Handling**: Provides clear error messages for failed conversions
- **Automatic Cleanup**: Temporary files are automatically managed and cleaned up

## Best Practices

1. **File Size**: While there's no strict limit, it's recommended to keep individual files under 50MB for optimal performance
2. **Batch Processing**: You can process multiple files simultaneously, but consider limiting batches to 5-10 files
3. **Format Support**: When possible, use standard file formats from the supported list for best results
4. **Error Handling**: Always check for error messages in the response when processing critical documents

## Integration Example

Here's how to integrate the plugin into your Dify workflow:

1. **Document Analysis Flow**
   ```
   Input: {files} -> MarkItDown Plugin -> LLM Analysis
   ```

2. **Content Extraction Flow**
   ```
   Input: {files} -> MarkItDown Plugin -> Text Extraction -> Database Storage
   ```

## Advantages Over Traditional Document Extraction

1. **Format Support**: Broader range of supported file formats
2. **Metadata Preservation**: Retains important metadata from source files
3. **Structured Output**: Consistently formatted Markdown output
4. **Batch Processing**: Efficient handling of multiple files
5. **Clear Separation**: Better organization of multiple file contents
6. **Error Handling**: Comprehensive error reporting and handling

## Technical Notes

- Based on MarkItDown 0.0.2a1
- Maintains backward compatibility with 0.0.1a3
- Implements plugin-based architecture for extensibility
- Automatic temporary file management
- Thread-safe processing for concurrent requests

## Limitations

- Network connectivity required for some conversion operations
- Processing time may vary based on file size and complexity
- Some advanced formatting may be simplified in the Markdown output

## Support

For issues and feature requests, please create an issue in the repository or contact the plugin maintainer.

---

*Note: This plugin is based on MarkItDown 0.0.2a1 and may receive updates as the base library evolves to its first non-alpha release.*

## Response Types Use Cases

1. **JSON Response**
   - Workflow automation and data processing
   - Status tracking and error handling
   - Structured data extraction
   - API integrations

2. **Blob Response**
   - Direct content processing
   - Raw markdown handling
   - Stream processing
   - File system operations

3. **Text Response**
   - Human readable output
   - Legacy system compatibility
   - Simple content viewing
   - Direct LLM input



contact：evanchen@dify.ai