# Trabajo_Integrador_Programcion

Food Store es un catálogo con filtro por categoría, una tabla paginada y un formulario para crear y editar productos. La tabla permite la baja lógica con confirmación. Esta versión adapta el [Food Store de Joel Herrera](https://github.com/joelherrera-print/Integrador_Progamacion_lll) con una interfaz oscura y una nueva foto de portada.

- `api/` contiene FastAPI, SQLModel, SQLite y la autocorrección del parcial.
- `web/` contiene el sitio en HTML, CSS y JavaScript.

## Probar en Windows

Abrí la carpeta del proyecto en Visual Studio Code. En la primera terminal, creá el entorno y arrancá la API.

```powershell
py -m venv venv
.\venv\Scripts\python.exe -m pip install -r api\requirements.txt
cd api
..\venv\Scripts\python.exe -m uvicorn main:app --reload
```

En otra terminal, desde la carpeta principal, arrancá la web.

```powershell
.\venv\Scripts\python.exe -m http.server 5500 --directory web
```

Abrí [Food Store local](http://localhost:5500/) o la [documentación de la API](http://127.0.0.1:8000/docs). La API carga 28 productos en 4 categorías al iniciar con una base vacía. Guarda los cambios en `api/foodstore.db`.

Para ejecutar las pruebas, desde `api/` corré estos comandos.

```powershell
..\venv\Scripts\python.exe probar_api.py
..\venv\Scripts\python.exe probar_api.py --ver-base
```

## Publicar la web y su API

1. En Render, creá un Blueprint conectado a este repositorio. `render.yaml` define el servicio `food-store-santi-prandina-api`. Cuando esté activo, comprobá su ruta `/docs`.
2. En GitHub, abrí **Settings → Secrets and variables → Actions → Variables**. Creá la variable `FOOD_STORE_API_URL` con la dirección HTTPS de ese servicio, sin `/docs`.
3. En **Settings → Pages**, elegí **GitHub Actions** como origen. En **Actions**, ejecutá **Publicar Food Store**.
4. Cuando termine la acción, abrí [Food Store en GitHub Pages](https://santiprandina.github.io/Trabajo_Integrador_Programcion/).

La API autoriza CORS para el sitio de Santi y los dos orígenes locales del puerto 5500. Su SQLite es independiente. En el plan gratuito de Render, los cambios en esa base pueden perderse cuando se reinicia o vuelve a desplegar la instancia.
