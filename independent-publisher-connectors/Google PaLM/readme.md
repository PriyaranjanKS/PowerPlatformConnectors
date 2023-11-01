# Google PaLM

## Publisher

Name: Priyaranjan KS

## Overview
The Google Palm API offers advanced text generation and manipulation capabilities. This documentation covers the endpoints, their parameters, and other essential details.

## API Information
- **Swagger Version**: 2.0
- **API Version**: 1.0
- **API Title**: Google Text Generation API
- **Host**: generativelanguage.googleapis.com
- **Base Path**: /
- **Schemes**: HTTPS
- **Consumes**: application/json
- **Produces**: application/json

## Security
### Obtaining an API Key

To start using the PaLM API, you need to obtain an API key. Follow these steps to get your API key:

1. **Visit the API Key Generation Page**
   - Go to [Google MakerSuite](https://makersuite.google.com/app/apikey) to access the API key generation interface.

2. **Create API Key**
   - Once on the page, you have two options:
     - **Create API Key in New Project**: Select this if you want to create a new project for your API key.
     - **Create API Key in Existing Project**: Choose this if you prefer to use an existing project for your API key.

By following these steps, you will obtain an API key that is required to authenticate and use the PaLM API.

**Note**: Ensure to keep your API key secure and do not share it publicly.

## Endpoints

### 1. List Models
#### GET `/v1beta2/models`
Retrieves a list of available models for text generation.

#### Parameters
| Name       | Optional | Description                             |
|------------|----------|-----------------------------------------|
| `pageSize` | Yes      | The maximum number of models to return. |
| `pageToken`| Yes      | A token for pagination across multiple pages. |

### 2. Get Model
#### GET `/v1beta2/models/{name}`
Retrieves the details of a specific model.

#### Parameters
| Name  | Optional | Description                             |
|-------|----------|-----------------------------------------|
| `name`| No       | The unique identifier of the model.     |

### 3. Generate Text
#### POST `/v1beta2/{modelType}/{modelName}:generateText`
Generates text based on a provided prompt.

#### Path Parameters
| Name        | Optional | Description                       |
|-------------|----------|-----------------------------------|
| `modelType` | No       | The type of the model.            |
| `modelName` | No       | The name of the model.            |

#### Request Body Parameters
| Name              | Optional | Description                                       |
|-------------------|----------|---------------------------------------------------|
| `prompt`          | No       | The input text prompt.                            |
| `safetySettings`  | Yes      | Settings for filtering unsafe content.            |
| `stopSequences`   | Yes      | Sequences that signal the end of text generation. |
| `temperature`     | Yes      | Controls the randomness of generated text.        |
| `candidateCount`  | Yes      | Number of response options to generate.           |
| `maxOutputTokens` | Yes      | The maximum size of the generated text.           |
| `topP`            | Yes      | Cumulative probability for token selection.       |
| `topK`            | Yes      | The number of top tokens to consider during generation. |

### 4. Generate Message
#### POST `/v1beta2/models/{model}:generateMessage`
Generates a response message based on the input prompt.

#### Path Parameters
| Name   | Optional | Description                       |
|--------|----------|-----------------------------------|
| `model`| No       | The name of the model.            |

#### Request Body Parameters
| Name        | Optional | Description                                   |
|-------------|----------|-----------------------------------------------|
| `prompt`    | No       | The structured textual input given as a prompt. |
| `context`   | Yes      | Additional input provided to the model.      |
| `temperature`| Yes     | Controls the randomness of the output.       |
| `topP`      | Yes      | Cumulative probability for token selection.  |
| `topK`      | Yes      | The number of top tokens to consider during sampling. |

### 5. Update Model
#### PUT `/v1beta2/models/{model}`
Updates the specified model's details.

#### Path Parameters
| Name   | Optional | Description                       |
|--------|----------|-----------------------------------|
| `model`| No       | The identifier of the model to update. |

#### Request Body Parameters
| Name        | Optional | Description                                   |
|-------------|----------|-----------------------------------------------|
| `description` | Yes    | A detailed description of the model.         |
| `parameters`  | Yes    | The updated parameters for the model.        |

### 6. Delete Model
#### DELETE `/v1beta2/models/{model}`
Deletes a specific model.

#### Path Parameters
| Name   | Optional | Description                       |
|--------|----------|-----------------------------------|
| `model`| No       | The identifier of the model to delete. |

*Please replace `{model}`, `{modelName}`, and `{modelType}` with appropriate values as per your use case.*


## Known Issues and Limitations
The PaLM API has several limitations which users should be aware of:

1. **Edge Cases**
   - The API may struggle with rare or unusual situations that are not well-represented in the training data.
   - This can lead to issues like model overconfidence, misinterpretation of context, or inappropriate outputs.

2. **Model Hallucinations, Grounding, and Factuality**
   - The API can lack grounding in real-world knowledge, leading to outputs that are plausible but factually incorrect, irrelevant, or nonsensical.

3. **Data Quality and Tuning**
   - The performance of the API is heavily dependent on the quality and accuracy of the input data.
   - Inaccurate or biased input data can lead to suboptimal performance or false model outputs.

4. **Bias Amplification**
   - The API may inadvertently amplify existing biases in the training data, leading to outputs that reinforce societal prejudices.

5. **Language Quality**
   - The API's multilingual capabilities are stronger in English, with potential for reduced performance in non-English languages or less-represented English dialects.
   - Fairness evaluations are primarily conducted in English, which may not cover all potential biases in other languages.

6. **Limited Domain Expertise**
   - The API may not provide accurate or detailed responses on highly specialized or technical topics.
   - For complex use cases, domain-specific tuning and human supervision are recommended.

7. **Length and Structure of Inputs and Outputs**
   - The API has a maximum input token limit of 8k and output token limit of 1k.
   - Safety classifiers are not applied if these limits are exceeded, potentially leading to poor model performance.
   - The API's performance can be affected by inputs with unusual or complex structures.
---