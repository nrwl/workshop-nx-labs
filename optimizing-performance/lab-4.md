ng g universal --collection=@schematics/angular customer-portal-universal
Update angular-cli.json:
  * Change customer-portal-universal "root": "apps/customer-portal/src",
  * "outDir": "dist-server/apps/customer-portal",
Update apps/customer-portal/src/tsconfig.server.json:
 * extend tsconfig.app.json instead of tsconfig.json
 *  compilerOptions: "paths": {
      "@tuskdesk-suite/*": [
        "../../../libs/*"
      ]
    }
(assumes installed @nguniversal/module-map-ngfactory-loader ts-loader @nguniversal/express-engine already)
app.server.module.ts
import { ModuleMapLoaderModule } from '@nguniversal/module-map-ngfactory-loader';


ng build --prod -a=customer-portal-universal --output-hashing=none
ng build --prod -a=customer-portal

Create server.ts:
```typescript
// These are important and needed before anything else
import 'zone.js/dist/zone-node';
import 'reflect-metadata';

import { enableProdMode } from '@angular/core';

import * as express from 'express';
import { join } from 'path';

// Faster server renders w/ Prod mode (dev mode never needed)
enableProdMode();

// Express server
const app = express();

const PORT = process.env.PORT || 4000;
const DIST_FOLDER = join(process.cwd(), 'dist');

// * NOTE :: leave this as require() since this file is built Dynamically from webpack
const { AppServerModuleNgFactory, LAZY_MODULE_MAP } = require('./dist/server/main.bundle');

// Express Engine
import { ngExpressEngine } from '@nguniversal/express-engine';
// Import module map for lazy loading
import { provideModuleMap } from '@nguniversal/module-map-ngfactory-loader';

app.engine('html', ngExpressEngine({
  bootstrap: AppServerModuleNgFactory,
  providers: [
    provideModuleMap(LAZY_MODULE_MAP)
  ]
}));

app.set('view engine', 'html');
app.set('views', join(DIST_FOLDER, 'browser'));

// TODO: implement data requests securely
app.get('/api/*', (req, res) => {
  res.status(404).send('data requests are not supported');
});

// Server static files from /browser
app.get('*.*', express.static(join(DIST_FOLDER, 'browser')));

// All regular routes use the Universal engine
app.get('*', (req, res) => {
  res.render(join(DIST_FOLDER, 'browser', 'index.html'), { req });
});

// Start up the Node server
app.listen(PORT, () => {
  console.log(`Node server listening on http://localhost:${PORT}`);
});
```

