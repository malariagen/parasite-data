# MalariaGEN Parasite Data

This repository provides technical documentation for parasite data, including access to the data resource and accompanying Jupyter Notebooks.

For further information, please see the [Parasite Data User Guide](https://malariagen.github.io/parasite-data/).

If you find a bug related to usage, public data or documentation, please raise an issue on this repository.

## Contents

- [Data Resources](#Data-Resource)
- [Accesing the Documentation](#Accesing-the-Documentation)
- [Running the Notebooks (Google Colab)](#Running-the-Notebooks-Google-Colab)
- [Running the Notebooks (Locally)](#Running-the-Notebooks-Locally)
  - [Dependencies](#Dependencies)
  - [How to Install Python Modules in a Virtual Environment](#How-to-Install-Python-Modules-in-a-Virtual-Environment)
  - [Cloning the Repository](#Cloning-the-Repository)
  - [Running Jupyter](#Running-Jupyter)
- [Documentation for Developers](#Documentation-for-Developers)
  - [Deployment](#Deployment)
  - [Making Changes to the Notebooks](#Making-Changes-to-the-Notebooks)
  - [Data Analysis](#Data-Analysis)
  - [Developing on JupyterLab on the Farm](#Developing-on-JupyterLab-on-the-Farm)

### Data Resource

The current data resources available are: - Pf7

The resources are explored through a series of Jupyter Notebooks, accessible from the `docs` directory in this repository.

### Accesing the Documentation

You can view the documentation [here](https://malariagen.github.io/parasite-data/). The notebooks and output plots are interactive, allowing you to explore the different dimensions of the dataset, and to visualise specific data points (e.g. by hovering and zooming in and out using the tool bar).

### Running the Notebooks (Google Colab)

The suggested way to use the resource is to open the notebooks in Google Colab, this will allow you to run code and change parameters, without any need for local installations. To do this open the [documentation](https://malariagen.github.io/parasite-data/) and select the notebook you would like to open. Click on the rocket icon in the top right hand corner and select `Colab`, as shown below.

!["Open colab"](docs/images/open_colab.png)

### Running the Notebooks (Locally)

To run the notebooks on your own computer you will need to clone this repository and install the following dependencies:

#### Dependencies

- Jupyter
- Python3
- numpy
- folium
- matplotlib
- bokeh
- pandas

#### How to Install Python Modules in a Virtual Environment

Running this notebook on your own machine requires Python packages to be installed. We recommend doing this in a virtual environment. Note that if `virtualenv` is not installed on your computer, you will need to use: `pip install virtualenv`.

Open a terminal and follow these instructions:

1. Create a virtual environment by typing out the following commands, replacing `<path to python3>`:

```
virtualenv -p <path to python3> parasite_notebooks_env
source parasite_notebooks_env/bin/activate
```

2. Install the dependencies in the virtual environment:

```
pip install numpy folium matplotlib bokeh pandas
```

To exit out of the environment simply type the following on the command line:

```
deactivate
```

If you want to enter the environment again you won't need to re-install the dependencies. Simply enter the following on the command line and it will load up everything you installed before:

```
source parasite_notebooks_env/bin/activate
```

#### Cloning the Repository

You will then need to clone this repository to your own machine. Navigate to where you would like to store this and run the following command:

```
git clone https://github.com/malariagen/parasite-data.git
```

#### Running Jupyter

To launch the notebooks on your own computer you will need to have Jupyter installed. If you don't have this already, you can install it using `pip` with the following command:

```
pip3 install jupyter
```

To launch Jupyter Notebook simply navigate to where you cloned this repository and run the following:

```
cd docs
jupyter-notebook
```

This should open a web page with directories showing. Simply click on the resource you would like to find out more about and select the notebook you would like to open. We recommend starting with `Metadata.ipynb`.

## Documentation for Developers

The documentation is a set of Jupyter Notebooks contained in the `docs` directory.

### Deployment

The notebooks are deployed automatically as a Jupyter Book to GitHub Pages by a GitHub Workflow. This is configured in `parasite-data/.github/workflows/gh-pages.yml` to install dependencies, build the book, and push it to `gh-pages`. The dependencies are listed in `requirements-deploy.txt`. This will run when a change is merged into the master branch.

The configuration for the Jupyter Book is set up in the `docs/` directory by three files:

- **\_config.yml** : contains the configuration for the book.
- **\_toc.yml** : configures the layout for the different sections of the book.
- **landing-page.md** : formats the landing page for opening the book.

### Making Changes to the Notebooks

To make any changes please use a new branch. Before merging into the master branch, you should test any changes locally.
To do this, you will need jupyter-book which can be installed via `pip`.

Navigate to the head directory of the repository and run the following to build the Jupyter Book locally:

```
jupyter-book build docs
```

If everything is successful this should output a link. Copy and paste this into your browser to check that your changes are as expected.

### Developing on JupyterLab on the Farm

1. Log into the farm
2. Clone the [bsub jupyterlab repository](https://github.com/wtsi-hgi/bsub_jupyter_lab)
3. Clone the [parasite-data repository](https://github.com/malariagen/parasite-data)
4. From the head directory of `bsub_jupyter_lab` run the following command, replacing `<team>` with your lsf group:

```
./bsub_jupyter_lab.sh -g <team> -c 4 -m 50000 -q normal
```

5. Copy the link that is output into your browser and JupyterLab should load
6. Create a virtual environment and activate it

```
virtualenv -p <path to python3> parasite_env
parasite_env/bin/activate
```

7. Install using pip

```
pip install ipykernel numpy folium matplotlib bokeh pandas
```

8. Manually add the kernel so you can select it in the notebook

```
python -m ipykernel install --user --name=parasite_env
```

9. Open notebook and set kernel to `parasite_env`
10. When you are done with this environment you can remove it as an option from your jupyter notebooks by running:

```
jupyter kernelspec uninstall parasite_env
```
