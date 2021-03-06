TSD - A TypeScript definition package manager
=============================================

TSD is a TypeScript definition file package manager.  let you easily download and install definition files to use in TypeScript projects.

> To view online package search - http://www.tsdpm.com/

> To view how to use TSD with NuGet Console - [Using TSD with Visual Studio Nuget Console](https://github.com/Diullei/tsd#using-tsd-with-visual-studio-nuget-console)

> To contribute by adding new references - [How to contribute](https://github.com/Diullei/tsd#how-to-contribute)

### How to install

TSD is installed using [node](http://nodejs.org/) and [npm](https://npmjs.org/). To install TSD use:

    npm install tsd -g

### Usage

> Your best friend at this stage is probably `tsd -h`.

To view all repository files use:

    tsd all

This will print all file definitions available on repository. To install some file on local project you must use `install` command followed by a lib name:

    tsd install node

This will create by default a folder named `d.ts` (if it doesn't exists) and will download the file definition to this folder.

### TSD configuration

You can define your own custom folder to store definition files with the command:

	tsd ncfg

This will create a file named `tsd-config.json` on current folder with the following content:

```json	
{
	"localPath": "ts-definitions",
	"repositoryType": "1",
	"uri": "https://github.com/Diullei/tsd/raw/master/deploy/repository.json"
}
```

* **localPath** - Must be the path to your local folder to store definition files. This folder will be created in the first time if not exists.
* **repositoryType** - this property is used to define if uri is a local folder or a url. Use `0` to local folder or `1` to url.
* **uri** - Define if the repository file is an url or a local folder.

### Installing dependencies

Some definition files have dependencies of another files like `socket.io` that depends of `node`. To install dependencies you can use `tsd install` command followed by a list of libs to install. 

Example:

	tsd install socket.io node express
	
This will install _express_, _socket.io_ and _node_ definitions.

### Install dependencies automatically

You can use `install*` command to allow TSD tool to automatically map and install all necessary dependencies. If you use `install* sochet.io` this will install `sochet.io` and `node` because `sochet.io` has `node` mapped as a dependency. If you use the command:

	tsd install* knockback
	
TSD will install `knockback`, `knockout` and `backbone` definition.

### Checking for updates

You can always use `tsd update` command to verify if your local libs are updated.

### Repository

To make a search for any file you must use `search` command.

Example:

    tsd search backbone

TSD get the file definitions from [DefinitelyTyped](https://github.com/borisyankov/DefinitelyTyped) project. You can view the repository references inside [repository.json](https://github.com/Diullei/tsd/blob/master/deploy/repository.json) file (I'm working to add some anothers). If you want to contribute please make a fork from tsd repo, change the repository.json and make a pull request.

> This file is updated constantly.

## How to contribute

To contribute adding new definition files references, "fork" this project and add a new file on `repo_data` folder according to the following specifications:

```javascript	
{
  "name": "LIB NAME", // must match the file name without json extension
  "description": "LIB DESCRIPTION",
  "versions": [
    {
      "version": "x.x", // LIB VERSION
      "key": "FILE VERSION KEY", // must be a unique key like a guid. You can use this tool 
      				 // http://www.guidgenerator.com/ to generate this key
      "dependencies": [
        {
          "name": "LIB NAME",
          "version": "VERSION"
        }
      ],
      "url": "DEFINITION FILE URL",
      "author": "DEFINITION FILE AUTHOR",
      "author_url": "AUTHOR URL"
    }
  ]
}
```

Example:

```json	
{
  "name": "angular-resource",
  "description": "Google - Angular.Js",
  "versions": [
    {
      "version": "1.0",
      "key": "8918D3CF-AAF2-4572-B3D2-509716336A99",
      "dependencies": [
        {
          "name": "angular",
          "version": "latest"
        }
      ],
      "url": "https://github.com/borisyankov/DefinitelyTyped/raw/master/angularjs/angular-resource.d.ts",
      "author": "Diego Vilar",
      "author_url": "https://github.com/diegovilar"
    }
  ]
}
```

Done that, send a pull request.

> NOTE: The definition files can be placed anywhere on the web, however I think [this project](https://github.com/borisyankov/DefinitelyTyped) ([DefinitelyTyped](https://github.com/borisyankov/DefinitelyTyped)) is the best place.

## Using TSD with Visual Studio NuGet Console

You can use TSD with Visual Studio NuGet Console. NuGet Console is a PowerShell Console and can normally call any application on Windows PATH. For view how to use TSD I suggest the following steps:

### Prerequisites

* [TypeScript Visual Studio Plugin](http://www.microsoft.com/en-us/download/details.aspx?id=34790)
* TSD 0.3.1 or last - [View How to install section](https://github.com/Diullei/tsd#how-to-install)

### Steps

1. Open Visual Studio and Create a TypeScript application 

![](https://github.com/Diullei/tsd/raw/master/doc_img/create_ts_app.png)

> I will create an application named `TestApp`

2. Open NuGet Console

![](https://github.com/Diullei/tsd/raw/master/doc_img/open_nuget_console.png)

3. Goto TestApp root folder. Enter the `cd .\TestApp` command on NuGet Console.

4. Create a TSD config file. On NuGet Console use the command: `tsd ncfg`.

![](https://github.com/Diullei/tsd/raw/master/doc_img/tsd_cnfg_nuget.png)

5. Now you can see that TSD has created a file named `tsd-config.json` on your app root folder. To include this file on your application go to Vidual Studio Solution Explorer and select `Show All Files`.

![](https://github.com/Diullei/tsd/raw/master/doc_img/show_all_files.png)

This will show `tsd-config.json` file on Solution Explorer.

6. Take right click on `tsd-config.json` file and select `Include In Project`. Now you can edit this file on visual Studio. [See configuration section](https://github.com/Diullei/tsd#tsd-configuration).

7. Try install `jquery` definition file using `tsd install jquery` on NuGet Console and go to Vidual Studio Solution Explorer and select `Show All Files`(if it is not enabled) to view `ts-definition` folder with `jquery` definition file. Include this folder in project.

> You can test other TSD commands like `tsd all` [See usage section](https://github.com/Diullei/tsd#usage).

## Change log

### v0.3.1 (2013-01-26)

* Web site http://www.tsdpm.com/
* Friendly console output.

### v0.3.0 (2013-01-25)

* Multiple installs at once install command [#3](https://github.com/Diullei/tsd/issues/3). Thanks to [@Crwth](https://github.com/Crwth)
* Command for show/info [#2](https://github.com/Diullei/tsd/issues/2). Thanks to [@semperos](https://github.com/semperos)
* Allow user to change repository url from local config file
* Command to create local config file
* Solved issue: DefinitelyTyped directory structure is lost [#4](https://github.com/Diullei/tsd/issues/4). Thanks to [@Crwth](https://github.com/Crwth)

### v0.2.2 (2012-11-07)

* Fix: now tsd works on linux/mac. Issue [#1](https://github.com/Diullei/tsd/issues/1). Thanks to [@seanhess](https://github.com/seanhess)

## License

TSD is distributed under the MIT license. [See license file here](https://raw.github.com/Diullei/tsd/master/LICENSE.txt) or below:

Copyright (c) 2012 by Diullei Gomes

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.