# `cdx:ai-ml` Namespace Taxonomy

This is the namespace for official CycloneDX properties specific to the Artificial Intelligence (AI) and Machine Learning (ML).

The official rules and processes apply - see [parent document](../cdx.md).

----

The following are the reserved namespaces for AI/ML under the `cdx:ai-ml` namespace.

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:model` | Model-related properties. |
| `cdx:ai-ml:tokenizer` | Tokenizer-related properties. |
| `cdx:ai-ml:prompt` | Prompt-related properties. |

_Boolean value_ are `true` or `false`; case sensitive.

---

> **📌 Proposed additions (2.0-dev-ai-ml):** This document extends the original `ai-ml.md` with new namespace sections that correspond to extensible `^cdx:ai-ml:` pattern fields in the CycloneDX v2.0 AI/ML JSON Schema. Sections and values marked **[PROPOSED]** are candidates for formal registration in the property taxonomy and for use as `cdx:ai-ml:` URN-style values inside the schema's `anyOf` enum+pattern fields.

---

## `cdx:ai-ml:model` Namespace Taxonomy

| Namespace | Description |
| --------- | ----------- |
| `cdx:ai-ml:model:modality` | Provide the modality/modalities the model supports. This describes the specific type(s) or format(s) of data the model is designed to process such as text, images, audio, video, or sensor data. |
| `cdx:ai-ml:model:template` | Mark a model as a template and describe its details. |
| `cdx:ai-ml:model:parameter` | Describe learned parameters of a model which dictated by the model's architecture and design before training. |
| `cdx:ai-ml:model:hyperparameter` | Describe parameters used to configure a model. |
| `cdx:ai-ml:model:architecture` | **[PROPOSED]** Describe the structural and behavioral architecture of the model. Maps directly to the `modelArchitecture.structural` object in the JSON schema. |
| `cdx:ai-ml:model:task` | **[PROPOSED]** Describe the ML task the model is designed to perform. Maps to the `modelTaskType` definition in the JSON schema. |
| `cdx:ai-ml:model:performance` | **[PROPOSED]** Describe performance metrics associated with the model. Maps to the `performanceMetric.type` definition in the JSON schema. |

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
| `cdx:ai-ml:model:tokenizer` | Mark a component as a (model) tokenizer. _Boolean value_. </br> This property MAY appear once. |
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
| `cdx:ai-ml:model:parameter:count` | Total number of learned parameters for the model. This reflects the model's design and structure (e.g., number of layers in a neural network, nodes, and connectivity). </br> The value SHOULD use the industry-standard naming convention of number followed by one of the letters: `M` (Million), `B` (Billion) or `T` (Trillion). May appear once. |
| `cdx:ai-ml:model:parameter:tune_method` | Describes how the model was fine-tuned on or adapted to new data. This property MAY appear multiple times. Value SHOULD be of industry-standard keywords such as those [listed in the section below](#names-of-industry-standard-fine-tuning-methods). Value MUST be a single keyword (e.g., `lora`) or a comma separated list of keywords (e.g., `sft,rlhf`). </br> This property MAY occur multiple times. |
| `cdx:ai-ml:model:parameter:_undefined:<NAME>` | `<NAME>` placeholder, used to provide an arbitrary model parameter name. Arbitrarty value and meaning. |

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

## **[PROPOSED]** `cdx:ai-ml:model:architecture` Namespace Taxonomy

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

Maps to `structural.primary` in the schema. The **Short form** column is the built-in schema enum value; the **URN-style form** column is the equivalent fully-qualified property taxonomy value. Rows marked **[PROPOSED]** have no built-in enum equivalent and MUST use the URN-style form.

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
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:diffusion` | Denoising diffusion probabilistic model — iteratively refines noise into data (e.g., DDPM, Stable Diffusion). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:flow-matching` | Continuous normalizing flow trained via flow matching / rectified flow (e.g., Flux, SD3). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:rbm` | Restricted Boltzmann Machine — energy-based generative model with stochastic hidden units. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:capsnet` | Capsule Network — architecture using dynamic routing between capsule groups to preserve spatial hierarchies. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:neuromorphic` | Architecture designed for deployment on neuromorphic hardware (e.g., Intel Loihi, IBM TrueNorth). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:primary:hybrid` | Explicit first-class combination of two or more distinct primary architectures (e.g., CNN+Transformer). |

### `cdx:ai-ml:model:architecture:secondary` Values

Maps to items in `structural.secondary` in the schema. Rows marked **[PROPOSED]** have no built-in enum equivalent and MUST use the URN-style form.

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
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:speculative-decoding` | Sub-network pairing a small draft model with a large verifier model to accelerate autoregressive generation. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:rotary-position-embedding` | Rotary Position Embedding (RoPE) sub-component encoding positional information via rotation matrices. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:grouped-query-attention` | Grouped-Query Attention (GQA) variant sharing key/value heads across groups of query heads to reduce KV-cache size. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:sliding-window-attention` | Attention mechanism restricting receptive field to a local sliding window (e.g., Mistral). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:retrieval-augmented` | Explicit retrieval sub-network prepended to or integrated into the model (e.g., RAG, RETRO). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:memory-augmented` | External or persistent memory bank integrated into the forward pass (e.g., MemGPT, Memorizing Transformers). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:multimodal-fusion` | Layer or block that fuses representations across more than one modality (e.g., cross-modal attention, FiLM conditioning). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:secondary:reranker` | Separate scoring / reranking head applied after an initial retrieval or generation step. |

### `cdx:ai-ml:model:architecture:topology` Values

Maps to `structural.topologyType` in the schema. Rows marked **[PROPOSED]** have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `dense` | `cdx:ai-ml:model:architecture:topology:dense` | All or most parameters are active during inference with full connectivity between layers. |
| `sparse` | `cdx:ai-ml:model:architecture:topology:sparse` | Only a subset of parameters are active during inference with selective connectivity. |
| `dynamic` | `cdx:ai-ml:model:architecture:topology:dynamic` | Parameter activation and connectivity patterns change based on input or runtime conditions. |
| `liquid` | `cdx:ai-ml:model:architecture:topology:liquid` | Continuously adaptive network structure with time-varying connections and activations. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:topology:mixture-of-depths` | Tokens are routed to different computational depths rather than different expert modules. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:topology:early-exit` | Inference exits at the earliest layer that meets a confidence threshold, reducing compute for easy inputs. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:architecture:topology:recurrent-hybrid` | Static layer layout that alternates between global attention and recurrent / SSM layers (e.g., Jamba, Zamba). |

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

