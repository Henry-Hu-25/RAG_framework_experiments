# OCR Framework Experiment

OCR_testing.ipynb tests the Optical Character Recognition capabilities of the Mistral OCR, the SOTA OCR model, with an emphasis of their viability for PDF content extraction for RAG.  

## PDF Collection Description

The collection includes 5 PDF files with varying content types to test the OCR system's capabilities:

1. **empty_graph.pdf** - an empty graph or chart with minimal text content.
2. **screenshot_text_and_image.pdf** - screenshot containing both text and background image elements.
3. **complex_graph.pdf** - complex graph/chart visualizations.
4. **syllabus.pdf** - a university course syllabus with structured text content and tables.
5. **table.pdf** - tabular data.

## OCR Experiment Results

1. **empty_graph.pdf**: The OCR system returned empty content, correctly identifying that there was no meaningful text to extract. However, the model did not return the image content, making it problematic for RAG.


2. **screenshot_text_and_image.pdf**: Successfully extracted the text content in the image:
   ```
   # Sample our Education Journals 
   
   >> Sign in here to start your access to the latest two volumes for 14 days
   ```
   However, the model did not capture the key visual content, such as the logo in the upper right corner. This selective capture of content poses a challenge for RAG, as some user queries regarding the graphic components of the image may not be answered.

3. **complex_graph.pdf**: The OCR system successfully identified and preserved the graph content, returning it as a base64-encoded image, while not returning the text content within the graph. It seems like the model categorizes content as either text or image. 

4. **syllabus.pdf**: Successfully extracted extensive text content from the syllabus, including headings, bullet points, and structured information about the course. The formatting and hierarchical structure of the text was well-preserved.

5. **table.pdf**: The OCR system successfully extracted tabular content.

## Conclusion
### Pros
1. The Mistral OCR model is a powerful tool for extracting text. It does a good job of handling hiearchy, structure and tabular content. It also offers flexiblity in input format, including PDFs and PNGs. 
2. It's fast and inexpensive (1,000 pages for $1, as of 3/20/2025), making it ideal for text-based PDFs.
### Cons
1. Its performance is not as stable for images. It might skip graphics altogether, or opt to return text content within a graphic while ignoring key visual content. 
2. It categorizes content as either text or image, making it tricky to retain both the image and its text content for RAG embeddings. 

In conclusion, the Mistral OCR model is a powerful tool for text extraction for RAG, and works well with predominantly text-based documents. However, it requires help from other tools to work well with image-heavy content in a RAG setting. 

