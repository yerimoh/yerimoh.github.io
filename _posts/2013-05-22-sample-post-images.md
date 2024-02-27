In this work, we equip masked language models (MLMs), e.g., BERT (Devlin et al., 2019),
with structured knowledge via self-supervised pretraining on raw text. Compared to the first class, we
expose LMs to structured information only during
pre-training, thus circumventing costly knowledge
retrieval and integration in both finetuning and inference. Also the dependency on the performance
of linking algorithm is greatly reduced. Compared
to the second class, we learn from free-form text
through MLMs rather than triples, which fosters
generalization on other downstream tasks.


Specifically, given a corpus of raw text and a
KG, two KG-guided self-supervision tasks are formulated to inject structured knowledge into MLMs.
First, taking inspiration from Baidu-ERNIE (Sun
et al., 2019a), we reformulate the masked language
modeling objective to an entity-level masking strategy, where entities are identified by linking their
text mentions to either concepts in a commonsense
KG or named entities in an ontological KG (Bollacker et al., 2008). The role of KG here is to provide a “vocabulary” of entities to be masked. To
further exploit implicit relational information underlying raw text, we design a KG-guided masking
scheme that selects informative entities by considering both document frequency and mutual reachability of the entities detected in the text. In addition to the new entity-level MLM task above,
a novel distractor-suppressed ranking task is proposed. Negative entity samples are derived from
the KG and used as distractors for the masked entities to make the learning more effective.


Note that our approach never observes the KG
directly, through triples or other forms. Rather,
the KG plays a guiding role in the proposed selfsupervised tasks. Its guidance helps the model
exploit the corpus more effectively as verified in
the experiments. If a downstream task can benefit
from explicit exposure to KG, a method by Davison
et al. (2019) can be used to transform KG triples
into natural grammatical texts for our model



We evaluate our method on five benchmarks (including question answering and knowledge base
completion) and one zero-shot testing. Results
show our method achieves state-of-the-art or competitive performance on all benchmarks.
