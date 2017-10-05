---
title: "Linux Azure tanılama kullanarak günlüklerini toplama | Microsoft Docs"
description: "Bu makalede, Azure'da çalışan Service Fabric Linux kümesinden günlükleri toplamak için Azure tanılama ayarlamak açıklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: 3e41caaeb38c55d1c6c3bfdce2f81c86b4aff4d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Azure Tanılama’yı kullanarak günlük toplama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Azure Service Fabric kümesi çalıştırırken, merkezi bir konumda tüm düğümlerdeki günlükleri toplamak için iyi bir fikirdir. Hizmetlerinizi, uygulamanızı veya küme olup günlüklerini merkezi bir konumda sahip çözümlemek ve sorunlarını gidermek kolaylaştırır. Karşıya yüklemek ve günlükleri toplamak için bir Azure Storage, Azure Application Insights veya Azure Event Hubs için günlükleri karşıya yükleyen Azure tanılama uzantısını kullanma yoludur. Ayrıca depolama veya Event Hubs etkinlikleri okumasına ve bir üründe gibi yerleştirin [günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) bir kapsamlı günlük arama ve analizi hizmeti ile yerleşik gelir.

## <a name="log-sources-that-you-might-want-to-collect"></a>Toplamak istediğiniz günlük kaynakları
* **Service Fabric günlükleri**: platformdan yayılan [LTTng](http://lttng.org) ve depolama hesabınıza yüklenir. Günlükleri çalışma olaylarını veya platform yayar çalışma zamanı olayları olabilir. Bu günlükler küme bildiriminde belirten konumda depolanır. (Depolama hesabı ayrıntıları almak için arama etiketi **AzureTableWinFabETWQueryable** ve Ara **StoreConnectionString**.)
* **Uygulama olaylarını**: hizmetinizin koddan yayılan. Metin tabanlı günlük dosyalarını--örneğin, LTTng Yazar herhangi bir günlük çözümü kullanabilirsiniz. Daha fazla bilgi için uygulamanızı izleme LTTng belgelerine bakın.  

## <a name="deploy-the-diagnostics-extension"></a>Tanılama uzantısını dağıtma
Günlükleri toplamayı ilk adımı, Service Fabric kümesindeki VM'lerin her birinde tanılama uzantısını dağıtmaktır. Tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz depolama hesabı yükler. Adımlar Azure portalında veya Azure Resource Manager kullanıp göre farklılık gösterir.

Tanılama uzantısını kümedeki sanal makineleri küme oluşturmanın bir parçası dağıtmak için ayarlanmış **tanılama** için **üzerinde**. Kümeyi oluşturduktan sonra portal kullanarak bu ayarı değiştiremezsiniz.

Ardından, dosyaları toplamak ve bunları depolama hesabınızda yerleştirmek için Linux Azure tanılama (LAD) yapılandırın. Bu işlem olarak Senaryo 3 ("Karşıya Yükle kendi günlük dosyaları") makalesinde açıklanan [kullanarak izleme ve Linux VM'ler tanılama LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Bu işlem aşağıdaki izlemeleri için size erişim alır. İzlemeler için tercih ettiğiniz Görselleştirici karşıya yükleyebilirsiniz.

Tanılama uzantısını Azure Kaynak Yöneticisi'ni kullanarak da dağıtabilirsiniz. İşlemi Windows ve Linux için benzer ve içinde Windows kümeleri için belgelenen [ile Azure tanılama günlükleri toplamak nasıl](service-fabric-diagnostics-how-to-setup-wad.md).

Operations Management Suite, açıklandığı gibi kullanabilirsiniz [Operations Management Suite günlük analizi Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Bu yapılandırmayı tamamladıktan sonra belirtilen günlük dosyaları LAD Aracısı'nı izler. Yeni bir satır dosyanın sonuna olduğunda, belirttiğiniz depolama için gönderilen bir syslog girişi oluşturur.

## <a name="next-steps"></a>Sonraki adımlar
Hangi olayların sorunlarını giderme sırasında incelemeniz daha ayrıntılı olarak anlamak için bkz: [LTTng belgelerine](http://lttng.org/docs) ve [kullanarak LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

