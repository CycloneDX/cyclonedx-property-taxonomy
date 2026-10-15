# `cdx:ai-ml` Namespace Taxonomy

This is the namespace for official CycloneDX properties specific to the Artificial Intelligence (AI) and Machine Learning (ML).

The official rules and processes apply - see [parent document](../cdx.md).

---

The following are the reserved namespaces for AI/ML under the `cdx:ai-ml` namespace.

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:model` | Model-related properties. |
| `cdx:ai-ml:tokenizer` | Tokenizer-related properties. |
| `cdx:ai-ml:dataset` | Dataset-related properties. |
| `cdx:ai-ml:prompt` | Prompt-related properties. |

_Boolean value_ are `true` or `false`; case sensitive.

---

## `cdx:ai-ml:model` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:model:modality` | Provide the modality/modalities the model supports. This describes the specific type(s) or format(s) of data the model is designed to process such as text, images, audio, video, or sensor data. |
| `cdx:ai-ml:model:template` | Mark a model's' template and describe its details. |
| `cdx:ai-ml:model:parameter` | Describe learned parameters of a model which dictated by the model's architecture and design before training. |
| `cdx:ai-ml:model:hyperparameter` | Describe parameters used to configure a model. |
| `cdx:ai-ml:model:architecture` | Describe the structural and behavioral architecture of the model. Maps directly to the `modelArchitecture.structural` object in the JSON schema. |
| `cdx:ai-ml:model:task` | Describe the ML task the model is designed to perform. Maps to the `modelTaskType` definition in the JSON schema. |
| `cdx:ai-ml:model:metric` | Describe metrics, typically performance metrics, associated with the model. Utilizes the `performanceMetric.type` definition in the JSON schema. |

### `cdx:ai-ml:model:tokenizer` Namespace Taxonomy

These following values SHOULD be used with the `cdx:ai-ml:model:tokenizer` property:

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:model:tokenizer` | Mark a component as a (model) tokenizer. _Boolean value_. </br> This property MAY appear once. |

#### Example: Marking a component as a model tokenizer

```jsonc
{
  // ...
  "components": [{
    "type": "library",
    "name": "my_tokenizer.py",
    // ...
    "properties": [
      {
        "name": "cdx:ai-ml:model:tokenizer",
        "value": "true"
      }
    ]
  }]
}
```

### `cdx:ai-ml:model:modality` Namespace Taxonomy

These following values SHOULD be used with the `cdx:ai-ml:model:modality` property:

| Value | Description |
| -------- | ----------- |
| `text` | Natural Language Processing (NLP) tasks and specializations such as Natural Language Understanding (NLU) for tasks like translation, summarization, conversation, classification and sentiment analysis. |
| `code` | Specialized, text-based modality used for software engineering and logic. |
| `instruct` | Specialized, text-based modality fine-tuned for understanding and executing natural language directives (i.e., instruction following). |
| `image` (vision) | Image-based (i.e., computer vision) processing tasks used for object detection, generation, and classification as well as document processing. |
| `video` | Video  processing tasks to extract structured information, including object detection, action recognition, scene detection, and temporal understanding. |
| `audio` | Audio processing tasks such as Automatic Speech Recognition (ASR), Speech-to-Text, music generation, and sound pattern recognition. |
| `sensor` (telemetry) |  Processes data from specialized sensors or hardware, such as LiDAR for autonomous vehicles or IoT sensor feeds. |
| `biometric` | Specialized sensor-based modality used for analyzing biological traits for tasks such as facial recognition, fingerprint scanning, or voice authentication. |
| `genomic` (telemetry) | Processes high-dimensional data used in drug discovery and medical research. |
| `_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary model modality name. |

#### Example: Using model modalities on the model's component

```jsonc
{
  // ...
  "component": {
    "type": "machine-learning-model",
    "bom-ref": "pkg:huggingface/FakeAI/CoderModel",
    // ...,
    "properties": [
      {
        "name": "cdx:ai-ml:model:modality",
        "value": "code"
      },
      {
        "name": "cdx:ai-ml:model:modality",
        "value": "instruct"
      }
    ]
  }
}
```

### `cdx:ai-ml:model:language` Namespace Taxonomy

Model language values MUST be valid [ISO 639-1 language codes](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes).

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:model:language` | Describe what language(s) a model was trained for. Value MUST be of [ISO 639-1 language codes](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes). Value MUST be a single language code (e.g. `nl`) or a comma separated list of language codes (e.g. `en,fr,de,it,ja,zh`). </br> This property MAY occur multiple times. |

### Example: Using multiple languages

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my model",
    "modelCard": {
      // ...
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:language",
            "value": "de,en"
          },
          {
            "name": "cdx:ai-ml:model:language",
            "value": "la"
          },
          {
            "name": "cdx:ai-ml:model:language",
            "value": "it"
          }
        ]
      }
    }
  }]
}
```

