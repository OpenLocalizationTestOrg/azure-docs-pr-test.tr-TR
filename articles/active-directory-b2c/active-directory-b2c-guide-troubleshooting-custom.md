---
title: "Azure Active Directory B2C: özel ilke sorunlarını giderme | Microsoft Docs"
description: "Azure Active Directory'de özel ilkeler ile çalışırken, yaklaşımlar hakkında toosolving hataları öğrenin."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Azure AD B2C özel ilkeleri ve kimlik deneyimi Framework sorun giderme

Azure Active Directory B2C kullanıyorsanız (Azure AD B2C) özel ilkeler, ilke dil XML biçiminde hello kimlik deneyimi Framework ayarlama zorluklar deneyimi.  Öğrenme toowrite özel ilkeler, yeni bir dil öğrenme gibi olabilir. Bu makalede, biz araçları açıklamak ve hızlı bir şekilde Yardım ipuçları bulmak ve sorunları çözün. 

> [!NOTE]
> Bu makalede, Azure AD B2C özel ilke yapılandırma sorunlarını gidermeye üzerine odaklanır. Bağlı olan taraf uygulaması veya kendi kimlik kitaplık hello adresi değil.

## <a name="xml-editing"></a>XML düzenleme

Merhaba özel ilkelerini ayarlama en sık karşılaşılan hata yanlış olan XML biçimli. İyi bir XML Düzenleyicisi neredeyse gereklidir. İyi bir XML Düzenleyicisi XML yerel olarak görüntüler, içerik renk kodları, Ortak terimleri doldurur, XML öğeleri dizini tutar ve şemasıyla doğrulayabilirsiniz. İki bizim sık kullanılan XML düzenleyicileri şunlardır:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Not Defteri'ni ++](https://notepad-plus-plus.org/)

XML dosyanızı karşıya yüklemeden önce XML Şeması doğrulama hataları tanımlar. Merhaba kök klasöründe hello starter pack Merhaba XML şema tanımı TrustFrameworkPolicy_0.3.0.0.xsd alın. XML düzenleyicinizi hello belgelerinde daha fazla bilgi aramak *XML araçları* ve *XML doğrulama*.

XML kuralları gözden yararlı bulabilirsiniz. Azure AD B2C algıladığı hataları biçimlendirme XML reddeder. Bazen, hatalı biçimlendirilmiş XML yanıltıcı hata iletileri neden olabilir.

## <a name="upload-policies-and-policy-validation"></a>İlkeleri ve ilke doğrulaması karşıya yükle

 XML dosya karşıya yükleme doğrulaması otomatik olarak yapılır. Çoğu hatalara hello karşıya yükleme toofail neden olabilir. Doğrulama karşıya yüklediğiniz hello ilke dosyası içerir. Ayrıca dosyaları hello karşıya yükleme dosyası başvuruyor çok hello zinciri içerir (bağlı olan taraf ilke dosyası, hello uzantıları dosya ve hello temel dosyanın hello). 
 
 Sık karşılaşılan doğrulama hataları hello şunları içerir.

Hata parçacığını:`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Merhaba ClaimType değeri yanlış yazılmış veya hello şemada yok.
* ClaimType değerleri en az bir hello İlkesi'nde hello dosyaların tanımlanmalıdır. 
    Örneğin, ` <ClaimType Id="socialIdpUserId">`
* ClaimType hello uzantıları dosyasında tanımlı, ancak ayrıca hello temel dosyanın TechnicalProfile değerindeki kullanılır, hello temel dosyanın karşıya bir hatayla sonuçlanır.

Hata parçacığını:`...makes a reference tooa ClaimsTransformation with id...`
* Merhaba hata hello olması için aynı hello ClaimType hata ettirilmesi nedenler hello.

Hata parçacığını:`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Bu hello hello Tenantıd değeri denetleyin ** \<TrustFrameworkPolicy\> ** ve ** \<BasePolicy\> ** öğeleri aynı Azure AD B2C hedef Kiracı.  

## <a name="troubleshoot-hello-runtime"></a>Merhaba çalışma zamanı sorun giderme

* Kullanım `Run Now` ve `https://jwt.io` tootest ilkelerinizi web veya mobil uygulama bağımsız olarak. Bu Web sitesine bir bağlı olan taraf uygulaması gibi davranır. Merhaba içeriğine hello JSON Web Token (Azure AD B2C İlkesi tarafından oluşturulan JWT) görüntüler. toocreate test uygulaması Framework'teki kimlik deneyimi, aşağıdaki değerleri kullanın hello:
    * Ad: TestApp
    * Web uygulaması/Web API: Hayır
    * Yerel istemci: Hayır

* Azure AD B2C, kullanım ve istemci tarayıcısı arasında iletileri tootrace hello değişimi [Fiddler](http://www.telerik.com/fiddler). Kullanıcı Yolculuğunuzun orchestration adımlarınızı nerede başarısız bir gösterge size yardımcı olabilir.

* İçinde **geliştirme modunu**, kullanın **Application Insights** tootrace hello etkinliğini kimlik deneyimi Framework kullanıcı Yolculuğunuzun. İçinde **geliştirme modunu**, talepler hello kimlik deneyimi Framework arasında hello exchange görebilirsiniz ve hello çeşitli talep kimlik sağlayıcıları, API tabanlı hizmetler gibi teknik profillerini tarafından tanımlanan sağlayıcıları Azure çok / multi-Factor-Authentication gibi Hello Azure AD B2C kullanıcı dizini ve diğer hizmetler.  

## <a name="recommended-practices"></a>Önerilen uygulamalar

**Birden fazla sürümünü senaryolarınızı tutun. Uygulamanız ile projesinde gruplandırın.** Merhaba Bankası, uzantıları ve bağlı olan taraf dosyaları birbirlerine doğrudan bağımlı. Bir grup olarak kaydedin. Yeni özellikler tooyour ilkeler eklendikçe ayrı çalışma sürümleri tutun. Aşama çalışma sürümlerinde kendi dosya sistemi ile etkileşim hello uygulama kodu.  Uygulamalarınızın birçok farklı bağlı olan taraf ilkelerinde Kiracı çağırabilir. Bunlar, Azure AD B2C ilkelerden bekledikleri hello talep bağımlı hale gelebilir.

**Geliştirme ve bilinen kullanıcı Yolculuklar teknik profilleriyle sınayın.** Sınanan başlangıç paketi ilkeleri tooset teknik profillerinizi yukarı kullanın. Bunları ayrı olarak kendi kullanıcı Yolculuklar dahil önce test edin.

**Geliştirme ve test edilmiş teknik profilleriyle kullanıcı Yolculuklar sınayın.** Bir kullanıcı gezisine Hello orchestration adımlardan artımlı olarak değiştirin. Aşamalı olarak hedeflenen senaryolarınızı oluşturun.

## <a name="next-steps"></a>Sonraki adımlar

* Github'da, hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip dosyasını indirin.
