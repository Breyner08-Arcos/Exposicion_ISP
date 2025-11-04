# 🧩 Principios SOLID y Patrón Builder — Ejemplos en Java

Este repositorio contiene ejemplos prácticos sobre los **principios SOLID** y el **Patrón de Diseño Builder** en Java.  
Los ejemplos están diseñados para servir como material de apoyo para una exposición universitaria (nivel intermedio-avanzado) sobre **buenas prácticas de diseño de software orientado a objetos**.

---

## 📘 Contenido

1. [Principios SOLID]
   - [S — Responsabilidad Única (SRP)]
   - [O — Abierto/Cerrado (OCP)]
   - [L — Sustitución de Liskov (LSP)]
   - [I — Segregación de Interfaces (ISP)]
   - [D — Inversión de Dependencias (DIP)]
2. [Patrón de Diseño Builder]
3. [Cómo ejecutar los ejemplos]

---

## 🧠 Principios SOLID

### **S — Responsabilidad Única (SRP)**  
Cada clase debe tener una sola razón para cambiar.  
➡️ Una clase, una responsabilidad.

**Ejemplo breve:**
```java
public class Reporte {
    public void generarPDF() { /* Lógica para generar PDF */ }
}

public class ReporteLogger {
    public void registrar(String mensaje) { /* Lógica para registrar logs */ }
}
```
✅ Aquí, `Reporte` se encarga del documento y `ReporteLogger` del registro de acciones.

---

### **O — Abierto/Cerrado (OCP)**  
El código debe estar abierto para extensión, pero cerrado para modificación.  
➡️ Puedes agregar nuevas funcionalidades sin alterar las existentes.

```java
public interface Descuento {
    double aplicar(double precio);
}

public class DescuentoNavidad implements Descuento {
    public double aplicar(double precio) {
        return precio * 0.9;
    }
}
```

---

### **L — Sustitución de Liskov (LSP)**  
Las subclases deben poder reemplazar a sus superclases sin alterar el comportamiento esperado.  
➡️ Evita herencia que rompa la compatibilidad del contrato.

---

### **I — Segregación de Interfaces (ISP)**  
Las clases no deben verse obligadas a implementar métodos que no usan.  
➡️ Divide las interfaces grandes en otras más pequeñas y específicas.

**Ejemplo:**
```java
public interface Imprimible {
    void imprimir();
}

public interface Escaneable {
    void escanear();
}
```

---

### **D — Inversión de Dependencias (DIP)**  
Los módulos de alto nivel **no deben depender de módulos de bajo nivel**, sino de **abstracciones**.  
Las abstracciones **no deben depender de los detalles**; los detalles deben depender de las abstracciones.

#### 📁 Ejemplo: Notificador DIP

**Código:**
```java
// Notificador.java
package DIP;
public interface Notificador {
    void enviarMensaje(String mensaje);
}

// EmailNotificador.java
package DIP;
public class EmailNotificador implements Notificador {
    public void enviarMensaje(String mensaje) {
        System.out.println("Enviando EMAIL: " + mensaje);
    }
}

// SMSNotificador.java
package DIP;
public class SMSNotificador implements Notificador {
    public void enviarMensaje(String mensaje) {
        System.out.println("Enviando SMS: " + mensaje);
    }
}

// GestorAlerta.java
package DIP;
public class GestorAlerta {
    private final Notificador notificador;
    public GestorAlerta(Notificador notificador) {
        this.notificador = notificador;
    }
    public void enviarAlerta(String mensaje) {
        notificador.enviarMensaje("[ALERTA] " + mensaje);
    }
}

// DemoDIP.java
package DIP;
public class DemoDIP {
    public static void main(String[] args) {
        Notificador email = new EmailNotificador();
        Notificador sms = new SMSNotificador();

        GestorAlerta alertaEmail = new GestorAlerta(email);
        GestorAlerta alertaSMS = new GestorAlerta(sms);

        alertaEmail.enviarAlerta("Servidor sobrecargado");
        alertaSMS.enviarAlerta("Temperatura del CPU alta");
    }
}
```

**Salida esperada:**
```
Enviando EMAIL: [ALERTA] Servidor sobrecargado
Enviando SMS: [ALERTA] Temperatura del CPU alta
```

---

## 🏗️ Patrón de Diseño Builder

El **Patrón Builder** permite construir objetos complejos paso a paso sin necesidad de múltiples constructores.

### 📁 Ejemplo: Reporte con Builder

**Código:**
```java
// Reporte.java
package DemoRepo;

public class Reporte {
    private String titulo;
    private String contenido;
    private String autor;
    private String fecha;

    private Reporte(Builder builder) {
        this.titulo = builder.titulo;
        this.contenido = builder.contenido;
        this.autor = builder.autor;
        this.fecha = builder.fecha;
    }

    @Override
    public String toString() {
        return "Reporte generado:\n" +
                "Título: " + titulo + "\n" +
                "Autor: " + autor + "\n" +
                "Fecha: " + fecha + "\n" +
                "Contenido:\n" + contenido;
    }

    public static class Builder {
        private String titulo;
        private String contenido;
        private String autor;
        private String fecha;

        public Builder titulo(String titulo) {
            this.titulo = titulo;
            return this;
        }

        public Builder contenido(String contenido) {
            this.contenido = contenido;
            return this;
        }

        public Builder autor(String autor) {
            this.autor = autor;
            return this;
        }

        public Builder fecha(String fecha) {
            this.fecha = fecha;
            return this;
        }

        public Reporte build() {
            return new Reporte(this);
        }
    }
}
```

```java
// DemoReporte.java
package DemoRepo;

public class DemoReporte {
    public static void main(String[] args) {
        Reporte reporte = new Reporte.Builder()
                .titulo("Informe de Ventas Q1 2025")
                .autor("Ana López")
                .fecha("04/11/2025")
                .contenido("Se registró un incremento del 15% respecto al trimestre anterior.")
                .build();

        System.out.println(reporte);
    }
}
```

**Salida esperada:**
```
Reporte generado:
Título: Informe de Ventas Q1 2025
Autor: Ana López
Fecha: 04/11/2025
Contenido:
Se registró un incremento del 15% respecto al trimestre anterior.
```
