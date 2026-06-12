# ML-KEM with AI

This directory contains a collection of experiments, prompts, and evaluations focused on the capabilities of various Large Language Models (LLMs) to understand, explain, and implement **ML-KEM** (Module-Lattice-based Key Encapsulation Mechanism), also known as **Kyber**.

ML-KEM is the NIST standard for post-quantum key exchange, designed to secure communications against potential attacks from future quantum computers.

## 📂 Contents

The files in this directory are primarily markdown (`.md`) and text (`.txt`) files documenting the interactions with different models:

- **Model Evaluations**: Files named after specific models (e.g., `gemma-31b-4bit`, `qwen-27b`, `qwen-opus-40b`) containing prompts and the resulting explanations of ML-KEM.
- **Code Implementations**: Files prefixed with `code-` (e.g., `code-gemma-31b-4bit-mlkem512.md`) which showcase the model's ability to generate code for ML-KEM operations.
- **Quantization Experiments**: Documentation on how different quantization levels (e.g., `4bit`, `5bit`, `mxfp8`) affect the model's reasoning and technical accuracy.

## 🎯 Goal

The objective of this research is to determine:
1. Which LLMs provide the most mathematically accurate explanations of lattice-based cryptography.
2. How quantization impacts the "reasoning" capabilities of models when dealing with complex cryptographic specifications.
3. The effectiveness of different model architectures (Gemma, Qwen, etc.) in implementing the ML-KEM standard.

## 🛠️ Usage

To explore the results, simply open the `.md` files. Most files follow a pattern of:
- **Prompt**: The specific question asked to the AI.
- **Thought Process**: The internal reasoning of the model (where available).
- **Response**: The final technical explanation or code snippet provided by the AI.
