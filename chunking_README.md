# Chunking Experiments

This document describes the experiments conducted in `chunking.ipynb` that test different configuration settings of the Chunkr API for document processing and chunking in a Retrieval-Augmented Generation (RAG) context.

## Testing Material

The experiments used a collection of 5 PDF files with varying content types to test the chunking capabilities:

1. **empty_graph.pdf** - An empty graph or chart with minimal text content.
2. **screenshot_text_and_image.pdf** - Screenshot containing both text and background image elements.
3. **complex_graph.pdf** - Complex graph/chart visualizations.
4. **syllabus.pdf** - A university course syllabus with structured text content and tables.
5. **table.pdf** - Tabular data.

These files represent different document types and formats commonly encountered in RAG applications, allowing for comprehensive testing of the chunking system's capabilities with diverse content.

## Experiments

### Experiment 1: Highest Performance Configuration

This experiment used a configuration optimized for the highest performance according to Chunkr documentation. Key settings included:

- High resolution enabled for all segments
- Layout analysis as the segmentation strategy
- LLM-based generation for all segment types (Captions, Footnotes, ListItems, Page, PageFooter, PageHeader, Pictures, SectionHeader, Text, Title)

This approach aims for maximum accuracy and quality in document processing but might be slower and more resource-intensive.

### Experiment 2: Selective Content Processing

This experiment modified the configuration to:

- Ignore headers and footers
- Enable image summarization

This configuration focuses on the main content of documents while providing summaries of images, potentially offering a better balance between processing speed and content quality.

### Experiment 3: Performance-Optimized Configuration

This experiment further adjusted the configuration for faster processing:

- Ignore headers and footers
- Enable image summarization
- Use faster output with heuristics (AUTO strategy)

This configuration prioritizes processing speed by using heuristic-based approaches rather than full LLM processing for certain content types, potentially trading some quality for improved performance.

## Applications

These experiments help understand the tradeoffs between different chunking configurations in a RAG system, particularly how different settings affect:

- Content extraction quality
- Processing speed
- Handling of different document elements (text, images, tables, etc.)
- Resource utilization

The findings can guide the selection of appropriate chunking strategies based on specific use case requirements, document types, and resource constraints.