### `cdx:ai-ml:model:template` Namespace Taxonomy

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:model:template:prompt` | Mark a component as a model prompt template. _Boolean value_. </br> This property MAY appear once. |
| `cdx:ai-ml:model:template:chat` | Mark a component as a model chat template. _Boolean value_. </br> This property MAY appear once. |

### `cdx:ai-ml:model:parameter` Namespace Taxonomy

Model properties reflect on the methods used to control the model's parameter count, training or fine-tuning.

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:model:parameter:count` | Total number of learned parameters for the model. This reflects the model's design and structure (e.g., number of layers in a neural network, nodes, and connectivity). </br> The value SHOULD use the industry-standard naming convention of number followed by one of the letters: `M` (Million), `B` (Billion) or `T` (Trillion). This property MAY appear once. |
| `cdx:ai-ml:model:parameter:tune_method` | Describes how the model was fine-tuned on or adapted to new data. Values SHOULD be industry-standard keywords such as those [listed in the section below](#names-of-industry-standard-fine-tuning-methods). Value MUST be a single keyword (e.g., `lora`) or a comma separated list of keywords (e.g., `sft,rlhf`). </br> This property MAY appear multiple times. |
| `cdx:ai-ml:model:parameter:quantization:scheme` | Identifies the quantization scheme described by the accompanying quantization sub-properties. Value SHOULD be one of the [quantization scheme values listed below](#quantization-scheme-values). This property MUST be present whenever any other `quantization` sub-property is used. MAY appear once. |
| `cdx:ai-ml:model:parameter:quantization:scale` | The scale factor(s) used by the quantization scheme. For per-tensor quantization, value is a string containing a single decimal number (e.g., `"0.0078125"`). For per-axis quantization, value is a string containing a JSON-serialized numeric array whose element `i` applies to slice `i` along the tensor dimension selected by `quantization:axis` (e.g., `"[0.0078125,0.015625]"`). MAY appear once. |
| `cdx:ai-ml:model:parameter:quantization:zeroPoint` | The zero-point offset(s) used by the quantization scheme. For per-tensor quantization, value is a string containing a single integer (e.g., `"128"`). For per-axis quantization, value is a string containing a JSON-serialized integer array whose element `i` applies to slice `i` along the tensor dimension selected by `quantization:axis` (e.g., `"[128,0]"`), with cardinality matching `quantization:scale`. MAY appear once. |
| `cdx:ai-ml:model:parameter:quantization:granularity` | The granularity at which quantization parameters are applied. Value MUST be one of: `per-tensor` (a single scale and zero-point applies to the entire tensor) or `per-axis` (separate scale and zero-point values apply along a specific axis). Defaults to `per-tensor` when absent. MAY appear once. |
| `cdx:ai-ml:model:parameter:quantization:axis` | The axis index along which per-axis quantization is applied. Required when `quantization:granularity` is `per-axis`; MUST be omitted or ignored when granularity is `per-tensor`. Value is a non-negative integer that identifies the quantized dimension in the tensor shape. MAY appear once. |
| `cdx:ai-ml:model:parameter:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary model parameter name. Arbitrary value and meaning. |

#### Names of industry-standard fine-tuning methods

These following and similar values SHOULD be used on the `cdx:ai-ml:model:parameter:tune_method` parameter:

| Value | Description |
| ----- | ----------- |
| `full` | Updates all model parameters during tuning. |
| `sft` | Supervised Fine-Tuning. Uses labelled, human-curated data to train the model.|
| `rlhf` | Reinforcement Learning from Human Feedback. |
| `adapter` | Inserts small layers within the architecture which are tuned. |
| `prompt` | appends trainable parameters to the input embeddings |
| `lora` | Low-Rank Adaptation (LoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |
| `alora` | Allocating Low-Rank Adaptation (ALoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |
| `qlora` | Quantized low-rank adaptation (QLoRA). A standard Parameter-Efficient Fine-Tuning (PEFT) method. |

#### Quantization scheme values

The `cdx:ai-ml:model:parameter:quantization:scheme` property identifies the mathematical contract between floating-point values and their quantized integer representation. A scheme determines which companion sub-properties (`scale`, `zeroPoint`, `granularity`, `axis`) are meaningful. Future schemes MAY introduce additional sub-properties under the same `cdx:ai-ml:model:parameter:quantization:` namespace without conflicting with existing entries.

| Value | Description |
| ----- | ----------- |
| `affine_asymmetric` | Affine (uniform) asymmetric quantization. Maps the floating-point range to an integer range via a scale and zero-point: `x_float = scale * (x_int - zeroPoint)`. The zero-point is not constrained by a symmetry requirement and may therefore be zero. The companion `scale` and `zeroPoint` sub-properties MUST be present. |
| `affine_symmetric` | Affine (uniform) symmetric quantization. A specialization of affine quantization that applies a symmetry constraint around real zero. The companion `scale` sub-property MUST be present. The zero-point convention depends on the declared integer representation; for zero-centered signed INT8 storage, `zeroPoint` is `0`. |
| `_undefined:<NAME>` | `<NAME>` placeholder, used to identify a quantization scheme not yet listed in this taxonomy. |

#### Example: Using model parameter names listed in the AI/ML taxonomy

The following pseudocode shows how you would include the defined (reserved) `count` and `tuning_method` model parameters on an ML model's model card:

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my model",
    "modelCard": {
      // ...
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:parameter:count",
            "value": "7B"
          },
          {
            "name": "cdx:ai-ml:model:parameter:tuning_method",
            "value": "sft,rlhf"
          },
          {
            "name": "cdx:ai-ml:model:parameter:tuning_method",
            "value": "qlora"
          },
          {
            "name": "cdx:ai-ml:model:parameter:tuning_method",
            "value": "adapter"
          }
        ]
      }
    }
  }]
}
```

#### Example: Using an unlisted model parameter name

The following pseudocode shows how you would include a model parameter that is not currently listed in the AI/ML namespace taxonomy.  Below, we introduce the metasyntactic parameter name `foo` with a value `bar`.

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my model with own parameter",
    "modelCard": {
      // ...
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:parameter:_undefined:foo",
            "value": "bar"
          }
        ]
      }
    }
  }]
}
```

#### Example: Using quantization parameters (per-tensor, affine asymmetric)

The following pseudocode shows how to describe per-tensor affine asymmetric quantization parameters in a model card:

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my quantized model",
    "modelCard": {
      // ...
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:parameter:quantization:scheme",
            "value": "affine_asymmetric"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:granularity",
            "value": "per-tensor"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:scale",
            "value": "0.0078125"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:zeroPoint",
            "value": "128"
          }
        ]
      }
    }
  }]
}
```

#### Example: Using quantization parameters (per-axis, affine symmetric)

The following pseudocode shows how to describe a PyTorch-style per-axis INT8 affine symmetric quantization of a weight tensor along axis `0`. In this signed INT8 example, the symmetric convention uses `zeroPoint = 0`, which the example omits. The `scale` property value is a string containing a JSON-serialized numeric array with one element per slice along the quantized axis.

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my symmetric per-axis quantized model",
    "modelCard": {
      // ...
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:parameter:quantization:scheme",
            "value": "affine_symmetric"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:granularity",
            "value": "per-axis"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:axis",
            "value": "0"
          },
          {
            "name": "cdx:ai-ml:model:parameter:quantization:scale",
            "value": "[0.00787402, 0.01574803, 0.00393701]"
          }
        ]
      }
    }
  }]
}
```

### `cdx:ai-ml:model:hyperparameter` Namespace Taxonomy

Model hyperparameters are the settings used when configuring a model (and its algorithms) that determine how the model is structured and loaded into memory before any training or inference takes place.

Hyperparameters can vary widely depending on model architecture and specific model variants that reflect on the model's capabilities and specific code implementation. This means that we cannot exhaustively list all possible parameters as properties in a taxonomy; however, we intend the `cdx:ai-ml:model:hyperparameter` namespace to be extended with names that actually match the specific implementation, for which the property name placeholder `<NAME>` may be utilized.

Given that there are some commonly agreed-upon model configuration property names that are found in [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) that are implemented on a [Transformer](https://en.wikipedia.org/wiki/Transformer_(deep_learning)) architecture the following properties are defined for the `cdx:ai-ml:model:hyperparameter` namespace:

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:model:hyperparameter:activation_dropout` | The regularization technique used during training that randomly masks (sets to zero) a percentage of the intermediate hidden state activations. |
| `cdx:ai-ml:model:hyperparameter:context_length` | The maximum number of tokens that the model can process at any one time. |
| `cdx:ai-ml:model:hyperparameter:hidden_act` | The activation function used on output values of the intermediate (hidden) layers of a neural network. The function transforms the raw, linear output into an activated output value that is passed to the next layer introducing non-linearity. It is industry-standard to reference these functions by short names such as ReLU (Rectified Linear Unit) or SiLU (Sigmoid Linear Unit) which SHOULD be encoded with the values `relu` and `silu` respectively. |
| `cdx:ai-ml:model:hyperparameter:hidden_size`, `:d_model` | The dimension of the input and output representations (i.e., of the token embeddings) used by the internal (hidden) layers of a model's neural network (e.g., `768`, `1024`, `4096`). |
| `cdx:ai-ml:model:hyperparameter:layer_norm_type` | The specific normalization technique used to stabilize training in a transformer model. It determines how the model rescales activation values to prevent gradients from exploding or vanishing (e.g., `RMSNorm`, `LayerNorm`, `Pre-LN`, `GroupNorm`, etc.). |
| `cdx:ai-ml:model:hyperparameter:num_hidden_layers`, `:num_layers` | The total number of intermediate (hidden) processing layers situated between the input layer and the output layer. The key `num_layers` is often used instead for non-transformer architectures (e.g., Recurrent Neural Networks (RNNs), Long Short-Term Memory (LSTM), etc.). |
| `cdx:ai-ml:model:hyperparameter:intermediate_size` | The number of "neurons" of the intermediate, hidden feed-forward layer within each Transformer block. This effectively describes the size of the "bottleneck" where the representation of the input data is expanded (typically 4 times the `hidden_size`) into a higher-dimensional space for processing before being projected back down to the main model hidden size. |
| `cdx:ai-ml:model:hyperparameter:layer_norm_epsilon` | The (very small) float value used in Transformer models which is added to the variance in the denominator of the layer normalization formula to prevent division by zero (e.g., `1e-06`, `1e-05`). |
| `cdx:ai-ml:model:hyperparameter:max_position_embeddings` | The maximum sequence/context length the model supports. |
| `cdx:ai-ml:model:hyperparameter:num_attention_heads` | The number of self-attention heads (e.g., `32`). |
| `cdx:ai-ml:model:hyperparameter:num_key_value_heads` | The number of attention heads used for the Key (K) and Value (V) projections in the attention mechanism of a transformer-based AI model. |
| `cdx:ai-ml:model:hyperparameter:quantization` | Defines the numerical precision (number of bits) used to store a model's weights (as tensors) (e.g., `bf16`, `q4_k_m`, `q8_0`, etc.). |
| `cdx:ai-ml:model:hyperparameter:tokenizer_class` | The specific software class (i.e., implementation) used to convert raw text into token IDs and back (e.g., `GPT2Tokenizer`, `LlamaTokenizer`, etc. ). |
| `cdx:ai-ml:model:hyperparameter:vocab_size` | The size of the token vocabulary. |
| `cdx:ai-ml:model:hyperparameter:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary model hyperparameter name. Arbitrarty value and meaning. |

Each well-known property MAY be used once.

#### Example: Using model hyperparameter names listed in the AI/ML taxonomy

The following pseudocode shows how you would include the defined (reserved) `hidden_act`, `hidden_size` and `num_hidden_layers` model hyperparameters on an ML model's model card:

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my model",
    // ...
    "modelCard": {
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:hyperparameter:hidden_act",
            "value": "relu"
          },
          {
            "name": "cdx:ai-ml:model:parameter:hidden_size",
            "value": "4096"
          },
          {
            "name": "cdx:ai-ml:model:parameter:num_hidden_layers",
            "value": "32"
          }
        ]
      }
    }
  }]
}
```

