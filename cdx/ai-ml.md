# `cdx:ai-ml` Namespace Taxonomy

This is the namespace for official CycloneDX properties specific to the Artificial Intelligence (AI)/machine Learning (ML) technology domain.

The official rules and processes apply - see [parent document](../cdx.md).

## AI/ML categories

The following list contains the reserved paths used as category groups for AI/ML properties under the `cdx:ai-ml` namespace.

| Path | Description |
|-----------|-------------|
| `cdx:ai-ml:model` |  Path segment used to group model-related properties. |
| `cdx:ai-ml:tokenizer` |  Path segment used to group tokenizer-related properties. |
| `cdx:ai-ml:prompt` | Path segment used to group prompt-related properties. |

----

### `model` properties

The following table lists the current set of fully-qualified property names for the `model` category:

| Property | Description |
|-----------|-------------|
| `cdx:ai-ml:model:parameter` | Used to describe the learned parameters of a model which  dictated by the model's architecture and design before training.  |
| `cdx:ai-ml:model:hyperparameter` | Used to describe a parameter used as input to a model and used during generation. |
| `cdx:ai-ml:model:tokenizer` | Used to annotate a component as a model tokenizer. |
| `cdx:ai-ml:model:template:prompt` | Used to annotate a component as a model prompt template. |
| `cdx:ai-ml:model:template:chat` | Used to annotate a component as a model chat template. |
| `cdx:ai-ml:model:languages` | Used to indicate what languages a model was trained for. The value for this property should be in the form of a comma-separated list of [ISO 639-1 language codes](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) (e.g., `"en,fr,de,it,ja,zh"`, etc.). |

---

### `model:parameter` properties

These properties reflect on the methods used to control the model's parameter count, training or finetuning.

| Property | Description |
|-----------|-------------|
| `count` | total number of learned parameters for the model. This reflects the model's design and structure (e.g., number of layers in a neural network, nodes, and connectivity). |
| `tune_method` | Describes how a pre-trained model was adapted to new data. This includes values such as: `full` (updates all model parameters), `lora` (parameter-efficient finetuning (PEFT) using the Low-Rank Adaptation), `adapter` ( inserts small layers within the architecture), `prompt` (appends trainable parameters to the input embeddings), etc. |

<!-- TODO: investigate describing (flash) attention methods; for example, MHA, GQA, MQA, etc. -->

---

### `model:hyperparameter` properties

Model hyperparameters are the settings used when configuring a model (and its algorithms) that determine how the model is structured and loaded into memory before any training or inference takes place.

Hyperparameters can vary widely depending on model architecture and specific model variants that reflect on the model's  capabilities and specific code implementation.  This means that we cannot exhaustively list all possible parameters as properties in a taxonomy; however, we intend the `model:hyperparameter` path to be extended with names that actually match the specific implementation.

Given that there are some commonly agreed-upon model configuration property names that are found in [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) that that are implemented on a [Transformer](https://en.wikipedia.org/wiki/Transformer_(deep_learning)) architecture the following properties are defined for the `model:hyperparameter` path segment:

| Property | Description |
|-----------|-------------|
| `hidden_size` \| `d_model` | The dimension of the input and output representations (i.e., of the token embeddings) used by the internal (hidden) layers of a model's neural network (e.g., 768, 1024, 4096). |
| `num_hidden_layers` \| `num_layers` | The total number of intermediate (hidden) processing layers situated between the input layer and the output layer. The key `num_layers` is often used instead for non-transformer architectures (e.g., Recurrent Neural Networks (RNNs), Long Short-Term Memory (LSTM), etc.). |
| `num_attention_heads` | The number of self-attention heads. |
| `num_key_value_heads` | The number of attention heads used for the Key (K) and Value (V) projections in the attention mechanism of a transformer-based AI model. |
| `intermediate_size` | The number of "neurons" of the intermediate, hidden feed-forward layer within each Transformer block. This effectively describes the size of the "bottleneck" where the representation of the input data is expanded (typically 4 times the  `hidden_size`) into a higher-dimensional space for processing before being projected back down to the main model hidden size. |
| `max_position_embeddings` | The maximum sequence/context length the model supports. |
| `vocab_size` | The size of the token vocabulary. |