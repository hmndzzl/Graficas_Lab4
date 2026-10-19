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

**Prerrequisitos:**

Contar con la cadena de herramientas de **[Rust (cargo)](https://rustup.rs/)** instalada y un entorno gráfico para abrir la ventana del renderizador.

1. Clona o descarga el repositorio en tu máquina.

   ```bash
   git clone https://github.com/hmndzzl/Graficas_Lab4.git
   ```

2. Abre tu terminal y navega hasta el directorio raíz del proyecto, el cual debe contener `Cargo.toml` y `Benatar.obj`.

   ```bash
   cd Graficas_Lab4
   ```

3. Ejecuta el renderizador. El perfil de desarrollo está configurado con `opt-level = 3` para optimizar el dibujo por software en CPU.

   ```bash
   cargo run
   ```

   También puedes ejecutarlo con el perfil de producción:

   ```bash
   cargo run --release
   ```

4. Para verificar la carga del modelo, el relleno de triángulos, el modo holograma y la cámara orbital, ejecuta las pruebas:

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
