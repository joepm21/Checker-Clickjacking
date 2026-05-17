# PVGUARD - Checker Clickjacking v2.0.0

**PVGUARD - Checker Clickjacking** es una herramienta escrita en Python para validar si una página web puede ser vulnerable a **Clickjacking**.

La herramienta analiza cabeceras de seguridad, verifica si existen controles contra carga en `iframe` y genera automáticamente una **PoC HTML interactiva** para demostrar el riesgo de forma visual en entornos autorizados.

---

## Descripción

Clickjacking es una técnica de ataque donde un sitio legítimo puede ser cargado dentro de un `iframe` y superpuesto sobre una interfaz falsa para engañar al usuario y lograr que realice acciones no intencionadas.

Esta herramienta permite identificar configuraciones inseguras relacionadas con Clickjacking mediante la revisión de cabeceras HTTP como:

- `X-Frame-Options`
- `Content-Security-Policy`
- Directiva `frame-ancestors`

Cuando no se detectan protecciones adecuadas, PVGUARD genera una PoC HTML que permite visualizar el escenario de ataque mediante una capa señuelo y un `iframe` del sitio objetivo.

---

## Características principales

- Verificación de vulnerabilidad a Clickjacking.
- Análisis de cabeceras HTTP de seguridad.
- Validación de `X-Frame-Options`.
- Validación de `Content-Security-Policy` con `frame-ancestors`.
- Generación automática de PoC HTML.
- PoC visual e interactiva en navegador.
- Apertura automática de la PoC generada.
- Soporte para múltiples plantillas de señuelo.
- Control de opacidad del `iframe`.
- Modo de solo verificación con `--check-only`.
- Modo para omitir verificación de headers con `--no-check`.
- Modo para no abrir automáticamente el navegador con `--no-open`.
- Normalización automática de URL si no se indica `http://` o `https://`.
- Banner actualizado con identidad PVGUARD.

---

## Requisitos

- Python 3
- Linux, Kali Linux o sistema compatible
- Conexión a internet para analizar URLs externas

La herramienta utiliza librerías estándar de Python, por lo que no requiere instalación adicional de dependencias externas.

Módulos usados:

- `argparse`
- `html`
- `os`
- `ssl`
- `sys`
- `urllib`
- `webbrowser`
- `datetime`
- `pathlib`

---

## Instalación

Clonar el repositorio:

```bash
git clone https://github.com/joepm21/Checker-Clickjacking.git
```

Entrar al directorio:

```bash
cd Checker-Clickjacking
```

Dar permisos de ejecución:

```bash
chmod +x checker_clickjacking
```

---

## Uso básico

Ejecutar análisis y generar PoC:

```bash
./checker_clickjacking -u https://ejemplo.com
```

También puedes ejecutarlo con Python:

```bash
python3 checker_clickjacking -u https://ejemplo.com
```

Si la URL no incluye protocolo, la herramienta agregará automáticamente `http://`.

Ejemplo:

```bash
./checker_clickjacking -u ejemplo.com
```

---

## Opciones disponibles

```bash
./checker_clickjacking -h
```

| Opción | Descripción |
|---|---|
| `-u`, `--url` | URL objetivo a analizar |
| `-o`, `--output` | Nombre del archivo HTML de salida |
| `--template` | Plantilla inicial para la PoC |
| `--list-templates` | Lista las plantillas disponibles |
| `--check-only` | Solo verifica cabeceras, no genera PoC |
| `--opacity` | Define la opacidad inicial del iframe entre `0.0` y `1.0` |
| `--no-check` | Omite la verificación de cabeceras |
| `--no-open` | No abre automáticamente la PoC generada |

---

## Ejemplos de uso

### Analizar una URL y generar PoC

```bash
./checker_clickjacking -u https://ejemplo.com
```

### Generar PoC con nombre personalizado

```bash
./checker_clickjacking -u https://ejemplo.com -o poc_clickjacking.html
```

### Solo verificar cabeceras de seguridad

```bash
./checker_clickjacking -u https://ejemplo.com --check-only
```

### Generar PoC usando una plantilla específica

```bash
./checker_clickjacking -u https://ejemplo.com --template login
```

### Generar PoC con opacidad inicial del iframe

```bash
./checker_clickjacking -u https://ejemplo.com --template pago --opacity 0.5
```

### Generar PoC sin abrir el navegador automáticamente

```bash
./checker_clickjacking -u https://ejemplo.com --no-open
```

### Saltar verificación de headers y generar PoC directamente

```bash
./checker_clickjacking -u https://ejemplo.com --no-check
```

### Listar plantillas disponibles

```bash
./checker_clickjacking --list-templates
```

---

## Plantillas disponibles

PVGUARD v2.0.0 incluye múltiples plantillas de señuelo para la PoC:

