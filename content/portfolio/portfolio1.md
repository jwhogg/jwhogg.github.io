---
title: 'Youtube2Summary'
date: 2024-06-032T14:25:04+01:00
draft: false
# math: true
# katex: true
---

[Github 🔗](https://github.com/jwhogg/youtube_to_summary)

🤗 Pipeline to generate summaries of youtube videos, using Whisper-Small for transcription, and BART-LARGE-XSUM for summarisation. 

BART has been finetuned on the popular CNN/Daily Mail Dataset, as it lends itself to summarisation tasks. Initially, we attempted to fine-tune GPT-2 for the summarisation task, but found it had poor performance: being a generative transfotmer, it generates words one-by-one, (extractive summarisation) whereas BART can generate at the sentence level (using abstractive summarisation). For more info on choice of summarisation model, see this article. We use the HuggingFace Transformers libary to abstract some of the PyTorch code using the pipeline submodule.

Although the code does work, there are many potential areas for improvement: quantisation of the model to improve runtime, a refined BART model that works better on summarisating conversational dialouge.


