---
title: "aaaClaims algılayan uygulamaları - Azure AD uygulaması Proxy | Microsoft Docs"
description: "Nasıl toopublish kullanıcılarınız tarafından güvenli uzaktan erişim için ADFS talep kabul ASP.NET uygulamalarının şirket içi."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Talep kullanan uygulamalarda uygulama proxy'si ile çalışma
[Talep kullanan uygulamalar](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) yeniden yönlendirme toohello güvenlik belirteci hizmeti (STS) gerçekleştirin. Hello STS bir belirteç karşılığında hello kullanıcıdan kimlik bilgilerini ister ve ardından hello kullanıcı toohello uygulaması yönlendirir. Bu yeniden yönlendirmeleri ile birkaç yolu tooenable uygulama proxy'si toowork vardır. Bu makale tooconfigure dağıtımınızı talep kullanan uygulamalar için kullanın. 

## <a name="prerequisites"></a>Ön koşullar
Talep kullanan uygulama hello bu hello STS toois Şirket ağınızın dışında kullanılabilir yönlendiren emin olun. Hello STS kullanılabilir bir proxy üzerinden gösterme veya dışında bağlantılarına izin veren yapabilirsiniz. 

## <a name="publish-your-application"></a>Uygulamanızı yayımlama

1. Açıklanan toohello yönergeleri göre uygulamanızı yayımlamak [uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).
2. Merhaba seçin ve Portalı'nda uygulama sayfası toohello gidin **çoklu oturum açma**.
3. Seçerseniz **Azure Active Directory** olarak, **ön kimlik doğrulama yöntemi**seçin **Azure AD çoklu oturum açma devre dışı özelliğini** olarak, **iç Kimlik doğrulama yöntemini**. Seçerseniz **geçiş** olarak, **ön kimlik doğrulama yöntemi**, toochange herhangi bir şey gerekmez.

## <a name="configure-adfs"></a>ADFS yapılandırın

İki yoldan biriyle talep kullanan uygulamalar için ADFS yapılandırabilirsiniz. Merhaba, özel etki alanlarını kullanarak önce gerçekleşir. Merhaba, WS-Federasyon ile ikinci olur. 

### <a name="option-1-custom-domains"></a>Seçenek 1: Özel etki alanları

Uygulamalarınızı tam için tüm dahili URL Merhaba, etki alanı adları (FQDN), sonra yapılandırabileceğiniz [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) uygulamalarınız için. İç URL'leri hello aynı hello kullan hello özel etki alanlarını toocreate harici URL. Ardından, dış URL'ler iç URL'nizde eşleştiğinde, kullanıcılarınızın şirket içi veya uzak olup hello STS yeniden yönlendirme çalışır. 

### <a name="option-2-ws-federation"></a>Seçenek 2: WS-Federasyon

1. ADFS Yönetimi'ni açın.
2. Çok Git**bağlı olan taraf güvenleri**uygulama ara sunucusu ile yayımlıyorsa hello uygulama sağ tıklatın ve seçin **özellikleri**.  

   ![Bağlı olan taraf güvenleri sağ uygulama adı - ekran görüntüsü](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Merhaba üzerinde **uç noktaları** sekmesinde, altında **uç nokta türü**seçin **WS-Federasyon**.
4. Altında **güvenilen URL**, uygulama proxy'si altında hello girilen hello URL'sini girin **dış URL** tıklatıp **Tamam**.  

   ![Bir uç nokta - ekleyin güvenilen URL değeri - ekran görüntüsü Ayarla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Sonraki adımlar
* [Çoklu oturum açmayı etkinleştir](application-proxy-sso-overview.md) talep kullanan olmayan uygulamalar için
* [Yerel istemci uygulamaları toointeract proxy uygulamalarla etkinleştir](active-directory-application-proxy-native-client.md)


