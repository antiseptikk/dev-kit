<h1 align="center">
    PHP dev-kit
</h1>

![Quality Assurance](https://github.com/antiseptikk/dev-kit/workflows/Quality%20Assurance/badge.svg?branch=main)

Installation & usage
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
