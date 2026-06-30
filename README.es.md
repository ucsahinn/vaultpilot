# &#128274; VaultPilot Enterprise Vault Console - README de entrada en español

<p align="center">
  &#127760; <strong>Documentaci&#243;n:</strong>
  <a href="README.de.md"><img src="https://flagcdn.com/w20/de.png" alt="Deutsch" width="20"></a> |
  <a href="README.es.md"><img src="https://flagcdn.com/w20/es.png" alt="Espa&#241;ol" width="20"></a> |
  <a href="README.md"><img src="https://flagcdn.com/w20/gb.png" alt="English" width="20"></a> |
  <a href="README.pt-BR.md"><img src="https://flagcdn.com/w20/br.png" alt="Portugu&#234;s (Brasil)" width="20"></a> |
  <a href="README.tr.md"><img src="https://flagcdn.com/w20/tr.png" alt="T&#252;rk&#231;e" width="20"></a> |
  <a href="README.fr.md"><img src="https://flagcdn.com/w20/fr.png" alt="Fran&#231;ais" width="20"></a>
</p>

> Este archivo es una portada en español, no un resumen corto. Cubre propósito, límites, uso, validación, seguridad y publicación.
>
> README canónico en inglés: [README.md](README.md)

Centro público de documentación y releases para VaultPilot password and secrets manager.

Empieza por el README canónico si necesitas la descripción inglesa más actual. Usa esta página cuando quieras el mismo contrato operativo en español.

## Estado y señales de confianza

|Área | Detalle|
|--- | ---|
|Estado | Repositorio público: ucsahinn/vaultpilot|
|Release preparada | La documentación pública de VaultPilot 2.0.0 está preparada; no trates v2.0.0 como prueba publicada hasta que los assets finales, hashes y manifiesto estén publicados y verificados.|
|Última release pública verificada | A 30 de junio de 2026: PassMan 1.8.21 en la página GitHub Releases de ucsahinn/vaultpilot.|
|Fuente de verdad | [README canónico en inglés](README.md)|
|Usuarios | Operadores enterprise que instalan o revisan VaultPilot; administradores que verifican flujos de update, backup, AD y extensión de navegador.|
|Validación | Los índices de documentación en inglés y turco siguen accesibles; existen los screenshots y assets visuales referenciados por README.|
|Seguridad | Documenta el contrato operativo enterprise y la ruta de confianza de releases; proporciona árboles de documentación en inglés/turco y artículos KB.|

## Qué es este repositorio

- Hub público de documentación para VaultPilot Enterprise Vault Console.
- Puerta de release y verificación para usuarios que revisan assets públicos.
- Mapa documental para quickstart de admin, instalación en Windows Server, AD agent, backups, extensión del navegador, sharing, update center y troubleshooting.
- Superficie pública segura para explicar el producto sin exponer código privado ni datos de vault de clientes.

## Qué no es

- No es el repositorio privado del código de la aplicación.
- No es un vault, almacén de credenciales ni tenant de cliente.
- No es lugar para signing keys, secretos de licencia, update keys ni paquetes privados de soporte.
- No sustituye la validación de assets descargados de una release.

## Para quién es

- Operadores enterprise que instalan o revisan VaultPilot.
- Administradores que verifican flujos de update, backup, AD y extensión de navegador.
- Revisores de seguridad que verifican el trust model y la validación de release.
- Usuarios de soporte que buscan troubleshooting público y guía de evidence pack.

## Inicio rápido

1. Clona o actualiza el repositorio.
2. Lee README, seguridad y el mapa de documentación.
3. Ejecuta las validaciones adecuadas.
4. Prepara solo los archivos cambiados de forma explícita.
5. Antes de push o release, revisa remoto, secretos y enlaces otra vez.

## Guía de decisión

- Necesitas overview -> docs/en/overview.md o docs/tr/overview.md.
- Necesitas instalación -> docs/en/install-windows-server.md o docs/tr/install-windows-server.md.
- Necesitas verificación de release -> docs/en/release-asset-verification.md o docs/tr/release-asset-verification.md.
- Necesitas troubleshooting -> docs/en/troubleshooting.md, docs/tr/troubleshooting.md o artículos KB.
- Necesitas postura pública de seguridad -> docs/en/security-and-trust-model.md, docs/tr/security-and-trust-model.md y SECURITY.md.

## Mapa del repositorio

