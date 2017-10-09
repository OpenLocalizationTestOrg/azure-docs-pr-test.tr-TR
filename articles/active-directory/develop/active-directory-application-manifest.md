---
title: aaaUnderstanding hello Azure Active Directory Uygulama bildirimi | Microsoft Docs
description: "Azure AD kiracısı bir uygulamanın kimlik yapılandırmada gösteren ve kullanılan toofacilitate OAuth yetkilendirme, onayı deneyimi ve daha fazlası hello Azure Active Directory Uygulama bildirimini ayrıntılı kapsamını."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Hello Azure Active Directory Uygulama bildirimini anlama
Azure Active Directory (AD ile) tümleştirme uygulamaları hello uygulaması için sürekli kimlik yapılandırma sağlayan bir Azure AD kiracısı ile kayıtlı olması gerekir. Bu yapılandırma, bir uygulama toooutsource Aracısı kimlik doğrulama/yetkilendirme ve Azure AD üzerinden izin senaryoları etkinleştirme zamanında alınmadığında. Merhaba hello Azure AD uygulama modeli hakkında daha fazla bilgi için bkz: [ekleme, güncelleştirme ve uygulama kaldırma] [ ADD-UPD-RMV-APP] makalesi.

## <a name="updating-an-applications-identity-configuration"></a>Bir uygulamanın kimlik yapılandırması güncelleştiriliyor
Özellikleri ve derece hello aşağıdakiler dahil zorluk farklılık uygulamanın kimlik yapılandırması hello özelliklerini güncelleştirmek için kullanılabilir gerçekte birden çok seçenek vardır:

* Merhaba  **[Azure portal'ın] [ AZURE-PORTAL] Web kullanıcı arabirimi** tooupdate hello en yaygın bir uygulamanın özelliklerini sağlar. Bu hızlı başlangıç ve uygulamanızın özelliklerini güncelleştirme en az hata potansiyeli yolu ancak desteklemez tam erişim tooall özellikleri, sonraki iki yöntem hello gibi verin.
* Gereken yeri hello Klasik Azure portalı sunulmaz tooupdate özellikleri daha Gelişmiş senaryolar için hello değiştirebilirsiniz **uygulama bildirimi**. Bu, bu makalenin hello odak ve hello sonraki bölümde başlangıç daha ayrıntılı ele alınmıştır.
* Ayrıca çok mümkündür**hello kullanan bir uygulamayı yazma [grafik API'si] [ GRAPH-API]**  tooupdate gerektiren uygulamanızı hello en çaba. Yönetim yazılımı yazma veya otomatik bir şekilde, düzenli olarak tooupdate uygulama özellikleri ihtiyacınız varsa bu çekici bir seçenek yine de olabilir.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Bir uygulamanın kimlik yapılandırması Hello uygulama bildirimi tooupdate kullanma
Merhaba aracılığıyla [Azure portal][AZURE-PORTAL], uygulamanızın kimlik yapılandırması hello satır içi bildirim Düzenleyicisi'ni kullanarak hello uygulama bildirimi güncelleştirerek yönetebilirsiniz. Ayrıca, indirin ve hello uygulama bildirimi bir JSON dosyası olarak yükleyin. Herhangi bir gerçek dosyası hello dizininde depolanır. Merhaba uygulama bildirimi yalnızca bir HTTP GET işlemi hello Azure AD Graph API uygulama varlığı ve hello karşıya yükleme hello uygulama varlığı üzerinde bir HTTP PATCH işlemi.

Sonuç olarak, sipariş toounderstand hello biçimi ve hello uygulama bildirimi özelliklerini tooreference hello grafik API'si ihtiyacınız olacak [uygulama varlığı] [ APPLICATION-ENTITY] belgeleri. Uygulama bildirimi olsa karşıya yükleme gerçekleştirilebilir güncelleştirmeleri örnekleri şunlardır:

* **İzin kapsamları (oauth2Permissions) bildirme** web API tarafından kullanıma sunulan. Merhaba "Exposing Web API'leri tooOther uygulamaları" konusuna bakın [Azure Active Directory Tümleştirme uygulamalarla] [ INTEGRATING-APPLICATIONS-AAD] hello kullanılarak kullanıcı kimliğine bürünme özelliğini uygulama hakkında bilgi için oauth2Permissions izni kapsam temsilci. Daha önce belirtildiği gibi uygulama varlık özellikleri hello grafik API'si belgelenen [varlık ve karmaşık tür] [ APPLICATION-ENTITY] başvurusu makalesinde olan hello oauth2Permissions özelliği de dahil olmak üzere, bir Koleksiyon türü [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Uygulama rolleri (appRoles) uygulamanız tarafından kullanıma sunulan bildirme**. Merhaba uygulama varlığın appRoles özellik türü koleksiyonudur [uygulama rolü][APPLICATION-ENTITY-APP-ROLE]. Merhaba bkz [rol tabanlı erişim denetimi kullanarak Azure AD bulut uygulamalarında] [ RBAC-CLOUD-APPS-AZUREAD] makale uygulama örneği.
* **Bilinen istemci uygulamaları (knownClientApplications) bildirme**, belirtilen istemci uygulamaları toohello kaynak/web API hello toologically bağ hello izni ver.
* **Azure AD tooissue grup üyeliklerini talep isteği** kullanıcı (groupMembershipClaims) imzalı hello için.  Bu hello kullanıcı dizin rol üyeliklerini ilgili yapılandırılmış tooissue talepleri de olabilir. Merhaba bkz [AD grupları kullanarak bulut uygulamalarında yetkilendirme] [ AAD-GROUPS-FOR-AUTHORIZATION] makale uygulama örneği.
* **Uygulama toosupport OAuth 2.0 örtük grant izin** akışlar (oauth2AllowImplicitFlow). Grant akış bu tür katıştırılmış JavaScript web sayfaları veya tek sayfa uygulamaları (SPA) ile kullanılır. Merhaba örtük yetkilendirme verme hakkında daha fazla bilgi için bkz: [anlama hello OAuth2 örtük izin akışı Azure Active Directory'de][IMPLICIT-GRANT].
* **X509 kullanımını etkinleştirmek hello gizli anahtarı olarak sertifikaları** (keyCredentials). Merhaba bkz [yapı hizmeti ve arka plan programı uygulamaları Office 365'te] [ O365-SERVICE-DAEMON-APPS] ve [Geliştirici Kılavuzu tooauth Azure Kaynak Yöneticisi API'si ile] [ DEV-GUIDE-TO-AUTH-WITH-ARM] uygulama örnekleri makaleler.
* **Yeni bir uygulama kimliği URI'sini ekleyin** uygulamanızın (identifierURIs[]). Uygulama Kimliği URI kullanılır toouniquely uygulamanın kendi Azure AD kiracısı içinde (veya özel etki alanını doğruladıysanız nitelikli hale geldiğinde çok kiracılı senaryoları için birden çok Azure AD kiracılarıyla) tanımlayın. İzinleri tooa kaynak uygulama istenirken kullanılan veya bir kaynak uygulaması için bir erişim belirteci alınıyor. Bu öğe güncelleştirdiğinizde hello aynı güncelleştirme hello uygulamanın ev kiracısında yaşadığı toohello karşılık gelen hizmet sorumlusunun servicePrincipalNames [] koleksiyonu yapılır.

Merhaba uygulama bildirimi de en iyi yolu tootrack sağlar hello uygulama kaydınızı durumu. JSON biçiminde kullanılabilir olduğu için uygulamanızın kaynak kodunu yanı sıra, kaynak denetimine hello dosya gösterimi denetlenebilir.

## <a name="step-by-step-example"></a>Adım adım örnek tarafından
Şimdi sağlar, uygulamanızın kimlik yapılandırması hello uygulama bildirimi aracılığıyla hello adımları gerekli tooupdate yol. Biz örnekler, önceki hello birini nasıl toodeclare yeni bir izin kapsam bir kaynak uygulaması gösteren vurgular:

1. İçinde toohello oturum [Azure portal][AZURE-PORTAL].
2. Kimlik doğruladınız sonra Azure AD kiracınıza hello sağ üst köşeden hello sayfasının seçerek belirleyin.
3. Seçin **Azure Active Directory** üzerinde sol gezinti bölmesinin ve tıklatın hello uzantı **uygulama kayıtlar**.
4. Tooupdate hello listesinde istediğiniz ve tıklayın Merhaba uygulaması bulun.
5. Merhaba uygulama sayfasından tıklatın **bildirim** tooopen hello satır içi bildirim Düzenleyici. 
6. Bu düzenleyiciyi kullanarak hello bildirimi doğrudan düzenleyebilirsiniz. Bu hello bildirim izleyen hello hello şemasını Not [uygulama varlığı] [ APPLICATION-ENTITY] yukarıda belirtildiği gibi: Örneğin, tooimplement/sunmaya yeni bir izin istiyoruz varsayılarak "Employees.Read.All" adlı Kaynak uygulamamız üzerinde (API), yalnızca yeni/saniye öğe toohello oauth2Permissions koleksiyonu IE eklediğiniz:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    Merhaba girişi benzersiz olmalıdır ve bu nedenle yeni genel olarak benzersiz bir kimlik (GUID) hello için oluşturmalıdır `"id"` özelliği. Bu durumda, biz belirtilmediğinden `"type": "User"`, bu izni herhangi bir hesabı kimlik doğrulaması tarafından hello Azure AD Kiracı kaynak/API'si uygulamanızın hangi hello kayıtlı razı tooby olabilir. Bu verir hello istemci uygulama izni tooaccess hello hesabın adına üzerinde. Merhaba açıklama ve görünen ad dizeleri onay sırasında ve hello Azure Portalı'ndaki Görüntü için kullanılır.
6. Merhaba bildirimi güncelleştirme bittiğinde, tıklatın **kaydetmek** toosave hello bildirimi.  
   
Hello bildirimi kaydedilir, kayıtlı bir istemciyi yukarıda eklediğimiz uygulama erişim toohello yeni bir izin verebilirsiniz. Bu süre kullanabilirsiniz hello istemci uygulamanın bildirimi düzenleme yerine Azure portal'ın Web UI hello:  

1. Önce toohello Git **ayarları** hello dikey tooadd erişim toohello yeni API, istediğiniz istemci uygulaması toowhich tıklatın **gerekli izinler** ve seçin **bir API seçin** .
2. Ardından hello Kiracı (API) uygulamalarında kayıtlı kaynak hello listesiyle birlikte sunulur. Merhaba kaynak uygulama tooselect veya tür hello hello uygulama hello arama kutusuna adını tıklatın. Merhaba uygulaması buldunuz tıklatın **seçin**.  
3. Bu toohello sürecek **Select izinleri** uygulama izinleri ve izinlere hello kaynak uygulaması için kullanılabilen temsilci hello listesi gösterecektir sayfası. Select hello sipariş tooadd yeni izin onu toohello istemci izinleri listesini istedi. Bu yeni izni hello "requiredResourceAccess" koleksiyon özelliği de hello istemci uygulamanın kimlik yapılandırmada depolanır.


Bu kadar. Şimdi kendi yeni kimlik Yapılandırması'nı kullanarak uygulamalarınızı çalışır.

## <a name="next-steps"></a>Sonraki adımlar
* Bir uygulamanın uygulama ve hizmet sorumlusu nesneleri arasındaki ilişki hello hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneleri Azure AD'de][AAD-APP-OBJECTS].
* Merhaba bkz [Azure AD Geliştirici sözlüğü] [ AAD-DEVELOPER-GLOSSARY] bazı hello çekirdek Azure Active Directory (AD) Geliştirici kavramları tanımları için.

Lütfen tooprovide geri bildirim aşağıdaki hello Açıklamalar bölümüne kullanın ve daraltın ve içeriği şekil yardımcı olur.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