#### Example: Using an unlisted model hyperparameter name

The following pseudocode shows how to include a model hyperparameter that is not currently listed in the AI/ML namespace taxonomy.  Below, we introduce the metasyntactic hyperparameter name `hamm` with a value `eggz`.

```jsonc
{
  // ...
  "components": [{
    "type": "machine-learning-model",
    "name": "my model with own hyperparameter",
    // ...
    "modelCard": {
      "modelParameters": {
        "properties": [
          {
            "name": "cdx:ai-ml:model:hyperparameter:_undefined:hamm",
            "value": "eggz"
          },
        ]
      }
    }
  }]
}
```

---

## `cdx:ai-ml:model:architecture` Namespace Taxonomy

The `cdx:ai-ml:model:architecture` namespace corresponds to the `modelArchitecture.structural` object in the CycloneDX v2.0 AI/ML JSON Schema (`cyclonedx-ai-ml-2.0.schema.json`).

Each field that has a `^cdx:ai-ml:[a-z0-9:-]+$` pattern extension accepts values in **two equivalent forms**:

- **Short form** — the plain enum string defined in the schema (e.g., `transformer`). Use this form for any value listed in the schema's built-in enum.
- **URN-style form** — the fully qualified `cdx:ai-ml:` prefixed path (e.g., `cdx:ai-ml:model:architecture:primary:transformer`). This form MUST be used for any value not present in the schema's built-in enum. Either form MAY be used for built-in values; the short form is preferred for brevity.

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:model:architecture:primary` | The core mathematical structural framework of the model backbone. Maps to `structural.primary`. |
| `cdx:ai-ml:model:architecture:secondary` | A secondary macro-layout or component sub-network built into the primary structure. MAY appear multiple times. Maps to items in `structural.secondary`. |
| `cdx:ai-ml:model:architecture:topology` | The runtime parameter activation and connection structure of the network layers. Maps to `structural.topologyType`. |

### `cdx:ai-ml:model:architecture:primary` Values

Maps to `structural.primary` in the schema. The **Short form** column is the built-in schema enum value; the **URN-style form** column is the equivalent fully-qualified property taxonomy value. Rows marked have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `transformer` | `cdx:ai-ml:model:architecture:primary:transformer` | Architecture based on self-attention mechanisms for processing sequential or spatial data. |
| `cnn` | `cdx:ai-ml:model:architecture:primary:cnn` | Convolutional Neural Network — architecture using convolutional layers for processing grid-like data. |
| `rnn` | `cdx:ai-ml:model:architecture:primary:rnn` | Recurrent Neural Network — architecture with recurrent connections for sequential data processing. |
| `lstm` | `cdx:ai-ml:model:architecture:primary:lstm` | Long Short-Term Memory — RNN variant with gating mechanisms for long-term dependencies. |
| `gru` | `cdx:ai-ml:model:architecture:primary:gru` | Gated Recurrent Unit — RNN variant with simplified gating compared to LSTM. |
| `gan` | `cdx:ai-ml:model:architecture:primary:gan` | Generative Adversarial Network — dual-network framework containing a generator and a discriminator. |
| `vae` | `cdx:ai-ml:model:architecture:primary:vae` | Variational Autoencoder — probabilistic encoder-decoder architecture mapping to a latent space. |
| `mamba` | `cdx:ai-ml:model:architecture:primary:mamba` | State-space model architecture with selective mechanisms for efficient sequence modeling. |
| `ssm` | `cdx:ai-ml:model:architecture:primary:ssm` | State Space Model — core architecture based on continuous or discrete state-space representations. |
| `gnn` | `cdx:ai-ml:model:architecture:primary:gnn` | Graph Neural Network — architecture optimized for processing graph-structured data elements. |
| `mlp` | `cdx:ai-ml:model:architecture:primary:mlp` | Multi-Layer Perceptron — classic feedforward architecture composed entirely of fully connected layers. |
| `rwkv` | `cdx:ai-ml:model:architecture:primary:rwkv` | Receptive Weighted Key Value — architecture combining parallelizable training with RNN-like inference. |
| `snn` | `cdx:ai-ml:model:architecture:primary:snn` | Spiking Neural Network — neuromorphic architecture utilizing discrete, time-dependent spiking activations. |
| `kan` | `cdx:ai-ml:model:architecture:primary:kan` | Kolmogorov-Arnold Network — architecture featuring learnable activation functions on edges rather than nodes. |
| `diffusion` | `cdx:ai-ml:model:architecture:primary:diffusion` | Denoising diffusion probabilistic model — iteratively refines noise into data (e.g., DDPM, Stable Diffusion). |
| `flow-matching` | `cdx:ai-ml:model:architecture:primary:flow-matching` | Continuous normalizing flow trained via flow matching / rectified flow (e.g., Flux, SD3). |
| `rbm` | `cdx:ai-ml:model:architecture:primary:rbm` | Restricted Boltzmann Machine — energy-based generative model with stochastic hidden units. |
| `capsnet` | `cdx:ai-ml:model:architecture:primary:capsnet` | Capsule Network — architecture using dynamic routing between capsule groups to preserve spatial hierarchies. |
| `neuromorphic` | `cdx:ai-ml:model:architecture:primary:neuromorphic` | Architecture designed for deployment on neuromorphic hardware (e.g., Intel Loihi, IBM TrueNorth). |
| `hybrid` | `cdx:ai-ml:model:architecture:primary:hybrid` | Explicit first-class combination of two or more distinct primary architectures (e.g., CNN+Transformer). |
| _(none)_ | `cdx:ai-ml:model:architecture:primary:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary primary architecture name. |

