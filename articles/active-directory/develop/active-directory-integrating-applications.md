---
title: "Azure Active Directory ile uygulamaları aaaIntegrating | Microsoft Docs"
description: "Nasıl tooadd, güncelleştirmek veya bir uygulamayı Azure Active Directory (Azure AD) kaldırmak ayrıntıları."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Uygulamaları Azure Active Directory ile tümleştirme
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Kurumsal geliştiriciler ve yazılım olarak-hizmet (SaaS) sağlayıcıları geliştirme ticari bulut hizmetlerini veya Azure Active Directory (Azure AD) tooprovide güvenli oturum açın ve yetkilendirme için ile tümleşik iş kolu uygulamaları kendi Hizmetler. toointegrate bir uygulama veya hizmet Azure AD ile bir geliştirici hello Klasik Azure Portalı aracılığıyla Azure AD ile ilk kendi uygulama hello ayrıntılarını kaydetmeniz gerekir.

Bu makalede nasıl tooadd, güncelleştirmek veya bir uygulamayı Azure AD'de kaldırmak gösterilmektedir. Merhaba farklı Azure AD ile nasıl tümleştirilebilir uygulama türlerini hakkında bilgi edineceksiniz tooconfigure uygulamaları tooaccess web API'leri gibi başka kaynaklar ve daha fazlası.

toolearn kayıtlı uygulama ve aralarındaki hello ilişki temsil eden daha hello iki Azure AD nesneler hakkında bkz [uygulama ve hizmet sorumlusu nesneleri](active-directory-application-objects.md); toolearn yönergeleri markalama hello hakkında daha fazla bilgi, Azure Active Directory ile uygulamaları geliştirirken kullanmak, bkz: [tümleşik uygulamalar için markalama yönergeleri](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Bir uygulama ekleme
Azure ad toouse hello yetenekleri istediği herhangi bir uygulama ilk Azure AD kiracısı kayıtlı olması gerekir. Bu kayıt işlemi hello URL olduğu gibi uygulamanızı Azure AD ayrıntılarını vermiş içerir bulunan, bir kullanıcının kimliği doğrulandıktan sonra URL toosend yanıtları Merhaba, hello uygulama ve benzeri tanımlayan URI hello.

Yalnızca toosupport oturum açma Azure AD'de kullanıcıları için gereken bir web uygulaması oluşturuyorsanız, yalnızca aşağıdaki hello yönergeleri izleyebilirsiniz. Uygulamanızın kimlik bilgileri veya izinleri tooaccess tooa web API gerekir ya da diğer tooallow kullanıcılardan gerekiyor tooaccess Azure AD kiracıları, bkz: [bir uygulamayı güncelleştirme](#updating-an-application) , uygulamanızın yapılandırma bölümü toocontinue.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister hello Azure portal'ın yeni bir uygulama
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.
4. Merhaba komut istemlerini izleyin ve yeni bir uygulama oluşturun. Belirli örnekler web uygulamaları veya yerel uygulamaları için isterseniz, kullanıma bizim [quickstarts](active-directory-developers-guide.md).
  * Web uygulamaları için hello sağlamak **oturum açma URL'si**, kullanıcılar, örneğin,'burada oturum açabilir, uygulamanızın hello temel URL olduğu `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Yerel uygulamalar için sağlayan bir **yeniden yönlendirme URI'si**, tooreturn belirteci yanıtları hangi Azure AD kullanır. Bir değer belirli tooyour uygulama girin. Örneğin`http://MyFirstAADApp`
5. Kayıt tamamladıktan sonra Azure AD, uygulamanızın hello uygulama kimliği bir benzersiz istemci tanımlayıcı atar. Uygulamanızı eklenir ve toohello hızlı başlangıç sayfasında uygulamanız için gerçekleştirilecek. Uygulamanızı bir web veya yerel uygulama olmasına bağlı olarak, farklı seçenekler konusunda görürsünüz tooadd ek yetenekler tooyour uygulama. Uygulamanızı eklendikten sonra uygulama tooenable kullanıcılar toosign diğer uygulamalarda erişim web API'leri, güncelleştirme başlar veya (veren diğer kuruluşların tooaccess uygulamanızı) çok kiracılı uygulama yapılandırın.

> [!NOTE]
> Varsayılan olarak, yeni oluşturulan hello uygulama kaydı, dizin toosign tooyour uygulamada yapılandırılan tooallow kullanıcılardan ' dir.
> 
> 

## <a name="updating-an-application"></a>Bir uygulamayı güncelleştirme
Uygulamanızı Azure AD ile kaydedildikten sonra güncelleştirilmiş toobe gerekebilir tooprovide tooweb API'leri erişmek için diğer kuruluşların ve daha fazla kullanılabilir duruma. Bu bölümde, uygulamanızın daha fazla tooconfigure gereksinim duyabileceğiniz çeşitli yolları açıklanmaktadır. İlk geliştiriciler, kuruluşunuzun veya başka bir kuruluş tarafından oluşturulan istemci uygulamalar tarafından kullanılan kaynak/API uygulamalar geliştiriyorsanız, önemli toounderstand olduğu biz hello onayı Framework bir bakış başlar.

Merhaba hakkında daha fazla bilgi için Azure AD'de şekilde kimlik doğrulaması çalışır, bkz: [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Merhaba izin Framework'e Genel Bakış
Merhaba istemci uygulaması, kayıtlı bir hello farklı bir Azure AD Kiracı tarafından güvenli hale getirilmiş API web tooaccess gerek yerel istemci uygulamaları ve Azure AD onay framework kolay toodevelop çok kiracılı web kolaylaştırır. Bu web API'leri dahil hello Microsoft Graph API (tooaccess Azure Active Directory, Intune ve Office 365'te Hizmetleri) ve diğer Microsoft hizmetlerini API'leri, ayrıca tooyour kendi web API'leri. bir kullanıcı veya yönetici toobe Dizin verilerine erişme içerebilir, dizinde kayıtlı ister onayı tooan uygulamasını vermiş Hello framework dayanır.

