- `sudo apt-get update && sudo apt-get install yarn` - installs yarn
- `yarn help` - gives help for every command
- `yarn init` - initializes the packages name
- `yarn config set init-license ISC`- change the default license when init
- `yarn config get init-license`- get the license
- `yarn config delete init-license` - remove the changed settings (ISC)
- `yarn licenses list`- list licenses of all packages
- `yarn pack`- zip all packages

## Packages:

- `yarn add lodash` - install packages
- `yarn install`- installs based on packages.json
- `yarn remove lodash`-remove lodash package
- `yarn outdated`- show uoutdated packages
- `yarn upgrade lodash --latest`- upgrade the package
- `yarn global add nodemon` - install globally
- `yarn global remove nodemon`- remove package globally
- `yarn list`- lists packages and dependencies
- `yarn list --depth=0` - lists only top layer, no dependencies
- `yarn list --pattern gulp`- list only dependencies for gulp
- `yarn add gulp -D`- install as dev dependency

## Lock file

- `yarn check`- checks that lock matches the packages
- `yarn import`- create lock file

## Scripts

- `yarn run dev` - same as npm run

## Cache

- `yarn cache list`- list packages in cache
- `yarn cache clean`- clear cache