### **[PROPOSED]** `cdx:ai-ml:model:task` Namespace Taxonomy

The `cdx:ai-ml:model:task` namespace corresponds to the `modelTaskType` definition in the JSON schema. Each value may be expressed in **two equivalent forms**:

- **Short form** — the plain string from the schema's built-in enum (e.g., `text-generation`).
- **URN-style form** — the fully qualified path (e.g., `cdx:ai-ml:model:task:text-generation`). MUST be used for values not in the built-in enum. Either form MAY be used for built-in values; the short form is preferred for brevity.

Rows marked **[PROPOSED]** have no built-in enum equivalent and MUST use the URN-style form.

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
| `other` | `cdx:ai-ml:model:task:other` | Other machine learning tasks not covered by predefined categories. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:reasoning` | Explicit chain-of-thought or multi-step logical reasoning (e.g., o1, DeepSeek-R1). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:code-review` | Automated review, critique, and improvement of existing source code. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:code-completion` | Context-aware in-editor code completion (e.g., Copilot fill-in-the-middle). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:document-parsing` | Extraction of structured data from documents including PDFs, invoices, and forms. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:image-to-3d` | Generation of 3D representations (NeRF, mesh, point cloud) from one or more 2D images. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:text-to-3d` | Generation of 3D assets from text descriptions. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:multimodal-generation` | Simultaneous generation of content across more than one modality from a single prompt. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:agentic-planning` | High-level task decomposition and multi-step planning for autonomous agents. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:tool-use` | Structured invocation of external tools, APIs, or function calls from model output. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:anomaly-detection` | Identification of outliers or deviations from expected distributions in structured or unstructured data. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:pose-estimation` | Detection and estimation of body keypoints or object pose from images or video. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:optical-flow` | Per-pixel motion estimation between consecutive video frames. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:super-resolution` | Up-sampling of low-resolution images or video to higher resolution. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:inpainting` | Reconstruction of missing or masked regions within an image or video. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:molecule-generation` | De novo design and generation of molecular structures for drug discovery or materials science. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:protein-structure-prediction` | Prediction of three-dimensional protein folding from amino acid sequences. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:task:weather-forecasting` | Prediction of atmospheric conditions from observational or reanalysis data. |

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

### **[PROPOSED]** `cdx:ai-ml:model:performance` Namespace Taxonomy

The `cdx:ai-ml:model:performance` namespace corresponds to the `performanceMetric.type` definition in the JSON schema. Each value may be expressed in **two equivalent forms**:

- **Short form** — the plain string from the schema's built-in enum (e.g., `bleu`).
- **URN-style form** — the fully qualified path (e.g., `cdx:ai-ml:model:performance:metric:bleu`). MUST be used for values not in the built-in enum. Either form MAY be used for built-in values; the short form is preferred for brevity.

Rows marked **[PROPOSED]** have no built-in enum equivalent and MUST use the URN-style form.

| Short form | URN-style form | Description |
| ---------- | -------------- | ----------- |
| `mmlu-pro` | `cdx:ai-ml:model:performance:metric:mmlu-pro` | Massive Multitask Language Understanding Pro — expert-level academic and professional reasoning across multiple disciplines. |
| `gpqa` | `cdx:ai-ml:model:performance:metric:gpqa` | Graduate-Level Google-Proof Q&A — highly difficult dataset for PhD-level reasoning and scientific problem-solving. |
| `math-500` | `cdx:ai-ml:model:performance:metric:math-500` | A subset of the MATH benchmark used to evaluate complex, multi-step mathematical reasoning. |
| `humaneval` | `cdx:ai-ml:model:performance:metric:humaneval` | Industry-standard benchmark for evaluating Python code generation and functional programming synthesis. |
| `swe-bench` | `cdx:ai-ml:model:performance:metric:swe-bench` | Software Engineering Benchmark — evaluates agentic ability to resolve real-world software engineering issues. |
| `ifeval` | `cdx:ai-ml:model:performance:metric:ifeval` | Instruction Following Evaluation — tests strict adherence to verifiable formatting constraints. |
| `livebench` | `cdx:ai-ml:model:performance:metric:livebench` | Frequently updated, contamination-free benchmark for reasoning, math, and coding. |
| `webarena` | `cdx:ai-ml:model:performance:metric:webarena` | Agentic benchmark for complex multi-step tasks using a web browser, APIs, and OS environments. |
| `lmsys-elo` | `cdx:ai-ml:model:performance:metric:lmsys-elo` | Crowd-sourced human preference rating derived from blind A/B battle tests in the LMSYS Chatbot Arena. |
| `strongreject` | `cdx:ai-ml:model:performance:metric:strongreject` | Standardized metric for measuring safety alignment against harmful prompts while avoiding false positives. |
| `perplexity` | `cdx:ai-ml:model:performance:metric:perplexity` | Fundamental language model metric measuring how well a probability model predicts a sample. |
| `bleu` | `cdx:ai-ml:model:performance:metric:bleu` | Bilingual Evaluation Understudy — metric for evaluating machine translation quality. |
| `rouge` | `cdx:ai-ml:model:performance:metric:rouge` | Recall-Oriented Understudy for Gisting Evaluation — metrics for automatic summarization and translation. |
| `latency` | `cdx:ai-ml:model:performance:metric:latency` | Time delay between input submission and output generation, typically measured in milliseconds or seconds. |
| `throughput` | `cdx:ai-ml:model:performance:metric:throughput` | Rate at which a model processes requests or tokens, typically measured in tokens per second or requests per second. |
| `coco` | `cdx:ai-ml:model:performance:metric:coco` | Common Objects in Context — benchmark for object detection, segmentation, and captioning in computer vision. |
| `vqa` | `cdx:ai-ml:model:performance:metric:vqa` | Visual Question Answering — evaluates a model's ability to answer questions about images. |
| `imagenet` | `cdx:ai-ml:model:performance:metric:imagenet` | Large visual database benchmark for image classification and object recognition. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:arc` | AI2 Reasoning Challenge — multiple-choice science question benchmark measuring commonsense and factual reasoning. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:hellaswag` | Commonsense NLI benchmark for sentence completion requiring real-world situational reasoning. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:truthfulqa` | Benchmark measuring a model's propensity to produce truthful answers versus plausible-sounding falsehoods. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:winogrande` | Large-scale Winograd schema challenge testing commonsense reasoning via pronoun disambiguation. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:gsm8k` | Grade-school math benchmark measuring multi-step arithmetic reasoning. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:mbpp` | Mostly Basic Python Programming benchmark for code generation via programming problems. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:bigbench-hard` | A subset of BIG-Bench tasks specifically selected for being difficult for current language models. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:mmlu` | Massive Multitask Language Understanding — the original 57-subject academic reasoning benchmark. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:mme` | Multimodal LLM Evaluation benchmark measuring perception and cognition across image-text pairs. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:seedbench` | SEED-Bench — multimodal benchmark with 19K multiple-choice questions covering spatial and temporal understanding. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:mtbench` | MT-Bench — multi-turn conversational benchmark graded by a strong LLM judge. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:agentic-success-rate` | Task-completion rate for autonomous agents evaluated on environment-grounded multi-step benchmarks. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:ttft` | Time-to-First-Token — latency from request submission to generation of the first output token. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:memory-footprint` | Peak GPU/CPU memory consumption during inference. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:f1` | Harmonic mean of precision and recall; standard metric for classification and span-extraction tasks. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:exact-match` | Strict string equality between prediction and reference; standard for extractive QA and code generation. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:map` | Mean Average Precision — area-under-precision-recall curve averaged over classes (detection/retrieval). |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:ndcg` | Normalised Discounted Cumulative Gain — ranking quality metric used in information retrieval. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:wer` | Word Error Rate — proportion of incorrectly predicted words; standard metric for ASR systems. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:cer` | Character Error Rate — character-level analogue of WER; used for OCR and low-resource ASR. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:fid` | Fréchet Inception Distance — distribution-level similarity metric for generative image quality. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:clip-score` | Cosine similarity between CLIP embeddings of generated images and conditioning text. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:power-consumption` | Average power draw (watts) during a standardised inference workload. |
| _(none)_ **[PROPOSED]** | `cdx:ai-ml:model:performance:metric:carbon-intensity` | gCO₂eq per inference request under a standardised workload and grid carbon intensity. |

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
            "type": "cdx:ai-ml:model:performance:metric:wer",
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

* If the `cdx:ai-ml:model:hyperparameter:tokenizer_class` hyperparameter value is declared, the `cdx:ai-ml:tokenizer:hyperparameter:tokenizer_class` value SHOULD match.
* Tokenizer hyperparameter values should be compatible with the tokenizer class implementation (value) provided on the `tokenizer_class` hyperparameter.
* Tokenizer hyperparameters that configure special token such as `bos_token`, `eos_token`, `pad_token`, etc. often utilize a distinct syntax such as the `<|` and `|>` that delineates them from other tokens (e.g., `<|im_start|>`, `<|pad_id|>`, `<|end_of_text|>`).

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
