# Sistema-Tunomatico

## 📌 Descripción general del sistema

Tunomático es un sistema de gestión de turnos digitales diseñado para optimizar la atención al público en entornos donde es necesario organizar la asignación y el seguimiento de turnos, como hospitales, instituciones públicas, bancos y centros de servicios.
Permite a los usuarios solicitar turnos de forma remota o presencial, visualizar los horarios disponibles y cancelar citas cuando sea necesario. El personal de atención puede gestionar el flujo de turnos, registrar la atención brindada y priorizar casos especiales. Finalmente, los administradores configuran parámetros clave del sistema, como servicios ofrecidos, horarios de funcionamiento y lógica de atención prioritaria.

Este sistema busca eliminar la necesidad de filas físicas, reducir tiempos de espera, y mejorar la calidad del servicio ofrecido a los ciudadanos o clientes.
***
## 🔍 Objetivos del Modelado
El objetivo principal del modelado arquitectónico del sistema Tunomático es representar de manera estructurada y detallada todos los aspectos funcionales y técnicos de la solución, desde su lógica de negocio hasta su despliegue físico. Para ello, se emplean técnicas de diseño orientado a objetos y se aplican patrones de diseño reconocidos.

Los objetivos específicos del modelado son:

📘 Visualizar los requerimientos funcionales del sistema mediante un diagrama de casos de uso UML, incluyendo actores y relaciones como `<<include>>`  y 
`<<extend>>`.

🧩 Diseñar la estructura lógica del sistema utilizando un diagrama de clases UML con atributos, métodos, relaciones y la aplicación de los patrones Singleton, Prototype y Adapter.

🖥 Representar la arquitectura física del sistema con un diagrama de implementación UML, donde se muestren nodos físicos, componentes del software y sus conexiones.

