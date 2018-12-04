---
title: Cómo usar el iniciador de Spring Boot para Azure Active Directory
description: Aprenda a configurar una aplicación de Spring Boot Initializer con el iniciador de Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 89e294fa739b59f87667f901e914fd5f050b5b8c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338779"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="cb8c8-103">Tutorial: Protección de una aplicación web de Java con Spring Boot Starter para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb8c8-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="cb8c8-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cb8c8-104">Overview</span></span>

<span data-ttu-id="cb8c8-105">En este artículo, se muestra cómo crear una aplicación de Java con **[Spring Initializr]**, que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb8c8-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb8c8-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb8c8-107">Crear una aplicación de Java mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="cb8c8-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="cb8c8-108">Configurar Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb8c8-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="cb8c8-109">Proteger la aplicación con las clases y anotaciones de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="cb8c8-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="cb8c8-110">Compilar y probar la aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="cb8c8-110">Build and test your Java application</span></span>

<span data-ttu-id="cb8c8-111">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb8c8-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb8c8-112">Prerequisites</span></span>

<span data-ttu-id="cb8c8-113">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="cb8c8-114">Un kit de desarrollo de Java (JDK) admitido</span><span class="sxs-lookup"><span data-stu-id="cb8c8-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="cb8c8-115">Para más información sobre los JDK disponibles para desarrollar en Azure, consulte <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="cb8c8-116">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="cb8c8-117">Creación de una aplicación con Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="cb8c8-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="cb8c8-118">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="cb8c8-119">Especifique que desea generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][create-spring-app-01]

1. <span data-ttu-id="cb8c8-121">Vaya a la sección **Core** y active la casilla **Security** (Seguridad) y, en la sección **Web**, active la casilla **Web**. Después, baje a la sección **Azure** y active la casilla **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Selección de los iniciadores Security, Web y Azure Active Directory][create-spring-app-02]

1. <span data-ttu-id="cb8c8-123">Desplácese a la parte inferior o superior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="cb8c8-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][create-spring-app-03]

1. <span data-ttu-id="cb8c8-125">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="cb8c8-126">Creación de una instancia de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb8c8-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="cb8c8-127">Creación de la instancia de Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb8c8-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="cb8c8-128">Inicie sesión en <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="cb8c8-129">Haga clic en **+Crear un recurso**, luego en **Identidad** y, por último, en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![Creación de una nueva instancia de Azure Active Directory][create-directory-01]

1. <span data-ttu-id="cb8c8-131">Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="cb8c8-132">Copie la dirección URL completa del directorio; se usará para agregar cuentas de usuario más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="cb8c8-133">(Por ejemplo, `wingtiptoysdirectory.onmicrosoft.com`). Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Especificación de los nombres de Azure Active Directory][create-directory-02]

1. <span data-ttu-id="cb8c8-135">Seleccione el nombre de cuenta en la parte superior derecha de la barra de herramientas de Azure Portal y haga clic en **Cambiar directorio**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Seleccione el nombre de su cuenta de Azure.][create-directory-03]

1. <span data-ttu-id="cb8c8-137">Seleccione la nueva instancia de Azure Active Directory en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Selección de la instancia de Azure Active Directory][create-directory-04]

1. <span data-ttu-id="cb8c8-139">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Propiedades** y copie el **Id. de directorio**; este valor se usará más adelante para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copia del identificador de Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="cb8c8-141">Adición de un registro de aplicación para la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="cb8c8-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="cb8c8-142">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Registros de aplicaciones** y haga clic en **Nuevos registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![Adición de un nuevo registro de aplicaciones][create-app-registration-01]

2. <span data-ttu-id="cb8c8-144">Especifique el valor de **Nombre** de la aplicación, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Crear registro de aplicaciones][create-app-registration-02]

4. <span data-ttu-id="cb8c8-146">Cuando aparezca la página para registrar la aplicación, copie su **Id. de aplicación**; usará este valor para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="cb8c8-147">Haga clic en **Configuración** y después en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-147">Click **Settings**, and then click **Keys**.</span></span>

   ![Creación de las claves del registro de aplicaciones][create-app-registration-03]

5. <span data-ttu-id="cb8c8-149">Agregue una **Descripción**, especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tendrá que copiar el valor de la clave para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="cb8c8-150">(No podrá recuperar este valor más adelante).</span><span class="sxs-lookup"><span data-stu-id="cb8c8-150">(You will not be able to retrieve this value later.)</span></span>

   ![Especificación de los parámetros de clave del registro de aplicaciones][create-app-registration-04]

6. <span data-ttu-id="cb8c8-152">En la página principal del registro de aplicaciones, haga clic en **Configuración** y **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permisos necesarios del registro de aplicaciones][create-app-registration-05]

7. <span data-ttu-id="cb8c8-154">Haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-154">Click **Windows Azure Active Directory**.</span></span>

   ![Selección de Microsoft Azure Active Directory][create-app-registration-06]

8. <span data-ttu-id="cb8c8-156">Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar los permisos de acceso][create-app-registration-07]

9. <span data-ttu-id="cb8c8-158">En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Concesión de permisos de acceso][create-app-registration-08]

10. <span data-ttu-id="cb8c8-160">En la página principal del registro de aplicación, haga clic en **Configuración** y, a continuación, haga clic en **URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Edición de las URL de respuesta][create-app-registration-09]

