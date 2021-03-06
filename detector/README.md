GPT-2 Output Detector
=====================

This directory contains the code for working with the GPT-2 output detector model, obtained by fine-tuning a
[RoBERTa model](https://ai.facebook.com/blog/roberta-an-optimized-method-for-pretraining-self-supervised-nlp-systems/)
with [the outputs of the 1.5B-parameter GPT-2 model](https://github.com/openai/gpt-2-output-dataset).
For motivations and discussions regarding the release of this detector model, please check out 
[our blog post](https://openai.com/blog/gpt-2-1-5b-release/) and [report](https://d4mucfpksywv.cloudfront.net/papers/GPT_2_Report.pdf).

## Downloading a pre-trained detector model

Download the weights for the fine-tuned `roberta-base` model (478 MB):

```bash
wget https://storage.googleapis.com/gpt-2/detector-models/v1/detector-base.pt
```

or `roberta-large` model (1.5 GB):

```bash
wget https://storage.googleapis.com/gpt-2/detector-models/v1/detector-large.pt
```

These RoBERTa-based models are fine-tuned with a mixture of temperature-1 and nucleus sampling outputs,
which should generalize well to outputs generated using different sampling methods.

## Running a detector model

You can launch a web UI in which you can enter a text and see the detector model's prediction
on whether or not it was generated by a GPT-2 model.

```bash
# (on the top-level directory of this repository)
pip install -r requirements.txt
python -m detector.server detector-base.pt
```

After the script says "Ready to serve", nagivate to http://localhost:8080 to view the UI.

## Training a new detector model

You can use the provided training script to train a detector model on a new set of datasets.
We recommend using a GPU machine for this task.

```bash
# (on the top-level directory of this repository)
pip install -r requirements.txt
python -m detector.train
```

The training script supports a number of different options; append `--help` to the command above for usage.
