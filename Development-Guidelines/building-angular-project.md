---
versionFrom: 7.0.0
---

# Working with the backoffice UI AngularJs project

## Overview
Umbraco 7 has a slightly unorthodox project structure, compared to a normal ASP.NET project. This is by design, a choice from the beginning to embrace a much larger group than the developers who know how to use Visual Studio.

As a result, the Umbraco UI is not a Visual Studio project, but a collection of folders and files, following certain conventions, and a small configuration file called `gulpfile` - we will get to the gulp part in a moment.

This means that anyone with a text editor can open the UI source, make changes and run the project, without having Visual Studio installed - we will get into how to do that in a moment as well.

The bottom line is the UI project has zero dependencies on ASP.NET or Windows. However, you will need Node.js installed, but don't worry we will get into that in a second.

## Prerequisites
Umbraco 7 needs a couple of things to run:

### Node.js
To compile and run the UI project you need [Node.js](https://nodejs.org) installed, it is needed for both Windows and OSX.

### gulp
When you have Node.js installed, you need to install gulp. gulp is a JavaScript task runner, basically like NAnt, MSBuild or any traditional build system [more about gulp here](https://gulpjs.com).

To install, open a terminal and run:

    npm install gulp-cli -g

For OSX users, you will most likely need to do:

    sudo npm install gulp-cli -g

This installs a `gulp` command into your terminal so you can run gulp scripts. That might sound scary, but really it isn't, while working with Umbraco 7, you will become really good friends with `gulp` and your terminal.

### Project dependencies
Now its time to install all the dependencies that the project requires to compile, debug, test, minify and so on. Luckily this is all automatic and is done with the Node.js package manager (which you already have installed with node)

In your terminal, browse to the `Umbraco.Web.Ui.Client` folder and run the command:

    npm install

This will output a ton of feedback in your terminal when it stops, your project is ready to run.

This might seem like a lot of stuff to do, but think of it this way, every time you set up this environment, all you have to do is run `npm install` and everything will be running smoothly.

## Running from source without Visual Studio or IIS
The Umbraco 7 project includes a complete mocked data model and an embedded web server to run off.

So to get the project up and running in a browser as fast as possible, open a terminal, browse to `Umbraco.Web.Ui.Client` folder and run the command:

    gulp dev

this will do the following:

- Compile and merge the project files
- Compile less files to one .css file
- Lint JavaScript files for syntax and style errors
- Run unit tests
- Setup a watcher to monitor for ongoing changes
- Start a web server on port 9999
- Open a browser to display localhost:9999/belle

gulp is doing all of this for us. Notice that it sets up a watcher, which means that every time you make a change, it will automatically recompile and test your code. If something is wrong the terminal will tell you why.

You can now login (no user/pass) and browse the UI with dummy data, this setup is perfect for fast CSS and JavaScript changes that do not require any *real* data.

## Running from Visual Studio

**Note:** we will make this even easier so the steps with node and gulp will not be required for .net developers in Visual Studio, but for now the below is needed:

To run from Visual Studio, open the solution and run the `Umbraco.Web.UI` project as a normal website project. But to get the latest Umbraco 7 files into this site you still need to open a terminal at `Umbraco.Web.Ui.Client` and run either:

    gulp dev

or for a one-time build:

    gulp build

This will compile all files and copy them into the appropriate folder in the VS project, if you run `gulp dev` it will also automatically update the VS project files as you edit them.

You should never edit the /umbraco/js/umbraco.*.js files directly, these will be overwritten on each build.

## using build.bat
The Umbraco source comes with a build.bat file that runs the full build process, which is the one we use on our nightly builds, it produces a complete zip file with a ready to use distribution.

The same rules apply as with running from Visual Studio, you need to run

    gulp build

Before running build.bat, then the latest UI files will be included.


## Conclusion
Having Umbraco 7 UI as a separate project does indeed give us a bit more complexity when building and running from Visual Studio since 2 build systems are in play: gulp and MSBuild.

However, the alternative would be to shove everything into the MSBuild process, making the entire thing inaccessible to a large number of frontend developers and with a clunkier and less up to date system.

So see it as an additional powerful tool in your arsenal, once you see the power, you don't want to go back.
