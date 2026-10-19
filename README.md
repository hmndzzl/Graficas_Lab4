# Benatar - Renderizador 3D

## Características y Funcionalidades

El proyecto es un renderizador de software desarrollado en Rust para visualizar la nave **Benatar**, e incluye:

- **Carga de Modelos OBJ**: Lectura de `Benatar.obj`, con 1,186 vértices y 2,340 caras triangulares. Se recorren manualmente los índices de las caras para obtener los vértices de cada triángulo.
- **Rasterización de Triángulos**: Relleno de triángulos mediante coordenadas baricéntricas, dibujando directamente sobre un framebuffer de **1280 × 960 píxeles**.
- **Proyección Ortográfica**: Vista del modelo sin distorsión por perspectiva, manteniendo una escala fija durante la órbita.
- **Búfer de Profundidad (Z-Buffer)**: Interpolación de profundidad por píxel para que las superficies cercanas oculten correctamente las caras posteriores en el modo sólido.
- **Acabado Anaranjado Metálico**: Sombreado por cara con iluminación difusa, brillos especulares y reflejos cálidos simulados.
- **Modo Holograma (Wireframe)**: Malla celeste con un halo suave que muestra las aristas de los triángulos, incluidas las traseras, para inspeccionar la geometría de la nave.
- **Cámara Orbital**: Giro horizontal y vertical alrededor del centro del modelo, conservando la distancia y limitando la elevación para evitar que la vista se invierta.

## Librerías Utilizadas

| Librería | Descripción e Importancia |
| :--- | :--- |
| `minifb` | Crea la ventana, recibe la entrada del teclado y muestra en pantalla el arreglo de píxeles del framebuffer. |
| `nalgebra-glm` | Proporciona vectores `Vec3` y operaciones matemáticas para transformar vértices, calcular normales, iluminar superficies y controlar la cámara orbital. |

## Controles

| Acción | Tecla |
| :--- | :--- |
| **Orbitar Horizontalmente** | `←` / `→` (Flechas) |
| **Elevar / Bajar la Cámara** | `↑` / `↓` (Flechas) |
| **Alternar Metal / Holograma** | `H` |
| **Salir** | `ESC` o cerrar la ventana |

## Guía de Ejecución

### Prerrequisitos

- **Rust y Cargo:** Tener instalado [Rust](https://rustup.rs/) (versión estable recomendada).
- **En Windows:** Contar con las herramientas de compilación de C++ (**Visual Studio C++ Build Tools** o el toolchain `x86_64-pc-windows-msvc`). `minifb` usa las APIs nativas de Win32, por lo que no requiere dependencias externas como SDL2.
- **En macOS / Linux:** Entorno gráfico activo y dependencias de ventana estándar (CMake/X11 en Linux si aplica).

---

### En Windows (PowerShell / CMD / Windows Terminal)

1. Abre **PowerShell** o **Windows Terminal** y clona el repositorio:

   ```powershell
   git clone https://github.com/hmndzzl/Graficas_Lab4.git
   cd Graficas_Lab4
   ```

2. Compila y ejecuta el proyecto:

   ```powershell
   cargo run --release
   ```

   *(También puedes usar `cargo run` estándar, el cual ya cuenta con `opt-level = 3` en desarrollo).*

3. Para correr las pruebas unitarias:

   ```powershell
   cargo test
   ```

---

### En macOS / Linux (Terminal / Bash / Zsh)

1. Abre tu terminal y clona el repositorio:

   ```bash
   git clone https://github.com/hmndzzl/Graficas_Lab4.git
   cd Graficas_Lab4
   ```

2. Compila y ejecuta el proyecto:

   ```bash
   cargo run --release
   ```

3. Para ejecutar las pruebas unitarias:

   ```bash
   cargo test
   ```

## Estructura del Proyecto

```text
Graficas_Lab4/
├── src/
│   ├── main.rs         # Ciclo principal, controles, proyección e iluminación.
│   ├── camera.rs       # Cámara orbital y cambio de base.
│   ├── color.rs        # Colores RGB, conversión hexadecimal y operaciones de color.
│   ├── framebuffer.rs  # Búfer de píxeles, profundidad y mezcla de colores.
│   ├── obj.rs          # Lectura de vértices y caras del modelo OBJ.
│   └── triangle.rs     # Rasterización de triángulos y dibujo de aristas con halo.
├── Benatar.obj         # Modelo 3D de la nave.
├── Benatar.mtl         # Archivo de materiales del modelo; el renderizador define su propio acabado.
├── instructions.md     # Enunciado del ejercicio.
├── Cargo.lock          # Versiones resueltas de las dependencias.
└── Cargo.toml          # Configuración de Rust, dependencias y optimización.
```

## Derechos de Autor y Aclaratoria Legal

**ESTE ES UN PROYECTO ÚNICAMENTE CON PROPÓSITOS EDUCATIVOS Y SIN FINES DE LUCRO.**

### Hugo Méndez - 241265
