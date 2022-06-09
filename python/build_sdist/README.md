# Build Python source distribution

This action builds a Python package source distribution and a pure-Python wheel.
The built distributions are uploaded as an artefact in the ``dist`` directory.

## Inputs

### `package-path` - string, optional

Path to the Python package. Deafults to the root directory of the repository.
