[![Build Status](https://travis-ci.org/Neutrollized/rundeck-gcp-nodes-plugin.svg?branch=rundeck-3.2.6)](https://travis-ci.org/Neutrollized/rundeck-gcp-nodes-plugin)
[![Code Climate](https://codeclimate.com/github/Neutrollized/rundeck-gcp-nodes-plugin.png)](https://codeclimate.com/github/Neutrollized/rundeck-gcp-nodes-plugin)

# Rundeck GCP Nodes Plugin
[![GitHub release](https://img.shields.io/badge/release-v3.2.6--1-blue.svg)](https://github.com/Neutrollized/rundeck-gcp-nodes-plugin/releases)

### [CHANGELOG](https://github.com/Neutrollized/rundeck-gcp-nodes-plugin/blob/master/CHANGELOG.md)

This is a Resource Model Source plugin for [Rundeck](https://www.rundeck.org) 3.x that provides Google Cloud Platform GCE Instances as nodes for the Rundeck Server.

If you're still running Rundeck v2.x, please use one of the releases labeled v2.7.1-2 or earlier.  Think of it like "The Price is Right": you want the closest version of the plugin to what you're running without going over.


## Installation

Download from the [releases page](https://github.com/Neutrollized/rundeck-gcp-nodes-plugin/releases).

Put the `rundeck-gcp-nodes-plugin-3.2.6-1.jar` into your `$RDECK_BASE/libext` dir.

You must also authenticate the rundeck-gcp-nodes-plugin to your google cloud platform
project.
* Log into your Google Cloud Platform console, go to the *API & Services*, then go to *Credentials*
* Hit *Create Credentials*, *Service account*.  In the service account details, enter **rundeck-gcp-nodes-plugin** as the service account name.  Make sure the key type is JSON
* IAM roles required: Project `Browser` & Compute Engine `Compute Viewer`  
* After creation of the SA, you may have to go in to see the details of the account and under *Keys* hit *ADD KEY* and create new key of JSON type.
* Rename the JSON file to `rundeck-gcp-nodes-plugin-PROJECTID.json` and place it in /etc/rundeck/ (replace `PROJECTID` with your GCP project id)
* Restart Rundeck


## Requirements

You will need to add the following labels to your GCP VMs if you want more accurate/meaning full values for the OS (because unfortunately, there currently isn't that data in a standalone field/value that describes that for your VM -- just look at the output of `gcloud compute instances describe`):
* `environment` (example value: prod)
* `osfamily` (example value: linux)
* `osname` (example value: rhel7)

*** No longer a requirement from `v2.7.1-2` onward ***


## Mapping Params

By default, your connection string (denoted by the `User @ Host` column in your project nodes page) is `rundeck@hostname`, but if you want it to show IP instead you can set the `hostname.selector` attribute to `networkInterfaces` or `accessConfigs` for internal and external(NAT) IPs respectively


### Bugs/TODOs:

`Only Running Instances` in the resource config doesn't work, it will always report the nodes regardless of state.


### Disclaimer

My work is built off of the work done by [jameshcoppens](https://github.com/jameshcoppens/rundeck-gcp-nodes-plugin) and I've only branched it off to updated/maintain it seeing as there are typos in the README that has gone unaddressed and hasn't been updated for ~2+ years.  There were some functionality/features I wanted to add for my own use (and at work) so here we are... :)
