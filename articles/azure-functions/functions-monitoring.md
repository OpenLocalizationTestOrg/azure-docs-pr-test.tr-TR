---
title: "Azure işlevleri izleme | Microsoft Docs"
description: "Azure işlevleri izleme öğrenin."
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a>Azure İşlevleri’ni izleme

## <a name="overview"></a>Genel Bakış 


**İzleyici** sekmesi her işlevi işlevinin her yürütme gözden geçirmenizi sağlar.

![Azure işlevleri İzleyici sekmesi](./media/functions-monitoring/monitor-tab.png) 

Bir yürütme tıklatmak süresi, giriş verilerini, hataları ve ilişkili günlük dosyalarını gözden geçirmenizi sağlar. Yararlı hata ayıklama ve performans işlevlerinizi ayarlama budur.


> [!IMPORTANT]
> Kullanırken [barındırma planı tüketim](functions-overview.md#pricing) Azure işlevleri için **izleme** döşeme işlev uygulaması genel bakış dikey penceresinde herhangi bir veri görüntülenmez. Platform dinamik olarak ölçeklendirir ve işlem örnekleri, bu ölçümleri tüketim plan üzerinde anlamlı olmayacak şekilde yönetir olmasıdır. İşlevi uygulamalarınızı kullanımını izlemek için bunun yerine bu makaledeki yönergeleri kullanmanız gerekir.
> 
> Aşağıdaki ekran görüntüsünde bir örnek gösterilmektedir:
> 
> ![Ana kaynak dikey penceresinde izleme](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Gerçek zamanlı izleme

Gerçek zamanlı izleme kullanılabilir tıklayarak **canlı olay akışının** aşağıda gösterildiği gibi. 

![Canlı olay akışı seçeneği İzleyici sekmesi](./media/functions-monitoring/monitor-tab-live-event-stream.png)

Canlı olay akışının yeni bir tarayıcı sekmesinde aşağıda gösterildiği gibi grafik haline. 

![Canlı olay akışı örnek](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Verilerinizi doldurulmalıdır başarısız olmasına neden olabilecek bilinen bir sorun yoktur. Bu karşılaşırsanız, canlı olay akışının içeren tarayıcı sekmesini kapatın ve ardından gerekebilir **canlı olay akışının** olay akışı verilerinizi düzgün bir şekilde doldurmak yeniden izin vermek için. 

Canlı olay akışının işlevinizi aşağıdaki istatistikleri grafik:

* Saniye başına başlatılan yürütmeleri
* Saniyede tamamlanan yürütmeleri
* Saniyede başarısız yürütmeleri
* Milisaniye cinsinden ortalama yürütme süresi.

Bu istatistikler gerçek zamanlı ancak gerçek yürütme verileri Grafikleme yaklaşık 10 saniye gecikme süresi olabilir.






## <a name="monitoring-log-files-from-a-command-line"></a>Bir komut satırından izleme günlük dosyaları


Yerel iş istasyonunda Azure komut satırı arabirimi (CLI) veya PowerShell kullanarak bir komut satırı oturumu için günlük dosyalarını akışını sağlayabilirsiniz.

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a>Azure CLI ile izleme işlevi uygulama günlük dosyaları

Başlamak için [Azure CLI yükleme](../cli-install-nodejs.md)

Aşağıdaki komutu ya da, ele diğer seçeneklerden birini kullanarak Azure hesabınıza günlüğüne [oturum açmak için Azure Azure CLI üzerinden](../xplat-cli-connect.md).

    azure login

Azure CLI Hizmet Yönetimi (ASM) modunu etkinleştirmek için aşağıdaki komutu kullanın:.

    azure config mode asm

Birden çok aboneliğiniz varsa, aboneliklerinizi listelemek ve geçerli Abonelik işlevi uygulamanızı içeren aboneliği ayarlamak için aşağıdaki komutları kullanın.

    azure account list
    azure account set <subscriptionNameOrId>

Aşağıdaki komutu, günlük dosyaları, komut satırı işlevi uygulamanızın akışı:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>PowerShell ile izleme işlevi uygulama günlük dosyaları

Başlamak için [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).

Azure hesabınızda, aşağıdaki komutu çalıştırarak ekleyin:

    PS C:\> Add-AzureAccount

Birden çok aboneliğiniz varsa, bunları doğru abonelik şu anda seçili bağlı olup olmadığını görmek için aşağıdaki komutu kullanarak ada göre listeleyebilirsiniz `IsCurrent` özelliği:

    PS C:\> Get-AzureSubscription

Etkin bir aboneliğiniz işlevi uygulamanızı içeren bir ayarlamak gerekiyorsa, aşağıdaki komutu kullanın:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Aşağıdaki komut ile PowerShell oturumunuz için günlükleri akışı:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Daha fazla bilgi için bkz [nasıl yapılır: akış günlükleri web uygulamaları için](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [İşlevi test etme](functions-test-a-function.md)
* [Ölçek işlevi](functions-scale.md)

