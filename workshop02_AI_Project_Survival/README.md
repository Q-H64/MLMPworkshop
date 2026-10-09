Project

Repository: https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix.git

Inference task: Image-to-image translation
(CycleGAN: Horse to Zebra; Pix2Pix: Facade Labels to Photos)

Repo map

Environment: environment.yml

Entry point: test.py

Model: Pretrained checkpoints are downloaded with scripts/download_cyclegan_model.sh and scripts/download_pix2pix_model.sh

Input: datasets/horse2zebra/testA or datasets/facades/

Output: results/

Environment setup

git clone git@github.com:junyanz/pytorch-CycleGAN-and-pix2pix.git

cd pytorch-CycleGAN-and-pix2pix

uv venv --python 3.11

source .venv/bin/activate

uv pip install --index-url https://download.pytorch.org/whl/cu121 \
  "torch==2.4.0" "torchvision==0.19.0"
  
uv pip install \
  "numpy==1.24.3" \
  "scikit-image" \
  "dominate>=2.8.0" \
  "Pillow>=10.0.0" \
  "wandb>=0.16.0"

Inference

(CycleGAN: Horse to Zebra)

bash ./scripts/download_cyclegan_model.sh horse2zebra

bash ./datasets/download_cyclegan_dataset.sh horse2zebra

python test.py --dataroot ./datasets/horse2zebra/testA --name horse2zebra_pretrained --model test --no_dropout

(Pix2Pix: Facade Labels to Photos)

bash ./scripts/download_pix2pix_model.sh facades_label2photo

bash ./datasets/download_pix2pix_dataset.sh facades

python test.py --dataroot ./datasets/facades/ --direction BtoA --model pix2pix --name facades_label2photo_pretrained

One real failure

Category: Missing dependencies

Root cause: After converting the Conda environment setup to UV, some required dependencies were missing, preventing the models from running.

Minimal fix: Installed the remaining required packages using UV, then successfully ran both CycleGAN and Pix2Pix.
 

AI agent check

Which AI coding agent did you use?: copilot

What did it change?: guided the environment setup

How did you verify the change?: I checked the repository README and environment file to confirm the exact dependency versions and command structure.
