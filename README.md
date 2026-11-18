# CesTick — Prototipo interactivo, Tucanthon 2026

Proyecto **nuevo desde cero** inspirado en los documentos «Memoria Técnica – Tucanthon» y «Propuesta – Prototipo». Interfaz azul, adaptable a móvil y escritorio, con dos modos (consumidor y comercio).

## Requisitos

Node.js 20.19+ o 22.12+ y npm, navegador moderno. Con conexión a Internet instala dependencias:

```bash
npm install
npm run dev
```

Abre la URL local indicada por Vite (normalmente http://localhost:5173). Compila para distribuir con:

```bash
npm run build
npm run preview
```

## Funciones y recorrido recomendado

**Consumidor**: Inicio → Comparar (agrega productos y cambia cantidades en Mi canasta) → Escanear → «Probar con un ticket preparado» → Revisión → Registrar compra → Historial / Alertas → Beneficios → Reclamar cupón.

**Comercio**: Cambia a «Comercio» en el selector de la barra lateral (en móvil abre menú ☰) → Cupones (crea una campaña) → Publicidad (activa/pausa anuncio demo) → Canjes (introduce el código generado en Beneficios).

Los valores se comparten entre pantallas y se guardan en `localStorage` en el mismo navegador. En Perfil puedes restaurar los datos de demostración.

## Qué es real, qué es demo

- ✅ Catálogo de ~50 productos, búsqueda y filtros, canasta y cantidades.
- ✅ Comparación matemática por tienda con precios **ficticios** y señalización de cobertura faltante.
- ✅ Captura de archivo de imagen y OCR con Tesseract.js en el cliente (si puede descargar idioma español/inglés), seguido de **corrección manual obligatoria**.
- ✅ Recorrido alternativo con ticket precargado, registro de compra, historial, observaciones de precio por sucursal reconocida, puntos y cupones.
- ✅ Puntos de prueba: 10 por ticket más 2 por producto único normalizado, máximo 20; restricciones locales sobre duplicados, recencia, límites.
- ✅ Reserva de cupón y validación desde la vista de comercio; puntos y cupos de demostración.
- ⚠️ No existe backend ni autenticación real. La validación del ticket **no prueba** una compra auténtica ni impide fraude entre navegadores/dispositivos.
- ⚠️ Los precios, negocios y campañas son **escenarios de prueba**, no precios o descuentos vigentes en Cancún. El OCR no garantiza detectar todos los formatos de ticket.
- ⚠️ No hay cobros reales, promociones reales, notificaciones push o conexiones a Profeco ni supermercados.
- ⚠️ Los datos de `localStorage` no se sincronizan entre dispositivos.

## Diseño y tecnología

React + Vite + TypeScript + CSS adaptable + lucide-react, Tesseract.js para OCR. Identidad azul. Estructura preparada para conectar un backend y posteriormente empaquetar mediante Capacitor; **todavía no se incluye un proyecto Android/iOS nativo**. Se agrega `capacitor.config.ts` para preparar esos proyectos desde un entorno con Android Studio o Xcode.

## Futuras integraciones

1. PostgreSQL / Supabase con autenticación, permisos por rol y reglas transaccionales para saldos y cupones.
2. Normalización robusta de productos, códigos de barras y extracción de sucursal desde recibos reales.
3. Fuente de datos de precios permitida y control de caducidad/procedencia y confianza de cada observación.
4. Geolocalización consentida / zona manual, distancia real y comparación con cobertura explícita.
5. Capacitor con plugins para cámara y almacenamiento seguro, pruebas en Android/iOS.
6. Factores antifraude, aviso de privacidad, consentimiento de uso comunitario de precios y resguardo de tickets.

## Privacidad

No subas tickets reales con información sensible al entorno de demostración sin revisar los datos. En esta versión el OCR se ejecuta en el navegador, y la imagen se usa para previsualización sin persistirla permanentemente; los artículos corregidos se guardan localmente.

## Empaquetado móvil (opcional)

Cuando hayas instalado las dependencias y el SDK nativo:

```bash
npm run cap:android # primera vez, requiere Android Studio
npm run cap:sync    # sincronizar cambios web
npx cap open android
```

Para iOS, usa `npm run cap:ios` y `npx cap open ios` en macOS con Xcode. En Android/iOS, confirma que cámara y lectura OCR funcionan en el WebView antes de publicar.


## Rediseño UX — navegación editorial

El menú lateral fue reemplazado por navegación horizontal en escritorio y barra inferior en móvil. El perfil permite entrar a historial, preferencias y modo comercio. El inicio ahora guía al usuario con tres pasos; el comparador, tickets, alertas, puntos y panel comercial conservan su lógica. La referencia visual es una landing editorial, pero CesTick mantiene su comportamiento de aplicación. Las fuentes de precios y promociones de ejemplo siguen identificadas como demostración.

## Ajuste visual — edición con más personalidad

Esta versión conserva los recorridos, el menú horizontal y la navegación móvil del prototipo UX. Se añadió `src/visual-enhancements.css`, con fondos azul hielo para agrupar secciones, tarjetas con un relieve discreto, detalles gráficos geométricos, jerarquía tipográfica y ajustes responsive. La vista de Alertas incorpora una ilustración **explícitamente decorativa** (no presenta un historial real de precios). No se alteraron cálculos, cupones, productos ni persistencia.
