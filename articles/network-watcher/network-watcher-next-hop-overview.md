---
title: "Azure Ağ İzleyicisi aaaIntroduction toonext atlama | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi'ne genel bakış sonraki atlama yeteneği sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Azure Ağ İzleyicisi giriş toonext atlama

Bir VM'ye gelen trafiği tooa hedef bir NIC ile ilişkili hello etkili rotalarını göre gönderilir Sonraki atlama hello sonraki atlama türü ve IP adresi bir paket için bir belirli bir sanal makine ve NIC alır Bu hello paket yönlendirilmiş toohello hedef yüklenmekte olan veya siyah olan hello trafiği holed toodetermine yardımcı olur. Rotaların trafik yönlendirilmiş tooan şirket içi konumu veya bir sanal gereç olduğu hello kullanıcı tarafından hatalı bir yapılandırma tooconnectivity sorunları yol açabilir. Sonraki atlama ayrıca hello sonraki atlama ile ilişkili hello yol tablosu döndürür. Bu rota Hello rota kullanıcı tanımlı bir yol olarak tanımlanırsa, bir sonraki atlama sorgulanırken döndürülür. Aksi takdirde sonraki atlama "Sistem yolu" döndürür.

![sonraki atlama genel bakış][1]

Merhaba, sonraki atlama sorgulanırken döndürülebilecek hello sonraki atlama türlerini listesi verilmiştir.

* Internet
* Değerinin VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>Sonraki adımlar

Nasıl toouse sonraki atlama toofind ziyaret ederek ile ağ bağlantısı sorunları öğrenmek [bir VM'de onay hello sonraki atlama](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













