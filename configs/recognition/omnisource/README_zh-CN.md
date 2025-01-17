# Omni-sourced Webly-supervised Learning for Video Recognition

[Haodong Duan](https://github.com/kennymckormick), [Yue Zhao](https://github.com/zhaoyue-zephyrus), [Yuanjun Xiong](https://github.com/yjxiong), Wentao Liu, [Dahua Lin](https://github.com/lindahua)

In ECCV, 2020. [Paper](https://arxiv.org/abs/2003.13042)

![pipeline](https://github.com/open-mmlab/mmaction2/blob/master/configs/recognition/omnisource/pipeline.png?raw=true)

## 模型库

### Kinetics-400

MMAction2 当前公开了 4 个 OmniSource 框架训练的模型，包含 2D 架构与 3D 架构。下表比较了使用或不适用 OmniSource 框架训练得的模型在 Kinetics-400 上的精度：

|   模型   | 模态 |  预训练  | 主干网络  | 输入 |     分辨率     | Top-1 准确率(Baseline / OmniSource (Delta)) | Top-5 准确率(Baseline / OmniSource (Delta))) |                         模型下载链接                         |
| :------: | :--: | :------: | :-------: | :--: | :------------: | :-----------------------------------------: | :------------------------------------------: | :----------------------------------------------------------: |
|   TSN    | RGB  | ImageNet | ResNet50  | 3seg |    340x256     |             70.6 / 73.6 (+ 3.0)             |             89.4 / 91.0 (+ 1.6)              | [Baseline](https://download.openmmlab.com/mmaction/recognition/tsn/tsn_r50_1x1x3_100e_kinetics400_rgb/tsn_r50_1x1x3_100e_kinetics400_rgb_20200614-e508be42.pth) / [OmniSource](https://download.openmmlab.com/mmaction/recognition/tsn/omni/tsn_imagenet_pretrained_r50_omni_1x1x3_kinetics400_rgb_20200926-54192355.pth) |
|   TSN    | RGB  |  IG-1B   | ResNet50  | 3seg | short-side 320 |             73.1 / 75.7 (+ 2.6)             |             90.4 / 91.9 (+ 1.5)              | [Baseline](https://download.openmmlab.com/mmaction/recognition/tsn/omni/tsn_1G1B_pretrained_r50_without_omni_1x1x3_kinetics400_rgb_20200926-c133dd49.pth) / [OmniSource](https://download.openmmlab.com/mmaction/recognition/tsn/omni/tsn_1G1B_pretrained_r50_omni_1x1x3_kinetics400_rgb_20200926-2863fed0.pth) |
| SlowOnly | RGB  | Scratch  | ResNet50  | 4x16 | short-side 320 |             72.9 / 76.8 (+ 3.9)             |             90.9 / 92.5 (+ 1.6)              | [Baseline](https://download.openmmlab.com/mmaction/recognition/slowonly/slowonly_r50_4x16x1_256e_kinetics400_rgb/slowonly_r50_4x16x1_256e_kinetics400_rgb_20200704-a69556c6.pth) / [OmniSource](https://download.openmmlab.com/mmaction/recognition/slowonly/omni/slowonly_r50_omni_4x16x1_kinetics400_rgb_20200926-51b1f7ea.pth) |
| SlowOnly | RGB  | Scratch  | ResNet101 | 8x8  | short-side 320 |             76.5 / 80.4 (+ 3.9)             |             92.7 / 94.4 (+ 1.7)              | [Baseline](https://download.openmmlab.com/mmaction/recognition/slowonly/omni/slowonly_r101_without_omni_8x8x1_kinetics400_rgb_20200926-0c730aef.pth) / [OmniSource](https://download.openmmlab.com/mmaction/recognition/slowonly/omni/slowonly_r101_omni_8x8x1_kinetics400_rgb_20200926-b5dbb701.pth) |

## Mini-Kinetics 上的基准测试

OmniSource 项目当前公开了所采集网络数据的一个子集，涉及 [Mini-Kinetics](https://arxiv.org/pdf/1712.04851.pdf) 中的 200 个动作类别。[OmniSource 数据集准备](/tools/data/omnisource/README_zh-CN.md) 中记录了这些数据集的详细统计信息。用户可以通过填写 [申请表](https://docs.google.com/forms/d/e/1FAIpQLSd8_GlmHzG8FcDbW-OEu__G7qLgOSYZpH-i5vYVJcu7wcb_TQ/viewform?usp=sf_link) 获取这些数据，在完成填写后，数据下载链接会被发送至用户邮箱。更多关于 OmniSource 网络数据集的信息请参照 [OmniSource 数据集准备](/tools/data/omnisource/README_zh-CN.md)。

MMAction2 在公开的数据集上进行了 OmniSource 框架的基准测试，下表记录了详细的结果（在 Mini-Kinetics 验证集上的精度），这些结果可以作为使用网络数据训练视频识别任务的基线。

### TSN-8seg-ResNet50

|   Setting    | Top-1 | Top-5 |                             ckpt                             |                             json                             |                             log                              |
| :----------: | :---: | :---: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   Baseline   | 77.4  | 93.6  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/baseline/tsn_r50_1x1x8_100e_minikinetics_rgb_20201030-b4eaf92b.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/baseline/tsn_r50_1x1x8_100e_minikinetics_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/baseline/tsn_r50_1x1x8_100e_minikinetics_rgb_20201030.log) |
|   +GG-img    | 78.0  | 93.6  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/googleimage/tsn_r50_1x1x8_100e_minikinetics_googleimage_rgb_20201030-23966b4b.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/googleimage/tsn_r50_1x1x8_100e_minikinetics_googleimage_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/googleimage/tsn_r50_1x1x8_100e_minikinetics_googleimage_rgb_20201030.log) |
| +[GG-IG]-img | 78.6  | 93.6  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/webimage/tsn_r50_1x1x8_100e_minikinetics_webimage_rgb_20201030-66f5e046.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/webimage/tsn_r50_1x1x8_100e_minikinetics_webimage_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/webimage/tsn_r50_1x1x8_100e_minikinetics_webimage_rgb_20201030.log) |
|   +IG-vid    | 80.6  | 95.0  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/insvideo/tsn_r50_1x1x8_100e_minikinetics_insvideo_rgb_20201030-011f984d.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/insvideo/tsn_r50_1x1x8_100e_minikinetics_insvideo_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/insvideo/tsn_r50_1x1x8_100e_minikinetics_insvideo_rgb_20201030.log) |
|    +KRaw     | 78.6  | 93.2  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/kineticsraw/tsn_r50_1x1x8_100e_minikinetics_kineticsraw_rgb_20201030-59f5d064.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/kineticsraw/tsn_r50_1x1x8_100e_minikinetics_kineticsraw_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/kineticsraw/tsn_r50_1x1x8_100e_minikinetics_kineticsraw_rgb_20201030.log) |
|  OmniSource  | 81.3  | 94.8  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/omnisource/tsn_r50_1x1x8_100e_minikinetics_omnisource_rgb_20201030-0f56ef51.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/omnisource/tsn_r50_1x1x8_100e_minikinetics_omnisource_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/tsn_r50_1x1x8_100e_minikinetics_rgb/omnisource/tsn_r50_1x1x8_100e_minikinetics_omnisource_rgb_20201030.log) |

### SlowOnly-8x8-ResNet50

|   Setting    | Top-1 | Top-5 |                             ckpt                             |                             json                             |                             log                              |
| :----------: | :---: | :---: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   Baseline   | 78.6  | 93.9  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/baseline/slowonly_r50_8x8x1_256e_minikinetics_rgb_20201030-168eb098.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/baseline/slowonly_r50_8x8x1_256e_minikinetics_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/baseline/slowonly_r50_8x8x1_256e_minikinetics_rgb_20201030.log) |
|   +GG-img    | 80.8  | 95.0  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/googleimage/slowonly_r50_8x8x1_256e_minikinetics_googleimage_rgb_20201030-7da6dfc3.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/googleimage/slowonly_r50_8x8x1_256e_minikinetics_googleimage_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/googleimage/slowonly_r50_8x8x1_256e_minikinetics_googleimage_rgb_20201030.log) |
| +[GG-IG]-img | 81.3  | 95.2  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/webimage/slowonly_r50_8x8x1_256e_minikinetics_webimage_rgb_20201030-c36616e9.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/webimage/slowonly_r50_8x8x1_256e_minikinetics_webimage_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/webimage/slowonly_r50_8x8x1_256e_minikinetics_webimage_rgb_20201030.log) |
|   +IG-vid    | 82.4  | 95.6  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/insvideo/slowonly_r50_8x8x1_256e_minikinetics_insvideo_rgb_20201030-e2890e8d.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/insvideo/slowonly_r50_8x8x1_256e_minikinetics_insvideo_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/insvideo/slowonly_r50_8x8x1_256e_minikinetics_insvideo_rgb_20201030.log) |
|    +KRaw     | 80.3  | 94.5  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/kineticsraw/slowonly_r50_8x8x1_256e_minikinetics_kineticsraw_rgb_20201030-62974bac.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/kineticsraw/slowonly_r50_8x8x1_256e_minikinetics_kineticsraw_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/kineticsraw/slowonly_r50_8x8x1_256e_minikinetics_kineticsraw_rgb_20201030.log) |
|  OmniSource  | 82.9  | 95.8  | [ckpt](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/omnisource/slowonly_r50_8x8x1_256e_minikinetics_omnisource_rgb_20201030-284cfd3b.pth) | [json](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/omnisource/slowonly_r50_8x8x1_256e_minikinetics_omnisource_rgb_20201030.json) | [log](https://download.openmmlab.com/mmaction/recognition/omnisource/slowonly_r50_8x8x1_256e_minikinetics_rgb/omnisource/slowonly_r50_8x8x1_256e_minikinetics_omnisource_rgb_20201030.log) |

下表列出了原论文中在 Kinetics-400 上进行基准测试的结果供参考：

|         Model          |  Baseline   |   +GG-img   | +[GG-IG]-img |   +IG-vid   |    +KRaw    | OmniSource  |
| :--------------------: | :---------: | :---------: | :----------: | :---------: | :---------: | :---------: |
|   TSN-3seg-ResNet50    | 70.6 / 89.4 | 71.5 / 89.5 | 72.0 / 90.0  | 72.0 / 90.3 | 71.7 / 89.6 | 73.6 / 91.0 |
| SlowOnly-4x16-ResNet50 | 73.8 / 90.9 | 74.5 / 91.4 | 75.2 / 91.6  | 75.2 / 91.7 | 74.5 / 91.1 | 76.6 / 92.5 |

## 注：

如果 OmniSource 项目对您的研究有所帮助，请使用以下 BibTex 项进行引用：

[ALGORITHM]

```BibTeX
@article{duan2020omni,
  title={Omni-sourced Webly-supervised Learning for Video Recognition},
  author={Duan, Haodong and Zhao, Yue and Xiong, Yuanjun and Liu, Wentao and Lin, Dahua},
  journal={arXiv preprint arXiv:2003.13042},
  year={2020}
}
```
