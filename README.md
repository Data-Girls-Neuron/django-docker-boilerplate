# Django + Docker Boilerplate
- [English](https://github.com/Data-Girls-Neuron/django-docker-boilerplate/edit/main/README.md#english-version)
- [Portuguese](https://github.com/Data-Girls-Neuron/django-docker-boilerplate/edit/main/README.md#vers%C3%A3o-em-portugu%C3%AAs)

# English Version
## Setting up my Django application

Creating an application with the Django frameworks is quite simple, something that helps a lot when it comes to the web developers' daily basis.

For this tutorial, you must have `python` and `pip` already installed on your machine.

1. Django Installation
```
pip install django
```

2. Project creation

In the terminal of your OS, in the directory of the folder where the project will be stored, execute the following command:
```
django-admin.py startproject myproject
```
Then, enter the created project directory
```
cd myproject
```
Run the following command to create the application
```
python manage.py startapp core
```

3. Include the application within the project's `INSTALLED_APPS`

Add the `core` application within the application list in the `myproject/settings.py` file
```
INSTALLED_APPS = [
     'django.contrib.admin',
     'django.contrib.auth',
     'django.contrib.contenttypes',
     'django.contrib.sessions',
     'django.contrib.messages',
     'django.contrib.staticfiles',
     'core'
]
```

4. Adding `SECRET_KEY` to `.env` file (it must be inside `.gitignore`)

First, let's create the environment variables file `.env`
```
echo "SECRET_KEY=<mysecretkeyvalye>" >> .env
```
Then we will install the `django-environ` lib
```
pip install django-environ
```
Finally, we will add the following lines of code to the `myproject/settings.py` file
```
import environ

env = environ.Env()
environ.Env.read_env()

SECRET_KEY = env('SECRET_KEY')
```

5. Running the application

To verify that everything is running as it should, run the following command in your terminal
```
python manage.py runserver
```
By default, port `8000` will be used to upload the application (if you want to use port 8080, for example, use the command `python manage.py runserver 8080`). To verify if the application is running correctly, go to the URL `http://127.0.0.1:8000/` of your preferred browser. You should see the following screen:

![django](https://user-images.githubusercontent.com/37030292/126253538-e4296fc0-fdf5-41ca-97da-f5725f77b863.PNG)

6. Bonus: Freezing library versions

A very useful resource to manage the versions of the libraries used in your application is to create the `requirements.txt` file
```
pip freeze > requirements.txt
```
It makes it easier when we want, for example, to install specific versions of a lib inside the Docker container without affecting the versions of the same installed on your machine.

## Docker Setup

To upload Docker containers, we need to specify instructions with Docker files. In this case, the `docker-compose.yml` file describes the services to be created in each container, and the `Dockerfile` file details the step-by-step build that will be performed.

### docker-compose.yml

- `myproject_web`: service of the application itself.
- `myproject_web_migrate`: service for migrating the database from the main application.
- `myproject_web_run`: service to run the main application.

![image](https://user-images.githubusercontent.com/37030292/126871177-5df3401e-4d4c-4f3c-8974-5cf90af8fd30.png)

### Dockerfile

- `FROM python:3.9.1`: creates an image of the Docker hub (pre-formatted container with initial configuration), in the case of a Linux container with Python installed on it.
- `ENV PYTHONUNBUFFERED 1`: environment variables that will be used inside the container.
- `RUN mkdir /webapps` and `WORKDIR /webapps`: creating and indicating in which directory the project files will be stored.
- `COPY` and `ADD`: commands used to copy the versions of Python libs specified in the `requirements.txt` file to be installed inside the container.
- `EXPOSE 8000`: mapping the port from the Guest (container) to the Host (your computer).

![image](https://user-images.githubusercontent.com/37030292/126871188-55cfa8b5-f0ae-4eb6-920e-3190b7588c1c.png)

### Running the application with Docker

1. Enter your project directory

`cd myproject`

2. Build Docker images and containers

`docker-compose up -d`

- Build main application service
![docker1](https://user-images.githubusercontent.com/37030292/126871362-0899521c-93b1-43d5-8b8a-3be02a274f3b.PNG)

- Build database migration service
![docker2](https://user-images.githubusercontent.com/37030292/126871220-42002c96-2290-4b57-ae72-067e3ebc3b24.PNG)

- Build service to run main application
![docker3](https://user-images.githubusercontent.com/37030292/126871222-655dc9ee-dfd3-4523-964d-09d66c3cac93.PNG)

- Expected message after building Docker objects
![docker4](https://user-images.githubusercontent.com/37030292/126871229-f9a5ca6f-9a4e-412a-939f-c49cb91ee6d5.PNG)

3. Building and running your application

`docker-compose up --build`

4. Go to `127.0.0.1:8000` in your favorite browser

### Docker Hub

![image](https://user-images.githubusercontent.com/37030292/126871486-52c29d5d-f1c1-4be6-9a58-aef120d6fc86.png)

# Versão em Português
## Configurando minha aplicação Django

Criar uma aplicação com o framework Django é bem simples, algo que facilita em muito o dia-a-dia dos desenvolvedores web. 

Para este tutorial, pedimos que o `python` e o `pip` já estejam instalados na sua máquina.

1. Instalação do Django
```
pip install django
```

2. Criação do projeto

No terminal do seu SO, no diretório da pasta em que será armazenado o projeto, execute o seguinte comando:
```
django-admin.py startproject myproject
```
Depois, entre no diretório do projeto criado
```
cd myproject
```
E, então, execute o seguinte comando para criar a aplicação
```
python manage.py startapp core
```

3. Incluir a aplicação dentro dos `INSTALLED_APPS` do projeto

Adicione a aplicação `core` dentro da lista de aplicações no arquivo `myproject/settings.py`
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'core'
]
```


4. Adicionando a `SECRET_KEY` no arquivo `.env` ( o mesmo deve estar dentro do `.gitignore`)

Primeiramente, vamos criar o arquivo de variáveis de ambiente `.env`
```
echo "SECRET_KEY=<mysecretkeyvalye>" >> .env
```
Depois, faremos a instalação da lib `django-environ`
```
pip install django-environ
```
Por último, adicionaremos as seguintes linhas de código no arquivo `myproject/settings.py`
```
import environ

env = environ.Env()
environ.Env.read_env()

SECRET_KEY = env('SECRET_KEY')
```

5. Executando a aplicação

Para verificar se tudo está rodando como deveria, execute o seguindo comando no seu terminal
```
python manage.py runserver
```
Por default, será utilizada a porta `8000` para subir a aplicação (caso queira utilizar a porta 8080, por exemplo, utiliza o comando `python manage.py runserver 8080`). Para verificar se a aplicação está rodando corretamente, vá para a URL `http://127.0.0.1:8000/` do seu broswer de preferência. Você deve visualizar a seguinte tela:

![django](https://user-images.githubusercontent.com/37030292/126253538-e4296fc0-fdf5-41ca-97da-f5725f77b863.PNG)

6. Bônus: Freezando as versões das libraries

Um recurso muito útil para gerenciar as versões das bibliotecas utilizadas na sua aplicação é criar o arquivo `requirements.txt`
```
pip freeze > requirements.txt
```
O mesmo facilita quando queremos, por exemplo, instalar versões específicas de uma lib dentro do container Docker sem afetar as versões das mesmas instaladas na sua máquina.


## Setup Docker

Para subir os containers Docker, precisamos especificar as instruções com os Docker files. No caso, o arquivo `docker-compose.yml` descreve os serviços para serem criados em cada container, e o arquivo `Dockerfile` detalha o passo-a-passo do build que será realizado.

### docker-compose.yml

- `myproject_web`: serviço da aplicação em si.
- `myproject_web_migrate`: serviço para migração da base de dados em relação à aplicação principal.
- `myproject_web_run`: serviço para rodar a aplicação principal.

![image](https://user-images.githubusercontent.com/37030292/126871177-5df3401e-4d4c-4f3c-8974-5cf90af8fd30.png)


### Dockerfile

- `FROM python:3.9.1`: cria uma imagem do Docker hub (container pré-formatado com configuração inicial), tratando-se de um container Linux com Python instalado nele.
- `ENV PYTHONUNBUFFERED 1`: variáveis de ambiente que serão utilizadas dentro do container.
- `RUN mkdir /webapps` e `WORKDIR /webapps`: criando e indicando em qual diretório ficarão armazenados os arquivos do projeto.
- `COPY` e `ADD`: comandos utilizados para copiar as versões das libs Python especificadas no arquivo `requirements.txt` para serem instaladas dentro do container.
- `EXPOSE 8000`: mapeando a porta do Guest (container) para o Host (seu computador). 

![image](https://user-images.githubusercontent.com/37030292/126871188-55cfa8b5-f0ae-4eb6-920e-3190b7588c1c.png)

### Rodando a aplicação com Docker

1. Entre no diretório do seu projeto

`cd myproject`

2. Build das imagens e containers Docker

`docker-compose up -d`

- Build serviço da aplicação principal
![docker1](https://user-images.githubusercontent.com/37030292/126871362-0899521c-93b1-43d5-8b8a-3be02a274f3b.PNG)

- Build serviço de migração da base de dados
![docker2](https://user-images.githubusercontent.com/37030292/126871220-42002c96-2290-4b57-ae72-067e3ebc3b24.PNG)

- Build serviço para executar a aplicação principal
![docker3](https://user-images.githubusercontent.com/37030292/126871222-655dc9ee-dfd3-4523-964d-09d66c3cac93.PNG)

- Mensagem esperada após build dos objetos Docker
![docker4](https://user-images.githubusercontent.com/37030292/126871229-f9a5ca6f-9a4e-412a-939f-c49cb91ee6d5.PNG)

3. Realizando o build e executando sua aplicação

`docker-compose up --build`

4. Vá para `127.0.0.1:8000` no seu browser de preferência

### Docker Hub

![image](https://user-images.githubusercontent.com/37030292/126871486-52c29d5d-f1c1-4be6-9a58-aef120d6fc86.png)

