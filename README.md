# finetuning
some frameworks and onsiderations 

### Conda Installation (Optional)
`⚠️Only use Conda if you have it. If not, use Pip`. Select either `pytorch-cuda=11.8,12.1` for CUDA 11.8 or CUDA 12.1. We support `python=3.10,3.11,3.12`.
```bash
conda create --name unsloth_env \
    python=3.11 \
    pytorch-cuda=12.1 \
    pytorch cudatoolkit xformers -c pytorch -c nvidia -c xformers \
    -y
conda activate unsloth_env

pip install unsloth
```

<details>
  <summary>If you're looking to install Conda in a Linux environment, <a href="https://docs.anaconda.com/miniconda/">read here</a>, or run the below 🔽</summary>
  
  ```bash
  mkdir -p ~/miniconda3
  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
  bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
  rm -rf ~/miniconda3/miniconda.sh
  ~/miniconda3/bin/conda init bash
  ~/miniconda3/bin/conda init zsh
  ```
</details>

#### Llama 3.1 (8B) max. context length
We tested Llama 3.1 (8B) Instruct and did 4bit QLoRA on all linear layers (Q, K, V, O, gate, up and down) with rank = 32 with a batch size of 1. We padded all sequences to a certain maximum sequence length to mimic long context finetuning workloads.
| GPU VRAM | 🦥Unsloth context length | Hugging Face + FA2 |
|----------|-----------------------|-----------------|
| 8 GB     | 2,972                 | OOM             |
| 12 GB    | 21,848                | 932             |
| 16 GB    | 40,724                | 2,551           |
| 24 GB    | 78,475                | 5,789           |
| 40 GB    | 153,977               | 12,264          |
| 48 GB    | 191,728               | 15,502          |
| 80 GB    | 342,733               | 28,454          |

#### Llama 3.3 (70B) max. context length
We tested Llama 3.3 (70B) Instruct on a 80GB A100 and did 4bit QLoRA on all linear layers (Q, K, V, O, gate, up and down) with rank = 32 with a batch size of 1. We padded all sequences to a certain maximum sequence length to mimic long context finetuning workloads.

| GPU VRAM | 🦥Unsloth context length | Hugging Face + FA2 |
|----------|------------------------|------------------|
| 48 GB    | 12,106                | OOM              |
| 80 GB    | 89,389                | 6,916            |

<br>

![](https://i.ibb.co/sJ7RhGG/image-41.png)
<br>

### Citation

You can cite the Unsloth repo as follows:
```bibtex
@software{unsloth,
  author = {Daniel Han, Michael Han and Unsloth team},
  title = {Unsloth},
  url = {http://github.com/unslothai/unsloth},
  year = {2023}
}
```
