# Cloud Foundry BOSH Deployment
In this repository proposes a standard way of maintaining BOSH deployment manifests.
By using modular templates combined with a mechanism for referencing upstream templates.

> Work in progress feedback appreciated

## Design Goals
Enabling BOSH operators to share common configuration between different deployments.
For example having a `QA` and `production` deployment for which only networking differs.

## Installation
Before you start make sure ruby, bundler and spiff are available on your system.
Instructions for installing spiff can found (here)[http://spiff.cfapps.io].

```
git clone https://github.com/rkoster/cf-boshdeployment.git
cd cf-boshdeployment
bundle install
```

## Usage
The BOSH plugin enabling the improved deployments work-flow,
extends some of the build in commands with support for `Better Deployments`.

**Set deployment**
Sets the current deployment. Will search in `./deployments`.
```
bosh deployment cf-warden
```

**Prepare deployment**
Resolves upstream templates (via releases).
Resolves and uploads releases/stemcells.
```
bosh prepare deployment
```

**Deploy**
Merges the specified templates into one deployment manifests using spiff.
And uses this file to initiate a `deploy`.
```
bosh deploy
```

### Deployment file
A `Better Deployments` deployment file has the following information:

**name:**
The name of your deployment

**director_uuid:**
The director_uuid of the targeted BOSH director

**releases:**
Array of releases used for resolving upstream templates

**meta:**
The meta hash is the last file merged into the final deployment file.
It can be used to define properties deployment specific properties.
