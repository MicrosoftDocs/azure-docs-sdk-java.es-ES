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
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 6d20593620c7fb73f8481be8705bdc42d4e9ce32
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2018
ms.locfileid: "37864055"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="35e4f-103">Cómo usar el iniciador de Spring Boot para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35e4f-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="35e4f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="35e4f-104">Overview</span></span>

<span data-ttu-id="35e4f-105">En este artículo se muestra cómo crear una aplicación con **[Spring Initializr]** que usa la funcionalidad Spring Boot Starter para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35e4f-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35e4f-106">requisitos previos</span><span class="sxs-lookup"><span data-stu-id="35e4f-106">Prerequisites</span></span>

<span data-ttu-id="35e4f-107">Los siguientes requisitos previos son necesarios para seguir los pasos descritos en este artículo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="35e4f-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [Ventajas para suscriptores de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="35e4f-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="35e4f-109">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="35e4f-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="35e4f-110">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="35e4f-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="35e4f-111">Creación de una aplicación personalizada mediante Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="35e4f-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="35e4f-112">Vaya a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="35e4f-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="35e4f-113">Especifique que quiere generar un proyecto de **Maven** con **Java**, escriba los nombres de **Group** (Grupo) y **Artifact** (Artefacto) de su aplicación y luego haga clic en el vínculo **Switch to the full version** (Cambiar a la versión completa) de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="35e4f-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar los nombres de grupo y artefacto][security-01]

1. <span data-ttu-id="35e4f-115">Vaya a la sección **Core** y active la casilla **Security** (Seguridad); en la sección **Web**, active la casilla **Web**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selección de los iniciadores Security y Web][security-02]

1. <span data-ttu-id="35e4f-117">Vaya a la sección **Azure** y active la casilla **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Seleccionar el iniciador Azure Active Directory][security-03]

1. <span data-ttu-id="35e4f-119">Desplácese a la parte inferior de la página y haga clic en el botón **Generate Project** (Generar proyecto).</span><span class="sxs-lookup"><span data-stu-id="35e4f-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Generación del proyecto de Spring Boot][security-04]

1. <span data-ttu-id="35e4f-121">Cuando se le solicite, descargue el proyecto en una ruta de acceso del equipo local.</span><span class="sxs-lookup"><span data-stu-id="35e4f-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="35e4f-122">Creación y configuración de una nueva instancia de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35e4f-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="35e4f-123">Creación de la instancia de Active Directory</span><span class="sxs-lookup"><span data-stu-id="35e4f-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="35e4f-124">Inicie sesión en <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="35e4f-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="35e4f-125">Haga clic en **+Nuevo**, luego en **Seguridad e identidad** y, por último, en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Creación de una nueva instancia de Azure Active Directory][directory-01]

1. <span data-ttu-id="35e4f-127">Rellene los campos **Nombre de la organización** y **Nombre de dominio inicial**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-127">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="35e4f-128">Copie la dirección URL completa del directorio; se usará para agregar cuentas de usuario más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-128">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="35e4f-129">(Por ejemplo, `wingtiptoysdirectory.onmicrosoft.com`). Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-129">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Especificación de los nombres de Azure Active Directory][directory-02]

1. <span data-ttu-id="35e4f-131">Seleccione la nueva instancia de Azure Active Directory en el menú desplegable, en la barra de herramientas superior de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="35e4f-131">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Selección de la instancia de Azure Active Directory][directory-03]

1. <span data-ttu-id="35e4f-133">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Propiedades** y copie el **Id. de directorio**; este valor se usará más adelante para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-133">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copia del identificador de Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="35e4f-135">Adición de un registro de aplicación para la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="35e4f-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="35e4f-136">Seleccione **Azure Active Directory** en el menú del portal, haga clic en **Información general** y haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-136">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adición de un nuevo registro de aplicaciones][directory-04]

1. <span data-ttu-id="35e4f-138">Haga clic en **Nuevo registro de aplicaciones**, especifique el valor de **Nombre de la aplicación**, use http://localhost:8080 como **URL de inicio de sesión** y, por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-138">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Crear registro de aplicaciones][directory-05]

1. <span data-ttu-id="35e4f-140">Haga clic en su registro de aplicaciones después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="35e4f-140">Click your application registration after it has been created.</span></span>

   ![Selección del registro de aplicaciones][directory-06]

1. <span data-ttu-id="35e4f-142">Cuando aparezca la página para registrar la aplicación, copie su **Id. de aplicación**; usará este valor para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-142">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="35e4f-143">Haga clic en **Configuración** y después en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-143">Click **Settings**, and then click **Keys**.</span></span>

   ![Creación de las claves del registro de aplicaciones][directory-07]