11. <span data-ttu-id="cb8c8-162">Escriba "<http://localhost:8080/login/oauth2/code/azure>" como nueva dirección URL de respuesta y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Adición de una nueva URL de respuesta][create-app-registration-10]

12. <span data-ttu-id="cb8c8-164">En la página principal para el registro de aplicación, haga clic en **Manifiesto**, establezca el valor del parámetro `oauth2AllowImplicitFlow` en `true` y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Configuración del manifiesto de aplicación][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="cb8c8-166">Para más información acerca del parámetro `oauth2AllowImplicitFlow` y otras opciones de configuración de la aplicación, consulte [Manifiesto de aplicación de Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="cb8c8-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="cb8c8-167">Adición de una cuenta de usuario al directorio y adición de esa cuenta a un grupo</span><span class="sxs-lookup"><span data-stu-id="cb8c8-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="cb8c8-168">En la página **Información general** de Active Directory, haga clic en **Todos los usuarios** y en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![Agregar una nueva cuenta de usuario][create-user-01]

1. <span data-ttu-id="cb8c8-170">Cuando se muestre el panel **Usuario**, escriba **Nombre** y el **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Especificar la información de la cuenta de usuario][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="cb8c8-172">Al escribir el nombre de usuario, debe especificar la misma dirección URL del directorio que usamos anteriormente en este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="cb8c8-173">Haga clic en **Grupos**, seleccione los grupos que usará para autorización en la aplicación y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="cb8c8-174">(Para este tutorial, agregue la cuenta al grupo _Usuarios_).</span><span class="sxs-lookup"><span data-stu-id="cb8c8-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Seleccionar los grupos del usuario][create-user-03]

1. <span data-ttu-id="cb8c8-176">Haga clic en **Mostrar contraseña** y copie la contraseña; se usará para iniciar sesión en la aplicación más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="cb8c8-177">Cuando haya copiado la contraseña, haga clic en **Crear** para agregar la nueva cuenta de usuario al directorio.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![Mostrar la contraseña][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="cb8c8-179">Configuración y compilación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cb8c8-179">Configure and compile your app</span></span>

1. <span data-ttu-id="cb8c8-180">Extraiga los archivos del proyecto que creó y descargó en un directorio anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="cb8c8-181">Vaya a la carpeta principal del proyecto y abra el archivo del proyecto de Maven `pom.xml` en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="cb8c8-182">Agregue las dependencias para la seguridad OAuth2 de Spring a `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

1. <span data-ttu-id="cb8c8-183">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="cb8c8-184">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="cb8c8-185">Especifique la configuración del registro de su aplicación con los valores que creó anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="cb8c8-186">Donde:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-186">Where:</span></span>

   | <span data-ttu-id="cb8c8-187">Parámetro</span><span class="sxs-lookup"><span data-stu-id="cb8c8-187">Parameter</span></span> | <span data-ttu-id="cb8c8-188">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="cb8c8-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="cb8c8-189">Contiene su **Id. de directorio** de Active Directory obtenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="cb8c8-190">Contiene el **Id. de aplicación** del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="cb8c8-191">Contiene el **Valor** de la clave del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="cb8c8-192">Contiene una lista de los grupos de Active Directory que se usarán para la autorización.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="cb8c8-193">Para obtener una lista completa de los valores disponibles en su archivo *application.properties*, consulte el [ejemplo de Azure Active Directory Spring Boot][AAD Spring Boot Sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="cb8c8-194">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="cb8c8-195">Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="cb8c8-196">Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="cb8c8-197">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-197">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="cb8c8-198">El nombre del grupo que especifique para el método `@PreAuthorize("hasRole('')")` debe contener uno de los grupos que especificó en el campo `azure.activedirectory.active-directory-groups` del archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="cb8c8-199">Puede especificar una configuración de autorización diferente para diferentes asignaciones de solicitudes; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

1. <span data-ttu-id="cb8c8-200">Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="cb8c8-201">Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="cb8c8-202">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-202">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="cb8c8-203">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cb8c8-203">Build and test your app</span></span>

1. <span data-ttu-id="cb8c8-204">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="cb8c8-205">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cb8c8-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Compilación de la aplicación][build-application]

1. <span data-ttu-id="cb8c8-207">Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080> en un explorador web; se le pedirá un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Inicio de sesión en su aplicación][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="cb8c8-209">Se le pedirá que cambie su contraseña si es el primer inicio de sesión de una cuenta de usuario nueva.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Cambiar la contraseña][update-password]
   > 

1. <span data-ttu-id="cb8c8-211">Cuando haya iniciado sesión correctamente, verá ver el texto de ejemplo "Hello World" desde el controlador.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Inicio de sesión correcto][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="cb8c8-213">Las cuentas de usuario que no están autorizadas recibirán un mensaje **HTTP 403 No autorizado**.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="cb8c8-214">Resumen</span><span class="sxs-lookup"><span data-stu-id="cb8c8-214">Summary</span></span>

<span data-ttu-id="cb8c8-215">En este tutorial, ha creado una nueva aplicación web de Java mediante el iniciador de Azure Active Directory, ha configurado un nuevo inquilino de Azure AD y ha registrado una nueva aplicación en él; después, ha configurado la aplicación para que use las clases y anotaciones de Spring para proteger la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb8c8-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb8c8-216">Next steps</span></span>

<span data-ttu-id="cb8c8-217">Para más información acerca de Spring y Azure, vaya al centro de documentación de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8c8-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb8c8-218">Spring en Azure</span><span class="sxs-lookup"><span data-stu-id="cb8c8-218">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
