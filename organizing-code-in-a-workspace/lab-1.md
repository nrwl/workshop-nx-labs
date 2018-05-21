# Lab: Create an App and a Lib

### Scenario

>  Time: 10 minutes

An Nx Workspace is an Angular CLI project configured to support multiple Angular applications as well as libs. The existing workspace is already set up with a customer portal app, a reporting app, libs for thier UI and business logic and even a Node server API for the data.

We want to add a new "logs" app to the workspace that will show a list of event logs that occur across the usage of the apps. Make use of the `app` and `lib` schematics that Nx provides to create the pieces needed for the initial iteration of the logs application.

<img width="1438" alt="screen shot 2018-04-17 at 12 08 47 am" src="https://user-images.githubusercontent.com/210413/38851596-8b12b1de-41d3-11e8-9b81-de4244d07723.png">

<br/>

---

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

1. Create a new npm script in the `package.json` file to serve the new logs app. Name it "logs" and use the command `ng serve --proxy-config=proxy.config.json -a=logs -p=4204`. Try the script out to make sure it works (pull up the logs app in the browser at http://localhost:4204).

   > Bonus: Do you recall how to run the npm command and auto-open the browser?

1. Use the `lib` schematic to create a new lib named **logs-backend**.

1. Import the `LogsBackendModule` into the **logs** app module. Use the import path `@tuskdesk-suite/logs-backend`.

## Viewing in the Browser


Run the following command(s) in individual terminals:
- `npm run server`
- `npm run logs`

Open up the browser to:
- http://localhost:4204 (logs app)
- http://localhost:3000 (REST server)

![screen shot 2018-05-20 at 8 54 39 pm](https://user-images.githubusercontent.com/210413/40286980-0dec895c-5c70-11e8-98e1-76555b23f6a2.png)

>  Note: Sometimes a change to TypeScript interfaces will not get picked up by the watch so you may need to stop/restart these if you feel your code is correct but you are getting an error. If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`. 

## Next Lab
Go to Organizing Code in a Workspace Lab #2: [Create a Lazy Loaded UI Lib](lab-2.md)
