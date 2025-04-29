## Multimodal RAG Architecture
- Text Extraction (Mistral OCR)
- Text Chunking (LangChain, chunking at 1024 tokens with step sizes of 512 tokens)
- Embedding and Indexing (Cohere Embed v3 - SOTA)
- Vector Index (Pinecone - vector data and metadata)
- Query Handling (Cohere Embed v3) 
- Semantic and Metadata Filtering + Retrieval (Pinecone)
- Prompt Engineering
- Answer Generation (OpenAI)

## Experiments
- Experiment 1: Identify content from a low resolution image without any text context - SUCCESS
- Experiment 2-1: Identify continuous content belonging to different pages - FAILURE
- Experiment 2-2: Identify continuous content belonging to different pages with OCR - SUCCESS

## Conclusion
- Multimodal models can successfully extract semantic meaning from images alone, even without accompanying text, demonstrating strong visual understanding.
- Understanding continuity across document pages improved significantly with layered chunking. 
- However, similarity search accuracy remained a challenge. Experiment 2-1 failed not because content was scattered across different chunks, but because the top-K matched chunks didn't contain the most relevant content. 


