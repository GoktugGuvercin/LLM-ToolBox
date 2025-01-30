
# BERT

### *Introduction:*

* It is specifically designed for pre-training deep bidirectional representations from unlabeled text. The main approach that they follow is to jointly condition on both left and right context in all layers. In that case, BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for various tasks

* It adapts masked language modeling (MLM) for pre-training objective. Some of input tokens are randomly masked, and the main purpose is to predict vocabulary ids of masked words. 

* The main limitation is the fact that language models are uni-directional. Their potential is quite limited, and also restricts what kind of architectures we can use for pre-training stage. For example,  GPT is left-to-right architecture, where every token can only attend to previous tokens in self-attention layers. This is actually sub-optimal solution for sentence-level tasks, and it can be also harmful when applying fine-tuning based approaches to token-level tasks such as question answering, where it is crucial to incorporate context from both directions. BERT proposed a way to learn bi-directional encoder representations, which helps to alleviate this uni-directionality problem. In this methodology, masked language modeling (MLM) is incorporated. 

### *Approach:*

Multi-layer bidirectional transformer encoder is used for model architecture, and the original implementation in “Attention is all you need” is followed. Bert is implemented in two different sizes: Bert-Base and Bert-Large

| Name  | # Layers | Hidden Size | Attention Head |Model Size
|:-----:|:--------:|:-----------:|:--------------:|:--------:
| Base  | 12  | 768 | 12 | 110M
| Large | 24  | 1024 | 16 | 340M


To make a comparison between BERT and GPT, we can use the following ontology:

   * BERT = Bidirectional self-attention = encoder-only architecture = Encoder from “Attention is all you need” paper

   * GPT = Constrained (Causal) self-attention = decoder-only architecture = Decoder from “Attention is all you need” paper

   * Constrained (Causal) self-attention refers to the masked attention; it enables self-attention only to attend to the context in the left side of the token.


In pre-training stage, an unlabeled data is used, and the network receives two different training signals at the same time. The first one is masked language modeling, while the second is next sentence prediction. In that way, two unsupervised tasks are charged for BERT pre-training stage. 

In fine-tuning stage, pre-trained weights are loaded into the model, and then all these weights are fine-tuned using labeled data for downstream tasks. At this point, each downstream task necessitates a separate fine-tuned model. 


# GPT-1

### *Introduction:*

* Supervised learning depends extensively on annotated datasets to yield instructive signals for training deep neural networks. Nevertheless, the reliance on manual labeling substantially constrains their applicability across diverse domains, since manual labeling requires substantial time and labor force, particularly when dealing with large-scale corpora. One promising strategy to mitigate this problem entails harnessing linguistic cues from unlabeled data in conjunction with considerable fine-tuning the model, which provides task-agnostic features with little adaptation to downstream tasks. 

* In this paper, this kind of semi-supervised approach is actually embraced by a two-stage training procedure. In the first stage, a language modeling objective is leveraged on unlabeled data to extract the initial features. Then, these features are refined through a supervised objective built at the top of annotated dataset tailored for downstream tasks.

* For the architectural design, GPT is empowered by the transformer. Compared to recurrent neural networks, transformers are more powerful to capture long-term dependencies within the text because they operate on more structured memory system and exert a typical information retrieval mechanism by key-query-value triplets. Consequently, this enables transformer models to have robust finetuning (information transfer) option for downstream tasks. 

* GPT is evaluated on four types of language understanding tasks:
    * Natural Language Inference
    * Question Answering
    * Semantic Similarity
    * Text Classification