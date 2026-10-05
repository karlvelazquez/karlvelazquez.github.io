Source: https://shared-language-force-embedding.github.io

Status: SUCCESS (AI-summarized/isolated extract via WebFetch, not raw HTML).

# Cross-modality Force and Language Embeddings for Natural Human-Robot Communication

## Authors
- Karl Velazquez (karlvelazquez@karlvelazquez.com)
- John Payne (johnpayn@mit.edu)

(Note: this project page lists only 2 authors, with Karl listed first; the full official author set per arXiv and the RSS program page is Tejwani, Velazquez, Payne, Bonato, Asada. Karl was a main contributor to the paper.)

## Abstract (as presented on project site)
A framework that maps language and force into a shared latent space, enabling seamless translation between verbal commands and physical interactions. The dual autoencoder model was trained using human data to facilitate collaborative human-robot interaction through multimodal communication.

## Key Components

**Framework:** A dual autoencoder architecture that encodes both modalities (language and force) into a shared latent space. Phrase inputs use GloVe word embeddings, while force profiles undergo feature extraction before encoding. Both can be decoded back to their original form or translated cross-modally.

**Data Collection:** The study involved 10 participants performing two procedures — Phrase-To-Force and Force-To-Phrase translation tasks — with a robotic arm. The research was motivated by observations of physical therapy sessions at Spaulding Rehabilitation Center.

**Results:** The dual autoencoder models "consistently outperformed the baselines across all core metrics" and demonstrated strong generalization to unseen modifiers and directions, particularly using SBERT embeddings for force accuracy.

## Links
- **Code Repository:** https://github.com/Shared-Language-Force-Embedding/shared-language-force-embedding
- **Contact:** Karl Velazquez (GitHub: karlvelazquez), John Payne (GitHub: johnpayne-dev)
