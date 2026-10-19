# Contexto: infraestructura de apps para clientes de appi

## Quién soy
Diego Villegas, de appi (agencia de automatización y desarrollo en Valledupar, Colombia). Desarrollo apps y páginas web para clientes y quiero gestionarlas todas de forma ordenada y barata.

## Decisiones tomadas
- **Hosting:** una sola cuenta de Cloudflare (appi), plan Workers Paid ($5 USD/mes compartido entre todos los clientes).
- **Código:** organización `appi` en GitHub, **un repositorio por proyecto**.
- **Despliegue:** cada repo se conecta a Cloudflare y se publica automáticamente con cada push.
- **Herramientas:** Claude (chat) para planear y escribir textos; Claude Code para construir, probar y desplegar.

## Stack de Cloudflare
- **Workers:** lógica/backend de cada app.
- **Pages / static assets:** páginas web de clientes (gratis e ilimitado).
- **D1:** base de datos SQL por cliente.
- **R2:** archivos (fotos, PDFs) por cliente.
- **KV:** solo para datos que se leen mucho y se escriben poco (config, sesiones). Evitar escrituras frecuentes, que son caras.
- **Workers AI:** IA integrada (modelos open source). Para IA más potente, llamar APIs externas (Claude/OpenAI) y usar AI Gateway para controlar el consumo por cliente.

## Convención de nombres
El mismo nombre en GitHub, Worker y recursos:
- Repo `cliente-proyecto` → Worker `cliente-proyecto` → D1 `cliente-proyecto-db` → R2 `cliente-proyecto-files`
- Ejemplos: `myjugo-pos`, `estetica-agenda`, `estetica-web`

## Reglas
- Los datos de cada cliente van **siempre separados**: su propia base de datos y su propio bucket. Nunca mezclar clientes.
- Cada cliente con su propio dominio.
- Construir una **plantilla base reutilizable** (login, usuarios, clientes, reportes) para no empezar de cero en cada proyecto.
- Si un cliente grande quiere ser dueño de su sistema, se le crea su propia cuenta de Cloudflare y yo la gestiono como miembro.

## Proyectos planeados
1. **POS para restaurante con 5 puntos de venta:** conectado a la nube, con reportes por punto. Debe **funcionar sin internet** (guardar ventas localmente y sincronizar cuando vuelva la conexión).
2. **Sistema para una estética:** agendamiento de citas y registro de clientes. Posible bot de WhatsApp y recordatorios.
3. **Páginas web de clientes:** que se conecten con sus apps (formularios, agendar, menú actualizado desde el POS, chat con IA).

## Siguiente paso
Arrancar con un proyecto pequeño (una página web) para probar el flujo completo GitHub → Cloudflare antes de construir el POS.

## Estilo de respuesta
Claro y al grano, en español. Explicaciones sencillas, a menos que pida detalles.
