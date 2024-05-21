
command line tool and registry of 3rd party libraries that we can add to our node applications.

// Install a package
npm i <packageName>
// Install a specific version of a package
npm i <packageName>@<version>
// Install a package as a development dependency
npm i <packageName> —save-dev
// Uninstall a package
npm un <packageName>
// List installed packages
npm list —depth=0
// View outdated packages
npm outdated
// Update packages
npm update


Package.json
Contains information about application e.g name, authors , versions, dependencies.

npm init
npm init --yes  -> package.json with all default values.




Semantic Versioning  (SemVer)

"mongoose": "^8.2.2" // Major.Minor.Patch 
^4 -> Interested in any version with major ver 4
~4.7.0 -> Interested in any version with major ver 4 and minor ver 7

devDependencies  required only at time of dev e.g - testing 
npm i jshint --save-dev    

Uninstall a package
npm un mongoose


npm i -g npm // add -g to all the commands for packages that required globally





