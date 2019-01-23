# How to use virtualenv with Python

Author: Guillaume Slevan-Tremblay

This tutorial will walk you through how to install and use virtual environments in your Python projects using *virtualenv*. Virtual environments are especially important when you work on many projects at the same time that require different package versions. It also is a good way to avoid dependencies errors in development phases and production debugging. It is highly recommended to start integrating this common practice to the daily workflow.

## 1. Install Python & pip
*If you already have Python and pip installed locally on your computer, you can skip to step 2.*

If you want to verify if it is indeed the case, you can run the commands below in your preferred shell interface. The message should show the version currently installed. In this case, the Python and pip versions installed are respectively 3.6.6 and 18.1.

```
> python --version
Python 3.6.6
> pip --version
pip 18.1 from c:\users\<username>\appdata\local\programs\python\python36\lib\site-packages\pip (python 3.6)
```

### 1.1 Installing Python
To install Python on your local drive, you can install the desired version from [python.org/downloads](https://www.python.org/downloads/). Make sure the Python version you install is compatible with the packages you plan on using as the latest version may not be incorporated in all packages yet.

Installing Python directly from their website will simultaneously install pip.

### 1.2 Managing paths
Windows - In Windows 10, you will often be required to add or modify **Path Environment Variables** to be able to use Python and pip directly in the shell. You may have to go through this procedure for most of the callable command you want to use in the shell.

1. Press Windows + R to open the **Run** dialog box.
2. Write "control panel", click OK and he control panel should open.
3. In the control panel, select **System and security** and then **System**.
4. In the left panel, click on **Advanced system settings**.
5. On the bottom left, click on **Environment Variables**. This is where the PATH environment variables are located and stored.
6. Under **System Variables**, select *Path* and click on **Edit**.
7. From there, you only have to add a new variable with the PATH where Python is installed. It should look like that: ```C:\Users\<username>\AppData\Local\Programs\Python\Python36\Scripts```.
8. Follow the same steps to include pip PATH environment variable.

## 2. Virtual environments with *virtualenv*
Once everything is set up on your main local environment, you can start using the [*virtualenv*](https://virtualenv.pypa.io/en/latest/) tool to create your own personalized environments. It is particularly useful to use different package versions in parallel while running different jobs for different projects.

If you don't have *virtualenv* installed, please do so via pip and test the installation by looking at the version.
```
> pip install virtualenv
...
> virtualenv --version
16.1.0
```

### 1. Creating a virtual environment
To create a virtual environment, navigate to the project directory where you want to place it from the command line and run:
```
> virtualenv env
```
*env* stands for the environment name. You can name it however you want (e.g. project-env, venv, project-venv), but the convention seem to opt for venv. **NOTE** that it is important to include the path env/ (or however you name your virtual environment) in the .gitignore file of your project in order to not save it on GitHub and potentially create conflict with other users.

By default, when creating a new virtual environment, the python version used is the default one on your computer. If you want to use another one, let's say python 2.7, you can specify the python version as follows:
```
> virtualenv env --python=python2.7
```
As you can notice here, the command *virtualenv* has been added to the PATH environment variables in order to use it as a command. Go to the steps described in [section 1.2](#1.2-managing-paths) to see how to do.

### 2. Using virtualenv
Using the virtual environment is somehow different depending on the shell scripting interface you are using. Here are the main possibilities on how to initiate the environment:

On windows CMD, run:
```
> source env\Scripts\activate.bat
```
On Windows Powershell, you do not have to write the source command. Just run:
```
> env\Scripts\activate.ps1
```
On Linux/Mac, run:
```
$ source env/bin/activate
```

Note that the name of the virtual environment will be visible between parentheses in front of the directory in the command line. Here is an example:
```
# Working locally
./user/<username>/<projectdir>/ >
# Using a virtual environment
(env) ./user/<username>/<projectdir>/ >
```

### 3. Packages & Requirements
Once you have created and activated your virtual environment, you can install all the packages you want using the pip command.

To save a list of installed packages, you can run:
```
(env) ./user/<username>/<projectdir>/ > pip freeze > requirements.txt
```
This will save a text file in your directory in order to allow someone else working on the same project to initiate the same environment as yours.

If you just cloned/added an ongoing project that requires the use of a virtual environment, create a virtual environment following steps 1 and 2. Then, install the requirements using this simple command:
```
(env) ./user/<username>/<projectdir>/ > pip install -r requirements.txt
```

### 4. Deactivating
Once you have finished working on a project and want to work locally or from another virtual environment, you simply have to deactivate the current virtual environment. All packages and dependencies installed inside this environment will remain the same until you use it again. You can always improve your environment while you use it. Just don't forget to update the requirements.txt file once and a while to keep everything updated.

To deactivate the virtual environment, simply run:
```
(env) ./user/<username>/<projectdir>/ > deactivate
```
The *(env)* in front of your command line should then disappear and you should now be working with your local default environment.

### 5. Deleting
To delete the virtual environment, just delete the associated folder directory directly in the folder window.
