---
title: Azure Service Fabric ile aaaReport ve onay durumunu | Microsoft Docs
description: "Hizmet kodunuzdan nasıl toosend durumu raporları ve toocheck hello durumu, Azure Service Fabric hello sistem durumu izleme araçları kullanarak hizmetinizin nasıl sağladığını öğrenin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Hizmet durumunu raporlama ve denetleme
Hizmetlerinizin sorunlarla, özelliği toorespond tooand düzeltme olaylar ve kesintileri bağlıdır özelliği toodetect hello sorunlarınızı hızla. Sorunları ve hataları toohello Azure Service Fabric sistem durumu Yöneticisi hizmeti kodunuzdan rapor standart sistem durumu izleme Service Fabric toocheck hello sistem durumunu sağlar araçları kullanabilirsiniz.

Merhaba hizmetinden sistem durumu raporu olan üç yolu vardır:

* Kullanım [bölüm](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) veya [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) nesneleri.  
  Merhaba kullanabilirsiniz `Partition` ve `CodePackageActivationContext` tooreport hello hello geçerli bağlam parçası olan öğeleri durumunu nesneleri. Örneğin, bir çoğaltma bir parçası olarak çalışan bir kod yalnızca bu çoğaltma, ait hello bölüm ve bir parçası olan hello uygulama sistem durumu bildirebilirsiniz.
* Kullanım `FabricClient`.   
  Kullanabileceğiniz `FabricClient` tooreport durumu hello küme değilse hello hizmet kodundan [güvenli](service-fabric-cluster-security.md) veya yönetici ayrıcalıkları olan hello Hizmeti çalışıyorsa. Çoğu gerçek dünya senaryoları değil güvenli olmayan kümeler kullanın veya yönetici ayrıcalıkları sağlayın. İle `FabricClient`, sistem durumu hello kümesinin parçası olan herhangi bir varlıkta bildirebilirsiniz. İdeal olarak, ancak hizmet kod yalnızca ilgili tooits kendi sistem durumu raporları göndermesi gerekir.
* Merhaba REST API'leri hello küme, uygulama, dağıtılan bir uygulama, hizmet, hizmet paketi, bölüm, çoğaltma veya düğüm düzeylerini kullanın. Bu, kullanılan tooreport durumu bir kapsayıcı içinde olabilir.

Bu makalede, hello hizmet kodundan durumu raporları bir örnek adım adım anlatılmaktadır. Service Fabric tarafından sağlanan hello araçları kullanılan toocheck hello sistem durumunu nasıl olabilir Hello örnek ayrıca gösterir. Bu makalede Hızlı Giriş toohello durumunu Service Fabric yeteneklerini izleme hedeflenen toobe olduğu. Daha ayrıntılı bilgi için bu makalenin hello sonunda hello bağlantıyla Başlat sistem durumu hakkında ayrıntılı makaleleri hello dizi okuyabilir.

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdakilerin yüklü olması gerekir:

* Visual Studio 2015 veya Visual Studio 2017
* Service Fabric SDK

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate yerel güvenli geliştirme küme
* PowerShell'i yönetici ayrıcalıklarıyla açın ve hello aşağıdaki komutları çalıştırın:

