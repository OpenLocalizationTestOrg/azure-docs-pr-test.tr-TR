---
title: "Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz? | Microsoft Belgeleri"
description: "Azure RemoteApp ağ bant genişliği kullanıcınızın kalitesinden nasıl etkileyebileceğini öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 74116902e973fba440b3c662fdf76202d052b4c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Ne zaman, arıyor adresindeki [genel ağ bant genişliği](remoteapp-bandwidth.md) Azure RemoteApp için gerekli, aşağıdaki etkenleri göz önünde bulundurmanız - bunlar tüm genel kullanıcı deneyimi etkiler dinamik bir sistem parçasıdır. 

* **Kullanılabilir ağ bant genişliği ve geçerli ağ koşulları** -parametreleri (kaybı, gecikme, değişim) belirli bir zamanda aynı ağ üzerinde bir dizi akış deneyimi, bir alçaltılmış genel kullanıcı deneyimi anlamı uygulama etkileyebilir. Bu parametreler Tıkanıklık denetimi mekanizması, buna denetimleri kapatma çakışmaları önlemek için aktarım hızı etkilediğinden, ağınızda kullanılabilir bant genişliği Tıkanıklığı, rastgele kaybı, gecikme işlevdir.  Örneğin, bir kayıplı veya ağı yüksek gecikme süresi ile kullanıcı deneyimini hatalı 1000 MB bant genişliğine sahip bir ağda bile hale getirir. Kaybı ve gecikme süresi aynı ağ ve bu kullanıcıların (örneğin indirilirken veya yazdırma büyük dosyaları karşıya yükleme videoları izlerken) ne yaptıklarını olan kullanıcı sayısına göre değişir.
* **Kullanım senaryosu** -kullanıcıların kişiler ve aynı ağ üzerinde bir grup olarak gerçekleştirdiği üzerinde deneyimi bağlıdır. Örneğin, bir slayt okunurken yalnızca tek kare güncelleştirilmesi gerekir; Kullanıcı skims ve bir metin belgesi içerik üzerinde birlikte kayar çerçeveler saniyede güncelleştirilmesi daha yüksek bir sayı ihtiyaç duyar. Bu senaryoda bir sunucuya geri ve İleri iletişimi sonunda daha fazla ağ bant genişliği kullanır. Ayrıca aşırı örneği göz önünde bulundurun: birden çok kullanıcı (4 K çözünürlük gibi) yüksek tanımlı videoları izlerken, HD konferans aramaları tutan, 3D video oyunlar oynamak veya CAD sistemlerde çalışma. Bunların tümü bile gerçekten yüksek bant genişliğine sahip ağ pratikte kullanılamaz hale getirebilir.
* **Ekran çözünürlüğü ve ekran sayısını** -daha fazla ağ bant genişliğini daha küçük ekranlar daha büyük filtrelerine tam güncelleştirme gerekli değildir. Temel alınan teknoloji kodlamak ve yalnızca güncelleştirilmiş ekranlar bölgeler iletmek oldukça iyi bir işi yapar ancak zaman, tüm ekranı güncelleştirilmesi gerekiyor. Kullanıcı daha yüksek çözünürlüklü ekran (örneğin 4 K çözünürlük) sahip olduğunda bu güncelleştirmeyi daha fazla ağ bant genişliği düşük çözünürlüklü (1024x768px gibi) bir ekran gerektirir. Yeniden yönlendirme için birden fazla ekran kullanırsanız, bu aynı mantığı uygular. Ekranlar sayısını artırmak bant genişliği gerekiyor.
* **Pano ve aygıt yeniden yönlendirme** - bu çok belirgin bir sorundur ancak birçok durumda kullanıcı Pano verilerinin büyük bir öbek depoluyorsa biraz zaman Uzak Masaüstü istemciden sunucuya aktarmak bu bilgileri sürer. Aşağı Akış deneyimi Pano içeriği upstream gönderirken deneyimi tarafından etkilenebilir. Bir tarayıcı veya web kamerası çok Yukarı Akış sunucusuna gönderilmesi gerekir veri üreten aynı için aygıt yeniden yönlendirmeyi - geçerlidir veya büyük bir belgeyi almak bir yazıcı gerekiyor veya yerel depolama büyük bir dosya kopyalamak için bulutta çalışan bir uygulama için kullanılabilir olması gerekir , kullanıcıların Atlanan çerçeveler fark veya geçici olarak "dondurulmuş" video aygıtı yeniden yönlendirme için gereken verileri ağ bant genişliğini artırmak için gerekiyor. 

Ağ bant genişliği gereksinimlerinizi değerlendirirken, tüm sistem olarak çalışan Bu faktör dikkate alınması gereken emin olun.

Şimdi, geri dönüp [ana ağ bant genişliği makale](remoteapp-bandwidth.md), ya da test yapmaya geçin, [ağ bant genişliği](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure RemoteApp ağ bant genişliği kullanımını tahmin etme](remoteapp-bandwidth.md)
* [Azure RemoteApp - bazı yaygın senaryolar ile ağ bant genişliği kullanımını test etme](remoteapp-bandwidthtests.md)
* [Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri](remoteapp-bandwidthguidelines.md)

