<!-- markdownlint-disable MD033 -->

# Hello Langflow

<https://github.com/langflow-ai/langflow>

## 1 run by docker compose

<https://docs.langflow.org/Deployment/deployment-docker>

```yml
services:
  langflow:
    # https://hub.docker.com/r/langflowai/langflow 
    image: langflowai/langflow:v1.1.1 
    ports:
      - "7860:7860"
    depends_on:
      - postgres
    environment:
      - LANGFLOW_DATABASE_URL=postgresql://langflow:langflow@postgres:5432/langflow
      - OLLAMA_URL=http://localhost:11434
    volumes:
      - langflow-data:/app/langflow

  postgres:
    image: postgres:16
    environment:
      POSTGRES_USER: langflow
      POSTGRES_PASSWORD: langflow
      POSTGRES_DB: langflow
    ports:
      - "5432:5432"
    volumes:
      - langflow-postgres:/var/lib/postgresql/data

volumes:
  langflow-postgres:
  langflow-data:
```

```sh
git clone https://github.com/langflow-ai/langflow.git
cd langflow/docker_example
docker compose up
```

## 2 play

<http://localhost:7860/>

### ollama

```sh
$ ollama serve --host 0.0.0.0
$ export OLLAMA_HOST=0.0.0.0


ip_address=$(ipconfig | findstr IPv4 | awk '{print $16}')
echo "http://${ip_address}:11434"
```

<http://192.168.31.67:11434>

<img alt="config" src="Screenshot 2025-01-05 211443.png" style="width:800px" />

<img alt="test" src="Screenshot 2025-01-05 211414.png" style="width:800px" />

----

## [option] python install

### install

#### venv

```sh
brew list | grep python
brew info python@3.10
$ /usr/local/opt/python@3.10/libexec/bin/python3 -V
Python 3.10.15
```

```sh
/usr/local/opt/python@3.10/libexec/bin/python3 -m venv lf_venv
source lf_venv/bin/activate
python -V
pip install --upgrade pip
```

#### conda

```sh
conda create --name lf_venv python=3.10 -y
conda activate lf_venv
python -V
python -m pip install --upgrade pip
```

#### install it

```sh
conda activate lf_venv
# https://raw.githubusercontent.com/langflow-ai/langflow/refs/heads/main/pyproject.toml
# python -m pip install langflow -U
# 依赖太乱 没成功 20250105
pip install --upgrade setuptools wheel
pip install -r requirements.txt
```

### run

```sh
conda activate lf_venv
python -m langflow run
```

### clean

```sh
conda deactivate
conda env remove -n lf_venv -y
conda env list
```
