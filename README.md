# Sypex Geo - Get location info by IP address

This extension is based on [Sypex Geo free databases](https://sypexgeo.net/) and lets you get the next info by IP address:

- Country code by ISO 3166-2
- Region code by ISO 3166-2
- City name
- Region name
- Country name
- City Latitude/Longitude data

The language requirements: PHP version >=5.3.0

The databases release date: **August 18, 2023**

## PHP frameworks integration

You have to use Composer to add Sypex Geo to your project based on PHP frameworks like Laravel, Yii, etc.

### Installation

To get the latest version via Composer:

```shell
composer require hostbrook/sypex-geo
```

### Upgrading

Whenever there is a new release, then from the command line in your **project root**:

```shell
composer update
```

## Usage

There are two different databases that come with the extension SxGeo.dat (country database, around 814kb) and SxGeoCity.dat (city database, around 39Mb).
The city database contains the same country info from the country database, but heavier. So, do not use the city database if you need to get just a country code.

### Usage with country database

If you need to get just a 2-symbol country code by ISO 3166-2:

```shell
// Add namespace at the beginning of the file:
use HostBrook\SypexGeo\SypexGeo;

...

// Create an object with the country database in the argument.
// Note: By default, the country database (SxGeo.dat) is used, so it can be skipped:
$SxGeo = new SypexGeo();

// get your IP address, for example:
$userIP = $_SERVER['REMOTE_ADDR'];

// Option 1 to get the ISO country code:
$userCountry = $SxGeo->getCountry($userIP); // returns string, the country code
// Option 2  is a short equialent for country database only:
$userCountry = $SxGeo->get($userIP);        // returns string, the country code

```

### Usage with city database

```shell
// Add namespace at the beginning of the file:
use HostBrook\SypexGeo\SypexGeo;

...

// Create an object with the city database in the argument:
$SxGeo = new SypexGeo('SxGeoCity.dat');

// Get your IP address, like an example:
$userIP = $_SERVER['REMOTE_ADDR'];

// Option 1 to get the city info:
var_dump( $SxGeo->getCity($userIP) );     // Array, the short info about a city
// Option 2 is a short equialent for the city database only:
var_dump( $SxGeo->get($userIP) );         // Array, the short info about a city

// City full info with timezone and region:
var_dump( $SxGeo->getCityFull($userIP) ); // Full info about a city

```

Example Data:

```shell
[
    'city' => [
        'id' => 524901,
        'lat' => 55.75222,
        'lon' => 37.61556,
        'name_ru' => 'Москва',
        'name_en' => 'Moscow',
        'okato' => '45',
    ],
    'region' => [
        'id' => 524894,
        'lat' => 55.76,
        'lon' => 37.61,
        'name_ru' => 'Москва',
        'name_en' => 'Moskva',
        'iso' => 'RU-MOW',
        'timezone' => 'Europe/Moscow',
        'okato' => '45',
    ],
    'country' => [
        'id' => 185,
        'iso' => 'RU',
        'continent' => 'EU',
        'lat' => 60,
        'lon' => 100,
        'name_ru' => 'Россия',
        'name_en' => 'Russia',
        'timezone' => 'Europe/Moscow',
    ],
];

```

### Addition parameters

If you need to work with multiple requests to a database, you can add two parameters during object creating to use caching and packet mode:

```shell
$SxGeo = new SypexGeo('SxGeoCity.dat', SXGEO_BATCH | SXGEO_MEMORY);
```

it can increase a response speed.
