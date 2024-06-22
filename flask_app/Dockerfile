FROM --platform=linux/amd64  python:3.8-slim-buster as build

WORKDIR /flask-app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY templates  templates

COPY static static

COPY demo.py demo.py

EXPOSE 5000

CMD ["python3", "demo.py"]




