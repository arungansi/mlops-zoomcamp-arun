FROM python:3.9.7-slim

RUN pip install -U pip
RUN pip install pipenv 

WORKDIR /app

#copy the 2 files to the working directory
COPY [ "Pipfile", "Pipfile.lock", "./" ] 

RUN pipenv install --system --deploy
# we dont want pipenv to create a virtual env. since we are inside a dedicated docker image we will specify --system which will install in the system python and not in virtual environment

COPY [ "predict.py", "lin_reg.bin", "./" ]

EXPOSE 9696

ENTRYPOINT [ "gunicorn", "--bind=0.0.0.0:9696", "predict:app" ]