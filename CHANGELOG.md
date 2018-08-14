# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## Unreleased

### Changed

* Refactored name(space) of `\Swis\JsonApi\Client\Items\JenssegersItem` to `\Swis\JsonApi\Client\Item` as we only have one item now.

### Removed

* `EloquentItem` is removed because it had some limitations which could not be fixed without being too opinionated.
* `NullItem` is removed in favor of simply `null`. This item was only used internally so this should not affect you.

## [0.7.5] - 2018-07-04

### Fixed

* Do not add attributes to item when empty [#20](https://github.com/swisnl/json-api-client/pull/20)

## [0.7.4] - 2018-06-20

### Fixed

* Reverted the behaviour of handling duplicate items back to what it was in <= 0.7.2. This change in behaviour was introduced in the last performance update (0.7.3). N.B. This change will only affect you if you parse documents with duplicate items, which violates the JSON API spec.

## [0.7.3] - 2018-06-01

### Changed

* Improved performance of JsonApi\Hydrator [#18](https://github.com/swisnl/json-api-client/pull/18)

## [0.7.2] - 2018-05-17

### Fixed

* Fixed building the request with headers

## [0.7.1] - 2018-05-16

### Fixed

* Corrected the path to the config file

## [0.7.0] - 2018-05-11

### Changed

#### Update art4/json-api-client to latest version, this changes some of the returned classes.

The following classes are changed in some arguments and some method returns, if you extended or directly use `\Swis\JsonApi\Client\JsonApi\Hydrator` or `\Swis\JsonApi\Client\JsonApi\Parser` please check your code.

```
\Art4\JsonApiClient\Resource\CollectionInterface -> \Art4\JsonApiClient\ResourceCollectionInterface
\Art4\JsonApiClient\Resource\ItemInterface -> \Art4\JsonApiClient\ResourceItemInterface
\Art4\JsonApiClient\Resource\IdentifierCollection -> \Art4\JsonApiClient\ResourceIdentifierCollection
\Art4\JsonApiClient\Resource\Identifier -> \Art4\JsonApiClient\ResourceIdentifier
\Art4\JsonApiClient\Resource\Collection -> \Art4\JsonApiClient\ResourceCollection
```

## [0.6.0] - 2018-03-06

### Added

* Added CHANGELOG.md

### Changed

* Changed package name in composer.json 
* Changed autodiscovery service provider in composer.json 

## [0.5.0] - 2018-03-06

### Added 

* Added a proper README with instructions.

### Changed

* Updated namespace to `Swis\JsonApi\Client` for consistency.
* Split service provider binds so overwriting is easier.

### Removed

* Extracted fixtures client to  [swisnl/php-http-fixture-client](https://github.com/swisnl/php-http-fixture-client) and [swisnl/guzzle-fixture-handler](https://github.com/swisnl/guzzle-fixture-handler)
* Removed resources as it was redundant.

## [0.4.0] - 2018-01-16

### Changed

Refactored to use [php-http/httpplug](http://docs.php-http.org/en/latest/index.html) instead of Guzzle so the library doesn't depend on a specific http client implementation.

This does change how you customize the ServiceProvider, just include an adapter for the client you want to use and the library uses [autodiscovery](http://docs.php-http.org/en/latest/discovery.html) to find the correct [adapter/client](http://docs.php-http.org/en/latest/clients.html). It also uses a [MessageFactory](http://docs.php-http.org/en/latest/message/message-factory.html) for creating Requests and Response objects.

So for example, if you want to use Guzzle, just `composer require php-http/guzzle6-adapter`, and all should be swell.

In order to have a working mock client for testing you now need to include [php-http/mock-client](http://docs.php-http.org/en/latest/clients/mock-client.html). Which is an easy way to mock requests.
