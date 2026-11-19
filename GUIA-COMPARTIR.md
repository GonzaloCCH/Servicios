# Compartir el resumen en vivo (solo ver)

Se hace una sola vez, desde el navegador (celular o computadora). Es gratis.

## 1. Crear el proyecto
1. Entra a https://console.firebase.google.com con una cuenta de Google.
2. "Agregar proyecto" → ponle un nombre (ej. servicios-hogar) → puedes desactivar Google Analytics → Crear.

## 2. Activar el acceso anónimo
1. Menú **Compilación → Authentication → Comenzar**.
2. Pestaña **Sign-in method** → **Anónimo** → Habilitar → Guardar.

## 3. Crear la base de datos
1. Menú **Compilación → Realtime Database → Crear base de datos**.
2. Elige la ubicación más cercana y **Modo bloqueado**.
3. Arriba verás la dirección, parecida a `https://servicios-hogar-default-rtdb.firebaseio.com`. **Cópiala**.
4. Pestaña **Reglas** → borra todo y pega esto → **Publicar**:

```
{
  "rules": {
    "h": {
      "$code": {
        ".read": true,
        ".write": "auth != null && (!data.exists() || data.child('o').val() === auth.uid)"
      }
    }
  }
}
```

## 4. Sacar la clave API
1. Rueda de ajustes (arriba a la izquierda) → **Configuración del proyecto**.
2. En "Tus apps" toca **</> (Web)** → ponle un nombre → Registrar app.
3. Copia el valor de `apiKey` (empieza con `AIza`).

## 5. Conectar la app
1. Publica la carpeta de la app en un hosting con https (Netlify Drop o GitHub Pages) y ábrela desde esa dirección.
2. **Ajustes → Compartir con los demás**: pega la dirección de la base de datos y la clave API → **Conectar y crear enlace**.
3. Toca **Compartir enlace** y mándalo por WhatsApp. Quien lo abra verá solo el resumen y podrá instalar la app desde Chrome ("Agregar a pantalla de inicio").

## Cómo funciona
- Tú sigues usando la app sin internet. Al conectarte, los cambios se suben solos.
- Los demás ven los datos al instante cuando tienen internet, y el último resumen guardado cuando no.
- Ellos no pueden modificar nada. Solo tu teléfono puede escribir.
- Cualquiera que tenga el enlace puede ver el resumen: compártelo solo con quienes pagan.
- El respaldo que guardas desde Ajustes incluye el permiso de escritura: no lo compartas. Sirve para recuperar todo si cambias de teléfono.
