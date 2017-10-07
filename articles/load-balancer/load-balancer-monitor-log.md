---
title: "aaaMonitor işlemleri, olaylar ve yük dengeleyici için sayaçları | Microsoft Docs"
description: "Nasıl tooenable olayları uyarı ve Azure yük dengeleyici için sistem durumu günlüğü araştırma öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Azure Load Balancer için günlük analizi

Günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici giderebilirsiniz. Bu günlükler bazıları hello Portalı aracılığıyla erişilebilir. Tüm günlükleri Azure blob depolama alanından ayıklanan ve farklı araçlar, Excel ve Powerbı gibi görüntülenebilir. Merhaba listeden hello günlüklerinin farklı türleri hakkında daha fazla bilgi edinebilirsiniz.

* **Denetim günlüklerini:** kullanabileceğiniz [Azure denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (daha önce işlem günlükleri olarak bilinen) tooview gönderilen tooyour Azure aboneliği ve durumlarını olan tüm işlemleri. Denetim günlüklerini varsayılan olarak etkindir ve hello Azure portal görüntülenebilir.
* **Uyarı olayı günlükleri:** hello yük dengeleyici tarafından bu günlük tooview uyarıları rasied kullanabilirsiniz. Merhaba durum hello yük dengeleyici için beş dakikada toplanır. Bu günlük yalnızca bir yük dengeleyici uyarı olayı tetiklenir yazılır.
* **Sistem durumu araştırma günlüklerini:** istekleri sistem durumu araştırma hataları nedeniyle hello yük dengeleyiciden gösterilmeyen örneği, arka uç havuzundaki hello sayısı gibi sistem durumu araştırma tarafından algılanan bu günlük tooview sorunları kullanabilirsiniz. Bu günlük toowhen yazılır hello durumu araştırma bir değişiklik yoktur.

> [!IMPORTANT]
> Günlük analizi yük dengeleyici yalnızca Internet'e yönelik için şu anda çalışıyor. Günlükleri yalnızca hello Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir. Merhaba Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız. Merhaba dağıtım modelleri hakkında daha fazla bilgi için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Günlü kaydını etkinleştir

Denetim günlüğü, her Resource Manager kaynak için otomatik olarak etkinleştirilir. Tooenable olay ve bu günlükleri kullanılabilir hello veri toplama durumu araştırma günlük toostart gerekir. Aşağıdaki adımları tooenable günlük hello kullanın.

Oturum açma toohello [Azure portal](http://portal.azure.com). Bir yük dengeleyici, henüz yoksa [bir yük dengeleyici oluşturma](load-balancer-get-started-internet-arm-ps.md) devam etmeden önce.

1. Merhaba Portalı'nda tıklatın **Gözat**.
2. Seçin **yük dengeleyici**.

    ![Portal - yük dengeleyici](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Mevcut bir Yük Dengeleyiciyi seçin >> **tüm ayarları**.
4. Merhaba sağ tarafında hello iletişim hello yük dengeleyici hello adı altında çok kaydırma**izleme**, tıklatın **tanılama**.

    ![Portal - yük dengeleyici ayarları](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. Merhaba, **tanılama** bölmesi altında **durum**seçin **üzerinde**.
6. Tıklatın **depolama hesabı**.
7. Altında **GÜNLÜKLERİ**, mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun. Merhaba kaydırıcı toodetermine hello olay günlüklerinde olay veriyi depolanacak kaç gün kullanın. 
8. **Kaydet** düğmesine tıklayın.

    ![Portal - tanılama günlükleri](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Denetim günlükleri ayrı bir depolama hesabı gerektirmez. Hello kullan depolama olay ve sistem durumu için yoklama günlüğü hizmeti ücret uygulanabilir.

## <a name="audit-log"></a>Denetim günlüğü

Merhaba denetim günlüğü varsayılan olarak oluşturulur. Merhaba günlükleri 90 gün boyunca Azure'nın olay günlüklerini deposunda korunur. Merhaba okuyarak Bu günlükler hakkında daha fazla bilgi [olayları görüntülemek ve Denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) makalesi.

## <a name="alert-event-log"></a>Uyarı olay günlüğü

Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temelinde. Merhaba olayları JSON biçiminde günlüğe kaydedilen ve hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır. Merhaba, bir olay örneği aşağıdadır.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Merhaba JSON çıktısını gösterir hello *eventname* hello yük dengeleyici hello nedenini açıklayan özelliğini bir uyarı oluşturdu. Bu durumda, oluşturulan hello uyarı IP NAT sınırlar kaynağı tarafından neden tooTCP bağlantı noktası Tükenme (SNAT) oluştu.

## <a name="health-probe-log"></a>Sistem durumu araştırma günlük

Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temel olarak ayrıntılı yukarıdaki başına. Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır. 'Öngörüler günlükleri loadbalancerprobehealthstatus' adlı bir kapsayıcı oluşturulur ve veriler aşağıdaki hello kaydedilir:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

Merhaba özellikleri alan hello temel bilgileri hello araştırma sistem durumu için Hello JSON çıktısını gösterir. Merhaba *dipDownCount* özelliği Merhaba, ağ trafiğini toofailed araştırma yanıtları son gösterilmeyen uç hello toplam örneği sayısı gösterilir.

## <a name="view-and-analyze-hello-audit-log"></a>Görüntüleme ve hello denetim günlüğü çözümleme

Görüntüleme ve yöntemleri aşağıdaki hello birini kullanarak denetim günlüğü verilerini çözümleme:

* **Azure Araçları:** bilgi almanızı hello denetim günlüklerini Azure PowerShell, hello Azure komut satırı arabirimi (CLI), hello Azure REST API'si aracılığıyla veya Azure Önizleme portalını hello. Her yöntem için adım adım yönergeler hello ayrıntılı [denetim işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.
* **Power BI:** zaten yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz. Hello kullanarak [Azure denetim günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), önceden yapılandırılmış panolar verilerinizle analiz edebilirsiniz veya gereksinimlerinizi görünümleri toosuit özelleştirebilirsiniz.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Görüntüleme ve hello durum araştırması ve olay günlüğü çözümleme

Tooconnect tooyour depolama alanına ihtiyacınız hesap ve olay ve sistem durumu araştırma günlükleri için hello JSON günlük girişlerini almak. Merhaba JSON dosyaları yükledikten sonra bunları tooCSV ve Excel, Powerbı veya başka bir veri görselleştirme araç görünümünde dönüştürebilirsiniz.

> [!TIP]
> Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız hello kullanabilirsiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure denetim günlükleri Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.
* [Görüntüleme ve Azure denetim günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.

## <a name="next-steps"></a>Sonraki adımlar

[Yük dengeleyici araştırmalarını anlama](load-balancer-custom-probe-overview.md)
