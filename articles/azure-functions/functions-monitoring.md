---
title: "Azure işlevleri aaaMonitoring | Microsoft Docs"
description: "Bilgi nasıl toomonitor Azure işlevleri."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Azure İşlevleri’ni izleme

## <a name="overview"></a>Genel Bakış 


Merhaba **İzleyici** her işlev tooreview verir sekmesi her yürütülmesini bir işlev.

![Azure işlevleri İzleyici sekmesi](./media/functions-monitoring/monitor-tab.png) 

Bir yürütme tıklatmak, tooreview hello süresi, giriş verilerini, hataları ve ilişkili günlük dosyaları sağlar. Yararlı hata ayıklama ve performans işlevlerinizi ayarlama budur.


> [!IMPORTANT]
> Merhaba kullanırken [barındırma planı tüketim](functions-overview.md#pricing) Azure işlevleri için hello **izleme** döşeme hello işlev uygulaması genel bakış dikey penceresinde herhangi bir veri görüntülenmez. Merhaba platform dinamik olarak ölçeklendirir ve işlem örnekleri, bu ölçümleri tüketim plan üzerinde anlamlı olmayacak şekilde yönetir olmasıdır. İşlevi uygulamalarınızın toomonitor hello kullanımı, bu makaledeki hello yönergeler yerine kullanmanız gerekir.
> 
> Aşağıdaki ekran görüntüsünde hello bir örnek gösterilmektedir:
> 
> ![Merhaba ana kaynak dikey penceresinde izleme](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Gerçek zamanlı izleme

Gerçek zamanlı izleme kullanılabilir tıklayarak **canlı olay akışının** aşağıda gösterildiği gibi. 

![Canlı olay akışı seçeneği hello İzleyici sekmesi](./media/functions-monitoring/monitor-tab-live-event-stream.png)

Merhaba canlı olay akışının yeni bir tarayıcı sekmesinde aşağıda gösterildiği gibi grafik haline. 

![Canlı olay akışı örnek](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Doldurulmuş, veri toofail toobe neden olabilecek bilinen bir sorun yoktur. Bu karşılaşırsanız, tooclose hello tarayıcı sekmesinde içeren hello canlı olay akışının ve ardından gerekebilir **canlı olay akışının** yeniden tooallow, tooproperly doldurmak olay akışı veri. 

Merhaba canlı olay akışının işlevinizi istatistiklerini aşağıdaki hello grafik:

* Saniye başına başlatılan yürütmeleri
* Saniyede tamamlanan yürütmeleri
* Saniyede başarısız yürütmeleri
* Milisaniye cinsinden ortalama yürütme süresi.

Bu istatistikler gerçek zamanlı ancak hello hello yürütme verileri Grafikleme gerçek yaklaşık 10 saniye gecikme süresi olabilir.






## <a name="monitoring-log-files-from-a-command-line"></a>Bir komut satırından izleme günlük dosyaları


Günlük dosyaları tooa komut satırı oturumu hello Azure komut satırı arabirimi (CLI) veya PowerShell kullanarak bir yerel iş istasyonunda akışını sağlayabilirsiniz.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>İşlev uygulama günlük dosyalarının hello Azure CLI ile izleme

başlatıldı, tooget [hello Azure CLI yükleme](../cli-install-nodejs.md)

Merhaba aşağıdakileri kullanarak Azure hesabınıza günlüğüne komutu ya da hiçbirini Merhaba, ele diğer seçenekleri [tooAzure hello Azure CLI gelen oturum](../xplat-cli-connect.md).

    azure login

Kullanım hello şu komutu tooenable Azure CLI Hizmet Yönetimi (ASM) mod:.

    azure config mode asm

Birden çok aboneliğiniz varsa, aşağıdaki komutları toolist hello aboneliklerinizi ve işlev uygulamanızı içeren kümesi hello geçerli abonelik toohello abonelik kullanın.

    azure account list
    azure account set <subscriptionNameOrId>

Merhaba bir işlev uygulaması toohello komut satırında hello günlük dosyalarının en aşağıdaki komutu akışı:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>PowerShell ile izleme işlevi uygulama günlük dosyaları

başlatıldı, tooget [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).

Azure hesabınızda hello aşağıdaki komutu çalıştırarak ekleyin:

    PS C:\> Add-AzureAccount

Birden çok aboneliğiniz varsa, bunları adıyla hello abonelik hello şu anda seçili olan doğru temel komutu toosee aşağıdaki hello ile listeleyebilirsiniz `IsCurrent` özelliği:

    PS C:\> Get-AzureSubscription

Tooset hello etkin bir aboneliğiniz toohello bir işlev uygulaması içeren gerekiyorsa, komutu aşağıdaki hello kullan:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Akış hello günlükleri tooyour PowerShell oturumu komutu aşağıdaki hello:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Daha fazla bilgi için çok başvurun[nasıl yapılır: akış günlükleri web uygulamaları için](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [İşlevi test etme](functions-test-a-function.md)
* [Ölçek işlevi](functions-scale.md)

