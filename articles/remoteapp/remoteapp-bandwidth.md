---
title: "Azure RemoteApp ağ bant genişliği kullanımını aaaEstimate | Microsoft Docs"
description: "Azure RemoteApp koleksiyonları ve uygulamalar için hello ağ bant genişliği gereksinimleri hakkında bilgi edinin."
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
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Azure RemoteApp ağ bant genişliği kullanımını tahmin etme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp hello Uzak Masaüstü Protokolü (RDP) toocommunicate hello Azure Bulut ve kullanıcılarınızın çalışan uygulamalar arasında kullanır. Bu makalede, ağ kullanımı ve potansiyel olarak Azure RemoteApp kullanıcı başına ağ bant genişliği kullanımını değerlendirme tooestimate kullanabileceğiniz bazı temel kılavuz bilgiler verilmektedir.

Kullanıcı başına bant genişliği kullanımını tahmin etme çok karmaşıktır ve birden çok uygulama aynı anda çoklu senaryolarda uygulamalar burada etkileyebilecek ağ bant genişliği kendi talebe dayalı birbirlerinin performans çalıştırmak gerektirir. Uzak masaüstü istemcisini (örneğin, Mac istemci HTML5 istemci karşı) bile hello türü toodifferent bant genişliği sonuçları yol açabilir. Bu zorluklar iş toohelp, biz hello kullanım senaryoları birkaç hello kategorileri tooreplicate gerçek dünya senaryoları bölün. (Merhaba gerçek dünya senaryosu, doğal olarak, bir kategori karışımıdır ve kullanıcı tarafından farklı yerlerde.)

Daha fazla - geçmeden önce RDP iyi tooexcellent deneyimi çoğu kullanım senaryosu için ağlarda 120 ms ve bant genişliği aşağıda gecikme süresi ile tekrar 5 MB sağlar - bu üzerinde RDP'ın özelliği toodynamically temel varsayıyoruz Not Ayarla hello kullanılabilir ağ kullanarak bant genişliği ve hello uygulama bant genişliği gereksinimlerini tahmin. Bu makalede olanlar hello sınırda olduğu senaryolar toounwind başlar ve kullanıcı deneyimi toodegrade başlar "çoğu kullanım senaryosu" toolook gider.

Şimdi makaleleri Etkenler tooconsider, taban çizgisi önerileri ve ne biz bizim tahminleri içermeyen gibi hello Ayrıntılar için aşağıdaki hello göz atın.

* [Nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?](remoteapp-bandwidthexperience.md)
* [Ağ bant genişliği kullanımınızı bazı yaygın senaryolar ile test etme](remoteapp-bandwidthtests.md)
* [Başlangıç saati veya özelliği tootest yoksa hızlı yönergeleri](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Ne biz dahil değil mi?
Testleri ve bizim genel (ve kuşkusuz genel) öneriler önerilen hello incelediğinizde, biz dikkate almaz pek çok etken olduğunu unutmayın. Örneğin, karşıya yükleme ve indirme bant genişliği asimetrik yapısını hello tarafından sağlanan kullanıcı deneyimi zorluklar hello. Çoğu Wi-Fi ağlarına asimetrik yapısını Hello ayrıca hello performans ve hello kullanıcı deneyimini algısına etkiler. Etkileşimli senaryoları için hello aşağı akış trafiği kayıp ses veya video çerçeveleri hello sayısını artırmak ve bu nedenle hello kullanıcı deneyimi akış hello algısı etkisi hello upstream, daha düşük öncelik. Ağ ve belirli kullanım durumu için iyi nedir kendi denemeler toosee çalıştırabilirsiniz.

Aygıt yeniden yönlendirme aşağıdakiler ele rağmen biz bağlı aygıtlar, depolama, yazıcılar, tarayıcılar, web kamera ve diğer USB cihazları gibi nedeni hello ağ trafiğini göz önünde bulundurarak hello bant genişliği etkisini içine sürdü değil. Bu cihazların Merhaba etkisini genellikle hello bant genişliği gereksinimlerini geçici olarak ani ve hello görev tamamlandığında kaybolduktan. Ancak sık yapıldığında, o bant genişliği isteğe bağlı oldukça belirgin olabilir.

Ayrıca bir kullanıcı aşağıdakiler ele değil hello içindeki diğer kullanıcıların etkileyebilir aynı ağ. Örneğin, 100 MB/sn ağ üzerinde 4 K video tüketen bir kullanıcı önemli ölçüde diğer etkileyebilecek kullanıcılar toodo çalışırken, aynı ağ üzerinde hello aynı görevi. Ne yazık ki hello sistem toplama sırasında nasıl gerçekleştireceğini hakkında ortak ya da tümünü kapsayan bir öneri eş zamanlı kullanım toogive giderek daha zor toodetermine hello etkisini alır. Biz diyebilirsiniz şey Protokolü teknolojisini temel hello hello en iyi hello kullanılabilir ağ bant genişliği kullanımını hale getirir, ancak kendi sınırlamalar vardır.

