# DAFNe: A One-Stage Anchor-Free Approach for Oriented Object Detection (modified)


<img src="./res/header.png"/>

Code for our Paper [DAFNe: A One-Stage Anchor-Free Approach for Oriented Object Detection](https://arxiv.org/abs/2109.06148).
 	
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/dafne-a-one-stage-anchor-free-deep-model-for/one-stage-anchor-free-oriented-object-1)](https://paperswithcode.com/sota/one-stage-anchor-free-oriented-object-1?p=dafne-a-one-stage-anchor-free-deep-model-for)</br>
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/dafne-a-one-stage-anchor-free-deep-model-for/one-stage-anchor-free-oriented-object-2)](https://paperswithcode.com/sota/one-stage-anchor-free-oriented-object-2?p=dafne-a-one-stage-anchor-free-deep-model-for)</br>
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/dafne-a-one-stage-anchor-free-deep-model-for/one-stage-anchor-free-oriented-object-3)](https://paperswithcode.com/sota/one-stage-anchor-free-oriented-object-3?p=dafne-a-one-stage-anchor-free-deep-model-for)

## Datasets

- UCAS-AOD: https://hyper.ai/datasets/5419
- DOTA 1.0/1.5: https://captain-whu.github.io/DOTA/index.html
  - Note: See [./tools/prepare_dota/](./tools/prepare_dota/) for instructions on how to prepare the DOTA datasets.
- HRSC2016: https://www.kaggle.com/guofeng/hrsc2016

## Setup
```bash
git clone https://github.com/tae-mo/DAFNe.git
cd DAFNe
pip install -r requirements.txt
```

## Docker Setup
prerequisite: **nvidia-docker**

if needed: [Install Nvidia-docker](https://www.notion.so/docker-1d1199fb3c574acbbce4978efefe1016)

Use the `Dockerfile` to build the necessary docker image:

``` bash
docker build -t dafne .
```

## Split Data
```bash
# default crop: resolution 1024, overlap 200
# can be changed
python tools/prepare_dota/split_dota.py --srcpath <DOTA-dir> --dstpath <split-data-dir> --dota-version <1.0 or 1.5>
```

## Training

Check out `./configs/pre-trained/` for different pre-defined configurations for the DOTA 1.0, DOTA 1.5, UCAS-AOD, and HRSC2016 datasets. Use these paths as argument for the `--config-file` option below.


### With Docker

Use the `./tools/run.py` helper to start running experiments

```bash
./tools/run.py --gpus 0,1,2,3 --config-file ./configs/dota-1.0/1024.yaml --data-dir <dota-split-dir>
```

### Pre-Trained Weights Usage in (when you test your model)
```bash
./tools/run.py --gpus 0 --config-file <CONFIG_PATH in ./results> --opts "MODEL.WEIGHTS <WEIGHTS_PATH>" --data-dir <data-dir> --output-dir <output-dir> --eval-only
```

## Pre-Trained Weights

| Dataset  | mAP (%) | Config                                                          | Weights                                                                                                    |
|----------|---------|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| UCAS-AOD | 89.65   | [ucas_aod_r101_ms](./configs/pre-trained/ucas_aod_r101_ms.yaml) | [ucas-aod-r101-ms.pth](https://drive.google.com/file/d/1snC7IU-ud-d6L_AxbDx_HG8QBINP2_RO/view?usp=sharing) |
| HRSC2016 | 89.76   | [hrsc_r50_ms](./configs/pre-trained/hrsc_r50_ms.yaml)           | [hrsc-r50-ms.pth](https://drive.google.com/file/d/10i3pHxiHgjJGzJoZK-HtNdsAyfGD5Ydj/view?usp=sharing)      |
| DOTA 1.0 | 76.95   | [dota-1.0_r101_ms](./configs/pre-trained/dota-1.0_r101_ms.yaml) | [dota-1.0-r101-ms.pth](https://drive.google.com/file/d/1-lgSLhKQSZBogI2YD0r64wjJV6k2xL4E/view?usp=sharing) |
| DOTA 1.5 | 71.99   | [dota-1.5_r101_ms](./configs/pre-trained/dota-1.5_r101_ms.yaml) | [dota-1.5-r101-ms.pth](https://drive.google.com/file/d/1MQbTngieoWh-DcJL-z55RnI3PUNeSvBv/view?usp=sharing) |