1. <span data-ttu-id="35e4f-145">Agregue una **Descripción**, especifique la **Duración** de la nueva clave y haga clic en **Guardar**; el valor de la clave se rellenará automáticamente al hacer clic en el icono **Guardar**, y tendrá que copiar el valor de la clave para configurar el archivo *application.properties* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-145">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="35e4f-146">(No podrá recuperar este valor más adelante).</span><span class="sxs-lookup"><span data-stu-id="35e4f-146">(You will not be able to retrieve this value later.)</span></span>

   ![Especificación de los parámetros de clave del registro de aplicaciones][directory-08]

1. <span data-ttu-id="35e4f-148">En la página principal del registro de aplicaciones, haga clic en **Configuración** y **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-148">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permisos necesarios del registro de aplicaciones][directory-09]

1. <span data-ttu-id="35e4f-150">Haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-150">Click **Windows Azure Active Directory**.</span></span>

   ![Selección de Microsoft Azure Active Directory][directory-10]

1. <span data-ttu-id="35e4f-152">Active las casillas **Acceder al directorio como usuario con sesión iniciada** y **Iniciar sesión y leer el perfil del usuario**, y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-152">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar los permisos de acceso][directory-11]

1. <span data-ttu-id="35e4f-154">En la página **Permisos necesarios**, haga clic en **Conceder permisos** y responda **Sí** a la pregunta.</span><span class="sxs-lookup"><span data-stu-id="35e4f-154">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Concesión de permisos de acceso][directory-12]

1. <span data-ttu-id="35e4f-156">En la página principal del registro de aplicación, haga clic en **Configuración** y, a continuación, haga clic en **URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-156">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Edición de las URL de respuesta][directory-14]

1. <span data-ttu-id="35e4f-158">Escriba "http://localhost:8080/login/oauth2/code/azure" como nueva dirección URL de respuesta y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-158">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Adición de una nueva URL de respuesta][directory-15]

1. <span data-ttu-id="35e4f-160">En la página principal para el registro de aplicación, haga clic en **Manifiesto**, establezca el valor del parámetro `oauth2AllowImplicitFlow` en `true` y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-160">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

   ![Configuración del manifiesto de aplicación][directory-16]

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-162">Para más información acerca del parámetro `oauth2AllowImplicitFlow` y otras opciones de configuración de la aplicación, consulte [Manifiesto de aplicación de Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="35e4f-162">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="35e4f-163">Adición de una cuenta de usuario al directorio y adición de esa cuenta a un grupo</span><span class="sxs-lookup"><span data-stu-id="35e4f-163">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="35e4f-164">En la página **Información general** de Active Directory, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-164">From the **Overview** page of your Active Directory, click **Users**.</span></span>

   ![Abrir el panel Usuarios][directory-17]

1. <span data-ttu-id="35e4f-166">Cuando se muestre el panel **Usuarios**, haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-166">When the **Users** panel is displayed, click **New user**.</span></span>

   ![Agregar una nueva cuenta de usuario][directory-18]

1. <span data-ttu-id="35e4f-168">Cuando se muestre el panel **Usuario**, escriba **Nombre** y el **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-168">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Especificar la información de la cuenta de usuario][directory-19]

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-170">Al escribir el nombre de usuario, debe especificar la misma dirección URL del directorio que usamos anteriormente en este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-170">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="35e4f-171">Haga clic en **Grupos**, seleccione los grupos que usará para autorización en la aplicación y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-171">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="35e4f-172">(Para este tutorial, agregue la cuenta al grupo _Usuarios_).</span><span class="sxs-lookup"><span data-stu-id="35e4f-172">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Seleccionar los grupos del usuario][directory-20]

1. <span data-ttu-id="35e4f-174">Haga clic en **Mostrar contraseña** y copie la contraseña; se usará para iniciar sesión en la aplicación más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-174">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span>

   ![Mostrar la contraseña][directory-21]

