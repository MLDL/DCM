Knowledge Transfer via Dense Cross-layer Mutual-distillation
=============

This repo contains code for the experiments in <a href="https://arxiv.org/pdf/2008.07816.pdf" target="_blank">Knowledge Transfer via Dense Cross-layer Mutual-distillation</a> (ECCV'2020) by Anbang Yao and Dawei Sun. This repo was developed based on the official pytorch implementation of <a href="https://github.com/szagoruyko/wide-residual-networks/tree/master/pytorch" target="_blank"> WRN </a>.

<img width="787" alt="illustration" src="images/illustration.png">

*Figure 1: Overall architecture of the proposed training framwork.*

<br>

Knowledge Distillation (KD) based methods adopt the oneway Knowledge Transfer (KT) scheme in which training a lower-capacity student network is guided by a pre-trained high-capacity teacher network. Recently, Deep Mutual Learning (DML) presented a two-way KT strategy, showing that the student network can be also helpful to improve the teacher network. In this paper, we propose Dense Crosslayer Mutual-distillation (DCM), an improved two-way KT method in which the teacher and student networks are trained collaboratively from scratch. To augment knowledge representation learning, well-designed auxiliary classifiers are added to certain hidden layers of both teacher and student networks. To boost KT performance, we introduce dense bidirectional KD operations between the layers appended with classifiers. After training, all auxiliary classifiers are discarded, and thus there are no extra parameters introduced to final models. We test our method on a variety of KT tasks, showing its superiorities over related methods.

Testing error (%, mean +/- std over 5 runs) on CIFAR-100:

Net 1 \| Net 2          |   baseline<br>Net 1 \| Net 2   |      DML<br>Net 1 \| Net 2     |      DCM<br>Net 1 \| Net 2
-----------------|:------------:|:-------------:|:-------------:
WRN-28-10 \| WRN-28-10 | 18.72 +/- 0.24 \| 18.72 +/- 0.24 | 17.89 +/- 0.26 \| 17.95 +/- 0.07 | 16.61 +/- 0.24 \| 16.65 +/- 0.22
WRN-28-10 \| MobileNet | 18.72 +/- 0.24 \| 26.30 +/- 0.35 | 17.24 +/- 0.13 \| 23.91 +/- 0.22 | 16.83 +/- 0.07 \| 21.43 +/- 0.20

See https://arxiv.org/abs/xxxx for details.

<img width="787" alt="CIFAR_error_rate" src="images/testing_error.png">

*Figure 2: Error rate of WRN-28-10 on CIFAR-100. (The results were averaged over 5 runs.)*

<br>

bibtex:
```
@inproceedings{Yao2020DCM,
  title={Knowledge Transfer via Dense Cross-layer Mutual-distillation},
  author={Yao, Anbang and Sun, Dawei},
  booktitle={Proceedings of the European Conference on Computer Vision},
  year={2020}
}
```

# Usage

### Install requirements

```
pip install -r requirements.txt
```

### Run DCM on CIFAR-100

```
# train wrn-28-10 v.s. wrn-28-10
cd wrn/
mkdir logs
python main.py --save ./logs/wrn-28-10 --depth 28 --width 10 --dataroot [path to the CIFAR dataset]
```

```
# train wrn-28-10 v.s. mobilenet
cd wrn_mobi/
mkdir logs
python main.py --save ./logs/wrn-28-10_mobilenet --dataroot [path to the CIFAR dataset]
```
