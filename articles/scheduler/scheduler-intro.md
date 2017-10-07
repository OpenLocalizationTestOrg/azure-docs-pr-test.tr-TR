---
title: Azure Scheduler aaaWhat mi? | Microsoft Belgeleri
description: "Azure Zamanlayıcı verir toodeclaratively Eylemler toorun hello bulutta açıklanmaktadır. Sonra, bu eylemleri otomatik olarak zamanlar ve çalıştırır."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Azure Scheduler nedir?
Azure Zamanlayıcı verir toodeclaratively Eylemler toorun hello bulutta açıklanmaktadır. Sonra, bu eylemleri otomatik olarak zamanlar ve çalıştırır.  Zamanlayıcı olmadığından bu kullanarak [Azure portal hello](scheduler-get-started-portal.md), kod, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), ya da Azure PowerShell.

Scheduler zamanlanan iş oluşturur, korur ve çağırır.  Scheduler iş yükü barındırmaz ya da kod çalıştırmaz. Yalnızca başka bir yerde (Azure’da, şirket içi ya da başka sağlayıcıda) barındırılan kodu *çağırır*. HTTP, HTTPS, depolama kuyruğu, hizmet veri yolu kuyruğu ya da hizmet veri yolu konusu aracılığıyla çağırır.

Zamanlayıcı zamanlamaları [işleri](scheduler-concepts-terms.md), bir gözden geçirebileceğiniz ve kesin ve güvenilir bir şekilde zamanlamaları iş yükleri toobe çalıştırın iş yürütme sonuçlarının geçmişini tutar. Azure WebJobs (Azure App Service Web Apps özelliğini hello parçası) ve diğer Azure zamanlama özellikleri hello arka planda Zamanlayıcısı'nı kullanın. Merhaba [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) hello bu eylemler için iletişimi yönetmeye yardımcı olur. Bu şekilde, Scheduler kolayca [karmaşık zamanlamalar ve gelişmiş yineleme oluşturmayı](scheduler-advanced-complexity.md) destekler.

Kendilerini Scheduler toohello kullanımını ödünç birkaç senaryo vardır. Örneğin:

* *Yinelenen uygulama eylemleri:* Twitter’dan akışa düzenli aralıklarla veri toplama.
* *Günlük bakım:* Günlüklerin günlük ayıklanması, yedeklemelerin ve diğer bakım görevlerinin gerçekleştirilmesi. Örneğin, bir yönetici tooback hello veritabanını 1: 00'da tercih edebilirsiniz her gün hello için sonraki dokuz ay.

Zamanlayıcı toocreate sağlar, Güncelleştir, Sil, görüntülemek ve işlerini yönetmek ve [iş koleksiyonları](scheduler-concepts-terms.md) komut dosyalarını kullanarak programlı ve hello Portalı'nda.

## <a name="see-also"></a>Ayrıca bkz.
 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile](scheduler-advanced-complexity.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

