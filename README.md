# biobeaker_testing
Testing biobeaker models!


# Installation

I've tried to recreate this environment in biobeaker.yml - try `mamba env create -f biobeaker.yml`, but that one still needs the below biobeaker/oracular/sfasta/acc2tax installations

From scratch installation:

```
mamba create -n biobeaker "python<3.9" tensorflow-gpu==2.11.0 -y
conda activate biobeaker
mamba install cudatoolkit -y # to get libcuda.11 for GPU/tensorflow

# at the time of this writing, biobeaker on pip has weird dependencies. Let's edit them in the pypi-distributed package until that's fixed:
wget https://files.pythonhosted.org/packages/eb/e0/088796c8e9c7316596d2ee9aaaaea87f03b4273b51467fff4479d54bf267/biobeaker-0.0.2.tar.gz
tar xvf biobeaker-0.0.2.tar.gz
cd biobeaker-0.0.2
# replace the bottom with this text:
# # Requirements
#[tool.poetry.dependencies]
#python = ">=3.7,<3.11"
#tensorflow = ">=2.4.1"
#tensorflow-addons = ">=0.12.1"
#numpy = ">=1.19.5"
#baseconvert = ">=1.0.0.a4"

cd ..
pip install ./biobeaker-0.0.2

pip install jupyterlab 'maturin[patchelf]' plotly pandas umap-learn fastaparser pyarrow matplotlib


biobeaker relies on a bunch of Rust-libraries called from within Python:

git clone https://github.com/jguhlin/oracular
git clone https://github.com/jguhlin/sfasta
git clone https://github.com/jguhlin/acc2tax

cd acc2tax
maturin develop -r

cd ../sfasta
cargo install --path sfa

cd ../oracular/pyracular
maturin develop -r

cd ../..
jupyter-lab

```
