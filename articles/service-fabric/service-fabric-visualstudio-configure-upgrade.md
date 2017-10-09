---
title: "Service Fabric uygulaması aaaConfigure hello yükseltme | Microsoft Docs"
description: "Nasıl tooconfigure hello ayarları Microsoft Visual Studio kullanarak bir Service Fabric uygulama yükseltme için bilgi edinin."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Visual Studio'da bir Service Fabric uygulaması Hello yükseltmesini yapılandırın
Azure Service Fabric için Visual Studio Araçları toolocal veya uzak bir küme yayımlamak için yükseltme desteği sağlar. Test ve hata ayıklama sırasında Merhaba uygulaması değiştirme yerine, uygulama tooa daha yeni sürümü tooupgrade istediğiniz üç senaryo vardır:

* Uygulama verileri hello yükseltme sırasında kaybı olmayacaktır.
* Olmayacak şekilde hello yükseltme sırasında herhangi bir hizmet kesintisi yükseltme etki alanları arasında yeterli hizmet örnekleri yaymak ise yüksek kullanılabilirlik kalır.
* Bunu yükseltilirken testleri bir uygulamaya karşı çalıştırabilirsiniz.

## <a name="parameters-needed-tooupgrade"></a>Parametreler tooupgrade gerekli
İki dağıtım türlerinden birini seçebilirsiniz: normal veya yükseltme. Bir yükseltme dağıtımı, korur ancak normal dağıtım tüm önceki dağıtım bilgileri ve verileri hello kümede siler. Visual Studio'da bir Service Fabric uygulaması yükselttiğinizde tooprovide uygulama yükseltme parametreleri ve sistem durumu denetimi ilkeleri gerekir. Uygulama yükseltme parametreleri Yardım sistem durumu denetimi ilkeleri hello yükseltme başarılı olup olmadığını belirlenirken hello yükseltme denetler. Bkz: [Service Fabric uygulama yükseltme: yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) daha fazla ayrıntı için.

Üç yükseltme modu vardır: *izlenen*, *UnmonitoredAuto*, ve *UnmonitoredManual*.

* İzlenen yükseltme hello yükseltme ve uygulama otomatikleştirir sistem durumu denetimi.
* Hello yükseltme UnmonitoredAuto yükseltme otomatik hale getirir, ancak uygulama sistem durumu denetimi atlar hello.
* UnmonitoredManual yükseltme yaptığınızda, toomanually gereken her bir yükseltme etki alanı yükseltme.

Her yükseltme modu parametreleri farklı kümelerini gerektirir. Bkz: [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) toolearn hello kullanılabilir yükseltme seçenekleri hakkında daha fazla bilgi.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Visual Studio'da bir Service Fabric uygulama yükseltme
Merhaba Visual Studio Service Fabric araçları tooupgrade Service Fabric uygulaması kullanıyorsanız, yayımlama işlemi toobe normal dağıtım yerine yükseltme hello denetleyerek belirtebilirsiniz **yükseltme Merhaba uygulaması** denetleyin bir kutu.

### <a name="tooconfigure-hello-upgrade-parameters"></a>tooconfigure hello yükseltme parametreleri
1. Merhaba tıklatın **ayarları** düğmesi sonraki toohello onay kutusu. Merhaba **yükseltme parametreleri Düzenle** iletişim kutusu görüntülenir. Merhaba **yükseltme parametreleri Düzenle** iletişim kutusu hello izlenen, UnmonitoredAuto ve UnmonitoredManual yükseltme modlarını destekler.
2. Toouse istediğiniz ve hello parametre Kılavuz doldurun hello yükseltme modu seçin.

    Her parametre varsayılan değerlerine sahip. İsteğe bağlı parametre hello *DefaultServiceTypeHealthPolicy* bir karma tablosu girişi alır. Merhaba karma tablosu için giriş biçimi örneği şudur *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* hello bir karma tablosu girdi alır başka bir isteğe bağlı parametre izlemektir biçimi:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Gerçekçi örneği aşağıdadır:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. UnmonitoredManual yükseltme modu seçerseniz, el ile bir PowerShell konsol toocontinue başlamalı ve hello yükseltme işlemini tamamlayın. Çok başvuran[Service Fabric uygulama yükseltme: Gelişmiş konular](service-fabric-application-upgrade-advanced.md) toolearn nasıl el ile yükseltme çalışır.

## <a name="upgrade-an-application-by-using-powershell"></a>PowerShell kullanarak uygulama yükseltme
PowerShell cmdlet'leri tooupgrade Service Fabric uygulaması kullanabilirsiniz. Bkz: [Service Fabric uygulama yükseltme öğretici](service-fabric-application-upgrade-tutorial.md) ve [başlangıç ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) ayrıntılı bilgi için.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Bir sistem durumu denetimi İlkesi hello uygulama bildirim dosyasında belirtin
Her bir Service Fabric uygulaması hizmetinde hello varsayılan değerleri geçersiz kılmak kendi sistem durumu ilkesi parametrelerine sahip olabilirsiniz. Bu parametre değerlerini hello uygulama bildirim dosyasında sağlayabilir.

Merhaba aşağıdaki örnek tooapply benzersiz bir sistem durumu ilkesi hello uygulama bildiriminde her hizmet için nasıl kontrol edin gösterir.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Sonraki adımlar
Bir uygulama dağıtımı hakkında daha fazla bilgi için bkz: [Azure Service Fabric, var olan bir uygulamayı dağıtmak](service-fabric-deploy-existing-app.md).