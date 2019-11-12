Jupyter Notebooks with Docker on Windows 7  
==========================================
Abstract:
```
Although Jupyter Notebooks are the de facto standard for data science to document
and develop Machine Learning processes, it still requires a significant amount of
work to install the required software on a local machine.  As requirements change
you may be required to add or remove existing software, creating dependency issues.
If you use a variety of tool chains this issue can become quite pronounced.  

In this presentation will show how to run Jupyter Notebooks locally on Windows 7
using docker pre-configured containers to avoid the dependencies issues, promote
sharing within a team, and speed development.
```
Note: This how-to assumes you have already installed Docker Toolbox on Windows.
We'll be using Cygwin (a unix shell plugin for Windows) but you are free to use whatever
command line tool you need.
 
Steps:  
* [Create a Local Docker Machine](#create-a-local-docker-machine)  
* [Configure Local Docker Machine NAT for Port 8888](#configure-local-docker-machine-nat-for-port-8888)  
* [Pull Jupyter Notebook Image](#pull-jupyter-notebook-image)  
* [Run the Jupyter Container](#run-the-jupyter-container) 
* [Access Notebook](#access-notebook) 
* [Restart Jupyter Container Once the Docker Machine has been Restarted](#restart-jupyter-container-once-the-docker-machine-has-been-restarted) 


## Create a Local Docker Machine
Create a local docker machine, the name can be anything you want, for this example we've used "jupyter-notebooks".  
Be sure docker is in your environment path variable.
```
docker-machine create -d virtualbox --virtualbox-memory=4096 jupyter-notebooks
```

## Configure Local Docker Machine NAT for Port 8888
So you can access the Jupyter Notebooks running on the container locally. Remember Jupyter Notebooks run on port 8888.    
Be sure virtualbox is in your environment path variable.
```
docker-machine stop jupyter-notebooks
vboxmanage modifyvm jupyter-notebooks --natpf1 ,tcp,,8888,,8888
docker-machine start jupyter-notebooks
```

## Pull Jupyter Notebook Image
Pull the jupyter Notebook first, it takes about 10 minutes
```
eval "$(docker-machine env jupyter-notebooks)"
docker pull jupyter/datascience-notebook
```

## Run the Jupyter Container
To start the contianer, run the following command.  We've named the container "datascience-notebook", but it's up to you.
```
docker run -p 8888:8888 -m 4g --name datascience-notebook \
-v /c/Users/kskalvar/git/Refactored_Py_DS_ML_Bootcamp-master:/home/jovyan/Refactored_Py_DS_ML_Bootcamp-master \
jupyter/datascience-notebook
```

## Access Notebook
Copy and paste URL displayed on the command line output in a browser
```
Example:
   http://127.0.0.1:8888/?token=2ca3e6e727c881220154faa141b82054f6549be73f4fcee3
```

## Restart Jupyter Container Once the Docker Machine has been Restarted
If you shutdown the machine, you can restart the container very easily without all the parameters.
```
docker start datascience-notebook
```

## References
Jupyter Notebook with Docker on Windows 7  
https://github.com/kskalvar/jupyter-notebook-with-docker-win7  

Docker Toolbox  
https://github.com/docker/toolbox  

Jupyter Docker Stacks  
https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html  

Cygwin  
https://cygwin.com  
