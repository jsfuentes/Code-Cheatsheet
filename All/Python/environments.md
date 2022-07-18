# Environments

## Pipenv vs virtualenv

Benefits of pipenv

- deterministic install with pipfile.lock
- Manages environment and pip simuletously
- Using new commands mean you dont have to remember to pip freeze 
- can have dev and prod envs 
- Easy way to enforce others use the best practice of environments, environments allow different global versions of packages
- Actually better syntax then virtual environments and pip freeze 

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