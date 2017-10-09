---
title: "Azure AD uygulama proxy'si için kimlik doğrulaması ile PingAccess olarak aaaHeader tabanlı | Microsoft Docs"
description: "PingAccess ve uygulama Proxy toosupport üstbilgi tabanlı kimlik doğrulaması ile uygulama yayımlama."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Uygulama proxy'si ve PingAccess ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması

Azure Active Directory Uygulama proxy'si ve PingAccess tooprovide Azure Active Directory erişimi tooeven müşterilerle birlikte daha fazla uygulama ortaklık. PingAccess genişletir hello [varolan uygulama proxy'si teklifleri](active-directory-application-proxy-get-started.md) üstbilgileri kimlik doğrulaması için kullanmak tooinclude tek oturum açma erişimini tooapplications.

## <a name="what-is-pingaccess-for-azure-ad"></a>Azure AD için PingAccess nedir?

Azure Active Directory için PingAccess toogive kullanıcıların erişim sağlayan PingAccess ve kimlik doğrulaması için üstbilgiler kullanan tek oturum açma tooapplications bir tekliftir. Uygulama proxy'si kullanarak Azure AD tooauthenticate erişimini ve hello bağlayıcı hizmeti trafiğinin geçirme gibi diğer, bu uygulamalar değerlendirir. PingAccess önünde hello uygulamaları bulunur ve Merhaba uygulaması okuyamamasını hello biçiminde hello kimlik doğrulaması alması hello erişim belirteci Azure AD'den bir üstbilgisine çevirir.

Şirket uygulamalarınızı toouse içinde imzaladığınızda kullanıcılarınız farklı bir şey fark olmaz. Bunlar hala herhangi bir yerden herhangi bir cihazda çalışabilirsiniz. 

Kendi kimlik doğrulama türü ne olursa olsun uzak trafik tooall uygulamaları Hello uygulama proxy'si bağlayıcılar doğrudan olduğundan, bunlar tooload Bakiye devam edeceğiz otomatik olarak, de.

## <a name="how-do-i-get-access"></a>Erişim nasıl sağlarım?

Bu senaryo, Azure Active Directory PingAccess arasındaki iş ortaklığına aracılığıyla sunulur olduğundan, her iki hizmet için lisans gerekir. Ancak, Azure Active Directory Premium abonelikleri too20 uygulamalarını kapsamaktadır temel bir PingAccess lisans içerir. 20'den fazla üstbilgi tabanlı uygulamalar toopublish gerekiyorsa, PingAccess ek lisans satın alabilirsiniz. 

Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Azure'da uygulamanızı yayımlama

