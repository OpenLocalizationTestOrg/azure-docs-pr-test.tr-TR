---
title: "aaaAzure CLI örnekleri | Microsoft Docs"
description: "Azure CLI örnekleri"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Ağ iletişimi için Azure CLI örnekleri

Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure CLI kullanarak oluşturulan komut dosyalarını içerir.

| | |
|-|-|
|**Azure kaynakları arasında bağlantı**||
| [Çok katmanlı uygulamalar için bir sanal ağ oluşturma](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur. Trafik toohello ön uç alt sınırlı tooHTTP ve SSH, trafik toohello sırasında arka uç alt sınırlı tooMySQL, bağlantı noktası 3306. |
| [Eş iki sanal ağlar](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Oluşturur ve iki sanal ağlarda hello bağlanır aynı bölgede. |
| [Bir ağ sanal gereç yoluyla trafiği yönlendirme](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Ön uç ve arka uç alt ağları ve mümkün tooroute trafiği hello iki alt ağlar arasında bir VM sanal ağ oluşturur. |
| [Gelen ve giden VM ağ trafiği filtreleme](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur. Gelen ağ trafiğini toohello ön uç alt sınırlı tooHTTP, HTTPS ve SSH değil. Merhaba arka uç alt ağından giden trafiği toohello Internet izin verilmez. |
|**Yük Dengeleme ve trafik yönü**||
| [Bakiye trafiği tooVMs yüksek kullanılabilirlik için yük](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur. |
| [Yük Dengelemesi birden çok Web sitesi vm'lerinde](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Birden çok IP yapılandırmaları, birleştirilmiş tooan Azure kullanılabilirlik kümesi, bir Azure yük dengeleyici erişilebilir olan iki VM'ler oluşturur. |
| [Uygulama yüksek kullanılabilirlik için birden çok bölgede doğrudan trafiği](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  İki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur. |
| | |
