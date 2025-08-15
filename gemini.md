Claro, he ajustado y refinado el documento. El objetivo ha sido hacerlo más generalista, profesional y, crucialmente, añadir una sección que aborda cómo interactuar cuando se trabaja con archivos de código extensos, considerando las limitaciones de tokens de los modelos de lenguaje.

La nueva estructura es más robusta y puede ser usada como una plantilla estándar para cualquier proyecto de refactorización con un asistente de IA.

-----

# 🤖 Directiva para Asistente de IA: Análisis y Refactorización de Código

## Misión: Mejora de Calidad y Arquitectura de Software

**Resumen:** Este documento sirve como directiva central para el asistente de IA. Su propósito es definir el contexto, los objetivos y las tareas solicitadas para el análisis y refactorización de un proyecto de software. Úsalo como la fuente principal de verdad para entender el estado actual y los objetivos de mejora.

-----

### **PARTE I: CONTEXTO DEL PROYECTO (ESTADO ACTUAL)**

#### **1. Descripción General**

  * **Nombre del Proyecto:** `[Ej: "Motor de Recomendaciones v2"]`
  * **Propósito Principal:** `[Ej: "Servicio que expone una API REST para ofrecer recomendaciones de productos personalizadas basadas en el historial del usuario."]`
  * **Dominio de Negocio:** `[Ej: "E-commerce, Retail"]`

#### **2. Stack Tecnológico**

  * **Lenguaje/Framework Principal:** `[Ej: "Kotlin con Spring Boot"]`
  * **Base de Datos / Persistencia:** `[Ej: "MongoDB, Redis para caché"]`
  * **Plataforma / Infraestructura:** `[Ej: "Desplegado en GKE con Docker"]`
  * **Testing:** `[Ej: "JUnit 5, Mockito"]`
  * **Herramientas Clave:** `[Ej: "Gradle, RabbitMQ, Alembic"]`

#### **3. Estructura del Repositorio**

*Describe la disposición actual de los directorios para establecer un punto de partida.*

```
/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/project/
│   │   │       ├── controller/    # Endpoints/Controladores
│   │   │       ├── service/       # Lógica de negocio dispersa
│   │   │       ├── model/         # Entidades de la base de datos
│   │   │       ├── repository/    # Acceso a datos
│   │   │       └── dto/           # Data Transfer Objects
│   │   └── resources/
│   └── test/
├── build.gradle
└── ...
```

#### **4. Convenciones y Estándares (Si existen)**

  * **Estilo de Código:** `[Ej: "Se sigue la guía de estilo oficial de Kotlin, con formateo automático vía ktlint."]`
  * **Convenciones de Nomenclatura:** `[Ej: "UpperCamelCase para clases, lowerCamelCase para funciones y variables."]`
  * **Gestión de Dependencias:** `[Ej: "Versionado semántico gestionado con Gradle."]`

-----

### **PARTE II: OBJETIVOS DE LA REFACTORIZACIÓN**

#### **🎯 5. Misión Principal**

El objetivo central es auditar y refactorizar el código fuente para mejorar su calidad intrínseca. Buscamos transformar la base de código en un sistema más **mantenible, escalable y robusto**, alineándolo con principios de diseño de software modernos y reduciendo la complejidad accidental.

#### **⚠️ 6. Diagnóstico: Puntos de Dolor y Deuda Técnica**

*Lista de problemas conocidos o sospechados que motivan esta iniciativa.*

  * **Ejemplo 1 (Bajo Acoplamiento):** "Los controladores contienen lógica de negocio compleja, mezclando la orquestación de HTTP con las reglas del dominio."
  * **Ejemplo 2 (DRY):** "Existe código repetido en las capas de repositorio para operaciones CRUD básicas sobre diferentes entidades."
  * **Ejemplo 3 (Robustez):** "El manejo de excepciones es ad-hoc y no sigue un patrón consistente, resultando en respuestas de error impredecibles."
  * **Ejemplo 4 (Testing):** "La cobertura de pruebas es baja en la capa de servicios, y las pruebas existentes son frágiles y están demasiado acopladas a la implementación."

#### **🏆 7. Criterios de Éxito y Objetivos Específicos**

