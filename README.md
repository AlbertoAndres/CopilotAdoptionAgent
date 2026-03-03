> **Nota**
> Esta es la **versión en español (México)** de este agente, **portada y adaptada desde el original** disponible en:  
> https://github.com/dokline/CopilotAdoptionAgent

# Copilot Adoption Agent

## Descripción general

El **Copilot Adoption Agent (1.1.0.7)** es una solución empaquetada de **Copilot Studio**, diseñada para ayudar a las organizaciones a acelerar la adopción de **Copilot Chat** y **Microsoft 365 Copilot** mediante campañas de comunicación automatizadas y estructuradas.

Este agente entrega un programa completo de adopción por correo electrónico de **30 días**, listo para ejecutarse, enviando a los usuarios **tres correos dirigidos por semana** que desarrollan progresivamente habilidades de Copilot en los niveles **Beginner**, **Intermediate** y **Advanced**.

Aunque el agente incluye orientación opcional de enablement para administradores, su propósito principal es **automatizar las comunicaciones de adopción**, no administrar licenciamiento ni aprovisionamiento.

---

## Qué hace este agente

- Automatiza la entrega de una campaña de adopción de Copilot por correo electrónico de 30 días.
- Envía 3 correos por semana (martes, miércoles y jueves a las 10:00 AM hora Central).
- Envía los correos desde el buzón autenticado del usuario que realiza la solicitud dentro de la experiencia del agente (author).
- Proporciona plantillas de correo preescritas tanto para **Copilot Chat** como para **Microsoft 365 Copilot**.
- Soporta rutas de aprendizaje **Beginner**, **Intermediate** y **Advanced**.
- Incluye flujos de prueba para validar la configuración del entorno.
- Ofrece Q&A opcional para enablement de usuarios y recomendaciones de adopción, aprovechando los **Enablement Guides** de ambos productos como fuentes de conocimiento.

---

## Componentes principales incluidos en la solución

### Copilot Studio Agent

Interfaz conversacional utilizada para configurar campañas, seleccionar el tipo de producto, elegir el nivel de habilidades y definir la audiencia objetivo.

### Prompts y lógica preconstruidos

Incluye toda la lógica de decisión, ramificaciones y pasos de configuración de campaña necesarios para ejecutar el programa de adopción.

### Biblioteca de plantillas de correo

Plantillas de comunicación completamente desarrolladas para:

- Beginner  
- Intermediate  
- Advanced  

Disponibles tanto para **Copilot Chat** como para **Microsoft 365 Copilot**.

---

## Power Automate (Agent) Flows (12 en total)

La solución incluye **12 flujos de Power Automate**, agrupados en conjuntos de **Test** y **Production**.

### 6 flujos de prueba (validación del entorno)

Permiten validar:

- Formato y renderizado de correos
- Selección correcta de plantillas
- Enrutamiento a las listas de distribución objetivo
- Autenticación del buzón personal del remitente
- Lógica de tiempos variables para pruebas (retrasos en minutos)
- Preparación general antes de lanzar una campaña en vivo

### 6 flujos de producción

Ejecutan la campaña real de 30 días:

- Envían correos martes, miércoles y jueves a las 10:00 AM hora Central  
- Inician en la siguiente ventana planificada según la interacción con el agente  
- Usan el producto seleccionado (**Copilot Chat** o **Microsoft 365 Copilot**)  
- Usan el nivel de habilidades seleccionado (**Beginner**, **Intermediate**, **Advanced**)  
- Envían correos desde el buzón autenticado del author  
- Incluyen correos de recordatorio para dar seguimiento al progreso de adopción  

Cada flujo de producción corresponde a una combinación específica de **producto + nivel**, manteniendo campañas aisladas, predecibles y fáciles de administrar. Se pueden ejecutar múltiples campañas en paralelo y todas son independientes entre sí.

---

## Prerrequisitos y roles requeridos

### Requisitos del entorno

- Tenant de **Microsoft 365** con **Copilot Studio** habilitado
- Acceso a un entorno de **Dataverse** (default o custom)
- Buzón de usuario con capacidad de envío de correo (cuenta Microsoft 365 del author)

