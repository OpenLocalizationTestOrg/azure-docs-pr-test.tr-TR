---
title: "Cloud App Discovery ile yönetilmeyen bulut uygulamaları bulma | Microsoft Docs"
description: "Bulma ve Cloud App Discovery, avantajları nelerdir ve nasıl çalıştığı ile uygulamaları yönetme hakkında bilgi sağlar."
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Cloud App Discovery ile bulma yönetilmeyen bulut uygulamaları
## <a name="overview"></a>Genel Bakış
Modern kuruluşlarda, BT departmanları işlerini yapmak için kuruluşları üyeleri kullanan tüm bulut uygulamaları tanımaz genellikle. Yöneticileri Kurumsal verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine yetkisiz erişimi endişeniz neden olurdu görmek kolaydır. Bu tanıma olmaması, bu güvenlik riskleri postalarla göründüğü için göz korkutucu bir plan oluşturma yapabilirsiniz.

Cloud App Discovery, kuruluşunuzdaki kişiler tarafından kullanılan bulut uygulamalarını keşfetmek sağlayan Azure Active Directory (AD) Premium özelliğidir.

**Cloud App Discovery ile şunları yapabilirsiniz:**

* Kullanılan bulut uygulamalarını bulmak ve bu kullanım ölçme kullanıcı sayısı, akış hacmine veya uygulamaya web isteklerinin sayısı.
* Bir uygulama kullanarak kullanıcıları belirleyin.
* Çevrimdışı analiz için verileri dışa aktarın.
* Bu uygulamalar BT denetimindeki getirin ve kullanıcı yönetimi için çoklu oturum açmayı etkinleştirme.

## <a name="how-it-works"></a>Nasıl çalışır?
1. Uygulama kullanımı aracıları kullanıcının bilgisayarlara yüklenir.
2. Aracıları tarafından yakalanan uygulama kullanım bilgilerini bulut uygulama bulma hizmeti için güvenli, şifrelenmiş bir kanal üzerinden gönderilir.
3. Cloud App Discovery hizmetine veri değerlendirir ve raporları oluşturur.

![Cloud App Discovery diyagramı](./media/active-directory-cloudappdiscovery/cad01.png)

Cloud App Discovery'yi kullanmaya başlamak için bkz: [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>İlgili makaleler
* [Cloud App Discovery güvenlik ve gizlilik konuları](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Cloud App Discovery Grup İlkesi Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Cloud App Discovery System Center Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Özel bağlantı noktaları ile Proxy sunucuları için bulut uygulama bulma kayıt defteri ayarları](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery Aracısı değişim günlüğü](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Cloud App Discovery sık sorulan sorular](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