1. <span data-ttu-id="35e4f-176">Haga clic en **Crear** para agregar la nueva cuenta de usuario al directorio.</span><span class="sxs-lookup"><span data-stu-id="35e4f-176">Click **Create** to add the new user account to your directory.</span></span>

   ![Crear una nueva cuenta de usuario][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="35e4f-178">Configuración y compilación de la aplicación de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="35e4f-178">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="35e4f-179">Extraiga los archivos del proyecto que creó y descargó en un directorio anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-179">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="35e4f-180">Vaya a la carpeta principal del proyecto y abra el archivo *pom.xml* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="35e4f-180">Navigate to the parent folder for your project, and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="35e4f-181">Agregue las dependencias para la seguridad OAuth2 de Spring; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-181">Add the dependencies for Spring OAuth2 security; for example:</span></span>

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

1. <span data-ttu-id="35e4f-182">Guarde y cierre el archivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="35e4f-182">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="35e4f-183">Vaya a la carpeta *src/main/resources* del proyecto y abra el archivo *application.properties* en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="35e4f-183">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="35e4f-184">Especifique la configuración del registro de su aplicación con los valores que creó anteriormente; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-184">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="35e4f-185">Donde:</span><span class="sxs-lookup"><span data-stu-id="35e4f-185">Where:</span></span>

   | <span data-ttu-id="35e4f-186">.</span><span class="sxs-lookup"><span data-stu-id="35e4f-186">Parameter</span></span> | <span data-ttu-id="35e4f-187">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="35e4f-187">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="35e4f-188">Contiene su **Id. de directorio** de Active Directory obtenido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="35e4f-188">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="35e4f-189">Contiene el **Id. de aplicación** del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="35e4f-189">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="35e4f-190">Contiene el **Valor** de la clave del registro de aplicaciones que completó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="35e4f-190">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="35e4f-191">Contiene una lista de los grupos de Active Directory que se usarán para la autorización.</span><span class="sxs-lookup"><span data-stu-id="35e4f-191">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-192">Para obtener una lista completa de los valores disponibles en su archivo *application.properties*, consulte el [ejemplo de Azure Active Directory Spring Boot][AAD Spring Boot Sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="35e4f-192">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="35e4f-193">Guarde y cierre el archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="35e4f-193">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="35e4f-194">Cree una carpeta llamada *controller* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="35e4f-194">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="35e4f-195">Cree un archivo de Java nuevo llamado *HelloController.java* en la carpeta *controller* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="35e4f-195">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="35e4f-196">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-196">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="35e4f-197">El nombre del grupo que especifique para el método `@PreAuthorize("hasRole('')")` debe contener uno de los grupos que especificó en el campo `azure.activedirectory.active-directory-groups` del archivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="35e4f-197">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-198">Puede especificar una configuración de autorización diferente para la asignación de solicitudes; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-198">You can specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="35e4f-199">Cree una carpeta llamada *security* en la carpeta src de Java para su aplicación; por ejemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="35e4f-199">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="35e4f-200">Cree un archivo Java nuevo llamado *WebSecurityConfig.java* en la carpeta *security* y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="35e4f-200">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="35e4f-201">Escriba el código siguiente, guarde el archivo y ciérrelo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-201">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="35e4f-202">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="35e4f-202">Build and test your app</span></span>

1. <span data-ttu-id="35e4f-203">Abra un símbolo del sistema y cambie el directorio a la carpeta donde se encuentra el archivo *pom.xml* de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="35e4f-203">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="35e4f-204">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35e4f-204">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Compilación de la aplicación][build-application]

1. <span data-ttu-id="35e4f-206">Después de que Maven compile e inicie la aplicación, abra <http://localhost:8080> en un explorador web; se le pedirá un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="35e4f-206">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Inicio de sesión en su aplicación][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-208">Se le pedirá que cambie su contraseña si es el primer inicio de sesión de una cuenta de usuario nueva.</span><span class="sxs-lookup"><span data-stu-id="35e4f-208">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Cambiar la contraseña][update-password]
   > 

1. <span data-ttu-id="35e4f-210">Cuando haya iniciado sesión correctamente, verá ver el texto de ejemplo "Hello World" desde el controlador.</span><span class="sxs-lookup"><span data-stu-id="35e4f-210">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Inicio de sesión correcto][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="35e4f-212">Las cuentas de usuario que no están autorizadas recibirán un mensaje **HTTP 403 No autorizado**.</span><span class="sxs-lookup"><span data-stu-id="35e4f-212">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="35e4f-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35e4f-213">Next steps</span></span>

<span data-ttu-id="35e4f-214">Para más información acerca de cómo usar Azure Active Directory, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="35e4f-214">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="35e4f-215">[Documentación de Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="35e4f-215">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="35e4f-216">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="35e4f-216">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="35e4f-217">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="35e4f-217">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="35e4f-218">Ejecución de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="35e4f-218">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="35e4f-219">Para más información sobre el uso de Azure con Java, consulte [Azure para desarrolladores de Java] y [Herramientas de Java para Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="35e4f-219">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="35e4f-220">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="35e4f-220">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="35e4f-221">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="35e4f-221">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="35e4f-222">Para ayudar a los desarrolladores a empezar con Spring Boot, puede encontrar varios paquetes de ejemplo de Spring Boot en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="35e4f-222">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="35e4f-223">Además de elegir de la lista de proyectos básicos de Spring Boot, el **[Spring Initializr]** ayuda a los desarrolladores en los primeros pasos para crear aplicaciones de Spring Boot personalizadas.</span><span class="sxs-lookup"><span data-stu-id="35e4f-223">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="35e4f-224">Para obtener un ejemplo más detallado, consulte el [ejemplo de Spring Boot para Azure Active Directory][AAD Spring Boot Sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="35e4f-224">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Documentación de Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desarrolladores de Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Ventajas para suscriptores de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
