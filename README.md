
# BERT

## Introduction:

* It is specifically designed for pre-training deep bidirectional representations from unlabeled text. The main approach that they follow is to jointly condition on both left and right context in all layers. In that case, BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for various tasks

* It adapts masked language modeling (MLM) for pre-training objective. Some of input tokens are randomly masked, and the main purpose is to predict vocabulary ids of masked words. 

* * The main limitation is the fact that language models are uni-directional. Their potential is quite limited, and also restricts what kind of architectures we can use for pre-training stage. For example,  GPT is left-to-right architecture, where every token can only attend to previous tokens in self-attention layers. This is actually sub-optimal solution for sentence-level tasks, and it can be also harmful when applying fine-tuning based approaches to token-level tasks such as question answering, where it is crucial to incorporate context from both directions. BERT proposed a way to learn bi-directional encoder representations, which helps to alleviate this uni-directionality problem. In this methodology, masked language modeling (MLM) is incorporated. 

## Approach:

* Multi-layer bidirectional transformer encoder is used for model architecture, and the original implementation in “Attention is all you need” is followed. Bert is implemented in two different sizes: Bert-Base and Bert-Large

Name | Number of Layers | Hidden Size | Attention Head | Model Size
Base | 12 | 768 | 12 | 110M
Large | 24 | 1024 | 16 | 340M

* To make a comparison between BERT and GPT, we can use the following ontology:

    * BERT = Bidirectional self-attention = encoder-only architecture = Encoder from “Attention is all you need” paper

    * GPT = Constrained (Causal) self-attention = decoder-only architecture = Decoder from “Attention is all you need” paper

    * Constrained (Causal) self-attention refers to the masked attention; it enables self-attention only to attend to the context in the left side of the token.


* In pre-training stage, an unlabeled data is used, and the network receives two different training signals at the same time. The first one is masked language modeling, while the second is next sentence prediction. In that way, two unsupervised tasks are charged for BERT pre-training stage. 

* In fine-tuning stage, pre-trained weights are loaded into the model, and then all these weights are fine-tuned using labeled data for downstream tasks. At this point, each downstream task necessitates a separate fine-tuned model. 
