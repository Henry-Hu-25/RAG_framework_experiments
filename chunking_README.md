# Chunking Experiments

This document describes the experiments conducted in `chunking.ipynb` document processing and chunking in a Retrieval-Augmented Generation (RAG) context.
Tools used: Chunkr API, LangChain 

## Testing Material

The experiments used a **syllabus.pdf** - A university course syllabus with structured text content and tables.
In past RAG attempts, we had challenges in chunking the syllabus, especially for content that belongs to the same section sematically but is separated by a page break. (see example Weeks 2-4:  SQL Language on page 2) 


## Chunkr API Experiments

### Experiment 1: Highest Performance Configuration

This experiment used a configuration optimized for the highest performance according to Chunkr documentation. Key settings included:

- High resolution enabled for all segments
- Layout analysis as the segmentation strategy
- LLM-based generation for all segment types (Captions, Footnotes, ListItems, Page, PageFooter, PageHeader, Pictures, SectionHeader, Text, Title)

### Experiment 2: Selective Content Processing

This experiment modified the configuration to:

- Ignore headers and footers
- Enable image summarization

### Experiment 3: Speed-Optimized Configuration

This experiment further adjusted the configuration for faster processing:

- Ignore headers and footers
- Enable image summarization
- Use faster output with heuristics (AUTO strategy)

## Chunkr API Conclusion
### Pros
1. **Element Recognition**: Chunkr API recognizes the different elements of a document, including text, images, captions, tables, and headers/footers, etc. making its output more flexible than a SOTA OCR model. 
2. **Visualization**: Users are able to view the chunks on the Chunkr UI. 

### Cons
1. **Chunking Performance**: We found some chunks to be too small and not semantically meaningful on their own (for example, a chunk contained only the headers). In addition, the challenge of chunking content that belongs to the same section semantically but is separated by a page break was not addressed. 
2. **Speed**: Chunkr API is relatively slow. Even with speed-optimized configuration, it takes 20 seconds to chunk a 9 page document. 
3. **Cost**: The cost of using Chunkr API is high. As of 3/25/2025, the starter plan sits at $50/month for 5000 pages ($0.01 per page). 

Overall, Chunkr API's chunking performance did not meet our use case requirements. 
