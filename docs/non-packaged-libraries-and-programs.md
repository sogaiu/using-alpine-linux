# Non-Packaged Libraries and Programs

## tree-sitter-module

For tree-sitter parser shared objects / libraries.

Already had these bits (also linked to from under `~/.emacs.d`), but FWIW:

```
cd ~/src
git clone https://github.com/casouri/tree-sitter-module
cd tree-sitter-module
bash batch.sh
```

## janet

To follow development of janet.

```
cd ~/src
git clone https://github.com/janet-lang/janet
cd janet
make clean && PREFIX=$HOME/.local make && PREFIX=$HOME/.local make install
```

