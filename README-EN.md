# RAG_Tutorial

I have worked on various Generative AI projects, including multiple large-scale enterprise-level RAG projects: Enterprise Q&A assistants and intelligent reply robots. Here, I will mainly share my experiences with RAG-related projects.

## What do various parameters in RAG mean? How should they be set? (Using Dify as an example)

This section not only introduces the main principles but also provides parameter setup options for various scenarios.

### Chunk Setting

1. **General Chunk Type**

   ![img](/img/General_Chunk.png)

   1. **Delimiter**
       The delimiter defines how text is divided into chunks. For example, `\n` represents a chunk split by a newline, and `\n\n` represents a chunk split by two newlines.
   2. **Maximum Chunk Length**
       This is the maximum length for a chunk. When chunking, the process will first split based on the delimiter. If the chunk exceeds the maximum length, it will split again. For example, if you set the Maximum Chunk Length to 500 and a segment of text is 600 tokens long, the chunking will occur at 500 tokens to prevent a chunk from containing too many tokens (like a chunk with thousands of tokens if delimiters are not placed well).

2. **Parent-Child Chunk Type**
    This involves setting paragraphs or the entire document as a parent chunk, with smaller chunks inside. The chunking setup is the same as described earlier.

   ![img](/img/Parent-Child_Chunk.png)

   1. **Paragraph Type**
       Treat each paragraph as a parent chunk. The chunking is determined by the delimiter. For example, use `\n\n` to define paragraphs, and set `\n` as the delimiter for smaller chunks.
       (Remember to disable "Replace consecutive spaces, newlines, and tabs," or it may merge paragraphs due to the `\n\n` being replaced by `\n`.)
   2. **Full Doc Type**
       Treat the entire document as a parent chunk, and set `\n` as the delimiter for smaller chunks.

### Index Method

![img](/img/Index_Method.png)

- **High Quality**
   The "Economical" mode only uses 10 keywords per chunk for retrieval, with no token consumption. For company-level projects, always choose "High Quality." Even individual developers should generally go with "High Quality."

### Embedding Model

![img](/img/Embedding_Model.png)

- **Embedding** converts text into vectors, and only vectors can be used for vector-based search.
- Simply choose the embedding model. It is recommended to use OpenAI's embedding model: `text-embedding-3-large`.

### Retrieval Setting

- **Keyword Search**
   Search based on keywords provided by the user and compare them with the keywords in the chunks.

  ![img](/img/Full_Text.png)

- **Vector Search**

  ![img](/img/Vector.png)
   Vector search works by converting the user's input into a vector, and the chunks are also converted into vectors for matching.

- **Hybrid Search**

  ![img](/img/Hybrid_Search.png)

  - **Weighted Score**
     Set a ratio to mix keyword search and vector search. For example, use 0.7 for Semantic and 0.3 for Keyword.
  - **Rerank**
     Use a model to dynamically and automatically adjust this ratio.

- **Top K and Score Threshold**

  The value of Top K depends on how many chunks you want to retrieve. For example, if each chunk is independent and has no relation to others, you can set it to 1. However, if the chunks are related, it is recommended to retrieve multiple chunks to improve accuracy.
   The Threshold determines the match rate at which the results are retrieved. This needs to be tested based on your specific use case.

## Best Combination Strategy - How to Implement Dify + RAGFlow?

## Contact Me: z1597006376@gmail.com

I will keep this simple for now and update it later when I have more time.

For specific RAG strategies, parameter setups, or if you have any questions about Generative AI or RAG, please feel free to contact me at z1597006376@gmail.com.