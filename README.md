# 🚛 FleteCalc — Cotizador de Fletes de Cargas

App web para cotizar fletes en Argentina. Deployada en **GitHub Pages**, gratuita, sin backend.

## Estructura

```
fletecalc/
├── index.html      ← App principal (no tocar salvo cambios de diseño)
├── precios.json    ← EDITÁ ESTE ARCHIVO para actualizar precios
└── README.md
```

---

## ⚡ Cómo deployar en GitHub Pages

### 1. Crear el repositorio

1. Entrá a [github.com/new](https://github.com/new)
2. Nombre: `fletecalc` (o el que quieras)
3. Visibilidad: **Public** (requerido para GitHub Pages gratis)
4. Crear repositorio

### 2. Subir los archivos

**Opción A — Desde la web de GitHub:**
1. Entrá al repo recién creado
2. "Add file" → "Upload files"
3. Arrastrá `index.html`, `precios.json` y `README.md`
4. Commit: "Primera versión"

**Opción B — Con Git:**
```bash
git clone https://github.com/TU_USUARIO/fletecalc.git
# Copiá los archivos a la carpeta
git add .
git commit -m "Primera versión FleteCalc"
git push origin main
```

### 3. Activar GitHub Pages

1. En el repo → **Settings** → **Pages** (menú lateral izquierdo)
2. Source: **Deploy from a branch**
3. Branch: `main` / `/ (root)`
4. Guardar

En 1-2 minutos tu app estará en:
```
https://TU_USUARIO.github.io/fletecalc/
```

---

## 📝 Cómo actualizar precios

### Gas Oil
1. Entrá al repo en GitHub
2. Hacé click en `precios.json`
3. Click en el ícono del lápiz (✏) para editar
4. Cambiá el valor de `"gasoil_litro"` y `"ultima_actualizacion"`
5. Commit → en segundos la app muestra el nuevo precio

```json
"combustible": {
  "gasoil_litro": 1450,   ← Cambiá este número
  "nota": "..."
}
```

### Peajes
En el mismo `precios.json`, cada corredor tiene `total_2ejes` y `total_3ejes`:

```json
{
  "id": "rosario_bsas",
  "nombre": "Rosario → Buenos Aires",
  "total_2ejes": 18500,   ← Cambiá estos
  "total_3ejes": 27500    ← valores
}
```

### Sueldo de referencia FADEEAC
```json
"indices": {
  "sueldo_minimo_chofer_larga_distancia": 850000  ← Actualizar con cada paritaria
}
```

---

## 🗺 Cómo funciona el cálculo de ruta

La app usa dos servicios gratuitos y sin API key:
- **Nominatim** (OpenStreetMap) para geocodificar ciudades
- **OSRM** para calcular distancia y tiempo de ruta

Si no encuentra la ruta, podés ingresar km y horas manualmente.

---

## 💡 Fórmula de precio

```
Costo base = combustible + peajes + gastos ruta
           + sueldo (prorrat.) + seguro (prorrat.)
           + amortización + admin (prorrat.)
           + mantenimiento (prorrat.) + seguro de carga

Precio de venta = Costo base / (1 - margen% - comisión%)
Ganancia        = Precio - (Costo base + Comisión chofer)
```

La comisión del chofer se calcula sobre el precio de venta final (no sobre el costo), resolviéndose algebraicamente para evitar circularidad.

---

## 🔧 Personalización rápida

Para agregar un corredor de peajes nuevo, editá `precios.json` y agregá un objeto al array `corredores`:

```json
{
  "id": "mi_corredor",
  "nombre": "Ciudad A → Ciudad B (RN XX)",
  "km": 250,
  "total_2ejes": 12000,
  "total_3ejes": 18000,
  "paradas": ["Parada 1", "Parada 2"]
}
```

---

Desarrollado con FleteCalc © 2025