💡 Justificar decisiones arquitectónicas y patrones utilizados, facilitando el paso del diseño a la implementación técnica en un entorno real.
***
## 🎯 Imagen del diagrama de casos de uso + descripción
![image](https://github.com/user-attachments/assets/0abc61cc-4330-4c9b-83cc-f9075505349b)

### 📌 Descripción general
El diagrama de casos de uso representa las principales funcionalidades del sistema Tunomático desde la perspectiva de los usuarios externos (actores). Este modelo ayuda a visualizar cómo interactúan los distintos tipos de usuarios con el sistema y cuáles son los servicios clave que se ofrecen, asegurando que se satisfagan todos los requisitos funcionales del sistema.

#### 👥 Actores identificados
- Usuario: Persona que solicita turnos, los visualiza o cancela.
- Personal de Atención: Operador que llama turnos, registra atención y gestiona prioridades.
- Administrador: Encargado de la configuración del sistema y parámetros de atención.

#### 🧩 Casos de uso destacados y relaciones aplicadas
- Solicitar Turno	Usuario	`<<include>>` Ver Turnos Disponibles
- Cancelar Turno	Usuario	`<<extend>>` Solicitar Turno
- Llamar Siguiente Turno	Personal de Atención	`<<extend>>` Gestionar Prioridades
- Configurar Sistema	Administrador	Relación directa

#### ✅ Justificación de las relaciones aplicadas
- Solicitar Turno incluye (`<<include>>`) el caso Ver Turnos Disponibles, ya que es imprescindible mostrar las opciones antes de seleccionar un turno.
- Cancelar Turno extiende (`<<extend>>`) de Solicitar Turno porque solo puede realizarse si se ha solicitado un turno previamente.
- Llamar Siguiente Turno extiende (`<<extend>>`) de Gestionar Prioridades, dado que en ciertos contextos (emergencias, turnos VIP) se pueden alterar los criterios de llamado.

### 🌟 Relación destacada
La relación Solicitar Turno `<<include>>` Ver Turnos Disponibles es clave porque refleja la obligatoriedad de revisar la disponibilidad antes de hacer una solicitud. Esta relación garantiza que el sistema guíe correctamente al usuario a través del flujo funcional.
***
## 🧩 Imagen del diagrama de clases + justificación de patrones
![image](https://github.com/user-attachments/assets/5c636d30-5346-4c29-9324-a799e79b8569)
### 🧩 Justificación Arquitectónica
El modelo de clases del sistema Tunomático fue diseñado bajo principios de cohesión alta y acoplamiento bajo, lo que favorece la mantenibilidad y la reutilización de componentes. Se identificaron las entidades principales del dominio (Usuario, Turno, GestorTurnos, etc.) y se organizaron con atributos, métodos y relaciones que reflejan el comportamiento esperado.
Además, se aplicaron patrones de diseño clásicos que refuerzan la solidez y extensibilidad del sistema ante cambios futuros.

## 🎯 Patrones Aplicados y Justificación
#### 🔹 Singleton
Aplicado en: GestorTurnos

Intención arquitectónica: Garantizar que exista una única instancia encargada de administrar los turnos, evitando duplicación de lógica y manteniendo el estado compartido de la aplicación.

Justificación: Como el sistema requiere un control centralizado del flujo de turnos y prioridad, se necesita una única fuente de verdad. El patrón Singleton asegura esto, ofreciendo acceso global controlado.

#### 🔹 Prototype
Aplicado en: Turno

Intención arquitectónica: Permitir la clonación de objetos Turno ya configurados, para evitar repetir estructuras al generar nuevos turnos con características similares.

Justificación: Aumenta la eficiencia al crear turnos nuevos sin reconfigurarlos manualmente, y facilita la duplicación segura de turnos sin acoplamiento directo al constructor original.

#### 🔹 Adapter
Aplicado en: NotificadorAdapter

Intención arquitectónica: Adaptar una interfaz de servicio externo (ServicioSMS) al sistema interno a través de una interfaz común (INotificador).

Justificación: Facilita la integración de distintos proveedores de notificaciones sin afectar el núcleo del sistema, favoreciendo la escalabilidad y el principio de inversión de dependencias.
***
## 🛠 Imagen del diagrama de implementación + decisiones técnicas
![image](https://github.com/user-attachments/assets/acd61307-91cb-4ef6-9094-6ce87bc85a3f)
## 🗂 Despliegue Físico y Decisiones Técnicas

#### El sistema se despliega en una arquitectura distribuida compuesta por:
- Un cliente web (navegador) que interactúa con el sistema mediante una interfaz HTML/JavaScript.
- Un servidor de aplicaciones, que contiene la lógica del negocio y los módulos que implementan los patrones de diseño.
- Un servidor de base de datos, encargado de almacenar la información persistente del sistema (usuarios, turnos, registros).
- Se optó por una arquitectura de 3 capas (presentación, lógica, datos) para separar responsabilidades.
- Se utilizaron patrones estructurales y creacionales para garantizar la modularidad del sistema.
- La implementación considera componentes desacoplados como el adaptador de notificaciones, lo cual facilita su mantenimiento.
- La base de datos puede estar alojada en un servidor local o en la nube, y la API es accesible por HTTP/REST.
***
## 🧠 Reflexiones finales del modelado

El proceso de modelado del sistema Tunomático ha permitido representar de forma precisa la estructura y el comportamiento del sistema desde una perspectiva orientada a objetos, siguiendo principios sólidos de diseño y buenas prácticas arquitectónicas.

Durante el modelado, se logró:

Comprender y abstraer los requerimientos funcionales mediante el diagrama de casos de uso, destacando relaciones críticas como `<<include>>` y `<<extend>>`.

Organizar la lógica de negocio en un modelo de clases robusto, con clases conectadas, atributos claros, métodos definidos y la integración efectiva de patrones como Singleton, Prototype y Adapter.

Diseñar un despliegue físico realista, que respeta la separación de capas y facilita el mantenimiento e integración futura con servicios externos.

Documentar decisiones técnicas que reflejan no solo cómo debe funcionar el sistema, sino también por qué se eligió cada estructura y patrón aplicado.

El modelado no solo ha sido una herramienta de diseño, sino también un ejercicio de reflexión arquitectónica, que prepara una base sólida para la futura implementación del sistema. Además, el uso de estándares UML y patrones de diseño favorece la comunicación entre los distintos perfiles del equipo de desarrollo.
