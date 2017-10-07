---
title: "Azure Stream Analytics işleri hizmet kesintilerine uğramaması | Microsoft Docs"
description: "Stream Analytics yapma hakkında rehberlik yükseltme esnek işler."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Akış analizi işi güvenilirlik hizmet güncelleştirmeleri sırasında garanti

Tam olarak yönetilen bir hizmet olan hello yetenek toointroduce yeni hizmeti işlevselliği ve hızlı bir hızda iyileştirmeleri parçasıdır. Sonuç olarak, Stream Analytics haftalık (veya daha sık) temelinde dağıtmak bir hizmet güncelleştirmesi olabilir. Ne kadar test bitti olsun hala, var olan, çalışan bir iş hatanın toohello giriş kesilebilir bir riski yoktur. Kritik akış işleme işleri çalıştırma müşteriler için bu riskleri kaçınılması toobe gerekir. Bir mekanizma müşterileri tooreduce kullanabilir Azure'un bu riskidir  **[eşleştirilmiş bölge](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modeli. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Azure eşleştirilmiş bölgeleri bu sorunu nasıl ele?

Akış analizi işleri eşleştirilmiş bölgelerde ayrı toplu olarak güncelleştirilir güvence altına alır. Sonuç olarak tooidentify olası sonu hataları ve bunları düzeltmek hello güncelleştirmeleri arasında yeterli zaman aralığı yok.

_Orta Hindistan hello özel_ (eşleştirilmiş, bölge, Güney Hindistan ve akış analizi varlığı yok), Analytics hello değil gerçekleşecek bir güncelleştirme tooStream hello dağıtımını aynı zaman eşleştirilmiş bölgeler kümesinde. Birden çok bölgeye dağıtımlarda **hello içinde aynı grubu** oluşabilir **Merhaba, aynı anda**.

Merhaba makale üzerinde  **[kullanılabilirlik ve eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  hello en güncel bilgileri üzerinde bölgeler eşleştirilmiş sahiptir.

Müşterilerin tavsiye edilir toodeploy aynı işleri eşleştirilmiş tooboth bölgeler önerilir. Ayrıca Analytics izleme kapasiteleri, müşterilerin iç olan de tooStream toomonitor hello işleri tavsiye gibi **her ikisi de** üretim işler. Bir sonu tanımlanan toobe hello Stream Analytics Hizmet güncelleştirmesi sonucu ise, uygun şekilde İlerlet ve herhangi bir aşağı akış tüketicileri toohello sağlıklı proje çıktı başarısız. Yükseltme toosupport hello yeni dağıtım tarafından etkilenen hello eşleştirilmiş bölge önlemek ve eşleştirilmiş hello işleri hello bütünlüğünü.
