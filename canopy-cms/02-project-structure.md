---
author:
    name: Jan Valo
order: 90
---
# Project Structure

The CMS base has a basic Laravel project structure that is extended by the packages that reside 
in the ```/platfrom``` folder.

The platform folder includes 4 types of main packages:

- ```/core``` - includes critical CMS modules that are required to run the CMS
- ```/packages``` - includes modules that provide base features accessible in the CMS and the frontend
- ```/plugins``` - includes non-critical/optional plugins that further extend the functionality of the CMS (Oplly functionality is part of that)
- ```/themes``` - includes the code used by front end, any custom logic used in the themes


## Core

This is a local dependency including the core framework for the Canopy CMS.

!!!
Currently, the core is part of the main repository, that will change in the future where it will become a dependency
!!!

## Packages

Similarly to the core, packages are individual dependencies that can be extracted as dependencies. They are individual laravel packages.

## Plugins

Plugins are packages that are loaded using custom configuration that is merged and autoloaded with the main composer in the project root