### Requisitos de roles

Para importar y configurar la solución, se requiere uno de los siguientes roles en el entorno destino:

- Environment Admin  
- System Administrator  
- Copilot Studio Administrator  
- Power Platform Admin  

Para enviar correos desde la cuenta del author, este también debe:

- Autenticar el conector de **Outlook** (durante la ingestión)
- Contar con licencia de **Microsoft 365 Copilot**
- Tener permiso para enviar correos a la lista de distribución objetivo

---

## Importar el Copilot Adoption Agent en Copilot Studio

### Descargar el paquete desde GitHub

1. Selecciona **Code** > **Download Zip**
2. Se descargará `CopilotAdoptionAgent_1_1_0_7.zip`
5. **No extraigas este archivo**, se usa directamente en formato zip

---

### Abrir Copilot Studio

Navega a:  
https://copilotstudio.microsoft.com  

Selecciona el entorno de **Dataverse** donde se instalará el agente.

### Importar la solución (paso crítico)

1. Ve a **…** en el panel izquierdo y selecciona **Solutions**
2. Selecciona **Import solution**
3. Carga el archivo `.zip`
4. Expande **Advanced Settings**
5. Desmarca **Enable all workflows and connections included in the solution**  
   Este paso es crítico para evitar que los flujos se activen antes de validar la autenticación del buzón.
6. Continúa con la importación

---

## Verificar Connection Resources

1. Abre la solución **Copilot Adoption Agent**
2. Selecciona **Connection Resources**
3. Localiza la conexión `cr_Outlook`
4. Verifica que esté asociada a la cuenta del author

---

## Uso del Copilot Adoption Agent

Dentro del agente, el author puede:

- Seleccionar el producto (**Copilot Chat** o **Microsoft 365 Copilot**)
- Seleccionar el nivel de habilidades
- Proporcionar la lista de distribución
- Confirmar el calendario de la campaña

### Ejecutar flujos de prueba (recomendado)

Validan:

- Formato de correos
- Enrutamiento
- Permisos
- Exactitud de plantillas

### Activar la campaña de producción

Una vez validado, se inicia el flujo de producción. Los correos se enviarán automáticamente durante 30 días desde el buzón del author.

No es obligatorio publicar formalmente el agente. Si quien lo ingesta es quien lo opera, se puede usar la experiencia **Test** directamente en Copilot Studio.

---

## Comandos principales

### `Prueba iniciar programador de correos`

Ejecuta la campaña en modo prueba:

- Valida formato y enrutamiento
- Prueba autenticación del buzón
- Permite controlar retrasos en minutos  
  Ejemplo: enviar correos cada 5 minutos

### `Iniciar programador de correos`

Inicia la campaña completa de 30 días:

- Producto seleccionado
- Nivel de habilidades seleccionado
- Lista de distribución configurada  
  Para múltiples correos, usar punto y coma (`;`) según el formato de Outlook
- Calendario fijo martes, miércoles y jueves a las 10:00 AM hora Central

---

## Preguntas y recomendaciones

El agente también puede responder sobre:

- Mejores prácticas de adopción de Copilot
- Tips de onboarding
- Estrategias de comunicación
- Dudas generales de enablement

Funciona tanto como motor de campañas como asesor de adopción.

---

## Notas de entrega de correos

- Los correos se envían desde el buzón autenticado del author
- Las campañas son independientes por producto y nivel
- Se pueden ejecutar múltiples campañas en paralelo
- El horario es fijo: martes, miércoles y jueves a las 10:00 AM hora Central

---

## Opciones de personalización

Al ser un agente **unmanaged**, los admins pueden personalizar:

- Plantillas HTML de correo
- Tiempos y cadencia
- Branding y formato
- Contenido adicional de enablement

---

## Soporte y troubleshooting

Si los correos no se envían:

- Verifica que el conector de Outlook esté conectado
- Asegura que la lista de distribución acepte envíos automatizados
- Confirma que los flujos de prueba se ejecuten correctamente
