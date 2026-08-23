# Entorno local

## Prerrequisitos

- Ruby/Rails según `Gemfile`.
- Node/npm para React integrado y build JavaScript.
- PostgreSQL local, actualmente esperado vía variables `PGHOST`, `PGPORT`, `PGUSER`, `PGPASSWORD`.
- No leer ni commitear `.env`.

## Comandos canónicos

```bash
bundle install
npm install
bin/rails db:prepare
bundle exec rspec
bin/rubocop
bin/brakeman --quiet --no-pager --exit-on-warn --exit-on-error
npm run build
bin/verify
```

## Datos locales

- Usar datos sintéticos por defecto.
- Datos reales, credenciales, exports privados o APIs autenticadas requieren OK humano explícito.
- `db:reset`, borrados y migraciones destructivas requieren OK humano.

## Integraciones

- Mercado Libre y Nubimetrics son objetivos de producto, pero sus capacidades deben verificarse antes de diseñar ingestion definitivo.
- No scraping sin decisión explícita.
- No cloud/deploy desde entorno local sin gate humano.
