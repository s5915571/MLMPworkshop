# Assignment 1 — AI Project Survival

## Project

**Project name:** CycleGAN

**Repository URL:** https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix

**Exact commit:** `2a7afba2895d52556dd5dfe07e8555ef657ced6f`

**Inference task:** Horse-to-zebra image translation using a pretrained CycleGAN generator.

I reproduced inference using the official CycleGAN repository and its pretrained `horse2zebra` model. I tested five horse images and generated corresponding zebra-style images.

## Repo map

**Environment:** Red Hat Enterprise Linux 9.8, Python 3.11.17, PyTorch 2.4.0+cu121, Torchvision 0.19.0+cu121, NumPy 1.24.3, NVIDIA GeForce RTX 4080 GPU.

**Entry point:** `test.py`

**Model:** `checkpoints/horse2zebra_pretrained/latest_net_G.pth`

**Input:** `datasets/horse2zebra/testA/`

**Output:** `results/horse2zebra_pretrained/test_latest/images/`

## Environment setup

The following commands reproduce the environment using `uv`.

```bash
mkdir -p ~/workshop02_projects
cd ~/workshop02_projects

git clone https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix.git
cd pytorch-CycleGAN-and-pix2pix

git checkout 2a7afba2895d52556dd5dfe07e8555ef657ced6f

uv python install 3.11
uv venv --python 3.11 .venv

uv pip install --python .venv/bin/python torch==2.4.0 torchvision==0.19.0 --index-url https://download.pytorch.org/whl/cu121

uv pip install --python .venv/bin/python "numpy==1.24.3" scikit-image "dominate>=2.8.0" "Pillow>=10.0.0" "wandb>=0.16.0"
```

Verify PyTorch and GPU availability:

```bash
.venv/bin/python -c "import torch; print(torch.__version__); print(torch.cuda.is_available()); print(torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'GPU unavailable')"
```

On my computer, CUDA availability was `True`, and the detected GPU was NVIDIA GeForce RTX 4080.

## Inference

Download the pretrained model:

```bash
bash ./scripts/download_cyclegan_model.sh horse2zebra
```

Download the dataset:

```bash
bash ./datasets/download_cyclegan_dataset.sh horse2zebra
```

Run inference on five test images:

```bash
.venv/bin/python test.py --dataroot datasets/horse2zebra/testA --name horse2zebra_pretrained --model test --no_dropout --num_test 5
```

Open the generated HTML report:

`results/horse2zebra_pretrained/test_latest/index.html`

Example evidence:

- **Input:** `evidence/input.png`
- **Output:** `evidence/output.png`

The images correspond to `n02381460_1000_real.png` and `n02381460_1000_fake.png` from my inference results.

## Troubleshooting — One real failure

**Category:** To be completed using an actual issue encountered during setup or reproduction.

**Root cause:** Not yet established.

**Minimal fix:** Not yet established.

No genuine inference failure has been documented so far. The model and dataset download scripts displayed a harmless `wget` timestamping warning, but both downloads completed successfully. This warning should not be misrepresented as a failure.

## AI agent check

**Which AI coding agent did you use?** ChatGPT (OpenAI).

**What advice did it give?** It guided me through setting up Python 3.11 using `uv`, installing compatible CUDA-enabled PyTorch packages, downloading the pretrained model and dataset, running inference, and locating the generated results.

**What command or fix did you apply yourself?** I executed the installation, verification, download, and inference commands in my Linux terminal.

**How did you verify the result yourself?** I confirmed that PyTorch reported CUDA availability as `True`, verified that CycleGAN initialized on `cuda:0`, checked the generated image files, and opened the HTML report to inspect the horse-to-zebra results.

## Peer reproduction

Peer feedback and reproduction results are recorded in `Peer_Reproduction.md`.

**Changes made after peer review:** Pending peer review.

