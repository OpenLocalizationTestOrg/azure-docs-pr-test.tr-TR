---
title: Azure Service Fabric uygulama aaaPackage | Microsoft Docs
description: "Nasıl toopackage tooa küme dağıtmadan önce bir Service Fabric uygulaması."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>Bir uygulama paketi
Bu makalede nasıl toopackage Service Fabric uygulama ve dağıtım için hazır olun.

## <a name="package-layout"></a>Paket düzeni
Hello uygulama bildirimi, bir veya daha fazla hizmet bildirimleri ve diğer gerekli paketi dosyaları bir Service Fabric kümesi içine dağıtımı için belirli bir düzende düzenlenmelidir. Bu makalede Hello örnek bildirimleri aşağıdaki dizin yapısını hello düzenlenmiş toobe gerekir:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

Merhaba klasörleri toomatch hello adlı **adı** karşılık gelen her öğenin öznitelikleri. Örneğin, hello hizmet bildirimi hello adlara sahip iki farklı kod paketi içerdiği **MyCodeA** ve **MyCodeB**, her kod için gerekli ikili dosyaları aynı adları içerecektir hello iki klasörlerle hello sonra Paket.

## <a name="use-setupentrypoint"></a>SetupEntryPoint kullanın
Kullanma için tipik senaryolar **SetupEntryPoint** toorun hello hizmet başlatılmadan önce yürütülebilir gerekir veya yükseltilmiş ayrıcalıklarla bir işlem tooperform ihtiyacınız olduğunda durumdadır. Örneğin:

* Ayarlama ve hizmet yürütülebilir gereksinimleri hello ortam değişkenleri başlatılıyor. Bu sınırlı tooonly yürütülebilir dosyalar hello Service Fabric programlama modeli yazılmış değil. Örneğin, bir node.js uygulamasını dağıtmak için yapılandırılmış bazı ortam değişkenleri npm.exe gerekir.
* Güvenlik sertifikaları yükleyerek erişim denetimini ayarlama.

