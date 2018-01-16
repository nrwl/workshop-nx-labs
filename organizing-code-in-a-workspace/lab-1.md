# Lab: 

## Scenario

## Instructions
1. Use the `app` schematic to create a new app named **logs**. Include the `--routing` flag. Use the `--dry-run` (or `-d` for short) to view what files will be created before hand.
1. Remove the default content in the `app.component.html` in the **logs** app and replace with an `h1` element for "TuskDesk Logs" and the `router-outlet` element.
1. Create a new npm script in the `package.json` file to serve the new logs app. Use the command `ng serve --proxy-config=proxy.config.json -a=logs -p=4204`. Try the script out to make sure it works (pull up the logs app in the browser at http://localhost:4204)
1. Use the `lib` schematic to create a new lib named **logs-backend**.
1. Import the `LogsBackendModule` into the **logs** app module. Use the import path `@tuskdesk-suite/logs-backend`.

## Next Lab
Go to []()