### `cdx:ai-ml:model:architecture:secondary` Values

Maps to items in `structural.secondary` in the schema. Rows marked have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `decoder-only` | `cdx:ai-ml:model:architecture:secondary:decoder-only` | Autoregressive macro-layout processing data left-to-right (e.g., GPT series). |
| `encoder-only` | `cdx:ai-ml:model:architecture:secondary:encoder-only` | Bidirectional macro-layout processing complete sequences simultaneously (e.g., BERT). |
| `encoder-decoder` | `cdx:ai-ml:model:architecture:secondary:encoder-decoder` | Sequence-to-sequence structure mapping an input representation to an output sequence (e.g., T5). |
| `mixture-of-experts` | `cdx:ai-ml:model:architecture:secondary:mixture-of-experts` | Sparse routing layer mechanism activating specific expert subnetworks per token. |
| `vae-bottleneck` | `cdx:ai-ml:model:architecture:secondary:vae-bottleneck` | Symmetric compression bottleneck utilizing mean and variance latent vectors. |
| `u-net` | `cdx:ai-ml:model:architecture:secondary:u-net` | Symmetric contracting and expanding macro-layout featuring skip connections between corresponding scales. |
| `residual-connections` | `cdx:ai-ml:model:architecture:secondary:residual-connections` | Explicit skip or identity shortcuts bypassing one or more structural layers. |
| `dual-encoders` | `cdx:ai-ml:model:architecture:secondary:dual-encoders` | Parallel feature extraction pipelines mapping different modalities into a shared space. |
| `cross-attention-gated` | `cdx:ai-ml:model:architecture:secondary:cross-attention-gated` | Explicit sub-component routing that conditions one feature stream using another via attention mechanisms. |
| `siamese-network` | `cdx:ai-ml:model:architecture:secondary:siamese-network` | Twin identical subnetworks sharing identical weights to compute similarity metrics. |
| `hybrid-backbone` | `cdx:ai-ml:model:architecture:secondary:hybrid-backbone` | Direct cascading combination of distinct primary layers (e.g., a CNN feature extractor feeding a Transformer). |
| `state-space-model` | `cdx:ai-ml:model:architecture:secondary:state-space-model` | State space model architectures using selective state spaces for sequence modeling (e.g., Mamba). |
| `flow-matching` | `cdx:ai-ml:model:architecture:secondary:flow-matching` | Flow-based generative model backbone using continuous normalizing flows. |
| `vision-encoder` | `cdx:ai-ml:model:architecture:secondary:vision-encoder` | Vision encoding component for processing image inputs in multimodal architectures (e.g., CLIP, SigLIP). |
| `adapter-layers` | `cdx:ai-ml:model:architecture:secondary:adapter-layers` | Parameter-efficient fine-tuning layers inserted into frozen models (e.g., LoRA, adapters). |
| `projector-layers` | `cdx:ai-ml:model:architecture:secondary:projector-layers` | Cross-modal projection components bridging different modalities (e.g., Q-Former, linear projectors). |
| `gated-linear-units` | `cdx:ai-ml:model:architecture:secondary:gated-linear-units` | Gated activation mechanisms using element-wise multiplication (e.g., GLU, SwiGLU, GeGLU). |
| `speculative-decoding` | `cdx:ai-ml:model:architecture:secondary:speculative-decoding` | Sub-network pairing a small draft model with a large verifier model to accelerate autoregressive generation. |
| `rotary-position-embedding` | `cdx:ai-ml:model:architecture:secondary:rotary-position-embedding` | Rotary Position Embedding (RoPE) sub-component encoding positional information via rotation matrices. |
| `grouped-query-attention` | `cdx:ai-ml:model:architecture:secondary:grouped-query-attention` | Grouped-Query Attention (GQA) variant sharing key/value heads across groups of query heads to reduce KV-cache size. |
| `sliding-window-attention` | `cdx:ai-ml:model:architecture:secondary:sliding-window-attention` | Attention mechanism restricting receptive field to a local sliding window (e.g., Mistral). |
| `retrieval-augmented` | `cdx:ai-ml:model:architecture:secondary:retrieval-augmented` | Explicit retrieval sub-network prepended to or integrated into the model (e.g., RAG, RETRO). |
| `memory-augmented` | `cdx:ai-ml:model:architecture:secondary:memory-augmented` | External or persistent memory bank integrated into the forward pass (e.g., MemGPT, Memorizing Transformers). |
| `multimodal-fusion` | `cdx:ai-ml:model:architecture:secondary:multimodal-fusion` | Layer or block that fuses representations across more than one modality (e.g., cross-modal attention, FiLM conditioning). |
| `reranker` | `cdx:ai-ml:model:architecture:secondary:reranker` | Separate scoring / reranking head applied after an initial retrieval or generation step. |
| _(none)_ | `cdx:ai-ml:model:architecture:secondary:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary secondary architecture name. |

### `cdx:ai-ml:model:architecture:topology` Values

Maps to `structural.topologyType` in the schema. Rows marked have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `dense` | `cdx:ai-ml:model:architecture:topology:dense` | All or most parameters are active during inference with full connectivity between layers. |
| `sparse` | `cdx:ai-ml:model:architecture:topology:sparse` | Only a subset of parameters are active during inference with selective connectivity. |
| `dynamic` | `cdx:ai-ml:model:architecture:topology:dynamic` | Parameter activation and connectivity patterns change based on input or runtime conditions. |
| `liquid` | `cdx:ai-ml:model:architecture:topology:liquid` | Continuously adaptive network structure with time-varying connections and activations. |
| `mixture-of-depths` | `cdx:ai-ml:model:architecture:topology:mixture-of-depths` | Tokens are routed to different computational depths rather than different expert modules. |
| `early-exit` | `cdx:ai-ml:model:architecture:topology:early-exit` | Inference exits at the earliest layer that meets a confidence threshold, reducing compute for easy inputs. |
| `recurrent-hybrid` | `cdx:ai-ml:model:architecture:topology:recurrent-hybrid` | Static layer layout that alternates between global attention and recurrent / SSM layers (e.g., Jamba, Zamba). |
| _(none)_ | `cdx:ai-ml:model:architecture:topology:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary topology type name. |

#### Example: Using built-in and URN-style values together

```jsonc
{
  "components": [{
    "type": "machine-learning-model",
    "name": "my-diffusion-model",
    "modelCard": {
      "modelArchitecture": {
        "structural": {
          "primary": "cdx:ai-ml:model:architecture:primary:diffusion",
          "topologyType": "dense",
          "secondary": [
            "u-net",
            "cdx:ai-ml:model:architecture:secondary:multimodal-fusion"
          ]
        }
      }
    }
  }]
}
```

---

### `cdx:ai-ml:model:task` Namespace Taxonomy

The `cdx:ai-ml:model:task` namespace corresponds to the `modelTaskType` definition in the JSON schema. Each value may be expressed in **two equivalent forms**:

- **Short form** — the plain string from the schema's built-in enum (e.g., `text-generation`).
- **URN-style form** — the fully qualified path (e.g., `cdx:ai-ml:model:task:text-generation`). MUST be used for values not in the built-in enum. Either form MAY be used for built-in values; the short form is preferred for brevity.

