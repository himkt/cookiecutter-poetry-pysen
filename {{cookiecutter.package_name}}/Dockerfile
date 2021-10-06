FROM python:3.8.12-slim-buster as builder

RUN pip3 install poetry==1.1.7
RUN pip3 install -U setuptools==57.5.0

WORKDIR /work

COPY pyproject.toml                ./
COPY poetry.lock                   ./
COPY {{cookiecutter.package_name}} ./{{cookiecutter.package_name}} 

RUN poetry export -f requirements.txt -o requirements.txt --dev


FROM python:3.8.12-slim-buster as runner

WORKDIR /work

COPY --from=builder /work/requirements.txt ./requirements.txt
COPY --from=builder /work/{{cookiecutter.package_name}} ./{{cookiecutter.package_name}}
COPY pyproject.toml ./

RUN pip3 install -r requirements.txt
RUN pip3 install .
