# eg-angular-verdaccio
Example project to show making angular package and distribute with verdaccio.

# Install and configure Verdaccio
* Clone the repo and get localnpm folder
* Install 
$> npm install
* Start Verdaccio Server at :4873
$> npm run start
* Set registry url for npm to Verdaccio
$> npm set registry http://localhost:4873/

* If needed, change registry url back to original npm registry
$> npm set registry https://registry.npmjs.com

## Add User
* run "npm adduser" after changing registry
* "npm whoami" to check user


# Make Angular package from existing project
* export needed components
@NgModule({
  ...
  exports: [MyComponent]
  ...

* Install ng-packagr
npm install ng-packagr --save-dev

* Add ng-package.json to project
{
    "$schema": "./node_modules/ng-packagr/ng-package.schema.json",
    "lib": {
      "entryFile": "public_api.ts"
    }
}

* Add public_api.ts to export modules
export * from './src/app/app.module'

* Add packagr to scripts
"scripts": {
  ...
  "packagr": "ng-packagr -p ng-package.json"
}

* Add dependencies to whitelist in ng-package.json
"whitelistedNonPeerDependencies": [
    "@angular/animations",
    "@angular/common",
    ...
]

* run "npm run packagr"
dist folder will be created

* run "npm pack" in dist folder
.tgz file will be created

* run "npm publish package-version.tgz"


# References
- https://verdaccio.org/
- https://stackoverflow.com/questions/47152331/how-to-setup-angular-project-as-a-dependency-in-package-json-of-another-angular/48317155 (axl-code's answer)

* Timeout issue
https://github.com/verdaccio/verdaccio/issues/720