---
title: 'Fine-tuning a pre-trained model from HuggingFace'
date: 2024-05-24T13:29:04+01:00
draft: false
---

We will be using a 🤗 [HuggingFace](https://huggingface.co/) model ([GPT-2 Medium](https://huggingface.co/openai-community/gpt2-medium))
##### 📙**[Jupyter Notebook](https://github.com/jwhogg/GPT-2-Fine-Tuning/blob/main/GPT-2%20Fine-tuning%20CNNDailyMail.ipynb)**

### Create train/test split for custom dataset
(can use sklearn for this)
### Get the model tokeniser
```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("your-model-here") #eg "bert-base-cased"
```
### Create encodings for train/test using tokeniser
```python
def tokenize_function(examples):
    return tokenizer(examples["text"], padding="max_length", truncation=True)

tokenized_datasets = raw_datasets.map(tokenize_function, batched=True)
# where raw_datasets is a dict with train/dev/test
```
- we need padding as the inputs must fit the models input even if they are too short

##### Create small datasets for development
```python
small_train_dataset = tokenized_datasets["train"].shuffle(seed=42).select(range(1000)) 
small_eval_dataset = tokenized_datasets["test"].shuffle(seed=42).select(range(1000)) 
full_train_dataset = tokenized_datasets["train"]
full_eval_dataset = tokenized_datasets["test"]
```
- use the full ones once you have all params figured out and want to do the final training
### Import model
```python
from transformers import GPT2Tokenizer, GPT2Model

tokenizer = GPT2Tokenizer.from_pretrained('gpt2-medium')
model = GPT2Model.from_pretrained('gpt2-medium')
```
### Training
- *Transformers* has a `Trainer` class that can speed up training of models, and does a lot of the work for us
- `Trainer` is defined as a dict of arguments and a `compute_metrics` function, but first we need to define these:
##### Training args:
```python
from transformers import TrainingArguments

training_args = TrainingArguments("test_trainer")
#use just default args to start with
#add arg: evaluation_strategy="epoch" to report metrics every epoch
```

#### Configure training metrics
- *Trainer* can take a `compute_metrics()` function, which takes predictions and labels (in a tuple), and returns a dict with metric names and values
- we can use the *Datasets* library to get access to common metrics
	- 'accuracy' is one of these
```python
import numpy as np
from datasets import load_metric

metric = load_metric("accuracy")

def compute_metrics(eval_pred):
    logits, labels = eval_pred #splitting tuple into the output logits and their labels
    predictions = np.argmax(logits, axis=-1) #convert logits into predictions
    return metric.compute(predictions=predictions, references=labels) #calc predict accuracy
```

### Define Trainer
```python
from Transformers import Trainer

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=small_train_dataset,
    eval_dataset=small_eval_dataset,
    compute_metrics=compute_metrics,
)
```

### Train and Evaluate:
```
trainer.train()
trainer.evaluate()
```

We are now done! the [training args](https://huggingface.co/docs/transformers/v4.15.0/en/main_classes/trainer#transformers.TrainingArguments) or dataset can be tweaked to try to improve performance

Remember to [save your model](https://discuss.huggingface.co/t/save-load-and-do-inference-with-fine-tuned-model/76291/2)!
	`model.save_pretrained("path/to/model.pt")`