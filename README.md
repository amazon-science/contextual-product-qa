## Contextual Product Question Answering

Contextual Product question answering (CPQA) has been a hot topic in e-commerce applications. Given a question about a product (context), the PQA system will search the product page and provide an instant answer, so that customers do not need to traverse over the page by themselves or seek help from real humans.
This can greatly improve their online shopping experience while significantly reducing the cost of customer service support.
This repository holds datasets supporting the contextual product question answering task.

Right now it includes two datasets:

* **semiPQA**: Question answering from semi-structured data described [in this paper](https://aclanthology.org/2022.ecnlp-1.14.pdf).
* **USB**: Question answering from heterogeneous data described [in this paper](https://aclanthology.org/2022.ecnlp-1.13.pdf).

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

If you use this dataset, please cite out paper:

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
## USB

It is of great value to answer product questions based on heterogeneous information sources available on web product pages, e.g., semi-structured attributes, text descriptions, userprovided contents, etc. USB is a large-scale benchmark dataset for answering product questions from 6 heterogeneous sources:
* semi-structured attribute: Product attributes in json format as in the semiPQA dataset.
* bullet point: Product summaries in the form of bullet points from the product page.
* product description: Product descriptions from the manufacturer and Amazon.
* on-site publication: Manually written Publications about products (for example [here](https://www.amazon.com/ospublishing/story/14423b91-4203-413e-a885-6005dca8d68e)).
* user review: User reviews written for the product.
* community answer: Top-voted community answers. Answers directly replying to questions in our question set are discarded

The USB dataset features (1) It provides clear annotations for both evidence ranking and answer generation, enabling us to perform in-depth evaluation of these two components separately. (2) We consider a mix of 6 heterogeneous sources, ranging from semi-structured specifications (jsons) to free sentences and (3) It represents naturally-occurring questions, unlike previous collections that elicited questions by showing answers explicitly. Questions from the USB dataset are all about the "toys and games" product category.

The USB folder contains the dataset. It contains two sub-folders for the evidence ranking and answer generation respectively. In each sub-folder, there exists 3 csv files: train, dev and test. CSV files are separated by "\t". 

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

If you use this dataset, please cite out paper:

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

## License

This library is licensed under the CDLA 1.0 Sharing License.

