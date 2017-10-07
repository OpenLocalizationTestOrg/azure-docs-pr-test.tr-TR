---
title: "Azure Active Directory’de uygulamalar, izinler ve onay.| Microsoft Docs"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar."
keywords: "Azure AD Connect nedir giriş tooAzure AD, uygulamalar, active Directory'yi yükleyin"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Azure Active Directory’de uygulamalar, izinler ve onay
Azure Active Directory içinde uygulamalar tooyour dizini ekleyebilirsiniz.  Merhaba uygulamaları uygulama hello türüne bağlı olarak değişebilir.  tooview uygulamalar hello Klasik Portalı'nda bir dizin seçin ve uygulamaları seçin.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

## <a name="types-of-apps"></a>Uygulama türleri

1. **Tek kiracılı uygulamalar** </br>
    - **Tek Kiracı uygulamaları** -genellikle tooas iş kolu (LOB) uygulamaları adlandırılır. Burada birisi kuruluşunuz içinde kendi uygulama geliştirir ve hello kuruluş toobe mümkün toosign toohello uygulamasında kullanıcıların görmesini hello böyledir.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Uygulama proxy'si uygulamaları** - Azure AD uygulaması Proxy, şirket içi uygulamayla kullanıma tek Kiracı uygulama kiracınızda (toplama toohello uygulama Proxy Hizmeti) kaydedilir. Bu uygulama tüm bulut etkileşimleri (örneğin, kimlik doğrulaması) için şirket içi uygulamanızı temsil eder. (Uygulama Ara Sunucusu, Azure AD Temel veya daha yüksek sürüm gerektirir.)


2. **Çok kiracılı uygulamalar**
    - **Diğerleri için onay çok kiracılı uygulamalar** - benzer çok "kuruluşunuzun geliştirdiği uygulamalarla tek Kiracı uygulamalar". Merhaba ana (Merhaba uygulama mantığı hello) yanı sıra diğer kiracılar kullanıcılardan de toohello uygulamasında tooand oturum onay farktır.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Başkalarının geliştirdiği ve Contoso’nun onay verebildiği çok kiracılı uygulamalar**. (Veya kısaca “onaylanan uygulamalar”.) Bu, "çok kiracılı uygulamalar, kuruluşunuzun geliştirdiği uygulamalarla" Merhaba Çevir tarafında bulunur. Başka bir kuruluştaki bir çok kiracılı uygulama geliştirir, kullanıcılar, kuruluşunuzun toohello uygulama onay ve tooit oturum açın.
    - **Microsoft birinci taraf uygulamaları** - Microsoft hizmetlerini temsil eden uygulamalar. Onay hello Hizmeti'ne kaydolma hello olgu tarafından yönetilir. Bazen özel UX ve yoktur belirli birinci taraf uygulamaları için genellikle ilkeleri erişim toohello uygulama etrafında kurarken kullanılan mantığı.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Önceden tümleştirilen uygulamalar** -Apps hello ekleyebileceğiniz Azure AD uygulama galerisinde kullanılabilir tooyour directory tooprovide tek oturum açma (ve sağlama bazı durumlarda) toopopular SaaS uygulamaları.
    - **Azure AD çoklu oturum açma**: SAML 2.0 veya OpenID Connect gibi desteklenen bir oturum açma protokolü aracılığıyla Azure AD ile tümleştirilebilen “Gerçek” SSO. Başlangıç Sihirbazı'nı ayarlama işlemleri size yol göstermektedir.
    - **Parola çoklu oturum açma**: Azure AD güvenli bir şekilde hello uygulama hello kullanıcının kimlik bilgilerini depolar ve hello kimlik bilgileri "eklenen" oturum açma hello forma hello Azure AD uygulama erişim tarayıcı uzantısı tarafından. Bu işlem aynı zamanda “parola kasası oluşturma” olarak bilinir.

## <a name="permissions"></a>İzinler

