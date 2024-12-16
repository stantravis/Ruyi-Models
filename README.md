# Ruyi-Models

English | [简体中文](./README_CN.md)

Welcome to Ruyi-Models!

Ruyi is an image-to-video model capable of generating cinematic-quality videos at a **resolution of 768**, with a frame rate of **24 frames per second**, totaling **5 seconds and 120 frames**. It supports **lens control** and **motion amplitude control**. Using a **RTX 3090 or RTX 4090**, you can generate 512 resolution, 120 frames (or 768 resolution, ~72 frames) videos **without any loss of quality**.

## Table of Contents

- [Installation Instructions](#installation-instructions)
- [Download Model (Optional)](#download-model-optional)
- [How to Use](#how-to-use)
- [Showcase](#showcase)
- [GPU Memory Optimization](#gpu-memory-optimization)
- [License](#license)

## Installation Instructions

The installation instructions are simple. Just clone the repo and install the requirements.

```shell
git clone https://github.com/IamCreateAI/Ruyi-Models
cd Ruyi-Models
pip install -r requirements.txt
```

### For ComfyUI Users

#### Method (1): Installation via ComfyUI Manager

TBD, not supported yet.

#### Method (2): Manual Installation

Download and save this repository to the path *ComfyUI/custom_nodes/Ruyi-Models*.

```shell
# download the repo
cd ComfyUI/custom_nodes/
git clone https://github.com/IamCreateAI/Ruyi-Models.git

# install requirements
pip install -r Ruyi-Models/requirements.txt
```

Install the dependency ComfyUI-VideoHelperSuite to display video output (skip this step if already installed).

```shell
# download ComfyUI-VideoHelperSuite
cd ComfyUI/custom_nodes/
git clone https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite.git

# install requirements
pip install -r ComfyUI-VideoHelperSuite/requirements.txt
```

##### For Windows Users

When using the Windows operating system, a common distribution is [ComfyUI_windows_portable_nvidia](https://github.com/comfyanonymous/ComfyUI/releases). When launched with `run_nvidia_gpu.bat`, it utilizes the embedded Python interpreter included with the package. Therefore, the environment needs to be set up within this built-in Python.

For example, if the extracted directory of the distribution is ComfyUI_windows_portable, you can typically use the following command to download the repository and install the runtime environment:

```shell
# download the repo
cd ComfyUI_windows_portable\ComfyUI\custom_nodes
git clone https://github.com/IamCreateAI/Ruyi-Models.git

# install requirements using embedded Python interpreter
..\..\python_embeded\python.exe -m pip install -r Ruyi-Models\requirements.txt
```

## Download Model (Optional)

Download the model and save it to certain path. To directly run our model, it is recommand to save the models into _Ruyi-Models/models_ folder. For ComfyUI users, the path should be _ComfyUI/models/Ruyi_.

| Model Name | Type | Resolution | Max Frames | Frames per Second | Storage Space | Download |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Ruyi-Mini-7B | Image to Video | 512 & 768 | 120 | 24 | 17 GB | [🤗](https://huggingface.co/IamCreateAI/Ruyi-Mini-7B) |

For example, after downloading Ruyi-Mini-7B, the file path structure should be:

```
📦 Ruyi-Models/models/ or ComfyUI/models/Ruyi/
├── 📂 Ruyi-Mini-7B/
│   ├── 📂 transformers/
│   ├── 📂 vae/
│   └── 📂 ...
```

> This repository **supports automatic model downloading**, but manual downloading provides more control. For instance, you can download the model to another location and then link it to the *ComfyUI/models/Ruyi* path using symbolic links or similar methods.

## How to Use

We provide two ways to run our model. The first is directly using python code.

```
python3 predict_i2v.py
```

Specifically, the script downloads the model to the _Ruyi-Models/models_ folder and uses images from the [_assets_](./assets/) folder as the start and end frames for video inference. You can modify the variables in the script to replace the input images and set parameters such as video length and resolution.

For users with more than 24GB of GPU memory, you can use predict_i2v_80g.py to enhance generation speed. For those with less GPU memory, we offer parameters to optimize memory usage, enabling the generation of higher resolution and longer videos by extending the inference time. The effects of these parameters can be found in the [GPU memory optimization section](#gpu-memory-optimization) section below.

Or use ComfyUI wrapper in our github repo, the detail of ComfyUI nodes is described in [_comfyui/README.md_](./comfyui/README.md).

## Showcase

### Image to Video Effects

<table>
    <tr>
        <td><video src="https://github.com/user-attachments/assets/2779d7fb-24b7-4b98-b297-404a9c369a25"></video></td>
        <td><video src="https://github.com/user-attachments/assets/bb193d9f-f6e9-4504-bf1a-5ba7c63adb3f"></video></td>
        <td><video src="https://github.com/user-attachments/assets/6f1e1aef-dd62-493e-8943-2ed45ac79c9c"></video></td>
        <td><video src="https://github.com/user-attachments/assets/199c8b47-b0bc-4ff7-bd12-6c193f424335"></video></td>
    </tr>
</table>

### Camera Control

<table>
    <tr>
        <td align=center><img src="assets/example_02.jpg" height=200></img>input</td>
        <td align=center><video src="https://github.com/user-attachments/assets/efcbacb0-3270-4043-b732-2a3b7d94650c"></video>left</td>
        <td align=center><video src="https://github.com/user-attachments/assets/4f68fe2f-af90-496c-a975-eb974004f369"></video>right</td>
    </tr>
    <tr>
        <td align=center><video src="https://github.com/user-attachments/assets/1058c5f3-3154-4415-a7ea-dc38c6862e94"></video>static</td>
        <td align=center><video src="https://github.com/user-attachments/assets/33898b54-de6e-4c64-bf4f-74098cac6325"></video>up</td>
        <td align=center><video src="https://github.com/user-attachments/assets/bada1fe5-39a4-44d2-b916-eeebf4b70dfd"></video>down</td>
    </tr>
</table>

### Motion Amplitude Control

<table>
    <tr>
        <td align=center><video src="https://github.com/user-attachments/assets/5010efb3-ba39-4589-bae1-28a27a35852e"></video>motion 1</td>
        <td align=center><video src="https://github.com/user-attachments/assets/52ee1e20-e5d4-40a1-9afd-2dfc3350a0cd"></video>motion 2</td>
        <td align=center><video src="https://github.com/user-attachments/assets/a818c5f5-a017-4221-91f6-bff44423d8b9"></video>motion 3</td>
        <td align=center><video src="https://github.com/user-attachments/assets/9863326d-b691-4493-86bb-82d8880e38e6"></video>motion 4</td>
    </tr>
</table>

## GPU Memory Optimization

We provide the options **`GPU_memory_mode` and `GPU_offload_steps` to reduce GPU memory usage**, catering to different user needs.

Generally speaking, using **less GPU memory requires more RAM and results in longer generation times**. Below is a reference table of expected GPU memory usage and generation times. Note that, the GPU memory reported below is the `max_memory_allocated()` value. The values read from nvidia-smi may be higher than the reported values because CUDA occupies some GPU memory (usually between 500 - 800 MiB), and PyTorch's caching mechanism also requests additional GPU memory.

### A100 Results

- Resolution of 512

| Num frames | normal_mode + 0 steps | normal_mode + 10 steps | normal_mode + 7 steps | normal_mode + 5 steps | normal_mode + 1 steps | low_gpu_mode + 0 steps |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 24 frames  | 16119MiB <br> _01:01s_ | 15535MiB <br> _01:07s_ | 15340MiB <br> _01:13s_ | 15210MiB <br> _01:20s_ | 14950MiB <br> _01:32s_ |  4216MiB <br> _05:14s_ |
| 48 frames  | 18398MiB <br> _01:53s_ | 17230MiB <br> _02:15s_ | 16840MiB <br> _02:29s_ | 16580MiB <br> _02:32s_ | 16060MiB <br> _02:54s_ |  4590MiB <br> _09:59s_ |
| 72 frames  | 20678MiB <br> _03:00s_ | 18925MiB <br> _03:31s_ | 18340MiB <br> _03:53s_ | 17951MiB <br> _03:57s_ | 17171MiB <br> _04:25s_ |  6870MiB <br> _14:42s_ |
| 96 frames  | 22958MiB <br> _04:11s_ | 20620MiB <br> _04:54s_ | 19841MiB <br> _05:10s_ | 19321MiB <br> _05:14s_ | 18281MiB <br> _05:47s_ |  9150MiB <br> _19:17s_ |
| 120 frames | 25238MiB <br> _05:42s_ | 22315MiB <br> _06:34s_ | 21341MiB <br> _06:59s_ | 20691MiB <br> _07:07s_ | 19392MiB <br> _07:41s_ | 11430MiB <br> _24:08s_ |

- Resolution of 768

| Num frames | normal_mode + 0 steps | normal_mode + 10 steps | normal_mode + 7 steps | normal_mode + 5 steps | normal_mode + 1 steps | low_gpu_mode + 0 steps |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 24 frames  | 18971MiB <br> _02:06s_ | 17655MiB <br> _02:40s_ | 17217MiB <br> _02:39s_ | 16925MiB <br> _02:41s_ | 16339MiB <br> _03:13s_ |  5162MiB <br> _13:42s_ |
| 48 frames  | 24101MiB <br> _04:52s_ | 21469MiB <br> _05:44s_ | 20592MiB <br> _05:51s_ | 20008MiB <br> _06:00s_ | 18837MiB <br> _06:49s_ | 10292MiB <br> _20:58s_ |
| 72 frames  | 29230MiB <br> _08:24s_ | 25283MiB <br> _09:45s_ | 25283MiB <br> _09:45s_ | 23091MiB <br> _10:10s_ | 21335MiB <br> _11:10s_ | 15421MiB <br> _39:12s_ |
| 96 frames  | 34360MiB <br> _12:49s_ | 29097MiB <br> _14:41s_ | 27343MiB <br> _15:33s_ | 26174MiB <br> _15:44s_ | 23834MiB <br> _16:33s_ | 20550MiB <br> _43:47s_ |
| 120 frames | 39489MiB <br> _18:21s_ | 32911MiB <br> _20:39s_ | 30719MiB <br> _21:34s_ | 29257MiB <br> _21:48s_ | 26332MiB <br> _23:02s_ | 25679MiB <br> _63:01s_ |

### RTX 4090 Results

The values marked with `---` in the table indicate that an out-of-memory (OOM) error occurred, preventing generation.

- Resolution of 512

| Num frames | normal_mode + 0 steps | normal_mode + 10 steps | normal_mode + 7 steps | normal_mode + 5 steps | normal_mode + 1 steps | low_gpu_mode + 0 steps |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 24 frames  | 16366MiB <br> _01:18s_ | 15805MiB <br> _01:26s_ | 15607MiB <br> _01:37s_ | 15475MiB <br> _01:36s_ | 15211MiB <br> _01:39s_ |  4211MiB <br> _03:57s_ |
| 48 frames  | 18720MiB <br> _02:21s_ | 17532MiB <br> _02:49s_ | 17136MiB <br> _02:55s_ | 16872MiB <br> _02:58s_ | 16344MiB <br> _03:01s_ |  4666MiB <br> _05:01s_ |
| 72 frames  | 21036MiB <br> _03:41s_ | 19254MiB <br> _04:25s_ | 18660MiB <br> _04:34s_ | 18264MiB <br> _04:36s_ | 17472MiB <br> _04:51s_ |  6981MiB <br> _06:36s_ |
| 96 frames  | -----MiB <br> _--:--s_ | 20972MiB <br> _06:18s_ | 20180MiB <br> _06:24s_ | 19652MiB <br> _06:36s_ | 18596MiB <br> _06:56s_ |  9298MiB <br> _10:03s_ |
| 120 frames | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | 21704MiB <br> _08:50s_ | 21044MiB <br> _08:53s_ | 19724MiB <br> _09:08s_ | 11613MiB <br> _13:57s_ |

- Resolution of 768

| Num frames | normal_mode + 0 steps | normal_mode + 10 steps | normal_mode + 7 steps | normal_mode + 5 steps | normal_mode + 1 steps | low_gpu_mode + 0 steps |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 24 frames  | 19223MiB <br> _02:38s_ | 17900MiB <br> _03:06s_ | 17448MiB <br> _03:18s_ | 17153MiB <br> _03:23s_ | 16624MiB <br> _03:34s_ |  5251MiB <br> _05:54s_ |
| 48 frames  | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | 20946MiB <br> _07:28s_ | 20352MiB <br> _07:35s_ | 19164MiB <br> _08:04s_ | 10457MiB <br> _10:55s_ |
| 72 frames  | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | -----MiB <br> _--:--s_ | 15671MiB <br> _18:52s_ |

## License

We’re releasing the model under a permissive **Apache 2.0 license**.

## BibTeX

```
@misc{createai2024ruyi,
      title={Ruyi-Mini-7B},
      author={CreateAI Team},
      year={2024},
      publisher = {GitHub},
      journal = {GitHub repository},
      howpublished={\url{https://github.com/IamCreateAI/Ruyi-Models}}
}
```

## Welcome Feedback and Collaborative Optimization

We sincerely welcome everyone to actively provide valuable feedback and suggestions, and we hope to work together to optimize our services and products. Your words will help us better understand user needs, allowing us to continuously enhance the user experience. Thank you for your support and attention to our work!

You are welcomed to join our [Discord](https://discord.com/invite/nueQFQwwGw) or Wechat Group (Scan QR code) for further discussion!

![wechat](assets/wechat_group.png)
