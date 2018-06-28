# Environments

## Pipenv vs virtualenv

Benefits of pipenv

- deterministic install with pipfile.lock
- Manages environment and pip simuletously
- Using new commands mean you dont have to remember to pip freeze 
- can have dev and prod envs 

Disadvantages

- New commands for installation and running 

## Setup

`pipenv install`create env if one doesn't exist or install everything

`pipenv --python 3` to specify version

## Usage

`pipenv install requests` instead of `pip install`

`pipenv run` to run stuff in virtual env

`pipenv run python` instead of `python`
