# Especificación del Prototipo: Panel de Administración - AgentHub

Este documento define los requisitos funcionales, estructurales y visuales para el desarrollo del prototipo frontend de AgentHub. Actúa como el contrato de diseño y comportamiento antes de la implementación del código HTML, CSS y JavaScript.

---

## 1. Descripción del Producto y Contexto

### ¿Qué es AgentHub?
AgentHub es una plataforma SaaS donde las empresas pueden alquilar agentes de Inteligencia Artificial (asistentes inteligentes preconfigurados). Estos agentes se equipan con capacidades modulares llamadas **skills** (navegación web, lectura de documentos, gestión de calendarios) y se despliegan para automatizar tareas de negocio específicas.

### El Usuario Administrador
El usuario de este panel es un miembro del equipo interno de AgentHub. Sus objetivos principales son supervisar la salud de la plataforma, gestionar las cuentas de usuario, configurar el catálogo de agentes y skills, y monitorear errores críticos del sistema.

---

## 2. Stack Tecnológico y Restricciones

* **HTML:** Estructura limpia utilizando etiquetas semánticas de HTML5 (`<header>`, `<aside>`, `<main>`, `<section>`, `<table>`).
* **CSS:** Estilos aplicados exclusivamente mediante **Tailwind CSS vía CDN**. No se permite CSS personalizado fuera de las utilidades nativas.
* **JavaScript:** Interactividad limitada a **JavaScript Vanilla (JS puro)**. No se permite el uso de frameworks (React, Vue, Angular) ni librerías externas de componentes.
* **Gestión de Datos:** 100% de los datos se encuentran **hardcodeados** en el HTML o en el script de JS. No hay conexiones a APIs ni base de datos en esta etapa.
* **Modo Oscuro:** Implementación global utilizando la estrategia de clases de Tailwind (`dark:`).

---

## 3. Guía de Estilo Visual (Tokens de Tailwind CSS - UI Stitch)

Para que la IA replique con exactitud la gama de colores "Vibrant Tech Minimalist / Vibrant Purple" del prototipo visual, se deben aplicar estrictamente los siguientes tokens:

