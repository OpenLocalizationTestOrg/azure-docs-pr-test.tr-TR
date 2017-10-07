---
title: "Azure AD uygulama proxy'si aaaCustom alanlarında | Microsoft Docs"
description: "Azure AD uygulama proxy'si özel etki alanlarında olan hello uygulama için bu hello URL'yi hello şekilde aynı kullanıcılarınız, nerede erişim bağımsız olarak yönetin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Azure AD uygulama proxy'si özel etki alanları ile çalışma

Azure Active Directory Uygulama proxy'si aracılığıyla uygulama yayımladığınızda, uzaktan çalışıyorsanız, kullanıcıların toogo toowhen için bir dış URL oluşturun. Bu URL'yi hello varsayılan etki alanı alır *yourtenant.msappproxy.net*. Örneğin, yayımladıysanız, bir uygulama giderleri adlı ve Kiracı Contoso adlı ardından hello dış URL https://expenses-contoso.msappproxy.net olacaktır. Kendi etki alanı adınızı toouse istiyorsanız, uygulamanız için özel bir etki alanı yapılandırın. 

Mümkün olduğunda, uygulamalarınız için özel etki alanları ayarlamanızı öneririz. Özel etki alanlarını hello avantajlarından bazıları şunlardır:

- Kullanıcılarınızın toohello uygulamayla alabilirsiniz içinde veya ağınızın dışındaki çalıştıkları olup olmadığını aynı URL'ye hello.
- Tüm uygulamalarınızın sahip Merhaba, aynı iç ve dış URL'ler tooanother işaret eden bir uygulama bağlantıları toowork hello kurumsal ağ dışından bile devam edin. 
- Marka bilgilerinizi denetlemek ve istediğiniz hello URL'leri oluşturun. 


## <a name="configure-a-custom-domain"></a>Özel bir etki alanı yapılandırma

### <a name="prerequisites"></a>Ön koşullar

Özel bir etki alanı yapılandırmadan önce hello hazırlanmış gereksinimlerine sahip olduğunuzdan emin olun: 
- A [doğrulanmış etki alanı eklenen tooAzure Active Directory](active-directory-domains-add-azure-portal.md).
- Bir PFX dosyası hello biçiminde hello etki alanı için özel bir sertifika. 
- Bir şirket içi uygulama [uygulaması Proxy üzerinden yayımlanan](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Özel etki alanınızı yapılandırın

Bu üç gereksinimleri hazır olduğunda, bu adımları tooset özel etki alanınızı ayarlama izleyin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** ve hello uygulamayı seçin toomanage istiyor.
3. Seçin **uygulama proxy'si**. 
4. Merhaba dış URL alanına hello açılır liste tooselect özel etki alanınızı kullanacak. Merhaba liste etki alanınızda görmüyorsanız, ardından bunu henüz doğrulanmış kurmadı. 
5. Seçin **Kaydet**
5. Merhaba **sertifika** hale devre dışı bırakıldı alan etkin. Bu alanı seçin. 

   ![Bir sertifika tooupload tıklatın](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Bu etki alanı için bir sertifika Karşıya zaten hello sertifika alanı hello sertifika bilgilerini görüntüler. 

6. Hello PFX sertifikasını karşıya yükleme ve hello sertifikanın hello parola girin. 
7. Seçin **kaydetmek** toosave değişikliklerinizi. 
8. Ekleme bir [DNS kaydı](../dns/dns-operations-recordsets-portal.md) yeniden yönlendirmeleri yeni dış URL toohello msappproxy.net etki hello. 

>[!TIP] 
>Özel etki alanı başına tooupload bir sertifika yeterlidir. Bir sertifika karşıya yükledikten sonra yeni bir uygulama yayımlama ve hello DNS kaydı dışında toodo ek yapılandırmaya sahip olmayan hello özel etki alanı seçebilirsiniz. 

## <a name="manage-certificates"></a>Sertifikaları yönetme

### <a name="certificate-format"></a>Sertifika biçimi
Merhaba sertifika imza yöntemleri sınırlaması yoktur. Tüm Eliptik Eğri Şifrelemesi (ECC), konu alternatif adı (SAN) ve diğer ortak sertifika türleri desteklenir. 

İstenen hello dış URL Hello joker eşleştiği sürece bir joker sertifikası kullanabilirsiniz. 

Otomatik olarak imzalanan sertifikalar, de kullanabilirsiniz. Özel sertifika yetkilisi kullanıyorsanız, hello CDP (sertifika iptal noktası dağıtım noktası) hello sertifikası için ortak olmalıdır.

### <a name="changing-hello-domain"></a>Merhaba etki alanını değiştirme
Tüm doğrulanmış etki hello dış URL aşağı açılan listesinde, uygulamanız için görünür. toochange hello etki alanı, hello uygulama için alan yalnızca güncelleştirme. Merhaba etki hello listede yoksa [doğrulanmış bir etki alanına eklemek](active-directory-domains-add-azure-portal.md). İlişkili bir sertifika henüz sahip olmayan bir etki alanı seçin, adım 5-7 tooadd hello sertifika izleyin. Ardından, hello DNS kaydı tooredirect hello yeni dış URL'den güncelleştirdiğinizden emin olun. 

### <a name="certificate-management"></a>Sertifika yönetimi
Bir dış konak hello uygulamaları paylaşmak sürece birden çok uygulama için aynı sertifika hello kullanabilirsiniz. 

Bir sertifikanın süresi dolduğunda tooupload bildiren bir uyarı elde hello portalı üzerinden başka bir sertifika. Merhaba sertifika iptal edilirse, kullanıcılarınızın Merhaba uygulaması erişirken bir güvenlik uyarısı görebilirsiniz. Biz için sertifikalar iptal denetimlerini yerine getirmiyor.  belirli bir uygulamada tooupdate hello sertifika toohello uygulama gidin ve yayımlanmış uygulamalar tooupload yeni bir sertifika özel etki alanlarını yapılandırma için 5-7 adımları izleyin. Merhaba eski sertifika diğer uygulamalar tarafından kullanılmadığından, otomatik olarak silinir. 

Şu anda hello ilgili uygulamalar Merhaba içeriğine toomanage sertifikaları gereksinim duyduğunuz tüm sertifika yönetimi tek tek uygulama sayfaları olduğundan. 

## <a name="next-steps"></a>Sonraki adımlar
* [Çoklu oturum açmayı etkinleştir](active-directory-application-proxy-sso-using-kcd.md) tooyour yayımlanan uygulamaları Azure AD kimlik doğrulaması ile.
* [Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md) tooyour yayımlanan uygulamalar.
* [Özel etki alanı adı tooAzure AD ekleyin](active-directory-domains-add-azure-portal.md)


