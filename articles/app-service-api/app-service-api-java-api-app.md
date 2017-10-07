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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Azure App Service içinde Java API uygulaması derleme ve dağıtma
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Bu öğreticide gösterilmiştir nasıl toocreate bir Java uygulaması ve tooAzure App Service API kullanarak uygulamaları dağıtma [Git]. Bu öğreticide Hello yönergeler Java çalıştırabilen tüm işletim sisteminde izlenebilir. Bu öğreticideki Hello kod kullanılarak oluşturulur [Maven]. [Jax-RS] kullanılan toocreate hello RESTful hizmeti olduğu ve hello üzerinde temel alınarak oluşturulur [Swagger] hello kullanarak meta verileri belirtimi [Swagger Editor].

## <a name="prerequisites"></a>Ön koşullar
1. [Java Geliştirme Seti 8] \(veya üzeri)
2. Dağıtım makinenize yüklü [Maven]
3. Dağıtım makinenize yüklü [Git]
4. Ücretli veya [ücretsiz deneme sürümü] abonelik çok[Microsoft Azure]
5. [Postman] gibi bir HTTP test uygulaması

## <a name="scaffold-hello-api-using-swaggerio"></a>Swagger.IO kullanarak iskele hello API
Merhaba swagger.io çevrimiçi düzenleyicisini kullanarak API'NİZİN hello yapısını temsil eden Swagger JSON veya YAML koduna girebilirsiniz. Merhaba API yüzey alanını tasarlanmış olduktan sonra platformlar ve altyapıları çeşitli kodunu dışarı aktarabilirsiniz. Merhaba sonraki bölümde iskele kurulmuş hello kodu değiştirilmiş tooinclude sahte işlevleri olacaktır. 

Bu Tanıtım başlayacak hello swagger.io düzenleyicisine yapıştıracağınız bir Swagger JSON gövdesi ile hangi sonra kullanılan toogenerate kod JAX-RS tooaccess bir REST API uç noktası kullan yapacak. Ardından, hello iskele kurulmuş kod tooreturn sahte verileri, bir veri kalıcılığı mekanizmasının üzerinde oluşturulan REST API düzenlersiniz.  

1. Swagger JSON kodunu tooyour Pano aşağıdaki hello kopyalayın:
   
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
2. Toohello gidin [Online Swagger Editor]. Bir kez hello tıklayın **Dosya -> JSON Yapıştır** menü öğesi.
   
    ![JSON Yapıştır menü öğesi][paste-json]
3. Merhaba kişi listesi API'si Swagger daha önce kopyaladığınız JSON yapıştırın. 
   
    ![JSON kodunu Swagger’a yapıştırma][pasted-swagger]
4. Merhaba belge sayfalarını ve hello düzenleyicide işlenen API özetini görüntüleyin. 
   
    ![Swagger ile Oluşturulan Belgeleri Görüntüleme][view-swagger-generated-docs]
5. Select hello **sunucu Oluştur -> JAX-RS** menü seçeneği tooscaffold hello sunucu tarafı kodu sonraki tooadd sahte uygulama Düzenle. 
   
    ![Kod Menü Öğesi Oluşturma][generate-code-menu-item]
   
    Merhaba kod oluşturulduktan sonra bir ZIP dosyası toodownload sağlanması. Bu dosya hello Swagger Kod Oluşturucu tarafından iskelesi oluşturulmuş hello kodunu içerir ve tüm ilişkili derleme betiklerini. Merhaba tüm kitaplık tooa dizini, geliştirme iş istasyonunuzdaki sıkıştırmasını açın. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Merhaba kod tooadd API uygulaması Düzenle
Bu bölümde, hello Swagger ile oluşturulan kodun sunucu-tarafı uygulamasını özel kodunuzla değiştirirsiniz. Merhaba yeni kod bir ArrayList kişi varlıkları toohello çağıran istemci döndürür. 

1. Açık hello *Contact.java* hello bulunan model dosyası *gen/src/java/swagger/GÇ/model* klasörünü kullanarak [Visual Studio Code] veya sık kullandığınız metin düzenleyiciyi. 
   
    ![Kişi Model Dosyasını açma][open-contact-model-file]
2. Merhaba Oluşturucusu hello içinde aşağıdaki ekleme **kişi** sınıfı. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Açık hello *Contactsapiserviceımpl.Java* hello bulunan hizmet uygulama dosyasını *src/main/java/GÇ/swagger/api/impl* klasörünü kullanarak [Visual Studio Code]veya sık kullandığınız metin düzenleyiciyi.
   
    ![Kişi Hizmeti Kod Dosyasını açma][open-contact-service-code-file]
4. Merhaba hello dosyasında bu yeni kodu tooadd sahte uygulama toohello servis kodu ile kodun üzerine yazın. 
   
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
5. Bir komut istemi açın ve dizin toohello kök klasörü, uygulamanızın değiştirin.
6. Maven komutunu toobuild hello koddan hello yürütün ve yerel olarak Jetty uygulama sunucusu hello kullanarak çalıştırın. 
   
        mvn package jetty:run
7. Merhaba komut penceresinde Jetty'nin bağlantı noktası 8080 üzerinde kodunuzu başlattığının gösterildiğini görmeniz gerekir. 
   
    ![Kişi Hizmeti Kod Dosyasını açma][run-jetty-war]
8. Kullanım [Postman] http://localhost: 8080/api/contacts sayfasında at toomake bir istek toohello "tüm kişileri Al" API yöntemi.
   
    ![Merhaba kişileri API çağrısı][calling-contacts-api]
