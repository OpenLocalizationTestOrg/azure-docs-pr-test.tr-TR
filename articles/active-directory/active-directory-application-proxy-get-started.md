---
title: "aaaHow tooprovide güvenli uzaktan erişim tooon içi uygulamalar"
description: "Nasıl toouse Azure AD uygulama proxy'si tooprovide güvenli uzaktan erişim tooyour uygulamaları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamalar

Çalışanlar bugün toobe üretken herhangi bir noktada herhangi bir zamanda ve herhangi bir CİHAZDAN istiyor. Kendi cihazlarda toowork tabletler, telefon veya dizüstü bilgisayarlar olmaları olup olmadığını isterler. Ve toobe mümkün tooaccess kendi uygulamaları SaaS uygulamaları hello bulutta ve şirket uygulamalarını şirket içi bekledikleri. Tooon içi uygulamalara erişim sağlayarak geleneksel sanal özel ağlar (VPN) veya sivil bölge (DMZ'ler) dahil. Yalnızca bu çözümleri karmaşık ve sabit toomake güvenlidir, ancak pahalı tooset çalıştığından ve yönetme.

Daha iyi bir yolu yoktur!

Modern iş gücü hello mobil-ilk bulut ilk world modern uzaktan erişim çözümü gerekir. Azure AD uygulama proxy'si, bir hizmet olarak uzaktan erişim sunar Azure Active Directory özelliğidir. Kolay toodeploy olduğu anlamına gelir, kullanın ve yönetin.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Azure Active Directory Uygulama proxy'si nedir?
Çoklu oturum açma (SSO) Azure AD uygulama proxy'si sağlar ve şirket içi web uygulamaları için güvenli uzaktan erişim barındırılır. Bazı uygulamalar toopublish istersiniz, SharePoint siteleri, Outlook Web Access veya sahip olduğunuz diğer iş KOLU web uygulamaları içerir. Bu şirket içi web uygulamaları Azure AD ile tümleşik aynı kimlik hello ve O365 tarafından kullanılan platform denetleyebilirsiniz. Son kullanıcılar, şirket içi uygulamalar hello O365 ve diğer SaaS uygulamaları eriştiklerinde aynı şekilde Azure AD ile tümleşik erişebilir. Toochange hello ağ altyapısına ihtiyacınız olmayan ya da VPN tooprovide kullanıcılarınız için bu çözümü gerektirir.

## <a name="why-is-application-proxy-a-better-solution"></a>Neden daha iyi bir çözüm uygulama proxy'si mi?
Azure AD uygulama proxy'si, şirket içi uygulamalarınızı uzaktan erişim basit, güvenli ve uygun maliyetli bir çözüm tooall sağlar.

Azure AD uygulama proxy'si şöyledir:

* **Basit**
   * Toochange gerek yoktur veya uygulamaları toowork uygulama ara sunucusu ile güncelleştirin. 
   * Kullanıcılarınız tutarlı kimlik doğrulaması deneyimi alır. Merhaba MyApps portal tooget çoklu oturum açma tooboth SaaS uygulamalarında hello Bulut ve uygulamaları şirket içi kullanabilirler. 
* **Güvenlik**
   * Azure AD uygulama proxy'si kullanarak uygulamalarınızı yayımladığınızda, Azure'da hello zengin yetkilendirme denetimleri ve güvenlik analizleri avantajlarından yararlanabilirler. Bulut ölçekli güvenlik ve koşullu erişim ve iki aşamalı doğrulama gibi Azure güvenlik özellikleri alır.
   * Güvenlik Duvarı toogive tüm gelen bağlantıları tooopen yoksa, kullanıcıların uzaktan erişim. 
* **Uygun maliyetli**
   * Saat ve para kaydedebilmeniz için uygulama proxy'si hello bulutta çalışır. Şirket içi çözümler genellikle yukarı tooset gerektirir ve DMZ'ler, uç sunucuların veya diğer karmaşık altyapıları.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Ne tür bir uygulama proxy'si ile uygulama iş?
Azure AD uygulama proxy'si ile dahili uygulama farklı türlerine erişebilir:

* Web kullanan uygulamalar [tümleşik Windows kimlik doğrulaması](active-directory-application-proxy-sso-using-kcd.md) kimlik doğrulaması  
* Web form tabanlı kullanan uygulamalar veya [başlığa göre](application-proxy-ping-access.md) erişim  
* Web tooexpose toorich uygulamaları farklı cihazlarda istediğiniz API'leri  
* Barındırılan uygulamalara arkasındaki bir [Uzak Masaüstü Ağ Geçidi](application-proxy-publish-remote-desktop.md)  
* Active Directory Authentication Library (ADAL) hello ile tümleşik zengin istemci uygulamaları

## <a name="how-does-application-proxy-work"></a>Uygulama proxy'si nasıl çalışır?
Uygulama proxy'si iş tooconfigure toomake gereken iki bileşeni vardır: bir bağlayıcı ve dış uç noktası. 

Merhaba, ağınızdaki Windows Server'da bulunur basit bir aracı Bağlayıcıdır. Merhaba bağlayıcı hello trafiği hello hello bulut tooyour uygulama şirket içi uygulama proxy'si hizmetinde akışından kolaylaştırır. Gelen bağlantı noktalarının tooopen sahip yok veya hiçbir şey hello DMZ'deki put yalnızca giden bağlantılar kullanır. Merhaba bağlayıcılar durum bilgisiz ve gerekirse hello bulut bilgi isteneceğini. Nasıl gibi bağlayıcılar hakkında daha fazla bilgi için Yük Dengeleme ve kimlik doğrulaması, bkz [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md). 

Kullanıcılarınızın uygulamalarınızı sırasında ağ dışında nasıl ulaşmak Hello dış uç noktadır. Bunlar ya da doğrudan saptamanıza tooan dış URL gidebilir veya Merhaba uygulaması hello MyApps portalı üzerinden erişebilirsiniz. Kullanıcılar bu uç noktalar tooone olduğunuzda, Azure AD içinde kimlik doğrulaması ve ardından hello bağlayıcı toohello şirket içi uygulama yönlendirilir.

 ![Azuread'i uygulama proxy'si diyagramı](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. Merhaba kullanıcı hello uygulama proxy'si hizmeti ile Merhaba uygulaması erişir ve yönlendirilmiş toohello Azure AD oturum açma sayfası tooauthenticate.
2. Bir başarılı oturum açma işleminden sonra bir belirteç oluşturulur ve toohello istemci aygıt gönderdi.
3. Merhaba istemci belirteci toohello hello kullanıcı asıl adı (UPN) alır uygulama proxy'si hizmeti hello ve güvenlik asıl adı (SPN) hello belirteci, ardından hello isteği toohello uygulama ara sunucusu Bağlayıcısı yönlendirir gönderir.
4. Çoklu oturum açma yapılandırdıysanız, hello bağlayıcı hello kullanıcı adına gerekli ek kimlik doğrulaması gerçekleştirir.
5. Merhaba bağlayıcı hello isteği toohello şirket içi uygulama gönderir.  
6. Merhaba yanıt uygulama proxy'si hizmeti ve bağlayıcı toohello kullanıcı gönderilir.

### <a name="single-sign-on"></a>Çoklu oturum açma
Azure AD uygulama proxy'si, tümleşik Windows kimlik doğrulaması (IWA) veya talep kullanan uygulamalar kullanmanız çoklu oturum açma (SSO) tooapplications sağlar. Uygulamanızı IWA kullanıyorsa, uygulama proxy'si hello kullanıcı Kerberos Kısıtlı temsilci tooprovide SSO kullanılarak temsil eder. Azure Active Directory güvenleri talep kullanan bir uygulamanız varsa, hello kullanıcı Azure AD tarafından zaten doğrulandı çünkü SSO çalışır.

Kerberos hakkında daha fazla bilgi için bkz: [tüm tooknow Kerberos Kısıtlı temsilci (KCD) hakkında istediğiniz](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Uygulamaları yönetme
Biri, uygulamanızın uygulama ara sunucusu ile yayımlanan, hello Azure portal'ın başka bir kuruluş uygulaması gibi yönetebilirsiniz. Koşullu erişim ve iki aşamalı doğrulama gibi Azure Active Directory güvenlik özellikleri kullanmak, kullanıcı izinlerini denetlemek ve uygulamanız için hello marka özelleştirme. 

## <a name="get-started"></a>başlarken

Uygulama proxy'si yapılandırmadan önce desteklenen bir olduğundan emin olun [Azure Active Directory edition](https://azure.microsoft.com/pricing/details/active-directory/) ve genel Yöneticisi olduğunuz bir Azure AD dizini.

Uygulama proxy'si ile iki adımda başlayın:

1. [Uygulama Ara sunucusunu etkinleştirme ve hello bağlayıcısını](active-directory-application-proxy-enable.md).    
2. [Uygulama yayımlama](active-directory-application-proxy-publish.md) -kullanım hızlı ve kolay sihirbaz tooget uzaktan, şirket içi uygulamalarınızı yayımlanan ve erişilebilir hello.

## <a name="whats-next"></a>Sırada ne var?
İlk uygulamanızı yayımladıktan sonra çok daha uygulama proxy'si ile yapabileceğiniz vardır:

* [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
* [Kendi etki alanı adınızı kullanarak uygulama yayımlama](active-directory-application-proxy-custom-domains.md)
* [Azure AD uygulama proxy'si bağlayıcılar hakkında bilgi edinin](application-proxy-understand-connectors.md)
* [Mevcut şirket içi Proxy sunucuları ile çalışma](application-proxy-working-with-proxy-servers.md) 
* [Özel bir ana sayfa ayarlama](application-proxy-office365-app-launcher.md)

Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)

