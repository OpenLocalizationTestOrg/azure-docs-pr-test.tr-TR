---
title: "aaaBuild ve Azure App Service içinde Java API uygulaması dağıtma"
description: "Öğrenin nasıl toocreate Java API uygulama paketini ve tooAzure uygulama hizmeti dağıtın."
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
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="3e78d-103">Azure App Service içinde Java API uygulaması derleme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="3e78d-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="3e78d-104">Bu öğreticide gösterilmiştir nasıl toocreate bir Java uygulaması ve tooAzure App Service API kullanarak uygulamaları dağıtma [Git].</span><span class="sxs-lookup"><span data-stu-id="3e78d-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="3e78d-105">Bu öğreticide Hello yönergeler Java çalıştırabilen tüm işletim sisteminde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3e78d-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="3e78d-106">Bu öğreticideki Hello kod kullanılarak oluşturulur [Maven].</span><span class="sxs-lookup"><span data-stu-id="3e78d-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="3e78d-107">[Jax-RS] kullanılan toocreate hello RESTful hizmeti olduğu ve hello üzerinde temel alınarak oluşturulur [Swagger] hello kullanarak meta verileri belirtimi [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="3e78d-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e78d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3e78d-108">Prerequisites</span></span>
1. <span data-ttu-id="3e78d-109">[Java Geliştirme Seti 8] \(veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="3e78d-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="3e78d-110">Dağıtım makinenize yüklü [Maven]</span><span class="sxs-lookup"><span data-stu-id="3e78d-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="3e78d-111">Dağıtım makinenize yüklü [Git]</span><span class="sxs-lookup"><span data-stu-id="3e78d-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="3e78d-112">Ücretli veya [ücretsiz deneme sürümü] abonelik çok[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="3e78d-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="3e78d-113">[Postman] gibi bir HTTP test uygulaması</span><span class="sxs-lookup"><span data-stu-id="3e78d-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="3e78d-114">Swagger.IO kullanarak iskele hello API</span><span class="sxs-lookup"><span data-stu-id="3e78d-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="3e78d-115">Merhaba swagger.io çevrimiçi düzenleyicisini kullanarak API'NİZİN hello yapısını temsil eden Swagger JSON veya YAML koduna girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="3e78d-116">Merhaba API yüzey alanını tasarlanmış olduktan sonra platformlar ve altyapıları çeşitli kodunu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="3e78d-117">Merhaba sonraki bölümde iskele kurulmuş hello kodu değiştirilmiş tooinclude sahte işlevleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e78d-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="3e78d-118">Bu Tanıtım başlayacak hello swagger.io düzenleyicisine yapıştıracağınız bir Swagger JSON gövdesi ile hangi sonra kullanılan toogenerate kod JAX-RS tooaccess bir REST API uç noktası kullan yapacak.</span><span class="sxs-lookup"><span data-stu-id="3e78d-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="3e78d-119">Ardından, hello iskele kurulmuş kod tooreturn sahte verileri, bir veri kalıcılığı mekanizmasının üzerinde oluşturulan REST API düzenlersiniz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="3e78d-120">Swagger JSON kodunu tooyour Pano aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="3e78d-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="3e78d-121">Toohello gidin [Online Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="3e78d-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="3e78d-122">Bir kez hello tıklayın **Dosya -> JSON Yapıştır** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![JSON Yapıştır menü öğesi][paste-json]
3. <span data-ttu-id="3e78d-124">Merhaba kişi listesi API'si Swagger daha önce kopyaladığınız JSON yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![JSON kodunu Swagger’a yapıştırma][pasted-swagger]
4. <span data-ttu-id="3e78d-126">Merhaba belge sayfalarını ve hello düzenleyicide işlenen API özetini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="3e78d-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Swagger ile Oluşturulan Belgeleri Görüntüleme][view-swagger-generated-docs]
5. <span data-ttu-id="3e78d-128">Select hello **sunucu Oluştur -> JAX-RS** menü seçeneği tooscaffold hello sunucu tarafı kodu sonraki tooadd sahte uygulama Düzenle.</span><span class="sxs-lookup"><span data-stu-id="3e78d-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Kod Menü Öğesi Oluşturma][generate-code-menu-item]
   
    <span data-ttu-id="3e78d-130">Merhaba kod oluşturulduktan sonra bir ZIP dosyası toodownload sağlanması.</span><span class="sxs-lookup"><span data-stu-id="3e78d-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="3e78d-131">Bu dosya hello Swagger Kod Oluşturucu tarafından iskelesi oluşturulmuş hello kodunu içerir ve tüm ilişkili derleme betiklerini.</span><span class="sxs-lookup"><span data-stu-id="3e78d-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="3e78d-132">Merhaba tüm kitaplık tooa dizini, geliştirme iş istasyonunuzdaki sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="3e78d-133">Merhaba kod tooadd API uygulaması Düzenle</span><span class="sxs-lookup"><span data-stu-id="3e78d-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="3e78d-134">Bu bölümde, hello Swagger ile oluşturulan kodun sunucu-tarafı uygulamasını özel kodunuzla değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="3e78d-135">Merhaba yeni kod bir ArrayList kişi varlıkları toohello çağıran istemci döndürür.</span><span class="sxs-lookup"><span data-stu-id="3e78d-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="3e78d-136">Açık hello *Contact.java* hello bulunan model dosyası *gen/src/java/swagger/GÇ/model* klasörünü kullanarak [Visual Studio Code] veya sık kullandığınız metin düzenleyiciyi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Kişi Model Dosyasını açma][open-contact-model-file]
