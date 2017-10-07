---
title: "uygulamaları için Azure AD SSO aaaConfigure | Microsoft Docs"
description: "Tooself hizmet uygulamaları tooAzure Active Directory nasıl bağlanacağını öğrenin SAML ve parola tabanlı SSO kullanma"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma
Bu makalede, yöneticiler tooconfigure tek oturum açma tooapplications hello Azure Active Directory Uygulama galerisinde yok sağlayan bir özellik hakkındadır *kod yazma olmadan*. Bu özellik 18 Kasım 2015 üzerinde technical preview sürümünden yayımlanmıştır ve dahil [Azure Active Directory Premium](active-directory-editions.md). Bunun yerine Geliştirici Kılavuzu nasıl görmek istiyorsanız toointegrate özel uygulama kodu aracılığıyla Azure AD ile bkz [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).

Hello Azure Active Directory Uygulama galerisinde toosupport Azure Active Directory ile çoklu oturum açma biçimi bilinen uygulamalar listesini bölümünde açıklandığı gibi sağlar [bu makalede](active-directory-appssoaccess-whatis.md). Siz (bir BT uzmanı veya sistem Tümleştirici kuruluşunuzdaki) Merhaba uygulaması bulduktan sonra tooconnect istediğiniz, izleme hello adım adım yönergeler hello Azure Yönetim Portalı tooenable çoklu oturum açma sunulan tarafından başlayabiliriz.

Müşterilerle [Azure Active Directory Premium](active-directory-editions.md) lisansları bu ek özellikler de alırsınız:

