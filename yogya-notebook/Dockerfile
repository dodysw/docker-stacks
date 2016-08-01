# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# 2016-08-01 Dody - add cx_Oracle, XML parsing related libs, specil HTTP clients, and airflow
FROM jupyter/scipy-notebook

MAINTAINER Dody Suria Wijaya <dodysw@gmail.com>

USER root

# cx_Oracle pre-requisite in Debian system
apt-get update && \
    apt-get install -y --no-install-recommends \
    libaio1 \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

RUN conda install --quiet --yes \
     'addict=1.0*' \
     'oracle-instantclient=11.2*'

# cx_Oracle needs libraries from oracle
ENV ORACLE_HOME=$CONDA_DIR/orahome

RUN pip --no-cache-dir install \
     'addict==1.0.0' \
     'airflow==1.7.1.3' \
     'cx_oracle==5.2.1' \
     'dicttoxml==1.7.4' \
     'grequests==0.3.0' \
     'zeep==4.1.4'
