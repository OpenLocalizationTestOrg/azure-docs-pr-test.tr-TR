---
title: "RemoteApp - aaaAzure nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz? | Microsoft Belgeleri"
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
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Ne zaman, arıyor hello [genel ağ bant genişliği](remoteapp-bandwidth.md) Azure RemoteApp için gerekli, aşağıdaki faktörleri göz hello tutmak - bunlar tüm etkileri genel kullanıcı deneyimi hello dinamik bir sistem parçasıdır. 

* **Kullanılabilir ağ bant genişliği ve geçerli ağ koşulları** -parametreleri (kaybı, gecikme, değişim) hello belirli bir zamanda aynı ağ üzerinde bir dizi akış deneyimi, bir alçaltılmış genel kullanıcı deneyimi anlamı Merhaba uygulaması etkileyebilir. Bu parametreler, aktarım hızı tooavoid çakışmaları hello Aç denetimlerinde hello Tıkanıklık denetimi mekanizmasını etkilediğinden hello bant genişliği, ağınızda kullanılabilir Tıkanıklığı, rastgele kaybı, gecikme işlevdir.  Örneğin, bir kayıplı veya ağı yüksek gecikme süresi ile Merhaba kullanıcı deneyimini hatalı 1000 MB bant genişliğine sahip bir ağda bile hale getirir. Merhaba kaybı ve gecikme hello üzerinde olan kullanıcılar hello sayısına göre farklılık aynı ağ ve bu kullanıcıların (örneğin indirilirken veya yazdırma büyük dosyaları karşıya yükleme videoları izlerken) ne yaptıklarını.
* **Kullanım senaryosu** -hello deneyimi bağlıdır hangi hello kullanıcıların kişiler ve hello bir grubu olarak aynı yaptıklarını üzerinde ağ. Örneğin, bir slayt okuma yalnızca güncelleştirilmiş bir tek çerçeve toobe gerektirir; Merhaba kullanıcı skims ve bir metin belgesi hello içerik üzerinde birlikte kayar çerçeveler toobe saniyede güncelleştirilmiş daha yüksek bir sayı ihtiyaç duyar. iletişimi geri hello ve İleri Bu senaryoda toohello sunucu daha fazla ağ bant genişliği sonunda tüketir. Ayrıca aşırı örneği göz önünde bulundurun: birden çok kullanıcı (4 K çözünürlük gibi) yüksek tanımlı videoları izlerken, HD konferans aramaları tutan, 3D video oyunlar oynamak veya CAD sistemlerde çalışma. Bunların tümü bile gerçekten yüksek bant genişliğine sahip ağ pratikte kullanılamaz hale getirebilir.
* **Ekran ekran çözünürlüğü ve hello sayısını** -gerekli toofull güncelleştirme büyük ekranlar, küçük ekranlar daha daha fazla ağ bant genişliği kadardır. Merhaba temel alınan teknoloji kodlamak ve yalnızca güncelleştirilmiş hello ekranlar hello bölgelerinin iletmek oldukça iyi bir işi yapar ancak zaman, güncelleştirilmiş toobe hello tam ekran gerekiyor. Merhaba kullanıcı daha yüksek çözünürlüklü ekran (örneğin 4 K çözünürlük) sahip olduğunda bu güncelleştirmeyi daha fazla ağ bant genişliği düşük çözünürlüklü (1024x768px gibi) bir ekran gerektirir. Yeniden yönlendirme için birden fazla ekran kullanırsanız, bu aynı mantığı uygular. Bant genişliği ekranlar hello sayısıyla tooincrease gerekir.
* **Pano ve aygıt yeniden yönlendirme** - bu çok belirgin bir sorundur ancak bir kullanıcı veri toohello Pano, büyük bir öbek depoluyorsa çoğu durumda bu bilgileri tootransfer hello Uzak Masaüstü İstemcisi için zaman bir bit toohello sunucu sürer. Merhaba aşağı akış deneyimi hello Pano içeriği upstream gönderme hello deneyimi tarafından etkilenebilir. Merhaba aynı için aygıt yeniden yönlendirmeyi - tarayıcı geçerlidir veya web kamerası çok gönderilen toobe Yukarı Akış toohello sunucunun gereken veri üreten veya bir yazıcı tooreceive büyük belge gerekiyor veya yerel depolama alanı ihtiyaçlarınızı hello bulut toocopy çalışan toobe kullanılabilir tooan uygulama bir büyük dosya kullanıcıları Atlanan çerçeveler fark veya geçici olarak "dondurulmuş" video hello aygıtı yeniden yönlendirmesi için gereken hello verileri hello ağ bant genişliğini artırmak için gerekiyor. 

Ağ bant genişliği gereksinimlerinizi değerlendirirken, emin tooconsider bir sistem olarak çalışan faktörlerin sağlayın.

Şimdi, toohello geri dönün [ana ağ bant genişliği makale](remoteapp-bandwidth.md), veya üzerinde tootesting taşımak, [ağ bant genişliği](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure RemoteApp ağ bant genişliği kullanımını tahmin etme](remoteapp-bandwidth.md)
* [Azure RemoteApp - bazı yaygın senaryolar ile ağ bant genişliği kullanımını test etme](remoteapp-bandwidthtests.md)
* [Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri](remoteapp-bandwidthguidelines.md)

