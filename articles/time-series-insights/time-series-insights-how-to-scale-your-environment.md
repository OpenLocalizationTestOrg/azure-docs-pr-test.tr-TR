---
title: "aaaHow tooscale Azure zaman serisi Öngörüler ortamınızı | Microsoft Docs"
description: "Bu öğretici kapsayan nasıl tooscale Azure zaman serisi Öngörüler ortamınızı"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Nasıl tooscale zaman serisi Öngörüler ortamınızı

Bu öğretici kapsayan nasıl tooscale zaman serisi Öngörüler ortamınızı.

> [!NOTE]
> Ölçek büyütme sku türleri arasında izin verilmiyor. S1 Sku olan bir ortamda bir S2 ortamına dönüştürülemiyor.

## <a name="s1-sku-ingress-rates-and-capacities"></a>S1 SKU giriş hızları ve kapasiteleri

| S1 SKU kapasitesi | Giriş oranı | Maksimum depolama kapasitesi
| --- | --- | --- |
| 1 | 1 GB (1 milyon olay) | Aylık 30 GB (30 milyon olay) |
| 10 | 10 GB (10 milyon olay) | Ayda 300 GB (300 milyon olay) |

## <a name="s2-sku-ingress-rates-and-capacities"></a>S2 SKU giriş hızları ve kapasiteleri

| S2 SKU kapasitesi | Giriş oranı | Maksimum depolama kapasitesi
| --- | --- | --- |
| 1 | 10 GB (10 milyon olay) | Ayda 300 GB (300 milyon olay) |
| 10 | 100 GB (100 milyon olay) | Aylık 3 TB (3 milyon olay) |

Kapasiteleri doğrusal olarak, S1 sku kapasitesi 2 ile her ay gün giriş oranı ve 60 GB (60 milyon olayları) başına 2 GB (2 milyon) olayları destekler şekilde ölçeklendirilir.

## <a name="changing-hello-capacity-of-your-environment"></a>Merhaba kapasite ortamınızın değiştirme

1. Hello Azure portal, select ortamı, kapasite hello toochange istiyor.
1. Ayarlar altında Yapılandır'ı tıklatın.
1. Giriş ücretlerinizi hello gereksinimlerini karşılayan hello kapasite kaydırıcı tooselect hello kapasitesini ve depolama kapasitesini kullanın.

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba yeni kapasite yeterli olduğunu doğrulayın tooprevent azaltma. Merhaba daha fazla ayrıntı için bkz *ortamınızı bastırma* bölüm [burada](time-series-insights-diagnose-and-solve-problems.md).
