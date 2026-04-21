---
description: pgvector extension health check for Spatie Laravel Health — version detection, configurable strictness
---

# healthcheck-pgvector

pgvector extension health check for `spatie/laravel-health`. Verifies the `vector` PostgreSQL extension is installed and active.

## Namespace

`IllumaLaw\HealthCheckPgvector`

## Key Check

- `PgvectorExtensionCheck` — queries `pg_extension` to confirm `vector` is installed and reports its version

## Registration

```php
use IllumaLaw\HealthCheckPgvector\PgvectorExtensionCheck;
use Spatie\Health\Facades\Health;

Health::checks([
    PgvectorExtensionCheck::new()
        ->required(true), // true = FAIL if missing; false = WARNING
]);
```

## Config

Publish: `php artisan vendor:publish --tag="healthcheck-pgvector-config"`

Options in `config/healthcheck-pgvector.php`:
- `required`: (bool) Global default for strictness.

## Notes

- Reports the pgvector version string in health meta data.
- Safely handles DB connection errors — returns `failed` with the exception message rather than crashing the health suite.
- Use in test environments that have a real PostgreSQL instance. For SQLite-based CI, skip this check via `->skipOnEnvironments(['testing'])`.
