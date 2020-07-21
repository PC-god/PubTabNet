# PubTabNet

PubTabNet is a large dataset for image-based table recognition, containing 568k+ images of tabular data annotated with the corresponding HTML representation of the tables. The table images are extracted from the scientific publications included in the [PubMed Central Open Access Subset (commercial use collection)](https://www.ncbi.nlm.nih.gov/pmc/tools/openftlist/). Table regions are identified by matching the PDF format and the XML format of the articles in the PubMed Central Open Access Subset. More details are available in our paper ["Image-based table recognition: data, model, and evaluation"](https://arxiv.org/abs/1911.10683).

## Headlines

`21/July/2020` - PubTabNet 2.0.0 is released, where the position (bounding box) of non-empty cells is added into the annotation. The annotation file is also changed from `json` format to `jsonl` format to reduce the requirement on large RAM.

`03/July/2020` - `Image-based table recognition: data, model, and evaluation` is accepted by ECCV20.

`01/July/2020` - Code of **T**ree-**Edit**-**D**istance-based **S**imilarity (TEDS) metric is [released](src).

## Updates in progress

### Encoder-dual-decoder model

In our paper, we proposed a new encoder-dual-decoder architecture, which was trained on PubTabNet and can accurately reconstruct the HTML representation of complex tables solely relying on image input. Due to legal constraints, the source code of the model will not be released.

### Ground truth of test set

The ground truth of test will not be release, as we want to keep it for a competition in the future. We will offer a service for people to submit and evaluate their results soon.

## Getting data

Images and annotations can be downloaded [here](https://developer.ibm.com/exchanges/data/all/pubtabnet/). If you want to download the data from the command line, you can use curl or wget to download the data.

```
curl -o <YOUR_TARGET_DIR>/PubTabNet.tar.gz https://dax-cdn.cdn.appdomain.cloud/dax-pubtabnet/2.0.0/pubtabnet.tar.gz
```

```
wget -O <YOUR_TARGET_DIR>/PubTabNet.tar.gz https://dax-cdn.cdn.appdomain.cloud/dax-pubtabnet/2.0.0/pubtabnet.tar.gz
```

## Annotation structure

The annotation is in the jsonl (jsonlines) format, where each line contains the annotations on a given sample in the following format:
The structure of the annotation jsonl file is:

```
{
   'filename': str,
   'split': str,
   'imgid': int,
   'html': {
     'structure': {'tokens': [str]},
     'cell': [
       {
         'tokens': [str],
         'bbox': [x0, y0, x1, y1]  # only non-empty cells have this attribute
       }
     ]
   }
}
```

## Cite us

```
@article{zhong2019image,
  title={Image-based table recognition: data, model, and evaluation},
  author={Zhong, Xu and ShafieiBavani, Elaheh and Yepes, Antonio Jimeno},
  journal={arXiv preprint arXiv:1911.10683},
  year={2019}
}
```

## Examples

A [Jupyter notebook](./exploring_PubTabNet_dataset.ipynb) is provided to inspect the annotations of 20 sample tables.


## Related links

[PubLayNet](https://github.com/ibm-aur-nlp/PubLayNet) is a large dataset of document images, of which the layout is annotated with both bounding boxes and polygonal segmentations. The source of the documents is [PubMed Central Open Access Subset (commercial use collection)](https://www.ncbi.nlm.nih.gov/pmc/tools/openftlist/). The annotations are automatically generated by matching the PDF format and the XML format of the articles in the PubMed Central Open Access Subset. More details are available in our paper ["PubLayNet: largest dataset ever for document layout analysis."](https://arxiv.org/abs/1908.07836), which was awarded the [best paper at ICDAR 2019](http://icdar2019.org/award/)!
