# Checkbox spread testing

This is an experiment that aims to provide a convenient way to test Checkbox

## Preparation

This repo uses image garden, to install image garden refer to this guide:

## Basic usage

This is the most basic usage. The changes in your local repo will be applied
to the edge version of the snap (the same snap as your base,
so core24 -> checkbox24) and every spread test will be exectuted against this
new "patched" snap. After that, spread will automatically collect artifacts
that the tests generate in a directory called `artifacts`

```bash
git clone https://github.com/Hook25/checkbox_snap_spread.git
cd checkbox_snap_spread
cp $PATH_TO_CHECKBOX_REPO .
image-garden.spread -artifacts=artifacts ubuntu-core-24
```

## Patching a different snap

Snap patching is a bit of an hack and not a silver bullet, it is faster than
building the snap from scratch but may not work in some situations. Notably,
when adding a new dependency, it will not work at all. For this reason, if
you add a `checkbox*.snap` package to the root of this repo before starting
the tests, it will be used instead of the edge version of Checkbox.

```bash
git clone https://github.com/Hook25/checkbox_snap_spread.git
cd checkbox_snap_spread
cp $PATH_TO_CHECKBOX_REPO .
cp $PATH_TO_CHECKBOX_XX_SNAP .
image-garden.spread -artifacts=artifacts ubuntu-core-24
```

## Testing the snap without patching

Finally, if building is not an issue, you can always put a `checkbox*.snap`
package in the root of the repo and no `checkbox` directory. This will run
the tests on the snap itself without patching it.

```bash
git clone https://github.com/Hook25/checkbox_snap_spread.git
cd checkbox_snap_spread
cp $PATH_TO_CHECKBOX_XX_SNAP .
image-garden.spread -artifacts=artifacts ubuntu-core-24
```

## Testing on other environments

This repo pre-defines a list of relevant environments, refer to spread.yaml to
have a comprehensive list. Although spread does support running the whole
matrix, there is no way to limit the maximum parallelism as of now, so
launching the whole matrix will probably quickly consume all RAM available on
your PC. To try it run:
```bash
image-garden.spread -artifacts=artifacts
```
