# Trabajo_Integrador_Programcion

Food Store es un catálogo con filtro por categoría, una tabla paginada y un formulario para crear y editar productos. La tabla permite la baja lógica con confirmación

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

La [API publicada en Railway](https://trabajointegradorprogramcion-production.up.railway.app/docs) usa la rama `main`, la carpeta raíz `/api` y Python 3.14. GitHub Actions ya tiene configurada esa dirección para publicar [Food Store en GitHub Pages](https://santiprandina.github.io/Trabajo_Integrador_Programcion/).

Para cambiar la dirección de la API, usá la variable de repositorio `FOOD_STORE_API_URL` con el origen HTTPS, sin `/docs`, y ejecutá **Actions → Publicar Food Store → Run workflow**.

La API autoriza CORS para el sitio de Santi y los dos orígenes locales del puerto 5500. En Railway, SQLite usa el almacenamiento del servicio. Los cambios de esa base pueden perderse cuando Railway reemplaza el contenedor.
