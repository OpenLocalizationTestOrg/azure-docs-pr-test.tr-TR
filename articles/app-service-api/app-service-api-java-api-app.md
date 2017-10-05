---
title: "Azure App Service içinde Java API uygulaması derleme ve dağıtma"
description: "Java API uygulama paketini oluşturma ve Azure App Service’e dağıtma hakkında bilgi edinin."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="acada-103">Azure App Service içinde Java API uygulaması derleme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="acada-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="acada-104">Bu öğretici bir Java uygulamasının nasıl oluşturulacağını ve [Git] kullanılarak Azure App Service API Apps’e nasıl dağıtılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="acada-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="acada-105">Bu öğreticideki yönergeler Java çalıştırabilen tüm işletim sistemlerinde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="acada-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="acada-106">Bu öğreticideki kod [Maven] kullanılarak derlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="acada-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="acada-107">[Jax-RS], RESTful Hizmetini oluşturmak için kullanılır ve [Swagger] meta veri belirtimine göre [Swagger Editor] kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="acada-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acada-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="acada-108">Prerequisites</span></span>
1. <span data-ttu-id="acada-109">[Java Geliştirme Seti 8] \(veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="acada-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="acada-110">Dağıtım makinenize yüklü [Maven]</span><span class="sxs-lookup"><span data-stu-id="acada-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="acada-111">Dağıtım makinenize yüklü [Git]</span><span class="sxs-lookup"><span data-stu-id="acada-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="acada-112">[Microsoft Azure] için ücretli veya [ücretsiz deneme] aboneliği</span><span class="sxs-lookup"><span data-stu-id="acada-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="acada-113">[Postman] gibi bir HTTP test uygulaması</span><span class="sxs-lookup"><span data-stu-id="acada-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="acada-114">Swagger.IO kullanarak API iskelesi kurma</span><span class="sxs-lookup"><span data-stu-id="acada-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="acada-115">Swagger.io çevrimiçi düzenleyicisini kullanarak API’nizin yapısını temsil eden Swagger JSON veya YAML koduna giriş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="acada-116">API yüzey alanı tasarlandıktan sonra kodu çeşitli platformlar ve çerçeveler için dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="acada-117">Sonraki bölümde iskele kurulmuş kod, sahte işlevleri içerecek şekilde değiştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="acada-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="acada-118">Bu gösterim swagger.io düzenleyicisine yapıştıracağınız ve ardından bir REST API’si uç noktasına erişmek üzere JAX-RS kullanan kodu oluşturmak için kullanılacak bir Swagger JSON gövdesi ile başlar.</span><span class="sxs-lookup"><span data-stu-id="acada-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="acada-119">Ardından, bir veri kalıcılığı mekanizmasının üzerinde oluşturulan REST API’sine benzeyen sahte veriler döndürmek için iskele kurulmuş kodu düzenlersiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="acada-120">Aşağıdaki Swagger JSON kodunu panonuza kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="acada-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="acada-121">[Online Swagger Editor] uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="acada-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="acada-122">Uygulamaya ulaştıktan sonra **Dosya -> JSON Yapıştır** menü öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![JSON Yapıştır menü öğesi][paste-json]
3. <span data-ttu-id="acada-124">Daha önce kopyaladığınız Kişi Listesi API’si Swagger JSON öğesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="acada-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![JSON kodunu Swagger’a yapıştırma][pasted-swagger]
4. <span data-ttu-id="acada-126">Belge sayfalarını ve düzenleyicide işlenen API özetini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="acada-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Swagger ile Oluşturulan Belgeleri Görüntüleme][view-swagger-generated-docs]
5. <span data-ttu-id="acada-128">Sahte uygulama eklemek üzere daha sonra düzenleyeceğiniz sunucu tarafı kodunun iskelesini oluşturmak için **Sunucu Oluştur -> JAX-RS** menü seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="acada-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Kod Menü Öğesi Oluşturma][generate-code-menu-item]
   
    <span data-ttu-id="acada-130">Kod oluşturulduktan sonra indirmeniz için ZIP dosyası sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acada-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="acada-131">Bu dosya Swagger kod oluşturucu tarafından iskelesi oluşturulmuş kodu ve tüm ilişkili derleme betiklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="acada-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="acada-132">Tüm kitaplığı, geliştirme iş istasyonunuzdaki bir dizine ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="acada-133">API uygulaması eklemek için kodu düzenleme</span><span class="sxs-lookup"><span data-stu-id="acada-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="acada-134">Bu bölümde Swagger ile oluşturulan kodun sunucu-tarafı uygulamasını özel kodunuzla değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="acada-135">Yeni kod, çağıran istemciye Kişi varlıkları için bir ArrayList döndürür.</span><span class="sxs-lookup"><span data-stu-id="acada-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="acada-136">*src/gen/java/io/swagger/model* klasöründe bulunan *Contact.java* model dosyasını [Visual Studio Code] veya sık kullandığınız metin düzenleyiciyi kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="acada-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Kişi Model Dosyasını açma][open-contact-model-file]