* **Color Primario (Vibrant Purple - #7C3AED):** Clases `violet-600` o `purple-600`. Utilizado para estados activos, botones principales, enlaces seleccionados y elementos de marca destacados.
* **Color Secundario / Texto Principal (#0F172A):** Clases `slate-900`. Se usa para fuentes principales en modo claro y como contenedor principal en modo oscuro (`dark:bg-slate-900`).
* **Color Terciario / Fondos Suaves (#F5F3FF):** Clases `violet-50` o `purple-50`. Utilizado para fondos de iconos atenuados o estados sutiles.
* **Color Neutral (#64748B):** Clases `slate-500`. Utilizado para etiquetas secundarias, bordes tenues y subtítulos.
* **Fondo General App (Modo Claro):** Fondo gris premium limpio `bg-slate-50`.
* **Fondo General App (Modo Oscuro):** Fondo oscuro profundo `dark:bg-slate-950`.
* **Redondeado de Tarjetas y Contenedores:** Bordes suaves usando obligatoriamente `rounded-2xl` o `rounded-xl`.
* **Sombras:** Efectos difuminados mediante `shadow-sm` o `shadow-indigo-100/40`.

---

## 4. Especificaciones Detalladas por Sección

La interfaz cuenta con una estructura base de dos columnas: un **Sidebar de navegación lateral persistente** a la izquierda (`w-64 fixed h-full bg-white dark:bg-slate-900 border-r border-slate-100 dark:border-slate-800`) y un **Contenedor principal de contenido** a la derecha (`ml-64 p-8 bg-slate-50 dark:bg-slate-950 min-h-screen`) que aloja una barra superior fija (con el Toggle de Modo Oscuro) y las siguientes seis secciones:

### 4.1. Dashboard
* **Grid de Métricas:** Una cuadrícula responsiva (1 columna en móvil, cuadrícula de 4 columnas en pantallas medianas/grandes: `grid grid-cols-1 md:grid-cols-4 gap-6 mb-6`) que contiene exactamente 4 tarjetas de métricas independientes:
    * *Métrica 1:* Ingresos totales generados (este mes).
    * *Métrica 2:* Pérdida total por descuentos y cupones.
    * *Métrica 3:* Número de agentes activos en todos los clientes.
    * *Métrica 4:* Número de agentes actualmente marcados como fallando.
* **Estilo de Tarjetas:** Cada tarjeta posee una estructura `bg-white dark:bg-slate-900 p-6 rounded-2xl border border-slate-100 dark:border-slate-800 shadow-sm`. Debe incluir un icono representativo dentro de un contenedor suave (`bg-violet-50 text-violet-600 p-2.5 rounded-xl dark:bg-violet-950/50 dark:text-violet-400`), una etiqueta superior de texto atenuado (`text-slate-400 dark:text-slate-500 text-xs font-bold uppercase tracking-wider mb-1`), un valor numérico/monetario destacado en tipografía de gran tamaño (`text-2xl font-bold text-slate-900 dark:text-white`), una sombra sutil y un color de acento en el borde o texto que la diferencie (ej. rojo `text-rose-600 bg-rose-50 dark:bg-rose-950/40` para agentes fallando, verde `text-emerald-600 bg-emerald-50` para ingresos).
* **Marcador de Gráfico:** Debajo del grid de métricas, un contenedor (`div`) de ancho completo con fondo sutil (`bg-violet-50/30 dark:bg-slate-900/40 p-12 rounded-2xl border-2 border-dashed border-violet-200 dark:border-slate-800 flex flex-col items-center justify-center min-h-[220px] mb-8`) y una etiqueta de texto centrada que actúe como marcador de posición para el "Gráfico de actividad semanal" con el subtítulo "Visualización dinámica de la carga de trabajo de los agentes".

### 4.2. Gestión de Usuarios
* **Tabla de Datos:** Una estructura `<table>` con diseño responsivo protegido (`overflow-x-auto rounded-2xl border border-slate-100 dark:border-slate-800 bg-white dark:bg-slate-900 shadow-sm`) que lista los usuarios registrados con las siguientes columnas: Nombre, Email, Plan (SaaS) y Estado (Activo / Suspendido).
* **Estilos de Celda y Badges:** La fila de cabecera usa `bg-slate-50 dark:bg-slate-800/60 p-4 text-xs font-bold text-slate-400`. El plan "Enterprise" usa una píldora púrpura sólida (`bg-violet-600 text-white text-xs px-2.5 py-1 rounded-lg font-semibold`), mientras que "Pro Plan" usa una píldora azul translúcida (`bg-blue-100 text-blue-700 dark:bg-blue-950/40 dark:text-blue-400`). El estado "Activo" muestra un punto verde indicador al lado.
* **Menú de Acciones:** La última columna de cada fila contiene un botón con el icono vertical de tres puntos (⋮) en tono `text-slate-400 hover:text-slate-600`. Al hacer clic en él, se debe alternar la visibilidad de un menú flotante absoluto (Dropdown con clases `absolute bg-white dark:bg-slate-900 border rounded-xl shadow-xl z-30`) con las opciones "Ver detalle" y "Eliminar".
* **Modal de Detalle:** Al seleccionar "Ver detalle", se activa un componente de modal superpuesto (Overlay con clases `fixed inset-0 bg-slate-950/60 backdrop-blur-sm z-50 flex items-center justify-center`) que bloquea el fondo. Este modal renderiza de manera estructurada dentro de una caja blanca/oscura elegante (`rounded-2xl max-w-lg w-full p-6`) el registro de perfil completo del usuario. El cierre se realiza mediante un botón dedicado "X" o haciendo clic en el fondo oscurecido (Backdrop).

### 4.3. Gestión de Agentes
* **Listado de Agentes:** Una vista organizada en filas o tarjetas estilizadas con bordes `rounded-2xl` que muestra el nombre del agente, el propietario (empresa cliente), el estado actual (representado con colores: punto verde para activo, gris para inactivo, rojo para fallando) y un panel inferior de habilidades.
* **Lista de Skills Colapsable:** Las habilidades vinculadas a cada agente se encuentran ocultas por defecto. La interfaz incluye un botón expandible (ej. "Ver Skills ▾") que, al ser pulsado, revela la lista de pequeños badges independientes mediante una transición animada suave de altura y opacidad (`transition-all duration-300 ease-in-out`).
* **Configuración y Acciones:** Cada agente dispone del menú de acciones (⋮). La opción "Configurar" abre un modal interactivo que carga el "System Prompt" (instrucciones base de la IA) dentro de un área de texto formateada con fuente monoespacio (`font-mono text-xs bg-slate-50 dark:bg-slate-950 p-4 rounded-xl text-slate-700 dark:text-slate-300 border`) para su revisión.

### 4.4. Catálogo de Skills
* **Bloque Informativo:** Al inicio de la sección, se incluye un banner de contexto o alerta estática con fondo púrpura muy claro (`bg-violet-50 dark:bg-violet-950/30 p-4 rounded-2xl border border-violet-100 dark:border-violet-900/50 mb-6 flex gap-3 text-sm text-violet-800 dark:text-violet-300`) que explica al administrador qué representa una "skill" dentro del ecosistema técnico de AgentHub.
* **Grid del Catálogo:** Una rejilla de tarjetas visuales (`grid grid-cols-1 md:grid-cols-3 gap-6`) donde cada elemento expone el nombre de la skill, una descripción funcional breve de su propósito y un badge numérico destacado en texto púrpura (`text-violet-600 dark:text-violet-400 font-semibold`) que indica de forma llamativa cuántos agentes la tienen integrada actualmente.
* **Acciones de Catálogo:** Cada tarjeta incluye el botón estándar de tres puntos (⋮) con las opciones flotantes de "Ver detalle" y "Eliminar".

### 4.5. Contrataciones de Agentes (Alquileres)
* **Historial de Contratos:** Una tabla detallada que registra las transacciones de alquiler de la plataforma siguiendo el diseño limpio del layout general. Columnas requeridas: Cliente, Agente Alquilado, Skills Contratadas (en formato de etiquetas compactas grises `bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-400 text-xs px-2 py-0.5 rounded`), Fechas del Contrato (Inicio - Fin) e Importe Total Pagado.
* **Dropdown Contextual:** Implementación uniforme del botón de acciones (⋮) en cada una de las filas de la tabla de contratos.
* **Desglose Financiero en Modal:** Al presionar "Ver detalle", se despliega un modal que simula una factura digital limpia, mostrando el desglose pormenorizado de los costes del contrato: la tarifa base del agente junto a la lista de precios individuales por cada skill añadida con líneas divisorias delgadas y un "Total" destacado en `font-bold text-lg text-slate-900 dark:text-white border-t-2 pt-3`.

### 4.6. Log de Errores
* **Tabla de Eventos:** Registro cronológico de fallos del sistema con las siguientes columnas: Marca de tiempo (Timestamp en formato monoespacio `font-mono text-xs text-slate-400`), Nombre del Agente, Tipo de Error y Descripción Breve.
* **Categorización por Badges:** El tipo o la gravedad del error (Crítico, Advertencia, Info) se visualiza a través de píldoras de texto (`badges`). Los errores de tipo "Crítico" se marcan obligatoriamente con un badge rojo brillante (`bg-rose-100 text-rose-700 dark:bg-rose-950/60 dark:text-rose-400 px-2 py-0.5 rounded-full text-xs font-medium`).
* **Resolución de Log:** El menú de acciones (⋮) de cada fila provee la opción "Ver detalle" (que abre un modal con el Stack Trace simulado del error) y la opción "Marcar como resuelto", la cual simula el cambio de estado aplicando dinámicamente mediante JS la clase `opacity-40 line-through` a toda la fila seleccionada.

---

## 5. Inventario de Componentes Reutilizables

Para garantizar la coherencia visual estricta con la paleta de Stitch, se definen los siguientes bloques de interfaz estandarizados:
* **Sidebar de Navegación:** Menú lateral izquierdo fijo. Los enlaces inactivos usan `text-slate-500 hover:bg-slate-50 hover:text-slate-900 dark:text-slate-400 dark:hover:bg-slate-800`. El enlace activo usa obligatoriamente fondo púrpura sólido (`bg-violet-600 text-white shadow-sm shadow-violet-600/10`). Incluye el botón principal **"Nuevo Agente"** estilizado en `bg-violet-600 hover:bg-violet-700 text-white text-sm font-semibold py-2.5 px-4 rounded-xl`.
* **Tarjeta de Métrica:** Caja contenedora con bordes redondeados amplios (`rounded-2xl`), fondo blanco/oscuro, sombra y distribución flex para datos clave.
* **Dropdown de Acciones:** Botón gatillo (⋮) con contenedor de opciones posicionado de forma absoluta (`absolute right-0 mt-2 w-44 bg-white dark:bg-slate-900 border border-slate-100 dark:border-slate-800 rounded-xl shadow-xl z-30 py-1`).
* **Modal Genérico:** Estructura compuesta por un Backdrop fijo difuminado (`fixed inset-0 bg-slate-950/60 backdrop-blur-sm z-50`) y un contenedor central animado para el contenido (`bg-white dark:bg-slate-900 rounded-2xl max-w-lg w-full p-6 shadow-2xl`).
* **Badge de Estado:** Etiquetas pequeñas redondeadas (`rounded-full px-2 py-0.5 text-xs font-medium`) con combinaciones de fondo y texto contrastantes según el estado.
* **Lista Colapsable:** Contenedor interactivo que oculta/muestra elementos hijos mediante clases de transición nativas de Tailwind (`transition-all duration-300`).
* **Toggle de Modo Oscuro:** Interruptor ubicado en la esquina superior derecha de la barra superior fija (Header) junto al buscador, la campana de notificaciones y el avatar circular.

---

## 6. Criterios de Aceptación (Verificables)

1. **Interactividad del Modo Oscuro:** Al hacer clic en el toggle de la barra superior, se debe alternar la clase `dark` en el elemento raíz del documento (`<html>` o `<body>`), cambiando los fondos claros a oscuros (`bg-slate-950`) y los textos oscuros a claros (`text-white`) de forma instantánea en toda la aplicación.
2. **Comportamiento de Dropdowns (⋮):** Al hacer clic en el botón de tres puntos de cualquier fila o tarjeta, el menú correspondiente debe aparecer. Si se hace clic en otro botón de acciones o fuera del menú, el dropdown previamente abierto debe cerrarse de forma automática para evitar solapamientos visuales.
3. **Ciclo de Vida de Modales:** La pulsación de "Ver detalle" o "Configurar" debe remover clases de ocultamiento (`hidden`) del modal objetivo. El modal debe cerrarse de manera inequívoca al pulsar el botón "X" interno, al presionar la tecla `Escape` o al hacer clic en cualquier punto del espacio gris/difuminado del backdrop de fondo.
4. **Animación de la Lista de Skills:** Al pulsar el control de expansión en la sección de agentes, el contenedor de skills debe desplegarse de manera fluida y limpia, sin saltos bruscos en el layout de la página.
5. **Simulación de Datos (Hardcoded):** El prototipo no debe mostrar errores de consola por llamadas fallidas a servidores; todas las interacciones (abrir modales, simular borrados o cierres) deben resolverse localmente modificando clases de visibilidad CSS mediante JavaScript.
6. **Responsividad Base:** El panel debe reordenar sus cuadrículas a una sola columna en pantallas móviles (`sm:grid-cols-1`) e incluir propiedades de desbordamiento horizontal (`overflow-x-auto` junto a `whitespace-nowrap`) en todas sus tablas para evitar que el diseño se rompa de manera lateral.
