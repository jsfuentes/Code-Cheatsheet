# Environments

Recommended is venv because rest don't really work, but maybe should try mamba.

### Update Outdated Packages

```
pip3 list --outdated --format=freeze | grep -v '^\-e' | cut -d = -f 1 | xargs -n1 pip3 install -U 
```

# Venv

```bash
python3 -m venv venv
source venv/bin/activate
#....

deactivate
```



# Conda/Mamba

[Mamba](https://mamba.readthedocs.io/en/latest/) is a faster drop in replacement for conda (100% faster, takes half the time)

```bash
mamba create -n makeittalk_env python=3.6
```

#### Conda

## Creation:

```bash
conda create --name myenv [python=verisonnumber] [package names]
conda create --name myenv python=2.7 scipy
```

## Usage

```bash
source activate [envname]
```

## Installation

```bash
pip install -r requirements.txt
```

## Inspection:

List all packages

```bash
conda list
conda info --envs
```

List all environments

## Removal:

```bash
conda remove --name flowers --al
```

## EXPORT:

```bash
conda env export > environment.yml
```

### More:

```bash
conda env --help
conda create --help
```

### And Jupyter notebook

```bash
conda install ipykernel
```

# Poetry

- Looks like Poetry is a [better/fast Pipenv](https://piptrends.com/compare/poetry-vs-pipenv)
- **Not recommended sometimes it just doesn't work**, but venv does like with dlib
  - `ERROR: Could not build wheels for dlib, which is required to install pyproject.toml-based projects`

## Differences of Poetry vs Pipenv

- pyproject.toml(PEP spec) vs Pipfile to store more deps info
- Pipenv has python version management
- Faster

### Installation

```bash
curl -sSL https://install.python-poetry.org | python3 -

curl -sSL https://install.python-poetry.org | asdf exec python3 - #if you are using asdf to manage python versions to avoid default pythons installed on MacOS
```

#### Setup

Use asdf to manage python versions

```bash
asdf global python 3.11.2 #seems to need global setting to desired version
poetry init #setup in project creating pyproject.toml
#may or may not need to set python version in the setup wizard
poetry env use python #might be needed to set version
```

##### Pull from existing

```bash
cat requirements.txt | xargs poetry add #can then delete requirements.txt
```

## Usage

```bash
poetry add pendulum #add new package
poetry add pendulum@~3.1.4 #for specific minor(3.1) version
poetry add pendulum@^3.1.4 #for specific major(3) version

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
