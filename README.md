# Gradients _do_ grow on trees: a linear-time O(N)-dimensional gradient for statistical phylogenetics
This repository contains the instructions and files to reproduce the analyses performed in the "Gradients _do_ grow on trees: a linear-time O(N)-dimensional gradient for statistical phylogenetics" paper by Ji et al.


### Setting up BEAGLE
Please follow the [BEAGLE installation instructions](https://github.com/beagle-dev/beagle-lib).
But get the `hmc-clock` branch.

For Mac users, the following commands will compile the CPU version of BEAGLE.
Follow the [instructions](https://github.com/beagle-dev/beagle-lib) if you need to install any other dependent software.

```
xcode-select --install
brew install libtool autoconf automake
git clone -b hmc-clock https://github.com/beagle-dev/beagle-lib.git
cd beagle-lib
./autogen.sh
./configure --without-opencl --without-cuda
sudo make install
```


For Linux users, the commands are similar.

```
sudo apt-get install build-essential autoconf automake libtool git pkg-config openjdk-9-jdk
git clone -b hmc-clock https://github.com/beagle-dev/beagle-lib.git
cd beagle-lib
./autogen.sh
./configure --without-opencl --without-cuda
sudo make install
```


The libraries are installed into `/usr/local/lib`.
You can find them by `ls /usr/local/lib/*beagle*`.


### Setting up BEAST

The following commands will compile the `hmc-clock` branch of BEAST.

```
git clone -b hmc-clock https://github.com/beast-dev/beast-mcmc.git
cd beast-mcmc
ant
```

For Mac users, you may need to install ant by `brew install ant` through [Homebrew](https://brew.sh/).

For Linux users, you can install ant by `sudo apt-get install ant`.

This will compile the `jar` files under `beast-mcmc/build/dist/` where you can find `beast.jar`, `beauti.jar` and `trace.jar`.

### Reproducing the analyses

You may use the following commands for each case of the three data sets as described in the manuscript.

Change your working directory to where you want to store the resulting log files first.

```
cd where_you_want_to_save_results
```

#### West Nile Virus

* Optimization
	* Analytic gradient

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/WNV/WNV_skyline_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/WNV/WNV_HMC_skyline_MLE_Analytic.xml
	```
	
	* Numeric gradient 

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/WNV/WNV_skyline_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/WNV/WNV_HMC_skyline_MLE_Numeric.xml
	```

* MCMC
	* Univariate operator

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/WNV/WNV_skyline_Serial_save -seed 666 -overwrite where_this_repository_is_stored/xmls/WNV/WNV_skyline_Serial_only_rates.xml
	```
	
	* vanilla HMC

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/WNV/WNV_skyline_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/WNV/WNV_skyline_HMC_vanilla_only_rates.xml
	```	
	
	* digonal preconditioned HMC

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/WNV/WNV_skyline_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/WNV/WNV_skyline_HMC_diagonal_only_rates.xml
	```
	
	

#### Lassa Virus


* Optimization
	* Analytic gradient

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -force_resume -load_state where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_MLE_Analytic.xml
	```
	
	* Numeric gradient 

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -force_resume -load_state where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_MLE_Numeric.xml
	```

* MCMC
	* Univariate operator

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_Serial_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_Serial_only_rates.xml
	```
	
	* vanilla HMC

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_HMC_vanilla_only_rates.xml	
	```
		
	* digonal preconditioned HMC


	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Lassa/Lassa_S_skygrid_HMC_diagonal_only_rates.xml
	```


#### Dengue Virus


* Optimization
	* Analytic gradient

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_MLE_Analytic.xml
	```
	
	* Numeric gradient 

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_optimization_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_MLE_Numeric.xml
	```

* MCMC
	* Univariate operator

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_Serial_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_Serial_only_rates.xml
	```
	
	* vanilla HMC

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_HMC_vanilla_only_rates.xml	
	```
	
	
	* digonal preconditioned HMC


	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -beagle_SSE_off -load_state where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_HMC_save -seed 666 -overwrite where_this_repository_is_stored/xmls/Dengue/Large_Dengue_Skyride_HMC_diagonal_only_rates.xml
	```