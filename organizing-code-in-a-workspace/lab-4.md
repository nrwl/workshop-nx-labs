# Lab: Run the Build Command and NPM Scripts

### Scenario

>  Time: 10 minutes

Building apps within an Nx Workspace is done with the Angular CLI `ng build <app-name>` command (along with any other options).

Try out building the apps in the project and investigate the build artifacts as you use different build option flags. Also try out the npm scripts that Nx provides to only build affected apps and to format code.

## Instructions
1. Run the Angular CLI `build <app-name>` command to target different apps in the workspace by name.

1. Explore the `dist` dir to see the results.

1. Run `build` again for an app with the `--prod` option flag, examine the results in the `dist` dir.

1. Run `build` for an app with `--prod` option flag, examine the results in the `dist` dir.

1. Run Nx's npm script `affected:apps` to see which apps are affected based on your branch's changes since cloning: `npm run affected:apps -- --base=origin/master`

1. Test out Nx's npm script `format:write` by making some formatting changes to an app or lib file and then running the script.

## Next Lab
Go to RxJS Lab #1: [Add Subscriptions to Ticket Search Form](/rxjs/lab-1.md)