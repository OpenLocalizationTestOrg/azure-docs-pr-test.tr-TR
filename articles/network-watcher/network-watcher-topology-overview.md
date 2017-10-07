---
title: "Azure Ağ İzleyicisi'ni de aaaIntroduction tootopology | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi topoloji özelliklerine genel bakış sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Azure Ağ İzleyicisi'ni de giriş tootopology

Topoloji, bir sanal ağ ağ kaynaklarının bir grafik döndürür. Merhaba grafikte hello bağlantısı hello kaynakları toorepresent hello son tooend ağ bağlantısı arasında gösterilmektedir.

![Topoloji genel bakış][1]

Merhaba Portalı'nda topoloji hello kaynak nesneleri döndürür bir sanal ağ temelinde. Merhaba kaynak grubu görüntülenmeyecek olsa bile hello Ağ İzleyicisi bölgesi dışında hello kaynakları kaynakları arasındaki çizgilerle hello ilişkileri gösterilen. Merhaba portal görünümünde döndürülen hello kaynakları grafiği çizilecek hello ağ bileşenleri bir alt kümesidir. ağ kaynakları toosee hello tam listesini kullanabilir [PowerShell](network-watcher-topology-powershell.md) veya [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Ağ İzleyicisi örneği toorun topoloji istediğiniz her bir bölge gereklidir.

Kaynakları hello bağlantı aralarında döndürülür gibi altında iki ilişki Modellenen.

- **Kapsama** -örnek: sanal ağ, bir NIC içeren bir alt ağ içerir
- **İlişkili** -örnek: bir NIC VM ile ilişkili

### <a name="next-steps"></a>Sonraki adımlar

Nasıl toouse PowerShell tooretrieve hello topolojisini görüntülemek ziyaret ederek bilgi [PowerShell ile Ağ İzleyicisi topolojisi](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
