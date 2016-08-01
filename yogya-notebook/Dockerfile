# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# 2016-08-01 Dody - add cx_Oracle, XML parsing related libs, specil HTTP clients, and airflow
FROM dodysw/scipy-notebook

MAINTAINER Dody Suria Wijaya <dodysw@gmail.com>

USER root

#libaio1:  cx_Oracle pre-requisite in Debian system
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libaio1 \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

# addict = use dict like json
# lxml = dependency for zeep
RUN conda config --set ssl_verify False && \
    conda config --add channels conda-forge && \
    conda install --quiet --yes \
     'addict=1.0*' \
     'lxml=3.6*' \
     'oracle-instantclient=11.2*'

# cx_Oracle needs libraries from oracle
ENV ORACLE_HOME=$CONDA_DIR/orahome

# airflow = batch framework
# dicttoxml = parse xml to dict for easy access, use with addict for maximum convenience
# grequests = Concurrent HTTP request library
# zeep = Soap client library
RUN pip --no-cache-dir install \
     'airflow==1.7.1.3' \
     'cx_oracle==5.2.1' \
     'dicttoxml==1.7.4' \
     'grequests==0.3.0' \
     'zeep==0.13.0'
