# workshop_docker_fixando

### Objetivo
```bash
salvar os principais comandos para executar um projeto com docker, pythonn e poetry
```

### Setar a versão do python
```bash
pyenv local 3.12.1
```

### Iniciar o poetry
```bash
poetry init
```

### informar ao poetry versão desejado do python
```bash
poetry env use 3.12.1 
```

### Ativar o ambiente virtual no poetry
```bash
poetry shell
```

### Instalar o streamlit
```bash
poetry add streamlit
```

### Executar o streamlit maquina local (teste)
```bash
poetry run streamlit run app.py
```

## Docker
### nessa etapa vamos criar uma imagem no arquivo docker file
```bash
FROM python:3.12        --imagem python
RUN pip install poetry  --instalar poetry
COPY . /src              --copiar tudo para src(como estivesse zipando codigo e docerfile)
WORKDIR /src             --trabalhar na pasta src   
RUN poetry install       --instalar o poetry
EXPOSE 8501             --expor a porta 8501
ENTRYPOINT ["poetry","run", "streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"] --executar o streamlit
```

### Criar a imagem do docker
```bash
docker build -t minha_primeira_imagem .
```

### Verificar porta 8501 está sendo utilizada
```bash
netstat -ano | findstr :8501
```

### Executar a container do docker
```bash
docker run -p 8501:8501 --name meu_primeiro_container minha_primeira_imagem
```