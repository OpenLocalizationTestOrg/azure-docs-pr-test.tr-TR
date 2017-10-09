---
title: "Service Fabric olay toplama Linux Azure Tanılama ile aaaAzure | Microsoft Docs"
description: "Toplama ve izleme ve tanılama Azure Service Fabric kümeleri için LAD kullanarak olay toplama hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Olay toplama ve Linux Azure Tanılama'yı kullanarak koleksiyonu
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur. Merhaba günlüklerini merkezi bir konumda sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hello uygulamaları ve Hizmetleri sorunları gidermenize yardımcı olur.

Bir yolu tooupload ve toplama günlükleri günlükleri tooAzure depolama yükler ve ayrıca hello seçeneği toosend günlükleri tooAzure Application Insights veya olay hub'ları içeren toouse hello Linux Azure tanılama (LAD) uzantısı olur. Ayrıca bir dış işlem tooread hello olayları depolama biriminden kullanın ve analiz platformu üründe gibi yerleştirin [OMS günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.

## <a name="log-and-event-sources"></a>Günlük ve olay kaynakları

### <a name="service-fabric-platform-events"></a>Service Fabric platform olayları
Service Fabric yayar aracılığıyla birkaç Giden kutusu günlükleri [LTTng](http://lttng.org)çalışma olaylarını veya çalışma zamanı olayları dahil. Bu günlükler kümenin Resource Manager şablonu belirtir hello hello konumda depolanır. tooget veya ayarlama hello depolama hesabı ayrıntıları, hello etiketini ara **AzureTableWinFabETWQueryable** ve Ara **StoreConnectionString**.

### <a name="application-events"></a>Uygulama olayları
 Yazılım düzenleme olduğunda, belirtildiği gibi uygulamaların ve hizmetlerin kodundan yayılan olaylar. Metin tabanlı günlük dosyalarını--örneğin, LTTng Yazar herhangi bir günlük çözümü kullanabilirsiniz. Daha fazla bilgi için uygulamanızı izleme hello LTTng belgelerine bakın.

[İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Merhaba tanılama uzantısını dağıtma
günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır. Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler. Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp göre farklılık gösterir.

toodeploy hello tanılama uzantısını toohello VM'ler küme oluşturma, bir parçası olarak hello kümedeki ayarlamak **tanılama** çok**üzerinde**. Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarı değiştiremezsiniz.

Ardından, Linux Azure tanılama (LAD) toocollect hello dosyaları yapılandırmak ve depolama hesabınızda yerleştirin. Bu işlem olarak Senaryo 3 ("Karşıya Yükle kendi günlük dosyaları") hello makalesinde açıklanan [kullanarak LAD toomonitor ve Linux VM'ler tanılamak](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Bu işlem alır toohello erişim aşağıdaki izler. Tercih ettiğiniz hello izlemeleri tooa Görselleştirici karşıya yükleyebilirsiniz.

Merhaba tanılama uzantısını Azure Kaynak Yöneticisi'ni kullanarak da dağıtabilirsiniz. Merhaba işlemi Windows ve Linux için benzer ve içinde Windows kümeleri için belgelenen [nasıl toocollect ile Azure tanılama günlüklerini](service-fabric-diagnostics-how-to-setup-wad.md).

Operations Management Suite, açıklandığı gibi kullanabilirsiniz [Operations Management Suite günlük analizi Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Bu yapılandırmayı tamamladıktan sonra belirtilen günlük dosyalarını hello LAD aracı izleyicileri hello. Yeni bir satır eklenmiş toohello dosyası olduğunda, belirttiğiniz gönderilen toohello depolama birimi bir syslog girişi oluşturur.

## <a name="next-steps"></a>Sonraki adımlar

daha ayrıntılı toounderstand sorunlarını giderme sırasında incelemeniz hangi olayların bkz [LTTng belgelerine](http://lttng.org/docs) ve [kullanarak LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
