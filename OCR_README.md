# OCR Framework Experiment

This repository contains experiments testing OCR (Optical Character Recognition) capabilities using the Mistral OCR API.

## PDF Collection Summary

The collection includes 5 PDF files with varying content types to test the OCR system's capabilities:

1. **empty_graph.pdf** - A PDF containing an empty graph or chart with minimal text content.
2. **screenshot_text_and_image.pdf** - A PDF with a screenshot containing both text and image elements.
3. **complex_graph.pdf** - A PDF with a complex graph/chart visualization.
4. **syllabus.pdf** - A PDF of a university course syllabus with structured text content.
5. **table.pdf** - A PDF containing tabular data.

These files were selected to test the OCR system's ability to handle different content types including plain text, tables, charts, and mixed content.

## OCR Experiment Results

The OCR experiments were conducted using the Mistral OCR API. The results show varying degrees of success depending on the content type:

### Text Extraction Results

1. **empty_graph.pdf**: The OCR system returned empty content, correctly identifying that there was no meaningful text to extract.

2. **screenshot_text_and_image.pdf**: Successfully extracted the text content:
   ```
   # Sample our Education Journals 
   
   >> Sign in here to start your access to the latest two volumes for 14 days
   ```

3. **complex_graph.pdf**: The OCR system identified and preserved the image content from the graph, returning it as a base64-encoded image. This suggests that while it may not extract text from complex visualizations, it can identify and preserve them as images.

4. **syllabus.pdf**: Successfully extracted extensive text content from the syllabus, including headings, bullet points, and structured information about the course. The formatting and hierarchical structure of the text was well-preserved.

5. **table.pdf**: Not fully demonstrated in the notebook output, but based on other examples, the OCR system likely attempted to extract tabular content.

### OCR Limitations and Challenges

1. When working with the OCR response data, there was an issue with accessing the response as an object versus as a dictionary. This was evidenced by the error:
   ```
   AttributeError: 'dict' object has no attribute 'pages'
   ```
   
   This indicates that the response format needs to be handled carefully, either by converting dictionary responses to the expected OCRResponse object type or by modifying code to handle both object and dictionary formats.

2. The system appears more successful with structured text content (like the syllabus) than with extracting text from charts and graphs.

3. For image-heavy content, the system correctly identifies and preserves images rather than trying to extract text from them.

Overall, the Mistral OCR API demonstrates good capabilities for text extraction from standard documents, with appropriate handling of images and non-text content. The API returns both the extracted text in markdown format as well as images encountered during processing, making it suitable for a variety of document analysis tasks.
