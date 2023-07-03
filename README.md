# KNOWLEDGE GRAPH FOR MULTI-HOP QUESTION ANSWERING

Question Answering (QA) currently has many limitations, especially in Vietnamese, in its ability to infer complex reasoning. In addition, historical language data has not been exploited much. The research team aims to study and develop the Multi-hop QA problem for Vietnamese history based on Knowledge Graph.

However, the model has not achieved the expected accuracy and complexity. Team will continue to develop the model and historical vocabulary to expand the knowledge graph and improve the Multi-hop QA tool based on the knowledge graph in the future.


%% trực quan hóa knowledge Graph

Details of the models and experimental results can be found in the following report.

## Result


| Models             | Accuracy                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Token+NER\_MATCHING           | 53.5046 |
| Token+NER\_phoNLP             | 43.1433 |
| **Token+NER\_sentence**       | **56.7348** |
| Token+NER\_original\_sentence | 53.7337 |
| Longest+NER\_MATCHING         | 52.9981 |
| Longest+NER\_phoNLP           | 43.143 |
| **Longest+NER\_sentence**     | **56.3394** |
| Underpy+NER\_MATCHING         | 52.8087 |
| Underpy+NER\_phoNLP           | 41.1765 |
| Underpy+NER\_sentence         | 56.0173 |


## Requirements


```bash
pip install langdetect
pip install unidecode
pip install pyvi
pip install underthesea
pip install py_vncorenlp
pip3 install phonlp
```
## Usage/Examples

### Vocabulary

```python
from Data.Vocabulary import

# Get word_regex from Vocabulary
get_vocabulary(path_vocabulary = '/absolute/path/to/vocabulary')
# \\b[Hh][Ồồ][  ][Cc][Hh][Íí][  ][Mm][Ii][Nn][Hh]\\b


# Insert word_list into vocabulary
insert_vocab(word_list, data = vocabulary , path= '/absolute/path/to/vocabulary')


# Remove word_list from vocabulary
remove_data(word_list, data = vocabulary , path= '/absolute/path/to/vocabulary')

```


### Tokenize

```python
from Tokenize.Tokenize import Tokenize, longest_matching, Underthesea_pyvi

model = Tokenize(vocab = True)

model.tokenizer(text = 'Hồ Chí Minh là nhà cách mạng cộng sản Việt Nam .')
# Hồ_Chí_Minh là nhà_cách_mạng_cộng_sản Việt_Nam

model.annotate(text = 'Tôi là nhà cách mạng cộng sản Việt Nam .')
# [['Hồ_Chí_Minh', 'P'], ['là', 'V'], ['nhà_cách_mạng_cộng_sản', 'N'], ['Việt_Nam', 'Np'], ['.', 'CH']]

```

### NER

```python
from ner.ner import NER

model = NER(token = Tokenize(), path_phonlp = '/absolute/path/to/phonlp_dict', normalize = True)


model.NER_sentence(sentence = 'Tôi là nhà cách mạng cộng sản Việt Nam .')
# [['Hồ_Chí_Minh', 'PER'], ['là', 'V'], ['nhà_cách_mạng_cộng_sản', 'PER'], ['Việt_Nam', 'LOC'], ['.', 'CH']]

```

### EXTRACT RELATION

```python
from ner.ner import NER
from RE.RE import extract_triples(tok, triples= result)

model = NER(token = Tokenize(), path_phonlp = '/absolute/path/to/phonlp_dict', normalize = True)


toks = model.NER_sentence(sentence = 'Tôi là nhà cách mạng cộng sản Việt Nam .')
# [['Hồ_Chí_Minh', 'PER'], ['là', 'V'], ['nhà_cách_mạng_cộng_sản', 'PER'], ['Việt_Nam', 'LOC'], ['.', 'CH']]

extract_triples(toks = toks, triples= triples)
# [['Hồ Chí Minh', 'nhà cách mạng cộng sạn', 'là'], ['nhà cách mạng cộng sản', 'Việt Nam', 'ở'], ['Hồ Chí Minh', 'Việt Nam', 'ở']

```
## Authors

- [@Tan Nhat Do - 21522575@gm.uit.edu.vn](https://github.com/tannd-ds)
- [@Phuong Dieu Nguyen - 21520091@gm.uit.edu.vn](https://github.com/ndp1707)
