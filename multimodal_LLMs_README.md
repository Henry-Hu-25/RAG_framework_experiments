## PDF Collection Description

The collection includes 6 PDF files with varying content types to test the OCR system's capabilities:

1. **empty_graph.pdf** - an empty graph or chart with minimal text content.
2. **screenshot_text_and_image.pdf** - screenshot containing both text and background image elements.
3. **complex_graph.pdf** - complex graph/chart visualizations.
4. **syllabus.pdf** - a university course syllabus with structured text content and tables.
5. **table.pdf** - tabular data.
6. **apple_10k_long_document.pdf** - Apple's annual report with a mix of text, images, and tables.

## Long Context Window Experiment Results (Gemini and Claude, 4/28/2025)

1. **empty_graph.pdf**: All models correctly decsribed the image content (type of graph and porportions of the graph).

2. **screenshot_text_and_image.pdf**: All models successfully extracted the text content in the image and captured the key visual content, such as the logo in the upper right corner.

3. **complex_graph.pdf**: All models successfully understood and returned the text content within the graph.

4. **syllabus.pdf**: All models successfully retreived continuous information spread across different pages.

5. **table.pdf**: All models successfully extracted tabular content.

6. **apple_10k_long_document.pdf**: Google Gemini family of models successfully understood the context and returned the relevant information. The Gemini family also returned output in JSON format and provided page number for reference, when prompted.

## Cross Model Comparion (Gemini vs. Claude, 4/28/2025)

**Pricing and Context Window**: 

| Model                | Input Cost (per 1M tokens) | Output Cost (per 1M tokens) | Context Window    | Notes                                  |
|----------------------|----------------------------|-----------------------------|-------------------|----------------------------------------|
| Gemini 2.5 Pro        | $1.25 – $2.50              | $10.00 – $15.00             | Up to 1M tokens   | High-performance, suitable for complex tasks |
| Gemini 2.5 Flash      | $0.15 (text/image/video)   | $0.60 – $3.50               | 1M tokens         | Balanced performance and cost         |
| Gemini 2.0 Flash      | $0.10 (text/image/video)   | $0.40                      | 1M tokens         | Cost-effective for general use        |
| Gemini 2.0 Flash-Lite | $0.075                     | $0.30                      | Not specified     | Budget-friendly, optimized for scale  |
| Claude 3.7 Sonnet     | $3.00                      | $15.00                     | 200K tokens       | Advanced reasoning capabilities       |
| Claude 3.5 Haiku      | $0.80                      | $4.00                      | 200K tokens       | Fast and cost-efficient               |
| Claude 3 Opus         | $15.00                     | $75.00                     | 200K tokens       | Premium model for complex tasks       |

**Conclusion**: 
Compared to Claude 3 family models, Google Gemini 2.X family models have a higher context window and are more cost-effective for general use. 

## Caching

**Observations**
    - Caching itself takes quite some time
    - Cashing costs: 
        - $1.00/1,000,000 tokens per hour
        - the cached tokens are then billed at $0.025/1,000,000 tokens, 1/4 of the original cost ($0.1/1,000,000 tokens) when used in following prompts
    - The minimum input token count for context caching is 4,096, and the maximum is the same as the maximum for the given model
    - For cashed documents, the reponse time is roughly 1/4 the time of the non-cached responses

**Quick Cost Estimate**
    - Assumptions: 30 page lecture slides, 60,000 tokens, 30 minutes study session, 20 questions
    - No-Caching Cost: 60,000 * 20 / 1,000,000 * 0.1 = $0.12
    - Caching Cost: 60,000 / 1,000,000 * 0.5 * 1 + 60,000 * 20 / 1,000,000 * 0.025 = $0.06
    - Intuition: longer caching time makes caching less cost-effective, more questions asked makes caching more cost-effective

## Message Chaining

Google's Gemini 2.0 Flash model allows for the creation of a multimodal chat session with its modern and older SDKs. It initializes the session with an empty history (no prior conversation). When the user sends a multimodal message, the model will output a response and include both the UserContent and Content(ModelContent) in the chat session's history. Moreover, in this mode, cashing also works. 
