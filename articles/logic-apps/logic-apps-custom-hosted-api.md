---
title: "aaaDeploy, çağrı ve web API'leri ve REST API'leri Azure Logic Apps için kimlik doğrulaması | Microsoft Docs"
description: "Dağıtma, kimlik doğrulaması ve Azure Logic Apps ile sistem tümleştirmeleri için iş akışlarında web API'leri & REST API çağrısı"
keywords: "Web API'leri, REST API'leri, bağlayıcılar, iş akışları, sistem tümleştirmeler, kimlik doğrulaması"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Dağıtımı, arama ve özel API'leri olarak bağlayıcılar mantıksal uygulamalar için kimlik doğrulaması

Çalıştırdıktan sonra [özel API oluşturma](./logic-apps-create-api-app.md) uygulamalar iş mantığı eylemler veya tetikleyicileri toouse sağlamak için bunları çağırmadan önce Apı'lerinizi dağıtmanız gerekir. Hello iyi deneyim için herhangi bir API'yi mantığı uygulamadan çağırıp rağmen ekleyin [Swagger meta verileri](http://swagger.io/specification/) , API'nin işlemlerini ve parametrelerini açıklar. Bu Swagger dosyası API'nizi daha iyi ve daha kolay logic apps ile tümleştirmenize yardımcı olur.

API olarak dağıtabilir miyim [web uygulamaları](../app-service-web/app-service-web-overview.md), ancak API olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'ler hello bulutta ve şirket içi kullanabilir. Herhangi bir kod Apı'leriniz toochange yok--yalnızca kod tooan API uygulamanızı dağıtın. Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan hello en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS).

logic apps tooyour API'leri çağrılarından tooauthenticate, kodunuzu tooupdate aktarıp Azure portal hello Azure Active Directory'yi ayarlama ayarlayabilirsiniz. Veya gerektirir ve kimlik doğrulama, API'nin kodlarda zorlayın.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>API'nizi bir web uygulaması veya API uygulaması olarak dağıtma

