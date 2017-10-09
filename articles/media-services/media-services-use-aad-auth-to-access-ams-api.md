---
title: "Azure Active Directory kimlik doğrulaması ile Azure Media Services API aaaAccess | Microsoft Docs"
description: "Kavramlar ve adımlar tootake toouse Azure Active Directory (Azure AD) tooauthenticate erişim toohello hakkında Azure Media Services API öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API
 
Hello Azure Media Services API bir RESTful API'sidir. Bu ortam kaynakları tooperform işlemleri bir REST API kullanarak veya kullanılabilir istemci SDK'ları kullanarak kullanabilirsiniz. Azure Media Services, Microsoft .NET için Media Services istemci SDK sunar. toobe yetkili tooaccess Media Services kaynakları ve hello Media Services API, ilk kimliğinin gerekir. 

Media Services destekler [Azure Active Directory (Azure AD)-tabanlı kimlik doğrulaması](../active-directory/active-directory-whatis.md). Hello Azure medya REST hizmeti gerektirir hello kullanıcı veya hello REST API istekleri yapan uygulamada ya da hello sahip **katkıda bulunan** veya **sahibi** rol tooaccess hello kaynakları. Daha fazla bilgi için bkz: [hello Azure portal'ın rol tabanlı erişim denetimi ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Şu anda, Media Services hello Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler. Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım dışı kalacaktır. Mümkün olan en kısa sürede toohello Azure AD kimlik doğrulama modeli geçirmek öneririz.

Bu belge nasıl tooaccess REST veya .NET API'lerini kullanarak Media Services API hello genel bir bakış sağlar.

## <a name="access-control"></a>Erişim denetimi

Hello Azure medya REST isteği toosucceed için hello arayan kullanıcının katkıda bulunan veya sahibi rolü hello tooaccess çalışıyor Media Services hesabı için olmalıdır.  
Merhaba sahibi rolüne sahip bir kullanıcı medya kaynağı (hesap) erişim toonew kullanıcıları veya uygulamalar verebilirsiniz. Merhaba katkıda bulunan rolü yalnızca hello medya kaynağı erişebilir.
Yetkisiz istekler 401 durum kodu ile başarısız olur. Bu hata kodu görürseniz, kullanıcı hello katkıda bulunan veya hello kullanıcının Media Services hesabı için atanan sahibi rolü olup olmadığını denetleyin. Bu hello Azure portal kontrol edebilirsiniz. Medya hesabınız için arama ve hello ardından **erişim denetimi** sekmesi. 

![Erişim denetimi sekmesi](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Kimlik doğrulama türleri 
 
Azure Media Services ile Azure AD kimlik doğrulaması kullandığınızda, iki kimlik doğrulama seçeneğiniz vardır:

- **Kullanıcı kimlik doğrulaması**. Media Services kaynaklarla hello uygulama toointeract kullanan bir kişi kimlik doğrulaması. Merhaba etkileşimli uygulaması ilk hello kullanıcıdan hello kullanıcının kimlik bilgilerini ister. Bir örnek yetkili kullanıcıların toomonitor kodlama işlemler tarafından kullanılan bir yönetim konsol uygulaması ya da canlı akış. 
- **Hizmet asıl kimlik doğrulaması**. Bir hizmetin kimliğini. Genellikle bu kimlik doğrulama yöntemini kullanan uygulamalar, arka plan programı services, orta katman Hizmetleri veya zamanlanmış işleri çalıştırma uygulamalardır. Web uygulamaları, işlev uygulamalarının, logic apps, API ve mikro örnektir.

### <a name="user-authentication"></a>Kullanıcı kimlik doğrulaması 

Merhaba kullanıcı kimlik doğrulama yöntemini kullanması gereken uygulamalardır Yönetimi'ni veya yerel uygulamalar izleme: mobil uygulamaları, Windows uygulamaları ve konsol uygulamaları. Bu tür çözüm senaryoları aşağıdaki hello hello hizmeti ile insan etkileşimi istediğinizde yararlıdır:

- İzleme Panosu kodlama işleriniz için.
- İzleme Panosu, Canlı akışlar için.
- Masaüstü ve mobil kullanıcılar tooadminister Media Services hesabı kaynaklarında uygulama yönetimi.

> [!NOTE]
> Bu kimlik doğrulama yöntemini tüketiciye yönelik uygulamalar için kullanılmamalıdır. 

Bir yerel uygulamayı ilk Azure AD'den bir erişim belirteci alması ve HTTP isteklerini toohello Media Services REST API yaptığınızda kullanmanız gerekir. Merhaba erişim belirteci toohello istek üstbilgisi ekleyin. 

Aşağıdaki diyagramda hello tipik etkileşimli uygulama kimlik doğrulama akışı gösterir: 

![Yerel uygulamalar diyagramı](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Diyagram önceki hello hello numaraları hello istekleri kronolojik sırada hello akışını temsil eder.

> [!NOTE]
> Merhaba kullanıcı kimlik doğrulama yöntemini kullandığınızda, tüm uygulamalar hello paylaşır aynı (varsayılan) yerel uygulama istemci Kimliğini ve yerel uygulama yeniden yönlendirme URI'si. 

1. Bir kullanıcıdan kimlik bilgilerini ister.
2. İstek şu parametreler hello Azure AD erişim belirteciyle:  

    * Azure AD Kiracı uç noktası.

        Azure portal hello Hello Kiracı bilgi alınabilir. İmlecinizi hello sağ üst köşedeki hello oturum açmış kullanıcı hello adın üzerine yerleştirin.
    * Media Services kaynak URI'si. 

        Bu URI olan hello aynı hello Media Services hesapları için aynı Azure ortamı (örneğin, https://rest.media.azure.net).

    * Media Services (yerel) uygulama istemci kimliği
    * Media Services (yerel) uygulama yeniden yönlendirme URI'si.
    * Kaynak URI'si REST Media Services için.
        
        Merhaba URI hello REST API uç noktası (örneğin, https://test03.restv2.westus.media.azure.net/api/) temsil eder.

    Bu parametreler tooget değerlerini görmek [hello Azure portal tooaccess Azure AD kimlik doğrulama ayarlarını kullanmak](media-services-portal-get-started-with-aad.md) hello kullanıcı kimlik doğrulama seçeneği kullanma.

3. Hello Azure AD erişim belirteci toohello istemci gönderilir.
4. Merhaba istemci hello Azure AD erişim belirteci ile isteği toohello Azure medya REST API gönderir.
5. Merhaba istemci hello veri Media Services'den geri alır.

Merhaba Media Services .NET İstemci SDK'sını kullanarak toouse Azure AD kimlik doğrulama toocommunicate REST ile nasıl istekleri hakkında daha fazla bilgi için bkz: [kullanım Azure AD kimlik doğrulama tooaccess hello .NET ile Media Services API](media-services-dotnet-get-started-with-aad.md). 

Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, 2. adımda açıklanan hello parametrelerini kullanarak bir Azure AD erişim belirteci isteği el ile oluşturmalısınız. Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Hizmet sorumlusu kimlik doğrulaması

Bu kimlik doğrulama yöntemini yaygın olarak kullanan uygulamaları orta katman Hizmetleri ve zamanlanmış işler çalışan uygulamalar şunlardır: web uygulamaları, işlev uygulamalarının, logic apps, API'ler ve mikro hizmetler. Bu kimlik doğrulama yöntemini de bir hizmet hesabı toomanage kaynakları toouse istiyor etkileşimli uygulamalar için uygundur.

Merhaba hizmet asıl kimlik doğrulama yöntemi toobuild tüketici senaryoları kullandığınızda, genellikle hello orta katman (aracılığıyla, bazı API) ve doğrudan mobil veya Masaüstü uygulama kimlik doğrulama ele alınır. 

toouse bu yöntem, Azure AD uygulaması oluşturmasına ve hizmet sorumlusu kendi Kiracı. Merhaba uygulaması oluşturduktan sonra hello uygulamasını katkıda bulunan veya sahibi rol erişim toohello Media Services hesabı verin. Hello Azure portal, Azure CLI kullanarak veya bir PowerShell Betiği ile bunu yapabilirsiniz. Var olan Azure AD uygulaması de kullanabilirsiniz. Kaydet ve Azure AD uygulaması ve hizmet sorumlusu yönetmek [hello Azure portal'ın](media-services-portal-get-started-with-aad.md). Ayrıca kullanarak bunu yapabilirsiniz [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) veya [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Orta katman uygulamalar](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Azure AD uygulaması oluşturduktan sonra ayarlar aşağıdaki hello için değerleri alır. Kimlik doğrulaması için bu değerleri gerekir:

- İstemci kimliği 
- Gizli anahtar 

Şekil önceki hello hello sayılar hello istekleri kronolojik sırada hello akışını temsil eder:
    
1. Orta katman uygulama (web API ya da web uygulaması) şu parametreler hello sahip bir Azure AD erişim belirteci ister:  

    * Azure AD Kiracı uç noktası.

        Azure portal hello Hello Kiracı bilgi alınabilir. İmlecinizi hello sağ üst köşedeki hello oturum açmış kullanıcı hello adın üzerine yerleştirin.
    * Media Services kaynak URI'si. 

        Bu URI olan hello aynı hello bulunan Media Services hesapları için aynı Azure ortamı (örneğin, https://rest.media.azure.net).

    * Kaynak URI'si REST Media Services için.

        Merhaba URI hello REST API uç noktası (örneğin, https://test03.restv2.westus.media.azure.net/api/) temsil eder.

    * Azure AD uygulama değerleri: Merhaba istemci Kimliğini ve istemci gizli anahtarı.
    
    Bu parametreler tooget değerlerini görmek [hello Azure portal tooaccess Azure AD kimlik doğrulama ayarlarını kullanmak](media-services-portal-get-started-with-aad.md) hello hizmet asıl kimlik doğrulama seçeneğini kullanarak.

2. Hello Azure AD erişim belirteci toohello orta katman gönderilir.
4. Merhaba orta katman hello Azure AD belirteci ile isteği toohello Azure medya REST API gönderir.
5. Merhaba orta katman hello veri Media Services'den geri alır.

Merhaba Media Services .NET İstemci SDK'sını kullanarak toouse Azure AD kimlik doğrulama toocommunicate REST ile nasıl istekleri hakkında daha fazla bilgi için bkz: [kullanım Azure AD kimlik doğrulama tooaccess .NET ile Azure Media Services API](media-services-dotnet-get-started-with-aad.md). 

Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, el ile bir Azure AD belirteç isteği 1. adımda açıklanan parametreleri kullanarak oluşturmanız gerekir. Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Sorun giderme

Özel durum: "Merhaba uzak sunucu bir hata döndürdü: (401) yetkisiz."

Çözüm: hello Media Services REST isteği toosucceed için hello arayan kullanıcı hello tooaccess çalışıyor Media Services hesabı katkıda bulunan veya sahibi rolünde olması gerekir. Daha fazla bilgi için bkz: Merhaba [erişim denetimi](media-services-use-aad-auth-to-access-ams-api.md#access-control) bölümü.

## <a name="resources"></a>Kaynaklar

aşağıdaki makaleleri hello Azure AD kimlik doğrulaması kavramlarını genel bakış şunlardır: 

- [Azure AD tarafından ele alınan kimlik doğrulama senaryoları](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Ekleme, güncelleştirme veya Azure AD'de uygulama kaldırma](../active-directory/develop/active-directory-integrating-applications.md)
- [Yapılandırma ve rol tabanlı erişim denetimi PowerShell kullanarak yönetme](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Sonraki adımlar

* Hello Azure portal çok kullanmak[Azure AD kimlik doğrulama tooconsume Azure Media Services API erişim](media-services-portal-get-started-with-aad.md).
* Azure AD kimlik doğrulaması çok kullanmak[.NET ile Azure Media Services API erişim](media-services-dotnet-get-started-with-aad.md).

