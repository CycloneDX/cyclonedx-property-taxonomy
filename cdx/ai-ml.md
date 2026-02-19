# `cdx:ai-ml` Namespace Taxonomy

This is the namespace for official CycloneDX properties specific to the Artificial Intelligence (AI)/machine Learning (ML) technology domain.

The official rules and processes apply - see [parent document](../cdx.md).

## AI/ML categories

The following list contains the reserved paths used as category groups for AI/ML properties under the `cdx:ai-ml` namespace.

| Path | Description |
| --- | --- |
| `cdx:ai-ml:model` |  Path segment used to group model-related properties. |
| `cdx:ai-ml:tokenizer` |  Path segment used to group tokenizer-related properties. |
| `cdx:ai-ml:prompt` | Path segment used to group prompt-related properties. |

---

### `model` properties

The following table lists the current set of fully-qualified property names for the `model` category:

| Property | Description |
| --- | --- |
| `cdx:ai-ml:model:parameter` | Used to describe the learned parameters of a model which  dictated by the model's architecture and design before training. |
| `cdx:ai-ml:model:hyperparameter` | Used to describe a parameter used as input to a model and used during generation. |
| `cdx:ai-ml:model:tokenizer` | Used to annotate a component as a (model) tokenizer. |
| `cdx:ai-ml:model:template:prompt` | Used to annotate a component as a model prompt template. |
| `cdx:ai-ml:model:template:chat` | Used to annotate a component as a model chat template. |
| `cdx:ai-ml:model:languages` | Used to indicate what languages a model was trained for. The value for this property should be in the form of a comma-separated list of [ISO 639-1 language codes](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) (e.g., `"en,fr,de,it,ja,zh"`, etc.). |

---

### `model:parameter` properties

These properties reflect on the methods used to control the model's parameter count, training or finetuning.

