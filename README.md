# Formalización de espacios de Hilbert y del teorema de representación de Riesz en Lean 4

**Trabajo Fin de Grado — Grado en Matemáticas, Universidad de Sevilla (2024)**

Este proyecto formaliza en el asistente de pruebas **Lean 4** la teoría básica de los espacios de Hilbert, culminando en una demostración verificada por ordenador del **teorema de representación de Riesz**: todo funcional lineal acotado sobre un espacio de Hilbert se puede representar de forma única como un producto escalar.

## ¿Qué significa "formalizar" un teorema?

Formalizar matemáticas consiste en escribir las definiciones y demostraciones en un lenguaje que un ordenador puede **verificar paso a paso**. A diferencia de una demostración en papel, aquí no hay huecos ni "se deja como ejercicio": cada paso lógico debe justificarse hasta el axioma, y el asistente de pruebas (Lean) comprueba mecánicamente que todo es correcto. Si el código compila, la demostración es válida.

Este tipo de trabajo exige un dominio profundo tanto de las matemáticas subyacentes como del razonamiento lógico riguroso, y es la base de proyectos como [Mathlib](https://github.com/leanprover-community/mathlib4), la mayor biblioteca de matemáticas formalizadas del mundo, de la que este proyecto toma su estilo y algunas herramientas.

## Qué se formaliza

Partiendo casi desde cero (definiendo las estructuras en lugar de importarlas hechas), el desarrollo construye:

1. **Espacios prehilbertianos** — la clase `InnerProductSpace`, con el producto escalar y sus axiomas (positividad, simetría conjugada, linealidad).
2. **Norma y métrica inducidas** — definición de la norma a partir del producto escalar y demostración de sus propiedades.
3. **Desigualdad de Cauchy-Schwarz** — pieza clave para probar que la norma inducida es efectivamente una norma.
4. **Completitud y espacios de Hilbert** — sucesiones de Cauchy, convergencia y la clase `HilbertSpace` como espacio prehilbertiano completo.
5. **Teorema de representación de Riesz** — el resultado principal, en dos partes:
   - *Existencia*: todo funcional lineal acotado `f : F → 𝕜` se representa como `f(x) = ⟨x, z⟩` para algún `z`, apoyándose en el teorema de la proyección ortogonal.
   - *Unicidad*: el vector representante `z` es único (`unicidad_riesz`).

## Estructura del repositorio

```
EspaciosHilbert/
├── definiciones.lean     # Producto escalar, espacios prehilbertianos, completitud, espacios de Hilbert
├── lemas.lean            # Lemas auxiliares sobre el producto escalar
├── cauchyschwarz.lean    # Desigualdad de Cauchy-Schwarz
├── normainducida.lean    # La norma inducida y sus propiedades
├── metricainducida.lean  # La métrica inducida por la norma
└── riesz.lean            # Proyección ortogonal y teorema de representación de Riesz
```

En total, ~650 líneas de Lean 4 estructuradas de forma modular: cada archivo importa los anteriores, reflejando la construcción matemática por capas.

## Detalles técnicos

- **Lean 4** (`v4.7.0-rc2`) con el sistema de construcción **Lake**.
- Dependencias: **Mathlib 4** (tipos base como `IsROrC` para trabajar sobre ℝ y ℂ de forma unificada) y **Aesop**.
- Las estructuras principales (`Inner`, `InnerProductSpace`, `HilbertSpace`) se definen en el propio proyecto siguiendo el estilo de Mathlib, en lugar de reutilizar las de la biblioteca — el objetivo del TFG era construir la teoría, no consumirla.
- El teorema de la proyección ortogonal sobre el núcleo del funcional se introduce como axioma (`teorema_proyeccion`), y a partir de él se demuestran la ortogonalidad de la proyección, la existencia del representante de Riesz y su unicidad.
- Las demostraciones usan el modo táctico de Lean 4 (`by_contra`, `push_neg`, `obtain`, reescrituras con `rw`, etc.).

## Compilación

Con [elan](https://github.com/leanprover/elan) instalado (gestiona la versión de Lean automáticamente vía `lean-toolchain`):

```bash
lake update      # descarga Mathlib y Aesop
lake build
```

> Nota: la primera compilación de Mathlib puede tardar bastante; `lake exe cache get` descarga binarios precompilados y lo acelera.

## Contexto

Este repositorio contiene el desarrollo en Lean 4 de mi Trabajo Fin de Grado *"Formalización de espacios de Hilbert en Lean4"* (Grado en Matemáticas, Universidad de Sevilla). La memoria escrita desarrolla la teoría matemática en paralelo al código.

---

*Autor: Adrián García Ruiz — [github.com/AdrianGR517](https://github.com/AdrianGR517)*
