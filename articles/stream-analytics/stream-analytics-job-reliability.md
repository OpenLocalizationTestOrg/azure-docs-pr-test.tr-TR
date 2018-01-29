---
title: "Azure Stream Analytics işleri hizmet kesintilerine uğramaması | Microsoft Docs"
description: "Stream Analytics yapma hakkında rehberlik yükseltme esnek işler."
services: stream-analytics
documentationCenter: 
authors: samacha
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 76e347ee62ffc07db1d8e74cf0ac5327a154fe4f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Akış analizi işi güvenilirlik hizmet güncelleştirmeleri sırasında garanti

Tam olarak yönetilen bir hizmet olma yeteneği yeni hizmet işlevselliği ve hızlı bir hızda geliştirmeleri tanıtır bir parçasıdır. Sonuç olarak, Stream Analytics haftalık (veya daha sık) temelinde dağıtmak bir hizmet güncelleştirmesi olabilir. Ne kadar test bitti olsun hala, var olan, çalışan bir iş bir hata giriş nedeniyle kesilebilir bir riski yoktur. Kritik akış işleme işleri çalıştırma müşteriler için bu riskleri kaçınılması gerekir. Müşteriler bu riskini azaltmak için kullanabileceğiniz bir Azure'nın mekanizmadır  **[eşleştirilmiş bölge](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modeli. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Azure eşleştirilmiş bölgeleri bu sorunu nasıl ele?

Akış analizi işleri eşleştirilmiş bölgelerde ayrı toplu olarak güncelleştirilir güvence altına alır. Sonuç olarak olası sonu hataları belirlemek ve düzeltmek için güncelleştirmeleri arasında yeterli zaman aralığı yok.

_Orta Hindistan dışında_ (eşleştirilmiş, bölge, Güney Hindistan ve akış analizi varlığı yok), Stream Analytics için bir güncelleştirme dağıtımının eşleştirilmiş bölgeler kümesinde aynı zamanda oluşacak değil. Birden çok bölgeye dağıtımlarda **aynı gruptaki** oluşabilir **aynı anda**.

Makale  **[kullanılabilirlik ve eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  üzerinde bölgeler eşleştirilmiş en güncel bilgileri içeriyor.

Müşteriler, aynı işleri hem eşleştirilmiş bölgelere dağıtmak için önerilir. İzleme kapasiteleri iç Stream Analytics yanı sıra müşterileri de işleri izlemek için önerilir gibi **her ikisi de** üretim işler. Stream Analytics Hizmet güncelleştirmesi sonucu olarak bir sonu tanımladıysanız, uygun şekilde İlerlet ve herhangi bir aşağı akış tüketiciye sağlıklı iş çıktısı için yük. Yükseltme desteklemek için yeni dağıtım tarafından etkilenen eşleştirilmiş bölge önlemek ve eşleştirilmiş işleri bütünlüğünü.
