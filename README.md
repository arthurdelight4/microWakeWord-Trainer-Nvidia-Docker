<div align="center">
  <img src="https://raw.githubusercontent.com/TaterTotterson/microWakeWord-Trainer-Nvidia-Docker/refs/heads/main/mmw.png" alt="MicroWakeWord Trainer Logo" width="100" />
  <h1>microWakeWord Trainer Docker</h1>
</div>

# 🥔 MicroWakeWord Trainer – Tater Approved  

**✅ Tater Totterson tested & working on an NVIDIA RTX 3070 Laptop GPU (8 GB VRAM).**  
Easily train microWakeWord detection models with this pre-built Docker image and JupyterLab notebook.  

---

## 🚀 Quick Start  

Follow these steps to get up and running:  

### 1️⃣ Pull the Pre-Built Docker Image  

```bash
docker pull ghcr.io/tatertotterson/microwakeword:latest
```

---

### 2️⃣ Run the Docker Container  

```bash
sudo docker run -it \
    --device=/dev/kfd \
    --device=/dev/dri \
    --security-opt seccomp=unconfined \
    --group-add video \
    -p 8888:8888 \
    -v $(pwd):/data \
    ghcr.io/tatertotterson/microwakeword:latest

```

**What these flags do:**  
- `--device=/dev/kfd` → Allow access to the Kernel Fusion Driver
- `--device=/dev/dri` → Allow access to your GPU
- `--security-opt seccomp=unconfined` → Give the container access to system calls for memory mapping
- `--group-add video` → Allow access to the GPU hardware in the container
- `-p 8888:8888` → Exposes JupyterLab on port 8888  
- `-v $(pwd):/data` → Saves your work in the current folder  

---

### 3️⃣ Open JupyterLab  

Visit [http://localhost:8888](http://localhost:8888) in your browser — the notebook UI will open.  

---

### 4️⃣ Set Your Wake Word  

At the **top of the notebook**, find this line:  

```bash
TARGET_WORD = "hey_tater"  # Change this to your desired wake word
```

Change `"hey_tater"` to your desired wake word (phonetic spellings often work best).  

---

### 5️⃣ Run the Notebook  

Run all cells in the notebook. This process will:  
- Generate wake word samples  
- Train a detection model  
- Output a quantized `.tflite` model ready for on-device use  

---

### 6️⃣ Retrieve the Trained Model & JSON  

When training finishes, download links for both the `.tflite` model and its `.json` manifest will be displayed in the last cell.  

---

## 🔄 Resetting to a Clean State  

If you need to start fresh:  

1. Delete the `data` folder that was mapped to your Docker container.  
2. Restart the container using the steps above.  
3. A fresh copy of the notebook will be placed into the `data` directory.  

---

## 🙌 Credits  

This project builds upon the excellent work of [kahrendt/microWakeWord](https://github.com/kahrendt/microWakeWord).  
Huge thanks to the original authors for their contributions to the open-source community!