Rows marked have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `text-generation` | `cdx:ai-ml:model:task:text-generation` | Generate coherent text continuations from prompts (e.g., GPT models). |
| `text-classification` | `cdx:ai-ml:model:task:text-classification` | Classify text into predefined categories (e.g., sentiment analysis, topic classification). |
| `token-classification` | `cdx:ai-ml:model:task:token-classification` | Classify individual tokens in text (e.g., named entity recognition, part-of-speech tagging). |
| `question-answering` | `cdx:ai-ml:model:task:question-answering` | Answer questions based on context or knowledge (e.g., extractive or generative QA). |
| `summarization` | `cdx:ai-ml:model:task:summarization` | Generate concise summaries of longer text documents. |
| `translation` | `cdx:ai-ml:model:task:translation` | Translate text from one language to another. |
| `text-to-text` | `cdx:ai-ml:model:task:text-to-text` | Transform text from one form to another (e.g., paraphrasing, style transfer). |
| `fill-mask` | `cdx:ai-ml:model:task:fill-mask` | Predict masked tokens in text (e.g., BERT-style masked language modeling). |
| `sentence-similarity` | `cdx:ai-ml:model:task:sentence-similarity` | Compute semantic similarity between text sequences. |
| `text-to-image` | `cdx:ai-ml:model:task:text-to-image` | Generate images from text descriptions (e.g., DALL-E, Stable Diffusion). |
| `text-to-video` | `cdx:ai-ml:model:task:text-to-video` | Generate video content from text descriptions. |
| `text-to-audio` | `cdx:ai-ml:model:task:text-to-audio` | Generate audio or music from text descriptions. |
| `text-to-speech` | `cdx:ai-ml:model:task:text-to-speech` | Convert text to spoken audio (speech synthesis). |
| `image-classification` | `cdx:ai-ml:model:task:image-classification` | Classify images into predefined categories (e.g., ResNet, ViT). |
| `image-segmentation` | `cdx:ai-ml:model:task:image-segmentation` | Segment images into regions or objects (semantic or instance segmentation). |
| `object-detection` | `cdx:ai-ml:model:task:object-detection` | Detect and localize objects in images (e.g., YOLO, R-CNN). |
| `image-to-image` | `cdx:ai-ml:model:task:image-to-image` | Transform images (e.g., style transfer, super-resolution, inpainting). |
| `image-to-text` | `cdx:ai-ml:model:task:image-to-text` | Generate text descriptions from images (e.g., image captioning). |
| `depth-estimation` | `cdx:ai-ml:model:task:depth-estimation` | Estimate depth information from images. |
| `video-classification` | `cdx:ai-ml:model:task:video-classification` | Classify video content into categories. |
| `audio-classification` | `cdx:ai-ml:model:task:audio-classification` | Classify audio into categories (e.g., sound event detection). |
| `automatic-speech-recognition` | `cdx:ai-ml:model:task:automatic-speech-recognition` | Transcribe spoken audio to text (e.g., Whisper). |
| `audio-to-audio` | `cdx:ai-ml:model:task:audio-to-audio` | Transform audio (e.g., noise reduction, voice conversion). |
| `voice-activity-detection` | `cdx:ai-ml:model:task:voice-activity-detection` | Detect presence of speech in audio streams. |
| `tabular-classification` | `cdx:ai-ml:model:task:tabular-classification` | Classify structured tabular data. |
| `tabular-regression` | `cdx:ai-ml:model:task:tabular-regression` | Predict continuous values from structured tabular data. |
| `time-series-forecasting` | `cdx:ai-ml:model:task:time-series-forecasting` | Predict future values in time series data. |
| `reinforcement-learning` | `cdx:ai-ml:model:task:reinforcement-learning` | Learn optimal actions through interaction with an environment. |
| `robotics` | `cdx:ai-ml:model:task:robotics` | Control and decision-making for robotic systems. |
| `graph-ml` | `cdx:ai-ml:model:task:graph-ml` | Machine learning tasks on graph-structured data. |
| `feature-extraction` | `cdx:ai-ml:model:task:feature-extraction` | Extract meaningful features or representations from data. |
| `embedding` | `cdx:ai-ml:model:task:embedding` | Generate dense vector representations of data. |
| `zero-shot-classification` | `cdx:ai-ml:model:task:zero-shot-classification` | Classify data without task-specific training examples. |
| `few-shot-learning` | `cdx:ai-ml:model:task:few-shot-learning` | Learn from very few examples per class. |
| `reasoning` `cdx:ai-ml:model:task:reasoning` | Explicit chain-of-thought or multi-step logical reasoning (e.g., o1, DeepSeek-R1). |
| `code-review` | `cdx:ai-ml:model:task:code-review` | Automated review, critique, and improvement of existing source code. |
| `code-completion` `cdx:ai-ml:model:task:code-completion` | Context-aware in-editor code completion (e.g., Copilot fill-in-the-middle). |
| `document-parsing` | `cdx:ai-ml:model:task:document-parsing` | Extraction of structured data from documents including PDFs, invoices, and forms. |
| `image-to-3d` | `cdx:ai-ml:model:task:image-to-3d` | Generation of 3D representations (NeRF, mesh, point cloud) from one or more 2D images. |
| `text-to-3d` | `cdx:ai-ml:model:task:text-to-3d` | Generation of 3D assets from text descriptions. |
| `multimodal-generation` | `cdx:ai-ml:model:task:multimodal-generation` | Simultaneous generation of content across more than one modality from a single prompt. |
| `agentic-planning` | `cdx:ai-ml:model:task:agentic-planning` | High-level task decomposition and multi-step planning for autonomous agents. |
| `tool-use` | `cdx:ai-ml:model:task:tool-use` | Structured invocation of external tools, APIs, or function calls from model output. |
| `anomaly-detection` |  `cdx:ai-ml:model:task:anomaly-detection` | Identification of outliers or deviations from expected distributions in structured or unstructured data. |
| `pose-estimation` | `cdx:ai-ml:model:task:pose-estimation` | Detection and estimation of body keypoints or object pose from images or video. |
| `optical-flow` | `cdx:ai-ml:model:task:optical-flow` | Per-pixel motion estimation between consecutive video frames. |
| `super-resolution` | `cdx:ai-ml:model:task:super-resolution` | Up-sampling of low-resolution images or video to higher resolution. |
| `inpainting` | `cdx:ai-ml:model:task:inpainting` | Reconstruction of missing or masked regions within an image or video. |
| `molecule-generation` | `cdx:ai-ml:model:task:molecule-generation` | De novo design and generation of molecular structures for drug discovery or materials science. |
| `protein-structure-prediction` | `cdx:ai-ml:model:task:protein-structure-prediction` | Prediction of three-dimensional protein folding from amino acid sequences. |
| `weather-forecasting` | `cdx:ai-ml:model:task:weather-forecasting` | Prediction of atmospheric conditions from observational or reanalysis data. |
| _(none)_ | `cdx:ai-ml:model:task:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary model task type name. |

#### Example: Referencing an extended task type

```jsonc
{
  "components": [{
    "type": "machine-learning-model",
    "name": "my-reasoning-model",
    "modelCard": {
      "modelArchitecture": {
        "tasks": [
          "text-generation",
          "cdx:ai-ml:model:task:reasoning",
          "cdx:ai-ml:model:task:tool-use"
        ]
      }
    }
  }]
}
```

---

### `cdx:ai-ml:model:performance` Namespace Taxonomy

The `cdx:ai-ml:model:performance` namespace corresponds to the `performanceMetric.type` definition in the JSON schema. Each value may be expressed in **two equivalent forms**:

- **Short form** — the plain string from the schema's built-in enum (e.g., `bleu`).
- **URN-style form** — the fully qualified path (e.g., `cdx:ai-ml:model:metric:performance:bleu`). MUST be used for values not in the built-in enum. Either form MAY be used for built-in values; the short form is preferred for brevity.

Rows marked have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `mmlu-pro` | `cdx:ai-ml:model:metric:performance:mmlu-pro` | Massive Multitask Language Understanding Pro — expert-level academic and professional reasoning across multiple disciplines. |
| `gpqa` | `cdx:ai-ml:model:metric:performance:gpqa` | Graduate-Level Google-Proof Q&A — highly difficult dataset for PhD-level reasoning and scientific problem-solving. |
| `math-500` | `cdx:ai-ml:model:metric:performance:math-500` | A subset of the MATH benchmark used to evaluate complex, multi-step mathematical reasoning. |
| `humaneval` | `cdx:ai-ml:model:metric:performance:humaneval` | Industry-standard benchmark for evaluating Python code generation and functional programming synthesis. |
| `swe-bench` | `cdx:ai-ml:model:metric:performance:swe-bench` | Software Engineering Benchmark — evaluates agentic ability to resolve real-world software engineering issues. |
| `ifeval` | `cdx:ai-ml:model:metric:performance:ifeval` | Instruction Following Evaluation — tests strict adherence to verifiable formatting constraints. |
| `livebench` | `cdx:ai-ml:model:metric:performance:livebench` | Frequently updated, contamination-free benchmark for reasoning, math, and coding. |
| `webarena` | `cdx:ai-ml:model:metric:performance:webarena` | Agentic benchmark for complex multi-step tasks using a web browser, APIs, and OS environments. |
| `lmsys-elo` | `cdx:ai-ml:model:metric:performance:lmsys-elo` | Crowd-sourced human preference rating derived from blind A/B battle tests in the LMSYS Chatbot Arena. |
| `strongreject` | `cdx:ai-ml:model:metric:performance:strongreject` | Standardized metric for measuring safety alignment against harmful prompts while avoiding false positives. |
| `perplexity` | `cdx:ai-ml:model:metric:performance:perplexity` | Fundamental language model metric measuring how well a probability model predicts a sample. |
| `bleu` | `cdx:ai-ml:model:metric:performance:bleu` | Bilingual Evaluation Understudy — metric for evaluating machine translation quality. |
| `rouge` | `cdx:ai-ml:model:metric:performance:rouge` | Recall-Oriented Understudy for Gisting Evaluation — metrics for automatic summarization and translation. |
| `latency` | `cdx:ai-ml:model:metric:performance:latency` | Time delay between input submission and output generation, typically measured in milliseconds or seconds. |
| `throughput` | `cdx:ai-ml:model:metric:performance:throughput` | Rate at which a model processes requests or tokens, typically measured in tokens per second or requests per second. |
| `coco` | `cdx:ai-ml:model:metric:performance:coco` | Common Objects in Context — benchmark for object detection, segmentation, and captioning in computer vision. |
| `vqa` | `cdx:ai-ml:model:metric:performance:vqa` | Visual Question Answering — evaluates a model's ability to answer questions about images. |
| `imagenet` | `cdx:ai-ml:model:metric:performance:imagenet` | Large visual database benchmark for image classification and object recognition. |
| `arc` | `cdx:ai-ml:model:metric:performance:arc` | AI2 Reasoning Challenge — multiple-choice science question benchmark measuring commonsense and factual reasoning. |
| `hellaswag` | `cdx:ai-ml:model:metric:performance:hellaswag` | Commonsense NLI benchmark for sentence completion requiring real-world situational reasoning. |
| `truthfulqa` | `cdx:ai-ml:model:metric:performance:truthfulqa` | Benchmark measuring a model's propensity to produce truthful answers versus plausible-sounding falsehoods. |
| `winogrande` | `cdx:ai-ml:model:metric:performance:winogrande` | Large-scale Winograd schema challenge testing commonsense reasoning via pronoun disambiguation. |
| `gsm8k` | `cdx:ai-ml:model:metric:performance:gsm8k` | Grade-school math benchmark measuring multi-step arithmetic reasoning. |
| `mbpp` | `cdx:ai-ml:model:metric:performance:mbpp` | Mostly Basic Python Programming benchmark for code generation via programming problems. |
| `bigbench-hard` | `cdx:ai-ml:model:metric:performance:bigbench-hard` | A subset of BIG-Bench tasks specifically selected for being difficult for current language models. |
| `mmlu` | `cdx:ai-ml:model:metric:performance:mmlu` | Massive Multitask Language Understanding — the original 57-subject academic reasoning benchmark. |
| `mme` | `cdx:ai-ml:model:metric:performance:mme` | Multimodal LLM Evaluation benchmark measuring perception and cognition across image-text pairs. |
| `seedbench` | `cdx:ai-ml:model:metric:performance:seedbench` | SEED-Bench — multimodal benchmark with 19K multiple-choice questions covering spatial and temporal understanding. |
| `mtbench` | `cdx:ai-ml:model:metric:performance:mtbench` | MT-Bench — multi-turn conversational benchmark graded by a strong LLM judge. |
| `agentic-success-rate` | `cdx:ai-ml:model:metric:performance:agentic-success-rate` | Task-completion rate for autonomous agents evaluated on environment-grounded multi-step benchmarks. |
| `bfcl` | `cdx:ai-ml:model:metric:performance:bfcl` | Berkeley Function-Calling Leaderboard — tool/API function-calling accuracy across diverse schemas and languages. |
| `browsecomp` | `cdx:ai-ml:model:metric:performance:browsecomp` | BrowseComp — hard multi-hop web research questions requiring compositional retrieval (OpenAI). |
| `gdpval` | `cdx:ai-ml:model:metric:performance:gdpval` | GDPVal — cross-domain general performance validation benchmark. |
| `taubench` | `cdx:ai-ml:model:metric:performance:taubench` | τ-bench (TauBench) — multi-step tool-augmented agentic task evaluation. |
| `terminal-bench` | `cdx:ai-ml:model:metric:performance:terminal-bench` | Terminal-Bench — long-horizon autonomous shell task completion. |
| `ttft` | `cdx:ai-ml:model:metric:performance:ttft` | Time-to-First-Token — latency from request submission to generation of the first output token. |
| `memory-footprint` | `cdx:ai-ml:model:metric:performance:memory-footprint` | Peak GPU/CPU memory consumption during inference. |
| `f1` | `cdx:ai-ml:model:metric:performance:f1` | Harmonic mean of precision and recall; standard metric for classification and span-extraction tasks. |
| `exact-match` | `cdx:ai-ml:model:metric:performance:exact-match` | Strict string equality between prediction and reference; standard for extractive QA and code generation. |
| `map` | `cdx:ai-ml:model:metric:performance:map` | Mean Average Precision — area-under-precision-recall curve averaged over classes (detection/retrieval). |
| `ndcg` | `cdx:ai-ml:model:metric:performance:ndcg` | Normalised Discounted Cumulative Gain — ranking quality metric used in information retrieval. |
| `wer` | `cdx:ai-ml:model:metric:performance:wer` | Word Error Rate — proportion of incorrectly predicted words; standard metric for ASR systems. |
| `cer` | `cdx:ai-ml:model:metric:performance:cer` | Character Error Rate — character-level analogue of WER; used for OCR and low-resource ASR. |
| `fid` | `cdx:ai-ml:model:metric:performance:fid` | Fréchet Inception Distance — distribution-level similarity metric for generative image quality. |
| `clip-score` | `cdx:ai-ml:model:metric:performance:clip-score` | Cosine similarity between CLIP embeddings of generated images and conditioning text. |
| `power-consumption` | `cdx:ai-ml:model:metric:performance:power-consumption` | Average power draw (watts) during a standardised inference workload. |
| `carbon-intensity` | `cdx:ai-ml:model:metric:performance:carbon-intensity` | gCO₂eq per inference request under a standardised workload and grid carbon intensity. |
| _(none)_ | `cdx:ai-ml:model:metric:performance:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary performance metric name. |

