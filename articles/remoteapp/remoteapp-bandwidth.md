---
title: "Azure RemoteApp ağ bant genişliği kullanımını tahmin | Microsoft Docs"
description: "Azure RemoteApp koleksiyonları ve uygulamalar için ağ bant genişliği gereksinimleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 16b4ba974742d004ea02e3f83e522b9c43f2ef40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Azure RemoteApp ağ bant genişliği kullanımını tahmin etme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp, Uzak Masaüstü Protokolü (RDP) Azure Bulutu ve kullanıcılarınızın çalışan uygulamalar arasında iletişim kurmak için kullanır. Bu makalede, bu ağ kullanımını tahmin ve büyük olasılıkla ağ bant genişliği kullanımını Azure RemoteApp kullanıcı başına değerlendirmek için kullanabileceğiniz bazı temel yönergeler sağlar.

Kullanıcı başına bant genişliği kullanımını tahmin etme çok karmaşıktır ve birden çok uygulama aynı anda çoklu senaryolarda uygulamalar burada etkileyebilecek ağ bant genişliği kendi talebe dayalı birbirlerinin performans çalıştırmak gerektirir. Uzak masaüstü istemcisini (örneğin, Mac istemci HTML5 istemci karşı) bile türünü farklı bant genişliği sonuçlara yol açabilir. Bu zorluklar çalışmanıza yardımcı olmak için biz kullanım senaryoları kategorilerinin birkaçı, gerçek dünya senaryoları çoğaltmak için ortak bölün. (Gerçek dünya senaryosu, doğal olarak, bir kategori karışımıdır ve kullanıcı tarafından farklı yerlerde.)

Daha fazla - geçmeden önce RDP mükemmel deneyimi için iyi bir çoğu kullanım senaryosu için ağlarda 120 ms ve bant genişliği aşağıda gecikme süresi ile tekrar 5 MB sağlar - bu RDP'ın kullanılabilir ağ bant genişliği ve tahmini uygulama bant kullanarak dinamik olarak ayarlamasını yeteneği dayanır varsayıyoruz Not gerekir. Bu makalede olanlar "çoğu kullanım senaryosu" gider sınırında olduğu senaryolar bırakma başlar ve kullanıcı deneyimi başlar düşmeye aramak için.

Şimdi dikkat edilecek noktalar dahil olmak üzere, Ayrıntılar için aşağıdaki makalelere taban çizgisi önerileri ve ne biz bizim tahminleri içermeyen göz atın.

* [Nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?](remoteapp-bandwidthexperience.md)
* [Ağ bant genişliği kullanımınızı bazı yaygın senaryolar ile test etme](remoteapp-bandwidthtests.md)
* [Saat veya test olanağı yoksa hızlı yönergeleri](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Ne biz dahil değil mi?
Önerilen testleri ve bizim genel (ve kuşkusuz genel) önerileri gözden geçirirken, biz dikkate almaz pek çok etken olduğunu unutmayın. Örneğin, karşıya yükleme asimetrik yapısını tarafından sağlanan kullanıcı deneyimi zorluklar bant genişliği indirin. Çoğu Wi-Fi ağlarına asimetrik yapısını ayrıca performans ve kullanıcı deneyimi algısına etkiler. Etkileşimli senaryoları için aşağı akış trafiği Yukarı Akış, kayıp ses veya video çerçeve sayısını artırmak ve bu nedenle akış deneyimi kullanıcı algısı etkisi daha düşük öncelik. Ağ ve belirli kullanım durumu için iyi görmek için kendi denemeler çalıştırabilirsiniz.

Aygıt yeniden yönlendirme aşağıdakiler ele rağmen biz bağlı aygıtlar, depolama, yazıcılar, tarayıcılar, web kamera ve diğer USB cihazları gibi nedeni ağ trafiği bant genişliğini etkisini dikkate değil. Bu cihazlar etkisini genellikle bant genişliği gereksinimlerini geçici olarak ani ve görev tamamlandığında kaybolduktan. Ancak sık yapıldığında, o bant genişliği isteğe bağlı oldukça belirgin olabilir.

Ayrıca bir kullanıcı aşağıdakiler ele değil aynı ağ içindeki diğer kullanıcıların etkileyebilir. Örneğin, 100 MB/sn ağ üzerinde 4 K video tüketen bir kullanıcı aynı görevi gerçekleştirmenin çalışırken, aynı ağ üzerindeki diğer kullanıcılarla önemli ölçüde etkileyebilir. Ne yazık ki sistem toplama sırasında nasıl yapar hakkında ortak ya da tümünü kapsayan bir öneri vermek için eşzamanlı kullanım etkisini belirlemek zor aşamalı olarak alır. Biz diyebilirsiniz şey temel Protokolü teknoloji kullanılabilir ağ bant genişliği kullanımını en iyi hale getirir, ancak kendi sınırlamalar vardır.

