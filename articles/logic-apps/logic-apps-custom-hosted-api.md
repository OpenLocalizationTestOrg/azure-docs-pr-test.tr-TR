---
title: "Dağıtımı, çağrı ve web API'leri ve REST API'leri Azure Logic Apps için kimlik doğrulaması | Microsoft Docs"
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Dağıtımı, arama ve özel API'leri olarak bağlayıcılar mantıksal uygulamalar için kimlik doğrulaması

Çalıştırdıktan sonra [özel API oluşturma](./logic-apps-create-api-app.md) eylemler veya logic apps akışlarında kullanmak için Tetikleyiciler sağlayın, bunları çağırmadan önce Apı'lerinizi dağıtmanız gerekir. Ve bir mantıksal uygulama, en iyi deneyim için herhangi bir API'yi çağırabilirsiniz rağmen ekleyin [Swagger meta verileri](http://swagger.io/specification/) , API'nin işlemlerini ve parametrelerini açıklar. Bu Swagger dosyası API'nizi daha iyi ve daha kolay logic apps ile tümleştirmenize yardımcı olur.

API olarak dağıtabilir miyim [web uygulamaları](../app-service-web/app-service-web-overview.md), ancak API olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'leri bulutta ve şirket içi kullanabilir. Tüm Apı'lerinizi kodda değişiklik--yalnızca kodunuzun bir API uygulamasına dağıtmak yok. Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS).

Logic apps gelen çağrıları, API'lerine doğrulamak için kodunuzu güncelleştirin zorunda kalmamak için Azure portalında Azure Active Directory'yi ayarlama ayarlayabilirsiniz. Veya gerektirir ve kimlik doğrulama, API'nin kodlarda zorlayın.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>API'nizi bir web uygulaması veya API uygulaması olarak dağıtma

Özel API'nizi mantığı uygulamadan aramadan önce Azure App Service'e API'nizi bir web uygulaması veya API uygulaması olarak dağıtın. Ayrıca, Swagger belgesinin mantığı Uygulama Tasarımcısı tarafından okunabilir hale getirmek için API tanımı özelliklerini ayarlamak ve Aç [çıkış noktaları arası kaynak paylaşımı (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) web uygulaması veya API uygulaması için.

1. Azure portalında web uygulaması veya API uygulaması seçin.