2. <span data-ttu-id="acada-138">**Contact** sınıfına aşağıdaki oluşturucuyu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="acada-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="acada-139">*src/main/java/io/swagger/api/impl* klasöründe bulunan *ContactsApiServiceImpl.java* hizmet uygulama dosyasını [Visual Studio Code] veya sık kullandığınız metin düzenleyiciyi kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="acada-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Kişi Hizmeti Kod Dosyasını açma][open-contact-service-code-file]
4. <span data-ttu-id="acada-141">Hizmet koduna sahte bir uygulama eklemek için dosyanın içindeki kodun üzerine bu yeni kodu yazın.</span><span class="sxs-lookup"><span data-stu-id="acada-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="acada-142">Bir komut istemi açın ve dizini uygulamanızın kök klasörüyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="acada-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="acada-143">Kodu derlemek için aşağıdaki Maven komutunu yürütün ve yerel olarak Jetty uygulama sunucusu ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="acada-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="acada-144">Komut penceresinde Jetty’nin bağlantı noktası 8080 üzerinde kodunuzu başlattığının gösterildiğini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Kişi Hizmeti Kod Dosyasını açma][run-jetty-war]
8. <span data-ttu-id="acada-146">[Postman] kullanarak http://localhost:8080/api/contacts sayfasında "tüm kişileri al" API yöntemine bir istek gönderin.</span><span class="sxs-lookup"><span data-stu-id="acada-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Kişiler API’sini çağırma][calling-contacts-api]
9. <span data-ttu-id="acada-148">[Postman] kullanarak http://localhost:8080/api/contacts/2 sayfasında bulunan "belirli kişiyi al" API yöntemine istek gönderin.</span><span class="sxs-lookup"><span data-stu-id="acada-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Kişiler API’sini çağırma][calling-specific-contact-api]
10. <span data-ttu-id="acada-150">Son olarak, konsolunuzda aşağıdaki Maven komutunu yürüterek Java WAR (Web Arşivi) dosyasını derleyin.</span><span class="sxs-lookup"><span data-stu-id="acada-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="acada-151">WAR dosyası derlendikten sonra **hedef** klasörüne yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="acada-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="acada-152">**Hedef** klasörüne gidin ve WAR dosyasını **ROOT.war** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="acada-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="acada-153">(Büyük harflerin bu biçimle eşleştiğinden emin olun).</span><span class="sxs-lookup"><span data-stu-id="acada-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="acada-154">Son olarak, WAR dosyasını Azure’a dağıtmak için kullanılacak bir **dağıt** klasörü oluşturmak üzere uygulamanızın kök klasöründen aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="acada-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="acada-155">Çıktıyı Azure App Service’de yayımlama</span><span class="sxs-lookup"><span data-stu-id="acada-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="acada-156">Bu bölümde Azure Portal’ı kullanarak yeni bir API oluşturma, bu API uygulamasını Java uygulamalarını barındıracak şekilde hazırlama ve yeni oluşturulan WAR dosyasını yeni API uygulamasını çalıştırmak üzere Azure App Service’e dağıtma hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="acada-157">[Azure portal] yeni bir API uygulaması oluşturmak için **Yeni -> Web + Mobil -> API uygulaması** menü öğesine tıklayın, uygulama bilgilerinizi girin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Yeni bir API uygulaması oluşturma][create-api-app]
2. <span data-ttu-id="acada-159">API uygulamanız oluşturulduktan sonra uygulamanızın **Ayarlar** dikey penceresini açın ve ardından **Uygulama ayarları** menü öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="acada-160">Kullanılabilir seçenekler arasından en son Java sürümlerini seçin, ardından **Web kapsayıcısı** menüsünden en son Tomcat’i seçin ve ardından **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![API uygulaması dikey penceresinde Java ayarı][set-up-java]
3. <span data-ttu-id="acada-162">**Dağıtım kimlik bilgileri** ayarlar menü öğesine tıklayın ve dosyaları API uygulamanızda yayımlarken kullanmak istediğiniz kullanıcı adını ve parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="acada-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Dağıtım kimlik bilgilerini ayarlama][deployment-credentials]
4. <span data-ttu-id="acada-164">**Dağıtım kaynağı** ayarlar menü öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="acada-165">Menüye girdikten sonra **Kaynak seç** düğmesine tıklayın, **Yerel Git Deposu** seçeneğini belirleyin ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acada-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="acada-166">Bunun yapılması Azure’da çalışan ve API uygulaması ile ilişkisi olan bir Git deposu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="acada-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="acada-167">Git deponuzun *ana* dalında her komut yürüttüğünüzde kodunuz çalışan canlı API uygulaması örneğinizde yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="acada-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Yeni bir yerel Git deposu ayarlama][select-git-repo]
5. <span data-ttu-id="acada-169">Yeni Git deposunun URL’sini panonuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="acada-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="acada-170">Birazdan önemli olacağı için bunu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="acada-170">Save this as it will be important in a moment.</span></span> 
   
    ![Uygulamanız için yeni bir Git deposu ayarlama][copy-git-repo-url]
