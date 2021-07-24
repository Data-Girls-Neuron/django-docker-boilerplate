FROM python:3.9.1
ENV PYTHONUNBUFFERED 1

RUN mkdir /webapps
WORKDIR /webapps
COPY requirements.txt /webapps/
RUN pip install -r /webapps/requirements.txt
ADD . /webapps/

# Django service
EXPOSE 8000