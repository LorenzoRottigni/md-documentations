
# Machine Learning Udemy Bootcamp 01 - Environment & setup

## Python Anaconda
Anaconda (https://www.anaconda.com) is a distro of python popular in data science and machine learning that includes several useful packages by default (such as jupyter, numpy, scipy, pandas, matplotlib, tensorflow, ...).
It's similar to a python virtual environment that has to be activated in order to use its requirements (conda activate).

Anaconda Navigator => anaconda control dashboard
Anaconda Prompt => anaconda CLI

### VENV
Pythonm virtual environment feature allows to have multiple Python versions and libraries on computer. 
```
# Create venv
conda create --name snowflakes numpy
# Activate venv
activate snowflakes
# Deactivate venv
deactivate
```
Conda create is used to create a new python venv: name flag defines the name of the the venv, positional args are libraries included in the created venv.
```
conda create --name v3venv python=3.5 anaconda numpy
```
Creates a venv named "v3venv" that uses python3.5 and has anaconda and numpy installed.
```
conda info --envs
```
Returns the list of venv available
## Jupyter
Jupyter is a development environment included with Anaconda, cool for analyzing and exploring data.
It allows the develop in interactive mode using a python instance as kernel behinde the scenes.
It combines "markdown cells" (read-only) with interactive "python cells"
commands:
- jupyter notebook: run jupyter in cwd