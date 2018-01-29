---
title: "Kullanılabilirlik bölgeleri genel bakış | Microsoft Docs"
description: "Bu makalede Azure kullanılabilirlik bölgelerinde genel bir bakış sağlar."
services: 
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
tags: 
ms.assetid: 
ms.service: azure
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2017
ms.author: markgal
ms.custom: mvc I am an ITPro and application developer, and I want to protect (use Availability Zones) my applications and data against data center failure (to build Highly Available applications).
ms.openlocfilehash: a0e654637bc4aca4230c56cc7c1706f5cd73622e
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/24/2018
---
# <a name="overview-of-availability-zones-in-azure-preview"></a>Kullanılabilirlik bölgeleri Azure (Önizleme) genel bakış

Veri merkezi düzeyi arızasına karşı korumak için kullanılabilirlik bölgeleri yardımcı. Bir Azure bölgesi içinde bulunur ve her biri kendi bağımsız sahip güç kaynağı, ağ ve soğutma. Dayanıklılık sağlamak için en az üç ayrı bölgelere etkinleştirilmiş tüm bölgelerde yoktur. Kullanılabilirlik bölgeleri fiziksel ve mantıksal ayırma bir bölge içinde uygulamaları ve verileri bölge düzeyinde hatalarından korur. 

![bir bölgenin bir bölgede giderek kavramsal görünümü](./media/az-overview/az-graphic-two.png)

## <a name="regions-that-support-availability-zones"></a>Kullanılabilirlik bölgeleri destekler bölgeleri

- Doğu ABD 2
- ABD Orta
- Batı Avrupa
- Fransa Orta

## <a name="services-that-support-availability-zones"></a>Kullanılabilirlik bölgeleri Destek Hizmetleri

Kullanılabilirlik bölgeleri destekler Azure hizmetler şunlardır:

- Linux Sanal Makineleri
- Windows Sanal Makineleri
- Sanal Makine Ölçek Kümeleri
- Yönetilen Diskler
- Load Balancer
- Genel IP adresi
- Bölge olarak yedekli depolama

## <a name="get-started-with-the-availability-zones-preview"></a>Kullanılabilirlik bölgeleri Önizleme kullanmaya başlama

Kullanılabilirlik bölgeleri Önizleme, Doğu ABD 2, BİZE Merkezi, Batı Avrupa ve belirli Azure hizmetlerinin Fransa merkezi bölgelerde kullanılabilir. 

1. [Kullanılabilirlik bölgeleri önizlemek için kaydolun](http://aka.ms/azenroll). 
2. Azure aboneliğinizde oturum açın.
3. Kullanılabilirlik bölgeyi destekleyen bir bölge seçin.
4. Kullanılabilirlik bölgeleri hizmetiniz ile kullanmaya başlamak için aşağıdaki bağlantılardan birini kullanın. 
    - [Bir sanal makine oluşturun](../virtual-machines/windows/create-portal-availability-zone.md)
    - [Bir sanal makine ölçek kümesi oluşturma](../virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones.md)
    - [PowerShell kullanarak yönetilen Disk ekleme](../virtual-machines/windows/attach-disk-ps.md#add-an-empty-data-disk-to-a-virtual-machine)
    - [Yük Dengeleyici](../load-balancer/load-balancer-standard-overview.md)

## <a name="next-steps"></a>Sonraki adımlar
- [Hızlı Başlangıç şablonları](http://aka.ms/azqs)