2. <span data-ttu-id="3e78d-138">Merhaba Oluşturucusu hello içinde aşağıdaki ekleme **kişi** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3e78d-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="3e78d-139">Açık hello *Contactsapiserviceımpl.Java* hello bulunan hizmet uygulama dosyasını *src/main/java/GÇ/swagger/api/impl* klasörünü kullanarak [Visual Studio Code]veya sık kullandığınız metin düzenleyiciyi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Kişi Hizmeti Kod Dosyasını açma][open-contact-service-code-file]
4. <span data-ttu-id="3e78d-141">Merhaba hello dosyasında bu yeni kodu tooadd sahte uygulama toohello servis kodu ile kodun üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="3e78d-142">Bir komut istemi açın ve dizin toohello kök klasörü, uygulamanızın değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3e78d-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="3e78d-143">Maven komutunu toobuild hello koddan hello yürütün ve yerel olarak Jetty uygulama sunucusu hello kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="3e78d-144">Merhaba komut penceresinde Jetty'nin bağlantı noktası 8080 üzerinde kodunuzu başlattığının gösterildiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e78d-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Kişi Hizmeti Kod Dosyasını açma][run-jetty-war]
8. <span data-ttu-id="3e78d-146">Kullanım [Postman] http://localhost: 8080/api/contacts sayfasında at toomake bir istek toohello "tüm kişileri Al" API yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Merhaba kişileri API çağrısı][calling-contacts-api]
9. <span data-ttu-id="3e78d-148">Kullanım [Postman] toomake bir istek toohello "belirli kişiyi Al" API yöntemine http://localhost: 8080/api/contacts/2 sayfasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="3e78d-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Merhaba kişileri API çağrısı][calling-specific-contact-api]
10. <span data-ttu-id="3e78d-150">Son olarak, aşağıdaki Maven komutunu konsolunuza hello yürüterek hello Java WAR (Web arşivi) dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e78d-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="3e78d-151">Merhaba WAR dosyası derlendikten sonra onu hello yerleştirilecek **hedef** klasör.</span><span class="sxs-lookup"><span data-stu-id="3e78d-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="3e78d-152">Merhaba gidin **hedef** klasörü ve yeniden adlandırma hello WAR dosyası çok**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="3e78d-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="3e78d-153">(Merhaba büyük/küçük harf bu biçimle eşleştiğinden emin olun).</span><span class="sxs-lookup"><span data-stu-id="3e78d-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="3e78d-154">Son olarak, komutlar hello kök klasöründen uygulama toocreate aşağıdaki hello yürütme bir **dağıtmak** klasörü toouse toodeploy hello WAR dosyası tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3e78d-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="3e78d-155">Yayımlama Hello çıktı tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="3e78d-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="3e78d-156">Bu bölümde nasıl hello kullanarak yeni bir API uygulaması Azure portalı, bu API uygulamasını Java uygulamalarını barındırmak için hazırlamak ve hello dağıtmak toocreate yeni WAR oluşturulan öğreneceksiniz tooAzure uygulama hizmeti toorun yeni API uygulamanızı dosya.</span><span class="sxs-lookup"><span data-stu-id="3e78d-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="3e78d-157">Hello yeni bir API uygulaması oluşturma [Azure portal], hello tıklayarak **yeni -> Web + mobil -> API uygulaması** menü öğesi, uygulama bilgilerinizi girin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3e78d-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Yeni bir API uygulaması oluşturma][create-api-app]
2. <span data-ttu-id="3e78d-159">API uygulamanız oluşturulduktan sonra uygulamanızın açmak **ayarları** dikey penceresinde ve hello ardından **uygulama ayarları** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="3e78d-160">Hello en son Tomcat'i seçin hello sonra hello kullanılabilir seçeneklerden en son Java sürümlerini seçin hello **Web kapsayıcısına** menüsüne ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3e78d-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Java API uygulaması dikey penceresinde hello ayarlayın][set-up-java]
3. <span data-ttu-id="3e78d-162">Merhaba tıklatın **dağıtım kimlik bilgileri** ayarlar menüsünü öğesi ve bir kullanıcı adı ve parola dosyaları tooyour API uygulaması yayımlama toouse istediğiniz sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Dağıtım kimlik bilgilerini ayarlama][deployment-credentials]
4. <span data-ttu-id="3e78d-164">Merhaba tıklatın **dağıtım kaynağı** ayarları menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="3e78d-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="3e78d-165">Bir kez hello tıklayın **Kaynak Seç** düğmesi, select hello **yerel Git deposu** seçeneğini ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3e78d-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="3e78d-166">Bunun yapılması Azure’da çalışan ve API uygulaması ile ilişkisi olan bir Git deposu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3e78d-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="3e78d-167">Her kod toohello yürüttükten *ana* şube Git deponuzun kodunuzu, Canlı çalışan API uygulaması Örneğinizde yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="3e78d-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Yeni bir yerel Git deposu ayarlama][select-git-repo]
5. <span data-ttu-id="3e78d-169">Merhaba yeni Git deposunun URL'sini tooyour panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3e78d-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="3e78d-170">Birazdan önemli olacağı için bunu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3e78d-170">Save this as it will be important in a moment.</span></span> 
   
    ![Uygulamanız için yeni bir Git deposu ayarlama][copy-git-repo-url]
