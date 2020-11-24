---
layout: post
title: Creating a Virtual Environment and Run Jupyter Notebook Inside
date: 2018-10-01
---

# Why do we need a virtual environment?
A virtual environment creates an isolated environment for us to install needed packages to run a certain project without disrupting the 
working environment of other projects. It is a widely used strategy to run multiple data science projects on the same computer.

# How to create a virtual environment?
First, open _Anaconda Prompt_, create a virtual environment with pip and python 3.5 (other Python versions are also applicable; alternatively, you don't need to mention version) as follows:
```
(base) C:\Users\USERNAME>conda create -n virtualenv pip python=3.5.0
```
Here, _virtualenv_ is the name of the virtual environment. It can customized to anything.

You can use the following command to check the list of all virtual environment in the system and your newly created one should show up
as well.
```
(base) C:\Users\USERNAME>conda info --envs
```

Then, activate the virtual environment using the following command:
```
(base) C:\Users\USERNAME>conda activate virtualenv
```
Now you can install needed packages within the virtual environment. For example, to install the tensorflow package: 
```
(virtualenv) C:\Users\USERNAME>pip install https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.12.0-cp35-cp35m-win_amd64.whl
```

# How to run Jupyter Notebook in virtual environment?

In the virtual environment, run the following command to install IPython kernel:
```
(virtualenv) C:\Users\USERNAME>pip install ipykernel 
```
Then, create the Jupyter notebook kernel as follows:
```
(virtualenv) C:\Users\USERNAME>ipython kernel install --user --name=KERNELNAME
```
Now open a Jupyter notebook and then go to _Kernel_, you will see your newly created kernel named KERNALNAME. Enjoy using it!

To remove the kernel, first find the kernel list:
```
(virtualenv) C:\Users\USERNAME>jupyter kernelspec list
```
Then remove the targeted kernel using the following command:
```
(virtualenv) C:\Users\USERNAME>jupyter kernelspec uninstall KERNELNAME
```

# How to delete a virtual environment?
Make sure you deactivate the virtual environment or restart Anaconda Prompt. Use the following command to remove virtual environment:

```
$ conda env remove --name $MyEnvironmentName
```

Alternatively you can go to the C:\Users\USERNAME\AppData\Local\Continuum\anaconda3\envs\MYENVIRONMENTNAME and delete the folder manually.
