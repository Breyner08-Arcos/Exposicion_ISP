# 🧩 Principio de Segregación de Interfaces (ISP)
📘 Descripción general

## El Principio de Segregación de Interfaces (Interface Segregation Principle - ISP) establece que:

**“Ninguna clase debería verse obligada a depender de métodos que no utiliza.”**

Este principio busca mantener las interfaces pequeñas, específicas y coherentes con una sola responsabilidad, evitando que las clases implementen métodos innecesarios o irrelevantes.

En otras palabras, es mejor tener varias interfaces pequeñas y bien definidas que una interfaz grande que **obligue a las clases a implementar métodos vacíos o sin sentido.**

**Ejemplo:**
```java
class Robot implements Trabajador {
    @Override
    public void trabajar() {
        System.out.println("Robot ensamblando piezas...");
    }

    // ❌ Este método no tiene sentido para un robot, pero está obligado a implementarlo
    @Override
    public void comer() {
        throw new UnsupportedOperationException("Un robot no necesita comer.");
    }
}
```
# Explicación del error

- La interfaz Trabajador tiene métodos que no son relevantes para todas las clases.

- Robot no necesita implementar comer(), pero la interfaz lo obliga.

- Genera dependencias innecesarias, violando el ISP.

El resultado es un código más frágil, difícil de mantener y menos reutilizable.

**Ejemplo: correcto**
```java
class Empleado implements Trabajador, Comedor {
    @Override
    public void trabajar() {
        System.out.println("Empleado trabajando en la oficina...");
    }

    @Override
    public void comer() {
        System.out.println("Empleado comiendo en la cafetería.");
    }
}

class Robot implements Trabajador {
    @Override
    public void trabajar() {
        System.out.println("Robot ensamblando piezas...");
    }
}
```
# Explicación

- Se dividió la **interfaz grande en dos más pequeñas**:

- Trabajador → se enfoca solo en trabajar.

- Comedor → se enfoca solo en comer.

- Empleado implementa ambas interfaces porque necesita ambos comportamientos.

- Robot implementa solo la interfaz Trabajador porque no necesita comer.

- Este diseño cumple con el ISP: cada clase solo depende de lo que realmente usa.
```

| Aspecto          | Ejemplo Incorrecto                            | Ejemplo Correcto                         |
| ---------------- | --------------------------------------------- | ---------------------------------------- |
| Interfaz         | Genérica y con métodos innecesarios           | Específica y enfocada                    |
| Implementaciones | Clases obligadas a implementar métodos vacíos | Clases solo implementan lo que necesitan |
| Acoplamiento     | Alto                                          | Bajo                                     |
| Reutilización    | Baja                                          | Alta                                     |
| Cumple ISP       | ❌ No                                         | ✅ Sí                                     |
```
### Diagrama de clases – Principio de Segregación de Interfaces (ISP)

Este diagrama representa la correcta aplicación del ISP, separando las responsabilidades en interfaces pequeñas y específicas.

![Diagrama ISP](Multimedia.jpg)
