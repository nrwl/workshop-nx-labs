# Lab: Create a Lazy Loaded UI Lib

## Scenario
The logs app needs some UI that displays the event logs reported by the system. Since apps should just be concerned with configuration and bootstrap, we will want to build this UI in libs.

The `lib` schematic has options that support creating libs that are configured for routing. Create a new lib for the list of logs that is lazy loaded by the logs app and use the Angular CLI schematic to generate a component to render some temporary log data in that new lib.

The Angular CLI schematic for generating a component:
```console
ng generate component <name>
```
(remember that you can always use the `-h` option flag to list details about the schematic)

## Instructions
1. Use the `lib` schematic to create a new lib named **logs-view**. Use the `--routing` and `--lazy` option flags and use the `--parent-module` option set to the **logs** app module file.
1. In the **logs** app module change the path on the route to an empty string.
1. Use the Angular CLI schematic to create a new component named **logs-list** and make use of the `--app` option to target the **logs-view** lib.
1. In the **logs-view** module, add a route with an empty path to the `LogsListComponent`. Include the `pathMatch: 'full'` property on the route object.
1. In the `LogsListComponent`, add a class field for logs and in the `ngOnInit` set that to an array of sample log objects (with a `message` property).
1. In the `logs-list.component.html`, add a `div` with an `ngFor` to render out the logs. Display the `message` in the div.

## Next Lab
Go to [Public APIs for Libs](lab-3.md)