# UBC GenAI Toolkit - Embeddings Module

## Overview

This module provides a standardized interface for generating text embeddings. It uses the Facade pattern to simplify the process of creating vector representations of text, which are essential for tasks like semantic search, retrieval-augmented generation (RAG), and text clustering.

This module currently uses `fastembed` to generate embeddings locally.

## Installation

```bash
npm install ubc-genai-toolkit-embeddings ubc-genai-toolkit-core
```

## Core Concepts

-   **`EmbeddingsModule`**: The main class and entry point for generating embeddings.
-   **`EmbeddingsConfig`**: An interface for configuring the module, such as specifying the model to use.
-   **`EmbeddingsResponse`**: A standardized response format containing the generated embeddings and usage statistics.

## Configuration

The `EmbeddingsModule` is configured during instantiation with an `EmbeddingsConfig` object.

```typescript
import {
	EmbeddingsModule,
	EmbeddingsConfig,
} from 'ubc-genai-toolkit-embeddings';
import { ConsoleLogger } from 'ubc-genai-toolkit-core'; // Example logger

// General Structure
interface EmbeddingsConfig {
	model: string; // Specify the model to use for embeddings
	logger?: LoggerInterface; // Optional: Provide a logger instance
}

// Example Configuration
const embeddingsConfig: EmbeddingsConfig = {
	model: 'sentence-transformers/all-MiniLM-L6-v2', // Example model
	logger: new ConsoleLogger(),
};

// Instantiate the module
const embeddings = new EmbeddingsModule(embeddingsConfig);
```

## Usage Examples

### Initialization

```typescript
import { EmbeddingsModule } from 'ubc-genai-toolkit-embeddings';
import { ConsoleLogger } from 'ubc-genai-toolkit-core';

const config: EmbeddingsConfig = {
	model: 'sentence-transformers/all-MiniLM-L6-v2',
	logger: new ConsoleLogger(),
};

const embeddings = new EmbeddingsModule(config);
```

### Creating a single embedding

```typescript
async function generateEmbedding(text: string) {
	try {
		const response = await embeddings.create(text);
		console.log('Embedding:', response.embedding);
		console.log('Usage:', response.usage);
	} catch (error) {
		console.error('Error sending message:', error);
	}
}

generateEmbedding('This is a test sentence.');
```

### Creating embeddings for a batch of documents

```typescript
async function generateBatchEmbeddings(documents: string[]) {
	try {
		const response = await embeddings.create(documents);
		console.log('Embeddings:', response.embeddings);
		console.log('Usage:', response.usage);
	} catch (error) {
		console.error('Error sending message:', error);
	}
}

generateBatchEmbeddings([
	'This is the first document.',
	'This is the second document.',
]);
```

## Error Handling

The module uses the common error types from `ubc-genai-toolkit-core`.