|Ruta | Por qué importa|
|--- | ---|
|`docs/en/` y `docs/tr/` | documentación principal del producto|
|`kb/en/` y `kb/tr/` | artículos KB de troubleshooting|
|[assets/screenshots/](assets/screenshots/) | screenshots públicos|
|[assets/visuals/](assets/visuals/) | diagramas SVG públicos|
|[RELEASES.md](RELEASES.md) | notas de release y assets|
|[PRIVACY.md](PRIVACY.md) | política de privacidad|
|[scripts/validate-docs.mjs](scripts/validate-docs.mjs) | validador de documentación|
|[SECURITY.md](SECURITY.md) | política de disclosure de seguridad|

## Flujo de trabajo

1. Actualiza ambos árboles de idioma cuando cambie el contrato del producto.
2. Mantén release notes y guía de verificación alineadas con los assets públicos reales.
3. Valida documentos y enlaces antes del commit.
4. Ejecuta secret scan antes del push.
5. Verifica remote HEAD y rendering de GitHub release/page después de publicar.

## Comandos y validación

Ejecuta estos comandos solo después de clonar el repositorio y entender qué escriben o verifican.

```powershell
npm run validate
node scripts/validate-docs.mjs
git diff --check
gitleaks dir . --no-banner --redact
```

## Lista de verificación

- Los índices de documentación en inglés y turco son accesibles.
- Existen los screenshots y assets visuales referenciados por README.
- No aparecen datos privados de vault, nombres de clientes, licencias, signing keys ni update secrets.
- El texto de verificación de release coincide con RELEASES.md.
- Remote HEAD queda verificado después del push.

## Límite de seguridad

- Documenta el contrato operativo enterprise y la ruta de confianza de releases.
- Proporciona árboles de documentación en inglés y turco más artículos KB.
- Mantiene documentados los release assets y la update trust chain.
- Incluye screenshots, assets visuales y scripts de validación para docs públicas.

Regla public-safe: no agregues secretos, tokens, cookies, private keys, prompts privados, datos de clientes, archivos auth locales, logs generados, archivos comprimidos ni build outputs salvo que el README canónico diga explícitamente que pertenecen al repo público.

## Higiene de release y publicación

- Publica instaladores y archivos comprimidos mediante GitHub Releases, no mediante commits de código.
- No commitees build output, paquetes privados de soporte ni signing material.
- Actualiza la documentación antes de anunciar estado de release pública.
- Revisa nombres de assets, versiones y remote HEAD después de push/release.

## Mantenimiento

- Mantén este README localizado alineado con README.md cuando cambie el contrato del repo.
- Prefiere enlaces verificables del repo frente a claims de marketing.
- No inventes comandos de instalación, métricas, usuarios, releases ni promesas de soporte.
- If a command is version-sensitive, re-check it before documenting it.
- When a localized file cannot be updated fully, leave a clear note instead of a partial translation.

## Ruta de contribución

- Abre un cambio enfocado sobre el conjunto mínimo de archivos.
- Lee AGENTS.md o CONTRIBUTING.md antes de editar cuando existan.
- Ejecuta los comandos de validación del repo indicados arriba.
- Revisa explícitamente los staged diffs antes del commit.
- Usa canales de security disclosure, no issues públicos, para reportes sensibles.

## Definición de terminado

Terminado significa: contenido completo, enlaces correctos, límites de seguridad claros, validación ejecutada, Git limpio y remote HEAD verificado después del push.

|Recomendación | Por qué importa|
|--- | ---|
|Contenido | Centro público de documentación y releases para VaultPilot password and secrets manager.|
|Enlaces | Todos los archivos locales referenciados deben existir y resolverse desde la raíz del repositorio.|
|Seguridad | No deben aparecer datos privados de vault, nombres de clientes, licencias, signing keys ni update secrets.|
|Verification | Valida estructura, enlaces, Markdown, secretos, scripts relevantes y remote HEAD antes de afirmar que algo está publicado.|
|Remote | Después del push, compara local HEAD con origin/main y GitHub remote HEAD.|

## Enlaces importantes

|Ruta | Por qué importa|
|--- | ---|
|[Canonical README](README.md) | README.md|
|[English docs](docs/en/README.md) | docs/en/README.md|
|[Turkish docs](docs/tr/README.md) | docs/tr/README.md|
|[English knowledge base](kb/en/README.md) | kb/en/README.md|
|[Turkish knowledge base](kb/tr/README.md) | kb/tr/README.md|
|[Release notes](RELEASES.md) | RELEASES.md|
|[Privacy](PRIVACY.md) | PRIVACY.md|
|[Security policy](SECURITY.md) | SECURITY.md|
