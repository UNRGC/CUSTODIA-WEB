# Custodia — Manual de referencia

**Custodia by Mercasoft** · Versión del documento 1.0 · Actualizado el 11 de julio de 2026

Este manual de referencia describe **cada pantalla, campo y acción** de Custodia. Está dirigido
al usuario, pero es más detallado que la guía de usuario: úsalo para consultar el
comportamiento exacto de una opción, resolver un error o entender qué hace cada botón.

> Para una guía introductoria paso a paso, consulta la **Guía de usuario**. Aquí encontrarás
> el detalle campo por campo.

---

## Índice

1. [Conceptos y arquitectura](#1-conceptos-y-arquitectura)
2. [Licencia](#2-licencia)
3. [Configuración](#3-configuracion)
4. [Clave de cifrado](#4-clave-de-cifrado)
5. [Empresas](#5-empresas)
6. [Nube (OneDrive)](#6-nube-onedrive)
7. [Programación de respaldos](#7-programacion-de-respaldos)
8. [Avisos por correo](#8-avisos-por-correo)
9. [Archivos y recuperación](#9-archivos-y-recuperacion)
10. [Bitácora](#10-bitacora)
11. [Servicio en segundo plano](#11-servicio-en-segundo-plano)
12. [Estados y mensajes](#12-estados-y-mensajes)
13. [Solución de problemas](#13-solucion-de-problemas)
14. [Preguntas frecuentes](#14-preguntas-frecuentes)
15. [Glosario](#15-glosario)

---

## 1. Conceptos y arquitectura

Custodia se compone de dos partes que trabajan juntas:

| Componente | Qué es | Función |
|---|---|---|
| **Aplicación** | La ventana que abres y usas | Configurar, consultar y lanzar acciones. |
| **Servicio en segundo plano** | Un Servicio de Windows | Ejecuta los respaldos programados aunque la ventana esté cerrada. |

- La **aplicación** se comunica con el **servicio** para validar la licencia, guardar la
  configuración y controlar los respaldos.
- El **servicio** debe estar **Activo** para que los respaldos automáticos se ejecuten.
- No es necesario mantener la ventana abierta, **pero el equipo debe estar encendido** a la hora
  programada.

**Flujo de un respaldo:** el servicio se conecta a tu servidor → genera la copia de cada empresa
seleccionada → la **cifra** con tu clave → la guarda en las carpetas locales → sube una copia a la
nube (si está conectada) → registra el resultado en la Bitácora → envía el aviso por correo.

---

## 2. Licencia

La licencia habilita el uso de Custodia. Mientras no haya una licencia válida y vigente, el resto
de la aplicación permanece bloqueado.

### Activar una licencia

1. Abre la sección **Más información**.
2. Escribe el **Número de serie** que te entregaron.
3. Presiona **Validar**.
4. Aparecerá el diálogo de **Términos y condiciones**. Debes:
   - Abrir y leer los términos (enlace **"Leer términos y condiciones"**).
   - Marcar la casilla **"He leído y acepto los términos y condiciones"**.
   - Presionar **Continuar**. El botón permanece deshabilitado hasta que marques la casilla.
5. Si aceptas, Custodia valida la licencia contra el servidor y muestra el resultado.

> Si cancelas el diálogo o no aceptas los términos, **la licencia no se activa**.

### Campos de licencia

| Campo | Descripción |
|---|---|
| **Número de serie** | El identificador de tu licencia. Se bloquea mientras la licencia esté vigente. |
| **Propietario** | Nombre a quien está registrada la licencia. |
| **Vigencia** | Rango de fechas en que la licencia es válida (Desde / Hasta). |
| **Estado** | Estado actual: Válida, Activa, Revocada, Expirada, Suspendida, etc. |

### Quitar licencia

Usa **Quitar licencia** para **liberar la activación de este equipo** y poder usar la licencia en
otra computadora.

- Libera la activación en el servidor y borra la licencia local.
- La aplicación vuelve a quedar **bloqueada** hasta validar una licencia de nuevo.
- Si la liberación falla en el servidor, la licencia **no** se borra localmente (para no dejar la
  activación huérfana).

> **Límite de activaciones:** si al validar aparece "Se alcanzó el límite de activaciones", libera
> otro equipo con **Quitar licencia** o contacta a soporte.

---

## 3. Configuración

Centro de toda la puesta a punto. Cambios aquí afectan a todos los respaldos.

### Conexión al servidor

| Campo | Descripción |
|---|---|
| **Servidor** | Dirección del servidor de base de datos (nombre o IP, e instancia si aplica). |
| **Usuario** | Usuario con permisos para leer y respaldar las bases. |
| **Contraseña** | Contraseña del usuario. |
| **Probar conexión** | Verifica los datos. **Verde** = correcto; **rojo** = revisa datos o red. |

Escribe los datos que te dio tu administrador y presiona **Probar conexión** antes de continuar.

### Carpetas de respaldo

Selecciona las carpetas locales donde se guardan las copias. Si no sabes cuáles usar, deja las
predeterminadas. Asegúrate de que tengan **espacio suficiente**.

---

## 4. Clave de cifrado

Los respaldos se guardan **cifrados**. Sin la clave correcta **no se pueden recuperar**.

- Custodia **genera una clave automáticamente desde el primer arranque**; puedes conservarla,
  **generar** otra o **escribir la tuya**.
- Usa **Copiar clave** y guárdala en un lugar seguro (como la llave de una caja fuerte).
- Cada respaldo se cifra con la clave **vigente al momento de crearlo**.

### Historial de claves

Si **cambias de clave**, los respaldos anteriores siguen cifrados con la clave anterior. Consulta
**Historial** para ver las claves previas y poder recuperar respaldos antiguos.

> **Importante:** si pierdes una clave, los respaldos cifrados con ella **no** se pueden recuperar
> ni regenerar. Guárdala siempre antes de cambiarla.

---

## 5. Empresas

Lista de todas las empresas/bases de datos encontradas en tu servidor.

- Cada fila muestra **Empresa**, **Base de datos**, **Tipo**, **Relacionadas** (empresas que se
  respaldan juntas por compartir sus documentos digitales), **Tamaño**, **Ruta de respaldo** y los
  controles de programación (**Personalizado** y **Automático**).
- Activa el interruptor **Automático** de las empresas que quieras incluir en la programación
  global, o asígnales un horario **Personalizado** desde su fila. Las que no tengan programación
  no se respaldan automáticamente.
- Desde la fila también puedes lanzar un **respaldo manual** o **restaurar** un respaldo de esa
  empresa en cualquier momento.
- Si tienes muchas empresas, empieza por las más importantes.
- Puedes usar **Calcular** (aquí o en Inicio) para estimar el espacio que ocuparán en la nube y
  elegir cuántas copias conservar.

---

## 6. Nube (OneDrive)

Guardar una copia en la nube te protege aunque el equipo falle. Custodia usa **OneDrive**.

### Conectar

1. En **Configuración**, ve a la sección **Nube**.
2. Presiona **Conectar**. Se abre la ventana de inicio de sesión de Microsoft.
3. Inicia sesión con la cuenta donde quieres guardar las copias.
4. Cuando la cuenta aparezca vinculada, cada respaldo se subirá automáticamente.

### Controles

| Control | Función |
|---|---|
| **Conectar / Desconectar** | Vincula o desvincula la cuenta de OneDrive. |
| **Cuenta conectada** | Muestra el correo de la cuenta actualmente vinculada. |
| **Calcular** | Estima el espacio necesario y las copias a conservar. |
| **Copias a conservar** | Número de respaldos que se mantienen; los más antiguos se eliminan al superar el límite. |

> El cálculo de espacio es **aproximado**: cada respaldo se estima en ~50 % del tamaño de la base
> por efecto de la compresión.

---

## 7. Programación de respaldos

Define cuándo se ejecutan los respaldos automáticos.

| Campo | Descripción |
|---|---|
| **Frecuencia** | Semanal o Mensual. |
| **Días** | Días de la semana en que se respalda. Usa **"Todos"** para marcarlos de una vez. |
| **Hora** | Hora de ejecución. Se recomienda una hora sin actividad (p. ej. de madrugada). |

- Deja el **equipo encendido** a la hora programada.
- El **servicio en segundo plano** debe estar **Activo** (ver §11).
- Puedes lanzar un **respaldo manual** en cualquier momento, sin esperar al horario.

---

## 8. Avisos por correo

Custodia envía un correo con el resultado de cada respaldo (exitoso o con error).

1. En **Configuración**, agrega los **destinatarios** (uno o varios correos).
2. Presiona **Correo de prueba** para confirmar que llega.
3. Si no llega, revisa que los correos estén bien escritos y la carpeta de **correo no deseado**.

---

## 9. Archivos y recuperación

La sección **Archivos** lista los respaldos disponibles, tanto **en la nube (OneDrive)** como
**locales**, ordenados por fecha.

| Columna | Descripción |
|---|---|
| **Nombre** | Identificador del respaldo. |
| **Tamaño** | Espacio que ocupa. |
| **Modificado** | Fecha y hora de creación. |

### Acciones en Archivos

| Acción | Descripción |
|---|---|
| **Descargar** | Descarga los respaldos seleccionados de la nube a la carpeta de respaldos local. |
| **Subir a la nube** | Sube (o resube) un respaldo local a OneDrive. Útil si la subida automática falló. |
| **Eliminar** | Elimina los respaldos seleccionados (de la nube o del equipo, según la lista). |

### Recuperar un respaldo

La restauración se realiza desde la pantalla **Inicio** (o desde la fila de la empresa en
**Empresas**), no desde Archivos:

1. En **Inicio**, dentro de **Acciones rápidas**, presiona **Restaurar**.
2. Selecciona el respaldo por su **fecha**. Custodia busca primero en la carpeta local y, si no
   hay copias locales, muestra las de la nube: se **descargan automáticamente** al restaurar (el
   avance se ve en la Bitácora). También puedes usar **Examinar archivo…** para elegir un
   respaldo guardado en otra ubicación.
3. Revisa la **información a restaurar** y confirma.

> **La recuperación necesita la clave de cifrado** con la que se creó ese respaldo. Si usaste una
> clave distinta en su momento, recupérala desde el **Historial de claves** (§4).

> **Advertencia:** restaurar **sobrescribe** datos existentes. Verifica el respaldo y el destino
> antes de confirmar.

### Recuperar instancia completa

Para reconstruir un equipo tras una pérdida (o migrar a uno nuevo), el diálogo Restaurar ofrece
**Recuperar instancia completa**:

1. Custodia **descarga de la nube** los respaldos que falten en la carpeta local.
2. Restaura primero las **bases de datos generales** (los catálogos de cada sistema).
3. Muestra la **lista de empresas encontradas** con su respaldo más reciente; las que no tienen
   respaldo aparecen marcadas con una advertencia.
4. Deja **seleccionadas** las empresas que quieras conservar y restaurar. Las que dejes **sin
   seleccionar se eliminan de la lista de empresas de su sistema** (se pide confirmación antes).

> Las empresas sin respaldo no se pueden restaurar: si las dejas seleccionadas, solo se conservan
> en la lista de su sistema.

---

## 10. Bitácora

Registro de todo lo que Custodia ha hecho. Úsala para confirmar de un vistazo que todo va bien.

| Columna | Descripción |
|---|---|
| **Fecha y hora** | Cuándo ocurrió la operación. |
| **Empresa** | Base de datos afectada. |
| **Operación** | Respaldo, subida a la nube, recuperación, etc. |
| **Estado** | Resultado de la operación. |
| **Mensaje** | Detalle o motivo del error, si lo hubo. |

- **Verde (éxito):** el respaldo se completó sin problemas.
- **Rojo (error):** algo falló. Lee el mensaje; si no lo resuelves, contacta a soporte.

> Al terminar cualquier operación (respaldo o restauración), Custodia muestra una **notificación
> dentro de la aplicación**, sin importar en qué pantalla estés.

---

## 11. Servicio en segundo plano

Desde la sección **Más información** controlas el Servicio de Windows que ejecuta los respaldos.

| Estado | Significado |
|---|---|
| **Activo** | El servicio funciona; los respaldos programados se ejecutarán. |
| **Detenido** | El servicio está parado; **no** habrá respaldos automáticos. |
| **No instalado** | El servicio no está instalado; contacta a soporte. |
| **Cambiando de estado…** | Operación en curso; espera a que termine. |

| Botón | Cuándo está disponible | Acción |
|---|---|---|
| **Iniciar** | Solo si el servicio está Detenido | Arranca el servicio. |
| **Detener** | Solo si el servicio está Activo | Detiene el servicio. |
| **Reiniciar** | Solo si el servicio está Activo | Reinicia el servicio. |

> Estas acciones requieren permisos de administrador; Windows puede pedir confirmación.

---

## 12. Estados y mensajes

### Estados de licencia

| Estado | Significado |
|---|---|
| Válida / Activa | La licencia es correcta y vigente. |
| Pendiente | Aún no activada o en proceso. |
| Expirada | Terminó su vigencia. |
| Suspendida | Temporalmente inhabilitada. |
| Revocada | Cancelada por el proveedor. |
| No válida | No corresponde o no se reconoce. |

### Motivos de rechazo al validar

| Mensaje | Qué hacer |
|---|---|
| No se encontró la licencia | Revisa el número de serie. |
| La licencia no corresponde a esta aplicación | Usa la licencia correcta de Custodia. |
| La licencia no corresponde a este cliente | Verifica con tu distribuidor. |
| La licencia fue revocada | Contacta a soporte. |
| La licencia está suspendida | Contacta a soporte. |
| La licencia aún no está vigente | Espera a la fecha de inicio. |
| La licencia expiró | Renueva la licencia. |
| Se alcanzó el límite de activaciones | Libera un equipo con **Quitar licencia** o contacta a soporte. |
| Este equipo no tenía una activación registrada | Ya estaba libre; puedes validarla en otro equipo. |

---

## 13. Solución de problemas

| Síntoma | Posible causa / solución |
|---|---|
| **"Sin conexión con el servicio"** | El servicio en segundo plano está detenido o no instalado. Ve a §11 e **Iniciar**. |
| **La prueba de conexión sale en rojo** | Revisa servidor, usuario, contraseña y la red. |
| **No se ejecutan los respaldos programados** | El equipo estaba apagado a la hora, o el servicio no está Activo. |
| **No puedo recuperar un respaldo** | Falta la clave de cifrado con la que se creó. Búscala en el Historial de claves. |
| **No llegan los correos de aviso** | Destinatarios mal escritos o el aviso cayó en correo no deseado. Usa **Correo de prueba**. |
| **La app está bloqueada** | No hay licencia válida vigente. Valida una licencia en **Más información**. |
| **"Se alcanzó el límite de activaciones"** | Libera otro equipo con **Quitar licencia**. |
| **Falla la subida a la nube** | Custodia la reintenta sola varias veces; el respaldo local queda a salvo. Si aun así falla, revisa la conexión y el espacio de OneDrive, y usa **Subir a la nube** en Archivos → Respaldos locales para reintentarla. |

---

## 14. Preguntas frecuentes

**¿Tengo que dejar la aplicación abierta?**
No. La ventana puede estar cerrada, pero el equipo debe estar **encendido** a la hora programada.

**Perdí mi clave de cifrado, ¿qué hago?**
La clave es indispensable y no se puede regenerar para copias antiguas. Si aún tienes acceso a
Custodia, cópiala desde Configuración. Si la perdiste, contacta a tu administrador o a soporte.

**¿Puedo hacer un respaldo ahora mismo, sin esperar al horario?**
Sí, puedes iniciar un respaldo manual en cualquier momento.

**No me llegan los correos de aviso.**
Verifica los destinatarios en Configuración, usa **Correo de prueba** y revisa el correo no deseado.

**¿Qué pasa si mi equipo se daña?**
Si conectaste OneDrive, tienes una copia en la nube. En un equipo nuevo instala Custodia, conecta
la misma cuenta de OneDrive y usa **Recuperar instancia completa** con tu clave de cifrado: los
respaldos se descargan y se restauran solos (§9).

**¿Puedo mover mi licencia a otra computadora?**
Sí. Usa **Quitar licencia** en el equipo actual para liberarla y luego valídala en el nuevo equipo.

---

## 15. Glosario

| Término | Definición |
|---|---|
| **Respaldo** | Copia de seguridad de una base de datos. |
| **Clave de cifrado** | Contraseña que protege los respaldos; necesaria para recuperarlos. |
| **Activación** | Vínculo entre una licencia y un equipo. |
| **Vigencia** | Periodo en que la licencia es válida. |
| **Servicio** | Proceso de Windows que ejecuta los respaldos en segundo plano. |
| **Bitácora** | Historial de operaciones y sus resultados. |
| **Nube** | Almacenamiento remoto (OneDrive) de una copia de los respaldos. |
| **Retención** | Número de copias que se conservan antes de borrar las más antiguas. |

---

*Custodia by Mercasoft — ¿Necesitas ayuda que no está aquí? Contacta a tu administrador o a
soporte técnico.*
