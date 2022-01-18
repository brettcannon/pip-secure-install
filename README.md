# pip-secure-install
A GitHub action to have [pip](https://pypi.org/project/pip/) install from a
requirements file as securely as possible.

# Inputs

## `python`

The command to run Python (as `-m` is used to run pip). Defaults to `python`.

## `requirements-file`

The path to the requirements file. Defaults to `requirements.txt`.

## `options`

Additional command-line options to pass to pip (e.g. `--target`).

# Design

A few options are turned on for pip to make sure [installations are secure](https://www.python.org/dev/peps/pep-0665/#secure-by-design) and reproducible:

- A requirements file must be specified to make sure all dependencies are known
  statically for auditing purposes (`-r`).
- No dependency resolution is done to make sure the requirements file is
  complete (`--no-deps`).
- All requirements must have a hash provided to make sure the files have not
  been tampered with (`--require-hashes`).
- Only wheels are allowed to have reproducible installs (`--only-binary :all:`).
