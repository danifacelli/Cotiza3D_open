# Cotiza3D

Cotiza3D es una app web pensada para quienes ofrecen servicios de impresión 3D y necesitan sacar presupuestos claros sin enredarse con planillas. Todo vive en tu navegador, así que puedes seguir probando precios, guardar clientes o preparar nuevas inversiones sin crear cuentas ni depender de una nube externa.

## Lo que puedes hacer
- **Dashboard en un vistazo:** resume ingresos, ganancia estimada, presupuestos pendientes y trabajos en curso. Además sugiere los próximos pasos para dejar la app lista.
- **Diseños reutilizables:** registra modelos con materiales, tiempos y costos. Puedes convertir cualquier diseño en presupuesto con un par de clicks.
- **Presupuestos completos:** arma cotizaciones detalladas, duplica versiones, controla estados (borrador, aceptado, en preparación, listo, entregado o cancelado) y genera precios en USD y en tu moneda local.
- **Clientes organizados:** guarda datos de contacto, histórico de trabajos y el total comprado por cada uno.
- **Insumos y máquinas:** administra filamentos, precios por kilo, impresoras, depreciación y consumo eléctrico para que los cálculos sean realistas.
- **Inversiones y futuras compras:** registra equipos o mejoras, sigue qué porcentaje ya recuperaste y convierte tu lista de deseos en inversiones reales cuando las compres.
- **Links útiles:** conserva referencias, tutoriales o tiendas asociadas a tu taller.
- **Configuración y respaldo:** ajusta margen, mano de obra, tarifas eléctricas, moneda local y exporta/importa toda tu información en un archivo JSON.

## Cómo empezar (en palabras simples)
1. **Instala Node.js 18 o superior**: al hacerlo también obtienes `npm`. Si ya lo tienes, sigue al paso 2.
2. **Descarga el proyecto**: puedes clonarlo con Git o bajar el ZIP desde tu repositorio favorito.
3. **Abre una terminal en la carpeta del proyecto** y ejecuta `npm install` para que se descarguen las dependencias.
4. **Lanza la app con `npm run dev`**. Se abrirá en `http://localhost:9002`. Mantén la terminal abierta mientras la usas.
5. **Guarda un acceso directo** a ese enlace en tu navegador para entrar rápido a tu panel.

> ¿Quieres instalarlo en otro equipo o compartir tus datos? Exporta un respaldo desde Configuración, copia el archivo y luego impórtalo en la otra instancia.

### Instalación local paso a paso
Si ya descargaste el repositorio (por clonación con Git o descomprimiendo un ZIP), sigue estos comandos en tu terminal:

```bash
# 1) Ubícate en la carpeta del proyecto (reemplaza la ruta si la moviste)
cd Cotiza3D_open

# 2) Instala las dependencias declaradas en package.json
npm install

# 3) Levanta el entorno de desarrollo en http://localhost:9002
npm run dev
```

Para un uso productivo puedes compilar y ejecutar la app con `npm run build` seguido de `npm run start`.

## Cómo está organizada la navegación
- `Dashboard`: métricas clave, progreso para recuperar inversiones y trabajos activos.
- `Diseños`: biblioteca de modelos previa a crear presupuestos.
- `Presupuestos`: tabla filtrable, estados, duplicación y totales por moneda.
- `Clientes`: contactos con historial de piezas y montos.
- `Insumos` y `Máquinas`: catálogos con vistas en tarjetas, edición rápida y eliminación segura.
- `Inversiones`: seguimiento de capital invertido vs. ganancias generadas.
- `Futuras Compras`: lista de deseos que puedes convertir en inversiones reales.
- `Links`: repositorio de recursos y tiendas que usas a diario.
- `Configuración`: parámetros globales y la sección de copia de seguridad/restauración.

## Cuida tus datos
- Todo se guarda en `localStorage`, por lo que tu información es privada y se queda en el navegador donde trabajas.
- Si borras la caché, cambias de equipo o quieres compartir el proyecto, exporta previamente el respaldo (`JSON`) y luego impórtalo.
- El archivo incluye materiales, máquinas, configuraciones, presupuestos, diseños, clientes, inversiones, listas de compras y links.

## Sigue construyendo
Cotiza3D está pensada para que puedas adaptarla a tu flujo de trabajo. Algunas ideas:
- Crea vistas personalizadas para tipos de impresión específicos (resina, SLS, etc.).
- Añade más monedas o automatiza la cotización del tipo de cambio.
- Integra recordatorios con tu calendario o herramientas CRM.

Si quieres profundizar en la parte técnica, estructura del código y cómo colaborar, revisa `docs/technical-overview.md`.

## Autor
Proyecto creado por **Daniel Facelli**. Conecta en LinkedIn: [https://www.linkedin.com/in/danielfacelli/](https://www.linkedin.com/in/danielfacelli/)
