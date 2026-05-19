# sistema_usuarios

# Sistema Modular de Gestión de Usuarios

Proyecto integrador que aplica:
- Entornos virtuales (venv)
- Gestión de dependencias (pip + requirements.txt)
- Variables de entorno (python-dotenv)
- Módulos y paquetes
- Importaciones absolutas y relativas

## Capturas de pantalla explicadas

### Creación del entorno virtual
![Creación entorno virtual](/images/Creación%20entorno%20virtual.png)

Se ejecutó "python -m venv venv" para crear un entorno virtual aislado. Esto genera la carpeta "venv/" con su propio intérprete y espacio de paquetes.

### Instalación de dependencias
![Instalando dependencias](/images/Instalando%20dependencias.png)

Con el entorno activado, se instaló "python-dotenv" usando "pip". La salida muestra la descarga exitosa del paquete.

### Ejecución del reto
![Ejecución del reto](/images/Ejecución%20reto.png)

### Registro de usuario (Opción 1)
![Opción 1](/images/Opción%201.png)

El usuario ingresa nombre, edad y email. El sistema valida los datos y asigna un ID automático. En este ejemplo se registró a Mateo con ID 1.

### Listado de usuarios (Opción 2)
![Opción 2](/images/Opción%202.png)

Muestra todos los usuarios registrados. Aquí aparece Mateo con sus datos.

### Búsqueda de usuario (Opción 3)
![Opción 3](/images/Opción%203.png)

Busca por nombre o email (coincidencia parcial, sin distinguir mayúsculas). Se buscó "Mateo" y se encontró el usuario correspondiente.

### Eliminación de usuario (Opción 4)
![Opción 4](/images/Opción%204.png)

Se solicita el ID del usuario a eliminar. En este caso se eliminó el ID 1, y el sistema confirma la acción.

### Salida del sistema (Opción 5)
![Opción 5](/images/Opción%205.png)

Al seleccionar la opción 5, el programa termina con un mensaje de despedida.

## 🧱 Explicación de la estructura modular del proyecto

El proyecto sigue una organización clara por responsabilidades, facilitando el mantenimiento y la escalabilidad.


## Módulos y sus responsabilidades

- **"app/config/settings.py"**  
  Usa "load_dotenv()" para leer el archivo ".env" y expone variables como "APP_NAME", "APP_VERSION", "ADMIN_USER". Centraliza toda la configuración sensible.

- **"app/usuarios/validaciones.py"**  
  Contiene funciones puras (sin efectos secundarios) que validan datos: "validar_nombre()", "validar_edad()", "validar_email()". Lanzan excepciones "ValueError" si algo falla.

- **"app/usuarios/gestor.py"**  
  Implementa la lógica de negocio:  
  - "registrar_usuario()": valida y agrega un usuario a una lista en memoria.  
  - "listar_usuarios()": retorna copia de la lista.  
  - "buscar_usuario()": filtra por nombre o email.  
  - "eliminar_usuario()": remueve por ID.  
  Usa importaciones relativas para traer las validaciones ("from .validaciones import ...").

- **"main.py"**  
  Es el orquestador: importa desde "app" las funciones necesarias, presenta el menú interactivo y maneja las excepciones. No contiene lógica de negocio ni validaciones.

## Flujo de importaciones

- Las importaciones dentro del paquete son **relativas** (ej. "from .validaciones import ...") para mayor claridad y portabilidad.  
- Desde "main.py" se usan **importaciones absolutas** (ej. "from app import registrar_usuario"), porque "main.py" está fuera del paquete "app".

## Variables de entorno

- El archivo ".env" (ignorado por Git) contiene:  

- APP_NAME=Sistema Gestión de Usuarios.
- APP_VERSION=1.0.
- ADMIN_USER=admin.

- "settings.py" los lee y los pone a disposición del resto del proyecto. Así, si se necesita cambiar el nombre de la aplicación, solo se modifica el ".env", no el código.

## Ventajas de esta modularización

1. **Separación de responsabilidades**: cada módulo tiene un propósito único.  
2. **Reutilización**: las validaciones y el gestor pueden importarse en otros proyectos.  
3. **Mantenibilidad**: corregir una validación no afecta al menú ni a la configuración.  
4. **Seguridad**: las credenciales no quedan fijas en el código.  
5. **Colaboración**: varios desarrolladores pueden trabajar en diferentes submódulos sin conflictos.

Aquí tienes una **breve conclusión textual** para incluir al final de tu README, informe o video reflexivo:

## Conclusión

Este proyecto integrador permitió aplicar de forma práctica los conceptos fundamentales de organización profesional en Python. La **modularización** facilitó la separación de responsabilidades, haciendo el código más mantenible y reutilizable. El uso de **entornos virtuales** evitó conflictos entre dependencias y aseguró la reproducibilidad del entorno mediante "requirements.txt". Las **variables de entorno** con "python-dotenv" protegieron información sensible y permitieron cambiar la configuración sin modificar el código fuente. Como resultado, se obtuvo un sistema funcional de gestión de usuarios que cumple con buenas prácticas de desarrollo, escalabilidad y seguridad. Este reto demostró que aplicar estos conceptos desde el inicio de un proyecto ahorra tiempo, reduce errores y facilita el trabajo en equipo.
