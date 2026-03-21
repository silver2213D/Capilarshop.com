# Configuración de Supabase para Escencia Capilar

## Paso 1: Crear la tabla en Supabase

1. Ve a tu proyecto en [https://app.supabase.com](https://app.supabase.com)
2. Abre el **SQL Editor**
3. Copia y ejecuta este código SQL:

```sql
-- Crear tabla productos
CREATE TABLE productos (
  id BIGINT PRIMARY KEY,
  nombre VARCHAR NOT NULL,
  categoria VARCHAR NOT NULL,
  seccion VARCHAR,
  precio BIGINT NOT NULL,
  imagen TEXT,
  descripcion TEXT,
  rating NUMERIC,
  descuento NUMERIC,
  stock BIGINT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Habilitar RLS (Row Level Security)
ALTER TABLE productos ENABLE ROW LEVEL SECURITY;

-- Crear políticas de acceso público
CREATE POLICY "Enable read access for all users" ON productos
  FOR SELECT USING (true);

CREATE POLICY "Enable insert for all users" ON productos
  FOR INSERT WITH CHECK (true);

CREATE POLICY "Enable update for all users" ON productos
  FOR UPDATE USING (true) WITH CHECK (true);

CREATE POLICY "Enable delete for all users" ON productos
  FOR DELETE USING (true);
```

## Paso 2: Verificar que los datos existan

Después de crear la tabla, ve a la pestaña **Table Editor** y verifica:
- La tabla `productos` está creada
- Las columnas coinciden con el script SQL

## Paso 3: Migrar productos existentes (opcional)

Si quieres guardar los productos actuales que tienes en la tienda:

1. En la página Admin, haz clic en "Añadir Producto"
2. Agrega los productos nuevamente
3. Se guardarán automáticamente en Supabase

## Paso 4: Verificar sincronización

Abre la **consola del navegador** (F12) para ver los mensajes de Supabase:
- `Productos cargados desde Supabase: X`
- `Producto insertado en Supabase`
- `Producto eliminado de Supabase`

## Troubleshooting

### Los productos no se sincroniza
- Verifica que la tabla `productos` existe en Supabase
- Revisa la consola del navegador (F12) para ver errores
- Asegúrate de que las políticas RLS están habilitadas

### Todo se guarda en el navegador pero no en Supabase
- Verifica tu conexión a internet
- Revisa que estés usando el SUPABASE_URL y SUPABASE_KEY correctos
- Asegúrate de que la tabla tiene las columnas correctas

### La tabla está vacía
- Agrega productos nuevos desde la página Admin
- Verifica que los permisos RLS están configurados correctamente