![Gösteren nasıl komutları toocreate güvenli geliştirme küme](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy bir uygulama ve sistem durumu denetleyin
1. Visual Studio'yu yönetici olarak açın.
2. Hello kullanarak bir proje oluşturma **durum bilgisi olan hizmet** şablonu.
   
    ![Durum bilgisi olan hizmeti ile bir Service Fabric uygulaması oluşturma](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Tuşuna **F5** toorun hello uygulama hata ayıklama modunda. Merhaba, dağıtılan toohello yerel küme uygulamasıdır.
4. Merhaba uygulaması çalıştırdıktan sonra hello bildirim alanında hello yerel Küme Yöneticisi simgesini sağ tıklatın ve seçin **yerel kümeyi Yönet** hello kısayol menüsü tooopen Service Fabric Explorer gelen.
   
    ![Bildirim alanından Service Fabric Explorer'ı açın](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. Bu görüntü olduğu gibi Hello uygulama sağlığını görüntülenmesi gerekir. Şu anda Merhaba uygulaması hatasız sağlıklı olmalıdır.
   
    ![Service Fabric Explorer'da sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Ayrıca, hello sistem durumu PowerShell kullanarak da kontrol edebilirsiniz. Kullanabileceğiniz ```Get-ServiceFabricApplicationHealth``` uygulamanın durumu ve kullanabilir toocheck ```Get-ServiceFabricServiceHealth``` toocheck bir hizmetin sistem durumu. hello ait hello sistem durumu raporu aynı PowerShell'de bu görüntüde uygulamasıdır.
   
    ![PowerShell'de sağlıklı uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>tooadd özel durum olayları tooyour servis kodu
Visual Studio'da Hello Service Fabric proje şablonları örnek kod içerir. Merhaba aşağıdaki adımlar hizmet kodunuzdan özel durum olayları nasıl raporlayabilirsiniz gösterir. Bu raporlar otomatik olarak durumunu Service Fabric, Service Fabric Explorer, Azure portal durum görünümü ve PowerShell gibi sağladığı izleme için standart araçları hello gösterilir.

1. Visual Studio'da daha önce oluşturduğunuz hello uygulamasını yeniden açın veya hello kullanarak yeni bir uygulama oluşturma **durum bilgisi olan hizmet** Visual Studio şablonu.
2. Merhaba Stateful1.cs dosyasını açın ve hello bulun `myDictionary.TryGetValueAsync` hello çağrı `RunAsync` yöntemi. Bu yöntem döndürdüğünü gördüğünüz bir `result` bu uygulamada hello anahtar mantığı tookeep sayısı çalışıyor olduğundan ayrı tutma hello sayacının geçerli değeri hello. Bu gerçek bir uygulamada olsaydı ve bir hata sonucu hello eksikliği temsil varsa, bu olay tooflag istersiniz.
3. tooreport bir hata sonucu hello eksikliği temsil eden bir sistem durumu olayı aşağıdaki adımları hello ekleyin.
   
    a. Merhaba eklemek `System.Fabric.Health` ad alanı toohello Stateful1.cs dosya.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Koddan sonra hello hello eklemek `myDictionary.TryGetValueAsync` çağırın
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Bir durum bilgisi olan hizmetinden raporlandığını çünkü biz çoğaltma sistem durumu raporu. Merhaba `HealthInformation` parametre rapor edilen hello sistem durumu sorun hakkında bilgi depolar.
   
    Durum bilgisiz hizmet oluşturduysanız koddan hello kullanın
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Hizmetinizin yönetici ayrıcalıklarıyla çalıştığından veya hello küme değilse [güvenli](service-fabric-cluster-security.md), de kullanabilirsiniz `FabricClient` aşağıdaki adımları hello gösterildiği gibi tooreport sistem durumu.  
   
    a. Merhaba oluşturma `FabricClient` örneği hello sonra `var myDictionary` bildirimi.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Koddan sonra hello hello eklemek `myDictionary.TryGetValueAsync` çağırın.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Şimdi bu arızanın benzetimini gerçekleştirin ve bunu hello sistem durumu izleme araçları görünmesini bakın. toosimulate hello hatası, yorum hello sistem durumu raporlama daha önce eklediğiniz kodu hello ilk satırı çıkışı. Merhaba ilk satırını açıklama sonra hello kodu örneği aşağıdaki hello gibi görünecektir.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Bu kod hello sistem durumu raporu her zaman harekete `RunAsync` yürütür. Merhaba değişiklik yaptıktan sonra basın **F5** toorun Merhaba uygulaması.
6. Merhaba uygulaması çalıştırdıktan sonra Service Fabric Explorer toocheck hello hello uygulama durumunu açın. Bu süre, Service Fabric Explorer hello uygulamanın sağlıksız olduğunu gösterir. Daha önce eklediğimiz hello koddan bildirilen hello hata nedeniyle budur.
   
    ![Service Fabric Explorer'da düzgün çalışmayan uygulama](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Merhaba ağaç görünümünde Service Fabric Explorer hello birincil çoğaltma seçerseniz, görürsünüz **sistem durumu** çok bir hata gösterir. Service Fabric Explorer da olan Ayrıntılar eklenen toohello hello sistem durumu raporu görüntüler `HealthInformation` hello kodu parametresi. Gördüğünüz hello aynı sistem durumu raporlarının PowerShell ve Azure portal hello.
   
    ![Service Fabric Explorer'da çoğaltma durumu](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Bu çoğaltma silinene kadar veya başka bir raporu tarafından değiştirilene kadar bu rapor hello sistem durumu Yöneticisi'nde kalır. Biz ayarlanmamış olduğundan `TimeToLive` hello bu sistem durumu raporu için `HealthInformation` nesne hello rapor her zaman geçerli olsun.

Sistem durumu hello çoğaltma bu durumda olan hello en parçalı düzeyde, bildirilen olduğunu öneririz. Üzerindeki sistem durumu bildirebilirsiniz `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

tooreport sistem durumunu `Application`, `DeployedApplication`, ve `DeployedServicePackage`, kullanmak `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric sistem üzerinde derin Dalış](service-fabric-health-introduction.md)
* [Hizmet durumu raporlama için REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [Uygulama durumu raporlama için REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

