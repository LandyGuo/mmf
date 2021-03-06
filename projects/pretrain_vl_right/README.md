# Visio-Linguistic Pretraining

This repository contains the code for modified implementation of VisualBERT and ViLBERT used in the folowwing paper. Please cite this paper if you are using these models:

* Singh, A., Goswami, V., & Parikh, D. (2019). *Are we pretraining it right? Digging deeper into visio-linguistic pretraining*. arXiv preprint arXiv:2004.08744. ([arXiV](https://arxiv.org/abs/2004.08744))
```
@article{singh2020we,
  title={Are we pretraining it right? Digging deeper into visio-linguistic pretraining},
  author={Singh, Amanpreet and Goswami, Vedanuj and Parikh, Devi},
  journal={arXiv preprint arXiv:2004.08744},
  year={2020}
}
```

## Installation

Clone this repository, and build it with the following command.
```
cd ~/mmf
python setup.py build develop
```

## Getting Data

We provide the different dataset features and ImDB files used for training the VisualBERT and ViLBERT models. Please follow the [Pythia documentation](https://learnpythia.readthedocs.io/en/latest/tutorials/quickstart.html#getting-data) to get data for each dataset as well as vocabulary files.

Below are the download links to the imdbs and features used for this project. **Note that LMDBs should be downloaded under `data/datasets/<dataset_name>/features/lmdbs/`. ImDB files should be extracted under `data/datasets/<dataset_name>/imdbs/`.**


| Datasets      | ImDBs | Feature LMDBs |
|--------------|----------|-------------------------------|
| COCO Captions     | [COCO ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/coco/imdbs/coco_captions.tar.gz) | [COCO trainval](https://dl.fbaipublicfiles.com/pythia/data/datasets/coco/features/lmdbs/coco_trainval2014.lmdb) [COCO test](https://dl.fbaipublicfiles.com/pythia/data/datasets/coco/features/lmdbs/coco_test2015.lmdb) |
| VQA2.0      | [VQA2.0 ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/vqa2/imdbs/vqa2.tar.gz) | [VQA2.0 trainval](https://dl.fbaipublicfiles.com/pythia/data/datasets/coco/features/lmdbs/coco_trainval2014.lmdb) [VQA2.0 test](https://dl.fbaipublicfiles.com/pythia/data/datasets/coco/features/lmdbs/coco_test2015.lmdb) |
| Concceptual Captions      | [CC ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/cc/imdbs/cc_captions.tar.gz) | [CC train](https://dl.fbaipublicfiles.com/pythia/data/datasets/cc/features/lmdbs/cc_train.lmdb) [CC val](https://dl.fbaipublicfiles.com/pythia/data/datasets/cc/features/lmdbs/cc_val.lmdb) |
| Vizwiz      | [Vizwiz ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/vizwiz/imdbs/vizwiz.tar.gz) | [Vizwiz](https://dl.fbaipublicfiles.com/pythia/data/datasets/vizwiz/features/lmdbs/vizwiz.lmdb) |
| SNLI-VE      | [SNLI ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/visual_entailment/imdbs/visual_entailment.tar.gz) | [SNLI](https://dl.fbaipublicfiles.com/pythia/data/datasets/visual_entailment/features/lmdbs/flickr30k.lmdb) |
| MM-IMDB      | [MMIMDB ImDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/mmimdb/imdbs/mmimdb.tar.gz) | [MMIMDB](https://dl.fbaipublicfiles.com/pythia/data/datasets/mmimdb/features/lmdbs/mmimdb.lmdb) |




## Training

### Pretraining

Example : To pretrain VisualBERT model on the COCO Captions dataset, run the following command
```
mmf_run config=projects/pretrain_vl_right/configs/visual_bert/masked_coco/full.yaml run_type=train_val dataset=masked_coco model=visual_bert
```

### Finetuning

Example : To finetune VisualBERT model on the VQA2.0 dataset, run the following command
```
mmf_run config=projects/visual_bert/configs/vqa2/defaults.yaml run_type=train_val dataset=vqa2 model=visual_bert checkpoint.resume_file=<path_to_pretrained_visual_bert_model> checkpoint.resume_pretrained=true
```

Configs for different settings and pretraining models are provided in the next section.

## Configs and Pretrained Models:

### VisualBERT Masked COCO

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked COCO 100%      | visual_bert | visual_bert.pretrained.coco.full             | projects/pretrain_vl_right/configs/visual_bert/masked_coco/full.yaml         |
| Masked COCO 50%      | visual_bert | visual_bert.pretrained.coco.fifty_pc              | projects/pretrain_vl_right/configs/visual_bert/masked_coco/fifty_pc.yaml         |
| Masked COCO 10%      | visual_bert | visual_bert.pretrained.coco.ten_pc              | projects/pretrain_vl_right/configs/visual_bert/masked_coco/ten_pc.yaml         |
| Masked COCO Train+Val      | visual_bert | visual_bert.pretrained.coco.full_train_val              | projects/pretrain_vl_right/configs/visual_bert/masked_coco/full_train_val.yaml        |

### VisualBERT Masked VQA2

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked VQA2 100%      | visual_bert | visual_bert.pretrained.vqa2.full             | projects/pretrain_vl_right/configs/visual_bert/masked_vqa2/full.yaml         |
| Masked VQA2 50%      | visual_bert | visual_bert.pretrained.vqa2.fifty_pc              | projects/pretrain_vl_right/configs/visual_bert/masked_vqa2/fifty_pc.yaml         |
| Masked VQA2 10%      | visual_bert | visual_bert.pretrained.vqa2.ten_pc              | projects/pretrain_vl_right/configs/visual_bert/masked_vqa2/ten_pc.yaml         |
| Masked VQA2 Train+Val      | visual_bert | visual_bert.pretrained.vqa2.full_train_val              | projects/pretrain_vl_right/configs/visual_bert/masked_vqa2/full_train_val.yaml        |

### VisualBERT Masked Conceptual Captions

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked CC 100%      | visual_bert | visual_bert.pretrained.cc.full             | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/full.yaml         |
| Masked CC 50%      | visual_bert | visual_bert.pretrained.cc.half              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/half.yaml         |
| Masked CC 10% (CC Small 100%)     | visual_bert | visual_bert.pretrained.cc.small              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/small.yaml         |
| Masked CC Small 50% (CC Small 50%)      | visual_bert | visual_bert.pretrained.cc.small_fifty_pc              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/small_fifty_pc.yaml        |
| Masked CC Small 10% (CC Small 10%)      | visual_bert | visual_bert.pretrained.cc.small_ten_pc               | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/small_ten_pc.yaml        |
| Masked CC Generated 100%      | visual_bert | visual_bert.pretrained.cc.full_coco_generated              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/full_coco_generated.yaml        |
| Masked CC Generated 50%      | visual_bert | visual_bert.pretrained.cc.half_coco_generated              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/half_coco_generated.yaml        |
| Masked CC Generated 10%      | visual_bert | visual_bert.pretrained.cc.small_coco_generated              | projects/pretrain_vl_right/configs/visual_bert/masked_conceptual_captions/small_coco_generated.yaml        |


### VisualBERT Finetuned Models

|  Finetuned Model | Pretrained Model        | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| VQA2 Train       | Masked COCO 100% | visual_bert | visual_bert.finetuned.vqa2.from_coco_train    | projects/visual_bert/configs/vqa2/defaults.yaml         |
| VQA2 Train+Val       | Masked COCO Train+Val | visual_bert | visual_bert.finetuned.vqa2.from_coco_train_val    | projects/visual_bert/configs/vqa2/train_val.yaml         |
| Vizwiz     | Masked VQA2 100% | visual_bert | visual_bert.finetuned.vizwiz.from_vqa2    | projects/visual_bert/configs/vizwiz/defaults.yaml |
| SNLI-VE        | Masked COCO 100% | visual_bert  | visual_bert.finetuned.visual_entailment.from_coco   | projects/visual_bert/configs/visual_entailment/defaults.yaml          |
| MMIMDB      | - | visual_bert    | visual_bert.finetuned.mmimdb.direct  | projects/visual_bert/configs/mmimdb/defaults.yaml   |

### ViLBERT Masked COCO

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked COCO 100%      | vilbert | vilbert.pretrained.coco              | projects/pretrain_vl_right/configs/vilbert/masked_coco/full.yaml         |

### ViLBERT Masked VQA2

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked VQA2 100%      | vilbert | vilbert.pretrained.vqa2              | projects/pretrain_vl_right/configs/vilbert/masked_vqa2/full.yaml         |


### ViLBERT Masked Conceptual Captions

| Pretrained model         | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| Masked CC 100%       | vilbert | vilbert.pretrained.cc.full              | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/full.yaml         |
| Masked CC 50%     | vilbert | vilbert.pretrained.cc.half            | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/half.yaml |
| Masked CC 10% (CC Small 100%)        | vilbert  | vilbert.pretrained.cc.small                       | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/small.yaml          |
| Masked CC Generated 100%      | vilbert    | vilbert.pretrained.cc.full_coco_generated                        | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/full_coco_generated.yaml   |
| Masked CC Generated 50%       | vilbert    | vilbert.pretrained.cc.half_coco_generated                    | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/half_coco_generated.yaml   |
| Masked CC Generated 10%       | vilbert           | vilbert.pretrained.cc.small_coco_generated                      | projects/pretrain_vl_right/configs/vilbert/masked_conceptual_captions/small_coco_generated.yaml          |



### ViLBERT Finetuned Models

|  Finetuned Model | Pretrained Model        | Model Key      | Pretrained Key                                   | Config                                                     |
|------------------|------------------|----------------|--------------------------------------------------|------------------------------------------------------------|
| VQA2 Train       | Masked VQA2 100% | vilbert | vilbert.finetuned.vqa2.from_vqa2_train    | projects/vilbert/configs/vqa2/defaults.yaml         |
| Vizwiz     | Masked COCO 100%  | vilbert | vilbert.finetuned.vizwiz.from_coco    | projects/vilbert/configs/vizwiz/defaults.yaml |
| SNLI-VE        | Masked COCO 100%  | vilbert  | vilbert.finetuned.visual_entailment.from_coco   | projects/vilbert/configs/visual_entailment/defaults.yaml          |
| MMIMDB      | - | vilbert    | vilbert.finetuned.mmimdb.direct  | projects/vilbert/configs/mmimdb/defaults.yaml   |
