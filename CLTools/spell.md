# Spell

Run code on GPUS like a god

## Setup

```bash
spell login
spell whoami
```

## Usage

```bash
# default CPU
spell run "python example.py"

# Nvidia's Tesla K80
spell run -t K80 "python example.py"

# Nvidia's Tesla V100 multi-GPU option
spell run -t V100x4 "python multi-example.py"
```

## Resources

Store data in resources

```bash
spell upload simpleNN/data/
spell ls
```

## Workspace

Create a workspace in the GUI, upload a jupyter file, and goooooo ez. Easily use resources. 