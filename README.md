[![Build Status](https://travis-ci.org/krishnan-r/sparkmonitor.svg?branch=master)](https://travis-ci.org/krishnan-r/sparkmonitor)
# Spark Monitor Fork - A fork of [SparkMonitor](https://krishnan-r.github.io/sparkmonitor/) that works with multiple Spark Sessions


## About
<table>
<tr>
<td><a href="http://jupyter.org/"><img src="https://user-images.githubusercontent.com/6822941/29750386-872556fe-8b5c-11e7-95e1-42b12d709017.png" height="50"/></a></td>
<td><b>+</b></td>
<td><a href="https://spark.apache.org/"><img src="https://user-images.githubusercontent.com/6822941/29750352-e9807b36-8b5b-11e7-929a-249f56c7cf79.png" height="80"/></a></td>
<td><b>=</b></td>
<td><a href="https://user-images.githubusercontent.com/6822941/29601568-d5e42934-87f9-11e7-9780-3cd3a0d8d86b.png" title="The SparkMonitor Extension."><img src="https://user-images.githubusercontent.com/6822941/29601568-d5e42934-87f9-11e7-9780-3cd3a0d8d86b.png" height="80"/></a></td>
</tr>
</table>
SparkMonitor is an extension for Jupyter Notebook that enables the live monitoring of Apache Spark Jobs spawned from a notebook. The extension provides several features to monitor and debug a Spark job from within the notebook interface itself. <br> 

***

![jobdisplay](https://user-images.githubusercontent.com/6822941/29753710-ff8849b6-8b94-11e7-8f9c-bdc59bf72143.gif)

## Features
* Automatically displays a live monitoring tool below cells that run Spark jobs in a Jupyter notebook
* A table of jobs and stages with progressbars
* A timeline which shows jobs, stages, and tasks
* A graph showing number of active tasks & executor cores vs time
* A notebook server extension that proxies the Spark UI and displays it in an iframe popup for more details
* For a detailed list of features see the use case [notebooks](https://krishnan-r.github.io/sparkmonitor/#common-use-cases-and-tests)
* [How it Works](https://krishnan-r.github.io/sparkmonitor/how.html)

<table>
<tr>
<td><a href="https://user-images.githubusercontent.com/6822941/29601990-d6256a1e-87fb-11e7-94cb-b4418c61d221.png" title="Jobs and stages started from a cell."><img src="https://user-images.githubusercontent.com/6822941/29601990-d6256a1e-87fb-11e7-94cb-b4418c61d221.png"></a></td>
<td><a href="https://user-images.githubusercontent.com/6822941/29601769-d8e82a26-87fa-11e7-9b0e-91b1414e7821.png" title="A graph of the number of active tasks and available executor cores."><img src="https://user-images.githubusercontent.com/6822941/29601769-d8e82a26-87fa-11e7-9b0e-91b1414e7821.png" ></a></td>
<td><a href="https://user-images.githubusercontent.com/6822941/29601776-d919dae4-87fa-11e7-8939-a6c0d0072d90.png" title="An event timeline with jobs, stages and tasks across various executors. The tasks are split into various coloured phases, providing insight into the nature of computation."><img src="https://user-images.githubusercontent.com/6822941/29601776-d919dae4-87fa-11e7-8939-a6c0d0072d90.png"></a></td>
</tr>
<tr>
<td><a href="https://user-images.githubusercontent.com/6822941/29750236-be1f6b0c-8b59-11e7-9a36-92e04e3bf05b.png" title="The Spark web UI as a popup within the notebook interface."><img src="https://user-images.githubusercontent.com/6822941/29750236-be1f6b0c-8b59-11e7-9a36-92e04e3bf05b.png" ></a></td>
<td><a href="https://user-images.githubusercontent.com/6822941/29750177-ea2c18b8-8b58-11e7-955e-69ecf33a6284.png" title="Details of a task."><img src="https://user-images.githubusercontent.com/6822941/29750177-ea2c18b8-8b58-11e7-955e-69ecf33a6284.png" ></a></td>
<td><a href="https://user-images.githubusercontent.com/6822941/29601997-d6533840-87fb-11e7-90ce-daa0fe73b9e5.png" title="An event timeline."><img src="https://user-images.githubusercontent.com/6822941/29601997-d6533840-87fb-11e7-90ce-daa0fe73b9e5.png"></a></td>
</tr>
</table>

## Build from source
npm version: 5.6.0
yarn version: 1.22.4
sbt version: 1.3.2
```bash
cd sparkmonitor/extension
#Build Javascript
yarn install # Only need to run the first time
yarn run webpack
#Build SparkListener Scala jar
cd scalalistener/
sbt package
```

## Run Locally
```bash
docker build -t sparkmonitor .
docker run -it -p 8888:8888 sparkmonitor
```

## Deploy New Version
```bash
cd sparkmonitor/extension
vi VERSION # bump version number
python setup.py sdist
twine upload --repository-url https://upload.pypi.org/legacy/ dist/*
```
If twine upload step fails, run `rm -rf dist/*`, bump the VERSION number, and rerun steps above.

## Quick Installation
```bash 
pip install sparkmonitor-s
jupyter nbextension install sparkmonitor --py --user --symlink 
jupyter nbextension enable sparkmonitor --py --user            
jupyter serverextension enable --py --user sparkmonitor
ipython profile create && echo "c.InteractiveShellApp.extensions.append('sparkmonitor.kernelextension')" >>  $(ipython profile locate default)/ipython_kernel_config.py
```
#### For more detailed instructions [click here](https://krishnan-r.github.io/sparkmonitor/install.html)

## Integration with ROOT and SWAN
At CERN, the SparkMonitor extension would find two main use cases:
* Distributed analysis with [ROOT](https://root.cern.ch/) and Apache Spark using the DistROOT module. [Here](https://krishnan-r.github.io/sparkmonitor/usecase_distroot.html) is an example demonstrating this use case.
* Integration with [SWAN](https://swan.web.cern.ch/), A service for web based analysis, via a modified [container image](https://github.com/krishnan-r/sparkmonitorhub) for SWAN user sessions.

