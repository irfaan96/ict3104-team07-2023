<div align="center">
<h1 align="center"><strong>ICT3104 Team 7</strong></h1>
<h2><font color="red"> 🕺🕺🕺 Follow Your Pose 💃💃💃 </font><br>
Pose-Guided Text-to-Video Generation using Pose-Free Videos</h2></div>

# Contributors

[Zafrulla Kamil Bin Saleem](https://github.com/ZafrullaKamil) - [2100764](2100764@sit.singaporetech.edu.sg)<br>
[Lee Yong Chong](https://github.com/2100711) - [2100711](2100711@sit.singaporetech.edu.sg)<br>
[K M Irfaan Ahmed](https://github.com/irfaan96) - [2100701](2100701@sit.singaporetech.edu.sg)<br>
[Sachin Agrawal](https://github.com/sachinagrawal19) - [2100805](2100805@sit.singaporetech.edu.sg)<br>
[Chang Wee Siang Wilson](https://github.com/criss-xyriss) - [2101446](2101446@sit.singaporetech.edu.sg)


<table class="center">
  <td><img src="gif_results/new_result_0830/a_man_in_the_park.gif"></td>
  <td><img src="gif_results/new_result_0830/a_Iron_man_in_the_street.gif"></td>
  <tr>
  <td width=25% style="text-align:center;">"The man is sitting on chair, on the park"</td>
  <td width=25% style="text-align:center;">"The Iron man, on the street
"</td>
  <!-- <td width=25% style="text-align:center;">"Wonder Woman, wearing a cowboy hat, is skiing"</td>
  <td width=25% style="text-align:center;">"A man, wearing pink clothes, is skiing at sunset"</td> -->
</tr>
<td><img src="gif_results/new_result_0830/a_strom.gif"></td>
<td><img src="gif_results/new_result_0830/a_astronaut_cartoon.gif"></td>
<tr>
<td width=25% style="text-align:center;">"The stormtrooper, in the gym
"</td>
<td width=25% style="text-align:center;">"The astronaut, earth background, Cartoon Style
"</td>
</tr>
</table >

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

12. Install necessary packages.

```bash
pip install -U --pre triton

pip install diffusers==0.11.1 torch==1.13.1 transformers==4.26.0 bitsandbytes==0.35.4 moviepy decord accelerate omegaconf einops ftfy gradio imageio-ffmpeg --extra-index-url https://download.pytorch.org/whl/cu113
```

13. Install project dependencies from `requirements.txt` in the root directory.

```bash
pip install -r requirements.txt
```

14. Installing `xformers`.

```bash
pip install https://github.com/brian6091/xformers-wheels/releases/download/0.0.15.dev0%2B4c06c79/xformers-0.0.15.dev0+4c06c79.d20221205-cp38-cp38-linux_x86_64.whl
```

15. Create a new folder `checkpoints` in the root directory.
16. Configure Git LFS:

```bash
sudo apt install git-lfs
git lfs install
```

17. Clone HuggingFace model repository:

```bash
git clone https://huggingface.co/YueMafighting/FollowYourPose_v1
```

18. Copy the contents of the cloned repository to the `checkpoints` folder

```bash
mv FollowYourPose_v1/* checkpoints/
```

19. Remove the cloned repository:

```bash
rm -rf FollowYourPose_v1
```

## 💃💃💃 Training
We fix the bug in Tune-a-video and finetune stable diffusion-1.4 on 8 A100.
To fine-tune the text-to-image diffusion models for text-to-video generation, run this command:

```bash
TORCH_DISTRIBUTED_DEBUG=DETAIL accelerate launch \
    --multi_gpu --num_processes=8 --gpu_ids '0,1,2,3,4,5,6,7' \
    train_followyourpose.py \
    --config="configs/pose_train.yaml" 
```

## 🕺🕺🕺 Inference
Once the training is done, run inference:

```bash
TORCH_DISTRIBUTED_DEBUG=DETAIL accelerate launch \
    --gpu_ids '0' \
    txt2video.py \
    --config="configs/pose_sample.yaml" \
    --skeleton_path="./pose_example/vis_ikun_pose2.mov"
```
You could make the pose video by [mmpose](https://github.com/open-mmlab/mmpose) , we detect the skeleton by [HRNet](https://mmpose.readthedocs.io/en/latest/model_zoo_papers/backbones.html#hrnet-cvpr-2019).  You just need to run the video demo to obtain the pose video.  Remember to replace the background with black.


## 💃💃💃 Local Gradio Demo
You could run the gradio demo locally, only need a `A100/3090`.
```bash
python app.py
```
then the demo is running on local URL:  `http://0.0.0.0:Port`

## 🕺🕺🕺 Weight
[Stable Diffusion] [Stable Diffusion](https://arxiv.org/abs/2112.10752) is a latent text-to-image diffusion model capable of generating photo-realistic images given any text input. The pre-trained Stable Diffusion models can be downloaded from Hugging Face (e.g., [Stable Diffusion v1-4](https://huggingface.co/CompVis/stable-diffusion-v1-4))


[FollowYourPose] We also provide our pretrained checkpoints in [Huggingface](https://huggingface.co/YueMafighting/FollowYourPose_v1/tree/main). you could download them and put them into `checkpoints` folder to inference our models.


```bash
FollowYourPose
├── checkpoints
│   ├── followyourpose_checkpoint-1000
│   │   ├──...
│   ├── stable-diffusion-v1-4
│   │   ├──...
│   └── pose_encoder.pth
```


## 💃💃💃 Results
We show our results regarding various pose sequences and text prompts.

Note mp4 and gif files in this github page are compressed. 
Please check our [Project Page](https://follow-your-pose.github.io/) for mp4 files of original video results.
<table class="center">
<tr>
  <td><img src="gif_results/new_result_0830/Trump_on_the_mountain.gif"></td>
  <td><img src="gif_results/new_result_0830/Trump_wear_yellow.gif"></td>
  <td><img src="gif_results/new_result_0830/astranaut_on_the_mountain.gif"></td>
</tr>
<tr>
  <td width=25% style="text-align:center;">"Trump, on the mountain
"</td>
  <td width=25% style="text-align:center;">"man, on the mountain
"</td>
  <td width=25% style="text-align:center;">"astronaut, on mountain"</td>
</tr>
</table>
<!--#########################################################-->
<table class="center">
<tr>
  <td><img src="gif_results/new_result_0830/a_girl_yellow.gif"></td>
  <td><img src="gif_results/new_result_0830/a_Iron_man_on_the_beach.gif"></td>
  <td><img src="gif_results/new_result_0830/hulk_on_the_mountain.gif"></td>
</tr>
<tr>
  <td width=25% style="text-align:center;">"girl, simple background"</td>
  <td width=25% style="text-align:center;">"A Iron man, on the beach"</td>
  <td width=25% style="text-align:center;">"A Hulk, on the mountain"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/new_result_0830/a_policeman_in_the_street.gif"></td>
  <td><img src="gif_results/new_result_0830/a_girl_in_the_forest.gif"></td>
  <td><img src="gif_results/new_result_0830/Iron_man_in_the_street.gif"></td>
</tr>
<tr>
  <td width=25% style="text-align:center;">"A policeman, on the street"</td>
  <td width=25% style="text-align:center;">"A girl, in the forest"</td>
  <td width=25% style="text-align:center;">"A Iron man, on the street"</td>
</tr>
</table>
<!--#########################################################-->
<table class="center">
<tr>
  <td><img src="gif_results/A Robot is dancing in Sahara desert.gif"></td>
  <td><img src="gif_results/sdsdA Iron man on the beach.gif"></td>
  <td><img src="gif_results/A Panda on the sea.gif"></td>
</tr>
<tr>
  <td width=25% style="text-align:center;">"A Robot, in Sahara desert"</td>
  <td width=25% style="text-align:center;">"A Iron man, on the beach"</td>
  <td width=25% style="text-align:center;">"A panda, son the sea"</td>
</tr>
</table>
<!--#########################################################-->
<table class="center">
<tr>
  <td><img src="gif_results/a man in the park, Van Gogh style.gif"></td>
  <td><img src="gif_results/fireman in the beach.gif"></td>
  <td><img src="gif_results/Batman brown background.gif"></td>
</tr>
<tr>
</tr>
<tr>
  <td width=25% style="text-align:center;">"A man in the park, Van Gogh style"</td>
  <td width=25% style="text-align:center;">"The fireman in the beach"</td>
  <td width=25% style="text-align:center;">"Batman, brown background"</td>
</tr>
</table>
<!--#########################################################-->


<table class="center">
<tr>
  <td><img src="gif_results/ertA Hulk on the sea .gif"></td>
  <td><img src="gif_results/lokA Superman on the forest.gif"></td>
  <td><img src="gif_results/A Iron man on the snow.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"A Hulk, on the sea"</td>
  <td width=25% style="text-align:center;">"A superman, in the forest"</td>
  <td width=25% style="text-align:center;">"A Iron man, in the snow"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/A man in the forest, Minecraft.gif"></td>
  <td><img src="gif_results/a man in the sea, at sunset.gif"></td>
  <td><img src="gif_results/James Bond, grey simple background.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"A man in the forest, Minecraft."</td>
  <td width=25% style="text-align:center;">"A man in the sea, at sunset"</td>
  <td width=25% style="text-align:center;">"James Bond, grey simple background"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/vryvA Panda on the sea.gif"></td>
  <td><img src="gif_results/nbthA Stormtrooper on the sea.gif"></td>
  <td><img src="gif_results/egbA astronaut on the moon.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"A Panda on the sea."</td>
  <td width=25% style="text-align:center;">"A Stormtrooper on the sea"</td>
  <td width=25% style="text-align:center;">"A astronaut on the moon"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/sssA astronaut on the moon.gif"></td>
  <td><img src="gif_results/ccA Robot in Antarctica.gif"></td>
  <td><img src="gif_results/zzzzA Iron man on the beach..gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"A astronaut on the moon."</td>
  <td width=25% style="text-align:center;">"A Robot in Antarctica."</td>
  <td width=25% style="text-align:center;">"A Iron man on the beach."</td>
</tr>
</table>

<!--#########################################################-->
<table class="center">
<tr>
  <td><img src="gif_results/yrvA Obama in the desert.gif"></td>
  <td><img src="gif_results/dfcA Astronaut on the beach.gif"></td>
  <td><img src="gif_results/sasqA Iron man on the snow.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"The Obama in the desert"</td>
  <td width=25% style="text-align:center;">"Astronaut on the beach."</td>
  <td width=25% style="text-align:center;">"Iron man on the snow"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/aaaA Stormtrooper on the sea.gif"></td>
  <td><img src="gif_results/A Iron man on the beach..gif"></td>
  <td><img src="gif_results/A astronaut on the moon.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"A Stormtrooper on the sea"</td>
  <td width=25% style="text-align:center;">"A Iron man on the beach."</td>
  <td width=25% style="text-align:center;">"A astronaut on the moon."</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/cdAstronaut on the beach.gif"></td>
  <td><img src="gif_results/cswSuperman on the forest.gif"></td>
  <td><img src="gif_results/cwIron man on the beach..gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"Astronaut on the beach"</td>
  <td width=25% style="text-align:center;">"Superman on the forest"</td>
  <td width=25% style="text-align:center;">"Iron man on the beach"</td>
</tr>
</table>
<!--#########################################################-->

<table class="center">
<tr>
  <td><img src="gif_results/dfewcAstronaut on the beach.gif"></td>
  <td><img src="gif_results/ewA Robot in Antarctica.gif"></td>
  <td><img src="gif_results/vervA Stormtrooper on the sea.gif"></td>

</tr>
<tr>

</tr>
<tr>
  <td width=25% style="text-align:center;">"Astronaut on the beach"</td>
  <td width=25% style="text-align:center;">"Robot in Antarctica"</td>
  <td width=25% style="text-align:center;">"The Stormtroopers, on the beach"</td>
</tr>
</table>
<!--#########################################################-->




## 🎼🎼🎼 Citation 
If you think this project is helpful, please feel free to leave a star⭐️⭐️⭐️ and cite our paper:
```bibtex
@article{ma2023follow,
  title={Follow Your Pose: Pose-Guided Text-to-Video Generation using Pose-Free Videos},
  author={Ma, Yue and He, Yingqing and Cun, Xiaodong and Wang, Xintao and Shan, Ying and Li, Xiu and Chen, Qifeng},
  journal={arXiv preprint arXiv:2304.01186},
  year={2023}
}
``` 


## 👯👯👯 Acknowledgements

This repository borrows heavily from [Tune-A-Video](https://github.com/showlab/Tune-A-Video) and [FateZero](https://github.com/ChenyangQiQi/FateZero). thanks the authors for sharing their code and models.

## 🕺🕺🕺 Maintenance

This is the codebase for our research work. We are still working hard to update this repo and more details are coming in days. If you have any questions or ideas to discuss, feel free to contact [Yue Ma](mailto:y-ma21@mails.tsinghua.edu.cn) or [Yingqing He](https://github.com/YingqingHe) or [Xiaodong Cun](mailto:vinthony@gmail.com).

