# JIO-Optimizing-LLM-Using-KG

This project involves implementing a RAG(Retireval Augmented Generation) system with the help of KG(Knowledge Graphs) to improve accuracy of retireval and answer. 

## Overview

This repository showcases the following :

1. **Data Extraction**: Data is scraped from a JIO FAQ site using Selenium.
2. **Data Structuring**: Unstructured data is processed using a Large Language Model (LLM) to generate a structured Knowledge Graph (KG).
3. **Knowledge Graph Storage**: The structured KG is stored in Neo4j, a graph database.
4. **Retrieval and Augmentation**: Using Cypher queries, relevant data is retrieved from the KG.
5. **Answer Generation**: An LLM processes the retrieved context and user queries to generate answers.

## Workflow

1. **Data Extraction with Selenium**
   FAQ Data is extracted from [JIO website][https://www.jio.com/help/faq#/] using selenium
   Dynamic content is handled such as interaction with dropdowns and buttons.

2. **Structuring Data with LLM**
   Using an LLM to process extracted data and create entities, relationships, and properties for the KG.
Example output schema:
```json
{
  "head": "Entity1",
  "head_type": "Type1",
  "head_description": "Description1",
  "relationship": "RelatesTo",
  "tail": "Entity2",
  "tail_type": "Type2",
  "tail_description": "Description2"
}
```

3. **Knowledge Graph in Neo4j**
   Structured data is stored Neo4j using the above schema.
   Data can be visualized and managed the KG using Neo4j's tools.

4. **Retrieval with Cypher Queries**
   Retrieve relevant nodes and relationships using Cypher.
   Vector search is performed to compare relevance of query with the stored nodes.
   Names and description of nodes are stored in vector form and a custom search algorithm is used, code for the algorthm has comments to explain it.
   Example query:
    ```cypher
    MATCH (h)-[r]->(t)  
    WHERE h.name CONTAINS 'keyword'  
    RETURN h, r, t
    ```

6. **Answer Generation with LLM**
   Pass retrieved data along with the user query to the LLM.
   Generate contextual and precise answers.
