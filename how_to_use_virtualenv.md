# How to use virtualenv with Python in Windows

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
*Note that this path applies only for Windows and can be different among users.*
8. Follow the same steps to include pip PATH environment variable.

## 2. Virtual environments with *virtualenv*
Once everything is set up on your main local environment, you can start using the [*virtualenv*](https://virtualenv.pypa.io/en/latest/) tool to create your own personalized and isolated environments. It is particularly useful to use different package versions in parallel while running different jobs for different projects.

If you don't have *virtualenv* installed, please do so via pip and test the installation by looking at the version.
```
> pip install virtualenv
...
> virtualenv --version
16.1.0
```

### 2.1 Creating a virtual environment
To create a virtual environment, navigate to the project directory where you want to place it from the command line and run:
```
> virtualenv venv
```
*env* stands for the environment name. You can name it however you want (e.g. project-env, env, project-venv), but most will opt for venv. **NOTE** that it is important to include the path venv/ (or however you name your virtual environment) in the .gitignore file of your project in order to not save it on GitHub and potentially create conflict with other users.

By default, when creating a new virtual environment, the python version used is the default one installed and currently connected on your computer. If you want to use another one, let's say python 2.7, you can specify the python version as follows:
```
> virtualenv venv --python=python2.7
```
As you can notice here, the command *virtualenv* has been added to the PATH environment variables in order to use it as a command. Go to the steps described in [section 1.2](#1.2-managing-paths) to see how to do.

### 2.2 Using virtualenv
Using the virtual environment is somehow different depending on the shell scripting interface you are using. Here are the main possibilities on how to initiate the environment:

On windows CMD, run:
```
> source venv\Scripts\activate.bat
```
On Windows Powershell, you do not have to write the source command. Just run:
```
> venv\Scripts\activate.ps1
```
On Linux/Mac, run:
```
$ source venv/bin/activate
```

Note that the name of the virtual environment will be visible between parentheses in front of the directory in the command line. Here is an example:
```
# Working locally
./user/<username>/<projectdir>/ >

# Using a virtual environment
(venv) ./user/<username>/<projectdir>/ >
```

### 2.3 Packages & Requirements
Once you have created and activated your virtual environment, you can install all the packages you want using the pip command. 

The following command will save a text file storing the virtual environment dependencies in your directory in order to allow someone else working on the same project to initiate the same environment as yours. The same is applicable if working on a local environment.

To save a list of installed packages with Windows CMD, you can run:
```
(venv) ./user/<username>/<projectdir>/ > pip freeze > requirements.txt
```

When using Powershell, it is important to specify the encoding in order to have an appropriate and exportable requirements.txt file.
```
pip freeze | Out-File -Encoding ASCII requirements.txt
```

When working on a new project, the requirements can be uploaded in the virtual environment as follows:
```
(venv) ./user/<username>/<projectdir>/ > pip install -r requirements.txt
```
It will possibly be long to install all dependencies at first use, but the environment will be saved in cache to facilitate reload on the following use. From there, more modules can be installed in the environment with pip and saved back in the requirements text file. It is a continuous loop to include in the development process.

### 2.4 Deactivating
Once you have finished working on a project and want to work locally or from another virtual environment, you simply have to deactivate the current virtual environment. All packages and dependencies installed inside this environment will remain the same until you use it again. You can always improve your environment while you use it. Just don't forget to update the requirements.txt file once and a while to keep everything updated.

To deactivate the virtual environment, simply run:
```
(venv) ./user/<username>/<projectdir>/ > deactivate
```
The *(venv)* annotation in front of your command line should then disappear and you should now be working with your local default environment.

### 2.5 Deleting
To delete the virtual environment, just delete the associated folder directory directly in the folder window. In Windows, you can also delete it with the command line directly with ```> rmdir venv```, but make sure you are located in the folder containing the virtual environment main folder.

## 3. Launching a Jupyter Notebook
Just like in Anaconda, you can launch your own iPython Notebook using the command line. Instead of using the Anaconda package suite already compiled and ready for data science purposes, it will rely on the local pip environment, or the virtual environment set up.

To have more information on which package and environment manager to use (i.e. pip or conda), this [**article**](https://medium.freecodecamp.org/why-you-need-python-environments-and-how-to-manage-them-with-conda-85f155f4353c?gi=f7459170850) covers why Anaconda or Miniconda is also a good choice and compares it to pip.

### 3.1
In the console, run :
```
# Install the package
> pip install jupyter

# Start a local Jupyter Notebook server
> jupyter Notebook
```
A new browser window should then open on the Jupyter Notebook homepage. This page can also been accessed with an url (localhost:8888/). Note that if you use the numbered url (127.0.0.1:8888), it will require the token printed out in the console interface where the server was first called. It just needs to be copied and entered in the specified cell.

If the jupyter command does not work, verify if it is was added in the environment path variables. If not, follow the steps described in the section [1.2](#Managing-paths).
