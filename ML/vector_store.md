# Vector Store

Store and query vectors

- Pinecone offers 2GB free tier and easy to use
- postgres has a vector search worth looking into

## Pinecone

```ts
import { Pinecone } from "@pinecone-database/pinecone";

const PINECONE_INDEX_NAME = "corpus-embeddings"; 
const pinecone = new Pinecone({
  apiKey: process.env.PINECONE_API_KEY,
});

export async function saveEmbeddingsToPinecone(
  corpusId: number,
  textPairs: string[],
  embeddings: number[][]
) {
  const index = pinecone.Index(PINECONE_INDEX_NAME);
  const vectors = textPairs.map((text, i) => ({
    id: `${corpusId}-${i}`,
    values: embeddings[i],
    metadata: { text, corpusId },
  }));

  const batchSize = 100;
  const batches = [];
  for (let i = 0; i < vectors.length; i += batchSize) {
    batches.push(vectors.slice(i, i + batchSize));
  }
  await Promise.all(batches.map((batch) => index.upsert(batch)));
}

export async function queryNearestEmbeddings(
  embedding: number[],
  corpusId: number,
  k: number = 3
) {
  const index = pinecone.Index(PINECONE_INDEX_NAME);
  const queryResponse = await index.query({
    vector: embedding,
    topK: k,
    includeMetadata: true,
    filter: { corpusId: corpusId },
  });
  return queryResponse.matches;
}
```

