---
title: "Azure Service Fabric uygulaması Yönetimi otomatikleştirmek | Microsoft Docs"
description: "Dağıtma, yükseltme, test ve PowerShell kullanarak Service Fabric uygulamaları kaldırın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: fb3c2a77ea887289eebf343e223c190781d0e4c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-the-application-lifecycle-using-powershell"></a>PowerShell kullanarak uygulama yaşam döngüsü otomatikleştirme
Pek çok görünüşünün [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) otomatikleştirilebilir.  Bu makalede PowerShell dağıtma, yükseltme, kaldırma ve Azure Service Fabric uygulamaları test etmek için ortak görevleri otomatik hale getirmek için nasıl kullanılacağı gösterilmektedir.  Yönetilen ve HTTP API'leri uygulama yönetimi için de kullanılabilir. Bkz: [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) daha fazla bilgi için.  

## <a name="prerequisites"></a>Ön koşullar
Makaleyi görevleri geçmeden önce yaptığınızdan emin olun:

* Açıklanan Service Fabric kavramları hakkında bilgi edinmek [Service Fabric teknik genel bakış](service-fabric-technical-overview.md).
* [Çalışma zamanı, SDK'yı ve araçları yüklemek](service-fabric-get-started.md), hangi de yükler **ServiceFabric** PowerShell modülü.
* [PowerShell betik yürütmesini etkinleştirme](service-fabric-get-started.md#enable-powershell-script-execution).
* Yerel küme başlatın.  Yönetici olarak yeni bir PowerShell penceresi başlatın ve ardından SDK klasöründeki Küme kurulumu betiğini çalıştırın:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Bu makaledeki tüm PowerShell komutları çalıştırmadan önce ilk yerel Service Fabric kümesi kullanarak bağlanmak [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Aşağıdaki görevler için yükseltme dağıtmak için v1 uygulama paketi ve v2 uygulama paketi gerektirir. Karşıdan [ **WordCount** örnek uygulama](http://aka.ms/servicefabricsamples) (Başlarken örneklerinde bulunur). Yapı ve Visual Studio'da Uygulama paketi (sağ tıklayın **WordCount** Çözüm Gezgini'nde ve select **paket**). V1 Kopyala `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` için `C:\Temp\WordCount`. Kopya `C:\Temp\WordCount` için `C:\Temp\WordCountV2`, yükseltme için v2 uygulama paketi oluşturma. Açık `C:\Temp\WordCountV2\ApplicationManifest.xml` bir metin düzenleyicisinde. İçinde **ApplicationManifest** öğe, değişiklik **ApplicationTypeVersion** "1.0.0" özniteliğine "2.0.0 uygulamanın sürüm numarasını güncelleştirmek için". Değiştirilen ApplicationManifest.xml dosyasını kaydedin.

## <a name="task-deploy-a-service-fabric-application"></a>Görev: Service Fabric uygulaması dağıtma
Yerleşik ve paketlenmiş uygulama (veya uygulama paketi İndirildikten sonra), yerel bir Service Fabric kümesi uygulamasına dağıtabilirsiniz. Dağıtım, uygulama paketini karşıya yükleme, uygulama türünü kaydetme ve uygulama örneği oluşturma içerir. Bir kümeye yeni bir uygulama dağıtmak için bu bölümdeki yönergeleri kullanın.

### <a name="step-1-upload-the-application-package"></a>1. adım: uygulama paketini karşıya yükleyin
Uygulama paketi görüntü deposuna karşıya yükleme, bir konumda iç Service Fabric bileşenleri için erişilebilir koyar.  Uygulama paketi gerekli uygulama bildirimini, hizmet bildirimlerini ve kod, yapılandırma ve uygulama ve hizmet örneği oluşturmak için veri paketleri içerir. Uygulama paketi yerel olarak doğrulamak istiyorsanız, kullanmak [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet'i.  [Kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu paketi yükler. Örneğin:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-the-application-type"></a>2. adım: uygulama türünü kaydetme
Uygulama paketi kaydetme, uygulama türü ve sürümü kullanmak için kullanılabilir uygulama bildiriminde bildirilen hale getirir. Paketin karşıya adım 1 ' de sistem okuma paket doğrulayın (çalışan eşdeğer [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) yerel olarak), paket içeriğini işlemek ve işlenen paket için bir iç sistem kopyalayın konum.  Çalıştırma [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
Kümede kayıtlı tüm uygulama türlerini görmek için Çalıştır [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-the-application-instance"></a>3. adım: uygulama örneği oluşturma
Bir uygulama kullanarak başarıyla kaydettirildi herhangi bir uygulama türü sürümü kullanılarak oluşturulabilir [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) komutu. Her uygulamanın adını bildirilen adresindeki zaman dağıtmak ve ile başlamalıdır **doku:** düzen ve her bir uygulama örneği için benzersiz olmalıdır. Uygulama türü adı ve uygulama türü sürümü içinde bildirilen **ApplicationManifest.xml** uygulama paketi dosyası. Varsayılan hizmetlerin hedef uygulama türü uygulama bildiriminde tanımlanmış ise, bunlar şu anda oluşturulur.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

[Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) komutu başarıyla, genel durumlarıyla birlikte oluşturulan tüm uygulama örnekleri listeler. [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) komutu listeler tüm hizmet örnekleri içinde verilen uygulama örneği başarıyla oluşturuldu. Varsayılan hizmetler (varsa) listelenir.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Görev: Service Fabric uygulama yükseltme
Güncelleştirilmiş uygulama paketine sahip daha önce dağıtılan bir Service Fabric uygulama yükseltme yapabilirsiniz. Bu görev, dağıtılan WordCount uygulamasını yükseltme "görevi: Deploy a Service Fabric application." Okuyun [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md) daha fazla bilgi için.

Örneği için bu örneği basit tutmak için Önkoşullar oluşturulan WordCountV2 uygulama paketine yalnızca uygulamanın sürüm numarasını güncelleştirildi. Hizmet kod, yapılandırma veya veri dosyalarını güncelleştirmek ve ardından yeniden oluşturma ve güncelleştirilmiş sürüm numaralarıyla Uygulama paketleme daha gerçekçi bir senaryo içerir.  

### <a name="step-1-upload-the-updated-application-package"></a>1. adım: güncelleştirilmiş uygulama paketini karşıya yükleyin
WordCount v1 uygulama yükseltilmesi hazırdır. Yönetici ve türü bir PowerShell penceresi açarsanız [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), WordCount uygulama türü 1.0.0 sürümünün dağıtıldığı bakın.  

Şimdi güncelleştirilmiş uygulama paketi (uygulama paketlerini Service Fabric tarafından depolandığı) Service Fabric Image store kopyalayın. Parametre **ApplicationPackagePathInImageStore** Service Fabric burada da bulabilir uygulama paketi bildirir. Uygulama paketi için aşağıdaki komutu kopyalar **WordCountV2** Image store içinde:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-the-updated-application-type"></a>2. adım: güncelleştirilmiş uygulama türünü kaydetme
Uygulamanın yeni sürümü kullanılarak gerçekleştirilen Service Fabric ile kaydetmek için sonraki adımdır [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-the-upgrade"></a>3. adım: yükseltme Başlat
Uygulama yükseltme çeşitli yükseltme parametreleri, zaman aşımları ve durumu ölçütlerini uygulanabilir. Okuyun [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) ve [yükseltme işlemi](service-fabric-application-upgrade.md) daha fazla bilgi için belgeler. Tüm hizmetler ve örnekleri olmalıdır *sağlıklı* yükselttikten sonra.  Ayarlama **HealthCheckStableDuration** 60 saniye (Hizmetleri için bir sonraki yükseltme etki alanına yükseltmeye devam etmeden önce en az 20 saniye için sağlıklı; böylece).  Ayrıca **UpgradeDomainTimeout** 1200 saniye ve **UpgradeTimeout** 3000 saniye. Son olarak, ayarlamak **UpgradeFailureAction** için **geri alma**, yükseltme sırasında hataları karşılaştıysanız Service Fabric uygulamayı önceki sürüme geri alındığında ister.

Kullanarak uygulama yükseltme şimdi başlatabilirsiniz [başlangıç ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Uygulama adı daha önce dağıtılan v1.0.0 uygulama adı ile aynı olduğunu unutmayın (fabric: / WordCount). Service Fabric, hangi uygulamanın yükseltilir tanımlamak için bu ad kullanır. Zaman aşımı çok kısa olacak şekilde ayarlarsanız sorunu bildiren bir zaman aşımı hatası iletisi karşılaşabilirsiniz. Başvurmak [uygulama yükseltmelerinde sorun giderme](service-fabric-application-upgrade-troubleshooting.md), veya zaman aşımları artırın.

### <a name="step-4-check-upgrade-progress"></a>4. adım: Onay yükseltme işlemi ilerleme durumu
Kullanarak uygulama yükseltme ilerleme durumunu izleyebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), veya kullanarak [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

Birkaç dakika içinde [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet'i gösterilmektedir tüm yükseltme etki alanlarının yükseltilen (tamamlandı).

## <a name="task-test-a-service-fabric-application"></a>Görevi: Service Fabric uygulaması Test
Yüksek kaliteli Hizmetleri yazmak için geliştiriciler hizmetlerini kararlılığını test etmek için güvenilir altyapı hataları anlamına olması gerekir. Service Fabric geliştiriciler hataya Eylemler anlamına ve Hizmetleri hataları varlığında chaos ve yük devretme testi senaryolarını kullanarak test olanağı sağlar.  Okuyun [hata analizi hizmetine giriş](service-fabric-testability-overview.md) ek bilgi için.

### <a name="step-1-run-the-chaos-test-scenario"></a>1. adım: chaos test senaryosu çalıştırma
Chaos test senaryosu hataları tüm Service Fabric kümesi oluşturur. Senaryo genellikle ay veya yıl ile birkaç saat içinde görülen hataları sıkıştırır. Yüksek hata oranı araya eklemeli hataları birleşimi, aksi takdirde eksik köşe durumlarda bulur. Aşağıdaki örnek chaos test senaryosu için 60 dakika çalışır.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-the-failover-test-scenario"></a>2. adım: yük testi senaryosuna çalıştırma
Yük devretme sınamasını senaryo hedefleri tüm küme yerine belirli hizmet bölümü ve diğer hizmetleri etkilenmemesini bırakır. İş mantığınızın çalışırken hizmet doğrulama benzetimli hataları bir dizi senaryo dolaşır. Bir hizmet doğrulama hatası daha fazla araştırma gereken bir sorun olduğunu gösterir. Yük devretme testi birden çok hataları anlamına chaos test senaryosu aksine her seferinde yalnızca bir arıza uygulanmasını. Aşağıdaki örnek 60 dakika için yük devretme testi doku karşı çalışır: / WordCount/WordCountService hizmet.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Görevi: Service Fabric uygulaması kaldırma
Dağıtılan bir uygulama örneğini silmek, sağlanan uygulama türü kümeden kaldırma ve uygulama paketi görüntü kaldırın.

### <a name="step-1-remove-an-application-instance"></a>1. adım: uygulama örneğini kaldırma
Uygulama örneğini artık gerekli olmadığında kalıcı olarak kullanarak kaldırabilirsiniz [Kaldır ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet'i. Bu da otomatik olarak tüm hizmet durumunu kalıcı olarak kaldırma uygulamaya ait tüm hizmetlere kaldırır. Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-the-application-type"></a>2. adım: uygulama türü kaydını kaldırma
Belirli bir uygulama türü sürümü artık gerektiğinde kullanarak kaydı [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet'i. Kullanılmayan türleri kaydını Image store uygulama paketinde tarafından kullanılan depolama alanını serbest bırakır. Bu karşı veya kendisine başvuran uygulama yükseltmelerini bekleyen örneği hiç uygulama vardır sürece uygulama türü kaydı olabilir.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-the-application-package"></a>3. adım: uygulama paketini kaldırma
Uygulama türü kaydı olduktan sonra uygulama paketi görüntü deposundan kullanarak Kaldırılabilir [Kaldır ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md)

[Bir uygulamayı dağıtma](service-fabric-deploy-remove-applications.md)

[Uygulama yükseltme](service-fabric-application-upgrade.md)

[Azure Service Fabric cmdlet'leri](/powershell/azure/overview?view=azureservicefabricps)

