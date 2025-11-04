# 📚 Ejemplos de Código – Principios SOLID y Patrón Builder (Java)

Este repositorio contiene ejemplos prácticos en Java que ilustran dos conceptos fundamentales en el diseño orientado a objetos:

- ✅ **Principios SOLID**, con enfoque especial en el **Principio de Segregación de Interfaces (ISP)**.
- 🏗️ **Patrón de diseño Builder**, para la construcción flexible de objetos complejos.

---

## 🔹 1. Principio de Segregación de Interfaces (ISP)

**Descripción:**  
El Principio de Segregación de Interfaces establece que *“los clientes no deberían depender de interfaces que no utilizan”*. Es decir, es mejor tener múltiples interfaces específicas que una sola interfaz general con muchos métodos.

### 📁 Archivos:
- `DispositivoMultifuncion.java`: contiene una interfaz inflada que combina impresión, escaneo y fax.
- `ImpresoraBasica.java`: implementa la interfaz completa, aunque solo necesita imprimir (viola ISP).
- `Impresora.java`, `Escaner.java`, `Fax.java`: interfaces separadas por responsabilidad (corrección).
- `CentroDeCopias.java`: ejemplo de clase que implementa múltiples interfaces específicas.

### ✅ Enseñanza clave:
Dividir una interfaz en partes más pequeñas mejora la reutilización, el mantenimiento y evita código innecesario como métodos vacíos o excepciones lanzadas por funciones no utilizadas.

---

## 🔹 2. Patrón de Diseño Builder

**Descripción:**  
El patrón Builder permite crear objetos complejos paso a paso, especialmente útil cuando un objeto tiene múltiples atributos opcionales. Evita el uso de constructores telescópicos y mejora la legibilidad.

### 📁 Archivos:
- `Pizza.java`: clase principal que encapsula el constructor privado y usa el patrón Builder interno.
- `PizzaBuilder`: clase estática interna que define los pasos para configurar y construir una pizza.
- `DemoPizza.java`: clase demo con un `main()` que construye una pizza personalizada usando el builder.

### 🧱 Ejemplo de uso:
```java
Pizza miPizza = new Pizza.PizzaBuilder("Grande")
    .masa("Delgada")
    .extraQueso(true)
    .pepperoni(true)
    .build();
```

### ✅ Enseñanza clave:
El patrón Builder permite instanciar objetos con gran flexibilidad, usando una sintaxis fluida y segura. Mejora la escalabilidad y claridad del código en comparación con constructores con muchos parámetros.

---
