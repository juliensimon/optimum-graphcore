<!---
Copyright 2020 The HuggingFace Team. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# SQuAD

Based on the script [`run_qa.py`](https://github.com/huggingface/transformers/blob/master/examples/pytorch/question-answering/run_qa.py).

**Note:** This script only works with models that have a fast tokenizer (backed by the 🤗 Tokenizers library) as it
uses special features of those tokenizers. You can check if your favorite model has a fast tokenizer in
[this table](https://huggingface.co/transformers/index.html#supported-frameworks).

`run_qa.py` allows you to fine-tune any model from our [hub](https://huggingface.co/models) (as long as its architecture has a `ForQuestionAnswering` version in the transformers library, and a `Pipelined` version available in optimum) on the SQUAD dataset or another question-answering dataset of the `datasets` library or your own csv/jsonlines files as long as they are structured the same way as SQUAD. You might need to tweak the data processing inside the script if your data is structured differently.

Note that if your dataset contains samples with no possible answers (like SQUAD version 2), you need to pass along the flag `--version_2_with_negative`.

## Fine-tuning BERT on SQuAD1.0

This example code fine-tunes BERT on the SQuAD1.0 dataset.
<!-- Add execution time once it is available.
It runs in 4 min (with BERT-base) or 68 min (with BERT-large)
on a single tesla V100 16GB.
-->

```bash
python run_qa.py \
  --model_name_or_path bert-base-uncased \
  --ipu_config_name Graphcore/bert-base-ipu \
  --dataset_name squad \
  --do_train \
  --do_eval \
  --per_device_train_batch_size 12 \
  --learning_rate 3e-5 \
  --num_train_epochs 2 \
  --max_seq_length 384 \
  --doc_stride 128 \
  --output_dir ./output/debug_squad/
```

<!-- Insert performance on IPU once final values are available.
Training with the previously defined hyper-parameters yields the following results:
```bash
f1 = 88.52
exact_match = 81.22
```
-->