Özel API'nizi mantığı uygulamadan aramadan önce API'nizi bir web uygulaması veya API uygulaması tooAzure uygulama hizmeti olarak dağıtın. Ayrıca, toomake Swagger belgenizi hello mantığı Uygulama Tasarımcısı tarafından okunabilir hello API tanımı özelliklerini ayarlama ve Aç [çıkış noktaları arası kaynak paylaşımı (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) web uygulaması veya API uygulaması için.

1. Hello Azure portal, web uygulaması veya API uygulaması seçin.

2. Açılır ve altında hello dikey penceresinde **API**, seçin **API tanımı**. Set hello **API tanımı konumu** swagger.json dosyanız için toohello URL.

   Genellikle, hello URL şöyle görünür:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Özel API'nizi için bağlantı tooSwagger dosyası](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Altında **API**, seçin **CORS**. Ayarlamak için hello CORS İlkesi **çıkış izin** çok**'*'** (tüm izin ver).

   Bu ayar mantığı Uygulama Tasarımcısı'ndan istekleri verir.

   ![Mantıksal Uygulama Tasarımcısı tooyour özel API'SİNDEN isteklere izin vermek](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Daha fazla bilgi için bu makalelere bakın:

* [ASP.NET web API için Swagger meta verileri ekleme](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [ASP.NET web API tooAzure uygulama hizmeti dağıtma](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Özel API'nizi mantığından uygulama iş akışları çağırın.

Merhaba API tanımı özellikleri ve CORS ayarladıktan sonra özel API'nin tetikleyiciler ve Eylemler, tooinclude iş akışınızda mantığı uygulama için kullanılabilir duruma gelir. 

*  Swagger URL'leri sahip tooview hello Web siteleri, abonelik sitelerinizi hello Logic Apps Tasarımcısı göz atabilirsiniz.

*  tooview kullanılabilir eylemler ve Swagger belgesinin üzerine gelerek girişleri kullanın hello [HTTP + Swagger eylem](../connectors/connectors-native-http-swagger.md).

*  toocall yok veya bir Swagger belgesinin kullanıma API'leri dahil olmak üzere herhangi bir API'yi hello ile her zaman bir istek oluşturabilirsiniz [HTTP eylemi](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Çağrıları tooyour özel API kimlik doğrulaması

Bu yolla tooyour özel API çağrıları güvenliğini sağlayabilirsiniz:

* [Kod değişiklikleri](#no-code): API'nizi ile koruma [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) hello Azure portal, bu nedenle yok tooupdate kodunuz varsa veya API'nizi yeniden dağıtın.

  > [!NOTE]
  > Varsayılan olarak, hassas yetkilendirme hello Azure portal kapatma hello Azure AD kimlik doğrulaması sağlamaz. Örneğin, bu kimlik doğrulama belirli Kiracı, tooa belirli kullanıcı veya uygulama, API toojust kilitler. 

* [API kodunu güncelleştirin](#update-code): zorlayarak API'nizi koruma [sertifika kimlik doğrulaması](#certificate), [temel kimlik doğrulaması](#basic), veya [Azure AD kimlik doğrulaması](#azure-ad-code) kodlarda.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Çağrıları tooyour API kodunu değiştirmeden kimlik doğrulaması

Bu yöntemin hello genel adımlar aşağıdadır:

1. İki oluşturmak [Azure Active Directory (Azure AD) uygulama kimlikleri](../app-service-api/app-service-api-dotnet-service-principal-auth.md): mantıksal uygulamanızı, diğeri web uygulaması (veya API uygulaması) için.

2. tooauthenticate çağrıları tooyour API'sini kullanın hello kimlik bilgileri (istemci kimliği ve parolası) Merhaba [hizmet asıl](../app-service-api/app-service-api-dotnet-service-principal-auth.md) mantıksal uygulamanız için Azure AD uygulama kimliği ile Merhaba ilişkili.

3. Merhaba uygulama kimlikleri mantığı uygulama tanımınızı içerir.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>1. Kısım: mantıksal uygulamanız için bir Azure AD uygulama kimliği oluşturma

Mantıksal uygulamanız bu Azure AD uygulama kimliği tooauthenticate Azure ad kullanır. Bu kimlik yukarı tooset dizininiz için bir kez yeterlidir. Örneğin, seçebileceğiniz toouse Merhaba, mantığı uygulamalarınız için aynı kimlik rağmen her mantıksal uygulama için benzersiz kimlik oluşturabilirsiniz. Hello Azure portal'ın bu kimlikleri ayarlayabilirsiniz [Klasik Azure portalı](#app-identity-logic-classic), veya [PowerShell](#powershell).

**Mantıksal uygulamanız için Hello uygulama kimliği hello Azure portal oluşturma**

1. Merhaba, [Azure portal](https://portal.azure.com "https://portal.azure.com"), seçin **Azure Active Directory**. 

2. Hello olduğunu onaylamak için web uygulaması veya API uygulaması ile aynı dizinde.

   > [!TIP]
   > tooswitch dizinler profilinizi tıklatın ve başka bir dizin seçin. Ya da seçin **genel bakış** > **anahtar dizini**.

3. Merhaba dizin menüsünde altında **Yönet**, seçin **uygulama kayıtlar** > **yeni uygulama kaydı**.

   > [!TIP]
   > Varsayılan olarak, dizininizde tüm uygulama kayıtları hello uygulama kayıtlar listesi gösterilir. yalnızca, uygulama kayıtlar, sonraki toohello arama kutusunda, tooview seçin **uygulamalarım**. 

   ![Yeni uygulama kaydı oluşturun](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Uygulama kimliğinizi bir ad verin, bırakın **uygulama türü** çok ayarlamak**Web uygulaması / API**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si**ve seçin **Oluşturma**.

   ![URL için uygulama kimliği oturum adı girin ve](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   mantıksal uygulamanız artık oluşturulan hello uygulama kimliği hello uygulama kayıtlar listesinde görüntülenir.

   ![Mantıksal uygulamanız için uygulama kimliği](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Merhaba uygulama kayıtlar listesinde, yeni uygulama kimliğini seçin. Kopyalayın ve hello kaydedin **uygulama kimliği** mantıksal uygulamanızı bölümü 3'te "istemci kimliği" Merhaba gibi toouse.

   ![Kopyalayın ve mantıksal uygulama için uygulama kimliği kaydedin](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Uygulama Kimliği ayarlarınızı görünür durumda değilse, seçin **ayarları** veya **tüm ayarları**.

7. Altında **API erişimini**, seçin **anahtarları**. Altında **açıklama**, anahtarınız için bir ad sağlayın. Altında **Expires**, anahtarınız için bir süre seçin.

   Oluşturmakta olduğunuz hello anahtar hello uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.

   ![Mantıksal uygulama kimliği için anahtar oluşturma](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Merhaba araç çubuğunda seçin **kaydetmek**. Altında **değeri**, anahtarınızı artık görünür. 
**Toocopy emin olun ve anahtarınızı kaydedin** daha sonra kullanmak üzere hello anahtarı gizli olduğu çıktığınızda hello anahtar dikey.

   Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, "gizli" ya da parola hello gibi bu anahtarı belirtin.

   ![Kopyalayın ve anahtarı için daha sonra kaydedin](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Merhaba Klasik Azure portalı mantıksal uygulamanızı için Hello uygulama kimliği oluşturma**

1. Buna Klasik Azure portalı Merhaba, seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Web uygulaması veya API uygulaması için kullandığınız aynı dizinde seçin hello.

3. Merhaba üzerinde **uygulamaları** sekmesinde, seçin **Ekle** hello sayfanın hello sonundaki.

4. Uygulama kimliğinizi bir ad verin ve seçin **sonraki** (sağ ok).

5. Altında **uygulama özellikleri**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si** ve **uygulama kimliği URI'si**ve seçin **tam** (onay işareti).

6. Merhaba üzerinde **yapılandırma** sekmesinde, kopyalamak ve hello kaydetme **istemci kimliği** bölümü 3'te, logic app toouse için.

7. Altında **anahtarları**açın hello **seçin süresi** listesi. Anahtarınız için bir süre seçin.

   Oluşturmakta olduğunuz hello anahtar hello uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.

8. Merhaba sayfasının Hello altında seçin **kaydetmek**. Birkaç saniye toowait olabilir.

9. Altında **anahtarları**toocopy emin olun ve artık görünür hello anahtarı kaydedin. 

   Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, "gizli" ya da parola hello gibi bu anahtarı belirtin.

Daha fazla bilgi için nasıl çok öğrenin [App Service uygulama toouse Azure Active Directory oturum açma yapılandırma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**PowerShell'de mantıksal uygulamanızı için Hello uygulama kimliği oluşturma**

Bu görevi PowerShell ile Azure Resource Manager aracılığıyla gerçekleştirebilirsiniz. PowerShell'de aşağıdaki komutları çalıştırın:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Toocopy hello emin olun **Kiracı kimliği** (GUID) Azure AD kiracınız için hello **uygulama kimliği**ve kullandığınız hello parola.

Daha fazla bilgi için nasıl çok öğrenin [PowerShell tooaccess kaynaklarla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Bölüm 2: web uygulaması veya API uygulaması için bir Azure AD uygulama kimliği oluşturma

Web uygulaması veya API uygulama zaten dağıtılmışsa, kimlik doğrulamasını etkinleştirmek ve hello Azure portal hello uygulama kimliği oluşturun. Aksi takdirde, şunları yapabilirsiniz [bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek](#authen-deploy). 

**Hello uygulama kimliği oluşturma ve kimlik doğrulaması hello dağıtılan uygulamalar için Azure Portalı'nda Aç**

1. Merhaba, [Azure portal](https://portal.azure.com "https://portal.azure.com"), bulma ve web uygulaması veya API uygulaması seçin. 

2. Altında **ayarları**, seçin **kimlik doğrulama/yetkilendirme**. Altında **App Service kimlik doğrulaması**, kimlik doğrulamasını **üzerinde**. Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.

   ![Kimlik doğrulamasını etkinleştirmek](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Artık web uygulaması veya API uygulaması için uygulama kimliği, aşağıda gösterildiği gibi oluşturun. Merhaba üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** çok**Express**. Seçin **yeni AD uygulaması oluştur**. Uygulama kimliğinizi bir ad verin ve seçin **Tamam**. 

   ![Web uygulaması veya API uygulaması için uygulama kimliği oluşturma](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Merhaba üzerinde **kimlik doğrulama / yetkilendirme dikey**, seçin **kaydetmek**.

Şimdi hello istemci Kimliğini bulun ve web uygulaması veya API uygulaması ile ilişkili hello uygulama kimliği için kimlik Kiracı. Bu kimlikleri bölümü 3'te kullanın. Bu nedenle hello Azure portal için aşağıdaki adımları devam veya [Klasik Azure portalı](#find-id-classic).

**Uygulama Kimliği'nin istemci Kimliğini bulmak ve web uygulaması veya hello Azure portalında bir API uygulaması için kimliği Kiracı**

1. Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**. 

   !["Azure Active Directory" seçin](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Merhaba üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** çok**Gelişmiş**.

3. Kopya hello **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.

   > [!TIP] 
   > Varsa **istemci kimliği** ve **veren URL'si** yoksa görünür hello Azure portal'ı yenilemeyi deneyin ve 1. adım yineleyin.

4. Altında **veren URL'si**, kopyalama ve kaydetme yalnızca GUID için bölümü 3 hello. Aynı zamanda bu GUID web uygulamanızı veya API uygulamasının dağıtım şablonu, gerekirse kullanabilirsiniz.

   Bu GUID belirli kiracının GUID ("Kiracı kimliği") ve bu URL'de görünmelidir:`https://sts.windows.net/{GUID}`

5. Değişikliklerinizi kaydetmeden kapatın hello **Azure Active Directory ayarları** dikey.

<a name="find-id-classic"></a>

**Uygulama Kimliği'nin istemci Kimliğini bulmak ve web uygulaması veya hello Klasik Azure portalında bir API uygulaması için kimliği Kiracı**

1. Buna Klasik Azure portalı Merhaba, seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Web uygulaması veya API uygulaması için kullandığınız hello dizini seçin.

3. Merhaba, **arama** kutusunda bulmak ve web uygulaması veya API uygulaması için hello uygulama kimliği seçin.

4. Merhaba üzerinde **yapılandırma** sekmesi, kopyalama hello **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.

5. Merhaba hello sonundaki hello istemci kimliği aldıktan sonra **yapılandırma** sekmesinde, seçin **uç noktaları görüntülemek**.

6. Merhaba URL'sini kopyalayın **Federasyon meta veri belgesi**ve toothat URL'ye gidin.

7. Açılan hello meta veri belgesinde hello kök Bul **EntityDescriptor kimliği** sahip öğesi bir **Entityıd** özniteliği bu formda:`https://sts.windows.net/{GUID}` 

      Bu öznitelik Hello GUID belirli kiracının (Kiracı kimliği) olarak GUID'dir.

8. Merhaba Kiracı kimliği kopyalayın ve gerekirse bölümü 3 ve ayrıca toouse web uygulamanızı veya API uygulamasının dağıtım şablonu kullanmak için bu kimliği kaydedin.

Daha fazla bilgi için şu konulara bakın:

* [Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek**

Hala mantığı uygulamanız için hello uygulama kimlikten web uygulaması veya farklı bir API uygulaması için bir Azure AD uygulama kimliği da oluşturmanız gerekir. toocreate hello uygulama kimliği, önceki izleyin hello Kısım 2'de Azure portal hello için adımları. Ayrıca, 1. Bölüm hello adımları ancak web uygulamanızı veya API uygulamasının gerçek emin toouse olun `https://{URL}` için **oturum açma URL'si** ve **uygulama kimliği URI'si**. Bu adımları, hem de hello istemci kimliği ve Kiracı kimliği, uygulamanızın dağıtım şablonu kullanmak için ve ayrıca bölümü 3 toosave sahip.

> [!NOTE]
> Web uygulaması veya API uygulaması için hello Azure AD uygulama kimliği oluşturduğunuzda, PowerShell yazmak yerine hello Azure portalında veya Klasik Azure portalını kullanmanız gerekir. Merhaba PowerShell komutunu gerekli hello izinlerini toosign kullanıcılar bir Web sitesi olarak ayarlamaz.

Merhaba istemci kimliği ve Kiracı kimliği aldıktan sonra bu kimlikleri subresource web uygulaması veya API uygulaması için dağıtım şablonunda olarak şunları içerir:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically dağıtmak boş web uygulaması ve bir mantıksal uygulama Azure Active Directory kimlik doğrulaması, birlikte [hello tam şablonu görüntüleme burada](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), veya **tooAzure dağıtmak** burada:

[![TooAzure dağıtma](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>3. Kısım: hello yetkilendirme mantıksal uygulamanızı bölümünde doldurma

Merhaba önceki şablonu zaten bu yetkilendirmesi bölümünde ayarladığınız sahip, ancak doğrudan hello mantıksal uygulama yazıyorsanız, hello tam yetkilendirme bölümü içermelidir.

Kod görünümünde gidin toohello mantıksal uygulama tanımını açın **HTTP** eylem bölümü, Bul hello **yetkilendirme** bölümünde ve bu satırı ekleyin:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Öğesi | Açıklama |
| ------- | ----------- |
| Kiracı |Merhaba GUID hello Azure AD kiracısı |
| Hedef kitle |Gereklidir. Merhaba GUID tooaccess - hello istemci web uygulaması veya API uygulaması için uygulama kimliği hello Kimliğinden istediğiniz hello hedef kaynak için |
| istemci kimliği |access - mantıksal uygulamanızı için hello uygulama kimliği hello istemci kimliği isteyen hello istemci Merhaba GUID |
| Gizli |Gereklidir. Merhaba anahtarı veya parolayı hello uygulama kimliği hello erişim belirteci isteyen hello istemci için gelen |
| type |Merhaba kimlik doğrulama türü. ActiveDirectoryOAuth kimlik doğrulaması için hello değerdir `ActiveDirectoryOAuth`. |

Örneğin:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Kod aracılığıyla güvenli API çağrıları

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Sertifika kimlik doğrulaması

mantıksal uygulama tooyour web uygulaması veya API uygulaması toovalidate hello gelen istekleri, istemci sertifikaları kullanabilirsiniz. kodunuzu, tooset öğrenin [nasıl tooconfigure TLS karşılıklı kimlik doğrulaması](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

Merhaba, **yetkilendirme** bölümünde, bu satırı ekleyin: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Öğesi | Açıklama |
| ------- | ----------- |
| type |Gereklidir. Merhaba kimlik doğrulama türü. SSL istemci sertifikaları için başlangıç değeri olmalıdır `ClientCertificate`. |
| password |Gereklidir. Merhaba istemci sertifikası (PFX dosyası) erişim için başlangıç parolası |
| PFX |Gereklidir. Base64 ile kodlanmış içeriği hello istemci sertifikasının (PFX dosyası) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Temel kimlik doğrulaması

toovalidate gelen istekleri mantığı uygulama tooyour web uygulaması veya API uygulaması temel kimlik doğrulaması, bir kullanıcı adı ve parola gibi kullanabilirsiniz. Temel kimlik doğrulaması genel bir desen olduğundan ve web uygulaması veya API uygulaması herhangi kullanılan dili toobuild bu kimlik doğrulaması kullanabilirsiniz.

Merhaba, **yetkilendirme** bölümünde, bu satırı ekleyin:

`{"type": "basic", "username": "username", "password": "password"}`.

| Öğesi | Açıklama |
| --- | --- |
| type |Gereklidir. Merhaba kimlik doğrulama türü. Temel kimlik doğrulaması için hello değeri olmalıdır `Basic`. |
| kullanıcı adı |Gereklidir. kimlik doğrulaması için Hello kullanıcı adı |
| password |Gereklidir. Merhaba parola kimlik doğrulaması |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Kod aracılığıyla Azure Active Directory kimlik doğrulaması

Varsayılan olarak, hassas yetkilendirme hello Azure portal kapatma hello Azure AD kimlik doğrulaması sağlamaz. Örneğin, bu kimlik doğrulama belirli Kiracı, tooa belirli kullanıcı veya uygulama, API toojust kilitler. 

toorestrict API erişim tooyour mantıksal uygulama kod, aracılığıyla hello JSON web token (JWT) sahip hello üstbilgi ayıklayın. Merhaba çağıranının kimliğini denetleyin ve eşleşmeyen istekleri reddedecek.

Tooimplement devam bu kimlik doğrulaması tamamen kendi kodu ve olmayan kullanım hello Azure portal, bilgi nasıl çok [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](../app-service-web/web-sites-authentication-authorization.md).

toocreate mantıksal uygulamanız için bir uygulama kimliği ve bu kimlik toocall API'nizi kullanın, hello önceki adımları izlemeniz gerekir.

## <a name="next-steps"></a>Sonraki adımlar

* [Tanılama günlükleri ve Uyarıları ile mantığı uygulama performansını kontrol etme](logic-apps-monitor-your-logic-apps.md)