# README

Este proyecto consiste en un script de Python (llamado `haz`) que permite ejecutar comandos sugeridos por OpenAI GPT-4o-mini basándose en un prompt de acción que describes. El script:

1. **Lee** la variable de entorno `OPENAI_API_KEY`, necesaria para conectarse a la API de OpenAI.
2. **Acepta** una ruta de archivo opcional (tecleada al inicio).
3. **Lee** el prompt de acción, ya sea:
    - **Desde los argumentos de línea de comandos** (todo lo que escribas tras `haz`)
    - **O de manera interactiva** si no has pasado argumentos.
4. **Construye** y envía una solicitud a la API de OpenAI para que devuelva uno o más comandos de terminal.
5. **Filtra** la respuesta de OpenAI, detecta si contiene código (bloques de comando) y, de ser así, muestra los comandos encontrados y te pide confirmación para ejecutarlos en tu sistema.
6. Si la respuesta es puramente textual, la muestra por pantalla sin intentar ejecutar nada.

## Requisitos

1. **Python 3**
2. **`requests`** instalado (p.e. `pip install requests`)
3. **`jq`** instalado, si deseas manipular JSON en otras partes, aunque no sea obligatorio para este script en concreto.
4. Una **clave** de OpenAI (`OPENAI_API_KEY`) definida como variable de entorno.

Para comprobarlo en Linux o macOS, puedes hacer:
```bash
echo $OPENAI_API_KEY
```
Si no está definida, exporta tu clave de la siguiente forma:
```bash
export OPENAI_API_KEY="tu_api_key_aquí"
```

## Uso

1. **Haz ejecutable el script** (si no lo está ya):
   ```bash
   chmod +x haz
   ```

2. **Ejecuta**:
   ```bash
   ./haz [prompt de acción]
   ```
    - **Si pasas texto tras `haz`**, se considerará tu prompt de acción. Por ejemplo:
      ```bash
      ./haz lista los archivos de esta carpeta
      ```
    - **Si no pasas texto**, se te pedirá que introduzcas el prompt de acción de forma interactiva.

3. **Ruta de archivo opcional**:  
   Al arrancar, el script te preguntará por el archivo objetivo (si aplica). Si no lo necesitas, simplemente presiona *Enter*.

4. **Confirmación**:
    - Cuando OpenAI devuelva comandos, aparecerán en pantalla y el script te pedirá confirmación (`¿Quieres ejecutar estos comandos? (s/n)`).
    - Si respondes `s`, el script los ejecutará en tu sistema.

## Ejemplo

```bash
./haz eliminar todos los archivos .zip
```
1. El script te preguntará por el archivo objetivo (opcional).
2. Luego llama a OpenAI con el prompt “eliminar todos los archivos .zip”.
3. Si la respuesta es un bloque de código con comandos, se mostrarán y te pedirá confirmación para ejecutarlos.

## Notas de seguridad

- **Atención** al usar el script, sobre todo si la acción que pides a OpenAI incluye borrar, cambiar permisos o descargar archivos. Podrías recibir y ejecutar comandos peligrosos. Revísalos cuidadosamente antes de confirmar su ejecución.
- Siempre ten presente que, en última instancia, los comandos se ejecutan con tus permisos de usuario.

## Licencia

Este proyecto se distribuye bajo la [MIT License](https://opensource.org/licenses/MIT). Puedes utilizarlo, modificarlo y redistribuirlo libremente, siempre y cuando incluyas esta información de licencia.