---
title: "aaa \"Bu Kurumsal uygulama hatası uygulama proxy'si uygulama kullanırken erişemiyor | Microsoft Docs\""
description: "Nasıl Azure AD uygulama proxy'si uygulamalarla tooresolve ortak erişim verir."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Uygulama proxy'si uygulama kullanılırken "Kurumsal bu uygulamaya erişemezsiniz" hatası

Bu makale bir Azure AD uygulama proxy'si uygulama bir "Bu Kurumsal uygulama erişilemiyor" hatasını gördüğünüzde karşılaştığı yaygın sorunları tootroubleshoot yardımcı.

## <a name="overview"></a>Genel Bakış
Bu hatayı gördüğünüzde hello sayfa ayrıca paylaşmak bir durum kodu. Bu kodu hello şu olabilir:

-   **Ağ geçidi zaman aşımı**: hello uygulama proxy'si hizmeti olan oluşturulamıyor tooreach hello bağlayıcı. Bu genellikle hello bağlayıcı atama, bağlayıcının kendisi veya kuralları hello bağlayıcı geçici ağ hello bir sorun olduğunu gösterir.

-   **Hatalı ağ geçidi**: hello Bağlayıcıdır oluşturulamıyor tooreach Merhaba arka uç uygulaması. Bu yanlış yapılandırma hello uygulamasının olduğunu gösteriyor olabilir.

-   **Yasak**: hello kullanıcı yetkili tooaccess Merhaba uygulaması değil. Merhaba kullanıcı toohello uygulama Azure Active Directory'de atanmadığında veya hello arka uçta izni tooaccess Merhaba uygulaması hello kullanıcı yoksa bu durum meydana gelebilir.

toofind hello kodu, hello hello hata iletisinin hello "Durum kodu" alanı için sol alt hello metin bakın. Ayrıca notları hello çok hello sayfanın sonundaki ek ipuçları ile arayın.

   ![Ağ geçidi zaman aşımı hatası](./media/application-proxy/connection-problem.png)

Nasıl tootroubleshoot hello kök nedenini bu hataları ve önerilen düzeltmeler hakkında daha fazla ayrıntı hakkında daha fazla bilgi için hello karşılık gelen bölümüne bakın.

## <a name="gateway-timeout-errors"></a>Ağ geçidi zaman aşımı hataları

Bir ağ geçidi zaman aşımı Hello hizmeti tooreach hello bağlayıcı çalışır ve oluşturamıyor toowithin hello zaman aşımı penceresinde oluşur. Bu tooa çalışma bağlayıcılar bağlayıcı grubuyla atanan bir uygulamayı nedeni genellikle veya hello bağlayıcı tarafından gerekli bazı bağlantı noktaları açık değil.


## <a name="bad-gateway-errors"></a>Hatalı ağ geçidi hataları

Hatalı ağ geçidi hata bu hello bağlayıcı oluşturulamıyor tooreach hello arka uç uygulaması olduğunu gösterir. Merhaba doğru uygulama yayımlandığından emin olun. Bu hataya neden yaygın hatalar:

-   Bir yazım hatasından veya hata hello İç URL

-   Merhaba uygulaması değil yayımlama hello kök dizini. Örneğin, yayımlama <http://expenses/reimbursement> ancak tooaccess çalışırken <http://expenses>

-   Merhaba Kerberos Kısıtlı temsilci (KCD) yapılandırma sorunları

-   Merhaba arka uç uygulaması sorunları

## <a name="forbidden-errors"></a>Yasaklanmış hataları

Yasak hata görürseniz, hello kullanıcı toohello uygulama atanmadı. Bu, Azure Active Directory'de veya Merhaba arka uç uygulaması olabilir.

toolearn tooassign kullanıcılar toohello uygulama, azure'da hello nasıl bkz: [yapılandırma belgelerine](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Merhaba kullanıcı Azure toohello uygulamada atanmış onaylarsanız, hello arka uç uygulamasındaki hello kullanıcı yapılandırmasını denetleyin. Kerberos Kısıtlı temsilci/tümleşik Windows kimlik doğrulaması kullanıyorsanız, bazı yönergeler KCD sorun giderme sayfamızı görebilirsiniz.

## <a name="check-hello-applications-internal-url"></a>Merhaba uygulamanın iç URL'yi denetleyin

İlk hızlı bir adım olarak, çift onay denetleyin ve hello uygulaması aracılığıyla açarak hello İç URL düzeltme **kurumsal uygulamalar**, hello seçtikten sonra **uygulama proxy'si** menüsü. Bu hello doğru İç URL, şirket içi ağ tooaccess hello uygulamanızdan kullanılan hello olduğunu doğrulayın.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Merhaba uygulama bağlayıcısı Grup çalışma tooa atandığından emin olun

tooverify hello uygulama bağlayıcısı Grup çalışma tooa atanır:

1.  Açık Merhaba uygulaması hello Portalı'nda çok giderek**Azure Active Directory**, üzerinde tıklatmak **kurumsal uygulamalar**, ardından **tüm uygulamaları.** Merhaba uygulaması açın ve sonra seçin **uygulama proxy'si** hello sol menüden.

2.  Merhaba bağlayıcı grubu alanına bakın. Merhaba grupta etkin bağlayıcılar yoksa, bir uyarı görürsünüz. Tüm uyarılar görmüyorsanız, çok "tüm gerekli bağlantı noktaları Güvenilenler listesine doğrulayın" geçin.

