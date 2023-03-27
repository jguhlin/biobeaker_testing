# biobeaker_testing
Testing biobeaker models!


# Installation

```
mamba create -n biobeaker "python<3.9" -y
conda activate biobeaker
mamba install cudatoolkit -y # to get libcuda.11 for GPU/tensorflow

pip install biobeaker jupyterlab 'maturin[patchelf]' plotly pandas umap-learn fastaparser

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
