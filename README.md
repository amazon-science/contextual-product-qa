## Contextual Product Question Answering

Contextual Product question answering (CPQA) has been a hot topic in e-commerce applications. Given a question about a product (context), the PQA system will search the product page and provide an instant answer, so that customers do not need to traverse over the page by themselves or seek help from real humans.
This can greatly improve their online shopping experience while significantly reducing the cost of customer service support.
This repository holds datasets supporting the contextual product question answering task.

Right now it includes two datasets:

* **semiPQA**: Question answering from semi-structured data described [in this paper](https://aclanthology.org/2022.ecnlp-1.14.pdf).
* **hetPQA**: Question answering from heterogeneous data described [in this paper](https://aclanthology.org/2022.ecnlp-1.13.pdf).
* **ePQA**: An updated version of hetPQA (less noise, finer-grained labels, consider context of candidate), described [in this paper](https://arxiv.org/abs/2305.09249).
* **xPQA**: Cross-lingual Product Question answering in 12 languages, described [in this paper](https://arxiv.org/abs/2305.09249).

## SemiPQA

Current research mainly focuses on finding answers from either unstructured text, like product descriptions and user reviews, or structured
knowledge bases with pre-defined schemas. Apart from the above two sources, a lot of product information is represented in a semistructured way, e.g., key-value pairs, lists, tables, json and xml files, etc. These semistructured data can be a valuable answer source since they are better organized than free text, while being easier to construct than structured knowledge bases.  SemiPQA is a dataset to benchmark PQA over semi-structured data. It contains 10,949 written questions about json-formatted data covering 258 unique attribute types (The numbers are slightly lower than the ones reported in the [paper](https://aclanthology.org/2022.ecnlp-1.14.pdf) as we removed some sensitive attributes). Each data point is paired with manually-annotated text that describes its contents, so that we can train a neural answer presenter to present the data in a natural way.


The semiPQA folder contains the dataset. It contains two sub-folders for the attribute ranking and data-to-text generation respectively. In each sub-folder, there exists 4 csv files: train, dev, testseen and testunseen, where the latter two correspond to seen and unseen attributes as mentioned in the paper. CSV files are separated by "\t". 

The attribute ranking filels contain the following columns:
* qid: question id
* qa_pair_id: question-candidate pair id
* question: question text
* candidate: candidate text (json-formed attributes converted into strings)
* label: 1 means that the candidate is relevant with the  question and 0 otherwise.

The data-to-text files contain the  following columns:
* data: data text (json-formed attributes converted into strings)
* text: manual written text describing the content of the data

## HetPQA

It is of great value to answer product questions based on heterogeneous information sources available on web product pages, e.g., semi-structured attributes, text descriptions, userprovided contents, etc. hetPQA is a large-scale benchmark dataset for answering product questions from 6 heterogeneous sources:
1. semi-structured attribute: Product attributes in json format as in the semiPQA dataset.
2. bullet point: Product summaries in the form of bullet points from the product page.
3. product description: Product descriptions from the manufacturer and Amazon.
4. on-site publication: Manually written Publications about products (for example [here](https://www.amazon.com/ospublishing/story/14423b91-4203-413e-a885-6005dca8d68e)).
5. user review: User reviews written for the product.
6. community answer: Top-voted community answers. Answers directly replying to questions in our question set are discarded

The hetPQA dataset features (1) It provides clear annotations for both evidence ranking and answer generation, enabling us to perform in-depth evaluation of these two components separately. (2) We consider a mix of 6 heterogeneous sources, ranging from semi-structured specifications (jsons) to free sentences and (3) It represents naturally-occurring questions, unlike previous collections that elicited questions by showing answers explicitly. Questions from the hetPQA dataset are all about the "toys and games" product category. The number of instances in the released version is slightly different from the one reported in the original paper as we filtered some sensitive contents.

The hetPQA folder contains the dataset. It contains two sub-folders for the evidence ranking and answer generation respectively. In each sub-folder, there exists 3 csv files: train, dev and test. CSV files are separated by "\t". 

The attribute ranking filels contain the following columns:
* qid: question id
* ASIN: ASIN number of the corresponding product
* qa_pair_id: question-candidate pair id
* question: question text
* candidate: candidate text
* label: 1 means that the candidate is relevant with the  question and 0 otherwise
* source: the source of the candidate, can be one of the 6 information sources included in the dataset

The data-to-text files contain the  following columns:
* ASIN: ASIN number of the corresponding product
* question: question text
* candidate: candidate text
* answer: manually written natural-sounding answer given the question and information contained in the candidate
* source: the source of the candidate, can be one of the 6 information sources included in the dataset

## ePQA

ePQA is a cleaner version of hetPQA with the following differences

The attribute ranking filels contain the following columns:
* It has higher annotation quality with rounds of verifications. In our in-house annotation, the error rate is less than 5%
* It does not restrict the product categories, while the hetPQA dataset focuses only on the toys and games product domain
* It defines finer-grained 3-class labels for each candidate, while the hetPQA dataset contains only binary labels
* Every candidate is checked with its context (surrounding sentences) to make sure the label is correct, while the hetPQA dataset does not check the context.
* For questions in the testset where none of the top-5 candidates are fully answering, we further ask annotators to actively search for the answer from the product page.

The files contain the following columns:
* ASIN: ASIN number of the corresponding product
* question: question text
* qid: question id
* candidate: candidate text
* qa_pair_id: question-answer id
* source: original source of the candidate
* context: surrounding sentences of the candidate
* label: 2 means the fully ansewring, 1 means helpful but not fully answering, 0 means irrelevant
* answer: manually written natural-sounding answer given the question and information contained in the candidate (if the candidate is fully answering)

## xPQA

xPQA is a large-scale annotated cross-lingual PQA dataset in 12 languages across 9 branches.

The files contain the following columns:
* ASIN: ASIN number of the corresponding product
* question: question text
* question_en: the translated English question
* qid: question id
* candidate: candidate text
* qa_id: question-answer id
* source: original source of the candidate
* context: surrounding sentences of the candidate
* label: 2 means the fully ansewring, 1 means helpful but not fully answering, 0 means irrelevant
* answer: manually written natural-sounding answer given the question and information contained in the candidate (if the candidate is fully answering)

"test_answerable_corrected.csv" contains only answerable questions in the "test.csv". The translations for Tamil and German are manually corrected translations instead of machine translations.

If you use these datasets, please cite out paper:
```
@inproceedings{shen-etal-2022-semipqa,
    title = "semi{PQA}: A Study on Product Question Answering over Semi-structured Data",
    author = "Shen, Xiaoyu  and
      Barlacchi, Gianni  and
      Del Tredici, Marco  and
      Cheng, Weiwei  and
      Gispert, Adri{\`a}",
    booktitle = "Proceedings of the Fifth Workshop on e-Commerce and NLP (ECNLP 5)",
    month = may,
    year = "2022",
    address = "Dublin, Ireland",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.ecnlp-1.14",
    doi = "10.18653/v1/2022.ecnlp-1.14",
    pages = "111--120",
}
```
```
@inproceedings{shen-etal-2022-product,
    title = "Product Answer Generation from Heterogeneous Sources: A New Benchmark and Best Practices",
    author = "Shen, Xiaoyu  and
      Barlacchi, Gianni  and
      Del Tredici, Marco  and
      Cheng, Weiwei  and
      Byrne, Bill  and
      Gispert, Adri{\`a}",
    booktitle = "Proceedings of the Fifth Workshop on e-Commerce and NLP (ECNLP 5)",
    month = may,
    year = "2022",
    address = "Dublin, Ireland",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.ecnlp-1.13",
    doi = "10.18653/v1/2022.ecnlp-1.13",
    pages = "99--110",
}
```
```
@article{shen2023xPQA,
  title={xPQA: Cross-Lingual Product Question Answering across 12 Languages},
  author={Shen, Xiaoyu and Asai, Akari and Byrne, Bill and Gispert, Adri\`a de},
  journal={arXiv preprint arXiv:2305.09249},
  year={2023}
}
```
## License

This library is licensed under the CDLA 1.0 Sharing License.

