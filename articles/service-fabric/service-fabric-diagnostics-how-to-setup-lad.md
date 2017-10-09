---
title: "Linux Azure tanılama kullanarak aaaCollect günlükleri | Microsoft Docs"
description: "Bu makalede, Azure'da çalışan Service Fabric Linux kümesinden Azure tanılama toocollect yukarı tooset nasıl günlüğe yazacağını açıklanmaktadır."
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
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Azure Tanılama’yı kullanarak günlük toplama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur. Merhaba günlüklerini merkezi bir konumda kolay tooanalyze kolaylaştırır ve hizmetlerinizin, uygulama veya hello kümenin kendisi olup sorunlarını giderme. Bir yolu tooupload toplama günlükleri ise toouse hello Azure tanılama uzantısını, hangi yüklemeleri tooAzure depolama, Azure Application Insights veya Azure Event Hubs günlüğe kaydeder. Ayrıca depolama veya Event Hubs hello etkinlikleri okumasına ve bir üründe gibi yerleştirin [günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) bir kapsamlı günlük arama ve analizi hizmeti ile yerleşik gelir.

## <a name="log-sources-that-you-might-want-toocollect"></a>Günlük kaynakları toocollect isteyebilirsiniz
* **Service Fabric günlükleri**: hello platformdan yayılan [LTTng](http://lttng.org) ve tooyour depolama hesabı yüklenir. Günlükler çalışma olaylarını olabilir veya platform hello çalışma zamanı olayları yayar. Bu günlükler depolanan hello konumda bu hello küme bildiriminde belirtir. (tooget hello depolama hesabı ayrıntıları hello etiketini ara **AzureTableWinFabETWQueryable** ve Ara **StoreConnectionString**.)
* **Uygulama olaylarını**: hizmetinizin koddan yayılan. Metin tabanlı günlük dosyalarını--örneğin, LTTng Yazar herhangi bir günlük çözümü kullanabilirsiniz. Daha fazla bilgi için uygulamanızı izleme hello LTTng belgelerine bakın.  

## <a name="deploy-hello-diagnostics-extension"></a>Merhaba tanılama uzantısını dağıtma
günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır. Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler. Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp göre farklılık gösterir.

toodeploy hello tanılama uzantısını toohello VM'ler küme oluşturma, bir parçası olarak hello kümedeki ayarlamak **tanılama** çok**üzerinde**. Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarı değiştiremezsiniz.

Ardından, Linux Azure tanılama (LAD) toocollect hello dosyaları yapılandırmak ve depolama hesabınızda yerleştirin. Bu işlem olarak Senaryo 3 ("Karşıya Yükle kendi günlük dosyaları") hello makalesinde açıklanan [kullanarak LAD toomonitor ve Linux VM'ler tanılamak](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Bu işlem alır toohello erişim aşağıdaki izler. Tercih ettiğiniz hello izlemeleri tooa Görselleştirici karşıya yükleyebilirsiniz.

Merhaba tanılama uzantısını Azure Kaynak Yöneticisi'ni kullanarak da dağıtabilirsiniz. Merhaba işlemi Windows ve Linux için benzer ve içinde Windows kümeleri için belgelenen [nasıl toocollect ile Azure tanılama günlüklerini](service-fabric-diagnostics-how-to-setup-wad.md).

Operations Management Suite, açıklandığı gibi kullanabilirsiniz [Operations Management Suite günlük analizi Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Bu yapılandırmayı tamamladıktan sonra belirtilen günlük dosyalarını hello LAD aracı izleyicileri hello. Yeni bir satır eklenmiş toohello dosyası olduğunda, belirttiğiniz gönderilen toohello depolama birimi bir syslog girişi oluşturur.

## <a name="next-steps"></a>Sonraki adımlar
daha ayrıntılı toounderstand sorunlarını giderme sırasında incelemeniz hangi olayların bkz [LTTng belgelerine](http://lttng.org/docs) ve [kullanarak LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