3.  Bu hello ise yanlış bağlayıcı Grup tooselect hello doğru Grup hello açılan kullanın ve artık tüm uyarıları görmek onaylayın. Bu ise hello bağlayıcı grubu hedeflenen, hello uyarı iletisi tooopen hello sayfası Bağlayıcı Yönetimi ile tıklayın.

4.  Buradan, vardır, birkaç yolu toodrill daha fazla:

  * Etkin bir bağlayıcı hello grubuna taşıyın: toothis grubuna ait olması gerekir ve görüş toohello hedef arka uç uygulaması olan bir active bağlayıcısı varsa, atanan hello grubuna hello bağlayıcı taşıyabilirsiniz. toodo, bu nedenle, hello bağlayıcı tıklayın. Merhaba "Bağlayıcı grubu" alanında hello açılan tooselect hello doğru Grup kullanın ve Kaydet'i tıklatın.

  * Bu grup için yeni bir bağlayıcı indirin: Bu sayfadan hello bağlantı çok alabileceğiniz[yeni bir bağlayıcı indirin](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). toobe doğrudan görüş toohello arka uç uygulaması olan bir makinede yüklü ve genellikle yerleştirildiği hello bağlayıcı gereksinimlerini Merhaba uygulaması aynı sunucuya hello. Kullanım hello Bağlayıcısı bağlantı toodownload hello hedef makine üzerine bir bağlayıcı indirin. Ardından, hello bağlayıcı tıklayın ve hello "Bağlayıcı grubu" açılan toomake toohello sağ grubuna ait olduğundan emin kullanın.

  * Etkin olmayan bir bağlayıcı araştırın: bağlayıcıyı devre dışı olarak gösteriliyorsa, oluşturulamıyor tooreach hello hizmetidir. Bu genellikle toosome gerekli bağlantı noktaları engellenme olur. toosolve Bu sorun, çok "doğrulayın tüm gerekli bağlantı noktalarının Güvenilenler listesine" taşıma.

Bu adımları kullandıktan sonra tooensure hello uygulama bağlayıcıları, test hello uygulamayı yeniden çalışma ile atanan tooa grubudur. Hala çalışmıyorsa toohello sonraki bölümde devam edin.

## <a name="check-all-required-ports-are-whitelisted"></a>Tüm gerekli bağlantı noktalarının Güvenilenler listesine olduğunu denetleyin

gerekli tüm bağlantı noktaları açıktır tooverify bağlantı noktaları açma belgelerimize bakın. Tüm gerekli hello bağlantı noktalarının açık olduğunu, toohello sonraki bölümde taşıyın.

## <a name="check-for-other-connector-errors"></a>Diğer bağlayıcı hataları denetle

Yukarıdaki hello hiçbiri hello sorunu gidermezse, hello sonraki toolook sorunları veya hatalar hello bağlayıcının kendisi ile adımdır. Merhaba bazı yaygın hatalar görebilirsiniz [sorun giderme belge](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

Ayrıca, doğrudan hello Connector günlükleri tooidentify hataları da bakabilirsiniz. Bizim hata iletileri pek çok daha özel öneriler düzeltmeler için mümkün tooshare olabilir. tooview hello günlükleri, nasıl görürüm toolearn [bağlayıcılar Belgelerimizi](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Ek çözümler

Yukarıdaki Hello hello sorunu gidermek alamadık, birkaç farklı olası nedenleri vardır. tooidentify hello sorunu:

Uygulamanız yapılandırılmış toouse ise çoklu oturum açma olmadan test hello uygulama tümleşik Windows kimlik doğrulaması (IWA). Aksi durumda, toohello sonraki paragrafı Taşı. Çoklu oturum açma, olmadan toocheck hello uygulamasını açın, uygulamanızın aracılığıyla **kurumsal uygulamalar** ve Git toohello **çoklu oturum açma** menüsü. Değişiklik hello açılan "Tümleşik Windows kimlik doğrulamasını" çok "Azure AD çoklu oturum açma devre dışı". 

Şimdi bir tarayıcı açın ve tooaccess hello uygulamayı yeniden deneyin. Kimlik doğrulaması için istenir ve hello uygulamasına alın. Bu çalışırsa, hello hello çoklu oturum açmayı etkinleştirir hello Kerberos Kısıtlı temsilci (KCD) yapılandırmayla sorunudur. bkz: Merhaba KCD sorun giderme sayfası.

Toosee hello hata devam ederseniz, burada bağlayıcı yüklü hello açmak hello uygulama için kullanılacak bir tarayıcı ve girişimi tooreach hello İç URL toohello makine gidin. Merhaba bağlayıcı hello başka bir istemciden gibi davranan aynı makine. Merhaba uygulaması bağlanamazsa, bu makine yüklenemiyor tooreach Merhaba uygulaması neden olduğunu araştırın veya bir bağlayıcı mümkün tooaccess hello uygulama bir sunucu üzerinde kullanın.

Bu makineden toolook sorunları veya hatalar hello bağlayıcının kendisi ile Merhaba uygulaması erişebiliyorsa. Merhaba bazı yaygın hatalar görebilirsiniz [sorun giderme belge](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). Ayrıca, doğrudan hello Connector günlükleri tooidentify hataları da bakabilirsiniz. Bizim hata iletileri pek çok daha özel öneriler düzeltmeler için mümkün tooshare olabilir. tooview hello günlükleri, nasıl görürüm toolearn [bağlayıcılar Belgelerimizi](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