#### Example: Referencing an extended performance metric

```jsonc
{
  "components": [{
    "type": "machine-learning-model",
    "name": "my-asr-model",
    "modelCard": {
      "quantitativeAnalysis": {
        "performanceMetrics": [
          {
            "type": "cdx:ai-ml:model:metric:performance:wer",
            "measure": { "value": 4.2, "unit": "%" }
          },
          {
            "type": "throughput",
            "measure": { "value": 240, "unit": "tokens/s" }
          }
        ]
      }
    }
  }]
}
```

---

### `cdx:ai-ml:tokenizer` Namespace Taxonomy

The following table lists the current set of namespaces in the `cdx:ai-ml:tokenizer` namespace:

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:tokenizer:hyperparameter` | Describe a parameter used to configure a tokenizer. |

### `cdx:ai-ml:tokenizer:hyperparameter` Namespace Taxonomy

Model tokenizers, although generally conforming to small set of industry-acknowledged implementations, often have distinct variants developed to work with a specific model it was used to train.  These tokenizers have their own hyperparameters that can be declared as properties on a CycloneDX component's model card as described for `model:hyperparameter` (above).

Given that there are some commonly agreed-upon tokenizer configuration property names that are found in [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) that are implemented on a [Transformer](https://en.wikipedia.org/wiki/Transformer_(deep_learning)) architecture the following properties are defined for the `cdx:ai-ml:tokenizer:hyperparameter` namespace:

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:tokenizer:hyperparameter:bos_token` | The Beginning-of-Sentence (BOS) token is a special token configured in a tokenizer that signifies the start of an input sequence. (e.g., `"<[end_of_text]>"`)|
| `cdx:ai-ml:tokenizer:hyperparameter:chat_template` | A string representation of the chat template that defines how to format conversational data using the configured tokenizer.|
| `cdx:ai-ml:tokenizer:hyperparameter:errors` | Configures how the tokenizer handles invalid UTF-8 byte sequences or character encoding issues when converting raw text into tokens. Known values include: `strict` (i.e., raise an error), `ignore` and `replace` (invalid token).|
| `cdx:ai-ml:tokenizer:hyperparameter:eos_token` | The End-of-Sentence (BOS) token is a special token configured in a tokenizer to act as a stop signal for text generation. |
| `cdx:ai-ml:tokenizer:hyperparameter:pad_token` | The pad token is a special token configured in a tokenizer to fill in empty spaces in shorter sequences within a batch, ensuring all input sequences have the exact same length. |
| `cdx:ai-ml:tokenizer:hyperparameter:padding_side` | Defines whether the tokenizer adds padding tokens (i.e., the `pad_token`) to the left or right side of a sequence to ensure all sequences in a batch are the same length. Known values are either `left` or `right`. |
| `cdx:ai-ml:tokenizer:hyperparameter:tokenizer_class` | The named tokenizer (class) implementation configured for the model when the tokenizer support multiple possible implementations. |
| `cdx:ai-ml:tokenizer:hyperparameter:unk_token` | The special token configured in a tokenizer to replace any input character or word that is not found in the model's vocabulary. |
| `cdx:ai-ml:tokenizer:hyperparameter:vocab_size` | The configured size of the token vocabulary. Please note this value SHOULD match the `vocab_size` model hyperparameter value if both are declared on the same model card. |
| `cdx:ai-ml:tokenizer:hyperparameter:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary tokenizer hyperparameter name. Arbitrarty value and meaning. |

Each well-known property MAY be used once, if not stated otherwise.

#### Tokenizer hyperparameter notes

- If the `cdx:ai-ml:model:hyperparameter:tokenizer_class` hyperparameter value is declared, the `cdx:ai-ml:tokenizer:hyperparameter:tokenizer_class` value SHOULD match.
- Tokenizer hyperparameter values should be compatible with the tokenizer class implementation (value) provided on the `tokenizer_class` hyperparameter.
- Tokenizer hyperparameters that configure special token such as `bos_token`, `eos_token`, `pad_token`, etc. often utilize a distinct syntax such as the `<|` and `|>` that delineates them from other tokens (e.g., `<|im_start|>`, `<|pad_id|>`, `<|end_of_text|>`).

#### Example: Using tokenizer hyperparameter names listed in the AI/ML taxonomy

The following pseudocode shows how you would include the defined (reserved) `eos_token` and `vocab_size` tokenizer hyperparameters on an ML model's model card:

```jsonc
{
  // ...
  "components": [{
    "type": "library",
    "name": "tokenization.py",
    // ...
    "properties": [
      {
          "name": "cdx:ai-ml:model:tokenizer",
          "value": "LLMTokenizer"
      },
      {
          "name": "cdx:ai-ml:tokenizer:hyperparameter:eos_token",
          "value": "<|end_of_text|>"
      },
      {
          "name": "cdx:ai-ml:tokenizer:parameter:vocab_size",
          "value": "152064"
      }
    ]
  }]
}
```

> **Note**: The `cdx:ai-ml:model:tokenizer` asserts (or tags) the associated component as a tokenizer with the implementation `LLMTokenizer` as the value before providing its hyperparameters.

#### Example: Using an unlisted tokenizer hyperparameter name

In the same way as shown in the model's `hyperparameter` example, the following pseudocode shows how you would include a tokenizer hyperparameter that is not currently listed in the AI/ML namespace taxonomy.  Below, we introduce the metasyntactic hyperparameter name `baz` with a value `qux`.

```jsonc
{
  // ...
  "components": [{
    "type": "library",
    "name": "tokenization.py",
    // ...
    "properties": [
      {
        "name": "cdx:ai-ml:model:tokenizer",
        "value": "LLMTokenizer"
      },
      {
        "name": "cdx:ai-ml:tokenizer:hyperparameter:_undefined:baz",
        "value": "qux"
      }
    ]
  }]
}
```

---

## `cdx:ai-ml:dataset` Namespace Taxonomy

The `cdx:ai-ml:dataset` namespace provides standardised properties for describing training and evaluation datasets referenced in an AI/ML BOM. These properties are designed to be placed on `data` components (or any component representing a dataset) within the `components` array.

The following are the reserved property names in the `cdx:ai-ml:dataset` namespace:

| Property | Description |
| -------- | ----------- |
| `cdx:ai-ml:dataset:stage` | The training pipeline stage in which this dataset was used. Value SHOULD be one of the [stage values listed below](#cdxai-mldatasetstage-values). This property MAY appear multiple times when the same dataset is used across more than one stage. Per-stage usage detail (e.g. subset, sampling configuration) SHOULD be described in a CycloneDX formula. |
| `cdx:ai-ml:dataset:category` | The content category or domain of the dataset. Value SHOULD be one of the [category values listed below](#cdxai-mldatasetcategory-values). This property MAY appear multiple times. |
| `cdx:ai-ml:dataset:date_obtained` | The date on which the dataset was obtained or ingested. Value MUST be a valid [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date string (e.g. `2024-03-15`). This property MAY appear once. |
| `cdx:ai-ml:dataset:size` | The storage size of the dataset as a human-readable string with a unit suffix (e.g. `420 GB`, `1.2 TB`). This property MAY appear once. |
| `cdx:ai-ml:dataset:languages` | The natural language(s) present in the dataset. Value MUST be a single [BCP-47](https://www.rfc-editor.org/rfc/rfc5646) language tag (e.g. `en`) or a comma-separated list of BCP-47 tags (e.g. `en,ja,de,fr`). The sentinel value `multilingual` MAY be used when the dataset spans a large number of languages and enumeration is impractical. This property MAY appear once. |
| `cdx:ai-ml:dataset:data:sources` | The EU AI Act data source category or categories that describe how the dataset was obtained. Value SHOULD be one of the [data sources values listed below](#cdxai-mldatasetdatasources-values). This property MAY appear multiple times when the dataset spans more than one source category. |
| `cdx:ai-ml:dataset:seed_data` | Indicates whether this dataset was used as seed data for generating a synthetic or derived dataset. _Boolean value_. This property MAY appear once. |
| `cdx:ai-ml:dataset:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary dataset property name. Arbitrary value and meaning. |

