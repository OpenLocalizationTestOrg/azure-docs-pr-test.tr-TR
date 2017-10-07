---
title: "aaaAzure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "Nasıl Service Fabric PowerShell kullanarak toodeploy ekleme ve kaldırma uygulamalarda."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Dağıtma ve PowerShell kullanarak uygulamaları kaldırma
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API’leri](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Bir kez bir [uygulama türü paketlenmiş][10], Azure Service Fabric kümesi içine dağıtımı için hazırdır. Dağıtım hello aşağıdaki üç adımları içerir:

1. Merhaba uygulama paketi toohello görüntü deposuna karşıya yükleme
2. Merhaba uygulama türünü kaydetme
3. Merhaba uygulama örneği oluşturma

Bir uygulamanın dağıtıldığını ve bir örnek hello kümede çalışan sonra hello uygulama örneği ve uygulama türünü silebilirsiniz. bir uygulama hello kümeden toocompletely Kaldır hello aşağıdaki adımları içerir:

1. Uygulama örneğini çalıştıran hello Kaldır (veya Sil)
2. Artık ihtiyacınız varsa hello uygulama türü kaydını kaldırma
3. Merhaba görüntü deposundan Hello uygulama paketini kaldırma

Kullanırsanız [uygulamalarında hata ayıklama ve dağıtma için Visual Studio](service-fabric-publish-app-remote-cluster.md) yerel geliştirme kümenizde yukarıdaki adımların tümünü hello bir PowerShell komut dosyası otomatik olarak işlenir.  Bu komut dosyası hello bulunan *komut dosyaları* hello uygulama projesi klasörü. Bu makalede, gerçekleştirebilmeleri için komut dosyası yaptıklarını üzerinde arka plan sağlar hello Visual Studio dışında aynı işlemleri. 
 
## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın
Bu makaledeki tüm PowerShell komutları çalıştırmadan önce her zaman başlamayı [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric kümesi. Merhaba aşağıdaki komutu çalıştırarak tooconnect toohello yerel geliştirme kümesi:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Bağlantı tooa uzaktan küme veya küme Azure Active Directory, X509 kullanılarak güvenli örnekleri için sertifikalar veya Windows Active Directory bkz [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Merhaba uygulama paketini karşıya yükleyin
Karşıya yükleme hello uygulama paketi iç Service Fabric bileşenleri tarafından erişilebilen bir konumda koyar.
Tooverify hello uygulama paketi yerel olarak istiyorsanız hello kullanın [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.

Merhaba [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) karşıya hello uygulama paketi toohello küme Image store komutu.
Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.  çalıştırma tooimport hello SDK Modülü:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio 2015'te. Varsayılan olarak, "MyApplicationType" Merhaba ApplicationManifest.xml listelenen hello uygulama türü adı bağlıdır.  Merhaba hello gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\<kullanıcıadı\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*. 

Merhaba aşağıdaki komut hello uygulama paketinin Merhaba içeriğine listeler:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Merhaba uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package). Merhaba sıkıştırma hello boyutunu ve dosya hello sayısını azaltır.
Merhaba yan etkisi olan, kaydetme ve kayıt hello uygulama türü daha hızlı. Özellikle hello zaman toocompress hello paketi eklerseniz karşıya yükleme zamanı şu anda, yavaş olabilir. 

toocompress bir paket kullanım hello aynı [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu. Sıkıştırma yapılabilir ayrı karşıya yükleme işlemini hello kullanarak `SkipCopy` bayrak veya hello ile birlikte karşıya yükleme işleminde. Sıkıştırılmış paketi üzerinde sıkıştırma uygulama yok.
toouncompress kullanımı bir sıkıştırılmış paket hello aynı [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello komutunu `UncompressPackage` geçin.

Merhaba aşağıdaki cmdlet'i hello paket toohello Image store kopyalamadan sıkıştırır. Merhaba paket artık hello sıkıştırılmış dosyaları içerir `Code` ve `Config` paketler. birçok dahili işlemleri (örneğin, paket paylaşımı, belirli doğrulamaları için uygulama türü adı ve sürümü ayıklama) için gerekli olduğu için hello uygulama ve hello hizmet bildirimlerini, daraltılmış değil. Sıkıştırma hello bildirimleri bu işlemleri verimli hale getirir.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Büyük uygulama paketlerini hello sıkıştırma zaman alır. En iyi sonuçlar için hızlı bir SSD sürücüsü kullanın. Ayrıca Hello sıkıştırma zamanları ve hello sıkıştırılmış paket hello boyutunu hello paket içeriğini göre farklılık.
Örneğin, hello ilk göstermek ve hello sıkıştırma süresiyle sıkıştırılmış paket boyutu hello bazı paketler için sıkıştırma istatistikleri aşağıdadır.

|Başlangıç boyutu (MB)|Dosya sayısı|Sıkıştırma zamanı|Sıkıştırılmış paket boyutu (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Bir paket sıkıştırılmış sonra karşıya yüklenen tooone olabilir veya birden çok Service Fabric gerektiği kümeleri. Merhaba dağıtım için sıkıştırılmış ve sıkıştırılmamış paketleri aynı mekanizmadır. Hello paket sıkıştırılmışsa, bu nedenle hello küme görüntü deposunda depolanır ve hello uygulamayı çalıştırmadan önce hello düğümde sıkıştırılmamış.


Merhaba aşağıdaki örnek hello paket toohello Image store "MyApplicationV1" adlı bir klasöre yükler:

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.  çalıştırma tooimport hello SDK Modülü:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Merhaba belirtmezseniz *- ApplicationPackagePathInImageStore* parametresi, hello uygulama paketi hello Image store hello "Hata ayıklama" klasörüne kopyalanır.

tooupload bir paket hello süresini birden çok faktörlere bağlı olarak farklılık gösterir. Bu etkenler hello paketi, başlangıç paket boyutu ve hello dosya boyutları dosya hello sayısı bazılarıdır. Merhaba ağ hızı hello kaynak makineyle hello Service Fabric kümesi arasında da hello karşıya yükleme zamanı etkiler. için varsayılan zaman aşımı hello [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 30 dakikadır.
Bağlı olarak açıklanan faktörleri Merhaba, tooincrease hello zaman aşımı olabilir. Merhaba paket hello kopya çağrısında sıkıştırma, tooalso gerekir hello sıkıştırma zaman göz önünde bulundurun.

Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.

## <a name="register-hello-application-package"></a>YAZMAÇ hello uygulama paketi
Merhaba uygulama türü ve sürümü hello uygulama paketi kaydedildikten sonra kullanılabilir hale hello uygulama bildiriminde bildirildi. Merhaba sistem hello önceki adımda karşıya yüklenen hello paket okur hello paket doğrular, hello paket içeriğini işler ve işlenen hello paket tooan iç sistem konumuna kopyalar.  

Merhaba çalıştırmak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello kümedeki uygulama türü ve dağıtımı için kullanılabilir hale getirin:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" Merhaba uygulama paketinin bulunduğu hello Image store hello klasöründe bulunur. Merhaba uygulama türü adı "MyApplicationType" Sürüm "1.0.0" (her ikisi de hello uygulama bildiriminde bulunur) ile artık hello kümesinde kayıtlı.

Merhaba [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) komut, yalnızca hello sistem başarıyla kaydedildi hello uygulama paketine sahip olduktan sonra döndürür. Ne kadar süreyle kayıt alır hello boyutu ve hello uygulama paketinin içeriğini bağlıdır. Gerekirse, hello **- TimeoutSec** parametresi kullanılan toosupply daha uzun bir süre olabilir (Merhaba varsayılan zaman aşımı olan 60 saniye).

Paket veya zaman aşımına uğruyor, hello kullanın. büyük bir uygulamanız varsa, **- zaman uyumsuz** parametresi. Merhaba komut hello küme hello register komutunun kabul eder ve gerektiği gibi hello işleme devam ettiğinde döndürür.
Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler. Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Bir uygulamadan hello kullanarak başarıyla kaydettirildi herhangi bir uygulama türü sürümü örneği [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet'i. her uygulamanın Hello adı hello ile başlamalı *"fabric:"* düzen ve her bir uygulama örneği için benzersiz olmalıdır. Hello uygulama bildiriminde hello hedef uygulama türünün tanımlı hiçbir varsayılan hizmetleri de oluşturulur.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir. Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlem ile çalışır.

uygulamalar ve hizmetler olarak adlandırılan toosee hello çalıştırmak hello kümede çalışan [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) ve [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Bir uygulamayı kaldırma
Uygulama örneğini artık gerekli olmadığında kalıcı olarak hello kullanarak adıyla kaldırabilirsiniz [Kaldır ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet'i. [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) tüm hizmet durumunu da, kalıcı olarak kaldırma toohello uygulama ait tüm hizmetleri otomatik olarak kaldırır. 

> [!WARNING]
> Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Bir uygulama türü kaydını kaldırma
Belirli bir uygulama türü sürümü artık gerekli olmadığında hello kullanarak hello uygulama türü kaydını kaldırma [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet'i. Merhaba Image store tarafından kullanılan kaydı siliniyor kullanılmayan uygulama türleri sürümleri depolama alanı. Uygulama türü olarak hiçbir uygulamaları karşı oluşturulur ve uygulama Beklemede yükseltmeler, Hayır başvurduğunuzdan sürece kaydı olabilir.

Çalıştırma [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello uygulama türleri şu anda kayıtlı hello kümede:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Çalıştırma [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister belirli uygulama türü:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Bir uygulama paketi hello görüntü deposundan kaldırır
Bir uygulama paketi artık gerekli olmadığında hello görüntü deposu toofree sistem kaynaklarının silebilirsiniz.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Sorun giderme
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Kopya ServiceFabricApplicationPackage bir ImageStoreConnectionString için sorar
Merhaba Service Fabric SDK ortam zaten hello Varsayılanlarını Ayarla doğru olması gerekir. Ancak gerekirse, hello ImageStoreConnectionString tüm komutlar için Service Fabric kümesi kullanarak bu hello hello değeri eşleşmelidir. Merhaba küme bildiriminde hello ImageStoreConnectionString bulabilirsiniz hello kullanarak alınan [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) ve Get-ImageStoreConnectionStringFromClusterManifest komutlar:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.  çalıştırma tooimport hello SDK Modülü:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Merhaba ImageStoreConnectionString hello küme bildiriminde bulunur:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.

### <a name="deploy-large-application-package"></a>Büyük uygulama paketini dağıtma
Sorun: [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) büyük uygulama paketi (GB sırasını) için zaman aşımına uğradı.
Deneyin:
- Daha büyük zaman aşımını belirtmek [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu ile `TimeoutSec` parametresi. Varsayılan olarak, hello zaman aşımı 30 dakikadır.
- Kaynak makine ve küme arasındaki Hello ağ bağlantısını denetleyin. Merhaba bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.
Merhaba istemci makine hello küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede hello küme olarak düşünün.
- Dış azaltma devreyi olmadığını denetleyin. Örneğin, Hello Image store yapılandırılmış toouse azure depolama olduğunda, karşıya yükleme kısıtlanan.

Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğradı. Deneyin:
- [Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.
Hello sıkıştırma hello boyutunu azaltır ve hangi sırayla hello trafik miktarını azaltır ve bu Service Fabric çalışma hello dosya sayısı, gerçekleştirmeniz gerekir. Merhaba karşıya yükleme işlemi (özellikle hello sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak daha hızlı kaydedin ve kaydı hello uygulama türü.
- Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.
- Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Merhaba komut hello küme hello komutu kabul eder ve hello uygulama türü hello kayıt zaman uyumsuz olarak devam ettiğinde döndürür. Bu nedenle, yoktur gerek toospecify daha yüksek bir zaman aşımı bu durumda. Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler. Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Birçok dosyalarıyla uygulama paketini dağıtma
Sorun: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).
Deneyin:
- [Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce. Merhaba sıkıştırma dosyaları hello sayısını azaltır.
- Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.
- Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Merhaba komut hello küme hello komutu kabul eder ve hello uygulama türü hello kayıt zaman uyumsuz olarak devam ettiğinde döndürür.
Bu nedenle, yoktur gerek toospecify daha yüksek bir zaman aşımı bu durumda. Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler. Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)

[Service Fabric sistem durumu giriş](service-fabric-health-introduction.md)

[Tanılama ve bir Service Fabric hizmeti sorun giderme](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulamada modeli](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