9. Kullanım [Postman] toomake bir istek toohello "belirli kişiyi Al" API yöntemine http://localhost: 8080/api/contacts/2 sayfasında bulunur.
   
    ![Merhaba kişileri API çağrısı][calling-specific-contact-api]
10. Son olarak, aşağıdaki Maven komutunu konsolunuza hello yürüterek hello Java WAR (Web arşivi) dosyasını oluşturun. 
    
         mvn package war:war
11. Merhaba WAR dosyası derlendikten sonra onu hello yerleştirilecek **hedef** klasör. Merhaba gidin **hedef** klasörü ve yeniden adlandırma hello WAR dosyası çok**ROOT.war**. (Merhaba büyük/küçük harf bu biçimle eşleştiğinden emin olun).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Son olarak, komutlar hello kök klasöründen uygulama toocreate aşağıdaki hello yürütme bir **dağıtmak** klasörü toouse toodeploy hello WAR dosyası tooAzure. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Yayımlama Hello çıktı tooAzure uygulama hizmeti
Bu bölümde nasıl hello kullanarak yeni bir API uygulaması Azure portalı, bu API uygulamasını Java uygulamalarını barındırmak için hazırlamak ve hello dağıtmak toocreate yeni WAR oluşturulan öğreneceksiniz tooAzure uygulama hizmeti toorun yeni API uygulamanızı dosya. 

1. Hello yeni bir API uygulaması oluşturma [Azure portal], hello tıklayarak **yeni -> Web + mobil -> API uygulaması** menü öğesi, uygulama bilgilerinizi girin ve ardından **oluşturma**.
   
    ![Yeni bir API uygulaması oluşturma][create-api-app]
2. API uygulamanız oluşturulduktan sonra uygulamanızın açmak **ayarları** dikey penceresinde ve hello ardından **uygulama ayarları** menü öğesi. Hello en son Tomcat'i seçin hello sonra hello kullanılabilir seçeneklerden en son Java sürümlerini seçin hello **Web kapsayıcısına** menüsüne ve ardından **kaydetmek**.
   
    ![Java API uygulaması dikey penceresinde hello ayarlayın][set-up-java]
3. Merhaba tıklatın **dağıtım kimlik bilgileri** ayarlar menüsünü öğesi ve bir kullanıcı adı ve parola dosyaları tooyour API uygulaması yayımlama toouse istediğiniz sağlayın. 
   
    ![Dağıtım kimlik bilgilerini ayarlama][deployment-credentials]
4. Merhaba tıklatın **dağıtım kaynağı** ayarları menü öğesi. Bir kez hello tıklayın **Kaynak Seç** düğmesi, select hello **yerel Git deposu** seçeneğini ve ardından **Tamam**. Bunun yapılması Azure’da çalışan ve API uygulaması ile ilişkisi olan bir Git deposu oluşturur. Her kod toohello yürüttükten *ana* şube Git deponuzun kodunuzu, Canlı çalışan API uygulaması Örneğinizde yayımlanır. 
   
    ![Yeni bir yerel Git deposu ayarlama][select-git-repo]
5. Merhaba yeni Git deposunun URL'sini tooyour panoya kopyalayın. Birazdan önemli olacağı için bunu kaydedin. 
   
    ![Uygulamanız için yeni bir Git deposu ayarlama][copy-git-repo-url]
6. Git itme hello WAR dosyası toohello çevrimiçi deposu. toodo bunu hello gidin **dağıtmak** klasör daha önce oluşturduğunuz böylece hello kodu App Service içinde çalışan toohello deposunu kolayca tamamlayabilir. Sonra hello konsol penceresinde olacak ve Git komutları toolaunch hello işlemi aşağıdaki hello vermek ve dağıtımı devre dışı bırakmak hello webapps klasörünün bulunduğu hello klasöre gittiğinizde. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Merhaba sorun sonra **itme** isteği, istenir hello dağıtım kimlik bilgileri için daha önce oluşturduğunuz hello parolası. Kimlik bilgilerinizi girdikten sonra güncelleştirme hello portal ekranınıza dağıtıldı görmeniz gerekir.
7. Bir kez daha Postman toohit hello yeni API uygulaması Azure App Service içinde çalışan dağıtılmış kullanırsanız, hello davranışın tutarlı olduğunu ve artık bu kişi verilerini beklenen şekilde döndürdüğünü ve iskelesi kurulmuş Java kodundaki basit kod değişikliklerini toohello Swagger.io kullanarak görürsünüz. 
   
    ![Azure içinde Java Kişiler REST API'sini canlı kullanma][postman-calling-azure-contacts]

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bir Swagger JSON dosyasını ve hello Swagger.io düzenleyicisinden elde edilen kurulmuş bazı Java kodla mümkün toostart yoktu. Burada, basit değişiklikleriniz ve Git dağıtım işlemi Java’da yazılmış işlevsel bir API uygulaması elde etmeyle sonuçlanmıştır. Merhaba sonraki öğretici gösterir nasıl çok[CORS kullanarak JavaScript istemcilerinden API uygulamalarını kullanmak][App Service API CORS]. Sonraki öğreticilerde hello serisi Göster nasıl tooimplement kimlik doğrulama ve yetkilendirme.

toobuild Bu örneği, öğrenin hello hakkında daha fazla [Java için depolama SDK'sı] toopersist hello JSON BLOB'ları. Veya hello kullanabilir [belge DB Java SDK'sı] toosave kişi veri tooAzure belge DB. 

<a name="see-also"></a>

## <a name="see-also"></a>Ayrıca Bkz.
Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Java geliştiricileri için Azure](/java/azure).

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
