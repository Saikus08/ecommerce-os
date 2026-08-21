# Code Quality — E-commerce OS

## Principios

- Rails idiomático primero.
- ActiveRecord antes que repositorios artificiales.
- Servicios solo cuando reduzcan complejidad real.
- Boundaries por necesidad, no por ceremonial.
- Código testeable y simple.
- Preferir nombres del negocio sobre nombres técnicos genéricos.
- No usar atajos que degraden mantenibilidad, seguridad o claridad para ahorrar tiempo en el corto plazo.
- Si una práctica rápida compite con una práctica correcta, elegir la correcta o parar y pedir decisión.

## Configuration

- No commitear secretos.
- No leer `.env`.
- Preferir variables explícitas por responsabilidad (`POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_HOST`) antes que URLs globales ambiguas en desarrollo.
- `DATABASE_URL` queda reservado para entornos donde la plataforma lo provee, como Railway/production.

## Data quality

- No mezclar hechos observados con cálculos o inferencias.
- Guardar datos normalizados cuando se consultan/calculan.
- Guardar `raw_payload` JSONB para respuestas externas importantes.
- Historizar datos cambiantes mediante snapshots.
- Usar constraints e índices para idempotencia.

## Integraciones

- Clients HTTP concretos por proveedor.
- Importers/mappers convierten respuestas externas en modelos propios.
- Jobs orquestan sincronización y retries.
- No esconder diferencias entre proveedores detrás de abstracciones prematuras.
- No scraping frágil sin aprobación explícita.

## Testing

- Cálculos determinísticos deben tener tests.
- Importers deben tener fixtures/respuestas representativas.
- Jobs deben ser idempotentes y testeables.
- Evitar tests acoplados a detalles irrelevantes de UI.
