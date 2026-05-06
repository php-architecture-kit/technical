# php-architecture-kit/technical

Technical classes, interfaces and utilities for PHP applications. A lightweight, zero-dependency utility library providing common low-level helpers.

## Features

- **`Assert`** - Validation utilities with customizable exception types
- **`ArrayTransformation`** - Array manipulation helpers
- **No dependencies** - Only requires PHP 7.4+
- **Framework-agnostic** - Works with any PHP project

## Installation

```bash
composer require php-architecture-kit/technical
```

## Quick Start

```php
use PhpArchitecture\Technical\Assert;
use PhpArchitecture\Technical\ArrayTransformation;

// Assert all items are instances of a given class
Assert::eachInstanceOf($items, SomeClass::class);

// Assert all items are strings
Assert::eachString($tags);

// Index an array by a derived key
$indexed = ArrayTransformation::indexBy($items, fn($item) => $item->getId());
```

## API Reference

### Assert

| Method | Description |
|--------|-------------|
| `eachInstanceOf(array $items, string $class, string $exceptionClass, int $displayLimit)` | Throws if any item is not an instance of `$class` |
| `eachString(array $items, string $exceptionClass, int $displayLimit)` | Throws if any item is not a string |

Both methods accept a custom `$exceptionClass` (must implement `Throwable`, defaults to `InvalidArgumentException`) and `$displayLimit` to cap how many invalid items appear in the message.

```php
use PhpArchitecture\Technical\Assert;
use RuntimeException;

Assert::eachInstanceOf($commands, Command::class, RuntimeException::class);
Assert::eachString($names, \DomainException::class, displayLimit: 3);
```

### ArrayTransformation

| Method | Description |
|--------|-------------|
| `indexBy(array $items, callable $key): array` | Re-keys an array using the return value of `$key($item)` |

```php
use PhpArchitecture\Technical\ArrayTransformation;

$users = [new User('alice'), new User('bob')];
$byName = ArrayTransformation::indexBy($users, fn(User $u) => $u->getName());
// ['alice' => User, 'bob' => User]
```

## License

MIT
