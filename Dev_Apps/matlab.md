# Matlab/Octave

Each file is a function, check console to see output and run functions

IN other files simply call the function name

You need to add folders to the load path in octave, type `path` into console to see the current files

Arrays index from 1

```matlab
S[:] #pretty sure this turns matrix into vector?
S' #transpose matrix
size(S) #row, column
fprintf('size(A) is %s\n', mat2str(size(A)))
```

## Operations

```matlab
Z ./ 100 # elementwise 100?
```

## For loops

Very slow avoid at all costs

```matlab
for n=1:10
    experiment()
    fprintf('%d-Experiment Complete', n);
end
```

### Octave

In console, install pkgs with:

```matlab
pkg install --forge [package-name]
```

