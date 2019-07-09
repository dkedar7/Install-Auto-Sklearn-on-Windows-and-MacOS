# Install auto-sklearn on Windows 10
The best way to use auto-sklearn on a Windows 10 machine is to make use of the Windows Sussystem for Linux (WSL). 
### Step 1. Open command prompt as administrator, run powershell and enter the following command-
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
This will make you restart your computer at the end.

### Step 2. Install the Ubuntu app from the Windows store.

### Step 3. Install pip
Pip isn't installed by default and it will have have to be installed separately.
If the command 'sudo apt-get install python3-pip' is run directly, it will give the error 'E: Unable to locate package python3-pip'. So, run the following commands in sequence-
```
sudo apt-get install software-properties-common
sudo apt-add-repository universe
sudo apt-get update
sudo apt-get install python3-pip
```

### Step 4. Install numpy
```
pip3 install numpy
```

### Step 5. Install auto-sklearn
```
pip3 install auto-sklearn
```

Try running the follwing code to check if auto-sklearn was installed properly-
```
import autosklearn.classification
import sklearn.model_selection
import sklearn.datasets
import sklearn.metrics
```

# Install auto-sklearn on MacOS

## How to install AutoML's auto-sklearn on MacOS
Using a conda virtual environment is recommended.

### If everything is ideal, running the following should get you going.
```
conda install gcc
pip uninstall pyrfr auto-sklearn
curl https://raw.githubusercontent.com/automl/auto-sklearn/master/requirements.txt | xargs -n 1 -L 1 pip install
pip install pyrfr auto-sklearn --no-cache-dir
```

### But, when are things ideal.

## 1. If conda can't find gcc, use the following command-
(PackagesNotFoundError: The following packages are not available from current channels:)
```
conda install -c anaconda gcc
```
Run the command 'conda install gcc' again. It should work this time.

## 2. The next most common issue is due to failure in swig.
(Failed building wheel for pyrfr
error: command 'swig' failed with exit status 1)
Running the following command should solve this problem
```
conda install clang_osx-64 clangxx_osx-64 swig
```
Now, the command 'curl https://raw.githubusercontent.com/automl/auto-sklearn/master/requirements.txt | xargs -n 1 -L 1 pip install' should work just fine.

I did the exact same things so far and managed to install auto-sklearn successfully. After that, from python, I tried to 'import autosklearn.classification', but it wasn't compatible with my version of numpy.
I got the following error- ValueError: numpy.ufunc size changed, may indicate binary incompatibility. Expected 216 from C header, got 192 from PyObject

## 3. Solving numpy incompatibility
Turns out the numpy version 1.15.4 that I had wasn't compatible, so I'd to upgrade it to 1.16.1 using
```
pip install numpy==1.16.1
```

Try running the follwing code to check if auto-sklearn was installed properly-
```
import autosklearn.classification
import sklearn.model_selection
import sklearn.datasets
import sklearn.metrics
```
