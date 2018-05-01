# Lab: Run the Build Command and NPM Scripts

### Scenario

>  Time: 10 minutes

Building apps within an Nx Workspace is done with the Angular CLI `ng build` command and using the `--app` option for targeting the app to build (along with any other options).

Try out building the apps in the project and investigate the build artifacts as you use different build option flags. Also try out the npm scripts that Nx provides to only build affected apps and to format code.

## Instructions
1. Run the Angular CLI `build` command and use the `-a` option to target different apps in the workspace by name.

1. Explore the `dist` dir to see the results.

1. Run `build` again for an app with the `--prod` option flag, examine the results in the `dist` dir.

1. Run `build` for an app with `--prod` and `--build-optimizer` option flags, examine the results in the `dist` dir.

1. Run the npm script `affected:apps` and target the SHAs `1ee3a41` and `b88bc46` (remember, you can use ` -- ` to pipe additional args through to the npm script).

1. Test out the npm script `format` by making some formatting changes to an app or lib file and then running the script.

## Next Lab
Go to RxJS Lab #1: [Add Subscriptions to Ticket Search Form](/rxjs/lab-1.md)