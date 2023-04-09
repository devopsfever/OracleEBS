1) Challenge build 1

Date : 22 Mar 2023

Angular Project build from Docker file
https://github.com/gothinkster/angular-realworld-example-app.git

-->  Issue 1:  Invalid host name

Fix    :   while staring angular service add --disable-host-check


--> Issue 2: jasime/core compatibility issue looking for version 3.8.0 but it had 3.6.0

FIX : Manauly go and change in application code package.json for jasime/core from 3.6.0 to 3.8.0

# Below are the scripts to change from scripts
sed 's/jasmine-core": "~3.6.0/jasmine-core": "~3.8.0/g' package.json > mypkg.json
sed 's/jasmine": "~3.6.0"/jasmine": "~3.8.0"/g' mypkg.json > opkg.json
cp opkg.json package.json


--> Issue 3: While starting the angualar service session got killed itself

FIX : Increase the memory of server, its less memory


