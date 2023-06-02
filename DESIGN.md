# Env

## for development of loadtime

### Create virtual env and install related packages
```
conda update -n base -c defaults conda --yes
conda create --yes -n env-loadtime
conda activate env-loadtime
conda install python=3.10.10 --yes
python -m pip install --upgrade pip
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
pip install accelerate transformers
pip install fastapi
pip install fastsession
pip install tokflow
pip install "uvicorn[standard]" gunicorn
pip install loadtime
pip install pytest

```

### Remove virtual env

```
conda deactivate
conda remove -n env-loadtime --all --yes
```

## Release


### Release tools

```
pip install setuptools wheel
python -m pip install --user --upgrade twine
```


### Remove existing dist 

```
rmdir /s /q dist
```

### Build for release

```
python setup.py sdist bdist_wheel
```

### Upload

```
python -m twine upload dist/*
```
