---
title: "Azure Service Fabric olay toplama Linux Azure tanılama | Microsoft Docs"
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
ms.openlocfilehash: bcc3a229369a065cfcfbd32eadbf3f6ae6fe0036
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Olay toplama ve Linux Azure Tanılama'yı kullanarak koleksiyonu
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Azure Service Fabric kümesi çalıştırırken, merkezi bir konumda tüm düğümlerdeki günlükleri toplamak için iyi bir fikirdir. Merkezi bir konumda günlükler sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hizmetler ve uygulamalar sorunları gidermenize yardımcı olur.

Karşıya yükleme ve günlükleri toplamak için bir yol günlükleri Azure Storage'a yükler ve ayrıca Azure Application Insights veya olay hub'ları için günlükleri gönderme seçeneği içeren Linux Azure tanılama (LAD) uzantısı kullanmaktır. Olayları depolama alanından okuyun ve bunları bir analiz platformu üründe gibi yerleştirmek için bir dış işlem kullanabilirsiniz [OMS günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.

## <a name="log-and-event-sources"></a>Günlük ve olay kaynakları

### <a name="service-fabric-platform-events"></a>Service Fabric platform olayları
Service Fabric yayar aracılığıyla birkaç Giden kutusu günlükleri [LTTng](http://lttng.org)çalışma olaylarını veya çalışma zamanı olayları dahil. Bu günlükler kümenin Resource Manager şablonu belirten konumda depolanır. Almak veya depolama hesabı ayrıntıları ayarlamak için arama etiketi için **AzureTableWinFabETWQueryable** ve Ara **StoreConnectionString**.

### <a name="application-events"></a>Uygulama olayları
 Yazılım düzenleme olduğunda, belirtildiği gibi uygulamaların ve hizmetlerin kodundan yayılan olaylar. Metin tabanlı günlük dosyalarını--örneğin, LTTng Yazar herhangi bir günlük çözümü kullanabilirsiniz. Daha fazla bilgi için uygulamanızı izleme LTTng belgelerine bakın.

[İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-the-diagnostics-extension"></a>Tanılama uzantısını dağıtma
Günlükleri toplamayı ilk adımı, Service Fabric kümesindeki VM'lerin her birinde tanılama uzantısını dağıtmaktır. Tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz depolama hesabı yükler. Adımlar Azure portalında veya Azure Resource Manager kullanıp göre farklılık gösterir.

Tanılama uzantısını kümedeki sanal makineleri küme oluşturmanın bir parçası dağıtmak için ayarlanmış **tanılama** için **üzerinde**. Kümeyi oluşturduktan sonra portal kullanarak bu ayarı değiştiremezsiniz.

Ardından, dosyaları toplamak ve bunları depolama hesabınızda yerleştirmek için Linux Azure tanılama (LAD) yapılandırın. Bu işlem olarak Senaryo 3 ("Karşıya Yükle kendi günlük dosyaları") makalesinde açıklanan [kullanarak izleme ve Linux VM'ler tanılama LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Bu işlem aşağıdaki izlemeleri için size erişim alır. İzlemeler için tercih ettiğiniz Görselleştirici karşıya yükleyebilirsiniz.

Tanılama uzantısını Azure Kaynak Yöneticisi'ni kullanarak da dağıtabilirsiniz. İşlemi Windows ve Linux için benzer ve içinde Windows kümeleri için belgelenen [ile Azure tanılama günlükleri toplamak nasıl](service-fabric-diagnostics-how-to-setup-wad.md).

Operations Management Suite, açıklandığı gibi kullanabilirsiniz [Operations Management Suite günlük analizi Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Bu yapılandırmayı tamamladıktan sonra belirtilen günlük dosyaları LAD Aracısı'nı izler. Yeni bir satır dosyanın sonuna olduğunda, belirttiğiniz depolama için gönderilen bir syslog girişi oluşturur.

## <a name="next-steps"></a>Sonraki adımlar

Hangi olayların sorunlarını giderme sırasında incelemeniz daha ayrıntılı olarak anlamak için bkz: [LTTng belgelerine](http://lttng.org/docs) ve [kullanarak LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).