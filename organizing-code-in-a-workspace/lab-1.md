# Lab: Create an App and a Lib

## Scenario
An Nx Workspace is an Angular CLI project configured to support multiple Angular applications as well as libs. The existing workspace is already set up with a customer portal app, a reporting app, libs for thier UI and business logic and even a Node server API for the data.

We want to add a new "logs" app to the workspace that will show a list of event logs that occur across the usage of the apps. Make use of the `app` and `lib` schematics that Nx provides to create the pieces needed for the initial iteration of the logs application.

Schematics can be run at the terminal from within the workspace by running:
```console
ng generate <schematic-name> <options>
```
The generate command has an alias **g** that can be used.

A list of options for a schematic can be discovered by using the `--help` flag (or **-h**):
```console
ng g <schematic-name> --help
```

## Instructions
1. Use the `app` schematic to create a new app named **logs**. Include the `--routing` flag. Use the `--dry-run` (or `-d` for short) to view what files will be created before hand.
1. Remove the default content in the `app.component.html` in the **logs** app and replace with an `h1` element for "TuskDesk Logs" and the `router-outlet` element.
1. Create a new npm script in the `package.json` file to serve the new logs app. Use the command `ng serve --proxy-config=proxy.config.json -a=logs -p=4204`. Try the script out to make sure it works (pull up the logs app in the browser at http://localhost:4204)
1. Use the `lib` schematic to create a new lib named **logs-backend**.
1. Import the `LogsBackendModule` into the **logs** app module. Use the import path `@tuskdesk-suite/logs-backend`.

## Next Lab
Go to [Create a Lazy Loaded UI Lib](organizing-code-in-a-workspace/lab-2.md)