Örneğin, bir web istemci uygulaması hello kullanıcı Office 365'ten hakkındaki tooread Takvim bilgileri gerektiriyorsa, bu kullanıcının gerekli tooconsent toohello istemci uygulaması olacaktır. İzin verilen sonra Merhaba istemci uygulaması hello kullanıcı adına mümkün toocall hello Microsoft Graph API olması ve gerektiği gibi hello Takvim bilgileri kullanın. Merhaba [Microsoft Graph API](https://graph.microsoft.io) (takvimleri ve Exchange, siteler ve SharePoint, OneDrive belgelerden, OneNote, Planlayıcısı çalışma kitaplarından görevlerden defterlerinden listelerinden iletileri gibi Office 365'te erişim toodata sağlar Excel, vb.), kullanıcıların ve grupların Azure AD'den ve diğer veri nesneleri daha fazla Microsoft bulut hizmetlerinden yanı sıra. 

Merhaba izin framework OAuth 2.0 ve çeşitli akışları yerleşik olarak bulunur, yetkilendirme kodu gibi verin ve istemci kimlik bilgileri, genel veya gizli istemcileri kullanarak verin. OAuth 2.0 kullanarak, Azure AD olası toobuild kolaylaştırır istemci uygulamaları, birimi gibi birçok farklı türde bir telefon, tablet, sunucu veya bir web uygulaması ve gerekli toohello kaynaklara erişim.

