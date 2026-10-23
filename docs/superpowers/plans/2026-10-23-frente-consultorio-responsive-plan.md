# Frente del consultorio responsive Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Servir la foto vertical del frente en celulares y la horizontal en pantallas grandes, con un encuadre proporcional a cada formato.

**Architecture:** Reemplazar la imagen única del hero por un elemento `<picture>` con la variante vertical como fuente base y la horizontal para `lg` en adelante. Ajustar las alturas responsive del contenedor sin cambiar sus efectos visuales ni el resto de la página.

**Tech Stack:** HTML estático, Tailwind CSS vía CDN, navegador responsive.

**Spec:** `docs/superpowers/specs/2026-10-23-frente-consultorio-responsive-design.md`

## Global Constraints

- Cambiar únicamente la imagen del hero en `index.html`.
- Usar `<picture>` con `media` para que el navegador elija una sola imagen según el ancho de pantalla.
- Mantener el efecto hover, la superposición de gradiente y el resto del diseño existente.
- No agregar dependencias ni JavaScript.

## Review Focus

- Viewport móvil: debe solicitarse y mostrarse `frenteConsultorioVertical.jpeg`.
- Viewport `lg` o superior: debe solicitarse y mostrarse `frenteConsultorioHorizontal.jpeg`.
- El `alt` debe permanecer en la imagen visible para accesibilidad.
- Las clases de tamaño deben evitar recortes excesivos en ambos formatos.
- Las rutas deben coincidir exactamente con los archivos existentes.

---

### Task 1: Actualizar el hero con imágenes responsive

**Files:**
- Modify: `index.html:190-194` (contenedor e imagen del hero)
- Test: verificación manual/estructural del HTML y rutas de recursos

**Interfaces:**
- Consumes: `Resources/Img/frenteConsultorioVertical.jpeg` y `Resources/Img/frenteConsultorioHorizontal.jpeg`.
- Produces: un `<picture>` en el hero que selecciona la fuente horizontal con `media="(min-width: 1024px)"` y usa la vertical como fallback.

- [ ] **Step 1: Confirmar los recursos**

Verificar que existan ambas rutas:

```powershell
Test-Path ".\Resources\Img\frenteConsultorioVertical.jpeg"
Test-Path ".\Resources\Img\frenteConsultorioHorizontal.jpeg"
```

Expected: ambas devuelven `True`.

- [ ] **Step 2: Reemplazar la imagen única por `<picture>`**

En el contenedor existente del hero, conservar el overlay y el `group`, cambiar la altura a `h-[620px] lg:h-[420px]`, y usar:

```html
<picture>
    <source media="(min-width: 1024px)" srcset="Resources/Img/frenteConsultorioHorizontal.jpeg">
    <img src="Resources/Img/frenteConsultorioVertical.jpeg" alt="Frente del consultorio odontológico" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-105">
</picture>
```

Mantener el contenedor con `rounded-2xl overflow-hidden` y sus sombras actuales.

- [ ] **Step 3: Verificar la estructura modificada**

Comprobar que el documento contenga un único `picture` del hero, las dos rutas exactas, el `media` de `1024px` y el nuevo texto alternativo:

```powershell
$html = Get-Content ".\index.html" -Raw
$html.Contains("<picture>") -and
$html.Contains("frenteConsultorioVertical.jpeg") -and
$html.Contains("frenteConsultorioHorizontal.jpeg") -and
$html.Contains('(min-width: 1024px)') -and
$html.Contains('alt="Frente del consultorio odontológico"')
```

Expected: `True`.

- [ ] **Step 4: Revisar el diff**

Run: `git --no-pager diff -- index.html docs/superpowers/specs/2026-10-23-frente-consultorio-responsive-design.md docs/superpowers/plans/2026-10-23-frente-consultorio-responsive-plan.md`

Expected: solo la especificación, el plan y el bloque de imagen del hero aparecen modificados.