Uygulama kaydedildikten sonra hello uygulama kaydı (diğer bir deyişle, hello Geliştirici) gerçekleştiren hello kullanıcısı hangi izinleri hello uygulamanın erişmesi ve hangi kaynaklara tanımlar. (Merhaba kaynaklardır, kendilerini diğer uygulamaları olarak tanımlanmış.) Örneğin, birisi posta okuyucu uygulaması oluşturmaya durum, uygulama hello "Posta kutularına erişim hello oturum açmış kullanıcı olarak" hello "Office 365 Exchange Online" kaynak izin gerektirir:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Bir uygulama (Merhaba istemci) toorequest başka bir uygulama (Merhaba kaynak) belirli bir izni için sırayla hello geliştiricisine hello kaynak mevcut hello izinleri tanımlar. Bizim örneğimizde, Microsoft, kaynak uygulama "Office 365 Exchange Online" hello, hello sahibi "Posta kutularına erişim hello oturum açmış kullanıcı olarak" adlı bir izin tanımladınız.

İzinleri tanımlarken hello uygulama geliştiricisi izin hello izni verdiği veya yönetici onayı gerektirip gerektirmediğini tanımlamanız gerekir. Bu geliştiriciler tooallow kullanıcılar tooconsent yalnızca düşük duyarlılık izinleri isteyen kendi tooapps sağlar, ancak admins tooconsent toomore hassas izinleri gerektirir. Örneğin, "Azure Active Directory" kaynak uygulama Merhaba, sınırlı salt okunur izinleri isteyen tooapps, kullanıcıların kabul şekilde, tanımlanmış.  Ancak, tam okuma izinleri ve tüm yazma izinleri için yönetici onayı gereklidir.

Yerel istemcilerin kimliği doğrulanmadığı için, yerel istemci uygulaması olarak tanımlanmış bir uygulama yalnızca temsilci atanmış izinler isteyebilir. Bu durum, bir belirteç edinilirken her zaman gerçek bir kullanıcının rol alması gerektiği anlamına gelir. Web uygulamaları ve web API’leri (gizli istemciler) için erişim belirteci alınırken mutlaka Azure AD ile kimlik doğrulaması yapılmalıdır. Ayrıca sahip oldukları yalnızca uygulama izinleri isteyen hello olasılığını anlamına gelir. Örneğin, bir arka uç hizmetine tooauthenticate tooanother arka uç hizmetine gerekiyorsa. Yalnızca uygulama izinleri isteyen uygulamalar her zaman yönetici onayı gerektirir.

Özetlemek gerekirse:



- Bir uygulama (istemci), diğer uygulamalar (kaynaklar) için gereken hello izinleri belirtir.
- Bir uygulama (kaynak) hangi izinlerin gösterilen tooother uygulamaların (istemciler) olduğunu belirtir.
- Bir izin yalnızca uygulama izni ya da temsilci atanmış izin olabilir.
- Temsilci atanmış izin, “kullanıcı onayına izin verir” veya “yönetici onayı gerektirir” olarak işaretlenebilir.
- Bir uygulamayı bir istemci olarak (izinleri tooa kaynak gerektiğini bildirerek), (Bu sunan hangi izinlerin bildirme tarafından) bir kaynak olarak ya da her ikisini de olarak davranabilir.

## <a name="controls"></a>Denetimler

Merhaba, hello farklı yönetici denetimleri bu davranış için kullanılabilir listesi aşağıdadır. hello Yöneticisi denetimleri hello Klasik Portalı'ndan erişilebilen hello dizini altında yapılandırın.

![](media/active-directory-apps-permissions-consent/apps7.png)

Hello Azure'nın altında portal **yönetmek**, **kullanıcı ayarlarını**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Kullanıcıların tooapps onayı olup olmadığını denetleyebilirsiniz:

Merhaba Klasik portalında seçin **kullanıcıların kendi verilerini uygulamaları izinleri tooaccess verebileceği.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Hello Azure portal, seçin **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Kullanıcılar kendi tek Kiracı İş KOLU uygulamaları kaydolabilir olup olmadığını denetleyebilirsiniz: hello Klasik portal seçin **kullanıcıları tümleşik uygulamalar eklemek.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Hello Azure portal, seçin **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Tooregister tek Kiracı İş KOLU uygulamaları kullanıcıların olsa bile toowhat kaydedilebilir sınırları vardır.  
>Örneğin, dizin yöneticisi olmayan geliştiriciler.
>
>- Kullanıcılar tek kiracılı bir uygulamayı çok kiracılı uygulama yapamaz.
>- Tek Kiracı İş KOLU uygulamaları kaydederken, kullanıcılar yalnızca uygulama izinleri tooother uygulamaları isteğinde bulunamaz.
>- Bu izinleri yönetici onayı gerektiriyorsa tek Kiracı İş KOLU uygulamaları kaydederken izinlere temsilci tooother uygulamaları isteğinde bulunamaz.
>- Kullanıcıların sahipleri olmadıkları değişiklikleri tooapps yapamazsınız.



