
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
   
   return static function (ECSConfig $config): void {
       $config->import(__DIR__.'/vendor/antiseptikk/dev-kit/ecs.php');
   
       $config->parallel();
       $config->paths(['src', 'tests']);
       $config->skip([
            InlineDocCommentDeclarationSniff::class . '.MissingVariable',
            InlineDocCommentDeclarationSniff::class . '.NoAssignment',
            VisibilityRequiredFixer::class => ['*Spec.php'],
            '**/var/*',
       ]);
       $config->ruleWithConfiguration(PhpdocSeparationFixer::class, ['groups' => [['Given', 'When', 'Then']]]);
       $config->ruleWithConfiguration(OrderedTypesFixer::class, ['null_adjustment' => 'always_last']);
       $config->ruleWithConfiguration(NullableTypeDeclarationForDefaultNullValueFixer::class, ['use_nullable_type_declaration' => true]);
   };

  ```

Usage
--------------------

**Coding Standard**

```bash
vendor/bin/ecs check src
```
