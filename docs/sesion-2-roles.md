# Guía Paso a Paso por Roles (Sesión 2)

> Esta guía está separada para que cada integrante (**A**, **B** y **C**) solo siga su propia sección paso a paso.

---

## 📋 Resumen de Roles y Flujo General

| Integrante | Rol | Función asignada |
|---|---|---|
| **A** | Dueño del repositorio | Contador de tareas pendientes |
| **B** | Colaborador | Botón limpiar completadas |
| **C** | Colaborador | Tema oscuro |

### ⏱️ Orden de ejecución:
1. **Paso 1:** A invita a B y C. B y C aceptan y clonan.
2. **Paso 2:** A crea las 3 Issues en GitHub.
3. **Paso 3:** Cada quien crea su rama, pega su código y hace commit + push.
4. **Paso 4:** Cada quien abre su PR. Se revisan en cadena: **A revisa a B**, **B revisa a C**, **C revisa a A**. Luego cada autor hace merge.
5. **Paso 5:** Conflicto a propósito con nombres (se resuelve en GitHub).
6. **Paso 6 y 7:** A actualiza el README y publica GitHub Pages.

---

# 👤 ROL A (Dueño del Repositorio - Contador)

### Paso A1: Invitar a B y C
1. En GitHub, entra a tu repositorio `tablero-tareas`.
2. Ve a **Settings** → **Collaborators** → botón **Add people**.
3. Busca y agrega los usuarios de GitHub de **B** y **C**.

---

### Paso A2: Crear las 3 Issues
En la pestaña **Issues** de tu repositorio en GitHub, da clic en **New issue** y crea:
1. Título: `Contador de tareas pendientes` → en **Assignees** asígnate a ti (**A**).
2. Título: `Botón limpiar completadas` → en **Assignees** asigna a **B**.
3. Título: `Tema oscuro` → en **Assignees** asigna a **C**.

---

### Paso A3: Tu rama y código (Contador)
1. Abre la terminal en tu proyecto `tablero-tareas` y ejecuta:
   ```bash
   git switch main
   git pull
   git switch -c contador
   ```
2. **Modifica `index.html`:**  
   Donde dice `<!-- Zona A: contador -->` (debajo de `</form>`), pega:
   ```html
   <p id="contador">0 tareas pendientes</p>
   ```
3. **Modifica `js/app.js`:**  
   Donde dice `// ===== Zona A: contador de pendientes (sesión 2) =====`, pega abajo:
   ```javascript
   function actualizarContador() {
     const pendientes = tareas.filter(t => !t.hecha).length;
     document.getElementById('contador').textContent = pendientes + ' tareas pendientes';
   }
   document.addEventListener('tareas:cambio', actualizarContador);
   actualizarContador();
   ```
4. Guarda los archivos y ejecuta:
   ```bash
   git add .
   git commit -m "Agrego contador de pendientes"
   git push -u origin contador
   ```

---

### Paso A4: Pull Request y Revisión
1. En GitHub, abre el Pull Request de tu rama `contador` hacia `main`.
2. En la descripción escribe: `Closes #1`.
3. En **Reviewers** (a la derecha) selecciona a **C**.
4. **Revisar a B:** Ve a los Pull Requests, abre el PR de **B** (`limpiar`), ve a la pestaña **Files changed**, da clic en el botón verde **Review changes** → selecciona **Approve** → **Submit review**.
5. Cuando **C** haya aprobado tu PR (`contador`), haz clic en **Merge pull request** → **Confirm merge**.
6. En tu terminal actualiza tu `main`:
   ```bash
   git switch main
   git pull
   ```

---

### Paso A5: Conflicto a propósito (Integrantes)
1. En tu terminal ejecuta:
   ```bash
   git switch main
   git pull
   git switch -c mi-nombre-a
   ```
2. En `index.html`, dentro de `<ul id="integrantes">`, reemplaza `<li>Agrega tu nombre aquí</li>` por tu nombre:
   ```html
   <li>Tu Nombre Completo (A)</li>
   ```
3. Guarda y ejecuta:
   ```bash
   git add index.html
   git commit -m "Agrego mi nombre al equipo"
   git push -u origin mi-nombre-a
   ```
