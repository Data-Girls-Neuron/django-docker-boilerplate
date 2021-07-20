# django-docker-boilerplate

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
Primeiramente, vamos criar o arquivo de variáveis de ambiente `.venv.`
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
