# SFDX

This is a quick and easy deployment of a Lightning B2B testing environment using SFDX and shell scripts.

This repository provides configuration files and scripts that a Salesforce developer can use to setup a SFDX project in order to deploy the testing environment. The SFDX will include the metadata from the **examples** directory, converted to the SFDX format, and will have additional scripts for deployment steps supported only in the SFDX environment.

## Getting Started

### SFDX Setup
1. Before continuing with the steps below, see [Salesforce DX Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm) to setup SFDX.


### Quick Start

1. Clone the whole ccrz repository:
```
git clone <Repository URL>
```
If you cannot clone from that location, download the .zip file and unzip it locally.

2. From the sfdx directory, run the script
```
./convert-examples-to-sfdx.sh
```
that will convert the examples from the metadata API format to the SFDX format and add them to the "path" you have specified in the sfdx-project.json file.

3. Create a scratch org using SFDX:
If you don't have a dev hub already authorized, do that now by running
```
sfdx force:auth:web:login -d
```
This will open a new browser window where you have to enter the credentials of your Dev Hub. The -d option will set that Dev Hub as your default one. Once you're logged in, the Dev Hub is authorized and you can close the browser. The Dev Hub will manage your future scratch orgs.

Run the command that creates the scratch org and specify the username for the administrator:
```
sfdx force:org:create -f config/project-scratch-def.json username=<YourScratchOrgUsernameInEmailFormat> -s -d <DurationInDays>
```

Install B2B Commerce for Visualforce Manage Package:

https://help.salesforce.com/s/articleView?id=sf.b2b_commerce_install_urls.htm&type=5

To open the new org:
```
sfdx force:org:open
```
Note: if that fails, you might need to first set that new scratch org as your default org with
```
sfdx force:config:set defaultusername=<YourScratchOrgUsernameInEmailFormat>
```

Notice that the existing settings in the ```project-scratch-def.json``` file will enable all the necessary licenses and org perms and prefs required for Lightning B2B. If the scratch org creation is successful you should not need to modify any org perms or prefs. This is only available for the scratch orgs though, and will not work for sandboxes or other environments. For those orgs, follow the documentation about the licenses and org preferences that need to be enabled for B2B on Lightning.

4. Make sure that your current directory is sfdx and create and setup a new store in your new scratch org by running the following script:
```
./quickstart-create-and-setup-store.sh
```

You are done!


