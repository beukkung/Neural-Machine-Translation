# Thai ↔ English Neural Machine Translation Experiments

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Fairseq-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Transformers](https://img.shields.io/badge/🤗-Transformers-yellow)](https://huggingface.co/docs/transformers/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
![Task](https://img.shields.io/badge/Task-Thai%20↔%20English%20NMT-6f42c1)
![Status](https://img.shields.io/badge/Status-Research%20%2F%20Portfolio-blue)

A collection of neural machine translation experiments for **English–Thai and Thai–English**, covering both custom Fairseq training and inference with pretrained translation models.

Rather than presenting one model as a finished product, this repository documents several approaches explored during the project and makes the differences explicit.

## Experiments at a glance

| Notebook | Direction / purpose | Main approach |
|---|---|---|
| [`ENTH_Fairseq.ipynb`](ENTH_Fairseq.ipynb) | English → Thai experiment | Fairseq training pipeline with BPE |
| [`ENTH_SCB_1M-MT-OPUS.ipynb`](ENTH_SCB_1M-MT-OPUS.ipynb) | English → Thai inference | VISTEC SCB_1M-MT-OPUS Transformer |
| [`THEN_Helsinki-NLP.ipynb`](THEN_Helsinki-NLP.ipynb) | Thai → English inference | Helsinki-NLP OPUS-MT via Transformers |

## 1. Custom Fairseq pipeline

The Fairseq notebook prepares Thai/English parallel text, builds BPE representations, runs Fairseq preprocessing, trains a translation model, and generates translations for evaluation.

```mermaid
flowchart LR
    A[Parallel EN / TH corpus] --> B[Text cleaning]
    B --> C[BPE preparation]
    C --> D[Fairseq preprocess]
    D --> E[Transformer training]
    E --> F[Generate translations]
    F --> G[BLEU evaluation]
```

The notebook uses the SCB machine-translation corpus and contains an experimental sacreBLEU output. That value should be interpreted only in the context of the exact historical split/configuration; this repository does not treat it as a general benchmark claim.

## 2. VISTEC SCB_1M-MT-OPUS inference

The second English→Thai notebook is adapted from the public VISTEC / depa AI Research Institute translation example and loads the released **SCB_1M-MT-OPUS + Transformer Base** model.

Its workflow includes:

- Fairseq model loading;
- Moses tokenization for English;
- PyThaiNLP/newmm-related Thai processing;
- SentencePiece/model vocabulary assets;
- batch translation over a local evaluation dataset.

The notebook itself contains an attribution note to the original VISTEC code.

## 3. Helsinki-NLP Thai→English

The Thai→English notebook uses Hugging Face Transformers with:

```text
Helsinki-NLP/opus-mt-th-en
```

It demonstrates tokenizer/model loading, GPU inference, beam/generation calls, and exploratory BLEU calculation.

## Repository structure

```text
.
├── ENTH_Fairseq.ipynb          # Custom English→Thai Fairseq experiment
├── ENTH_SCB_1M-MT-OPUS.ipynb  # Pretrained SCB/VISTEC English→Thai inference
├── THEN_Helsinki-NLP.ipynb     # Helsinki-NLP Thai→English inference
├── .gitignore
├── .gitattributes
└── README.md
```

## Dependencies

The notebooks were created in an older research environment and use different stacks. Depending on the notebook, packages include:

```text
torch
fairseq
transformers
sentencepiece
sacrebleu
pythainlp
mosestokenizer
deepcut
pandas
numpy
```

Some cells pin historical package versions or Git commits. Reproducing them today may require a compatible Python/PyTorch environment rather than installing the newest releases blindly.

## Data and model assets

Training/evaluation corpora and large model checkpoints are not committed to this repository. Some notebooks download external pretrained assets at runtime or expect local parallel-text files.

When reproducing the experiments, verify the license and usage terms of each dataset and pretrained model separately.

## Evaluation guidance

Machine translation quality should not be summarized by one number. A modern reproduction should record:

- sacreBLEU with its full signature;
- chrF / chrF++;
- COMET or another learned metric where appropriate;
- human review for adequacy, fluency, named entities, numbers, and Thai-specific linguistic errors;
- inference speed and memory footprint.

## Limitations

- The notebooks use historical library APIs and environment-specific paths.
- The experiments are not normalized into one shared training/evaluation harness.
- Dataset splits and preprocessing differ across approaches.
- Translation quality is not summarized in a single reproducible benchmark table.
- Pretrained-model behavior depends on third-party model releases.

## Potential improvements

1. Standardize all experiments on one dataset split and evaluation script.
2. Add reproducible environment files/containers.
3. Store preprocessing rules and tokenizer versions explicitly.
4. Compare strong modern multilingual models on the same test set.
5. Add qualitative error categories for Thai segmentation, entities, numbers, and formality.
6. Package inference behind a consistent CLI/API.

## Skills demonstrated

NLP · neural machine translation · transformers · Fairseq · Hugging Face Transformers · BPE / tokenization · Thai language processing · model evaluation

## Acknowledgements

The repository experiments use or reference public work from **VISTEC / depa AI Research Institute of Thailand**, **Helsinki-NLP**, **PyTorch Fairseq**, Hugging Face, and the respective dataset/model authors. Please consult upstream projects for original licenses and citation requirements.

## License

No repository-level open-source license is currently included. Third-party datasets, model checkpoints, and source examples remain subject to their original licenses.
