# Aloha

Experiments & demos with **LeRobot Aloha** robot arm  

## 🖥️ System Information
- **Operating System**: Ubuntu 20.04 (via Windows WSL)
- **GPU**: NVIDIA GeForce RTX 4060, Driver Version 576.52, CUDA 12.9 【Train in RTX4090D 24G or AutoDL platform】
- **Hardware**: Logitech C920 Webcam, Xuanya hardware robotic arm based on Aloha

## 📦 Features
- Simulation & real-world control
- Imitation learning & reinforcement learning
- Dataset collection & analysis

## 🎥 camera 
- 介绍你使用的摄像头型号、分辨率、安装方式
- 示例：
  ```bash
  # 查看可用摄像头
  ls /dev/video*
  # 启动摄像头采集脚本
  python scripts/camera_setup.py



## 🛠 Installation
```bash
git clone https://github.com/yourusername/aloha-project.git
cd aloha-project
# install dependencies etc.



 
 

````markdown
## 🧪 AutoDL Training Setup

This section documents the training environment setup and execution on the **AutoDL platform**, including conda environment setup, code installation, Hugging Face integration, and training script usage.

---

### 🔧 Environment Setup

1. **Initialize Conda**
```bash
conda env list
conda activate base
conda init
````

> Restart the terminal after initializing conda.

2. **Create and activate environment**

```bash
conda create -y -n lerobot python=3.10
conda activate lerobot
```

3. **Enable Network Turbo (AutoDL Specific)**

```bash
source /etc/network_turbo
# Output: Successfully enabled. Note: Academic use only, no stability guaranteed.
```

---

### 📦 Project Setup

4. **Clone project repositories**

```bash
git clone https://github.com/Xuanya-Robotics/lerobot.git
cd lerobot
git clone https://github.com/Xuanya-Robotics/Alicia_duo_sdk.git Alicia_duo_sdk
```

5. **Install dependencies**

```bash
conda install ffmpeg -c conda-forge
pip install -e .
```

---

### 🔐 Hugging Face Configuration

1. **Set Git Credential Helper**

```bash
git config --global credential.helper store
```

2. **Login using token**

```bash
hf auth login --token <your_token>
# Example:
# hf auth login --token hf_..................... 
```

> After login, the token will be saved locally. You may add `--add-to-git-credential` if needed.

3. **Set Hugging Face username environment variable**

```bash
HF_USER=$(hf auth whoami | head -n 1) && echo $HF_USER
# Example output: Enstar07
```

---

### 🏋️ Training Examples

#### 📡 Training from Hugging Face cloud dataset

```bash
python lerobot/scripts/train.py \
  --dataset.repo_id Enstar07/demo_dataset3 \
  --policy.type act \
  --output_dir outputs/train/act_alicia_duo_model_final \
  --job_name alicia_duo_act_training_final \
  --policy.device cuda \
  --batch_size 32 \
  --steps 2000 \
  --save_freq 500 \
  --eval_freq 500 \
  --log_freq 100
```

> ⚠️ Cloud-based dataset training may suffer from network delays.
> For large datasets, consider using FileZilla to upload local data directly to AutoDL.

---

#### 💾 Training from Local Dataset (uploaded via FileZilla)

```bash
python lerobot/scripts/train.py \
  --dataset.repo_id /root/lerobot/data/zhuiPick3 \
  --policy.type act \
  --output_dir outputs/train/act_alicia_duo_model_final \
  --job_name alicia_duo_act_training_final \
  --policy.device cuda \
  --batch_size 32 \
  --steps 2000 \
  --save_freq 500 \
  --eval_freq 500 \
  --log_freq 100
```

---

#### 🚀 Full-scale Training (successful)

```bash
python lerobot/scripts/train.py \
  --dataset.repo_id /root/lerobot/data/zhuiPick3 \
  --policy.type act \
  --output_dir outputs/train/act_alicia_duo_model_final \
  --job_name alicia_duo_act_training_final \
  --policy.device cuda \
  --batch_size 64 \
  --steps 20000 \
  --save_freq 1000 \
  --eval_freq 1000 \
  --log_freq 500
```

---

### 📤 Model Export & Deployment

* After training completes, use **FileZilla** to download the trained model directory to your local system.
* Update the deployment script path:

```python
# In dp_inference.py
ckpt_path = "/home/zexuan/Robot/xuanArm/system2/lerobot/outputs/train/filezilla/020000/pretrained_model"
```

* Then run deployment:

```bash
cd examples/
python dp_inference.py
```

---

```

---

 ## 🧪 AutoDL Training Notes
```


