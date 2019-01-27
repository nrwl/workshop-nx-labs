# Pre-Workshop Instructions

## Local Environment Requirements
The following are required to be able to work with the workshop code on your local machine:
- Node.js
- Git
- Angular CLI and Nx Schematics installed globally (done with NPM or Yarn)
  ```console
  npm install -g @angular/cli @nrwl/schematics
  ```

## The Project Code
We will be working with an existing Nx Workspace project repo during the workshop that can be found at:

https://github.com/nrwl/workshop-nx-starter

#### Pulling down the code
You can clone the repo onto your local machine by using the following **git** command at the terminal:
```console
git clone https://github.com/nrwl/workshop-nx-starter.git
```

#### Installing dependencies
Once you have that cloned you will want to change to that directory and use NPM (or Yarn) to install the project dependencies:
```console
cd ./workshop-nx-starter
npm install
```

#### Confirming the set up
There are two Angular applications in the repo to start with, a **customer portal** and a **reporting** app. There is also a node **server** app for the data API. After cloning the repo and installing the dependencies you will want to confirm that you are able to run these.

Run the following in 3 separate terminal windows within the local directory for your repo:
1. `npm run server`
1. `npm run customer-portal`
1. `npm run reporting`

These will start up in watch mode, so the terminal window will remain in use. You can cancel the watch mode with `ctrl+c` when you are ready to stop them. Make sure that these all run without any errors.

Then open up a browser and navigate to the 2 applications:
- Reporting App  
  http://localhost:4202
- Customer Portal App  
  http://localhost:4203

Confirm that these two apps render in the browser and that there are no console errors in the dev tools. Note that these apps have UI that is not interactive at some parts. Those are the parts we will build out in the workshop!

When you are done confirming that these apps run you can stop those watch runs by using `ctrl+c` in each terminal window.

#### Additional installs
The workshop covers NgRx, which has a way to hook into Redux dev tools for browsers. While not a requirement for the workshop, the Redux dev tools are most likely going to be something you will want to have as you write NgRx code going forward.

Instructions for installing the Redux dev tools can be found at:

https://github.com/zalmoxisus/redux-devtools-extension

#### Questions/Issues
If you run into any challenges please let us know prior to the workshop so we can work to assist in solving those challenges.
