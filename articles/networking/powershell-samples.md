---
title: "aaaAzure PowerShell örnekleri | Microsoft Docs"
description: "Azure PowerShell örnekleri"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a>Ağ iletişimi için Azure PowerShell örnekleri

Merhaba aşağıdaki tabloda Azure PowerShell kullanarak yerleşik bağlantılar tooscripts içerir.

| | |
|-|-|
|**Azure kaynakları arasında bağlantı**||
| [Çok katmanlı uygulamalar için bir sanal ağ oluşturma](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur. Trafik toohello ön uç alt sınırlı tooHTTP, trafik toohello sırasında arka uç alt sınırlı tooSQL, bağlantı noktası 1433. |
| [Eş iki sanal ağlar](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Oluşturur ve iki sanal ağlarda hello bağlanır aynı bölgede. |
| [Bir ağ sanal gereç yoluyla trafiği yönlendirme](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Ön uç ve arka uç alt ağları ve mümkün tooroute trafiği hello iki alt ağlar arasında bir VM sanal ağ oluşturur. |
| [Gelen ve giden VM ağ trafiği filtreleme](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Bir sanal ağ ile ön uç ve arka uç alt ağlar oluşturur. Gelen ağ trafiğini toohello ön uç alt ağıdır sınırlı tooHTTP ve HTTPS... Merhaba arka uç alt ağından giden trafiği toohello Internet izin verilmez. |
|**Yük Dengeleme ve trafik yönü**||
| [Bakiye trafiği tooVMs yüksek kullanılabilirlik için yük](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Birkaç yüksek oranda kullanılabilir sanal makineleri ve yükü dengelenmiş yapılandırma oluşturur. |
| [Yük Dengelemesi birden çok Web sitesi vm'lerinde](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Birden çok IP yapılandırmaları, birleştirilmiş tooan Azure kullanılabilirlik kümesi, bir Azure yük dengeleyici erişilebilir olan iki VM'ler oluşturur. |
| [Uygulama yüksek kullanılabilirlik için birden çok bölgede doğrudan trafiği](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  İki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur. |
| | |