- Kullanıcıların parola SSO (diğer adıyla “parola kasası oluşturma”) kullanan önceden tümleştirilmiş uygulamalar ekleyip ekleyemeyeceğini denetleyebilirsiniz ![](media/active-directory-apps-permissions-consent/apps10.png)



- Uygulamalara hangi koşullar altında erişilebileceğini denetleyebilirsiniz (koşullu erişim). Bu hem toohello istemci uygulaması hem de toohello kaynak uygulama geçerlidir unutmayın. Bu nedenle, bu hello "Office 365 Exchange Online" uygulama yalnızca uyumlu makinelerden erişilebilir bildiren bir koşullu erişim ilkesi ayarlayabilirsiniz söyleyin.  Bir kullanıcı toouse çevrimiçi izinleri tooExchange ister bir istemci uygulaması çalıştığında bu ilkeyi de ilkenin etkisini gösterip.



- İçine razı tooand hangilerinin kullanılmakta olan uygulamaları silinmiş görünürlüğe sahiptir.

1.  Bir kullanıcı tooan uygulama izin ServicePrincipal nesne hello Kiracı içinde oluşturulur. ServicePrincipal oluşturma hello denetim raporuna dahil edilir.
2.  Kullanıcı oturum açma etkinliği raporları için hangi uygulama hello kullanıcı oturum söyleyin. 

## <a name="example"></a>Örnek

Örnek olarak, Kiracı kullanıcılar için oturum açtığınız fark hello "FabrikamMail Office 365 için" uygulama atalım. “FabrikamMail”, “Fabrikam, Inc.” tarafından yayımlanan Android’e yönelik bir posta okuma uygulamasıdır. Bu hello döner "çok kiracılı uygulamalara Contoso onayı diğer geliştirme".

Kullanıcıların tooconsent izin verilirse, ilk kez oturum onay istemi hello alın:![](media/active-directory-apps-permissions-consent/apps14.png)

", Posta kutularına erişebilmeleri" Merhaba kullanıcı dönük izin dizesi "Office 365 Exchange Online tarafından" (diğer bir deyişle, Exchange) kullanıma sunulan hello "Posta kutularına erişim hello oturum açmış kullanıcı olarak" izni olur.

Office 365 için kaydolurken hangi eklendi Exchange (Merhaba kaynak) hello ServicePrincipal nesnesi arayarak hello izinleri görebilirsiniz. Farklı seçenekler ve yapılandırmaları kaydetmek için kullanılan kiracınızda bulunan hello ServicePrincipal nesnesinin örneği"" Merhaba uygulama düşünebilirsiniz.  Bu hello kullanarak bkz `Get-AzureADServicePrincipal` PowerShell'de.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

"Kabul et" Merhaba kullanıcı tıkladığında izin başlatılır. İlk olarak, "Office 365 için FabrikamMail" için bir ServicePrincipal nesnesi hello Kiracı içinde oluşturulur. Merhaba ServicePrincipal şuna benzer:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Onaylıyorsunuz tooan uygulamasını hello aşağıdaki arasında bir Oauth2PermissionGrant bağlantı oluşturur:
  
- Merhaba kullanıcı nesnesi
- Merhaba istemci uygulamaları ServicePrincipalName (SPN)
- Merhaba kaynak uygulamaları ServicePrincipalName (SPN)
- Merhaba kaynak uygulama izinleri.  

FabrikamMail Hello durumda onu şuna benzer:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientID** FabrikamMail'ın hizmet asıl nesne kimliği (Merhaba, yeni oluşturduğunuz), **Principalıd** hello kullanıcı nesne kimliği (Merhaba kullanıcının) rıza, **ResourceId**Exchange'in hizmet asıl nesne kimliği, kapsam olduğundan izin verdiği Exchange hello izni olan).

Kullanıcıların tooconsent izin verilmiyorsa, bu izni bildiren bir ekran gereklidir görürler.