---

### `cdx:ai-ml:dataset:stage` Values

A dataset component MAY carry more than one `cdx:ai-ml:dataset:stage` property when it participates in multiple pipeline stages. When the specific configuration, subset, or sampling ratio differs between stages, those details SHOULD be captured in the CycloneDX `formulation` field as discrete training tasks referencing this component by its `bom-ref`.

| Value | Description |
| ----- | ----------- |
| `pre-training` | Dataset used during the initial large-scale pre-training stage. |
| `post-training` | Dataset used during any stage after pre-training, including supervised fine-tuning, Reinforcement Learning from Human Feedback (RLHF), alignment, or instruction tuning. |
| `fine-tuning` | Dataset used during a task-specific or domain-specific fine-tuning stage. |
| `evaluation` | Dataset used exclusively for model evaluation or benchmarking; not used during training. |
| `_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary training stage name. |

---

### `cdx:ai-ml:dataset:category` Values

| Value | Description |
| ----- | ----------- |
| `code` | Source code, programming examples, or software-related text. |
| `web` | Content sourced from web crawls or scraped web pages. |
| `math` | Mathematical texts, proofs, problems, and solutions. |
| `multilingual` | Content spanning multiple natural languages without a single dominant language. |
| `domain` | Specialised domain knowledge (e.g., scientific literature, legal text, medical records). |
| `instructions` | Instruction-following examples, prompt–response pairs, or chat conversation data. |
| `technical` | Technical documentation, manuals, or structured reference material. |
| `books` | Long-form prose from books, novels, or other published works. |
| `academic` | Academic papers, preprints, or scholarly publications. |
| `news` | News articles or journalistic content. |
| `_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary dataset category name. |

