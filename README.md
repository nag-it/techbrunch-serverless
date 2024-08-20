# techbrunch-serverless

## serverless-azure

### Prerequisites

Install nodejs (if not already done)

Windows:

Visit https://nodejs.org/ and download the Windows Installer (.msi) for the LTS version

Linux:

```
sudo apt purge nodejs npm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
nvm install node
```

Install Azure Core Tools ( see [here](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Cisolated-process%2Cnode-v4%2Cpython-v2%2Chttp-trigger%2Ccontainer-apps&pivots=programming-language-csharp#install-the-azure-functions-core-tools))
```
npm i -g azure-functions-core-tools@4 --unsafe-perm true
```

The -g flag means that the package is installed globally on your system and should be available under (Windows)
```
C:\Users\<Your-Username>\AppData\Roaming\npm\node_modules\azure-functions-core-tools
```
To be able to run the Azure Functions Core Tools from the command line, you need to add the path to the executable to your PATH environment variable
```
C:\Users\<Your-Username>\AppData\Roaming\npm\node_modules\azure-functions-core-tools\bin
```

### Setup Project

Clone the following GitHub repository: https://github.com/nag-it/techbrunch-serverless.git

Or create your own project using Maven archetype:
```
mvn archetype:generate \
-DarchetypeGroupId="com.microsoft.azure" \
-DarchetypeArtifactId="azure-functions-archetype"
```

In both cases, please adjust *<functionAppName>serverless-azure-XYZ</functionAppName>* with your user id.

### Run locally

Build and run the project locally:
```
mvn clean package
mvn azure-functions:run
```
If you see errors like 'Failed to start Worker Channel. Process fileName: %JAVA_HOME%/bin/java' check out the following [solution](https://stackoverflow.com/questions/64032219/azure-function-in-java-does-not-work-locally)

Call the serverless function:
```
http://localhost:7071/api/HttpExample?name=Bob
```

### Deploy to Azure

Deploy the project to Azure:

```
az login
az account set --subscription=1bd6c9df-485a-459f-9a7c-6ce143b7909d

mvn clean package
mvn azure-functions:deploy
```