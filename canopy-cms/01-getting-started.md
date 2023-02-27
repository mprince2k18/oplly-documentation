---
author:
    name: Jan Valo
order: 100
---
# Getting Started

Canopy is a custom-built Content Management System (CMS) developed 
using Laravel PHP framework. 

!!!contrast
The Oplly platform and elements like Website and API were developed as 
an extension of the existing eCommerce plugin that was refactored to 
include functionality required for Oplly project. These pages aim to describe
components in more detail to help understand the structure to make development 
easier.
!!!

## System Requirements

 - Nginx web server
 - PHP >= 7.3 with the following modules:
   - BCMath
   - Ctype
   - Fileinfo
   - JSON
   - Mbstring
   - OpenSSL
   - PDO
   - Tokenizer
   - XML
   - Re_write server
   - Curl
 - MySQL/MariaDB

## Installation and Setup

The entire development environment and code repository are containerized using ```Docker``` to include production-like 
configuration.

The fastest way to setup the project is to pull the devststack repository to a folder next to the base repository.
