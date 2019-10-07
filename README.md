## Create Unlocked Package

##### 1) Create an unlocked package without a namespace, and supply the alias or username for your Dev Hub org if it’s not already set as the default
   ```
   sfdx force:package:create --name dreamhouse --description "My Package" --packagetype Unlocked --path force-app --nonamespace --targetdevhubusername DevHub
   ```
* `--name` is the package name. This name is an alias you can use when running subsequent packaging commands.
* `--path` is the directory that contains the contents of the package.
* `--packagetype` indicates which kind of package you’re creating, in this case, unlocked.

##### 2) Open the sfdx-project.json
##### 3) Change the versionName to ``Version 1.0``, and the versionNumber to ``1.0.0.NEXT`` and let's save the sfdx-project.json file.
##### 4) In the `yourname` directory, create the package version, which associates the metadata with the package.
   ```
   sfdx force:package:version:create -p dreamhouse -d force-app -k test1234 --wait 10 -v DevHubAlias
   ```
* `-p` is the package alias that maps to the package ID.
* `-d` is the directory that contains the contents of the package.
* `-k` is the installation key that protects your package from being installed by unauthorized individuals.

It’s normal for the package version creation process to take several minutes.

    
    Successfully created the package version [08cxxx]. Subscriber Package Version Id: 04txxx.
    Package Installation URL: https://login.salesforce.com/packaging/installPackage.apexp?p0=04txxx
    As an alternative, you can use the "sfdx force:package:install" command.

##### 5) Notice that the packageAliases section in sfdx-project.json has a new entry
```json
"packageAliases" : {
   "dreamhouse" : "0Hoxxx",
   "dreamhouse@1.0.0-1" : "04txxx"
}
```

##### 6) Use the package version alias to install the package version in the scratch org that you created earlier
```
sfdx force:package:install --wait 10 --publishwait 10 --package dreamhouse@1.0.0-1 -k test1234 -r -u MyScratchOrg
```
It can take several minutes for a newly created package version to be available in the scratch org. The installation begins once the package version is available.

##### 7) After the package is installed, open the scratch org to view the package.
```
sfdx force:org:open -u MyScratchOrg
```



##### 8) From Setup, enter `Installed Packages` in the Quick Find box and select **_Installed Packages_**.