2. Açılır ve altında dikey penceresinde **API**, seçin **API tanımı**. Ayarlama **API tanımı konumu** swagger.json dosyanızı URL'si.

   Genellikle, URL şöyle görünür:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Özel API için Swagger dosyasına bağlantı](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Altında **API**, seçin **CORS**. CORS İlkesi'ni ayarlamak **çıkış izin** için  **'*'** (tüm izin ver).

   Bu ayar mantığı Uygulama Tasarımcısı'ndan istekleri verir.

   ![İstekleri mantığı Uygulama Tasarımcısı'ndan özel API'nizi izin verir.](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Daha fazla bilgi için bu makalelere bakın:

* [ASP.NET web API için Swagger meta verileri ekleme](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [ASP.NET web API'ları Azure App Service'e dağıtma](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Özel API'nizi mantığından uygulama iş akışları çağırın.

API tanımı özellikleri ve CORS ayarladıktan sonra özel API'nin tetikleyiciler ve Eylemler, logic app akışınıza eklemek kullanılabilir duruma gelir. 

*  Swagger URL'lere sahip Web siteleri görüntülemek için Logic Apps Tasarımcısı'nda, abonelik Web sitelerine göz atabilirsiniz.

*  Swagger belgesinin göstererek kullanılabilir eylemler ve girişleri görüntülemek için kullanın [HTTP + Swagger eylem](../connectors/connectors-native-http-swagger.md).

*  Yok veya bir Swagger belgesinin kullanıma API'leri dahil olmak üzere herhangi bir API'yi çağırmak için her zaman bir istekle oluşturabilirsiniz [HTTP eylemi](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-to-your-custom-api"></a>Kimlik doğrulaması, özel API çağrıları

Bu şekilde, özel API çağrıları güvenliğini sağlayabilirsiniz:

* [Kod değişiklikleri](#no-code): API'nizi ile koruma [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) Azure portalı üzerinden bu nedenle, kodunuzu güncelleştirin veya API'nizi yeniden dağıtmak zorunda değilsiniz.

  > [!NOTE]
  > Varsayılan olarak, Azure portalında kapatma Azure AD kimlik doğrulaması hassas yetkilendirme sağlamaz. Örneğin, bu kimlik doğrulama API'nizi yalnızca belirli bir kiracı için değil, belirli bir kullanıcı veya uygulama kilitler. 

* [API kodunu güncelleştirin](#update-code): zorlayarak API'nizi koruma [sertifika kimlik doğrulaması](#certificate), [temel kimlik doğrulaması](#basic), veya [Azure AD kimlik doğrulaması](#azure-ad-code) kodlarda.

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a>Kodunu değiştirmeden, API çağrıları kimlik doğrulaması

Bu yöntem için genel adımlar aşağıdadır:

1. İki oluşturmak [Azure Active Directory (Azure AD) uygulama kimlikleri](../app-service-api/app-service-api-dotnet-service-principal-auth.md): mantıksal uygulamanızı, diğeri web uygulaması (veya API uygulaması) için.

2. API'nizi çağrı kimliğini doğrulamak için kimlik bilgilerini (istemci kimliği ve parolası) kullanın [hizmet sorumlusu](../app-service-api/app-service-api-dotnet-service-principal-auth.md) mantıksal uygulamanız için Azure AD uygulama kimliği ile ilişkili.

3. Uygulama kimlikleri mantığı uygulama tanımınızı içerir.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>1. Kısım: mantıksal uygulamanız için bir Azure AD uygulama kimliği oluşturma

Mantıksal uygulamanızı Azure AD karşı kimlik doğrulaması için bu Azure AD uygulama kimliğini kullanır. Yalnızca bu kimliği dizininiz için bir kez ayarlamanız gerekir. Örneğin, her mantıksal uygulama için benzersiz kimlik Oluştur olsa bile, tüm mantıksal uygulamalar için aynı kimlik kullanmayı seçebilirsiniz. Azure portalında bu kimlikleri ayarlayabilirsiniz [Klasik Azure portalı](#app-identity-logic-classic), veya [PowerShell](#powershell).

**Azure portalda mantıksal uygulamanızı için uygulama kimliği oluşturma**

1. İçinde [Azure portal](https://portal.azure.com "https://portal.azure.com"), seçin **Azure Active Directory**. 

2. Web uygulaması veya API uygulaması olarak aynı dizinde olduğunuzu doğrulayın.

   > [!TIP]
   > Dizinleri geçmek için profilinizi tıklatın ve başka bir dizin seçin. Ya da seçin **genel bakış** > **anahtar dizini**.

3. Dizin menüsünde altında **Yönet**, seçin **uygulama kayıtlar** > **yeni uygulama kaydı**.

   > [!TIP]
   > Varsayılan olarak, dizininizdeki tüm uygulama kayıtları uygulama kayıtlar listesi gösterilir. Yalnızca, uygulama kayıtlar yanındaki Arama kutusunu görüntülemek için seçin **uygulamalarım**. 

   ![Yeni uygulama kaydı oluşturun](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Uygulama kimliğinizi bir ad verin, bırakın **uygulama türü** kümesine **Web uygulaması / API**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si**ve seçin **Oluştur**.

   ![URL için uygulama kimliği oturum adı girin ve](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   Mantıksal uygulamanız artık oluşturduğunuz uygulama kimliğini uygulama kayıtlar listesinde görüntülenir.

   ![Mantıksal uygulamanız için uygulama kimliği](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Uygulama kayıtlar listesinde, yeni uygulama kimliğini seçin. Kopyalayıp kaydedin **uygulama kimliği** mantıksal uygulamanızı bölümü 3'te "istemci kimlik" olarak kullanılmak üzere.

   ![Kopyalayın ve mantıksal uygulama için uygulama kimliği kaydedin](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Uygulama Kimliği ayarlarınızı görünür durumda değilse, seçin **ayarları** veya **tüm ayarları**.

7. Altında **API erişimini**, seçin **anahtarları**. Altında **açıklama**, anahtarınız için bir ad sağlayın. Altında **Expires**, anahtarınız için bir süre seçin.

   Oluşturmakta olduğunuz anahtar uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.

   ![Mantıksal uygulama kimliği için anahtar oluşturma](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Araç çubuğunda seçin **kaydetmek**. Altında **değeri**, anahtarınızı artık görünür. 
**Kopyalama ve anahtarınızı kaydetmek emin olun** daha sonra kullanmak üzere anahtar gizli olduğu çıktığınızda anahtar dikey.

   Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, bu anahtarı parola ya da "gizli" olarak belirtin.

   ![Kopyalayın ve anahtarı için daha sonra kaydedin](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Azure Klasik Portalı'nda mantığı uygulamanız için uygulama kimliği oluşturma**

1. Klasik Azure portalında seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Web uygulaması veya API uygulaması için kullandığınız aynı dizini seçin.

3. Üzerinde **uygulamaları** sekmesinde, seçin **Ekle** sayfanın sonundaki.

4. Uygulama kimliğinizi bir ad verin ve seçin **sonraki** (sağ ok).

5. Altında **uygulama özellikleri**, benzersiz bir sağlamak için bir etki alanı olarak biçimlendirilmiş dize **oturum açma URL'si** ve **uygulama kimliği URI'si**ve seçin **tam** (onay işareti).

6. Üzerinde **yapılandırma** sekmesinde, kopyalamak ve kaydetme **istemci kimliği** bölümü 3'te kullanmak mantığı uygulamanız için.

7. Altında **anahtarları**, açık **seçin süresi** listesi. Anahtarınız için bir süre seçin.

   Oluşturmakta olduğunuz anahtar uygulama kimliğin "gizli" veya parolasını mantıksal uygulamanızı olarak görev yapar.

8. Sayfanın alt kısmındaki seçin **kaydetmek**. Birkaç saniye beklemeniz gerekebilir.

9. Altında **anahtarları**kopyaladığınızdan emin olun ve anahtarı kaydetme artık görünür. 

   Mantıksal uygulamanızı bölümü 3'te yapılandırdığınızda, bu anahtarı parola ya da "gizli" olarak belirtin.

Daha fazla bilgi için bilgi nasıl [uygulama hizmeti uygulamanızı Azure Active Directory oturum açma kullanacak şekilde yapılandırma](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**PowerShell'de mantığı uygulamanız için uygulama kimliği oluşturma**

Bu görevi PowerShell ile Azure Resource Manager aracılığıyla gerçekleştirebilirsiniz. PowerShell'de aşağıdaki komutları çalıştırın:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Kopyaladığınızdan emin olun **Kiracı kimliği** (GUID) Azure AD kiracınız için **uygulama kimliği**ve kullandığınız parola.

Daha fazla bilgi için bilgi nasıl [kaynaklarına erişmek için PowerShell ile bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Bölüm 2: web uygulaması veya API uygulaması için bir Azure AD uygulama kimliği oluşturma

Web uygulaması veya API uygulama zaten dağıtılmışsa, kimlik doğrulamasını etkinleştirmek ve Azure portalında uygulama kimliği oluşturun. Aksi takdirde, şunları yapabilirsiniz [bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek](#authen-deploy). 

**Uygulama Kimliği oluşturma ve kimlik doğrulama dağıtılan uygulamalar için Azure Portalı'nda Aç**

1. İçinde [Azure portal](https://portal.azure.com "https://portal.azure.com"), bulma ve web uygulaması veya API uygulaması seçin. 

2. Altında **ayarları**, seçin **kimlik doğrulama/yetkilendirme**. Altında **App Service kimlik doğrulaması**, kimlik doğrulamasını **üzerinde**. Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**.

   ![Kimlik doğrulamasını etkinleştirmek](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Artık web uygulaması veya API uygulaması için uygulama kimliği, aşağıda gösterildiği gibi oluşturun. Üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** için **Express**. Seçin **yeni AD uygulaması oluştur**. Uygulama kimliğinizi bir ad verin ve seçin **Tamam**. 

   ![Web uygulaması veya API uygulaması için uygulama kimliği oluşturma](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Üzerinde **kimlik doğrulama / yetkilendirme dikey**, seçin **kaydetmek**.

Artık web uygulaması veya API uygulaması ile ilişkili olan uygulama kimliği için istemci kimliği ve Kiracı kimliği bulmanız gerekir. Bu kimlikleri bölümü 3'te kullanın. Bu nedenle Azure portalı için aşağıdaki adımları devam veya [Klasik Azure portalı](#find-id-classic).

**Web uygulaması veya API uygulaması için uygulama kimliği'nin istemci kimliği ve Kiracı kimliği Azure portalında Bul**

1. Altında **kimlik doğrulama sağlayıcıları**, seçin **Azure Active Directory**. 

   !["Azure Active Directory" seçin](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Üzerinde **Azure Active Directory ayarları** dikey penceresinde ayarlamak **yönetim modu** için **Gelişmiş**.

3. Kopya **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.

   > [!TIP] 
   > Varsa **istemci kimliği** ve **veren URL'si** yoksa, görünür, Azure portal'ı yenilemeyi deneyin ve 1. adım yineleyin.

4. Altında **veren URL'si**, kopyalamak ve yalnızca GUID için bölümü 3 kaydedin. Aynı zamanda bu GUID web uygulamanızı veya API uygulamasının dağıtım şablonu, gerekirse kullanabilirsiniz.

   Bu GUID belirli kiracının GUID ("Kiracı kimliği") ve bu URL'de görünmelidir:`https://sts.windows.net/{GUID}`

5. Değişikliklerinizi kaydetmeden kapatın **Azure Active Directory ayarları** dikey.

<a name="find-id-classic"></a>

**Uygulama Kimliği'nin istemci kimliği ve Kiracı kimliği web uygulamanızı veya API uygulaması için Azure Klasik Portalı'nda bulunamıyor**

1. Klasik Azure portalında seçin [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Web uygulaması veya API uygulaması için kullandığınız dizini seçin.

3. İçinde **arama** kutusunda bulmak ve web uygulaması veya API uygulaması için uygulama kimliği seçin.

4. Üzerinde **yapılandırma** sekmesinde, kopya **istemci kimliği**ve bölüm 3'te kullanmak için bu GUID'i kaydedin.

5. İstemci kimliği alt kısmındaki aldıktan sonra **yapılandırma** sekmesinde, seçin **uç noktaları görüntülemek**.

6. URL'sini kopyalayın **Federasyon meta veri belgesi**ve bu URL'sine gidin.

7. Kök açar meta veri belgesi bulabilir **EntityDescriptor kimliği** var öğesi bir **Entityıd** özniteliği bu formda:`https://sts.windows.net/{GUID}` 

      Bu öznitelik belirli kiracının GUID (Kiracı kimliği) olarak GUID'dir.

8. Kiracı kimliği kopyalayın ve gerekirse kullanmak için bu kimliği bölümü 3'te ve web uygulamanızı veya API uygulamasının dağıtım şablonu kullanmak üzere kaydedin.

Daha fazla bilgi için şu konulara bakın:

* [Azure uygulama hizmetinde API uygulamaları için kullanıcı kimlik doğrulaması](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Bir Azure Resource Manager şablonu ile dağıtırken kimlik doğrulamasını etkinleştirmek**

Hala mantığı uygulamanız için uygulama kimliği web uygulaması veya farklı bir API uygulaması için bir Azure AD uygulama kimliği da oluşturmanız gerekir. Uygulama kimliği oluşturmak için Azure portalı için Kısım 2 önceki adımları izleyin. Ayrıca, 1. Bölüm adımları ancak web uygulamanızı veya API uygulamasının gerçek kullandığınızdan emin olun `https://{URL}` için **oturum açma URL'si** ve **uygulama kimliği URI'si**. Bu adımları, istemci kimliği ve Kiracı kimliği, uygulamanızın dağıtım şablonu kullanmak için ve ayrıca bölümü 3 kaydetmek gerekir.

> [!NOTE]
> Web uygulaması veya API uygulaması için Azure AD uygulama kimliği oluşturduğunuzda, Azure portalında veya Klasik Azure portalı yerine PowerShell kullanmanız gerekir. PowerShell komutunu kullanıcılar bir Web sitesine oturum için gerekli izinleri ayarlayın değil.

İstemci kimliği ve Kiracı kimliği aldıktan sonra bu kimlikleri subresource web uygulaması veya API uygulaması için dağıtım şablonunda olarak şunları içerir:

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

Boş web uygulaması ve bir mantıksal uygulama Azure Active Directory kimlik doğrulaması ile birlikte otomatik olarak dağıtmak için [burada tam şablonu görüntüleme](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), veya **Azure'a Dağıt** burada:

[![Azure’a dağıtma](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a>3. Kısım: mantıksal uygulamanızı yetkilendirme bölümünde doldurma

Önceki şablonu zaten bu yetkilendirmesi bölümünde ayarladığınız sahip, ancak mantıksal uygulama doğrudan yazıyorsanız, tam yetkilendirme bölümü içermelidir.

Açık mantığı uygulama tanımınızı kod görünümünde Git **HTTP** eylem bölümü Bul **yetkilendirme** bölümünde ve bu satırı ekleyin:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Öğesi | Açıklama |
| ------- | ----------- |
| Kiracı |Azure AD kiracısı için GUID |
| Hedef kitle |Gerekli. Erişim - web uygulaması veya API uygulaması için uygulama kimliği istemci Kimliğinden istediğiniz hedef kaynak için GUID |
| istemci kimliği |Access - mantıksal uygulamanızı için uygulama kimliği istemci Kimliğinden isteyen istemci için GUID |
| Gizli |Gerekli. Anahtar ya da erişim belirteci isteyen istemci için uygulama kimliği paroladan |
| type |Kimlik doğrulama türü. ActiveDirectoryOAuth kimlik doğrulaması için değerdir `ActiveDirectoryOAuth`. |

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

Web uygulaması veya API uygulaması için mantıksal uygulamanızı öğesinden gelen istekleri doğrulamak için istemci sertifikaları kullanabilirsiniz. Kodu ayarlamak için bilgi [TLS karşılıklı kimlik doğrulamasını yapılandırmak nasıl](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

İçinde **yetkilendirme** bölümünde, bu satırı ekleyin: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Öğesi | Açıklama |
| ------- | ----------- |
| type |Gerekli. Kimlik doğrulama türü. SSL istemci sertifikaları için değer olmalıdır `ClientCertificate`. |
| password |Gerekli. İstemci sertifikası (PFX dosyası) erişmek için parola |
| PFX |Gerekli. Base64 ile kodlanmış içeriği istemci sertifikasını (PFX dosyası) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Temel kimlik doğrulaması

Web uygulaması veya API uygulaması mantıksal uygulamanızı öğesinden gelen istekleri doğrulamak için bir kullanıcı adı ve parola gibi temel kimlik doğrulaması kullanabilirsiniz. Temel kimlik doğrulaması genel bir desen olduğundan ve web uygulaması veya API uygulaması oluşturmak için kullanılan herhangi bir dilde bu kimlik doğrulaması kullanabilirsiniz.

İçinde **yetkilendirme** bölümünde, bu satırı ekleyin:

`{"type": "basic", "username": "username", "password": "password"}`.

| Öğesi | Açıklama |
| --- | --- |
| type |Gerekli. Kimlik doğrulama türü. Temel kimlik doğrulaması için değer olmalıdır `Basic`. |
| kullanıcı adı |Gerekli. Kimlik doğrulaması için kullanıcı adı |
| password |Gerekli. Kimlik doğrulaması için parola |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Kod aracılığıyla Azure Active Directory kimlik doğrulaması

Varsayılan olarak, Azure portalında kapatma Azure AD kimlik doğrulaması hassas yetkilendirme sağlamaz. Örneğin, bu kimlik doğrulama API'nizi yalnızca belirli bir kiracı için değil, belirli bir kullanıcı veya uygulama kilitler. 

Mantıksal uygulamanızı kodlarda için API erişimini kısıtlamak için JSON web token (JWT) sahip üstbilgi ayıklayın. Arayanın Kimliği denetleyin ve eşleşmeyen istekleri reddedecek.

Ayrıca, bu kimlik doğrulama kendi kodunuzu tamamen uygulamak ve Azure portalını kullanma yükleneceği öğrenin nasıl [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](../app-service-web/web-sites-authentication-authorization.md).

Mantıksal uygulamanız için bir uygulama kimliği oluşturmak ve bu kimlik, API çağrısı için kullanmak için önceki adımları izlemelisiniz.

## <a name="next-steps"></a>Sonraki adımlar

* [Tanılama günlükleri ve Uyarıları ile mantığı uygulama performansını kontrol etme](logic-apps-monitor-your-logic-apps.md)