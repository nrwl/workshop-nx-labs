# Lab: Service Workers

Enable service worker in your application.

Run console command to update angular CLI settings:

```console
ng set apps.0.serviceWorker=true
```

Create new file:

```ts
import { ServiceWorkerModule } from '@angular/service-worker';
ServiceWorkerModule.register('/ngsw-worker.js', {enabled: environment.production})
```

```json 
apps/customer-portal/ngsw.json:
{
  "index": "/index.html",
  "assetGroups": [{
    "name": "customer-portal",
    "installMode": "prefetch",
    "resources": {
      "files": [
        "/favicon.ico",
        "/index.html"
      ],
      "versionedFiles": [
        "/*.bundle.css",
        "/*.bundle.js",
        "/*.chunk.js"
      ]
    }
  }, {
    "name": "assets",
    "installMode": "lazy",
    "updateMode": "prefetch",
    "resources": {
      "files": [
        "/assets/**"
      ]
    }
  }]
}
```


Make new npm script: 

```js
"customer-portal:service-worker": "ng build --prod -a=customer-portal && dist/apps/customer-portal --proxy=/api:http://localhost:3000/api"

```

Run the following commands:

```console 
npm run server
npm run customer-portal:service-worker
```

Steps:

*  Open Chrome Devtools > Application. Should see the service worker installed
*  Go to Chrome Devtools > Network. Check "Offline" checkbox.
*  Refresh page (Page should still load). Look at Network tab to see that all items were loaded from Service Worker.
*  Run lighthouse again and compare the scores. 
   >  Note: Lighthouse in Chrome devtools may not honor service worker cache, but the Chrome extension will.
