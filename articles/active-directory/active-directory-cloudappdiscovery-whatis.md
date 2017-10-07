---
title: "aaaFinding yönetilmeyen bulut uygulamaları Cloud App Discovery ile | Microsoft Docs"
description: "Bulma ve Cloud App Discovery, hello avantajları nelerdir ve nasıl çalıştığı ile uygulamaları yönetme hakkında bilgi sağlar."
services: active-directory
keywords: "cloud app discovery'yi, uygulamaları yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Cloud App Discovery ile bulma yönetilmeyen bulut uygulamaları
## <a name="overview"></a>Genel Bakış
Modern kuruluşlarda, BT departmanları kuruluşu üyelerini işlerine toodo kullanmak tüm hello bulut uygulamaları tanımaz genellikle. Yöneticiler yetkisiz erişim toocorporate verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine endişeniz neden olurdu kolay toosee olur. Bu tanıma olmaması, bu güvenlik riskleri postalarla göründüğü için göz korkutucu bir plan oluşturma yapabilirsiniz.

Cloud App Discovery, kuruluşunuzda hello kişiler tarafından kullanılan toodiscover bulut uygulamalarını sağlayan Azure Active Directory (AD) Premium özelliğidir.

**Cloud App Discovery ile şunları yapabilirsiniz:**

* Kullanılan hello bulut uygulamalarını bulmak ve bu kullanım kullanıcı sayısı, trafik veya web istekleri toohello uygulama sayısı birim göre ölçün.
* Bir uygulama kullanarak hello kullanıcıları belirleyin.
* Çevrimdışı analiz için verileri dışa aktarın.
* Bu uygulamalar BT denetimindeki getirin ve kullanıcı yönetimi için çoklu oturum açmayı etkinleştirme.

## <a name="how-it-works"></a>Nasıl çalışır?
1. Uygulama kullanımı aracıları kullanıcının bilgisayarlara yüklenir.
2. Merhaba uygulama kullanım bilgilerini Hello aracıları tarafından yakalanan bir güvenli ve şifrelenmiş bir kanal toohello bulut uygulama bulma hizmeti gönderilir.
3. Merhaba Cloud App Discovery hizmetine hello veri değerlendirir ve raporları oluşturur.

![Cloud App Discovery diyagramı](./media/active-directory-cloudappdiscovery/cad01.png)

cloud App Discovery ile başlatılan tooget bakın [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>İlgili makaleler
* [Cloud App Discovery güvenlik ve gizlilik konuları](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Cloud App Discovery Grup İlkesi Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Cloud App Discovery System Center Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Özel bağlantı noktaları ile Proxy sunucuları için bulut uygulama bulma kayıt defteri ayarları](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery Aracısı değişim günlüğü](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Cloud App Discovery sık sorulan sorular](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

