# Get location info by IP address

This extension is based on Sypex Geo Database [https://sypexgeo.net/](https://sypexgeo.net/).

The language requirements: PHP version >=5.3.0

The database signatures release date:  June 30, 2021

## Installation & Set Up

To get the latest version via Composer:
```shell
composer require hostbrook/sypex-geo
```

## Upgrading

Whenever there is a new release, then from the command line in your **project root**:

```shell
composer update
```

## Basic Usage ( with city database example )

```shell
use \HostBrook\SypexGeo\SypexGeo;

...

// Create an object with the required database:
$SxGeo = new SypexGeo('SxGeoCity.dat');

// get your IP address:
$userIP = $_SERVER['REMOTE_ADDR'];

var_export($SxGeo->getCityFull($userIP)); // Full info about a city
var_export($SxGeo->get($userIP));         // Short info aboy a city

```

## Basic Usage ( with country database example )

```shell
use \HostBrook\SypexGeo\SypexGeo;

...

// Create an object with the required database:
$SxGeo = new SypexGeo('SxGeo.dat');

// get your IP address:
$userIP = $_SERVER['REMOTE_ADDR'];

$userCountry = $SxGeo->getCountry($userIP); // Country code
var_export($SxGeo->get($userIP));           // Country code

```
