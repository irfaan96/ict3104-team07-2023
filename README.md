<h1><strong>ICT3104 Team 7</strong></h1>

## Contributors

| Name                     | GitHub Profile         | Student ID |
|--------------------------|------------------------|------------|
| Zafrulla Kamil Bin Saleem| [ZafrullaKamil](https://github.com/ZafrullaKamil) | 2100764 |
| Lee Yong Chong           | [2100711](https://github.com/2100711) | 2100711 |
| K M Irfaan Ahmed         | [irfaan96](https://github.com/irfaan96) | 2100701 |
| Sachin Agrawal           | [sachinagrawal19](https://github.com/sachinagrawal19) | 2100805 |
| Chang Wee Siang Wilson   | [criss-xyriss](https://github.com/criss-xyriss) | 2101446 |

## Running on Google Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](PASTE_YOUR_NOTEBOOK_URL_HERE)

## Environment Setup
We used `conda` in `Ubuntu` to setup the project environment.

Follow this steps to setup the environment:

1. Update system repositories.

```bash
sudo apt update
```

2. Install curl package.

```bash
sudo apt install curl -y
```

3. Prepare `Anaconda` installation script.

```bash
curl --output anaconda.sh https://repo.anaconda.com/archive/Anaconda3-2023.09-0-Linux-x86_64.sh

sha256sum anaconda.sh
```

4. Install Anaconda.

```bash
bash anaconda.sh
```
> Note: Follow the instructions on the screen. You can press `Enter` to accept the defaults. Do not forget to say `yes` when the installer asks if you want to initialize `Anaconda3` by running `conda init`.

6. Activate the installation.

```bash
source ~/.bashrc
```

7. Verify the installation.

```bash
conda list or conda --version
```

8. Create a new environment with the following command.

```bash
conda create -n fupose python=3.8
```

9. Activate the environment with the following command.

```bash
conda activate fupose
```

11. Clone this repository to your preferred location.

```bash
git clone https://github.com/irfaan96/ict3104-team07-2023.git
```

12. Navigate to the root directory of the project.

```bash
cd ict3104-team07-2023
```

13. Install `jupyter notebook`.

```bash
conda install jupyter notebook
```

14. Run `jupyter notebook`.

```bash
jupyter notebook
```

15. Run `ICT3104_Project.ipynb` notebook.


## References

- [FollowYourPose](https://github.com/mayuelala/FollowYourPose)
- [MMPose](https://github.com/open-mmlab/mmpose)
- [Charades dataset](https://prior.allenai.org/projects/charades)
- [Sims4Action dataset](https://github.com/aroitberg/sims4action)
- [FFmpeg](https://www.ffmpeg.org/)
- [MediaPipe](https://github.com/google/mediapipe)
- [Anaconda Installation](https://linuxhint.com/install-anaconda-ubuntu-22-04/)
- [NVIDIA CUDA Toolkit](https://developer.nvidia.com/cuda-downloads)

## Citation

Yue Ma, Yingqing He, Xiaodong Cun, Xintao Wang, Ying Shan, Xiu Li, Qifeng Chen. (2023).

- [Follow Your Pose Repository](https://github.com/mayuelala/FollowYourPose)
- [Research Paper](https://arxiv.org/abs/2304.01186)

## Acknowledgements
This repository borrows heavily from [Tune-A-Video](https://github.com/showlab/Tune-A-Video) and [FateZero](https://github.com/ChenyangQiQi/FateZero). Thanks the authors for sharing their code and models.
