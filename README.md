
<p align="center">
    <a href="https://thomas-ferney.fr" target="_blank">
        <img src="https://thomas-ferney.fr/images/github-ban-dev-kit.png" />
    </a>
</p>

<h1 align="center">
    PHP dev-kit
</h1>

![Quality Assurance](https://github.com/antiseptikk/dev-kit/workflows/Quality%20Assurance/badge.svg?branch=main)
![Packagist Downloads](https://img.shields.io/packagist/dt/antiseptikk/dev-kit?label=Packagist)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/antiseptikk/dev-kit?label=Last%20release)

Installation
--------------------

1. Install this package:

    ```bash
    $ composer require --dev antiseptikk/dev-kit
    ```
    
2. Create a file named `ecs.php` in the root directory of your project.

   ```php
   <?php

   declare(strict_types=1);
   
   use Symfony\Component\DependencyInjection\Loader\Configurator\ContainerConfigurator;
   use Symplify\EasyCodingStandard\ValueObject\Option;
   
   return static function (ContainerConfigurator $containerConfigurator): void
   {
       $containerConfigurator->import(__DIR__.'/vendor/antiseptikk/dev-kit/ecs.php');
   
       $parameters = $containerConfigurator->parameters();
       $parameters->set(Option::LINE_ENDING, "\n");
   };

   ```

3. Creates a file named `psalm.xml` in the root directory of your project.

   ```xml
   <?xml version="1.0"?>
   <psalm
      errorLevel="1"
      resolveFromConfigFile="true"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns="https://getpsalm.org/schema/config"
      xsi:schemaLocation="https://getpsalm.org/schema/config vendor/vimeo/psalm/config.xsd"
   >
       <projectFiles>
           <directory name="src" />
           <ignoreFiles>
               <directory name="vendor" />
           </ignoreFiles>
       </projectFiles>
   </psalm>
   ```

Usage
--------------------

**Static Analysis**

-  Psalm
      
   ```bash
   vendor/bin/psalm
   ```

- PHPStan

   ```bash
   vendor/bin/phpstan analyse src
   ```

   By default, PHPStan runs only the most basic checks. Head to [Rule Levels](https://phpstan.org/user-guide/rule-levels) to learn how to turn on stricter checks.

**Coding Standard**

```bash
vendor/bin/ecs check src
```
