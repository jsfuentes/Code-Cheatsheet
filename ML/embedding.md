# Embedding

Embeddings Can Be Used For:

- Similarity Search/Retrieval: query for similar items/lines/docs (distance) for RAG, rec systems
- Classification/Clustering/Anomaly Detection

Embeddings can be at the word, sentence, paragraph, document level and be across mediums into images/audio([CLIP](https://huggingface.co/docs/transformers/en/model_doc/clip)) too. Can be based on context too(BERT & GPT), so bank different embedding depending on context

## Options

Comparing:

- [MTEB(Massive Text Embedding Benchmark)](https://huggingface.co/spaces/mteb/leaderboard)
  - Consider embeddings for your use case/lang, as no model is SOTA for all tasks including
- Also see 

- Recommendation 9/21/24: 
  -  [VoyageAI](), `voyage-3` and `voyage-3-lite`
    - First 200 million tokens [free](https://docs.voyageai.com/docs/pricing)
    - `voyage-3-lite` 3.82% better retrieval than OpenAI v3 large with 6x less cost and embedding size
    -  [`voyage-code-2`](https://blog.voyageai.com/2024/01/23/voyage-code-2-elevate-your-code-retrieval/), [`voyage-law-2`](https://blog.voyageai.com/2024/04/15/domain-specific-embeddings-and-retrieval-legal-edition-voyage-law-2/), [`voyage-finance-2`](https://blog.voyageai.com/2024/06/03/domain-specific-embeddings-finance-edition-voyage-finance-2/), and [`voyage-multilingual-2`](https://blog.voyageai.com/2024/06/10/voyage-multilingual-2-multilingual-embedding-model/),

- Other Options
  - [OpenAI](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings)
  - https://replicate.com/collections/embedding-models


## Voyage AI

js

```ts
import { VoyageAIClient } from "voyageai";

const client = new VoyageAIClient({ apiKey: "YOUR_API_KEY" });
await client.embed({
    input: ["input1", "input2", "input3", "input4"],
    model: "voyage-3-lite",
});
```

py

```python
import voyageai

vo = voyageai.Client()
# This will automatically use the environment variable VOYAGE_API_KEY.
# Alternatively, you can use vo = voyageai.Client(api_key="<your secret key>")

# Embed the documents
documents_embeddings = vo.embed(
    documents, model="voyage-3", input_type="document"
).embeddings
```

## OpenAI

Js

```js
import OpenAI from "openai";

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

export async function generateEmbedding(text: string): Promise<number[]> {
  const response = await openai.embeddings.create({
    model: "text-embedding-3-large",
    input: text,
  });

  return response.data[0].embedding;
}
```

