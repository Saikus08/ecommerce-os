# Política MCP y CLI

## Principio

Usar la herramienta más simple que produzca evidencia confiable y reproducible.

Orden preferido:

1. Repo/local primero.
2. CLI reproducible segundo.
3. MCP solo cuando aporta información externa, visual, actualizada o capacidades que no conviene replicar localmente.

Los MCPs son parte del harness de trabajo, no del producto E-commerce OS.

## Context7

Usar Context7 cuando:

- consultemos documentación actual de Rails, React, gems, librerías, SDKs, CLIs o APIs;
- haya dudas de configuración/versiones;
- una decisión técnica dependa de comportamiento actual del proveedor.

No usar Context7 para lógica propia del dominio, leer código del repo, debugging local simple o reemplazar tests.

## Browser automation

Usar browser automation cuando:

- se necesite exploración visual o interacción real de browser;
- haya que probar flujos UI manualmente;
- un bug dependa de DOM, navegación, foco, viewport o interacción.

No usar browser automation para scraping o extracción de datos reales sin decisión explícita.

## Integraciones externas

- Mercado Libre y Nubimetrics pueden investigarse como fuentes del producto.
- Separar capacidades públicas, autenticadas, cuenta propia, contrato/export/manual y no disponibles.
- Si un MCP/fetch/API falla o no está autenticado, declarar la falta; no inventar evidencia.
- No enviar secretos, datos reales, dumps ni exports privados a herramientas externas sin OK humano.

## Reglas de seguridad

- No leer `.env` ni secretos mediante MCP o CLI.
- No agregar nuevos MCPs, skills o herramientas sin justificar qué decisión del proyecto mejoran.
- Si una herramienta ahorra tiempo pero reduce trazabilidad o calidad, no usarla.
