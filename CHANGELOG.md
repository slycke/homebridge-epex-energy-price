# Changelog

All notable changes to this project will be documented in this file. This project uses [Semantic Versioning](https://semver.org/).

## TODO
* added feature "motion sensors" 
  * triggering during N hours (configurable) of lowest price in 24h timeslot.
  * triggering duringand M hours (configurable) of highgest price in 24h timeslot.
* remove @slycke namespace.
* only log on the hour (on price change)


## version 0.0.5
* handle incomplete data returned from the ENTSOE API, e.g.: Energy Prices 12.1.D not available for 20th January on TP	20.01.2025 12:04 https://transparency.entsoe.eu/news/widget?id=678e3a6bc3645d7db0416fbd
* only log on the hour (on price change), less spam in the logs
* removed option to set fallback price in case of errors, always use max allowed (100)
* expanded debug logs and cleaned up
* remove namespace.

## version 0.0.3

* initial release
* cleanup logging