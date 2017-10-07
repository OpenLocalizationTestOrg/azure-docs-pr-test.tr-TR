---
title: "aaaExporting bir Azure barındırılan API tooPowerApps ve Microsoft Flow | Microsoft Docs"
description: "Uygulama hizmeti tooPowerApps ve Microsoft Flow tooexpose bir API nasıl barındırılan genel bakış"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Bir Azure barındırılan API tooPowerApps ve Microsoft Flow dışa aktarma

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Özel bağlayıcılar PowerApps ve Microsoft Flow için oluşturma

[PowerApps](https://powerapps.com) oluşturma ve tooyour veri bağlanan ve platformlar arası çalışması özel iş uygulamaları kullanmak için bir hizmettir. [Microsoft Flow](https://flow.microsoft.com) kolay tooautomate iş akışları ve sık kullanılan uygulamalar ve hizmetler arasındaki iş süreçlerini kolaylaştırır. PowerApps ve Microsoft Flow yerleşik bağlayıcılar toodata kaynakları Office 365, Dynamics 365, Salesforce ve daha fazlası gibi çeşitli gelir. Ancak, kullanıcıların toobe mümkün tooleverage veri kaynakları ve API'leri kuruluşu tarafından oluşturulması gerekir.

Benzer şekilde, daha fazla geniş çapta içinde hello kuruluş toomake kendi API kullanılabilir tooPowerApps ve Microsoft Flow kullanıcılar isteyebilirsiniz kendi API tooexpose istediğiniz geliştiriciler. Bu konuda nasıl yerleşik Azure uygulama hizmeti ya da Azure işlevleri tooPowerApps ve Microsoft Flow tooexpose bir API gösterir. [Azure uygulama hizmeti](https://azure.microsoft.com/services/app-service/) geliştiriciler tooquickly ve kolayca yapı Kurumsal düzeyde web, mobil ve API uygulamaları sağlayan bir hizmet olarak platform bir tekliftir. [Azure işlevleri](https://azure.microsoft.com/services/functions/) tooother bölümlerini sistem ve talebe göre ölçeklendirin tepki gösterebilmesi tooquickly yazar kod sağlayan bir olay tabanlı sunucusuz işlem çözümüdür.

Bu hizmetler hakkında daha fazla toolearn bakın:
- [PowerApps öğrenme Destekli](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Microsoft Akış öğrenme Destekli](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [App Service nedir?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Azure işlevleri nedir](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>API tanımı paylaşımı

API, kullanarak genellikle açıklanmıştır bir [OpenAPI belge](https://www.openapis.org/) (bazen "Swagger" Belge tooas denir). Bu tüm hello hangi işlemleri kullanılabilir ve hello verileri nasıl yapılandırılacağını hakkında bilgi içerir. PowerApps ve Microsoft Flow özel bağlayıcıları herhangi OpenAPI 2.0 belgeniz için oluşturabilirsiniz. Özel bir bağlayıcı oluşturulduktan sonra tam olarak hello kullanılabilmesi için aşağıdakilerden birini aynı şekilde yerleşik bağlayıcılar hello ve bir uygulamaya hızlı bir şekilde tümleştirilebilir.

Azure uygulama hizmeti ve Azure işlevleri [yerleşik destek](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) oluşturma, barındırma ve OpenAPI belge yönetme. Sipariş toocreate web, mobil için özel bir bağlayıcı, API veya işlev uygulaması, PowerApps ve akış hello tanımı bir kopyasını verilen toobe gerekir.

> [!NOTE]
> Merhaba API tanımı bir kopyasını kullanıldığından, PowerApps ve Microsoft Flow hemen güncelleştirmeleri veya en son değişiklikleri toohello uygulama hakkında bilmez. Merhaba API yeni bir sürümü kullanılabilir duruma getirildiyse, şu adımları hello yeni sürümü için tekrarlanmalıdır. 

tooprovide PowerApps ve Microsoft Flow barındırılan hello API tanımı, uygulamanız için şu adımları izleyin:

1. Açık hello [Azure Portal](https://portal.azure.com) ve tooyour uygulama hizmeti veya Azure işlevleri uygulamasına gidin.

    Azure uygulama hizmeti kullanıyorsanız, seçin **API tanımı** hello ayarları listesinden. 
    
    Azure işlevleri kullanıyorsanız, işlevi uygulamanızı seçin ve ardından **Platform özellikleri**ve ardından **API tanımı**. Ayrıca tooopen hello seçebilir **API tanımı (Önizleme)** yerine sekmesinde.

2. API tanımı sağladıysanız göreceğiniz bir **verme tooPowerApps + Microsoft Flow** düğmesi. Bu düğme toobegin hello dışa aktarma işlemi'ı tıklatın.

3. Select hello **Export modunu**. Bu toofollow toocreate bağlayıcı gerekir hello adımları belirler. Uygulama hizmeti API tanımıyla PowerApps ve Microsoft Flow sağlamak için iki seçenek sunar:

    **Express** hello Azure portal hello özel bir bağlayıcı içinde oluşturmanızı sağlar. Oturum açma hello geçerli kullanıcının izni toocreate bağlayıcılar hello hedef ortamda sahip gerektiriyor. Bu gereksinimi karşılarsınız, önerilen yaklaşımı hello budur. Bu mod kullanıyorsanız, hello izleyin [Express verme](#express) aşağıdaki yönergeleri.

    **El ile** hello PowerApps veya Microsoft Flow portallarını kullanılarak alınabilir, hello API tanımı bir kopyasını dışa aktardığınız sağlar. Hello Azure kullanıcı ve hello kullanıcı izni toocreate Bağlayıcılarla kişiler farklı olduğunda veya hello bağlayıcı başka bir kiracı içinde oluşturulan toobe gerekirse önerilen yaklaşımı hello budur. Bu mod kullanıyorsanız, hello izleyin [el ile dışarı ve içeri aktarma](#manual) aşağıdaki yönergeleri.

<a name="express"></a>
## <a name="express-export"></a>Express dışarı aktarma

Bu bölümde, yeni özel bir bağlayıcı hello Azure portalı içinde oluşturur. Oturum açmanız gerekir hello Kiracı toowhich tooexport istiyor ve özel bir bağlayıcı izni toocreate hello hedef ortamda olması gerekir.

1. Toocreate hello bağlayıcı istediğiniz hello ortamını seçin. Ardından, özel bağlayıcı için bir ad sağlayın.

2. API tanımı tüm güvenlik tanımlarını içeriyorsa, bunlar #2. adımda çağrılacağı. Gerekirse, hello güvenlik toogrant kullanıcılar tooyour API'sine erişim yapılandırma ayrıntıları sağlar. Daha fazla bilgi için bkz: [kimlik doğrulaması](#auth) aşağıda. 

3. Tıklatın **Tamam** toocreate özel Bağlayıcınızı.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>El ile dışarı ve içeri aktarma

Sipariş toocreate web, mobil için özel bir bağlayıcı, API veya işlev uygulaması iki adımı gerekecektir:

1. [Uygulama hizmeti ya da Azure işlevleri Hello API tanımı alınıyor](#export)
2. [PowerApps ve Microsoft Flow Hello API tanımı içeri aktarma](#import)

Verili bir kullanıcı her iki Eylemler izni tooperform olmayabilir gibi iki adımları, kuruluş içindeki ayrı kişiler tarafından gerçekleştirilen toobe gerekir mümkündür. Bu durumda, katkıda bulunan erişim toohello uygulama hizmeti veya Azure işlevleri uygulaması olan bir geliştirici tooobtain hello API tanımı (tek bir JSON dosyası) veya bir bağlantı tooit gerekir. Bunlar tanımı tooa PowerApps ya da Microsoft Flow sahibi tooprovide gerekir. Sahibi hello meta veri toocreate hello özel bağlayıcısını kullanabilirsiniz.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Uygulama hizmeti ya da Azure işlevleri Hello API tanımı alınıyor

Bu bölümde, App Service API, daha sonra hello PowerApps ya da Microsoft Flow portalda kullanılan toobe hello API tanımı verecektir.

1. Tooeither seçebilirsiniz **karşıdan hello API tanımı** veya **bir bağlantı**. Hangisi seçin, hello sonuç hello sonraki bölümde sağlanacaktır. Bu seçeneklerden birini seçin ve hello yönergeleri izleyin.
 
2. API tanımı tüm güvenlik tanımlarını içeriyorsa, bunlar #2. adımda çağrılacağı. İçeri aktarma sırasında PowerApps ve Microsoft Flow bunlar algılar ve güvenlik bilgilerini ister. Merhaba kimlik bilgilerini ilgili tooeach tanımını hello sonraki bölümde toplayın. Daha fazla bilgi için bkz: [kimlik doğrulaması](#auth) aşağıda. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>PowerApps ve Microsoft Flow Hello API tanımı içeri aktarma

Bu bölümde, PowerApps ve Microsoft daha önce edindiğiniz hello API tanımı kullanılarak Flow özel bir bağlayıcı oluşturur. Özel bağlayıcıları yalnızca bir kez tooimport hello tanımı gerekir böylece hello iki hizmetleri arasında paylaşılır. Özel bağlayıcılar hakkında daha fazla bilgi için bkz: [kaydetmek ve PowerApps içinde özel bağlayıcılarını kullanmak] ve [kaydetmek ve Microsoft Flow özel bağlayıcılarını kullanmak].

1. Açık hello [Powerapps web portalı](https://web.powerapps.com) veya hello [Microsoft Flow web portalı](https://flow.microsoft.com/)ve oturum açın. 

2. Merhaba tıklatın **ayarları** hello sağ üst köşesinde, başlangıç sayfası ve Seç düğmesini (Merhaba dişli simgesi) **özel Bağlayıcılar**. 

3. Tıklatın **özel bağlayıcı oluşturma**.

4. Merhaba üzerinde **genel** sekmesinde, API için bir ad ve hello OpenAPI tanımı karşıya yükleme veya hello meta veri URL'sini yapıştırın. Tıklatın **devam**.

4. Merhaba üzerinde **güvenlik** sekmesinde istendiğinde tooprovide kimlik doğrulama ayrıntıları, varsa, hello önceki bölümde edindiğiniz hello değerleri girin. Aksi durumda, toohello sonraki adıma geçin.

5. Merhaba üzerinde **tanımları** sekmesinde OpenAPI dosyasında tanımlanan tüm hello işlemleri otomatik olarak doldurulur. Tüm gerekli işlemleri tanımlanmışsa, toohello sonraki adıma gidebilirsiniz. Değilse, ekleme ve burada işlemleri değiştirme.

6. Tıklatın **Bağlayıcısı oluşturma**. Tootest API çağrıları istiyorsanız toohello sonraki adıma gidin.

7. Merhaba üzerinde **Test** sekmesinde, bir bağlantı oluşturmak, bir işlemi tootest seçin ve hello işlem için gereken herhangi bir veri girin.

8. Tıklatın **Test işlemi**.


<a name="auth"></a>
## <a name="authentication"></a>Kimlik Doğrulaması

PowerApps ve Microsoft Flow kullanıcıların özel bağlayıcının kullanılan toolog olabilen kimlik sağlayıcıları koleksiyonu yerel olarak destekler. API'nizi kimlik doğrulaması gerektiriyorsa, olarak yakalanan emin olun bir _güvenlik tanımı_ OpenAPI belgenize. Dışa aktarma sırasında bir Microsoft Flow tooperform oturum açma eylemleri PowerApps izin tooprovide yapılandırma değerlerini gerekir.

Bu bölüm hello hızlı akış tarafından desteklenen hello kimlik doğrulaması türlerini kapsar: API anahtarı, Azure Active Directory ve genel OAuth 2.0. Sağlayıcılar ve her gerektirir hello kimlik tam listesi için bkz: [kaydetmek ve PowerApps içinde özel bağlayıcılarını kullanmak] ve [kaydetmek ve Microsoft Flow özel bağlayıcılarını kullanmak].

### <a name="api-key"></a>API anahtarı
Bu güvenlik düzeni kullanıldığında, bir bağlantı oluşturduğunuzda Bağlayıcınızı hello kullanıcılarının istendiğinde tooprovide hello anahtar olacaktır. Hangi anahtar gerekli bildiğiniz bir API anahtar adı toohelp sağlayabilir. Azure işlevleri için bu hello işlev uygulaması içinde çeşitli işlevleri kapsayan hello konak anahtarlarından birini genellikle olacaktır.

### <a name="azure-active-directory"></a>Azure Active Directory
AAD oturum açma gerektiren özel bir bağlayıcıyı yapılandırırken iki AAD uygulama kayıtlar gereklidir: bir toomodel hello arka uç API'si ve PowerApps ve akış adet toomodel hello Bağlayıcısı.

API'nizi hello ilk kaydı ile yapılandırılmış toowork olmalıdır ve bu zaten hello kullandıysanız dikkate [App Service kimlik doğrulama/yetkilendirme](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) özelliği.

Ele hello adımları kullanarak hello ikinci kayıt hello Bağlayıcısı oluşturma toomanually olacaktır [bir AAD uygulaması ekleme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Merhaba kaydedilmesi temsilci toohave erişim tooyour API ve bir yanıt URL'si gerekiyor `https://msmanaged-na.consent.azure-apim.net/redirect`. Lütfen bakın [Bu örnek](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) API'nizi hello Azure Resource Manager için daha fazla ayrıntı için değiştirme.

yapılandırma değerlerini aşağıdaki hello gereklidir:
- **İstemci kimliği** -AAD kayıt Bağlayıcınızı istemci kimliği hello
- **İstemci parolası** -AAD kayıt bağlayıcının hello istemci parolası
- **Oturum açma URL'si** - hello AAD ana URL. Ortak Azure'da, bu genellikle olacaktır `https://login.windows.net`.
- **Kiracı kimliği** -hello Kiracı toobe hello oturum açma için kullanılan kimliği hello. Bu "ortak" veya hangi hello Bağlayıcısı oluşturuldu hello Kiracı kimliği hello gerekir.
- **Kaynak URL** -API arka uç AAD kaydınızı kaynak URL'sini hello

> [!IMPORTANT]
> Başka bir kişi hello API tanımı PowerApps ve Microsoft Flow halinde hello el ile akışının bir parçası içe aktarıyorsanız, tooprovide gerekir hello istemci kimliği ve istemci parolası ile bunları **hello bağlayıcı kayıt**yanı Kaynak URL Hello API'nizi. Bu gizli anahtarları güvenli bir şekilde yönetildiğinden emin olun. **Merhaba API kendisini Hello güvenlik kimlik bilgileri paylaşmaz.**

### <a name="generic-oauth-20"></a>Genel OAuth 2.0
Merhaba genel OAuth 2.0 desteği herhangi OAuth 2.0 sağlayıcısı ile toointegrate sağlar. Bu, toobring yerel olarak desteklenmeyen içinde özel sağlayıcı sağlar.

yapılandırma değerlerini aşağıdaki hello gereklidir:
- **İstemci kimliği** -hello OAuth 2.0 istemci kimliği
- **İstemci parolası** -hello OAuth 2.0 istemci parolası
- **Yetkilendirme URL'si** -OAuth 2.0 yetkilendirme URL'si hello
- **Simge URL** -OAuth 2.0 belirteç URL hello
- **URL yenileme** -OAuth 2.0 yenileme URL hello



[kaydetmek ve PowerApps içinde özel bağlayıcılarını kullanmak]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[kaydetmek ve Microsoft Flow özel bağlayıcılarını kullanmak]: https://flow.microsoft.com/documentation/register-custom-api/
