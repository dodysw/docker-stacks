# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/minimal-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# libav-tools for matplotlib anim
RUN apt-get update && \
    apt-get install -y --no-install-recommends libav-tools && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

# Install Python 3 packages
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
RUN conda install --quiet --yes \
    'ipywidgets=5.1*' \
    'pandas=0.18*' \
    'numexpr=2.5*' \
    'matplotlib=1.5*' \
    'scipy=0.17*' \
    'seaborn=0.7*' \
    'scikit-learn=0.17*' \
    'scikit-image=0.11*' \
    'sympy=1.0*' \
    'cython=0.23*' \
    'patsy=0.4*' \
    'statsmodels=0.6*' \
    'cloudpickle=0.1*' \
    'dill=0.2*' \
    'numba=0.23*' \
    'bokeh=0.11*' \
    'sqlalchemy=1.0*' \
    'h5py=2.5*' && \
    conda remove --quiet --yes --force qt pyqt && \
    conda clean -tipsy

# Activate ipywidgets extension in the environment that runs the notebook server
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix

# Configure ipython kernel to use matplotlib inline backend by default
RUN mkdir -p $HOME/.ipython/profile_default/startup
COPY mplimporthook.py $HOME/.ipython/profile_default/startup/

USER $NB_USER
