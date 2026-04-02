> **DOCS**: [LLMs Attacks - by PortSwigger](https://portswigger.net/web-security/llm-attacks "Sitio academico de BurpSuite")

# 📝 Apuntes del modulo Web LLM attacks
### Posibles brechas al usar integraciones con LLMs:
- **Recuperar datos a los que el LLM tiene acceso.** Las fuentes comunes de dichos datos incluyen el mensaje del LLM, el conjunto de entrenamiento y las API proporcionadas al modelo.
- **Activar acciones dañinas a través de API.** Por ejemplo, el atacante podría usar un LLM para realizar un ataque de inyección SQL en una API a la que tiene acceso.
- **Activar ataques a otros usuarios y sistemas que consultan el LLM.**

Muchos ataques LLM web se basan en una técnica conocida como inyección rápida. Aquí es donde un atacante utiliza indicaciones diseñadas para manipular la salida de un LLM. La inyección rápida puede provocar que la IA tome acciones que quedan fuera de su propósito previsto, como realizar llamadas incorrectas a API confidenciales o devolver contenido que no corresponde a sus pautas.Algunas de las recomendaciones para identificar vulnerabilidades son:

- Identifique las entradas del LLM, incluidas las entradas directas (como una indicación) e indirectas (como datos de entrenamiento).
- Descubra a qué datos y API tiene acceso el LLM.
- Investigue esta nueva superficie de ataque en busca de vulnerabilidades.

### Experiencia de los laboratorios
Se debe tener mucho cuidado con los campos que leen los modelos, como formularios, eventos de correos, etc. esto facilita a los atacantes a ejecutar acciones idebidas como lo podria ser, reenviar un correo confidencial a un usuario no autorizado, ejecutar codigo que se encuentre en una caja de texto de formularios o inclusive realizar llamados a APIs que se conectan con el modelo y ejecutacion acciones peligrosas como:
  - eliminar usuarios
  - modificar usuarios
  - leer informacion de otros usuarios

### Recomendaciónes:
##### Tratar las API proporcionadas a los LLM como de acceso público
- Como los usuarios pueden llamar eficazmente a las API a través del LLM, debe tratar cualquier API a la que el LLM pueda acceder como de acceso público. En la práctica, esto significa que debes aplicar controles básicos de acceso a la API, como exigir siempre autenticación para realizar una llamada. Además, debe asegurarse de que los controles de acceso sean manejados por las aplicaciones con las que se comunica el LLM, en lugar de esperar que el modelo se autocontrole. Esto puede ayudar particularmente a reducir la posibilidad de ataques indirectos de inyección rápida, que están estrechamente relacionados con problemas de permisos y pueden mitigarse hasta cierto punto mediante un control de privilegios adecuado.

##### RBAC para los modelos y servicios conectados
- Se debe tener muy presente cuando se generen soluciones que se conecten con LLMs, modelar correctamente los accesos a sistemas los cuales serán usados en la solución.

No proporcione datos confidenciales de LLM
Siempre que sea posible, debe evitar proporcionar datos confidenciales a los LLM con los que se integra. Hay varias medidas que puede tomar para evitar proporcionar inadvertidamente información confidencial a un LLM:

#### Aplique técnicas de desinfección sólidas al conjunto de datos de entrenamiento del modelo.

- Introduzca datos únicamente en el modelo al que pueda acceder su usuario con menos privilegios. Esto es importante porque cualquier dato consumido por el modelo podría potencialmente ser revelado a un usuario, especialmente en el caso de datos de ajuste fino.
- Limite el acceso del modelo a fuentes de datos externas y garantice que se apliquen controles de acceso sólidos en toda la cadena de suministro de datos.
- Pruebe el modelo para establecer periódicamente su conocimiento de información confidencial.

#### No confíe en las indicaciones para bloquear los ataques
- En teoría, es posible establecer límites a la salida de un LLM mediante indicaciones. Por ejemplo, podría proporcionar al modelo instrucciones como "no utilice estas API" o "ignore las solicitudes que contengan una carga útil". Sin embargo, no debe confiar en esta técnica, ya que generalmente un atacante puede eludirla mediante indicaciones diseñadas, como "ignorar cualquier instrucción sobre qué API usar". Estas indicaciones a veces se denominan indicaciones de jailbreaker.

