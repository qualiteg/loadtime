# How to release loadtime 

## for development of loadtime only

### Create virtual env and activate it

- Linux 

```
cd loadtime
python -m venv venv
./venv/bin\activate
```


- Windows

```
cd loadtime
python -m venv venv
.\venv\Scripts\activate
```

### upgrade pip

```
python -m pip install --upgrade pip
```

### install packages for release

```
pip install setuptools wheel
python -m pip install --upgrade twine
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

### Enter credentials

