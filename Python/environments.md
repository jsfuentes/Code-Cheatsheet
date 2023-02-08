# Environments

# Poetry

**Looks like Poetry is a [better/fast Pipenv**](https://piptrends.com/compare/poetry-vs-pipenv)

## Differences of Poetry vs Pipenv

- pyproject.toml(PEP spec) vs Pipfile to store more deps info
- Pipenv has python version management
- Faster

### Installation

Rec use asdf to install python versions

```bash
curl -sSL https://install.python-poetry.org | python3 -

curl -sSL https://install.python-poetry.org | asdf exec python3 - #if you are using asdf to manage python versions to avoid default pythons installed on MacOS
```

#### Setup

```bash
poetry --version
poetry init #setup in project creating pyproject.toml
```

## Usage

```bash
poetry add pendulum #add new package
poetry install #install all packages
poetry run python your_script.py #run
poetry shell #to enter the shell
poetry update #equivalent to deleting poetry.lock and rerunning
```

Make sure to put poetry.lock in VC

```
poetry env info #show env info
```

# Pipenv

## Pipenv vs virtualenv

Benefits of pipenv

- deterministic install with pipfile.lock
- Manages environment and pip simuletously
- Using new commands mean you dont have to remember to pip freeze 
- can have dev and prod envs 
- Easy way to enforce others use the best practice of environments, environments allow different global versions of packages
- Actually better syntax then virtual environments and pip freeze and requirements.txt

Disadvantages

- New intrusive commands for installation and running 
- another layer of abstraction using virtualenvs underneath
- https://github.com/pypa/pipenv/issues/796, if you mv the file you have to reinstall the pipenv :O [fix by having ]

## Setup

`pip install pipenv`

`pip install --user pipenv`

`pipenv install`create env if one doesn't exist or install everything

`pipenv --python 3` to specify version

## Usage

`pipenv install requests` instead of `pip install`

`pipenv install pymongo==3.4.0` for specific version

`pipenv run` to run stuff in virtual env

`pipenv run python` instead of `python`

##### Deploying

`pipenv install --deploy —system`

## Jupyter Notebook

To use a specific pipenv with jupyter notebook, install Jupyter and new kernel in the environment

```bash
pipenv install ipykernel
```

```bash
ipython kernel install --user --name=projectname
```

To later delete this kernel: 

- `jupyter kernelspec uninstall projectname`
- `jupyter kernelspec list`

# Venv

```
source venv/bin/activate

deactivate
```