4. En GitHub abre el Pull Request hacia `main`. Si eres el primero en mezclarlo, haz **Merge pull request** directo. Si te aparece conflicto con B o C, da clic en **Resolve conflicts**, deja ambos nombres en la lista `<li>`, borra las marcas `<<<<<<<`, `=======`, `>>>>>>>` y confirma el merge.

---

### Paso A6: Actualizar README.md
1. En tu terminal ejecuta:
   ```bash
   git switch main
   git pull
   ```
2. Edita `README.md` para incluir a los 3 integrantes y qué función hizo cada quien:
   ```markdown
   ## Equipo
   - Nombre de A (Contador)
   - Nombre de B (Limpiar completadas)
   - Nombre de C (Tema oscuro)
   ```
3. Guarda y sube el cambio:
   ```bash
   git add README.md
   git commit -m "Actualizo equipo en el README"
   git push origin main
   ```

---

### Paso A7: Publicar Release y GitHub Pages
1. En la página del repositorio, ve a la columna derecha: **Releases** → **Create a new release**.
2. **Choose a tag:** escribe `v1.0.0` y da clic en **Create new tag: v1.0.0 on publish**.
3. Título del Release: `Versión 1.0`.
4. Clic en **Generate release notes** → **Publish release**.
5. Ve a **Settings** del repositorio → menú izquierdo **Pages**:
   - **Source:** `Deploy from a branch`
   - **Branch:** `main` / carpeta `/ (root)`
   - Clic en **Save**.
6. En un par de minutos tu página estará activa en:  
   `https://TU-USUARIO.github.io/tablero-tareas/`

---

---

# 👤 ROL B (Colaborador - Limpiar Completadas)

