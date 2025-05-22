# Test
**Introducción a Git y su uso colaborativo con repositorios remotos**

Git es un sistema de control de versiones distribuido que permite gestionar el historial de cambios en archivos, especialmente útil en proyectos de desarrollo de software. Con Git, los desarrolladores pueden trabajar en paralelo, mantener un historial claro de las modificaciones y colaborar de manera efectiva sin sobrescribir el trabajo de otros.

## Conceptos básicos

* **Repositorio local**: Es la copia del proyecto en tu máquina, que incluye el historial de versiones.
* **Repositorio remoto**: Es una copia del proyecto alojada en un servidor (por ejemplo, GitHub, GitLab o Bitbucket) que permite la colaboración entre varios usuarios.
* **Commit**: Es una instantánea de los archivos en un momento determinado con un mensaje que describe los cambios.
* **Branch (rama)**: Permite desarrollar funciones nuevas o corregir errores sin afectar la versión principal del proyecto.
* **Merge**: Es la integración de los cambios de una rama en otra.
* **Pull**: Trae cambios del repositorio remoto al local.
* **Push**: Envía los cambios locales al repositorio remoto.

### Uso recomendado en entornos colaborativos

Cuando varios usuarios trabajan en un mismo proyecto con un repositorio remoto, se recomienda seguir estos pasos y prácticas:

#### 1. **Clonar el repositorio**

Para obtener una copia local del proyecto:

```bash
git clone https://url-del-repositorio.git
```

#### 2. **Crear una rama para trabajar**

Es buena práctica no trabajar directamente en la rama principal (`main` o `master`). En su lugar, se crea una nueva rama para cada funcionalidad o corrección:

```bash
git checkout -b nombre-de-la-rama
```

#### 3. **Hacer cambios y confirmarlos**

Después de editar archivos, se deben añadir y confirmar los cambios:

```bash
git add .
git commit -m "Descripción clara del cambio"
```

#### 4. **Actualizar el repositorio local**

Antes de subir los cambios, conviene actualizar el repositorio local con los cambios que puedan haber hecho otros:

```bash
git pull origin main  # o la rama correspondiente
```

#### 5. **Resolver conflictos si existen**

Si hay conflictos (dos personas modificaron la misma línea), Git indicará los archivos afectados para que se resuelvan manualmente antes de continuar.

#### 6. **Subir los cambios**

Una vez confirmados y actualizados los cambios, se pueden subir:

```bash
git push origin nombre-de-la-rama
```

#### 7. **Solicitar revisión e integración**

En plataformas como GitHub o GitLab, se abre una *pull request* o *merge request* para que otros revisen el código antes de integrarlo a la rama principal.

### Buenas prácticas

* Realizar *commits* frecuentes y con mensajes descriptivos.
* Usar ramas temáticas (feature/login, fix/error-404).
* Revisar y probar el código antes de integrarlo.
* Mantener actualizada la rama local frecuentemente.
* Documentar cambios relevantes y coordinar con el equipo.

Git no solo facilita el trabajo colaborativo, sino que también proporciona trazabilidad, respaldo y control sobre la evolución de los proyectos. En equipos organizados, su uso adecuado es fundamental para mantener la calidad y consistencia del desarrollo.


Claro, a continuación te presento un **ejemplo práctico** del uso de Git en un entorno colaborativo, con **dos personas trabajando en un proyecto común** a través de un repositorio remoto (como GitHub).

---

## 🔧 Escenario

Supongamos que dos desarrolladores, **Ana** y **Luis**, trabajan en un proyecto llamado `calculadora`. El repositorio remoto está alojado en GitHub:
`https://github.com/empresa/calculadora.git`

El objetivo es que cada uno agregue una función distinta: Ana agregará la función de **suma**, y Luis la de **resta**.

---

## 🧩 Paso a paso del flujo de trabajo

### 📥 1. Clonación del repositorio remoto (ambos)

Cada uno clona el repositorio remoto en su máquina local:

```bash
git clone https://github.com/empresa/calculadora.git
cd calculadora
```

### 🌿 2. Crear ramas para trabajar

Cada desarrollador crea su propia rama desde `main` para trabajar de forma independiente.

**Ana:**

```bash
git checkout -b feature/suma
```

**Luis:**

```bash
git checkout -b feature/resta
```

### 📝 3. Hacer cambios y hacer commits

Cada uno implementa su función en un archivo llamado `calculadora.py`.

**Ana edita `calculadora.py`:**

```python
def suma(a, b):
    return a + b
```

Y guarda los cambios con:

```bash
git add calculadora.py
git commit -m "Agregar función suma"
```

**Luis edita `calculadora.py`:**

```python
def resta(a, b):
    return a - b
```

Y guarda sus cambios:

```bash
git add calculadora.py
git commit -m "Agregar función resta"
```

### 🔃 4. Sincronización con el repositorio remoto

**Ana hace push de su rama:**

```bash
git push origin feature/suma
```

**Luis también:**

```bash
git push origin feature/resta
```

### ✅ 5. Pull Request (o Merge Request)

Desde GitHub, cada uno crea una **pull request** para integrar sus cambios en `main`.

Por ejemplo:

* Ana: `feature/suma → main`
* Luis: `feature/resta → main`

### ⚠️ 6. Resolver conflictos si los hay

Si ambos modificaron el mismo archivo (como en este caso), es posible que uno deba **sincronizar su rama con `main` antes de hacer merge**, y resolver conflictos.

Por ejemplo, si Luis hace merge después de Ana, debe:

```bash
git checkout feature/resta
git pull origin main  # Para traer los últimos cambios
```

Si Git detecta un conflicto, mostrará marcas como estas en `calculadora.py`:

```python
<<<<<<< HEAD
def resta(a, b):
    return a - b
=======
def suma(a, b):
    return a + b
>>>>>>> main
```

Luis debe editar el archivo para dejarlo así, por ejemplo:

```python
def suma(a, b):
    return a + b

def resta(a, b):
    return a - b
```

Luego:

```bash
git add calculadora.py
git commit -m "Resolver conflicto entre funciones suma y resta"
git push origin feature/resta
```

Y vuelve a intentar el merge.

### 🏁 7. Finalizar: Merge aprobado

Una vez revisadas las pull requests y resueltos los conflictos, se hace merge a `main`.

---

## ✅ Resultado final

La rama `main` ahora contiene:

```python
def suma(a, b):
    return a + b

def resta(a, b):
    return a - b
```

Y los dos desarrolladores han colaborado sin pisarse el trabajo mutuamente.

---

¿Quieres que prepare este ejemplo en un proyecto mínimo de archivos que puedas probar localmente?
