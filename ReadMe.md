# APS One Touch (AOT)

One touch is a tool to install all required software and tools for setting up STORDIS Advances Programmable Switches (APS) series.
This tools configures BF2556X_1T and BF6064X_T with BF_SDE, BSP, SAL(Switch Abstraction Layer) and Stratum
To get the files required by installer contact STORDIS.

Default input while execution i.e. when user just presses enter without any input appears in square braces i.e. '[n]' or '[do_nothing]'

## Release Compatibility 
|Device|AOT|SAL|APSN BSP|SDE|
|---|---|---|---|---|
|BF2556X_1T<br>BF6064X_T|v1.3.0|sal_1.1.0|bf-reference-bsp-9.2.0-BF2556_5189449.zip<br>bf-reference-bsp-9.2.0-BF6064_0ee36ac.zip|BF_SDE_9.2|
|BF2556X_1T<br>BF6064X_T|v1.2.0|sal_1.1.0|BF2556X-1T_BSP_9.0.0(master HEAD)<br>BF6064X_BSP_9.0.0(master HEAD)|BF_SDE_9.1<br>BF_SDE_9.2|



## settings.yaml

This is an input file for the tool so as to minimize user inputs. settings.yaml should be the first file to be modified while preparing APS.

By default, settings.yaml is picked up from project directory, But user can also give an absolute path to other setting file as a CLI argument while executing python scripts. 
Just that every other settings file should have format same as settings.yaml in project path.
This way user can save different settings in different files with relevant names and need not to modify same file while launching AOT with different settings.


## Quick start
For a quick start user should check for following node values in settings.yaml if different than default:
- SWITCH Model
- BF SDE
  - sde_pkg 
  - sde_home
- BSP 
  - ref_bsp
  - aps_bsp_pkg 
- BUILD_PROFILES -> selected -> '*sde_hw_profile'
- python3 InstallAPS.py

If you errors related to absent dependencies Refer section [How to run](#how-to-run) below.

By default, all the package paths are calculated relative to user_home or relative to `PATH_PREFIX` if provided.
For further node details see Profiles section below.

## Profiles

### sde_hw_profile
   Select the profile for installing BF_SDE and BSP on the switch. Check 'BF SDE' and 'BSP' nodes configuration in settings.yaml.
   
### sal_hw_profile
   Select the profile for using Switch Abstraction Layer (SAL) on the switch.
   Contact STORDIS to get sal.zip, unzip it into APS-One-touch/release/ directory.
   Check 'BF SDE', 'BSP' nodes configuration in settings.yaml.
   Currently 'SAL' node configuration in settings.yaml is useful for SAL development only for end users it can be ignored. Also on console only valid input for end users for 'SAL' is 'r' or 'run' or 'i' for installing thirdparty SWs in case SDE is not built with p4_runtime_profile.
   
### stratum_hw_profile
   For Stratum users on the switch.
   Check 'BF SDE', 'BSP', 'STRATUM' nodes configuration in settings.yaml. 'SAL' integration with STRATUM is in progress so need not to configure 'SAL' for stratum_x_profile and  
   select 'do nothing' for SAL while executing stratum_x_profile. 
   - x_sim_profile - Used for development.

## How to run

- Install dependency packages :
  - sudo apt install python3 (if not already installed)
  - sudo apt install python (python2.7 if not already installed, used by p4studio_build.py)
  - sudo apt-get install libusb-1.0-0-dev (required for BSP compilation)
  - sudo apt-get install libcurl4-openssl-dev (required for BSP compilation)
- Start installation :
  - python3 InstallAPS.py <optional - abs path to settings file>
- Also, if dependencies for a specific profile are already installed you can directly run the
 respective installation script for that profile.
 e.g. You can directly trigger SAL installation by executing 'python3 sal.py <optional - abs path to settings file>', in case dependencies SDE and BSP are already installed, This save user from giving inputs for dependencies.


## Recommendations
This version of AOT currently is tested on :
* Ubuntu 18.04.4 LTS
* gcc-8/g++-8


## Support

Raise issues or raise issue in GitHub repo : <https://github.com/apsnw/APS-One-touch/issues>
