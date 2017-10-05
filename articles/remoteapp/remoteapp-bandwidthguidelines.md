---
title: "Azure RemoteApp ağ bant genişliği - genel yönergeleri | Microsoft Docs"
description: "Azure RemoteApp koleksiyonları ve uygulamalar için bazı temel ağ bant genişliği yönergeleri anlayın."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Saati veya çalıştırmak için özelliği yoksa [ağ bant genişliği testleri](remoteapp-bandwidthtests.md) Azure RemoteApp için kullanıcı başına ağ bant genişliğini tahmin etmenize yardımcı olabilecek bazı oldukça genel yönergeler aşağıda verilmiştir.

Bu senaryolar karışımı varsa, hiçbir şey küçük (veya eşittir) öneririz olmayan uzak bir ortamda Internet'e bağlı modern uygulamalar için en düşük ağ bant genişliği olarak 10 MB/sn. (Açıklandığı gibi bu daha iyi garanti değil de, ortalama kullanıcı deneyimi daha.)

## <a name="complex-powerpoint-simple-powerpoint"></a>Karmaşık PowerPoint, basit PowerPoint
Azure RemoteApp en iyi 100 MB LAN'da yapar. 10 MB/sn ağ profilde 120 ms yukarıda değişim birden fazla % 5, olduğunda kullanıcı ortalama bir deneyim görürsünüz. Çerçeve atlandığından farklı - Örneğin, bir slayt gösterisi glaring 1 MB/s kullanıcı animasyonlu geçişler hiç göremeyebilirsiniz.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, karma PDF, PDF, metni
10 MB/sn ağ yakın LAN birçok yönden profilidir. Olabilir ancak bazı değişim ekranda görüntüleri durumdayken bir kullanıcı kaydırdığında 1 MB/sn Tamam bir deneyim sağlar.

## <a name="flash-video-youtube"></a>Flash video (YouTube)
10 MB/sn (kare hızıyla takip edin ancak artar değişimi kabul edilebilir anlamına gelir) durumdayken 100 MB/sn LAN en iyi deneyimi sağlar. 1 MB/sn'ye değişim çok yüksek ve fark.

## <a name="word-typing-word-remote-input"></a>Word yazarak (Word uzak giriş)
Düşük bant genişliği kullanım senaryosu budur. 256 KB/sn'ye kadar iyi bir deneyim LAN olarak sunuyoruz.

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Azure RemoteApp ağ bant genişliği kullanımını tahmin etme](remoteapp-bandwidth.md)
* [Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting bazı yaygın senaryolar ile ağ bant genişliği kullanımı](remoteapp-bandwidthtests.md)

