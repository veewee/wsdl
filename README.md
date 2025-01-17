# WSDL

This package provides tools and helpers for dealing with WSDLs.


## Installation

```bash
composer require php-soap/wsdl
```

## WSDL Loader

A WSDL loader is able to load the contents of a WSDL file.

### Psr18Loader

For loading WSDL's, you might want to use a PSR-18 client to do the hard HTTP work.
You'll have to include the [php-soap/psr18-transport](https://github.com/php-soap/psr18-transport/#psr18loader) in order to use this loader:

```sh
composer require php-soap/psr18-transport
```

```php
use Http\Client\Common\PluginClient;
use Soap\Psr18Transport\Wsdl\Psr18Loader;

$loader = Psr18Loader::createForClient(
    $wsdlClient = new PluginClient(
        $psr18Client,
        ...$middleware
    )
);

$contents = $loader('http://some.wsdl');
```


### StreamWrapperLoader

Loads the content of a WSDL by using any of the enabled [stream wrappers](https://www.php.net/manual/en/wrappers.php).
It can either be a file, http, ...

```php
use Soap\Wsdl\Loader\StreamWrapperLoader;

$loader = new StreamWrapperLoader(
    stream_context_create([
        'http' => [
            'method' => 'GET',
            'header'=>"User-Agent: my loader\r\n",
        ],        
    ])
);
$contents = $loader($wsdl);
```