* SAML 2.0 kimlik sağlayıcısı (SP tarafından başlatılan veya IDP başlatılan) destekleyen herhangi bir uygulama Self Servis tümleştirilmesi
* Kullanarak bir HTML tabanlı oturum açma sayfasına sahip herhangi bir web uygulaması Self Servis tümleştirilmesi [parola tabanlı SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Self Servis bağlantı kullanıcı sağlama için hello SCIM'yi protokolünü kullanan uygulamaların ([burada açıklanan](active-directory-scim-provisioning.md))
* Özelliği tooadd bağlantılar hello tooany uygulamada [Office 365 uygulama Başlatıcı](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) veya hello [Azure AD erişim paneli](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Bu yalnızca kullanır ancak henüz dahil edilmiş toohello Azure AD uygulama galerisinde edilmemiş SaaS uygulamaları içerebilir, ancak kuruluşunuz hello Bulut veya şirket içi kontrol tooservers dağıtmış olan üçüncü taraf web uygulamaları.

Bu özellikleri olarak da bilinen, *uygulama tümleştirmesi şablonları*, SAML, SCIM'yi ya da form tabanlı kimlik doğrulamasını destekleyen uygulamalar için standartlara dayalı bağlantı noktaları sağlar ve esnek seçeneklerini ve ayarlarını içerir Uygulama geniş sayısı ile uyumluluk. 

## <a name="adding-an-unlisted-application"></a>Listede bulunmayan bir uygulama ekleme
tooconnect bir uygulama tümleştirme şablonu kullanarak bir uygulamayı Azure Active Directory yönetici hesabını kullanarak hello Azure Yönetim Portalı'na oturum ve toohello Gözat **Active Directory > [Directory] > uygulamalar**bölümünde, select **Ekle**ve ardından **hello Galeriden bir uygulama eklemek**. 

![][1]

Merhaba uygulama galerisinde hello kullanarak listelenmemiş bir uygulama eklemek için **özel** kategori hello soldaki veya hello seçerek **listede bulunmayan bir uygulama eklemek** hello aramada gösterilen bağlantı sonuçları, istenen uygulamanızı bulunamadı. Uygulamanız için bir ad girdikten sonra hello çoklu oturum açma seçenekleri ve davranışını yapılandırabilirsiniz. 

**Hızlı İpucu**: hello uygulama galerisinde hello uygulama zaten varsa, en iyi uygulama, hello arama işlevi toocheck toosee kullanın. Merhaba uygulama bulundu ve "çoklu oturum açmanın" sonra Merhaba uygulaması açıklamasını değinmektedir zaten Federasyon çoklu oturum açma için desteklenir. 

![][2]

Bu şekilde bir uygulama eklemek bir çok benzer deneyim toohello önceden tümleştirilmiş uygulamalar için kullanılabilir bir sağlar. toostart, select **yapılandırma çoklu oturum açma**. Merhaba sonraki ekranda, çoklu oturum açma yapılandırmak için üç seçenek aşağıdaki hello aşağıdaki bölümlerde açıklanan hello gösterir.

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD çoklu oturum açma
Bu seçenek tooconfigure SAML tabanlı kimlik doğrulaması için Merhaba uygulaması seçin. Bu gerektiren uygulama desteği SAML 2.0 hello ve nasıl toouse Merhaba devam etmeden önce Merhaba uygulaması SAML özellikleri hakkında bilgi toplamanız gerekir. Seçtikten sonra **sonraki**, istendiğinde tooenter üç farklı URL'ler Merhaba uygulaması için toohello SAML uç noktaları karşılık gelen olacaktır. 

![][4]

Bunlar:

* **Oturum üzerinde URL'si (SP tarafından başlatılan yalnızca)** – toosign bileşenini toothis uygulama hello kullanıcı gider burada. Merhaba uygulaması yapılandırılmışsa tooperform hizmet sağlayıcısı tarafından başlatılan tek oturum açma, sonra bir kullanıcı toothis URL gittiğinde, hello hizmet sağlayıcısı gerekli yeniden yönlendirme tooAzure AD tooauthenticate hello ve hello kullanıcı olarak oturum. Bu alan doldurulursa, Azure AD bu URL toolaunch hello uygulamadan Office 365 ve Azure AD erişim paneli hello kullanır. Bu alan ommited olan sonra Azure AD yerine kimlik sağlayıcısı gerçekleştirmek-zaman hello uygulama hello Azure AD erişim paneli, Office 365 veya Azure AD hello tek başlatıldıktan üzerinde başlatılan oturum oturum açma URL'si (Merhaba Pano sekmesinden copiable).
* **Veren URL'si** -hello veren URL benzersizce Merhaba uygulaması hangi tek oturum açma yapılandırılan için. Bu Azure AD hello geri tooapplication gönderir hello değerdir **İzleyici** parametredir hello SAML belirteci ve Merhaba uygulaması beklenen toovalidate onu. Bu değer ayrıca hello görünür **varlık kimliği** hello uygulama tarafından sağlanan herhangi bir SAML meta veri içinde. Ne hakkında ayrıntılar için Hello uygulamanın SAML belgelerine bakın varlık kimliği veya İzleyici değer olup olmadığı. Merhaba İzleyici URL hello SAML belirteci döndürülen toohello uygulamada görünme örneği aşağıdadır:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **Yanıt URL'si** -hello yanıt URL'si olan burada hello uygulama tooreceive hello SAML belirteci bekler. Bu aynı zamanda başvurulan tooas hello olup **onaylama tüketici Hizmeti'ni (ACS) URL**. SAML belirteci yanıt URL'si veya ACS URL nedir ile ilgili ayrıntılar için Hello uygulamanın SAML belgelerine bakın.
  Bunlar girdikten sonra tıklatın **sonraki** tooproceed toohello sonraki ekranda. Bu ekran hangi gereksinimlerini toobe tooaccept Azure AD'den bir SAML belirtecine yapılandırdığınız hello uygulama yan tooenable üzerinde hakkında bilgi sağlar. 

![][5]

Hangi değerlerin gerekli hello uygulamaya bağlı olarak farklılık gösterir, Ayrıntılar için hello uygulamanın SAML belgelerine kontrol edin. Merhaba **oturum açma** ve **oturum kapatma** her iki hizmet URL'si toohello çözmek için Azure AD Örneğinize hello SAML istek işleme uç noktadır aynı uç noktası. Merhaba veren URL'si hello "Veren" Merhaba SAML belirteci verilen toohello uygulama içinde görünen hello değerdir. 

Uygulamanızı yapılandırıldıktan sonra tıklatın **sonraki** düğmesine tıklayın ve ardından hello **tam** tooclose hello iletişim. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Kullanıcılar ve gruplar tooyour SAML uygulama atama
Ardından, uygulamanızın SAML tabanlı kimlik sağlayıcısı olarak yapılandırılmış toouse Azure AD silindikten sonra neredeyse hazır tootest hale gelir. Güvenlik denetimi olarak Azure AD, Azure AD kullanarak erişim verildi sürece hello uygulamasına toosign vermeden bir belirteç yayınlamayacaktır. Kullanıcılar, doğrudan veya bir üyesi olan bir grubu aracılığıyla erişim verilebilir. 

tooassign bir kullanıcı veya grup tooyour uygulama tıklatın hello **Kullanıcıları Ata** düğmesi. Hello kullanıcı veya grup tooassign istiyor ve hello seçin seçin **atamak** düğmesi. 

![][6]

Bir kullanıcı atama Azure AD tooissue hello kullanıcı yanı sıra bu uygulama tooappear için bir kutucuğa hello kullanıcının erişim panelinde neden için bir belirteç izin verir. Merhaba kullanıcı Office 365 kullanıyorsa, bir uygulama döşeme hello Office 365 uygulama Başlatıcı de görüntülenir. 

Hello kullanarak hello uygulaması için bir kutucuk logosu yükleyebilirsiniz **karşıya logosu** hello düğmesinde **yapılandırma** hello uygulama sekmesinde. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Merhaba SAML belirtecinde verilen hello talepler özelleştiriliyor
Bir kullanıcı toohello uygulama doğruladığında, Azure AD benzersiz olarak tanımlayan hello kullanıcı hakkında bilgileri (veya talep) içeren bir SAML belirteci toohello uygulaması gönderirsiniz. Varsayılan olarak bu hello kullanıcının kullanıcı adı, e-posta adresi, ad ve Soyadı içerir. 

Görüntülemek veya hello hello altındaki SAML belirteci toohello uygulama gönderilen hello talep Düzenle **öznitelikleri** sekmesi. 

![][7]

Neden ihtiyacınız olabilecek hello SAML belirtecinde verilen tooedit hello talepler iki olası nedeni vardır: •hello uygulama farklı bir talep URI'ler ayarlayın veya talep değerleri •Your uygulama hello gerektiren bir şekilde dağıtılan toorequire yazıldı NameIdentifier talep toobe Azure Active Directory'de depolanan bir şey hello kullanıcı adı (AKA kullanıcı asıl adı) dışında. 

Nasıl tooadd ve düzenleme talepleri için bu senaryolar hakkında daha fazla bilgi için bu bilgiye denetleyin [talep özelleştirme makale](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Merhaba SAML uygulamayı test etme
Azure AD ve Merhaba uygulaması Hello SAML URL'leri ve sertifika yapılandırıldıktan sonra kullanıcılar veya gruplar, azure'da toohello uygulama atanmış ve hello talep gözden ve gerekirse düzenlenebilir ardından hello içine hazır toosign hello kullanıcıdır uygulama. 

tootest, yalnızca oturum-Azure AD erişim paneli toohello uygulama atanmış bir kullanıcı hesabı kullanarak https://myapps.microsoft.com adresindeki hello ve hello bölme hello uygulama tookick oturum açma hello tek işlem kapatmak için tıklayın. Alternatif olarak, doğrudan hello uygulama ve oturum açma buradan için oturum açma URL'si toohello göz atabilirsiniz. 

Hata ayıklama ipuçları için bkz [nasıl makale toodebug SAML tabanlı tek oturum açma tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Parola çoklu oturum açma
Bu seçenek tooconfigure seçin [parola tabanlı çoklu oturum açma](active-directory-appssoaccess-whatis.md) oturum açma bir HTML sayfası olduğu bir web uygulaması. SSO, ayrıca vaulting, başvurulan tooas parola parola tabanlı Kimlik Federasyonu Desteği toomanage kullanıcı erişimi ve parolaları tooweb uygulamaları etkinleştirir. Birkaç kullanıcı tooshare tooyour kuruluşunuzun sosyal medya uygulama hesapları gibi tek bir hesap gereken yeri senaryoları için de yararlıdır. 

Seçtikten sonra **sonraki**, istendiğinde tooenter hello hello uygulamanın web tabanlı oturum açma sayfası URL'sini olacaktır. Bu hello kullanıcı adı ve parola giriş alanları içeren hello sayfa olması gerektiğini unutmayın. Bir işlem tooparse hello oturum açma sayfasında bir kullanıcı adı girişi ve bir parola girişi için bir kez girilen, Azure AD başlatır. Merhaba işlem başarılı olmazsa, sonra da, toomanually yakalama hello alanları sağlayacak bir tarayıcı uzantısı (Internet Explorer, Chrome veya Firefox gerektirir) yükleme bir alternatif işleminde size rehberlik eder.

Merhaba oturum açma sayfası yakalandıktan sonra kullanıcılar ve gruplar atanabilir ve kimlik bilgisi ilkeleri yalnızca normal gibi ayarlanabilir [parola SSO uygulamaları](active-directory-appssoaccess-whatis.md).

Not: Hello kullanarak hello uygulaması için bir kutucuk logosu yükleyebilirsiniz **karşıya logosu** hello düğmesinde **yapılandırma** hello uygulama sekmesinde. 

## <a name="existing-single-sign-on"></a>Varolan çoklu oturum açma
Bu seçenek tooadd bir bağlantı tooan uygulama tooyour kuruluşunuzun Azure AD erişim paneli veya Office 365 portalında seçin. Şu anda Azure Active Directory Federasyon Hizmetleri (veya başka bir Federasyon Hizmeti) kullanan bu tooadd bağlantılar toocustom web uygulamaları, Azure AD kimlik doğrulama için yerine kullanabilirsiniz. Veya ayrıntılı bağlantılar toospecific SharePoint sayfaları veya yalnızca kullanıcı erişimi paneller üzerinde tooappear istediğiniz diğer web sayfaları ekleyebilirsiniz. 

Seçtikten sonra **sonraki**, istendiğinde tooenter hello hello uygulama toolink URL'sini olacaktır. Tamamlandığında, kullanıcılar ve gruplar hello hello uygulama tooappear neden toohello uygulama atanabilir [Office 365 uygulama Başlatıcı](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) veya hello [Azure AD erişim paneli](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) olan kullanıcılar için.

Not: Hello kullanarak hello uygulaması için bir kutucuk logosu yükleyebilirsiniz **karşıya logosu** hello düğmesinde **yapılandırma** hello uygulama sekmesinde.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [İçinde talep tooCustomize verilen nasıl Pre-Integrated uygulamalar için SAML belirteci hello](active-directory-saml-claims-customization.md)
* [Sorun giderme SAML tabanlı çoklu oturum açma](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