Hakkında daha fazla bilgi için tooconfigure hello **SetupEntryPoint**, bkz: [hizmet Kurulum giriş noktası için hello ilkesi yapılandırma](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Yapılandırma
### <a name="build-a-package-by-using-visual-studio"></a>Visual Studio kullanarak bir paket oluşturun
Visual Studio 2015 toocreate uygulamanızı kullanıyorsanız hello paket komutu tooautomatically yukarıda açıklanan hello düzeni eşleşen bir paket oluştur kullanabilirsiniz.

toocreate bir paket, Çözüm Gezgini'nde hello uygulama projesine sağ tıklayın ve aşağıda gösterildiği gibi hello Paketi komutu seçin:

![Visual Studio ile bir uygulama paketleme][vs-package-command]

Paketleme tamamlandığında hello paketi hello konumu hello bulabilirsiniz **çıkış** penceresi. Visual Studio uygulamanızda hata ayıklama veya dağıttığınızda hello paketleme adım otomatik olarak gerçekleşir.

### <a name="build-a-package-by-command-line"></a>Komut satırı tarafından bir paket oluşturun
Ayrıca kullanarak uygulamanızı kurma olası tooprogrammatically paketi olan `msbuild.exe`. Merhaba çıktı aynı olacak şekilde hello başlık altında Visual Studio çalışıyor.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Sınama hello paketi
Hello kullanarak yerel olarak PowerShell aracılığıyla hello paket yapısı doğrulayabilirsiniz [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) komutu.
Bu komut için bildirimi ayrıştırma sorunları denetler ve tüm başvuruları doğrulayın. Bu komut, yalnızca hello dizinleri ve dosyaları hello paketindeki yapısal doğruluğunu hello doğrular.
Tüm gerekli dosyaların mevcut olduğunu denetleme ötesinde hello kod veya veri paket içeriğini hiçbirini doğrulamak değil.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Bu hello bu hatayı gösterir *MySetup.bat* hello hizmet bildiriminde başvurulan dosya **SetupEntryPoint** hello kod paketi eksik. Merhaba eksik dosya eklendikten sonra hello uygulama doğrulama geçirir:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Uygulamanız varsa, [uygulama parametreleri](service-fabric-manage-multiple-environment-app-configuration.md) tanımlanan, bunları geçirebilirsiniz [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) uygun doğrulama için.

Merhaba uygulaması dağıtılacağı hello küme biliyorsanız, hello geçirdiğiniz önerilir `ImageStoreConnectionString` parametresi. Bu durumda, hello paketi de hello kümede çalışmakta olan önceki sürümlerini Merhaba uygulaması doğrulanır. Örneğin, hello doğrulama bir paket olup olmadığını tespit edebilirsiniz hello ile aynı sürümü ancak farklı içerik zaten dağıtıldı.  

Merhaba uygulaması doğru paketlenir ve doğrulama başarılı sonra değerlendirme sıkıştırma gerekirse hello boyutu ve dosya hello sayısı göre.

## <a name="compress-a-package"></a>Bir paket Sıkıştır
Bir paket çok büyük veya çok sayıda dosya sahip olduğunda, daha hızlı dağıtımı için sıkıştırın. Sıkıştırma, dosyaları ve başlangıç paket boyutu hello sayısını azaltır.
Sıkıştırılmış uygulama paketi için [Uploading hello uygulama paketi](service-fabric-deploy-remove-applications.md#upload-the-application-package) (özel sıkıştırma zaman hesaba katıldığında varsa) artık karşılaştırılan toouploading hello sıkıştırılmamış paketi sürebilir ancak [kaydetme](service-fabric-deploy-remove-applications.md#register-the-application-package) ve [kayıt hello uygulama türü](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sıkıştırılmış uygulama paketi için daha hızlıdır.

Merhaba dağıtım için sıkıştırılmış ve sıkıştırılmamış paketleri aynı mekanizmadır. Hello paket sıkıştırılmışsa, bu nedenle hello küme görüntü deposunda depolanır ve hello uygulamayı çalıştırmadan önce hello düğümde sıkıştırılmamış.
Merhaba sıkıştırma hello geçerli Service Fabric paketi hello sıkıştırılmış sürümüyle değiştirir. Başlangıç klasörü yazma izni izin vermeniz gerekir. Sıkıştırma zaten sıkıştırılmış bir paketi çalıştıran herhangi bir değişiklik verir.

Merhaba Powershell komutunu çalıştırarak bir paket sıkıştırabilirsiniz [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) ile `CompressPackage` geçin. Merhaba sıkıştırmasını hello ile aynı paketini komutunu `UncompressPackage` geçin.

Merhaba aşağıdaki komutu hello paket toohello Image store kopyalamadan sıkıştırır. Kullanarak, gerektiği kadar bir sıkıştırılmış paket tooone veya daha fazla Service Fabric kümeleri kopyalayabilirsiniz [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello olmadan `SkipCopy` bayrağı.
Merhaba paket artık hello sıkıştırılmış dosyaları içerir `code`, `config`, ve `data` paketler. birçok dahili işlemleri (örneğin, paket paylaşımı, belirli doğrulamaları için uygulama türü adı ve sürümü ayıklama) için gerekli olduğu için hello uygulama bildirimi ve hello hizmeti bildirimleri, daraltılmış değil.
Sıkıştırma hello bildirimleri bu işlemleri verimli hale getirir.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Alternatif olarak, sıkıştırma ve kopyalama hello paketiyle [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) tek bir adımda.
Merhaba paket büyükse hello paket sıkıştırma ve hello karşıya yükleme toohello küme için yeterince zaman aşımı tooallow zaman sağlar.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Dahili olarak, Service Fabric sağlama toplamı doğrulaması için hello uygulama paketleri için hesaplar. Sıkıştırma kullanırken hello sağlama her paketi sürümleri daraltılmış hello üzerinde hesaplanır.
Sıkıştırılmamış bir uygulama paketinizi kopyalanır ve hello toouse sıkıştırma istiyorsanız aynı paketin hello hello sürümleri değiştirmelisiniz `code`, `config`, ve `data` paketleri tooavoid sağlama toplamı eşleşmezliği. Merhaba paketleri, hello sürümünü değiştirme yerine, değişmeden varsa, kullanabileceğiniz [fark sağlama](service-fabric-application-upgrade-advanced.md). Bu seçenek ile Merhaba değişmeden paket dahil etmeyin yerine hello hizmet bildirimden başvuru.

Benzer şekilde, hello paketin sıkıştırılmış bir sürümünü karşıya ve sıkıştırılmamış bir paket toouse istediğiniz hello sürümleri tooavoid hello sağlama toplamı eşleşmezliği güncelleştirmeniz gerekir.

Merhaba paket artık doğru paketlenmiş doğrulandı ve için hazır olması için (gerekirse), sıkıştırılmış [dağıtım](service-fabric-deploy-remove-applications.md) tooone ya da daha fazla Service Fabric kümeleri.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Visual Studio kullanarak dağıtırken paketleri Sıkıştır
Merhaba ekleyerek dağıtım, Visual Studio toocompress paketleri söyleyebilirsiniz `CopyPackageParameters` öğesi tooyour yayımlama profili ve ayarlama hello `CompressPackage` çok öznitelik`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Sonraki adımlar
[Dağıtma ve uygulamaları kaldırma] [ 10] açıklar nasıl toouse PowerShell toomanage uygulama örnekleri

[Birden çok ortamlar için uygulama parametreleri yönetme] [ 11] açıklar nasıl tooconfigure parametreleri ve farklı uygulama örnekleri için ortam değişkenleri.

[Uygulamanız için güvenlik ilkelerini yapılandırmak] [ 12] toorun güvenlik ilkeleri toorestrict erişim'in altında hizmetleri nasıl açıklar.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