---

### `cdx:ai-ml:dataset:data:sources` Values

Corresponds to the data source categories defined in Section 2 ("Lists of data sources") of the EU AI Act Annex XI template (Article 53 of the EU AI Act). The `cdx:ai-ml:dataset:data:sources` property answers the question: *how or where was this data originally collected?* A dataset component MAY carry more than one `cdx:ai-ml:dataset:data:sources` property when the dataset is assembled from multiple source categories.

| Value | Description |
| ----- | ----------- |
| `publicly-available` | Dataset obtained from a publicly accessible repository, open release, or other public source. |
| `third-party-private` | Dataset obtained from a third party that is not publicly accessible. |
| `web-crawl` | Data collected via automated crawling or scraping of publicly accessible web content. |
| `user-data` | Data originating from real human user interactions or direct user capture (e.g., feedback, conversations, user-generated content). |
| `synthetic` | Data that was synthetically generated and is not derived directly from real-world observations. |
| `other` | Data sourced through means not covered by the categories above. |
| `_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary source designation. |

---

### Example: Annotating a pre-training dataset component

The following pseudocode shows how the `cdx:ai-ml:dataset` properties would be applied to a dataset component in the `components` array of a CycloneDX BOM.

```jsonc
{
  // ...
  "components": [{
    "type": "data",
    "bom-ref": "dataset--GneissWeb",
    "name": "GneissWeb",
    "description": "Large-scale English web text corpus curated from Common Crawl with quality filtering.",
    "externalReferences": [{
      "type": "distribution",
      "url": "https://huggingface.co/datasets/ibm-granite/GneissWeb"
    }],
    "properties": [
      {
        "name": "cdx:ai-ml:dataset:stage",
        "value": "pre-training"
      },
      {
        "name": "cdx:ai-ml:dataset:category",
        "value": "web"
      },
      {
        "name": "cdx:ai-ml:dataset:languages",
        "value": "en"
      },
      {
        "name": "cdx:ai-ml:dataset:size",
        "value": "9.6 TB"
      },
      {
        "name": "cdx:ai-ml:dataset:date_obtained",
        "value": "2024-06-01"
      },
      {
        "name": "cdx:ai-ml:dataset:data:sources",
        "value": "publicly-available"
      },
      {
        "name": "cdx:ai-ml:dataset:data:sources",
        "value": "web-crawl"
      },
      {
        "name": "cdx:ai-ml:dataset:seed_data",
        "value": "false"
      }
    ]
  }]
}
```

### Example: Annotating a synthetic post-training dataset

```jsonc
{
  // ...
  "components": [{
    "type": "data",
    "bom-ref": "dataset--NuminaMath-CoT",
    "name": "NuminaMath-CoT",
    "description": "Chain-of-thought math reasoning dataset synthetically generated from seed problems.",
    "externalReferences": [{
      "type": "distribution",
      "url": "https://huggingface.co/datasets/AI-MO/NuminaMath-CoT"
    }],
    "properties": [
      {
        "name": "cdx:ai-ml:dataset:stage",
        "value": "post-training"
      },
      {
        "name": "cdx:ai-ml:dataset:category",
        "value": "math"
      },
      {
        "name": "cdx:ai-ml:dataset:languages",
        "value": "en"
      },
      {
        "name": "cdx:ai-ml:dataset:data:sources",
        "value": "publicly-available"
      },
      {
        "name": "cdx:ai-ml:dataset:data:sources",
        "value": "synthetic"
      },
      {
        "name": "cdx:ai-ml:dataset:seed_data",
        "value": "false"
      }
    ]
  }]
}
```

### Example: Using an unlisted dataset property name

The following pseudocode shows how to include a dataset property that is not currently listed in the `cdx:ai-ml:dataset` namespace taxonomy. Below, we introduce the metasyntactic property name `foo` with a value `bar`.

```jsonc
{
  // ...
  "components": [{
    "type": "data",
    "name": "my-dataset",
    "properties": [
      {
        "name": "cdx:ai-ml:dataset:_undefined:foo",
        "value": "bar"
      }
    ]
  }]
}
```