Merhaba izin framework hakkında daha ayrıntılı bilgi için bkz: [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx), [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md)ve yetkili erişimi tooOffice 365 aracılığıyla alma hakkında bilgi için Microsoft Graph bkz [Microsoft Graph ile uygulama kimlik doğrulaması](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Merhaba onayı deneyimi örneği
Merhaba aşağıdaki adımlarda size hello onayı deneyimi hello uygulama geliştiricisi ve kullanıcı için nasıl çalıştığını gösterir.

1. Web istemci uygulamanızın yapılandırma sayfasında hello Azure portal'ın hello gerekli izinler bölüm hello menülerini kullanarak uygulamanızın gerektirdiği hello izinlerini ayarlayın.
   
    ![İzinleri tooother uygulamalar](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Uygulamanızın izinlerini güncelleştirildi, hello uygulaması çalıştıran ve bir kullanıcı hakkında toouse Merhaba ilk zamanı göz önünde bulundurun. Merhaba uygulaması zaten bir erişim veya yenileme belirteci, hello uygulama ele geçirmiş değil, yeni erişim ve yenileme belirteci toogo tooAzure Reklamın yetkilendirme uç noktası tooobtain kullanılan tooacquire olabilir bir yetkilendirme kodu gerekir.
3. Merhaba kullanıcı zaten kimliği doğrulanmazsa tooAzure AD toosign istenir.
   
    ![Kullanıcı veya yönetici oturum açma tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Merhaba kullanıcı oturum açtıktan sonra Azure AD hello kullanıcı bir onay sayfasına gösterilen toobe gerekip gerekmediğini belirler. Bu belirleme, hello kullanıcı (veya kuruluşun yönetici) zaten hello uygulama izin verilip üzerinde temel alır. İzin zaten verilmiş değil, Azure AD hello kullanıcıdan ve toofunction gereken hello gerekli izinleri görüntüler. hello hello onay iletişim kutusunda görüntülenen izinler kümesi olan hello hello izinlere temsilci hello Azure portal'ın ne seçilmiş aynıdır.
   
    ![Kullanıcı onayı deneyimi](./media/active-directory-integrating-applications/consent.png)
5. Merhaba kullanıcısına izin veren sonra bir kimlik doğrulama kodu kullanılan tooacquire bir erişim belirteci kullanılabilir ve belirtecini yenileme tooyour uygulama döndürülür. Merhaba bu akışı hakkında daha fazla bilgi için bkz: [uygulama tooweb API bölümü web](active-directory-authentication-scenarios.md#web-application-to-web-api) bölümüne [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).

6. Bir yönetici olarak kiracınızda tüm hello kullanıcılar adına tooan uygulamanın temsilci izinleri de onay. Bu, hello onay iletişim hello Kiracı her kullanıcı için görüntülenmesini engeller. Hello bunu yapabilirsiniz [Azure portal](https://portal.azure.com) uygulama sayfanızdan. Hello gelen **ayarları** dikey, uygulamanız için tıklayın **gerekli izinler** üzerinde hello tıklatıp **izinler** düğmesi. 

    ![Açık yönetici onayı için izinler](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Hello kullanarak açık izin verme **izinler** hello erişim belirteci onay değilse, başarısız olur bir onay istemi istendiği düğmesi ADAL.js, kullanarak tek sayfa uygulamaları için (SPA) şu anda gerekli zaten verilmiş.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Bir istemci uygulama tooaccess web API'ları yapılandırma
Bir web/gizli istemci uygulaması toobe mümkün tooparticipate kimlik doğrulaması gerektirir (ve bir erişim belirteci edinmek) bir yetkilendirme grant akışında için sırayla güvenli kimlik bilgileri oluşturmanız gerekir. Azure portal Hello tarafından desteklenen hello varsayılan kimlik doğrulama yöntemidir istemci kimliği + simetrik anahtar. Bu bölümde hello yapılandırma adımları gerekli tooprovide hello gizli anahtar, istemcinin kimlik bilgilerini ele alınacaktır.

Ayrıca, istemci can önce erişimi bir web API açık kaynak uygulama tarafından (IE: Microsoft Graph API), hello izin framework olun hello istemci hello izin verme istenen gereken, temel alınarak hello izinleri alır. Varsayılan olarak, tüm uygulamaları izinleri Azure Active Directory (grafik API'si) ve Azure Hizmet Yönetimi API'si, varsayılan olarak seçilmiş hello Azure AD "etkinleştirme oturum açma ve okuma kullanıcının profilini" iznine sahip seçebilirsiniz. İstemci uygulamanız bir Office 365 Azure AD kiracısında kayıtlı değilse, web API'leri ve SharePoint ve Exchange Online için izinleri de seçilebilir. Aralarından seçim yapabileceğiniz [iki tür izin](active-directory-dev-glossary.md#permissions) hello aşağı açılır menüler sonraki toohello istenen web API'si:

* Uygulama izinleri: Tooaccess hello web API doğrudan kendisini (kullanıcı içerik yok) olarak istemci uygulamanız gerekir. Bu türdeki izinler yönetici izni gerektirir ve ayrıca yerel istemci uygulamaları için kullanılabilir değil.
* Temsilci izinleri: Tooaccess hello web API hello oturum açmış kullanıcı, ancak seçilen hello izinle sınırlı erişimi olan istemci uygulamanız gerekir. Merhaba izni yönetici izni gerektiren olarak yapılandırılmadığı sürece izni bu tür bir kullanıcı tarafından verilebilir. 

> [!NOTE]
> Hello Klasik Azure portalı yaptığınız gibi bir temsilci izni tooan uygulama ekleme otomatik olarak hello Kiracı içindeki toohello kullanıcılar izin vermez. eklenen hello çalışma zamanında izinleri vermiş olması için hello yönetici hello tıklatır sürece hello kullanıcılar yine de el ile onaylaması gerekir **izinler** hello düğmesinden **gerekli izinler** bölümü hello Azure Portalı'nda Hello uygulama sayfası. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>web API tooadd kimlik bilgileri veya izinleri tooaccess
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. tooadd web uygulamanızın kimlik bilgilerini, gizli bir anahtar hello ayarları dikey penceresinde hello "Anahtarlar" bölümünden'ı tıklatın.  
   
   * Anahtarınız için bir açıklama ekleyin ve bir 1 veya 2 yıl süresini seçin. 
   * Merhaba yapılandırma değişiklikleri kaydettikten sonra hello en sağdaki sütun hello anahtar değeri içerir. Emin toocome dönecek çalışma zamanında kimlik doğrulaması sırasında istemci uygulamanızda toothis bölüm ve kopyalama, isabet sonra kaydedin, sizin için olması için kullanın.
5. istemcisinden, tooadd işlemlerinizi tooaccess kaynak API'leri hello ayarları dikey penceresinde hello "Gerekli izinler" bölümünden'ı tıklatın. 
   
   * İlk olarak, hello "Ekle" düğmesini tıklatın.
   * "Bir API seçin" tooselect hello gelen toopick istediğiniz kaynak türünü tıklatın.
   * Kullanılabilir API'ler Hello listesini gözden geçirmek veya hello arama kutusu tooselect uygulamalardan web API'si ortaya hello kullanılabilir kaynak dizininizde kullanın. İlgilendiğiniz, ardından tıklatın hello kaynağa tıklayın **seçin**.
   * Seçildikten sonra toohello taşıyabilirsiniz **Select izinleri** seçebileceğiniz hello "uygulama izinlerini" ve "İzinlere temsilci" uygulamanız için menüsünde.
   
6. Tamamlandığında, hello tıklatın **Bitti** düğmesi.

> [!NOTE]
> Tıklatmak hello **Bitti** düğmesi dizininize uygulamanızda hello izinlerini tabanlı yapılandırdığınız tooother uygulamaları için hello izinleri de otomatik olarak ayarlar.  Merhaba uygulamayı bakarak bu uygulama izinlerini görüntüleyebilirsiniz **ayarları** dikey.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Bir kaynak uygulama tooexpose web API'ları yapılandırma
Web API'si geliştirmek ve erişim göstererek kullanılabilir tooclient uygulamaları hale [kapsamları](active-directory-dev-glossary.md#scopes) ve [rolleri](active-directory-dev-glossary.md#roles). Yalnızca diğer Microsoft web API'leri, hello grafik API'si gibi hello ve Office 365 API'leri hello gibi bir doğru yapılandırılmış web API kullanılabilir hale getirilir. Erişim kapsamları ve rolleri aracılığıyla sunulur, [uygulama bildirimi](active-directory-dev-glossary.md#application-manifest), uygulamanızın kimlik yapılandırması temsil eden bir JSON dosyası olduğu.  

bölümden hello nasıl tooexpose erişim, hello kaynak uygulamanın bildirimi değiştirerek kapsamlarını gösterir.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Erişim kapsamları tooyour kaynak uygulama ekleme
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. Tıklatın **bildirim** düzenleyicisinden hello uygulama sayfası tooopen hello satır içi bildirim. 
5. JSON parçacığı aşağıdaki hello düğümle Değiştir "oauth2Permissions". Bu kod parçacığında nasıl erişim tooa kaynak türü "bir istemci uygulaması kaynak sahibi toogive sağlayan kullanıcı kimliğine bürünme özelliğini", bilinen bir kapsam tooexpose temsilci bir örnektir. Kendi uygulamanız için hello metin ve değerleri değiştirdiğinizden emin olun:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    Merhaba kimliği değeri kullanarak oluşturduğunuz yeni oluşturulan bir GUID olmalıdır bir [GUID oluşturma aracı](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) veya program aracılığıyla. Merhaba web API'si tarafından kullanıma sunulan hello izni için benzersiz bir tanımlayıcı temsil eder. İstemci uygun şekilde yapılandırıldıktan sonra web API toorequest erişim tooyour web API ve çağrıları Merhaba, bu durumda user_impersonation hello kapsamı (scp) talep kümesi toohello değer yukarıdaki sahip bir OAuth 2.0 JWT belirteci sunacaktır.
   
   > [!NOTE]
   > Ek kapsamlar daha sonra gerektikçe getirebilir. Web API çeşitli farklı işlevler ile ilişkili birden çok kapsam doğurabilir göz önünde bulundurun. Şimdi erişim toohello hello kapsamı (scp) kullanarak web API'si talep alınan hello OAuth 2.0 JWT belirteci kontrol edebilirsiniz.
   > 
   > 
6. Tıklatın **kaydetmek** toosave hello bildirimi. API web dizininizde diğer uygulamalar tarafından kullanılan toobe yapılandırılmış.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>dizininizde gösterilen tooother uygulamaları tooverify hello web API'si olan
1. Merhaba üst menüsünde **uygulama kayıtlar**seçin hello istenen istemci uygulaması tooconfigure erişim toohello web API istediğiniz ve toohello ayarlar dikey gidin.
2. Merhaba gelen **gerekli izinler** bölümünde, yalnızca bir izin için kullanıma sunulan hello web API seçin. Merhaba izinlere temsilci açılan menüsünden hello yeni izni seçin.

![Yapılacaklar listesi izinleri gösterilir](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Merhaba uygulama bildirimi hakkında daha fazla bilgi
Merhaba uygulama bildirimi, aslında biz ele alınan hello API erişim kapsamları dahil olmak üzere Azure AD uygulama kimliği yapılandırma tüm özniteliklerini tanımlayan hello uygulama varlığı güncelleştirmek için bir mekanizma olarak görev yapar. Merhaba hello uygulama varlığı hakkında daha fazla bilgi için lütfen bkz [Graph API uygulaması varlık belgelerine](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). İçinde hello uygulama varlık kullanılan üyeler toospecify izinleri tam başvuru bilgileri bulacaksınız:  

* bir koleksiyonu hello appRoles üye, [uygulama rolü](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) kullanılan toodefine hello olabilir varlıklar **uygulama izinleri** web API'si için  
* bir koleksiyonu hello oauth2Permissions üye, [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) kullanılan toodefine hello olabilir varlıklar **izinlere temsilci** web API'si için

Uygulama hakkında daha fazla bilgi için bildirim kavramları genel olarak, çok başvurun[anlama hello Azure Active Directory Uygulama bildirimini](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Hello Azure AD grafik ve Office 365 Microsoft Graph API aracılığıyla erişme  
Belirtilen önceki, ayrıca tooexposing/erişimi API'leri kendi kaynak uygulaması, istemci uygulaması tooaccess Microsoft kaynaklar tarafından kullanıma sunulan API'leri güncelleştirebilirsiniz.  "Microsoft Graph" Merhaba listesinde izinleri tooother uygulamalar olarak adlandırılır, kullanılabilir Microsoft Graph API veya Azure AD ile kayıtlı olan tüm uygulamaları hello. Office 365 tarafından sağlanan Azure AD kiracısı istemci uygulamanızı kaydediyorsanız hello Microsoft Graph API toovarious Office 365 kaynaklar tarafından kullanıma sunulan hello izinleri de erişebilirsiniz.

Microsoft Graph API'si tarafından sunulan erişim kapsamları üzerinde tam hakkında bilgi için lütfen bkz hello [izin kapsamları | Microsoft Graph API kavramları](https://graph.microsoft.io/docs/authorization/permission_scopes) makalesi.

> [!NOTE]
> Tooa geçerli sınırlama, yerel istemci uygulamaları hello "kuruluşunuzun dizinine erişim" izni kullanırsanız hello Azure AD Graph API yalnızca çağırabilir.  Bu kısıtlama, web uygulamaları için geçerli değil.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Çok kiracılı uygulamaları yapılandırma
Bir uygulama tooAzure AD eklerken, yalnızca kuruluşunuzdaki kullanıcılar tarafından erişilen, uygulama toobe isteyebilirsiniz. Alternatif olarak, dış kuruluşlar bulunan kullanıcılar tarafından erişilen, uygulama toobe isteyebilirsiniz. Bu iki uygulama türleri tek bir kiracı ve çok kiracılı uygulamalar olarak adlandırılır. Tek bir kiracı uygulama toomake hello yapılandırmasını değiştirmek, bu bölümde, aşağıda anlatılmaktadır bir çok kiracılı uygulama.

Tek bir kiracı ve çok kiracılı uygulama arasında önemli toonote hello farklılıkları şöyledir:  

* Tek kiracılı uygulama bir kuruluştaki kullanıma yöneliktir. Bunlar genellikle Kurumsal geliştirici tarafından yazılan bir satır iş kolu (LoB) uygulaması yayımlanır. Tek kiracılı uygulama, yalnızca bir dizindeki kullanıcı tarafından erişilen toobe gerekir ve bunun sonucunda, yalnızca bir dizinde sağlanan toobe gerekir.
* Birçok kuruluşta kullanılmak için çok kiracılı uygulama. Genellikle bir bağımsız yazılım satıcısı (ISV) tarafından yazılmış bir hizmet olarak yazılım (SaaS) web uygulaması oldukları. Çok kiracılı uygulamalara gereksinim kullanıcı veya yönetici onayı tooregister gerektiren burada kullanılacakları, her dizin için sağlanan toobe bunları hello Azure AD onay framework desteklenir. Merhaba kaynak sahibinin cihazda yüklü olan gibi tüm yerel istemci uygulamalar varsayılan olarak çok kiracılı olduğuna dikkat edin. Merhaba hello daha fazla ayrıntı için yukarıda onayı Framework bölüm genel bakış hello izin Framework'te bakın.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Dış kullanıcılar toogrant uygulama erişim tootheir kaynaklarınızı etkinleştirme
Kuruluşunuz dışında toomake kullanılabilir tooyour müşterileri veya ortakları istediğiniz bir uygulama yazıyorsanız, tooupdate hello uygulama hello Azure portal tanımında gerekir.

> [!NOTE]
> Çok kiracılı etkinleştirirken, uygulamanızın uygulama kimliği URI'si doğrulanmış bir etki alanına ait olduğundan emin olmalısınız. Ayrıca, hello dönüş URL'si https:// ile başlamalıdır. Daha fazla bilgi için bkz: [uygulama ve hizmet sorumlusu nesneleri](active-directory-application-objects.md).
> 
> 

Dış kullanıcılar için tooenable erişim tooyour uygulaması: 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. Hello ayarları dikey penceresinden tıklayın **özellikleri** ve Çevir hello **çoklu kiralanan** çok geçiş**Evet**.

Yukarıdaki, kullanıcılar ve Yöneticiler, diğer kuruluşların değiştirmek hello yaptıktan sonra mümkün toogrant uygulama erişim tootheir dizininize ve diğer verileri olacaktır.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Çalışma zamanında Hello Azure AD onay framework tetikleme
toouse hello izin framework, çok kiracılı istemci uygulamaları, OAuth 2.0 kullanan yetkilendirme istemeniz gerekir. [Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) olan nasıl bir web uygulaması, yerel uygulama veya sunucu/arka plan programı uygulama isteklerini yetkilendirme kodları ve erişim belirteçleri toocall kullanılabilir tooshow web API'leri.

Web uygulamanız da kullanıcılar için bir kayıt deneyimi sunabilir. Kayıt bir deneyim sunmak, o hello kullanıcı düğmesi kaydolma yeniden yönlendirme hello tarayıcı toohello Azure AD OAuth2.0 uç nokta veya Openıd Connect kullanıcı bilgisi uç noktasına yetkilendirecek tıklayın beklenir. Bu uç noktalar hello id_token inceleyerek hello uygulama tooget hello yeni kullanıcı bilgilerini verin. Merhaba kayıt aşaması, hello kullanıcıya bir onay istemi benzer toohello hello hello onayı Framework bölüm genel bakış yukarıda gösterilenle sunulur.

Alternatif olarak, web uygulamanızı "Şirketim oturum" Yöneticilerin çok sağlayan bir deneyimi sunabilir. Bu deneyim ayrıca hello kullanıcı toohello Azure AD OAuth yeniden yönlendirme 2.0 kimlik doğrulama uç noktası. Bu durumda, bir istem geçirdiğiniz admin_consent = parametresi toohello burada Merhaba yönetici vermek kuruluşu adına izin uç nokta tooforce hello yönetici onayı deneyimi, yetkilendirin. Toohello genel Yönetici rolüne ait bir hesap ile kimliğini doğrulayan bir kullanıcıya izin verebilirsiniz; diğer hata iletisi alırsınız. Başarılı onay üzerinde hello yanıt admin_consent içerecek = true. Bir erişim belirteci redeeming, bir hello kuruluşunda bilgileri sağlarız id_token ve uygulamanız için kaydolan Merhaba yönetici alırsınız.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>OAuth etkinleştirme 2.0 örtük tek sayfa uygulamaları için verme
Tek sayfa uygulamanın (SPAs), genellikle, iş mantığını hello uygulamanın web API'si arka uç tooperform çağırır hello tarayıcıda çalışan JavaScript ağır ön uç ile yapılandırılmıştır. Azure AD içinde barındırılan SPAs için Azure AD ile OAuth 2.0 örtük verme tooauthenticate hello kullanıcı kullanın ve kullanabileceğiniz bir belirteç elde toosecure çağırır hello uygulamanın JavaScript istemci tooits geri son web API. Merhaba kullanıcı izin verildi sonra bu aynı kimlik doğrulama protokolü kullanılan tooobtain belirteçleri toosecure çağrıları hello istemci hello uygulama için yapılandırılan diğer web API kaynaklar arasında olabilir. Merhaba örtük yetkilendirme verme ve karar Uygulama senaryonuz için uygun olup olmadığını Yardım hakkında daha fazla toolearn bkz [anlama hello OAuth2 örtük izin akışı Azure Active Directory'de ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Varsayılan olarak, OAuth 2.0 örtük Grant uygulamalar için devre dışıdır. Uygulamanız için OAuth 2.0 örtük verme ayarı hello tarafından etkinleştirebilirsiniz `oauth2AllowImplicitFlow` değeri kendi [uygulama bildirimi](active-directory-application-manifest.md), uygulamanızın kimlik yapılandırması temsil eden bir JSON dosyası olduğu.

#### <a name="tooenable-oauth-20-implicit-grant"></a>tooenable OAuth 2.0 örtük verin
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. Merhaba uygulama sayfasından tıklatın **bildirim** tooopen hello satır içi bildirim Düzenleyici.
   Bulun ve hello "oauth2AllowImplicitFlow" değerini "true" çok ayarlayın. Varsayılan olarak "false" şeklindedir.
   
    `"oauth2AllowImplicitFlow": true,`
5. Güncelleştirilmiş hello bildirimini kaydedin. Kaydedildikten sonra API web toouse OAuth 2.0 örtük verme tooauthenticate kullanıcıların artık yapılandırılmış.


## <a name="removing-an-application"></a>Bir uygulamayı kaldırma
Bu bölümde, nasıl bir uygulama, Azure AD'den tooremove Kiracı açıklanmaktadır.

### <a name="removing-an-application-authored-by-your-organization"></a>Kuruluşunuz tarafından yazılan bir uygulamayı kaldırma
Bu, "Şirketimin sahip olduğu uygulamalar" Merhaba filtre hello ana "Uygulamaları" sayfasında altında Azure AD kiracınız için Göster hello uygulamalarıdır. Teknik terimleriyle bunlar hello Klasik Azure Portalı aracılığıyla el ile ya da program aracılığıyla PowerShell aracılığıyla kaydedilmiş uygulamaları veya grafik API'si hello. Daha açık belirtmek gerekirse, bunlar hem uygulama ve hizmet asıl nesne tarafından kiracınızda gösterilir. Bkz: [uygulama ve hizmet sorumlusu nesneleri](active-directory-application-objects.md) daha fazla bilgi için.

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove dizininizden tek kiracılı uygulama
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. Merhaba uygulama sayfasından tıklatın **silmek**.
5. Tıklatın **Evet** hello onay iletisi.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove dizininizden çok kiracılı uygulama
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba üst menüsünde, **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve tooconfigure istediğiniz hello uygulamayı tıklatın. Bu toohello uygulamanın hızlı başlangıç sayfasını ele yanı Merhaba uygulaması hello ayarları dikey penceresini açın.
4. Merhaba ayarlar dikey penceresinden seçin **özellikleri** ve Çevir hello **çoklu kiralanan** çok geçiş**Hayır**. Bu uygulama toobe tek Kiracı dönüştürür, ancak hello uygulama hala tooit zaten seçtiği bir kuruluş içinde kalır.
5. Tıklatın hello üzerinde **silmek** hello uygulama sayfası düğmesinden.
6. Tıklatın **Evet** hello onay iletisi.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Başka bir kuruluş tarafından yetkili bir çok kiracılı uygulama kaldırma
Bu, özellikle hello hello "Şirketimin sahip olduğu uygulamalar" listesi altında listelenmeyen olanları, Azure AD kiracınızın hello "Uygulamaları Şirketim kullanır" filtre hello ana "uygulamaları" sayfasında altında göster hello uygulamaların bir alt kümesidir. Teknik olarak bu hello onay işlemi sırasında kayıtlı çok kiracılı uygulamalardır. Daha açık belirtmek gerekirse, bunlar yalnızca bir hizmet sorumlusu nesnesi kiracınızda gösterilir. Bkz: [uygulama ve hizmet sorumlusu nesneleri](active-directory-application-objects.md) daha fazla bilgi için.

İçinde tooremove bir çok kiracılı uygulamanın erişim tooyour dizini (izin verilen sonra) sipariş, hello şirket Yöneticisi bir Azure aboneliği tooremove hello Azure portalı üzerinden erişimi olmalıdır. Alternatif olarak, hello şirket Yöneticisi hello kullanabilirsiniz [Azure AD PowerShell cmdlet'leri](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove erişim.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba bkz [tümleşik uygulamalar için markalama yönergeleri](active-directory-branding-guidelines.md) uygulamanız için görsel kılavuz ipuçları için.
* Bir uygulamanın uygulama ve hizmet sorumlusu nesneleri arasındaki ilişki hello hakkında daha fazla bilgi için bkz: [uygulama ve hizmet sorumlusu nesneleri](active-directory-application-objects.md).
* toolearn hello rol hello uygulama bildirim yürütür, hakkında daha fazla bilgi görmek [hello Azure Active Directory Uygulama bildirimini anlama](active-directory-application-manifest.md)
* Merhaba bkz [Azure AD Geliştirici sözlüğü](active-directory-dev-glossary.md) bazı hello çekirdek Azure Active Directory (AD) Geliştirici kavramları tanımları için.
* Merhaba ziyaret [Active Directory Geliştirici Kılavuzu](active-directory-developers-guide.md) tüm geliştirici genel bakış için içerik ilgili.

