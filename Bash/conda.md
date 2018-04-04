# Conda
## Creation:
```bash
conda create --name myenv [python=verisonnumber] [package names]
conda create --name myenv python=2.7 scipy
```
## Inspection:
```bash
List all packages: conda list
List all environments: conda info --envs
```

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
Conda create --help
```
### And Jupyter notebook
```bash
conda install ipykernel
```
