
# Knowledge Document Classification by Chunks

![](KnowledgeDocumentClassificationChunkByChunk.png)

This workflow will loop classify each segment of a single document in the Dify knowledge base based on the input.
If any segment is classified as “include 2023 year”, the loop will break early and stop further classification.
If all segments in the document are classified as “not include”, the process will move on to the next document.

This workflow can be applied in scenarios such as confidential content inspection and sensitive information identification at the paragraph level in documents.

## how to use

1. Create Knowledge API Secret key like `dataset-YNcow9NDZeGA1f2tFokkX0Sr`
2. Create Knowledge dataset and upload some file and get `dataset_id`

    use this api with API Secret key to get `dataset_id`

    ```bash
    curl --location --request GET 'http://dify.lan:80/v1/datasets?page=1&limit=20' \
    --header 'Authorization: Bearer dataset-YNcow9NDZeGA1f2tFokkX0Sr' | jq
    ```

3. Import DSL file [KnowledgeDocumentClassificationChunkByChunk.yml](./KnowledgeDocumentClassificationChunkByChunk.yml)
4. Change [Conversation Variable](https://docs.dify.ai/guides/workflow/variables#conversation-variables)

    Conversation Variable

    - dataset_key from step 1
    - dataset_id from step 2


## Why chunk by chunk

For long-text classification,
due to the limited context window and constrained semantic understanding of the model,
segmenting the text can lead to better classification performance.

At the same time, since the Dify knowledge base has already segmented the documents,
it is possible to directly retrieve these segments from the Dify knowledge base.
