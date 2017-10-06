---
title: "aaaAzure Automation DSC genel bakış | Microsoft Docs"
description: "Bir genel bakış, Azure Otomasyonu istenen durum yapılandırması (DSC), koşulları ve bilinen sorunlar"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell dsc, istenen durum yapılandırması, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Azure Otomasyonu DSC genel bakış

Azure Otomasyonu DSC, toowrite sağlayan bir Azure hizmetidir, yönetmek ve PowerShell istenen durum yapılandırması (DSC) derlemek [yapılandırmaları](https://msdn.microsoft.com/powershell/dsc/configurations), içeri aktarma [DSC kaynakları](https://msdn.microsoft.com/powershell/dsc/resources)ve atayın Merhaba bulutta tüm yapılandırmaları tootarget düğümleri.

## <a name="why-use-azure-automation-dsc"></a>Azure Otomasyonu DSC neden kullanılır?

Azure Otomasyonu DSC Azure dışında DSC kullanarak birkaç avantajı sağlar.

### <a name="built-in-pull-server"></a>Yerleşik çekme sunucu

Azure Automation'ın sağladığı bir [DSC istek sunucusuyla](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) hedef düğümleri otomatik olarak yapılandırmaları alması için bunları istenen toohello durumu uygun ve uyumlulukları hakkında rapor.
Azure Otomasyonu Hello yerleşik çekme sunucusunda yukarı hello gerek tooset ortadan kaldırır ve kendi çekme sunucunuz.
Azure Otomasyonu sanal veya fiziksel Windows veya Linux makineler, hello Bulut veya şirket içi hedefleyebilirsiniz.

### <a name="management-of-all-your-dsc-artifacts"></a>Tüm DSC yapıları Yönetimi

Azure Otomasyonu DSC getirir aynı yönetim katmanı çok hello[PowerShell istenen durum Yapılandırması](https://msdn.microsoft.com/powershell/dsc/overview) gibi Azure Otomasyonu PowerShell komut dosyası için sunar.

Hello Azure portal veya PowerShell, tüm, DSC yapılandırmalarını, kaynak ve hedef düğümleri yönetebilirsiniz.

![Hello Azure Otomasyonu dikey penceresi ekran görüntüsü](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Günlük analizi raporlama verilerini alma

Azure Otomasyonu DSC'ye yönetilen düğümler ayrıntılı raporlama durum veri toohello yerleşik çekme sunucusuna gönderir.
Bu veri tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı Azure Otomasyonu DSC toosend yapılandırabilirsiniz.
toosend DSC durum veri tooyour günlük analizi çalışma alanı, nasıl görürüm toolearn [İleri Azure Otomasyonu veri tooOMS günlük analizi raporlama DSC](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Tanıtım videosu

Tooreading izlemeyi mi tercih ediyorsunuz? Mayıs 2015, ne zaman Azure Otomasyonu DSC ilk duyurulan video aşağıdaki hello göz vardır.

>[!NOTE]
>Merhaba kavramları ve bu videoda ele alınan ömrünü doğru olsa da, bu videonun kaydedilmesinden sonra Azure Otomasyonu DSC değişmiştir.
>Genel kullanıma sunulmuştur, hello Azure portal çok daha geniş bir kullanıcı Arabirimine sahiptir ve birçok ek özellikleri desteklemektedir.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Sonraki adımlar

* Azure Otomasyonu DSC'ye tooonboard düğümleri toobe yönetilen nasıl toolearn bakın [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)
* Azure Automation DSC kullanmaya tooget bakın [Azure Otomasyonu DSC ile çalışmaya başlama](automation-dsc-getting-started.md)
* toolearn tootarget düğümleri atayabilirsiniz bir DSC yapılandırmaları derleme hakkında bkz [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md)
* Azure Otomasyonu DSC için PowerShell cmdlet başvuru için bkz: [Azure Otomasyonu DSC cmdlet'leri](/powershell/module/azurerm.automation/#automation)
* Fiyatlandırma bilgileri için bkz: [Azure Otomasyonu DSC fiyatlandırma](https://azure.microsoft.com/pricing/details/automation/)
* toosee sürekli dağıtım ardışık düzeninde, Azure Automation DSC kullanmaya ilişkin bir örnek görmek [sürekli dağıtım tooIaaS VM'ler kullanarak Azure Otomasyonu DSC ve Chocolatey](automation-dsc-cd-chocolatey.md)
