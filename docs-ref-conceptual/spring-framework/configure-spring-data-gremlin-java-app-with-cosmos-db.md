---
title: Uso de Spring Data Gremlin Starter con SQL API de Azure Cosmos DB
description: Aprenda a configurar una aplicación creada con Spring Boot Initializer con SQL API de Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 70bed5696048af1de857f1064bf98e83ab96ca53
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991569"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a>Uso de Spring Data Gremlin Starter con SQL API de Azure Cosmos DB

## <a name="overview"></a>Información general

Spring Data Gremlin Starter proporciona compatibilidad con Spring Data para el lenguaje de consultas Gremlin de Apache, que los desarrolladores pueden usar con cualquier almacén de datos compatibles con Gremlin.

En este artículo se muestra cómo crear una base de datos de Azure Cosmos DB mediante Azure Portal para usarla con la API de Gremlin, cómo usar **[Spring Initializr]** para crear una aplicación Java personalizada y, después, cómo agregar la funcionalidad Spring Data Gremlin Starter a su aplicación personalizada para almacenar datos en Azure Cosmos DB y recuperarlos mediante Gremlin.

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Un kit de desarrollo de Java (JDK) admitido Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

> [!IMPORTANT]
>
> Se necesita Spring Boot versión 2.0 o posteriores para completar los pasos descritos en este artículo.
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a>Creación de una base de datos de Azure Cosmos DB mediante Azure Portal

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a>Creación de la base de datos de Azure Cosmos DB para su uso con la API de Gremlin

1. Vaya a Azure Portal en <https://portal.azure.com/> y haga clic en **+Crear un recurso**.

   ![Creación de un recurso][AZ01]

1. Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.

   ![Creación de una base de datos de Azure Cosmos DB][AZ02]

1. En la página **Azure Cosmos DB**, escriba la información siguiente:

   * Escriba un **identificador** único, que usará como identificador URI de la base de datos. Por ejemplo: si especificó **wingtiptoysdata** como valor de **ID**, el URI de Gremlin sería *wingtiptoysdata.gremlin.cosmosdb.azure.com*.
   * Elija **Gremlin (Graph)** para la API.
   * Elija la **suscripción** que quiere usar para la base de datos.
   * Especifique si quiere crear un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos diferente.
   * Especifique la **ubicación** de la base de datos.
   
   Cuando haya especificado estas opciones, haga clic en **Crear** para crear la base de datos.

   ![Especificación de las opciones de Azure Cosmos DB][AZ03]

1. Cuando se ha creado la base de datos, se muestra en el **panel** de Azure, así como en las páginas **Todos los recursos** y **Azure Cosmos DB**. Puede hacer clic en la base de datos en cualquiera de esas ubicaciones para abrir la página de propiedades de la caché.

   ![Todos los recursos][AZ04]