*Definición clara de cómo se ve el estado final deseado.*

  * **Ejemplo 1 (Arquitectura):** "Extraer la lógica de negocio a una capa de dominio/aplicación clara, dejando los controladores delegando la ejecución."
  * **Ejemplo 2 (Reusabilidad):** "Implementar un patrón de repositorio genérico para eliminar la duplicación de código en las operaciones de base de datos."
  * **Ejemplo 3 (Consistencia):** "Establecer un sistema centralizado de manejo de excepciones a nivel de framework (ej: `@ControllerAdvice` en Spring)."
  * **Ejemplo 4 (Calidad):** "Lograr una cobertura de pruebas de al menos 80% para la lógica de negocio crítica, utilizando mocks de forma efectiva."

#### **📐 8. Principios Guía para el Análisis**

*Principios de diseño que deben guiar todas las sugerencias y refactorizaciones.*

  * **SOLID:**
      * **SRP (Single Responsibility):** Cada clase o módulo debe tener una única razón para cambiar.
      * **OCP (Open/Closed):** Las entidades de software deben estar abiertas a la extensión, pero cerradas a la modificación.
      * **LSP (Liskov Substitution):** Los subtipos deben ser sustituibles por sus tipos base.
      * **ISP (Interface Segregation):** Es mejor tener muchas interfaces específicas que una sola de propósito general.
      * **DIP (Dependency Inversion):** Los módulos de alto nivel no deben depender de los de bajo nivel; ambos deben depender de abstracciones.
  * **DRY (Don't Repeat Yourself):** Evitar la duplicación de código mediante abstracciones.
  * **KISS (Keep It Simple, Stupid):** Preferir soluciones sencillas y claras sobre las complejas.
  * **Bajo Acoplamiento y Alta Cohesión:** Minimizar las dependencias entre módulos y asegurar que el contenido de un módulo esté fuertemente relacionado.

-----

### **PARTE III: COLABORACIÓN Y MODO DE TRABAJO**

#### **📋 9. Tareas Solicitadas**

Cuando se solicite asistencia, las tareas principales serán:

1.  **Análisis de Arquitectura:**

      * Evaluar la estructura actual del proyecto y proponer mejoras (ej: arquitectura limpia, hexagonal, por capas).
      * Identificar violaciones de los límites entre capas y sugerir cómo corregirlas.
      * Señalar módulos con alto acoplamiento o baja cohesión.

2.  **Revisión de Código (`Code Review`):**

      * Analizar fragmentos o archivos de código en busca de "code smells" y antipatrones.
      * Sugerir aplicaciones concretas de los principios guía (SOLID, DRY, etc.) sobre el código proporcionado.
      * Recomendar patrones de diseño (ej: Strategy, Factory, Repository) para resolver problemas específicos.

3.  **Generación de Código Refactorizado:**

      * A partir de un bloque de código, generar una versión mejorada, explicando claramente los cambios y los beneficios obtenidos.
      * Asistir en la creación de nuevas estructuras (clases, interfaces, módulos) y en la migración de lógica hacia ellas.

4.  **Estrategia de Pruebas:**

      * Para un módulo o función, sugerir qué casos de prueba (unitarios, de integración, de borde) son necesarios.
      * Ayudar a escribir pruebas claras y efectivas para el código nuevo o refactorizado.

#### **📦 10. Interacción con Código Extenso (Protocolo de "Chunking")**

Dado que los modelos de lenguaje tienen un límite de contexto (tokens), para analizar archivos extensos o múltiples archivos, seguiremos este protocolo:

1.  **Declaración de Intención:** Indicaré claramente el objetivo y los archivos que necesito que analices en conjunto. (Ej: "Quiero refactorizar el servicio `OrderService.java` que interactúa con `OrderRepository.java`. Empecemos con el servicio.").
2.  **Suministro en Fragmentos (Chunks):** Proporcionaré el código en fragmentos manejables, dentro de bloques de código. Esperaré tu confirmación antes de enviar el siguiente fragmento.
      * **Yo:** "Aquí está la primera parte de `OrderService.java`:"
        ```java
        // ... chunk 1 of code ...
        ```
      * **Tú:** "Entendido. He procesado la primera parte. Por favor, envía la siguiente."
3.  **Análisis Final:** Una vez que haya enviado todo el código relevante y te lo haya notificado (Ej: "Ese era el último fragmento del servicio"), realizarás el análisis completo solicitado, considerando todo el contexto proporcionado.

Este protocolo asegura que no se pierda información y que tu análisis sea exhaustivo y preciso.