### Paso B1: Aceptar invitación y clonar
1. Acepta la invitación que te llegó al correo o en [https://github.com/notifications](https://github.com/notifications).
2. Abre tu terminal en la carpeta donde guardas tus proyectos (ej. `Documentos`) y ejecuta:
   ```bash
   git clone https://github.com/USUARIO-A/tablero-tareas.git tablero-equipo
   cd tablero-equipo
   code .
   ```

---

### Paso B2: Tu rama y código (Limpiar)
1. En la terminal de VS Code ejecuta:
   ```bash
   git switch -c limpiar
   ```
2. **Modifica `index.html`:**  
   Donde dice `<!-- Zona B: botón limpiar -->` (debajo de `</ul>`), pega:
   ```html
   <button id="limpiar" type="button">Limpiar completadas</button>
   ```
3. **Modifica `js/app.js`:**  
   Donde dice `// ===== Zona B: limpiar completadas (sesión 2) =====`, pega abajo:
   ```javascript
   document.getElementById('limpiar').addEventListener('click', () => {
     tareas = tareas.filter(t => !t.hecha);
     guardar();
     render();
   });
   ```
4. Guarda los archivos y ejecuta:
   ```bash
   git add .
   git commit -m "Agrego botón limpiar completadas"
   git push -u origin limpiar
   ```

---

### Paso B3: Pull Request y Revisión
1. En GitHub, ve al repositorio de A y abre el Pull Request de tu rama `limpiar` hacia `main`.
2. En la descripción escribe: `Closes #2`.
3. En **Reviewers** (a la derecha) selecciona a **A**.
4. **Revisar a C:** Ve a la pestaña **Pull requests**, abre el PR de **C** (`tema-oscuro`), ve a **Files changed**, da clic en **Review changes** → selecciona **Approve** → **Submit review**.
5. Cuando **A** haya aprobado tu PR (`limpiar`), da clic en **Merge pull request** → **Confirm merge**.
6. En tu terminal actualiza tu rama principal:
   ```bash
   git switch main
   git pull
   ```

---

### Paso B4: Conflicto a propósito (Integrantes)
1. En tu terminal ejecuta:
   ```bash
   git switch main
   git pull
   git switch -c mi-nombre-b
   ```
2. En `index.html`, dentro de `<ul id="integrantes">`, reemplaza `<li>Agrega tu nombre aquí</li>` por tu nombre:
   ```html
   <li>Tu Nombre Completo (B)</li>
   ```
3. Guarda y ejecuta:
   ```bash
   git add index.html
   git commit -m "Agrego mi nombre al equipo"
   git push -u origin mi-nombre-b
   ```
4. En GitHub abre el Pull Request hacia `main`.
5. Si GitHub indica **"This branch has conflicts that must be resolved"**:
   - Da clic en **Resolve conflicts**.
   - Verás las marcas de Git (`<<<<<<<`, `=======`, `>>>>>>>`).
   - Borra las marcas y asegúrate de dejar **ambos** nombres en la lista con sus etiquetas `<li>`.
   - Da clic en **Mark as resolved** → **Commit merge** → **Merge pull request**.
6. En tu terminal finaliza actualizando:
   ```bash
   git switch main
   git pull
   ```

---

---

# 👤 ROL C (Colaborador - Tema Oscuro)

### Paso C1: Aceptar invitación y clonar
1. Acepta la invitación recibida por correo o en [https://github.com/notifications](https://github.com/notifications).
2. Abre tu terminal en tu carpeta de trabajo y ejecuta:
   ```bash
   git clone https://github.com/USUARIO-A/tablero-tareas.git tablero-equipo
   cd tablero-equipo
   code .
   ```

---

### Paso C2: Tu rama y código (Tema Oscuro)
1. En la terminal de VS Code ejecuta:
   ```bash
   git switch -c tema-oscuro
   ```
2. **Modifica `index.html`:**  
   Donde dice `<!-- Zona C: botón de tema -->` (dentro de `<header>`), pega:
   ```html
   <button id="tema" type="button">Tema oscuro</button>
   ```
3. **Modifica `css/estilos.css`:**  
   Al final de todo el archivo, pega:
   ```css
   body.oscuro {
     background: #1e1e1e;
     color: #eee;
   }

   body.oscuro #lista li {
     background: #2b2b2b;
   }

   body.oscuro footer {
     color: #aaa;
     border-color: #444;
   }
   ```
4. **Modifica `js/app.js`:**  
   Donde dice `// ===== Zona C: tema oscuro (sesión 2) =====`, pega abajo:
   ```javascript
   const botonTema = document.getElementById('tema');
   if (localStorage.getItem('tema') === 'oscuro') document.body.classList.add('oscuro');
   botonTema.addEventListener('click', () => {
     document.body.classList.toggle('oscuro');
     localStorage.setItem('tema', document.body.classList.contains('oscuro') ? 'oscuro' : 'claro');
   });
   ```
5. Guarda los archivos y ejecuta:
   ```bash
   git add .
   git commit -m "Agrego tema oscuro"
   git push -u origin tema-oscuro
   ```

---

### Paso C3: Pull Request y Revisión
1. En GitHub, abre el Pull Request de tu rama `tema-oscuro` hacia `main`.
2. En la descripción escribe: `Closes #3`.
3. En **Reviewers** (a la derecha) selecciona a **B**.
4. **Revisar a A:** Ve a la pestaña **Pull requests**, abre el PR de **A** (`contador`), ve a **Files changed**, da clic en **Review changes** → selecciona **Approve** → **Submit review**.
5. Cuando **B** haya aprobado tu PR (`tema-oscuro`), haz clic en **Merge pull request** → **Confirm merge**.
6. En tu terminal actualiza tu rama principal:
   ```bash
   git switch main
   git pull
   ```

---

### Paso C4: Conflicto a propósito (Integrantes)
1. En tu terminal ejecuta:
   ```bash
   git switch main
   git pull
   git switch -c mi-nombre-c
   ```
2. En `index.html`, dentro de `<ul id="integrantes">`, pon tu nombre:
   ```html
   <li>Tu Nombre Completo (C)</li>
   ```
3. Guarda y ejecuta:
   ```bash
   git add index.html
   git commit -m "Agrego mi nombre al equipo"
   git push -u origin mi-nombre-c
   ```
4. En GitHub abre el Pull Request hacia `main`.
5. Si aparece conflicto:
   - Da clic en **Resolve conflicts**.
   - Borra las marcas (`<<<<<<<`, `=======`, `>>>>>>>`).
   - Conserva los nombres de tus compañeros junto con el tuyo.
   - Da clic en **Mark as resolved** → **Commit merge** → **Merge pull request**.
6. En tu terminal finaliza actualizando:
   ```bash
   git switch main
   git pull
   ```