| Template | Descripción |
|---|---|
| `premio` | Premio / Sorteo |
| `login` | Inicio de sesión |
| `pago` | Confirmación de pago |
| `actualizacion` | Actualización requerida |
| `newsletter` | Newsletter / Suscripción |
| `encuesta` | Encuesta rápida |
| `cupon` | Cupón descuento |
| `cloud` | Almacenamiento cloud |
| `soporte` | Ticket de soporte |
| `documento` | Firma de documento |
| `delivery` | Seguimiento delivery |
| `calendario` | Invitación calendario |
| `wifi` | Portal WiFi |
| `banca` | Verificación bancaria |
| `mfa` | Código MFA |
| `vpn` | Portal VPN |
| `capacitacion` | Capacitación interna |
| `inventario` | Inventario TI |
| `alerta` | Alerta de seguridad |
| `recompensa` | Programa de recompensas |

Ejemplo:

```bash
./checker_clickjacking -u https://ejemplo.com --template login
```

---

## Ejemplo de salida en consola

<img width="962" height="603" alt="image" src="https://github.com/user-attachments/assets/ec00630f-f8f5-4c69-8d27-52f917cea8b0" />

---

## Archivo generado

Por defecto, la herramienta genera:

```bash
checker_clickjacking.html
```

Este archivo contiene:

- Información general del objetivo.
- Resultado del análisis.
- Estado de cabeceras HTTP.
- Recomendaciones de remediación.
- Demo interactiva de Clickjacking.
- Selector de plantillas.
- Control de opacidad del iframe.
- Botón para mostrar u ocultar el iframe.

---

## Validaciones realizadas

La herramienta revisa si la aplicación cuenta con mecanismos de defensa contra Clickjacking.

### X-Frame-Options

Se considera protección válida si se encuentra:

```http
X-Frame-Options: DENY
```

o:

```http
X-Frame-Options: SAMEORIGIN
```

### Content-Security-Policy

Se revisa si la política CSP contiene la directiva:

```http
frame-ancestors
```

Ejemplos seguros:

```http
Content-Security-Policy: frame-ancestors 'none';
```

```http
Content-Security-Policy: frame-ancestors 'self';
```

---

## Recomendaciones de remediación

Para mitigar Clickjacking, se recomienda implementar una de las siguientes configuraciones.

### Bloquear completamente el uso en iframes

```http
X-Frame-Options: DENY
```

o:

```http
Content-Security-Policy: frame-ancestors 'none';
```

### Permitir iframes solo desde el mismo origen

```http
X-Frame-Options: SAMEORIGIN
```

o:

```http
Content-Security-Policy: frame-ancestors 'self';
```

### Configuración recomendada moderna

```http
Content-Security-Policy: frame-ancestors 'none';
```

La directiva `frame-ancestors` es la opción más flexible y moderna para controlar qué sitios pueden embeber una aplicación dentro de un frame.

---

## Cambios en v2.0.0

- Generación automática de PoC HTML mejorada.
- Interfaz HTML más profesional para la PoC.
- Inclusión de veredicto visual de vulnerabilidad.
- Análisis de `X-Frame-Options`.
- Análisis de `Content-Security-Policy`.
- Revisión de `frame-ancestors`.
- Múltiples plantillas de señuelo.
- Selector dinámico de plantillas dentro de la PoC.
- Control de opacidad del iframe.
- Botón para mostrar u ocultar el iframe.
- Opción `--check-only`.
- Opción `--no-check`.
- Opción `--no-open`.
- Opción `--list-templates`.
- Opción `--template`.
- Opción `--opacity`.
- Apertura automática de la PoC generada en navegador.
- Mejoras en la salida por consola.
- Recomendaciones de remediación dentro del HTML generado.
- Aviso legal integrado en la PoC.

---

## Versiones

| Versión | Descripción |
|---|---|
| `v1.0.0` | Primera versión funcional para validar Clickjacking y generar HTML básico |
| `v2.0.0` | Versión mejorada con PVGUARD, múltiples plantillas, análisis de headers y PoC interactiva |

---

## Uso ético

Esta herramienta debe utilizarse únicamente en:

- Laboratorios propios.
- Entornos de práctica.
- Auditorías internas autorizadas.
- Pruebas de penetración con permiso explícito.
- Programas de bug bounty donde la prueba esté permitida.

El uso no autorizado contra sistemas de terceros puede ser ilegal.

El autor no se hace responsable por el uso indebido de esta herramienta.

---

## Autor

**Gh0s7m4n**  

Repositorio:

```text
https://github.com/joepm21/Checker-Clickjacking
```

---

## Licencia

Proyecto publicado con fines educativos, de investigación y pruebas de seguridad autorizadas.
