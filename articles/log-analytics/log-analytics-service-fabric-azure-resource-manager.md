---
title: "Günlük analizi kullanarak Service Fabric uygulamaları aaaAssess hello Azure portalı | Microsoft Docs"
description: "Günlük hello Azure portal tooassess hello risk ve Service Fabric uygulamalarınızı durumunu kullanarak analizleri hello Service Fabric çözüm kullanabilir mikro hizmetler, düğümleri ve kümelerini."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Service Fabric uygulamaları ve mikro hizmetler hello Azure portal ile değerlendirin

> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Service Fabric simgesi](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

Bu makalede nasıl toouse hello günlük analizi toohelp Service Fabric çözümde tanımlamak ve Service Fabric küme genelinde sorunlarını giderme açıklanmaktadır.

Merhaba Service Fabric çözümü bu verileri Azure WAD tablolardan toplayarak Service Fabric Vm'lerinizi Azure Tanılama verileri kullanır. Günlük analizi, Service Fabric framework olaylar dahil olmak üzere, daha sonra okur **güvenilir hizmeti olayları**, **aktör olayları**, **çalışma olaylarını**, ve **özel ETW olayları**. Merhaba çözüm panosu ile Service Fabric ortamınızda mümkün tooview önemli sorunlar ve ilgili olayları şunlardır.

Merhaba çözümüyle başlatılan tooget tooconnect ihtiyacınız Service Fabric kümesi tooa günlük analizi çalışma alanı. Üç senaryoları tooconsider şunlardır:

1. Service Fabric kümesi dağıtmadıysanız hello adımlarda kullanmak ***bir Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı dağıtma*** toodeploy yeni bir küme ve tooreport tooLog Analytics yapılandırılmamış olabilir.
2. Konakları toouse toocollect performans sayaçları, Service Fabric kümesi güvenlik gibi diğer OMS çözümleri gerekiyorsa hello adımları ***Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı VM uzantısı ile dağıtma yüklü.***
3. Service Fabric kümesi zaten dağıttıysanız ve tooconnect istiyorsanız bunu tooLog Analytics, hello adımlarını izleyin ***var olan bir depolama hesabı tooLog Analytics ekleme.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı dağıtın.
Bu şablon, aşağıdaki hello:

1. Azure Service Fabric kümesi zaten bağlı tooa günlük analizi çalışma alanı dağıtır. Yeni bir çalışma alanı hello şablon ya da zaten varolan bir günlük analizi çalışma alanını giriş hello adını dağıtırken hello seçeneği toocreate sahip.
2. Merhaba tanılama depolama hesabı toohello günlük analizi çalışma alanı ekler.
3. Günlük analizi çalışma alanınızdaki Hello Service Fabric çözümü sağlar.

[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Seçtiğinizde, bundan sonra hello Dağıt düğmesi yukarıdaki, Azure portalı açıldığında, tooedit parametrelere sahip hello. Emin toocreate yeni bir kaynak grubu şöyle bir yeni günlük analizi çalışma alanı adı girin:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Merhaba yasal koşulları kabul edin ve tıklatın **oluşturma** toostart hello dağıtım. Merhaba dağıtım tamamlandıktan sonra bkz: hello yeni çalışma ve oluşturulan küme ve gerekir WADServiceFabric hello * eklenen olayı, WADWindowsEventLogs ve WADETWEvent tabloları:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı VM uzantısı ile dağıtın.

Bu şablon, aşağıdaki hello:

1. Azure Service Fabric kümesi zaten bağlı tooa günlük analizi çalışma alanı dağıtır. Yeni bir çalışma alanı oluşturun veya var olan bir kullanın.
2. Merhaba tanılama depolama hesapları toohello günlük analizi çalışma alanı ekler.
3. Merhaba günlük analizi çalışma alanındaki Hello Service Fabric çözümü sağlar.
4. Service Fabric kümesi her sanal makine ölçek Hello MMA Aracı Uzantısı yükler. Yüklü hello MMA aracıyla düğümleriniz hakkında mümkün tooview performans ölçümleri olduğunuz.

[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Aşağıdaki yukarıdaki, giriş hello gerekli parametreleri aynı adımları hello ve dağıtımı devre dışı tetiklersiniz. Bir kez daha hello yeni çalışma alanı, küme ve WAD tablolar tüm oluşturulan görmeniz gerekir:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Performans verileri görüntüleme

Perf Veri tooview, düğümlerinden:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Merhaba günlük analizi çalışma alanından hello Azure portal'ı başlatın.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Merhaba soldaki bölmede tooSettings gidin ve veri seçin >> Windows performans sayaçlarını >> "Ekle hello Seçili performans sayaçlarını": ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- Günlük aramada sorguları toodelve düğümleriniz ilgili ana metriklerini içine aşağıdaki hello kullan:

    a. Karşılaştırma hangi düğümlerin sorunu yaşıyor hello son bir saat toosee, tüm düğümler arasında ortalama CPU kullanımı hello ve ne zaman aralığında bir ani bir düğüm vardı:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Bu sorgu ile her bir düğümde kullanılabilir bellek benzer çizgi grafiklerde görüntüleyin:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview listesini düğümlerinizin her düğüm için kullanılabilir MBayt için hello tam ortalama değer gösteren tüm, bu sorguyu kullanın:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. Hello saatlik ortalama inceleyerek, belirli bir düğümüne toodrill aşağı istediğiniz hello durumda CPU kullanımı, en az, en fazla ve 75-yüzdelik olduğunuz mümkün toodo bunu kullanarak bu sorgu (bilgisayar alanı değiştirin):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Günlük analizi performans ölçümlerini hello adresindeki hakkında daha fazla bilgi okumak [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Varolan bir depolama hesabı tooLog Analytics ekleme

Bu şablon, yalnızca var olan depolama hesapları tooa yeni veya var olan günlük analizi çalışma alanınız ekler.

[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> Zaten varolan bir günlük analizi çalışma alanı ile çalışıyorsanız, bir kaynak grubu seçilmesinde "Var olanı kullan" ve arama hello günlük analizi çalışma içeren hello kaynak grubu için seçin. Yeni bir olduğunda oluşturacak Aksi takdirde.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Bu şablon dağıtıldıktan sonra mümkün toosee hello depolama hesabı bağlı tooyour günlük analizi çalışma alanı olacaktır. Bu örnekte, t ı yukarıda oluşturduğunuz bir daha fazla depolama hesabı toohello Exchange çalışma eklendi.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Service Fabric olaylarını görüntüle

Merhaba dağıtımları tamamlanır ve hello Service Fabric çözüm çalışma alanınızda etkinleştirildi sonra hello seçeneğini **Service Fabric** döşeme hello günlük analizi portal toolaunch hello Service Fabric panosunda. Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir. Her sütun, belirtilen zaman aralığı hello sütunun ölçütlerine sayısı eşleştirerek hello üst 10 olaylarını listeler. Merhaba tüm liste tıklayarak sağlar günlük arama çalıştırabilirsiniz **tümünü görmek** hello sağ alt her sütunun veya hello sütun başlığını tıklatarak.

| **Service Fabric olay** | **Açıklama** |
| --- | --- |
| Önemli sorunlar |Bir görüntü RunAsyncFailures RunAsynCancellations ve düğüm listeleri gibi sorunların. |
| İşletimsel olayları |Uygulama yükseltme ve dağıtımları gibi önemli çalışma olaylarını. |
| Güvenilir hizmeti olayları |Önemli güvenilir hizmeti olayları böyle bir Runasyncinvocations. |
| Aktör olayları |Aktör yöntemi, aktör etkinleştirmeleri ve deactivations ve benzeri tarafından oluşturulan özel durumları gibi mikro-Hizmetleri tarafından oluşturulan önemli aktör olayları. |
| Uygulama olayları |Uygulamalarınız tarafından oluşturulan tüm özel ETW olayları. |

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf4.png)

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri için Service Fabric nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | Operations Manager Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 dakika |

> [!NOTE]
> Tıklayarak bu olayları hello Service Fabric çözüm hello kapsamını değiştirebilirsiniz **verilerini alarak son 7 gün** hello Pano hello üstünde. Bir gün veya altı saat olmak üzere son yedi gün içinde hello oluşturulan olayları gösterir. Ya da seçebilirsiniz **özel** toospecify özel bir tarih aralığı.
>
>

## <a name="next-steps"></a>Sonraki adımlar

* Kullanım [günlük analizi günlük aramalarda](log-analytics-log-searches.md) tooview ayrıntılı Service Fabric olay verileri.
