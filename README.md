# Plan 21K — Training Tracker

Web app mobile-first para seguimiento del plan de entrenamiento de media maratón (30 Ago 2026).

## Stack

- **Frontend**: HTML/CSS/JS vanilla — sin frameworks, sin build tools
- **Base de datos**: Supabase (Postgres)
- **Hosting**: GitHub Pages

---

## Setup en 5 pasos

### 1. Crear proyecto en Supabase

1. Ir a [supabase.com](https://supabase.com) → New project
2. Elegir región más cercana (ej: São Paulo)
3. Guardar la contraseña del proyecto

### 2. Cargar el plan

1. En tu proyecto Supabase → **SQL Editor**
2. Pegar todo el contenido de `seed.sql`
3. Ejecutar → debería mostrar "Success. 88 rows affected"

### 3. Obtener las credenciales

En Supabase → **Settings → API**:
- `Project URL` → algo como `https://xxxx.supabase.co`
- `anon / public` key → el token largo que empieza con `eyJ...`

### 4. Configurar la app

Abrí `index.html` y editá las líneas 2-3 del bloque de config:

```js
const SUPABASE_URL  = 'https://xxxx.supabase.co';
const SUPABASE_KEY  = 'eyJ...tu-anon-key...';
```

> **Alternativa sin editar código**: Si abrís la app sin configurar las keys,
> aparece un formulario para ingresarlas. Se guardan en `localStorage`.

### 5. Deploy a GitHub Pages

```bash
# Crear repo nuevo
git init
git add index.html seed.sql README.md
git commit -m "init: plan 21K tracker"
git remote add origin https://github.com/TU_USER/plan-21k.git
git push -u origin main

# En GitHub → Settings → Pages → Source: main / root
```

La app queda disponible en `https://TU_USER.github.io/plan-21k/`

---

## Estructura del proyecto

```
plan-21k/
├── index.html   # App completa (todo en un archivo)
├── seed.sql     # Schema + datos del plan (88 entrenamientos)
└── README.md
```

---

## Tabla `workouts` — estructura

| Columna     | Tipo   | Descripción                          |
|-------------|--------|--------------------------------------|
| id          | serial | PK autoincremental                   |
| semana      | int    | Número de semana (1–22)              |
| km_sem      | int    | Kilómetros totales de la semana      |
| dia         | text   | Día abreviado (Mar, Mié, Vie, Dom)   |
| fecha       | date   | Fecha del entrenamiento              |
| tipo        | text   | easy / strength / tempo / interval / long / race / rest |
| sesion      | text   | Nombre corto de la sesión            |
| descripcion | text   | Descripción del workout              |
| detalle     | text   | Notas adicionales / tips             |

---

## Features de la app

- **Countdown en vivo** hasta el 30 de agosto
- **Próximo entrenamiento** — detecta si es hoy o el siguiente futuro
- **Semana actual** — vista rápida de los 4 entrenamientos
- **Barra de progreso** — semanas completadas vs restantes
- **Plan completo** — accordion colapsable por semana
- **Modal de detalle** — tap en cualquier entrenamiento
- **Config dinámica** — formulario para ingresar keys sin editar código

---

## Personalización

Los colores por tipo de entrenamiento están en las variables CSS:

```css
--easy:     #4a9e6b;
--strength: #5b8dd9;
--tempo:    #c97f2a;
--interval: #c94444;
--long:     #7b5ea7;
--race:     #f4600c;
--rest:     #4a7a8a;
```
