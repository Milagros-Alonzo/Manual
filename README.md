# Manual
Manual para la creación de la fuente de datos ODBC, hasta la conexión hacia esta desde JDBC
##Manual que muestre desde la creación de la fuente de datos ODBC, hasta la conexión hacia esta desde JDBC.

## Creación de la fuente de datos ODBC 
###  1. Abrir el Panel de control:
Haz clic en el botón de "Inicio" de Windows y selecciona "Panel de control".

### 2. Acceder a las fuentes de datos ODBC:
Dependiendo de la versión de Windows que estés utilizando, busca una de las siguientes opciones:

En Windows 10 y Windows 8: En el Panel de control, selecciona "Sistema y seguridad" y luego "Herramientas administrativas". A continuación, haz clic en "Orígenes de datos ODBC".
En versiones anteriores de Windows (por ejemplo, Windows 7): En el Panel de control, busca y selecciona "Herramientas administrativas" y luego haz doble clic en "Orígenes de datos ODBC".
[![Whats-App-Image-2023-07-22-at-1-29-06-PM-2.jpg](https://i.postimg.cc/Vkh3mzGY/Whats-App-Image-2023-07-22-at-1-29-06-PM-2.jpg)](https://postimg.cc/SnWZGbb5)
### 3.Crear una nueva fuente de datos:
Dentro de la ventana "Administrador de orígenes de datos ODBC", ve a la pestaña "DSN de usuario" o "DSN del sistema", según prefieras. Seleccionar "DSN de usuario" permitirá que la fuente de datos esté disponible solo para tu usuario, mientras que "DSN del sistema" la hará accesible para todos los usuarios del sistema. Por cuestiones de seguridad, es recomendable utilizar "DSN de usuario" si no tienes razones específicas para utilizar "DSN del sistema".

Ventana del Administrador ODBC:
[![Captura-de-pantalla-2023-07-25-222221.png](https://i.postimg.cc/Pqh5zC1X/Captura-de-pantalla-2023-07-25-222221.png)](https://postimg.cc/nXRxncdg)
### 4. Seleccionar el controlador de la base de datos:
Haz clic en el botón "Agregar" para ver una lista de controladores de base de datos disponibles. Elige el controlador apropiado para la base de datos que deseas conectar. Si no ves el controlador en la lista, es posible que debas instalarlo antes de continuar.

[![Captura-de-pantalla-2023-07-25-222243.png](https://i.postimg.cc/TYJd2RZB/Captura-de-pantalla-2023-07-25-222243.png)](https://postimg.cc/dLDP4KQ9)


### 5. Configurar la fuente de datos: 
Rellena los campos necesarios para configurar la conexión con tu base de datos. Los campos requeridos pueden variar según el tipo de base de datos y el controlador que estés utilizando. Aquí hay algunos campos comunes que deberás completar:

- Nombre: Asigna un nombre descriptivo para la fuente de datos ODBC.
- Descripción: Proporciona una descripción opcional para identificar la fuente de datos.
- Servidor: Especifica la ubicación o dirección IP del servidor de la base de datos.
- Base de datos: Indica el nombre de la base de datos a la que deseas conectarte.
- Autenticación: Elige el tipo de autenticación que utilizarás para acceder a la base de datos (por ejemplo, usuario y contraseña).

Ventana para visualizar los conectores:
[![imagen-2023-07-25-231655291.png](https://i.postimg.cc/DfjRK6PV/imagen-2023-07-25-231655291.png)](https://postimg.cc/ThbtVrsQ)


### 6.Probar la conexión:
Algunos asistentes de configuración te permitirán probar la conexión antes de finalizar. Asegúrate de probarla para verificar que todo esté configurado correctamente.

### 7. Finalizar la configuración: 
Una vez que hayas completado todos los campos necesarios y probado la conexión, haz clic en "Aceptar" o "Finalizar" para guardar la fuente de datos ODBC.


[![imagen-2023-07-25-232229803.png](https://i.postimg.cc/kGJVF9hH/imagen-2023-07-25-232229803.png)](https://postimg.cc/sQLD3FzP)
### 8. Verificar la fuente de datos: 
Regresa a la lista de fuentes de datos ODBC en el "Administrador de orígenes de datos ODBC" para asegurarte de que la nueva fuente de datos se haya creado correctamente.

[![imagen-2023-07-25-232445170.png](https://i.postimg.cc/CKMLQJ4Z/imagen-2023-07-25-232445170.png)](https://postimg.cc/TKS6yVFG)



## ** Conexión del ODBC a JDBC **

Una vez se halla logrado la creación de las fuentes ODBC pasaremos a Java para hacer la coneccion al JDBC, en este caso en particular utilizaremos MariaDB como base de datos.
Lo primero es tener una base de datos creadas para poder hacer la conexión.

[![imagen-2023-07-24-000234502.png](https://i.postimg.cc/9MDwFJg7/imagen-2023-07-24-000234502.png)](https://postimg.cc/sQRgT9rj)

Como se logra ver ya tengo varias bases de datos creadas y en esta ocación utilizare la llamada  "datos" para hacer el ejemplo de conexion.
Luego  de esto seguimos con la conexion en java y para esto debemos seguir los siguientes pasos:

1. Importar las clases necesarias: Asegúrate de importar las clases necesarias para la conexión JDBC. Esto incluye las clases 
```
java.sql.Connection
java.sql.DriverManager
java.sql.SQLException.
```
2. Cargar el controlador JDBC: Antes de establecer la conexión, debes cargar el controlador JDBC correspondiente para MariaDB. Para versiones más recientes de MariaDB, se utiliza el controlador org.mariadb.jdbc.Driver. Para cargar el controlador, utiliza Class.forName().

3. Establecer la conexión: Utiliza la clase java.sql.Connection para establecer la conexión con la base de datos MariaDB. Debes proporcionar la URL de conexión que incluya la información del servidor, la base de datos y las credenciales de acceso.

3. Realizar operaciones en la base de datos: Una vez establecida la conexión, puedes utilizar la clase java.sql.Statement para enviar consultas SQL a la base de datos y obtener resultados.

4. Cerrar la conexión: Cuando hayas terminado de utilizar la conexión, asegúrate de cerrarla para liberar los recursos.


Al final el código completo sería el siguiente:
```
package com.mycompany.conexionjdbc;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConexionJDBC {
    public static void main(String[] args) {
        // Datos de conexión
        String jdbcURL = "jdbc:mariadb://localhost:3306/datos";
        String usuario = "estudiante";
        String contraseña = "estudiante";

        try {
            // Cargar el controlador JDBC para MariaDB
            Class.forName("org.mariadb.jdbc.Driver");

            // Establecer la conexión
            Connection connection = DriverManager.getConnection(jdbcURL, usuario, contraseña);

            // Realizar operaciones en la base de datos
            Statement statement = connection.createStatement();
            String sqlQuery = "SELECT * FROM datos";
            ResultSet resultSet = statement.executeQuery(sqlQuery);

            while (resultSet.next()) {
                // Procesar los resultados
                // Por ejemplo: String columna1 = resultSet.getString("nombre_columna");
            }

            // Cerrar los recursos
            resultSet.close();
            statement.close();
            connection.close();
        } catch (ClassNotFoundException | SQLException e) {
        }
    }
}
```



###End