6. <span data-ttu-id="3e78d-172">Git itme hello WAR dosyası toohello çevrimiçi deposu.</span><span class="sxs-lookup"><span data-stu-id="3e78d-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="3e78d-173">toodo bunu hello gidin **dağıtmak** klasör daha önce oluşturduğunuz böylece hello kodu App Service içinde çalışan toohello deposunu kolayca tamamlayabilir.</span><span class="sxs-lookup"><span data-stu-id="3e78d-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="3e78d-174">Sonra hello konsol penceresinde olacak ve Git komutları toolaunch hello işlemi aşağıdaki hello vermek ve dağıtımı devre dışı bırakmak hello webapps klasörünün bulunduğu hello klasöre gittiğinizde.</span><span class="sxs-lookup"><span data-stu-id="3e78d-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="3e78d-175">Merhaba sorun sonra **itme** isteği, istenir hello dağıtım kimlik bilgileri için daha önce oluşturduğunuz hello parolası.</span><span class="sxs-lookup"><span data-stu-id="3e78d-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="3e78d-176">Kimlik bilgilerinizi girdikten sonra güncelleştirme hello portal ekranınıza dağıtıldı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e78d-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="3e78d-177">Bir kez daha Postman toohit hello yeni API uygulaması Azure App Service içinde çalışan dağıtılmış kullanırsanız, hello davranışın tutarlı olduğunu ve artık bu kişi verilerini beklenen şekilde döndürdüğünü ve iskelesi kurulmuş Java kodundaki basit kod değişikliklerini toohello Swagger.io kullanarak görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Azure içinde Java Kişiler REST API'sini canlı kullanma][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="3e78d-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e78d-179">Next steps</span></span>
<span data-ttu-id="3e78d-180">Bu makalede, bir Swagger JSON dosyasını ve hello Swagger.io düzenleyicisinden elde edilen kurulmuş bazı Java kodla mümkün toostart yoktu.</span><span class="sxs-lookup"><span data-stu-id="3e78d-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="3e78d-181">Burada, basit değişiklikleriniz ve Git dağıtım işlemi Java’da yazılmış işlevsel bir API uygulaması elde etmeyle sonuçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3e78d-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="3e78d-182">Merhaba sonraki öğretici gösterir nasıl çok[CORS kullanarak JavaScript istemcilerinden API uygulamalarını kullanmak][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="3e78d-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="3e78d-183">Sonraki öğreticilerde hello serisi Göster nasıl tooimplement kimlik doğrulama ve yetkilendirme.</span><span class="sxs-lookup"><span data-stu-id="3e78d-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="3e78d-184">toobuild Bu örneği, öğrenin hello hakkında daha fazla [Java için depolama SDK'sı] toopersist hello JSON BLOB'ları.</span><span class="sxs-lookup"><span data-stu-id="3e78d-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="3e78d-185">Veya hello kullanabilir [belge DB Java SDK'sı] toosave kişi veri tooAzure belge DB.</span><span class="sxs-lookup"><span data-stu-id="3e78d-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="3e78d-186">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="3e78d-186">See Also</span></span>
<span data-ttu-id="3e78d-187">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Java geliştiricileri için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="3e78d-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure portal]: https://portal.azure.com/
[belge DB Java SDK'sı]: ../documentdb/documentdb-java-application.md
[ücretsiz deneme sürümü]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Geliştirme Seti 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Swagger Editor]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Java için depolama SDK'sı]:../storage/blobs/storage-java-how-to-use-blob-storage.md
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
