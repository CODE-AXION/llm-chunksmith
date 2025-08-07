# llm-chunksmith
Intelligent Document Chunker. Automatically detects semantic boundaries in Markdown/Raw Text documents, performs hierarchical sub-chunking, and returns coherent content blocks with metadata along with table preservation.

COMING SOON (This will be paid script but dont worry it will be dirt cheap and pretty affordable !!! )...

OUTPUT:
```json
[
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets"
    },
    "page_content": "Open-Domain QA Datasets\n\nWe experiment on five different open-domain QA datasets with Wikipedia as the retrieval source: Natural Questions (NQ, Kwiatkowski et al., 2019), TriviaQA (TQA, Joshi et al., 2017), Web Questions (WebQ, Berant et al., 2013), SQuAD (Rajpurkar et al., 2016), and Entity Questions (EQ, Sciavolino et al., 2021)."
  },
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets",
      "Section Header (1)": "Dense Retrieval Models"
    },
    "page_content": "Dense Retrieval Models\nWe compare the performance of the four following supervised or unsupervised dense retriever models. Here, supervised models refer to ones that have used human-labeled query-passage pairs as supervision during training, and vice versa.\n\n- SimCSE (Gao et al., 2021) is a BERT-base (Devlin et al., 2019) encoder trained on unlabeled sentences sampled randomly from Wikipedia. SimCSE can be transferred to use as an unsupervised retriever (Chen et al., 2023b).\n- Contriever (Izacard et al., 2022) is an unsupervised retriever, instantiated with a BERT-base\nencoder. Contriever is contrastively trained by segment pairs constructed from unlabeled documents from Wikipedia and web crawl data.\n- DPR (Karpukhin et al., 2020) is a dual-encoder BERT-base model fine-tuned on passage retrieval tasks directly using the question-passage pair labels from NQ, TQA, WebQ and SQuAD.\n- GTR (Ni et al., 2022) is a T5-base encoder (Raffel et al., 2020) pretrained on online forum QA data, and fine-tuned with question-passage pair labels on MS MARCO (Nguyen et al., 2016) and NQ datasets."
  },
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets",
      "Section Header (2)": "Passage Retrieval Evaluation"
    },
    "page_content": "Passage Retrieval Evaluation\nWe evaluate the retrieval performance at the passage level when the corpus is indexed at the passage, sentence, or proposition level respectively. For sentence and proposition level retrieval, we follow the setting introduced in Lee et al. (2021b), where the score of the passage is based on the maximum similarity score between the query and all sentences or propositions in a passage. In practice, we first retrieve a slightly larger number of text units, then map each unit to the source passage, and eventually return the top- $k$ unique passages. We use Passage Recall@ $k$ as our evaluation metric, which is defined as the percentage of questions for which the correct answer is found within the top- $k$ retrieved passages.\n\nTo further understand how different retrieved passages affect the downstream QA. We use Fusion-in-Decoder (FiD, Izacard and Grave, 2021) model to extract answers from retrieved passages. We use a T5-large sized FiD model trained on NQ dataset in our experiments. The exact match (EM) score computes the percentage of questions for which the predicted answer exactly matches the ground truth."
  },
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets",
      "Section Header (3)": "Open-domain QA Evaluation on Retrieval-Augmented Language Models"
    },
    "page_content": "Open-domain QA Evaluation on Retrieval-Augmented Language Models\nAnother aspect of the choice of granularity lies in what units should be used in the prompt for retrieval-augmented language models. For large language models, retrieval-augmented generation is achieved by prepending retrieved units to user instruction and taking them as the input for language models. We aim to understand the implications of using retrieved units of different granularity within the same computational budget at inference time. To fairly compare using different granularity in the"
  },
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets",
      "Section Header (3)": "Open-domain QA Evaluation on Retrieval-Augmented Language Models",
      "block_type": "Table"
    },
    "page_content": "| Retriever | Granularity | NQ | | TQA | | WebQ | | SQuAD | | EQ | | Avg. | |\n| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |\n| | | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 |\n| Unsupervised Dense Retrievers | | | | | | | | | | | | | | |\n| SimCSE | Passage | 28.8 | 44.3 | 44.9 | 59.4 | 39.8 | 56.0 | 29.5 | 45.5 | 28.4 | 40.3 | 34.3 | 49.1 |\n| | Sentence | 35.5 | 53.1 | 50.5 | 64.3 | 45.3 | 64.1 | 37.1 | 52.3 | 36.3 | 50.1 | 40.9 | 56.8 |\n| | Proposition | 41.1 | 58.9 | 52.4 | 66.5 | 50.0 | 66.8 | 38.7 | 53.9 | 49.5 | 62.2 | 46.3 | 61.7 |\n| Contriever | Passage | 42.5 | 63.8 | 58.1 | 73.7 | 37.1 | 60.6 | 40.8 | 59.8 | 36.3 | 56.3 | 43.0 | 62.8 |\n| | Sentence | 46.4 | 66.8 | 60.6 | 75.7 | 41.7 | 63.1 | 45.1 | 63.5 | 42.7 | 61.3 | 47.3 | 66.1 |\n| | Proposition | 50.1 | 70.0 | 65.1 | 77.9 | 45.9 | 66.8 | 50.7 | 67.7 | 51.7 | 70.1 | 52.7 | 70.5 |\n| Supervised Dense Retrievers | | | | | | | | | | | | | | |\n| DPR | Passage | 66.0 | 78.0 | 71.6 | 80.2 | 62.9 | 74.9 | 38.3 | 53.9 | 47.5 | 60.4 | 57.3 | 69.5 |\n| | Sentence | 66.0 | 78.0 | 71.8 | 80.5 | 64.1 | 74.4 | 40.3 | 55.9 | 53.7 | 66.0 | 59.2 | 71.0 |\n| | Proposition | 65.4 | 77.7 | 70.7 | 79.6 | 62.8 | 75.1 | 41.4 | 57.2 | 59.4 | 71.3 | 59.9 | 72.2 |\n| GTR | Passage | 66.3 | 78.4 | 70.1 | 79.4 | 63.3 | 76.5 | 54.4 | 68.1 | 71.7 | 80.5 | 65.2 | 76.6 |\n| | Sentence | 66.4 | 79.4 | 71.6 | 80.9 | 62.2 | 76.8 | 60.9 | 73.4 | 72.5 | 81.3 | 66.7 | 78.4 |\n| | Proposition | 66.5 | 79.6 | 72.2 | 80.9 | 63.2 | 77.4 | 63.3 | 75.0 | 74.9 | 83.0 | 68.0 | 79.2 |"
  },
  {
    "metadata": {
      "Header": "Open-Domain QA Datasets",
      "Section Header (3)": "Open-domain QA Evaluation on Retrieval-Augmented Language Models"
    },
    "page_content": "Table 3: Passage retrieval performance (Recall@k = 5, 20) on five different open-domain QA datasets when pre-trained dense retrievers work with the three different granularity from the retrieval corpus. Underline denotes cases where the training split of the target dataset was included in the training data of the dense retriever.\nprompts under the same computation budget, we set a token length limit for retrieved units.\n\nFor this reason, we follow an evaluation setup where the maximum number of retrieved tokens is capped at $l=100$ or 500 , i.e. only the top $l$ tokens from passage, sentence, or proposition level retrieval are fed into the language model as input. We evaluate the percentage of questions for which the predicted answer exactly matches (EM) the ground truth. We denote our metric as EM @ $l$ tokens. We use LLaMA-2-7B [touvron2023llama] in our evaluation. To ensure the model's output aligns with the format of each dataset, we employ in-context learning, incorporating four-shot demonstrations as illustrated in Figure 9."
  }
]
```

