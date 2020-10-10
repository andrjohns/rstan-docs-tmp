# Installing RStan

## Configuring Toolchain

Prior to installing RStan, you need to configure your R installation to be able to compile C++ code. Follow the link below for your respective operating system for more instructions:

 - Windows - Configuring C++ Toolchain
 - Mac - Configuring C++ Toolchain
 - Linux - Configuring C++ Toolchain

## Installing RStan

### Install Packages
You can now install RStan via:
```
install.packages("rstan", repos = "https://cloud.r-project.org/",
                 dependencies = TRUE)
```

Before moving to the next section verify that the following packages are at or above the indicated version:

 - ```rstan```: 2.21.2
 - ```StanHeaders```: 2.21.0-6
 - ```inline```: 0.3.16


### Verify Installation

To verify your installation, you can run the RStan example/test model:
```
library(rstan)
example(stan_model,run.dontrun = TRUE)
```

The model should then compile and sample. You may also see the warning:
```
Warning message:
In system(paste(CXX, ARGS), ignore.stdout = TRUE, ignore.stderr = TRUE) :
  'C:/rtools40/usr/mingw_/bin/g++' not found
```

This is safe to ignore and will be removed in the next RStan release.

# Encountering Errors

If you are unable to install RStan or successfully run the example/test model, then please open a new thread on the Stan forums (https://discourse.mc-stan.org) with a description of your problem and any error message, and we will help troubleshoot your installation.