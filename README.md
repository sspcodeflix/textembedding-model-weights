# textembedding-model-weights

Offline copy of the `sentence-transformers/all-MiniLM-L6-v2` embedding model in ONNX format, for use with [FastEmbed](https://github.com/qdrant/fastembed) on machines that can't reach Hugging Face.

- Source: [Qdrant/all-MiniLM-L6-v2-onnx](https://huggingface.co/Qdrant/all-MiniLM-L6-v2-onnx), an ONNX port of [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)
- License: Apache-2.0 (see [LICENSE](LICENSE))
- Output: 384-dimensional vectors, max 256 tokens per input (longer text is truncated), English

## Verify the files

```bash
cd all-MiniLM-L6-v2-onnx && sha256sum -c SHA256SUMS
```

All lines should say `OK`. `model.onnx` should be about 90 MB. If it's a few hundred bytes, you got a Git LFS pointer instead of the real file.

## Use with FastEmbed

```bash
pip install fastembed
```

```python
from fastembed import TextEmbedding

model = TextEmbedding(
    model_name="sentence-transformers/all-MiniLM-L6-v2",
    specific_model_path="./all-MiniLM-L6-v2-onnx",  # loads locally, no download
)
vectors = list(model.embed(["hello world"]))
```

Tested with fastembed 0.8.1.