6. <span data-ttu-id="acada-172">WAR dosyasını çevrimiçi depoya Git ile iletin.</span><span class="sxs-lookup"><span data-stu-id="acada-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="acada-173">Bunu yapmak için daha önce oluşturduğunuz **dağıt** klasörüne gidin, böylece kodu App Service içinde çalışan depoya kolayca uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="acada-174">Konsol penceresine gelip web uygulamaları klasörünün bulunduğu klasöre gittiğinizde işlemi başlatmak ve dağıtımı devre dışı bırakmak için aşağıdaki Git komutlarını verin.</span><span class="sxs-lookup"><span data-stu-id="acada-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="acada-175">**Push** isteğini verdikten sonra daha önce dağıtım kimlik bilgisi için oluşturduğunuz parola istenir.</span><span class="sxs-lookup"><span data-stu-id="acada-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="acada-176">Kimlik bilgilerinizi girdikten sonra güncelleştirmenin dağıtıldığı portal ekranını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="acada-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="acada-177">Azure App Service’de çalışan yeni dağıtılmış API uygulamasını bulmak için bir kez daha Postman kullanırsanız davranışın tutarlı olduğunu ve bu kez kişi verilerini beklenen şekilde döndürdüğünü ve iskelesi kurulmuş Swagger.io Java kodundaki basit kod değişikliklerini kullandığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="acada-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Azure içinde Java Kişiler REST API'sini canlı kullanma][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="acada-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acada-179">Next steps</span></span>
<span data-ttu-id="acada-180">Bu makalede, bir Swagger JSON dosyasını ve Swagger.io düzenleyicisinden elde edilen iskelesi kurulmuş bazı Java kodlarını kullanmaya başladınız.</span><span class="sxs-lookup"><span data-stu-id="acada-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="acada-181">Burada, basit değişiklikleriniz ve Git dağıtım işlemi Java’da yazılmış işlevsel bir API uygulaması elde etmeyle sonuçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="acada-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="acada-182">Sonraki öğreticide [CORS kullanarak JavaScript istemcilerinden API uygulamalarını kullanma][App Service API CORS] işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="acada-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="acada-183">Serinin sonraki öğreticileri, kimlik doğrulama ve yetkilendirmenin nasıl uygulandığını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="acada-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="acada-184">Bu örneği geliştirmek için JSON blob’larını devam ettirmek üzere [Java için Depolama SDK’sı] hakkında daha fazla bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="acada-185">Veya kişi verilerinizi Azure Belge DB’sine kaydetmek için [Belge DB Java SDK’sı] kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acada-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="acada-186">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="acada-186">See Also</span></span>
<span data-ttu-id="acada-187">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Java geliştiricileri için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="acada-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure portal]: https://portal.azure.com/
[Belge DB Java SDK’sı]: ../documentdb/documentdb-java-application.md
[ücretsiz deneme]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Geliştirme Seti 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Swagger Editor]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Java için Depolama SDK’sı]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
