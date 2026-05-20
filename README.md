# PVGUARD - Checker Clickjacking

![Version](https://img.shields.io/badge/version-1.0%20%7C%202.0-brightgreen)
![Python](https://img.shields.io/badge/python-3.x-blue)
![Uso](https://img.shields.io/badge/uso-autorizado-red)

## Descripción

**PVGUARD - Checker Clickjacking** es una herramienta en Python diseñada para verificar si una aplicación web cuenta con protecciones contra ataques de **Clickjacking** y generar una **Prueba de Concepto (PoC)** en HTML.

La herramienta analiza encabezados de seguridad como `X-Frame-Options` y `Content-Security-Policy: frame-ancestors`, y genera una demostración visual para evidenciar si el sitio puede ser embebido dentro de un `iframe`.

El proyecto incluye dos versiones principales:

- **v1.0**: versión inicial por línea de comandos para generar una PoC básica de Clickjacking.
- **v2.0**: versión mejorada, apertura automática de la PoC, análisis visual de headers, selector de plantillas y 20 templates diferentes.

---

## Versiones

### Checker Clickjacking v1.0

La primera versión permite generar una PoC HTML de Clickjacking indicando una URL objetivo desde la terminal.

Características principales:

- Ejecución desde CLI.
- Generación directa de PoC HTML.
- Verificación básica de headers de seguridad.
- Herramienta ligera y fácil de usar.
- Enfocada en pruebas rápidas de Clickjacking.

Ejemplo de uso:

```bash
./checker_clickjacking https://example.com
```

---

### Checker Clickjacking v2.0

La segunda versión incluye mejoras visuales, funcionales y de usabilidad para facilitar la generación de PoC y la presentación de evidencia.

Características principales:


- Análisis de encabezados de seguridad.
- Detección de `X-Frame-Options`.
- Detección de `Content-Security-Policy: frame-ancestors`.
- Generación de reporte HTML interactivo.
- Apertura automática de la PoC generada en el navegador.
- Opción para evitar la apertura automática usando `--no-open`.
- Control de opacidad del iframe víctima.
- Botón para mostrar u ocultar el iframe.
- Selector de plantillas dentro del HTML generado.
- 20 templates diferentes para distintos escenarios de demostración.
- Modo `--check-only` para verificar headers sin generar PoC.
- Modo `--no-check` para generar la PoC sin validar headers.


Ejemplo de uso:

```bash
./checker_clickjacking -u https://example.com
```

Ejemplo usando una plantilla específica:

```bash
./checker_clickjacking -u https://example.com --template banca
```

Ejemplo con opacidad personalizada:

```bash
./checker_clickjacking -u https://example.com --template alerta --opacity 0.5
```

Ejemplo sin abrir automáticamente el navegador:

```bash
./checker_clickjacking -u https://example.com --no-open
```

---

## Templates disponibles

La versión 2.0 incluye 20 plantillas distintas para simular diferentes escenarios de ingeniería social o interfaces señuelo durante una prueba autorizada.

```bash
premio
login
pago
actualizacion
newsletter
encuesta
cupon
cloud
soporte
documento
delivery
calendario
wifi
banca
mfa
vpn
capacitacion
inventario
alerta
recompensa
```

Para listar las plantillas disponibles:

```bash
./checker_clickjacking --list-templates
```

---

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/joepm21/Checker-Clickjacking.git
cd Checker-Clickjacking
```

También puedes ejecutar el script directamente con Python 3 si no requiere dependencias externas adicionales:

```bash
python3 checker_clickjacking -h
```

---

## Uso general

Ver ayuda:

```bash
./checker_clickjacking -h
```

Analizar una URL y generar la PoC:

```bash
./checker_clickjacking -u https://example.com
```

Guardar el resultado con un nombre personalizado:

```bash
./checker_clickjacking -u https://example.com -o reporte_clickjacking.html
```

Verificar únicamente los headers:

```bash
./checker_clickjacking -u https://example.com --check-only
```

Generar PoC sin verificar headers:

```bash
./checker_clickjacking -u https://example.com --no-check
```

---

## Encabezados evaluados

La herramienta revisa principalmente los siguientes controles de seguridad:

### X-Frame-Options

Permite definir si un sitio puede ser cargado dentro de un `iframe`.

Valores recomendados:

```http
X-Frame-Options: DENY
```

O:

```http
X-Frame-Options: SAMEORIGIN
```

### Content-Security-Policy: frame-ancestors

Control moderno para restringir qué orígenes pueden embeber el sitio.

Ejemplo recomendado:

```http
Content-Security-Policy: frame-ancestors 'none';
```

O, si solo se permite el mismo dominio:

```http
Content-Security-Policy: frame-ancestors 'self';
```

---

## Recomendación de remediación

Si la aplicación permite ser cargada dentro de un `iframe` sin restricciones, se recomienda implementar controles de seguridad a nivel de encabezados HTTP.

Configuración recomendada:

```http
X-Frame-Options: DENY
Content-Security-Policy: frame-ancestors 'none';
```

En aplicaciones donde sea necesario permitir `iframe` para dominios específicos, se debe usar una política restrictiva y explícita:

```http
Content-Security-Policy: frame-ancestors 'self' https://dominio-autorizado.com;
```

---

## Casos de uso

Esta herramienta puede ser utilizada en:

- Pruebas de penetración web autorizadas.
- Laboratorios de seguridad.
- Programas de Bug Bounty donde el alcance lo permita.
- Validación de headers de seguridad.
- Generación de evidencia para reportes técnicos.
- Demostraciones controladas sobre ataques de Clickjacking.

---

## Autor

**Gh0s7m4n**  

---

## Aviso legal

Esta herramienta debe utilizarse únicamente en entornos autorizados, laboratorios propios, pruebas de penetración con permiso o programas de Bug Bounty donde la prueba esté permitida.

El uso no autorizado contra sistemas de terceros puede constituir una actividad ilegal. El autor no se responsabiliza por el uso indebido de esta herramienta.