INPUT:

```

Open-Domain QA Datasets

We experiment on five different open-domain QA datasets with Wikipedia as the retrieval source: Natural Questions (NQ, Kwiatkowski et al., 2019), TriviaQA (TQA, Joshi et al., 2017), Web Questions (WebQ, Berant et al., 2013), SQuAD (Rajpurkar et al., 2016), and Entity Questions (EQ, Sciavolino et al., 2021).

Dense Retrieval Models
We compare the performance of the four following supervised or unsupervised dense retriever models. Here, supervised models refer to ones that have used human-labeled query-passage pairs as supervision during training, and vice versa.

- SimCSE (Gao et al., 2021) is a BERT-base (Devlin et al., 2019) encoder trained on unlabeled sentences sampled randomly from Wikipedia. SimCSE can be transferred to use as an unsupervised retriever (Chen et al., 2023b).
- Contriever (Izacard et al., 2022) is an unsupervised retriever, instantiated with a BERT-base
encoder. Contriever is contrastively trained by segment pairs constructed from unlabeled documents from Wikipedia and web crawl data.
- DPR (Karpukhin et al., 2020) is a dual-encoder BERT-base model fine-tuned on passage retrieval tasks directly using the question-passage pair labels from NQ, TQA, WebQ and SQuAD.
- GTR (Ni et al., 2022) is a T5-base encoder (Raffel et al., 2020) pretrained on online forum QA data, and fine-tuned with question-passage pair labels on MS MARCO (Nguyen et al., 2016) and NQ datasets.


Passage Retrieval Evaluation
We evaluate the retrieval performance at the passage level when the corpus is indexed at the passage, sentence, or proposition level respectively. For sentence and proposition level retrieval, we follow the setting introduced in Lee et al. (2021b), where the score of the passage is based on the maximum similarity score between the query and all sentences or propositions in a passage. In practice, we first retrieve a slightly larger number of text units, then map each unit to the source passage, and eventually return the top- $k$ unique passages. We use Passage Recall@ $k$ as our evaluation metric, which is defined as the percentage of questions for which the correct answer is found within the top- $k$ retrieved passages.

To further understand how different retrieved passages affect the downstream QA. We use Fusion-in-Decoder (FiD, Izacard and Grave, 2021) model to extract answers from retrieved passages. We use a T5-large sized FiD model trained on NQ dataset in our experiments. The exact match (EM) score computes the percentage of questions for which the predicted answer exactly matches the ground truth.

Open-domain QA Evaluation on Retrieval-Augmented Language Models
Another aspect of the choice of granularity lies in what units should be used in the prompt for retrieval-augmented language models. For large language models, retrieval-augmented generation is achieved by prepending retrieved units to user instruction and taking them as the input for language models. We aim to understand the implications of using retrieved units of different granularity within the same computational budget at inference time. To fairly compare using different granularity in the

| Retriever | Granularity | NQ | | TQA | | WebQ | | SQuAD | | EQ | | Avg. | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 | R@5 | R@20 |
| Unsupervised Dense Retrievers | | | | | | | | | | | | | | |
| SimCSE | Passage | 28.8 | 44.3 | 44.9 | 59.4 | 39.8 | 56.0 | 29.5 | 45.5 | 28.4 | 40.3 | 34.3 | 49.1 |
| | Sentence | 35.5 | 53.1 | 50.5 | 64.3 | 45.3 | 64.1 | 37.1 | 52.3 | 36.3 | 50.1 | 40.9 | 56.8 |
| | Proposition | 41.1 | 58.9 | 52.4 | 66.5 | 50.0 | 66.8 | 38.7 | 53.9 | 49.5 | 62.2 | 46.3 | 61.7 |
| Contriever | Passage | 42.5 | 63.8 | 58.1 | 73.7 | 37.1 | 60.6 | 40.8 | 59.8 | 36.3 | 56.3 | 43.0 | 62.8 |
| | Sentence | 46.4 | 66.8 | 60.6 | 75.7 | 41.7 | 63.1 | 45.1 | 63.5 | 42.7 | 61.3 | 47.3 | 66.1 |
| | Proposition | 50.1 | 70.0 | 65.1 | 77.9 | 45.9 | 66.8 | 50.7 | 67.7 | 51.7 | 70.1 | 52.7 | 70.5 |
| Supervised Dense Retrievers | | | | | | | | | | | | | | |
| DPR | Passage | 66.0 | 78.0 | 71.6 | 80.2 | 62.9 | 74.9 | 38.3 | 53.9 | 47.5 | 60.4 | 57.3 | 69.5 |
| | Sentence | 66.0 | 78.0 | 71.8 | 80.5 | 64.1 | 74.4 | 40.3 | 55.9 | 53.7 | 66.0 | 59.2 | 71.0 |
| | Proposition | 65.4 | 77.7 | 70.7 | 79.6 | 62.8 | 75.1 | 41.4 | 57.2 | 59.4 | 71.3 | 59.9 | 72.2 |
| GTR | Passage | 66.3 | 78.4 | 70.1 | 79.4 | 63.3 | 76.5 | 54.4 | 68.1 | 71.7 | 80.5 | 65.2 | 76.6 |
| | Sentence | 66.4 | 79.4 | 71.6 | 80.9 | 62.2 | 76.8 | 60.9 | 73.4 | 72.5 | 81.3 | 66.7 | 78.4 |
| | Proposition | 66.5 | 79.6 | 72.2 | 80.9 | 63.2 | 77.4 | 63.3 | 75.0 | 74.9 | 83.0 | 68.0 | 79.2 |

Table 3: Passage retrieval performance (Recall@k = 5, 20) on five different open-domain QA datasets when pre-trained dense retrievers work with the three different granularity from the retrieval corpus. Underline denotes cases where the training split of the target dataset was included in the training data of the dense retriever.
prompts under the same computation budget, we set a token length limit for retrieved units.

For this reason, we follow an evaluation setup where the maximum number of retrieved tokens is capped at $l=100$ or 500 , i.e. only the top $l$ tokens from passage, sentence, or proposition level retrieval are fed into the language model as input. We evaluate the percentage of questions for which the predicted answer exactly matches (EM) the ground truth. We denote our metric as EM @ $l$ tokens. We use LLaMA-2-7B [touvron2023llama] in our evaluation. To ensure the model's output aligns with the format of each dataset, we employ in-context learning, incorporating four-shot demonstrations as illustrated in Figure 9.

```