| Property | Description |
| --- |--- |
| `count` | total number of learned parameters for the model. This reflects the model's design and structure (e.g., number of layers in a neural network, nodes, and connectivity).  The value should use the industry-standard naming convention of number followed by one of the letters: `M` (Million), `B` (Billion) or `T` (Trillion) (e.g., `1.7M`, `8B`, `70B` or `1T`). |
| `tune_methods` | Describes how the model was fine-tuned on or adapted to new data. The value for this property should be in the form of a comma-separated list of industry-standard values such as those [listed in the section below](#names-of-industry-standard-fine-tuning-methods) (e.g., `"sft, rlhf"`). |

#### Names of industry-standard fine-tuning methods

These following and similar values should be used on the `tune_methods` parameter:

| value | Description |
| --- | --- |
| `full` | Updates all model parameters during tuning. |
| `sft` | Supervised Fine-Tuning. Uses labelled, human-curated data to train the model.|
| `rlhf` | Reinforcement Learning from Human Feedback. |
| `adapter` | Inserts small layers within the architecture which are tuned. |
| `prompt` | appends trainable parameters to the input embeddings |
| `lora` | Low-Rank Adaptation (LoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |
| `alora` | Allocating Low-Rank Adaptation (ALoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |
| `qlora` | Quantized low-rank adaptation (QLoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |

<!-- TODO: investigate describing (flash) attention methods; for example, MHA, GQA, MQA, etc. -->

---

### `model:hyperparameter` properties

Model hyperparameters are the settings used when configuring a model (and its algorithms) that determine how the model is structured and loaded into memory before any training or inference takes place.

Hyperparameters can vary widely depending on model architecture and specific model variants that reflect on the model's  capabilities and specific code implementation.  This means that we cannot exhaustively list all possible parameters as properties in a taxonomy; however, we intend the `model:hyperparameter` path to be extended with names that actually match the specific implementation.

Given that there are some commonly agreed-upon model configuration property names that are found in [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) that that are implemented on a [Transformer](https://en.wikipedia.org/wiki/Transformer_(deep_learning)) architecture the following properties are defined for the `model:hyperparameter` path segment:

| Property | Description |
| --- | --- |
| `activation_dropout` | The regularization technique used during training that randomly masks (sets to zero) a percentage of the intermediate hidden state activations. |
| `context_length` | The maximum number of tokens that the model can process at any one time. |
| `hidden_act` | The activation function used on output values of the intermediate (hidden) layers of a neural network. The function transforms the raw, linear output into an activated output value that is passed to the next layer introducing non-linearity. It is industry-standard to reference these functions by short names such as ReLU (Rectified Linear Unit) or SiLU (Sigmoid Linear Unit) which should be encoded with the values `relu` and `silu` respectively.  |
| `hidden_size`, `d_model` | The dimension of the input and output representations (i.e., of the token embeddings) used by the internal (hidden) layers of a model's neural network (e.g., `768`, `1024`, `4096`). |
| `layer_norm_type` | The specific normalization technique used to stabilize training in a transformer model. It determines how the model rescales activation values to prevent gradients from exploding or vanishing (e.g., `RMSNorm`, `LayerNorm`, `Pre-LN`, `GroupNorm`, etc.). |
| `num_hidden_layers`, `num_layers` | The total number of intermediate (hidden) processing layers situated between the input layer and the output layer. The key `num_layers` is often used instead for non-transformer architectures (e.g., Recurrent Neural Networks (RNNs), Long Short-Term Memory (LSTM), etc.). |
| `intermediate_size` | The number of "neurons" of the intermediate, hidden feed-forward layer within each Transformer block. This effectively describes the size of the "bottleneck" where the representation of the input data is expanded (typically 4 times the `hidden_size`) into a higher-dimensional space for processing before being projected back down to the main model hidden size. |
| `layer_norm_epsilon` | The (very small) float value used in Transformer models which is added to the variance in the denominator of the layer normalization formula to prevent division by zero (e.g., `1e-06`, `1e-05`). |
| `max_position_embeddings` | The maximum sequence/context length the model supports. |
| `num_attention_heads` | The number of self-attention heads (e.g., `32`). |
| `num_key_value_heads` | The number of attention heads used for the Key (K) and Value (V) projections in the attention mechanism of a transformer-based AI model. |
| `quantization` | Defines the numerical precision (number of bits) used to store a model's weights (as tensors) (e.g., `bf16`, `Q4_K_M`, `Q8_0`, etc.). |
| `tokenizer_class` | The specific software class (i.e., implementation) used to convert raw text into token IDs and back (e.g., `GPT2Tokenizer`, `LlamaTokenizer`, etc. ). |
| `vocab_size` | The size of the token vocabulary. |

---

### `tokenizer:hyperparameter` properties

Model tokenizers, although generally conforming to small set of industry-acknowledged implementations, often have distinct variants developed to work with a specific model it was used to train.  These tokenizers have their own hyperparameters that can be declared as properties on a CycloneDX component's model card as described for `model:hyperparameters` (above).

Given that there are some commonly agreed-upon tokenizer configuration property names that are found in [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) that that are implemented on a [Transformer](https://en.wikipedia.org/wiki/Transformer_(deep_learning)) architecture the following properties are defined for the `tokenizer:hyperparameter` path segment:

| Property | Description |
| --- | --- |
| `bos_token` |  The Beginning-of-Sentence (BOS) token is a special token configured in a tokenizer that signifies the start of an input sequence. (e.g., `"<[end_of_text]>"`)|
| `chat_template` | A string representation of the chat template that defines how to format conversational data using the configured tokenizer.|
| `errors` | Configures how the tokenizer handles invalid UTF-8 byte sequences or character encoding issues when converting raw text into tokens. Known values include: `strict` (i.e., raise an error), `ignore` and `replace` (invalid token).|
| `eos_token` |  The End-of-Sentence (BOS) token is a special token configured in a tokenizer to act as a stop signal for text generation. |
| `pad_token` |  The pad token is a special token configured in a tokenizer to fill in empty spaces in shorter sequences within a batch, ensuring all input sequences have the exact same length. |
| `padding_side` | Defines whether the tokenizer adds padding tokens (i.e., the `pad_token`) to the left or right side of a sequence to ensure all sequences in a batch are the same length. Known values are either `left` or `right`. |
| `tokenizer_class` | The named tokenizer (class) implementation configured for the model when the tokenizer support multiple possible implementations. |
| `unk_token` | The special token configured in a tokenizer to replace any input character or word that is not found in the model's vocabulary. |
| `vocab_size` | The configured size of the token vocabulary.  Please note this value should match the `vocab_size` model hyperparameter value if both are declared on the same model card. |

#### Tokenizer hyperparameter notes

* if the `model:hyperparameters:tokenizer_class` hyperparameter value is declared,  the `tokenizer:hyperparameters:tokenizer_class` value should match.
* Tokenizer hyperparameter values should be compatible with the tokenizer class implementation (value) provided on the `tokenizer_class` hyperparameter.
* Tokenizer hyperparameters that configure special token such as `bos_token`, `eos_token`, `pad_token`, etc. often utilize a distinct syntax such as the `<|` and `|>` that delineates them from other tokens (e.g., `<|im_start|>`, `<|pad_id|>`, `<|end_of_text|>`).