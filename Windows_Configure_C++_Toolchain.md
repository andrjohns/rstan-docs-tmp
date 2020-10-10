## Windows - Configuring C++ Toolchain

### R 3.6

#### Install RTools

The first step is to RTools3.5 from CRAN, also linked here: https://cran.r-project.org/bin/windows/Rtools/history.html

Next, we need to configure R to be able to find the installed toolchain. To do this, we need to add the RTools directory to the system PATH variable and set the BINPREF variable to point to the right compilers. We'll use the ```pkgbuild``` package to find the RTools installation directory (this is an RStan dependency, and so would have been installed regardless):
```
install.packages("pkgbuild")

rt_path = pkgbuild::rtools_path()
rt_bin = paste0(substr(rt_path,1,nchar(rt_path)-4),"/mingw_$(WIN)/bin/")
writeLines(paste0('PATH="',rt_path,';${PATH}"'), con = "~/.Renviron")
writeLines(paste0('Sys.setenv(BINPREF = "',rt_bin,'")'), con = "~/.Rprofile")
```

Then restart R and verify that the toolchain has been found by installing an R package from source:
```
install.packages("jsonlite",type="source")
```

### R4.0 

#### Remove old RStan configuration

If you had previously installed RStan under 3.6 you may have some configuration files left over that will cause issues under R4.0.

The first thing to check is whether the ```BINPREF``` environment variable is pointing to the old RTools installation by running ```Sys.getenv("BINPREF")```.

You can skip to the next section if your output looks like the following:
```
Sys.getenv("BINPREF")
[1] ""
```

However, if your output looks like:
```
Sys.getenv("BINPREF")
[1] "C:/Rtools/mingw_$(WIN)/bin/"
```
Then you need to check whether your ```.Rprofile``` file has been configured to set this variable on R startup. If you run the following command and get the output:
```
readLines("~/.Rprofile")
[1] "Sys.setenv(BINPREF = "C:/Rtools/mingw_$(WIN)/bin/")"
```

Then you need to delete your ```.Rprofile``` file. You can get the location of this file by running:
```
file.path(Sys.getenv("HOME"), ".Rprofile")
```
Delete that file and then restart R. If ```BINPREF``` is no longer set, then you should get the following output:
```
Sys.getenv("BINPREF")
[1] ""
```

#### RTools4 Installation

The first step is to install RTools4 following the instructions here: https://cran.r-project.org/bin/windows/Rtools/

Make sure that you follow the instructions that put RTools on the path. Repeated here for clarity:
```
writeLines('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', con = "~/.Renviron")
```

Then restart R and verify that RTools is being found via:
```
Sys.which("make")
## "C:\\rtools40\\usr\\bin\\make.exe"
```

And that you can install packages from source:
```
install.packages("jsonlite", type = "source")
```