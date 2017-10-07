---
title: aaaUpgrade tooAzure AD uygulama proxy'si | Microsoft Docs
description: "Hangi proxy Microsoft Forefront ya da birleşik erişim ağ geçidi yükseltme yapıyorsanız en iyi çözümdür seçin."
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
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Uzaktan erişim çözümlerini karşılaştırın

Azure Active Directory Uygulama proxy'si Microsoft sunar iki uzaktan erişim çözümlerinin biridir. Merhaba diğer Web uygulama proxy'si, hello şirket içi sürümü. Bu iki çözümleri Microsoft sunulan önceki ürün değiştirin: Microsoft Forefront Threat Yönetimi ağ geçidi (TMG) ve birleşik erişim ağ geçidi (UAG). Bu makale toounderstand kullanmak nasıl tooeach diğer bu dört çözümlerini karşılaştırın. Hala hello kullananlar TMG veya UAG çözümleri kullanım için bu makale toohelp plan, geçiş tooone hello uygulama proxy'si, kullanın. 


## <a name="feature-comparison"></a>Özellik karşılaştırması

Bu tablo toounderstand kullanmak nasıl tooeach diğer tehdit Yönetimi ağ geçidi (TMG), Unified erişim ağ geçidi (UAG), Web uygulaması Ara sunucusu (WAP) ve Azure AD uygulama proxy'si (AP) karşılaştırın.

| Özellik | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Sertifika kimlik doğrulaması | Evet | Evet | - | - |
| Seçmeli olarak tarayıcı uygulama yayımlama | Evet | Evet | Evet | Evet |
| Ön kimlik doğrulaması ve çoklu oturum açma | Evet | Evet | Evet | Evet | 
| Katman 2/3 güvenlik duvarı | Evet | Evet | - | - |
| İleriye doğru proxy özellikleri | Evet | - | - | - |
| VPN özellikleri | Evet | Evet | - | - |
| Zengin protokol desteği | - | Evet | Evet, HTTP üzerinden çalışıyorsa | Evet, HTTP üzerinden veya Uzak Masaüstü Ağ geçidi üzerinden çalışıyorsa |
| ADFS Ara sunucusu olarak görev yapar | - | Evet | Evet | - |
| Uygulama erişimi için bir portal | - | Evet | - | Evet |
| Yanıt gövdesi bağlantı çevirisi | Evet | Evet | - | Evet | 
| Üst bilgileri ile kimlik doğrulaması | - | Evet | - | Evet, PingAccess ile | 
| Bulut ölçekli güvenlik | - | - | - | Evet | 
| Koşullu erişim | - | Evet | - | Evet |
| Merhaba sivil bölge (DMZ) herhangi bir bileşeni | - | - | - | Evet |
| Hiçbir gelen bağlantıları | - | - | - | Evet |

Çoğu senaryoda, hello modern çözümü olarak Azure AD uygulaması öneririz. Web uygulama proxy'si, AD FS için bir proxy sunucu gerektiren, tercih edilen senaryolar ve Azure Active Directory'de özel etki alanları kullanamazsınız. 

Azure AD uygulama proxy'si sunar benzersiz avantaj ne zaman gibi toosimilar ürünleri karşılaştırıldığında:

- Azure AD'yi tooon içi genişletme
   - Bulut ölçekli güvenlik ve koruma
   - Kolay tooenable koşullu erişim ve çok faktörlü kimlik doğrulaması gibi özellikleri olan
- Merhaba sivil bölge içinde hiçbir componenet
- Gerekli gelen bağlantı
- Kullanıcılarınızın O365 dahil olmak üzere tüm uygulamalarını, toofor gidin, Azure AD SaaS uygulamalarında tümleşik ve şirket içi web uygulamaları bir erişim paneli. 


## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD uygulaması tooprovide güvenli uzaktan erişim tooon içi uygulamaları kullanın](active-directory-application-proxy-get-started.md)
- [Forefront TMG ve UAG tooApplication Proxy geçişi](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