1. Cuando se muestre la página de propiedades de la base de datos, haga clic en **Claves de acceso** y copie el identificador URI y las claves de acceso de la base de datos; usará estos valores en su aplicación de Spring Boot.

   ![Claves de acceso][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a>Adición de un gráfico a la base de datos de Azure Cosmos DB

1. Haga clic en **Explorador de datos** y después en **Nuevo grafo**.

   ![Nuevo grafo][AZ06]

1. Cuando aparezca la página **Agregar grafo**, especifique la información siguiente:

   * Especifique un **Id. de base de datos** único para la base de datos.
   * Especifique un **Id. de grafo** único para el grafo.
   * Puede elegir especificar la **Capacidad de almacenamiento** o puede aceptar el valor predeterminado.
   * Especifique el valor de **Rendimiento**; para este ejemplo, puede elegir 400 unidades de solicitud (RU).
   
   Cuando haya especificado estas opciones, haga clic en **Crear** para crear el grafo.

   ![Agregar grafo][AZ07]

1. Una vez creado el grafo, puede usar el **Explorador de datos** para verlo.

   ![Visualización de las propiedades del grafo][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Creación de una aplicación sencilla de Spring Boot con Spring Initializr

1. Vaya a <https://start.spring.io/>.

1. Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación, especifique en **Spring Boot** una versión que sea igual o posterior a 2.0 y, luego, haga clic en el botón **Generate Project** (Generar proyecto).

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr usa los nombres de **Group** (Grupo) y **Artifact** (Artefacto) para crear el nombre del paquete, por ejemplo: *com.example.wintiptoysdata.
   >

1. Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. Después de extraer los archivos en el sistema local, la aplicación sencilla de Spring Boot estará lista para editarla.

   ![Archivos de proyecto personalizados de Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a>Configuración de la aplicación de Spring Boot para usar Spring Data Gremlin Starter

1. Busque el archivo *pom.xml* en el directorio de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   O bien

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Guarde el archivo pom.xml.][PM01]

1. Abra el archivo *pom.xml* en un editor de texto y agregue Spring Data Gremlin Starter a la lista `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Edición del archivo pom.xml][PM02]

1. Guarde y cierre el archivo *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Configuración de la aplicación de Spring Boot para usar Azure Cosmos DB

1. Busque el directorio *resources* de la aplicación y cree un nuevo archivo llamado *application.yml*. Por ejemplo: 

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Creación del archivo application.yml][RE01]

1. Abra el archivo *application.yml* en un editor de texto y agréguele las siguientes líneas; a continuación, sustituya los valores de ejemplo por las propiedades adecuadas de su base de datos:

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   
   Donde:
   
   | Campo | DESCRIPCIÓN |
   |---|---|
   | `endpoint` | Especifica el URI de Gremlin para la base de datos, que deriva del **ID** único que especificó al crear la base de datos de Azure Cosmos DB anteriormente en este tutorial. |
   | `port` | Especifica el puerto TCP/IP, que debería ser **443** para HTTPS. |
   | `username` | Especifica los valores únicos **Id. de base de datos** e **Id. de grafo** que usó al agregar el grafo anteriormente en este tutorial; debe especificarse con la siguiente sintaxis: "/dbs/**{id. de base de datos}**/colls/**{id. de grafo}**". |
   | `password` | Especifica la **clave de acceso** principal o secundario que copió anteriormente en este tutorial. |
   | `telemetryAllowed` | Especifique **true** si desea habilitar los datos de telemetría; en caso contrario, **false**.

1. Guarde y cierre el archivo *application.yml*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Adición de ejemplo de código para implementar funcionalidad básica de base de datos

En esta sección, creará las clases de Java necesarias para almacenar datos en la base de datos.

### <a name="modify-the-main-application-class"></a>Modificación de la clase de aplicación principal

1. Busque el archivo de Java de la aplicación principal en el directorio del paquete de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Búsqueda del archivo de Java de la aplicación][JV01]

1. Abra el archivo de Java de la aplicación principal en un editor de texto y agregue las siguientes líneas al archivo:

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. Guarde y cierre el archivo de Java de la aplicación principal.

### <a name="define-a-basic-class-for-storing-configuration-information"></a>Definición de una clase básica para almacenar información de configuración

1. Cree una carpeta llamada *config* en el directorio del paquete de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. Cree un archivo Java nuevo llamado *UserRepositoryConfiguration.java* en el directorio *config*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. Guarde y cierre el archivo *UserRepositoryConfiguration.java*.

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a>Definición del conjunto de clases que definen los elementos de la base de datos de grafos

1. Cree una carpeta llamada *domain* en el directorio del paquete de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. Cree un archivo Java nuevo llamado *Person.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. Guarde y cierre el archivo *Person.java*.

1. Cree un archivo Java nuevo llamado *Relation.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. Guarde y cierre el archivo *Relation.java*.

1. Cree un archivo Java nuevo llamado *Network.java* en el directorio *domain*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. Guarde y cierre el archivo *Network.java*.

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a>Definición del conjunto de clases que definen los repositorios de la base de datos de grafos

1. Cree una carpeta llamada *repository* en el directorio del paquete de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   O bien

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. Cree un archivo Java nuevo llamado *NetworkRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. Guarde y cierre el archivo *NetworkRepository.java*.

1. Cree un archivo Java nuevo llamado *PersonRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. Guarde y cierre el archivo *PersonRepository.java*.

1. Cree un archivo Java nuevo llamado *RelationRepository.java* en el directorio *repository*; a continuación, abra el archivo en un editor de texto y agregue las siguientes líneas:

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. Guarde y cierre el archivo *RelationRepository.java*.

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml*; por ejemplo:

   `cd C:\SpringBoot\wingtiptoysdata`

   O bien

   `cd /users/example/home/wingtiptoysdata`

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. La aplicación mostrará varios mensajes en tiempo de ejecución y, si no hay errores, puede usar Azure Portal para ver el contenido de su base de datos de Azure Cosmos DB. Para ello, haga clic en el **Explorador de datos** en la página de propiedades de la base de datos, a continuación, haga clic en **Ejecutar consulta de Gremlin** y, a continuación, seleccione un elemento de la lista de resultados para ver los datos.

   ![Uso del Explorador de documentos para ver los datos][JV03]

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.

> [!div class="nextstepaction"]
> [Spring en Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionales

Consulte los siguientes artículos para más información sobre la compatibilidad de Azure para Gremlin y Graph API:

* [Introducción a Azure Cosmos DB: Graph API](/azure/cosmos-db/graph-introduction)

* [Compatibilidad de Azure Cosmos DB con grafos de Gremlin](/azure/cosmos-db/gremlin-support)

* [Azure Cosmos DB: Creación una base de datos de grafos mediante Java y Azure Portal](/azure/cosmos-db/create-graph-java)

* [Tutorial: Consulta de Graph API de Azure Cosmos DB mediante Gremlin](/azure/cosmos-db/tutorial-query-graph)

* [Spring Data Gremlin Starter]

Para más información sobre el uso de Azure Cosmos DB y Java, consulte los siguientes artículos:

* [Documentación sobre Azure Cosmos DB]

* [Azure Cosmos DB: Creación de una base de datos de documentos mediante Java y Azure Portal][Build a SQL API app with Java]

* [Spring Data para SQL API de Azure Cosmos DB]

Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:

* [Implementación de una aplicación de Spring Boot en Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Working with Azure DevOps and Java] (Trabajo con Azure DevOps y Java).

**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes. Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>. Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Azure para desarrolladores de Java]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data para SQL API de Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Trabajo con Azure DevOps y Java)
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
