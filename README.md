# php-cs

The file [.php_cs.dist](.php_cs.dist) contains all rules which apply to the coding standards for rebuy. You can find the description of these rules in the [PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer/blob/master/README.rst) repository. 

## Examples

### Travis code style check

```bash
vendor/bin/php-cs-fixer fix --config=vendor/rebuy/php-cs/.php_cs.dist -v --dry-run --using-cache=no `git diff --name-only --diff-filter=ACMRTUXB $TRAVIS_COMMIT_RANGE`
```

**Note:** If you define the path in your own `.php_cs.dist` file, you might want use `--path-mode intersection`. 

### Fixing code styles

```bash
vendor/bin/php-cs-fixer fix --config=vendor/rebuy/php-cs/.php_cs.dist yourDirectory/`
```

### Fixing code styles from $yourBranch to master

```bash
vendor/bin/php-cs-fixer fix --config=.php_cs.dist `git diff --name-only --diff-filter=ACMRTUXB master`
```

## Overwriting rules

There might be some scenarios where you have to adjust the rules defined here, in this case you can include the base file and extend it to your needs:

```php
<?php

$config = include 'vendor/rebuy/php-cs/.php_cs.dist';

$currentRules = $config->getRules();
$newRules = [
    'phpdoc_no_empty_return' => false,
];

$config->setRules(array_merge($currentRules, $newRules));
```
