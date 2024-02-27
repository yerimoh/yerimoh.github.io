To ground our approach, this section summarizes
MLMs for pre-training bidirectional Transformers (Devlin et al., 2019). Compared to causal
LMs (Peters et al., 2018) trained unidirectionally,
MLMs randomly mask some tokens and predict
the masked tokens by considering their context on
both sides. Formally, given a piece of text U, a
tokenizer, e.g., BPE (Sennrich et al., 2016), is used
to produce a sequence of tokens [w1, . . . , wn]. A
certain percentage of the original tokens are then
masked and replaced: of those, 80% with the special token [MASK], 10% with a token sampled
from the vocabulary V, and the remaining kept
unchanged. The masked sequence, denoted as
[w
(m)
1
, . . . , w
(m)
n ], is passed into a Transformer encoder to produce contextualized representations for
the sequence:



where H ∈ R
dh×n
and dh denotes the hidden size.
The training loss LM for MLM task is defined as





where M denotes the set of masked token indices,
and P(wi
|H:,i) is the probability of predicting the
original token wi given the representations computed from the masked token sequence




3 Proposed Method


This section begins with a description of entitylevel masked language modeling. Section 3.2 proposes a KG-guided entity masking scheme for
the entity-level MLM task. A novel distractorsuppressed ranking task is presented in Section 3.3,
which operates on the masked entities and their negative entity samples from the KG. We use a multitask learning objective combining the two tasks
above to jointly train our proposed Graph-guided
Masked Language Model (GLM). An illustration
of the GLM is shown in Figure 2.



3.1 Entity-Level Masked Language Model