Bu makale, bir uygulamanın bu senaryo için hello ile ilk kez yayımlama kişiler için tasarlanmıştır. Tooget hem uygulama hem de PingAccess, ayrıca toohello yayımlama adımları çalışmaya nasıl aracılığıyla size yardımcı olacaktır. Her iki hizmet zaten yapılandırdıktan ancak adımları yayımlama hello bir Yenileyici istiyorsanız hello Bağlayıcısı yükleme atlayın ve çok taşıma[, uygulama tooAzure AD uygulama proxy'si ile ekleme](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Bu senaryo Azure AD arasında ortaklık olduğundan ve PingAccess, bazı hello yönergeleri mevcut Ping kimlik site hello üzerinde.

### <a name="install-an-application-proxy-connector"></a>Bir uygulama ara sunucusu Bağlayıcısı'nı yüklemek

Zaten uygulama Proxy etkin olması ve yüklü bir bağlayıcı varsa, bu bölüm atlayın ve çok taşıma[, uygulama tooAzure AD uygulama proxy'si ile ekleme](#add-your-app-to-azure-ad-with-application-proxy).

Merhaba uygulama ara sunucusu Bağlayıcısı olduğu bir Windows Server, uzak çalışanlar tooyour hello trafiğinden yönlendiren hizmeti yayımlanan uygulamalar. Daha ayrıntılı yükleme yönergeleri için bkz: [uygulama ara sunucusunu etkinleştirme hello Azure portal](active-directory-application-proxy-enable.md).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.
2. Seçin **Azure Active Directory** > **uygulama proxy'si**.
3. Seçin **Bağlayıcısı'nı indir** toostart hello uygulama ara sunucusu Bağlayıcısı indirme. Merhaba yükleme yönergelerini izleyin.

   ![Uygulama Ara sunucusunu etkinleştirme ve hello bağlayıcı indirin](./media/application-proxy-ping-access/install-connector.png)

4. Merhaba Bağlayıcısı indirme otomatik olarak etkinleştirmelisiniz uygulama proxy'si değil, seçebilirsiniz, ancak dizininiz için **uygulama ara sunucusunu etkinleştirme**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Uygulama tooAzure AD uygulama proxy'si ile ekleme

İki Eylemler hello Azure portal tootake ihtiyacınız vardır. İlk olarak, uygulamanızın uygulama proxy'si ile toopublish gerekir. Ardından, toocollect hello PingAccess adımları sırasında kullanabilirsiniz hello uygulama hakkında bazı bilgiler gerekir.

Bu adımları toopublish uygulamanızı izleyin. 1-8, bkz: izlenecek adımların daha ayrıntılı için [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).

1. Merhaba son bölümünde almadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.
2. Seçin **Azure Active Directory** > **kurumsal uygulamalar**.
3. Seçin **Ekle** hello dikey penceresinde hello üstünde.
4. Seçin **şirket içi uygulama**.
5. Yeni uygulamanızı hakkında bilgi içeren hello gerekli alanları doldurun. Yönergeler hello ayarları için aşağıdaki hello kullan:
   - **İç URL**: normal şekilde hello şirket ağında olduğunuzda, sayfasında toohello uygulamanın oturum geçen hello URL'sini sağlayın. Bu senaryo için hello Bağlayıcısı hello ön sayfa hello uygulamasının olarak tootreat hello PingAccess proxy olması gerekir. Şu biçimi kullanın: `https://<host name of your PA server>:<port>`. başlangıç bağlantı noktası, varsayılan değer 3000 olmakla birlikte PingAccess yapılandırabilirsiniz.
   - **Ön kimlik doğrulama yöntemi**: Azure Active Directory
   - **Üstbilgiler URL'de çevir**: Hayır

   >[!NOTE]
   >Bu ilk uygulamanızı ise, bağlantı noktası 3000 toostart kullanın ve tooupdate PingAccess yapılandırmanızı değiştirirseniz, bu ayar geri dönün. İkinci veya sonraki uygulamanız varsa bu toomatch hello PingAccess içinde yapılandırdığınız dinleyicisi gerekir. Daha fazla bilgi edinmek [PingAccess dinleyicileri](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Seçin **Ekle** hello dikey penceresinde hello sonundaki. Uygulamanızı eklenir ve hello Hızlı Başlat menüsü açılır.
7. Merhaba Hızlı Başlangıç menüsünde seçin **test etmek için bir kullanıcı atamak**ve en az bir kullanıcı toohello uygulama ekleyin. Bu test hesap erişim toohello şirket içi uygulama olduğundan emin olun.
8. Seçin **atamak** toosave hello test kullanıcı ataması.
9. Merhaba uygulama yönetimi dikey penceresinde, seçin **çoklu oturum açma**.
10. Seçin **üstbilgi tabanlı oturum açma** hello açılan menüsünden. **Kaydet**’i seçin.

   >[!TIP]
   >Üstbilgi tabanlı çoklu oturum açma kullanarak, ilk kez kullanıyorsanız tooinstall PingAccess gerekir. toomake emin Azure aboneliğinizi otomatik olarak PingAccess yüklemenizi, bu tek oturum açma sayfası toodownload PingAccess kullanım hello bağlantıyı ilişkilidir. Şimdi hello indirme sitesi açmak veya toothis sayfa daha sonra geri dönün. 

   ![Üstbilgi tabanlı oturum açma seçin](./media/application-proxy-ping-access/sso-header.PNG)

11. Merhaba kurumsal uygulamalar dikey penceresini kapatın veya tüm hello yolu toohello sol tooreturn toohello Azure Active Directory menüsüne gidin.
12. Seçin **uygulama kayıtlar**.

   ![Uygulama kayıtlar seçin](./media/application-proxy-ping-access/app-registrations.png)

13. Yeni eklediğiniz, ardından select hello uygulama **yanıt URL'leri**.

   ![Yanıt URL'leri seçin](./media/application-proxy-ping-access/reply-urls.png)

14. Merhaba dış URL hello yanıt URL'leri listesindeki bu atanan tooyour uygulamanızı adım 5'te ise toosee denetleyin. Değilse, şimdi ekleyin.
15. Merhaba uygulama ayarları dikey penceresinde, seçin **gerekli izinleri**.

  ![Gerekli izinleri seçin](./media/application-proxy-ping-access/required-permissions.png)

16. **Add (Ekle)** seçeneğini belirleyin. Merhaba API seçin **Windows Azure Active Directory**, ardından **seçin**. Merhaba izinlerini seçin **okuma ve tüm uygulamaları yazma** ve **oturum açın ve kullanıcı profilini okuma**, ardından **seçin** ve **Bitti**.  

  ![İzinleri seçin](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Merhaba PingAccess adımlar için bilgi toplama

1. Uygulama ayarları dikey üzerinde seçin **özellikleri**. 

  ![Özellikler'i seçin](./media/application-proxy-ping-access/properties.png)

2. Merhaba Kaydet **uygulama kimliği** değeri. PingAccess yapılandırdığınızda bu hello istemci kimliği için kullanılır.
3. Merhaba uygulama ayarları dikey penceresinde, seçin **anahtarları**.

  ![Anahtarları seçin](./media/application-proxy-ping-access/Keys.png)

4. Bir anahtar açıklama girerek ve sona erme tarihi hello açılan menüden seçerek bir anahtar oluşturun.
5. **Kaydet**’i seçin. Bir GUID hello görünür **değeri** alan.

  Bu değer şimdi mümkün toosee olmayacak şekilde yeniden sonra bu pencereyi kapatın.

  ![Yeni bir anahtar oluşturun](./media/application-proxy-ping-access/create-keys.png)

6. Merhaba uygulama kayıtlar dikey penceresini kapatın veya tüm hello yolu toohello sol tooreturn toohello Azure Active Directory menüsüne gidin.
7. Seçin **özellikleri**.
8. Merhaba Kaydet **dizin kimliği** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>İsteğe bağlı - güncelleştirme GraphAPI toosend özel alanlar

Azure AD kimlik doğrulaması için gönderir güvenlik belirteçleri listesi için bkz: [Azure AD belirteç başvurusu](./develop/active-directory-token-and-claims.md). Diğer belirteçleri gönderir bir özel talep gerekiyorsa, GraphAPI tooset hello uygulama alanını kullanın *acceptMappedClaims* çok**doğru**. Azure AD Graph Explorer'a veya MS Graph toomake bu yapılandırmayı kullanabilirsiniz. 

Bu örnek Graph Explorer'a kullanır:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>PingAccess indirin ve uygulamanızı yapılandırma

Tüm hello Azure Active Directory kurulum adımlarını tamamladığınıza göre PingAccess tooconfiguring üzerinde taşıyabilirsiniz. 

Merhaba hello PingAccess bu senaryonun parçası için ayrıntılı adımlar devam hello Ping kimlik belgeleri [yapılandırma PingAccess Azure AD için](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Bu adımları, PingAccess hesabı zaten yoksa, alma, hello PingAccess sunucusu yükleme ve hello hello Azure portal ' kopyaladığınız dizini kimliği ile bir Azure AD OIDC sağlayıcı bağlantısı oluşturma hello işleminde size yol. Ardından, üzerinde PingAccess hello uygulama kimliği ve anahtarı değerlerini toocreate Web oturumu kullanın. Bundan sonra kimlik eşlemesi ayarlamanız ve bir sanal ana bilgisayar, site ve uygulama oluşturun.

### <a name="test-your-app"></a>Uygulamanızı test etme

Tüm bu adımları tamamladıktan sonra uygulamanızı açık ve çalışıyor olması. tootest, bir tarayıcı açın ve Azure'da hello uygulama yayımlandığında, oluşturduğunuz toohello dış URL'yi gidin. Bu, atanan toohello uygulama Hello test hesabıyla oturum açın.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD için PingAccess yapılandırın](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?](application-proxy-sso-overview.md)
- [Uygulama proxy'si sorun giderme](active-directory-application-proxy-troubleshoot.md)
