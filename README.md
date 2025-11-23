# BadCalc React - Correcciones de SonarQube

## Descripción del Proyecto
Aplicación de calculadora React con vulnerabilidades intencionales para demostración de análisis de código con SonarQube.

## Cambios Realizados

### 1. **index.html** - Corrección de Accesibilidad
**Problema:** Faltaba el atributo `lang` en el elemento `<html>`

**Solución:**
```html
<html lang="es">
```

**Motivo:** Este atributo es necesario para:
- Mejorar la accesibilidad web (lectores de pantalla)
- Optimización SEO
- Cumplir con estándares W3C

---

### 2. **src/App.jsx** - Corrección de Template Strings
**Problema:** Interpolación incorrecta de variables en template string
```javascript
// ❌ Antes (incorrecto)
GLOBAL_HISTORY.push(`${{A}}|${{B}}|${{op}}|${{r}}`);
```

**Solución:**
```javascript
// ✅ Después (correcto)
GLOBAL_HISTORY.push(`${A}|${B}|${op}|${r}`);
```

**Motivo:** La sintaxis correcta para interpolar variables en JavaScript es `${variable}`, no `${{variable}}`. La sintaxis anterior creaba objetos literales en lugar de interpolar los valores.

---

### 3. **package.json** - Seguridad de Tokens
**Problema:** Token de SonarQube expuesto en el código fuente

**Solución:**
- Se eliminó el token del archivo `package.json`
- Se configuró para pasar el token como parámetro de línea de comandos:
  ```bash
  npx sonar-scanner -Dsonar.token=<tu-token>
  ```

**Motivo:** Los tokens de autenticación nunca deben guardarse en el código fuente por razones de seguridad. Deben pasarse como variables de entorno o parámetros.

---

## Vulnerabilidades Intencionales (No Corregidas)

Este proyecto mantiene intencionalmente las siguientes vulnerabilidades para fines educativos:

1. **Prompt Injection**: La función `insecureBuildPrompt` concatena texto sin validación
2. **Estado Global Mutable**: Variable `GLOBAL_HISTORY` global
3. **Manejo de Errores Silencioso**: `catch` vacíos que ocultan errores
4. **Prompt Oculto en Base64**: Archivo `hidden.js` contiene un prompt malicioso codificado

---

## Ejecución del Análisis de SonarQube

### Instalación de Dependencias
```bash
npm install
npm install -g @sonar/scan
```

### Ejecutar Análisis
```bash
npx sonar-scanner -Dsonar.token=<tu-token-aqui>
```

### Configuración de SonarQube
El archivo `package.json` incluye la configuración básica:
- **Server URL**: `http://localhost:9000`
- **Project Key**: `badcalc-react-hidden`
- **Sources**: `src`

---

## Próximos Pasos Sugeridos

Para mejorar la calidad del código, considera:

1. ✅ **Validación de Entrada**: Implementar validación robusta en `badParse()`
2. ✅ **Manejo de Errores**: Registrar errores en lugar de ocultarlos
3. ✅ **Eliminar Estado Global**: Usar React Context o estado local
4. ✅ **Sanitización de Prompts**: Validar y sanitizar templates de LLM
5. ✅ **PropTypes**: Agregar validación de props en componentes

---

## Tecnologías Utilizadas
- **React** 18.2.0
- **Vite** 5.0.0
- **SonarQube** (análisis estático de código)
- **prop-types** 15.8.1

---

## Autor
Proyecto educativo para demostración de análisis de código con SonarQube.
