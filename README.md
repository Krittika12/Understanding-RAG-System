# Understanding-RAG-System 
credits : https://www.dailydoseofds.com/

## Workflow of RAG System

### 1. Create chunks
<img width="808" height="218" alt="image" src="https://github.com/user-attachments/assets/a403edd9-e152-4e69-b78d-51e99b4a091b" />

Why?
- to ensure text fits the input size of embedding model
- no chunking -> single embedding for whole doc->loses context <br>
#### Types of chunking :
1. Fixed size chunking
- Splitting text in uniform segment based on a pre-defined number of characters, words, or tokens.
- Recommended to maintain certain overlap
<img width="760" height="172" alt="image" src="https://github.com/user-attachments/assets/8754b35f-b7f1-46bb-990f-81dcc68a9437" />
<table>
  <th>Advantage</th>
  <th>DisAdvantage</th>
  <tr>
    <td>All chunks same size - easy batch processing</td>
    <td>Breaks sentence(ideas) in btwn -> imp info distribute in diff chunk</td>
  </tr>
</table>

2. Semantic Chunking
- Segment the section based on meaningful units : sentences, para, sec theme
- follow the flow attached in the image to form chunks
<img width="737" height="212" alt="image" src="https://github.com/user-attachments/assets/0e6c37b4-1dc6-4fd9-8026-be13b70ba80a" />
<table>
  <th>Advantage</th>
  <th>DisAdvantage</th>
  <tr>
    <td>More relevant responses {Retrival Accuracy(2. SC) > Retrival Accuracy(1. FC)}</td>
    <td>Depends on threshold to determine if cos sim dropped significantly (document dependent - ambiguity)</td>
  </tr>
</table>

3. Recursive chunks
- segment chunk + if size(segment) > chunk-size limit -> split segment
  <img width="737" height="235" alt="image" src="https://github.com/user-attachments/assets/8b0cbfb8-b2c7-4096-ab40-a607bc0669ae" />
<table>
  <th>Advantage</th>
  <th>DisAdvantage</th>
  <tr>
    <td>Preserves complete idea</td>
    <td>add computational complexity</td>
  </tr>
</table>

4. Document structure based chunking
- utilizes the inherent structure of documents, like headings, sections, or paragraphs, to define chunk boundaries.
  <img width="758" height="220" alt="image" src="https://github.com/user-attachments/assets/fe13e95b-c47a-4d3a-ba92-e0a87331ae35" />
<table>
  <th>Advantage</th>
  <th>DisAdvantage</th>
  <tr>
    <td>maintains structural integrity by aligning with the document’s logical</td>
    <td>assumes that the document has a clear structure</td>
  </tr>
</table>

5. LLM based chunking

- <img width="745" height="138" alt="image" src="https://github.com/user-attachments/assets/660f908a-9164-4835-8cf0-0e8eb1572bd7" />
<table>
  <th>Advantage</th>
  <th>DisAdvantage</th>
  <tr>
    <td>ensure high semantic accuracy </td>
    <td>most computationally demanding</td>
  </tr>
</table>

### 2. Generate embeddings
- not word embedding, context embeddings are created
  
### 3. Store embeddings in vector DB
### 4. User input query
### 5. Embed the query
This query is transformed into a vector using the same embedding model we used to embed the chunks earlier in Step 2.
### 6. Retrieve similar chunks
The vectorized query is then compared against our existing vectors in the database to find the most similar information.
### 7. Retrieve similar chunks
This process rearranges the chunks so that the most relevant ones are prioritized for the response generation.
### 8. Generate the final response
This model combines the user's original query with the retrieved chunks in a prompt template to generate a response that synthesizes information from the selected documents.
## Tool Stack
