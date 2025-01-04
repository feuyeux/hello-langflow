# Hello Langflow

<https://github.com/langflow-ai/langflow>

## install

```sh
brew list | grep python                                                                     2 ↵
brew info python@3.10
$ /usr/local/opt/python@3.10/libexec/bin/python3 -V
Python 3.10.15
```

```sh
/usr/local/opt/python@3.10/libexec/bin/python3 -m venv lf_venv
source lf_venv/bin/activate
pip install --upgrade pip
python -V
pip install langflow
```

## run

```sh
python -m langflow run
```
