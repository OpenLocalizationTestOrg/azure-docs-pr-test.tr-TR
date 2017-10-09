---
title: "Azure Service Fabric uygulaması Yönetimi aaaAutomate | Microsoft Docs"
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
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>PowerShell kullanarak hello uygulama yaşam döngüsü otomatikleştirme
Merhaba pek çok görünüşünün [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) otomatikleştirilebilir.  Bu makalede, dağıtma, yükseltme, kaldırma ve Azure Service Fabric uygulamaları test etmek için nasıl toouse PowerShell tooautomate ortak görevler gösterilmektedir.  Yönetilen ve HTTP API'leri uygulama yönetimi için de kullanılabilir. Bkz: [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) daha fazla bilgi için.  

## <a name="prerequisites"></a>Ön koşullar
Merhaba makalede toohello görevlerde taşımadan önce yaptığınızdan emin olun:

* Açıklanan hello Service Fabric kavramları hakkında bilgi edinmek [Service Fabric teknik genel bakış](service-fabric-technical-overview.md).
* [Merhaba çalışma zamanı, SDK'yı ve araçları yüklemek](service-fabric-get-started.md), hangi de yükler hello **ServiceFabric** PowerShell modülü.
* [PowerShell betik yürütmesini etkinleştirme](service-fabric-get-started.md#enable-powershell-script-execution).
* Yerel küme başlatın.  Yönetici olarak yeni bir PowerShell penceresi başlatın ve ardından hello SDK klasöründeki hello Küme kurulumu betiğini çalıştırın:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Bu makaledeki tüm PowerShell komutları çalıştırmadan önce ilk toohello yerel Service Fabric kümesi kullanarak bağlanmak [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* görevleri aşağıdaki hello v1 uygulama paketi toodeploy ve v2 uygulama paketi için yükseltme gerektirir. Merhaba karşıdan [ **WordCount** örnek uygulama](http://aka.ms/servicefabricsamples) (Merhaba Başlarken örnekleri bulunur). Derleme ve paket Merhaba uygulaması Visual Studio'da (sağ tıklayın **WordCount** Çözüm Gezgini'nde ve select **paket**). Kopya hello v1 paketinde `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` çok`C:\Temp\WordCount`. Kopya `C:\Temp\WordCount` çok`C:\Temp\WordCountV2`, yükseltme için hello v2 uygulama paketi oluşturma. Açık `C:\Temp\WordCountV2\ApplicationManifest.xml` bir metin düzenleyicisinde. Merhaba, **ApplicationManifest** öğe, değişiklik hello **ApplicationTypeVersion** çok "1.0.0" özniteliği "2.0.0" tooupdate hello uygulama sürüm numarası. Değiştirilen hello ApplicationManifest.xml dosyasını kaydedin.

## <a name="task-deploy-a-service-fabric-application"></a>Görev: Service Fabric uygulaması dağıtma
Yerleşik ve Merhaba uygulaması paketlenmiş (veya hello uygulama paketi İndirildikten sonra), yerel bir Service Fabric kümesi hello uygulamasına dağıtabilirsiniz. Dağıtım hello uygulama paketini karşıya yükleme, hello uygulama türünü kaydetme ve hello uygulama örneği oluşturma içerir. Bu bölümde toodeploy yeni bir uygulama tooa küme Hello yönergeleri kullanın.

### <a name="step-1-upload-hello-application-package"></a>1. adım: hello uygulama paketini karşıya yükleyin
Merhaba uygulama paketi toohello karşıya Image store, bir konum erişilebilir toointernal Service Fabric bileşenleri koyar.  Merhaba uygulama paketi hello gerekli uygulama bildirimini, hizmet bildirimlerini ve kod, yapılandırma ve veri paketleri toocreate hello uygulama ve hizmet örneklerini içerir. Tooverify hello uygulama paketi yerel olarak istiyorsanız hello kullanın [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet'i.  Merhaba [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) karşıya hello paket komutu. Örneğin:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>2. adım: hello uygulama türünü kaydetme
Kayıt hello uygulama paketi hello uygulama türü ve sürümü kullanmak için kullanılabilir hello uygulama bildiriminde bildirilen yapar. Merhaba sistemi hello adım 1 karşıya yüklenen hello paket okur, hello paketi doğrulanamıyor (eşdeğer toorunning [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) yerel olarak), işlem hello paket içeriğini ve işlenen hello paket tooan kopyalayın İç sistem konumu.  Merhaba çalıştırmak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
Tüm hello uygulama türleri kayıtlı hello çalıştırmak hello kümede toosee [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>3. adım: hello uygulama örneği oluşturma
Bir uygulama hello kullanarak başarıyla kaydettirildi herhangi bir uygulama türü sürümü kullanılarak oluşturulabilir [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) komutu. her uygulamanın Hello adı bildirilen adresindeki zaman dağıtmak ve hello ile başlamalıdır **doku:** düzen ve her bir uygulama örneği için benzersiz olmalıdır. Merhaba uygulama türü adı ve uygulama türü sürümü hello bildirilir **ApplicationManifest.xml** hello uygulama paketi dosyası. Varsayılan hizmetlerin hello uygulama bildiriminde hello hedef uygulama türü olarak tanımlanmış olan, bunlar şu anda oluşturulur.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Merhaba [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) komutu başarıyla, genel durumlarıyla birlikte oluşturulan tüm uygulama örnekleri listeler. Merhaba [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) komutu tüm içinde verilen uygulama örneği başarıyla oluşturuldu hello hizmet örnekleri listeler. Varsayılan hizmetler (varsa) listelenir.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Görev: Service Fabric uygulama yükseltme
Güncelleştirilmiş uygulama paketine sahip daha önce dağıtılan bir Service Fabric uygulama yükseltme yapabilirsiniz. Bu görev, dağıtılan hello WordCount uygulamasını yükseltme "görevi: Deploy a Service Fabric application." Okuyun [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md) daha fazla bilgi için.

Bu örneğin, yalnızca hello uygulamanın sürüm numarasını tookeep şeyler basit hello önkoşullarını oluşturulan hello WordCountV2 uygulama paketine güncelleştirildi. Hizmet kod, yapılandırma veya veri dosyalarını güncelleştirmek ve ardından yeniden oluşturma ve güncelleştirilmiş sürüm numaralarıyla hello Uygulama paketleme daha gerçekçi bir senaryo içerir.  

### <a name="step-1-upload-hello-updated-application-package"></a>1. adım: hello güncelleştirilmiş uygulama paketini karşıya yükleyin
Merhaba WordCount v1 uygulama yükseltme hazır toobe ' dir. Yönetici ve türü bir PowerShell penceresi açarsanız [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), hello WordCount uygulama türü 1.0.0 sürümünün dağıtıldığı bakın.  

Şimdi kopyalama hello (Merhaba uygulama paketlerini Service Fabric tarafından depolandığı) uygulama paketi toohello Service Fabric Image store güncelleştirildi. parametre hello **ApplicationPackagePathInImageStore** Service Fabric burada da bulabilir hello uygulama paketi bildirir. kopya uygulama paketi çok hello komutu aşağıdaki hello**WordCountV2** hello Image store içinde:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>2. adım: Kayıt hello uygulama türü güncelleştirildi.
Merhaba sonraki tooregister hello uygulamanın yeni sürümü hello hello kullanarak gerçekleştirilebilir Service Fabric ile adımdır [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>3. adım: Başlangıç hello yükseltme
Çeşitli yükseltme parametreleri, zaman aşımları ve durumu ölçütlerini uygulanan tooapplication yükseltmeler olabilir. Merhaba okuma [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) ve [yükseltme işlemi](service-fabric-application-upgrade.md) toolearn daha fazla belgeleri. Tüm hizmetler ve örnekleri olmalıdır *sağlıklı* hello yükselttikten sonra.  Set hello **HealthCheckStableDuration** too60 saniye (toohello hello yükseltme devam etmeden önce en az 20 saniye sonraki yükseltme etki alanı için hello Hizmetleri sağlıklı; böylece).  Ayrıca kümesi hello **UpgradeDomainTimeout** too1200 saniye ve hello **UpgradeTimeout** too3000 saniye. Son olarak, hello ayarlayın **UpgradeFailureAction** çok**geri alma**, hangi hataları yükseltme sırasında hata oluşursa, Service Fabric geri alındığında istekleri hello uygulama toohello önceki sürümü.

Hello kullanarak şimdi hello uygulama yükseltme başlatabilirsiniz [başlangıç ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Bu hello uygulama adı olduğu hello aynı hello v1.0.0 uygulama adı daha önce dağıtmış gibi not (fabric: / WordCount). Service Fabric hangi uygulamanın yükseltilir bu adı tooidentify kullanır. Merhaba zaman aşımlarını toobe çok kısa ayarlarsanız, durumları sorun hello bir zaman aşımı hatası iletisi karşılaşabilirsiniz. Çok başvuran[uygulama yükseltmelerinde sorun giderme](service-fabric-application-upgrade-troubleshooting.md), veya hello zaman aşımlarını artırın.

### <a name="step-4-check-upgrade-progress"></a>4. adım: Onay yükseltme işlemi ilerleme durumu
Kullanarak uygulama yükseltme ilerleme durumunu izleyebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), veya hello kullanarak [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

Birkaç dakika içinde hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet'i gösterilmektedir tüm yükseltme etki alanlarının yükseltilen (tamamlandı).

## <a name="task-test-a-service-fabric-application"></a>Görevi: Service Fabric uygulaması Test
toowrite yüksek kaliteli Hizmetleri, geliştiricilerin toobe mümkün tooinduce güvenilmez altyapı hataları tootest hello kararlılığını hizmetlerini gerekir. Service Fabric geliştiricilere hello özelliği tooinduce hata eylemleri sağlar ve chaos ve yük devretme testi senaryolarını kullanarak hataları hello varlığını test Hizmetleri'nde hello.  Okuyun [giriş toohello hata analizi hizmeti](service-fabric-testability-overview.md) ek bilgi için.

### <a name="step-1-run-hello-chaos-test-scenario"></a>1. adım: hello chaos test senaryosu çalıştırabilirsiniz
Merhaba chaos testi senaryosu hello tüm Service Fabric kümesi arasında hataları oluşturur. Merhaba senaryo genellikle birkaç saat ay veya yıl tooa görülen hataları sıkıştırır. yüksek hata oranı araya eklemeli hataları Hello birleşimi aksi eksik köşe durumları bulur. Merhaba aşağıdaki örnek hello chaos test senaryosu için 60 dakika çalışır.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>2. adım: hello yük devretme testi senaryosu çalıştırma
Merhaba yük devretme sınamasını senaryo hedefleri hello tüm küme yerine belirli hizmet bölümü ve diğer hizmetleri etkilenmemesini bırakır. İş mantığınızın çalışırken hello senaryo bir dizi hizmet doğrulama benzetimli hataları dolaşır. Bir hizmet doğrulama hatası daha fazla araştırma gereken bir sorun olduğunu gösterir. Hello yük devretme testi, aynı anda birden çok hataları anlamına karşılıklı toohello chaos testi senaryosu olarak yalnızca bir arıza uygulanmasını. Merhaba aşağıdaki örnek hello yük devretme testi 60 dakika hello doku karşı çalışır: / WordCount/WordCountService hizmet.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Görevi: Service Fabric uygulaması kaldırma
Dağıtılan bir uygulama örneğini silmek, sağlanan hello uygulama türü hello kümeden kaldırma ve görüntü hello hello uygulama paketi kaldırın.

### <a name="step-1-remove-an-application-instance"></a>1. adım: uygulama örneğini kaldırma
Uygulama örneğini artık gerekli olmadığında kalıcı olarak hello kullanarak kaldırabilirsiniz [Kaldır ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet'i. Bu da otomatik olarak tüm hizmet durumunu kalıcı olarak kaldırma toohello uygulama ait tüm hizmetlere kaldırır. Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>2. adım: hello uygulama türü kaydını kaldırma
Belirli bir uygulama türü sürümü artık gerektiğinde hello kullanarak kaydı [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet'i. Merhaba Image store hello uygulama paketi tarafından kullanılan kaydı siliniyor kullanılmayan türleri sürümleri depolama alanı. Bu karşı veya kendisine başvuran uygulama yükseltmelerini bekleyen örneği hiç uygulama vardır sürece uygulama türü kaydı olabilir.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>3. adım: hello uygulama paketini kaldırma
Merhaba uygulama türü kaydı olduktan sonra hello uygulama paketi hello görüntü deposundan hello kullanarak Kaldırılabilir [Kaldır ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md)

[Bir uygulamayı dağıtma](service-fabric-deploy-remove-applications.md)

[Uygulama yükseltme](service-fabric-application-upgrade.md)

[Azure Service Fabric cmdlet'leri](/powershell/azure/overview?view=azureservicefabricps)

