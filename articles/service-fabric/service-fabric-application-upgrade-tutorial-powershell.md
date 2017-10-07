---
title: "PowerShell kullanarak aaaService Fabric uygulama yükseltme | Microsoft Docs"
description: "Bu makalede bir Service Fabric uygulaması dağıtma, hello kodunu değiştirme ve PowerShell kullanarak yükseltme çalışırken hello deneyimi anlatılmaktadır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>PowerShell kullanarak Service Fabric uygulama yükseltme
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Merhaba en sık kullanılan ve önerilen yükseltme izlenen hello yükseltme yaklaşımdır.  Azure Service Fabric sistem durumu ilkeleri kümesine göre hello hello uygulama yükseltiliyor izler. Bir güncelleştirme etki alanı (UD) yükseltildikten sonra Service Fabric hello uygulama durumunu değerlendirir ve toohello sonraki güncelleştirme etki alanı devam eder veya hello sistem durumu ilkeleri bağlı olarak hello yükseltme başarısız olur.

İzlenen uygulama yükseltme yönetilen hello veya yerel API'leri kullanılarak gerçekleştirilebilir PowerShell veya REST. Visual Studio kullanarak bir yükseltme gerçekleştirme hakkında yönergeler için bkz: [Visual Studio kullanarak uygulamanızı yükseltme](service-fabric-application-upgrade-tutorial.md).

Service Fabric izlenen kesinti olmadan yükseltme ile Merhaba Uygulama Yöneticisi hello uygulama sağlıklı ise Service Fabric toodetermine kullandığını hello sistem durumu değerlendirme ilkesi yapılandırabilirsiniz. Hello Yöneticisi (Otomatik geri alma işleminden örneğin.) hello sistem durumu değerlendirmesi başarısız olduğunda gerçekleştirilecek hello eylem toobe ek olarak, yapılandırabilirsiniz Bu bölümde bir PowerShell kullanan hello SDK örnekleri için izlenen bir yükseltme anlatılmaktadır. Merhaba aşağıdaki Microsoft Virtual Academy video Ayrıca, uygulama yükseltmesi açıklanmaktadır:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>1. adım: Derleme ve hello görsel nesneler örnek dağıtma
Derleme ve hello uygulama yayımlama hello uygulama projesine sağ tıklayarak **VisualObjectsApplication,** ve hello seçerek **Yayımla** komutu.  Daha fazla bilgi için bkz: [Service Fabric uygulaması yükseltme Öğreticisi](service-fabric-application-upgrade-tutorial.md).  Alternatif olarak, uygulamanızın PowerShell toodeploy kullanabilirsiniz.

> [!NOTE]
> Merhaba Service Fabric komutlardan herhangi birini PowerShell'de kullanılabilir önce ilk tooconnect toohello küme hello kullanarak ihtiyacınız `Connect-ServiceFabricCluster` cmdlet'i. Benzer şekilde, küme yerel makinenizde zaten ayarlanmış bu hello kabul edilir. Merhaba makale bakın [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started.md).
> 
> 

Visual Studio'da Hello projesi oluşturduktan sonra hello PowerShell komutunu kullanabilirsiniz [kopya ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello uygulama paketi toohello görüntü. Tooverify hello uygulama paketi yerel olarak istiyorsanız hello kullanın [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet'i. Merhaba sonraki tooregister hello uygulama toohello Service Fabric hello kullanarak çalışma zamanı adımdır [Register-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet'i. Merhaba son toostart hello uygulama örneğini hello kullanarak adımdır [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet'i.  Bu üç adımı benzer toousing hello olan **dağıtma** Visual Studio menü öğesi.

Şimdi, kullanabileceğiniz [Service Fabric Explorer, tooview Merhaba küme ve hello uygulaması](service-fabric-visualizing-your-cluster.md). Merhaba uygulama gittiğinizde tooin Internet Explorer yazarak olabilecek bir web hizmeti etkinleştirilmiş [http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) hello adres çubuğundaki.  Merhaba ekranında dolaşma bazı kayan görsel nesneler görmeniz gerekir.  Ayrıca, kullanabileceğiniz [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck hello uygulama durumu.

## <a name="step-2-update-hello-visual-objects-sample"></a>2. adım: Güncelleştirme hello görsel nesneler örnek
Adım 1'de dağıtılan hello sürümüyle hello visual nesneleri değil döndürme fark edebilirsiniz. Şimdi burada hello görsel nesneler de döndürme bu uygulama tooone yükseltin.

Merhaba VisualObjects.ActorService projesi hello VisualObjects çözüm içinde seçin ve hello StatefulVisualObjectActor.cs dosyasını açın. Bu dosyanın içindeki toohello yöntemi gidin `MoveObject`, çıkışı açıklama `this.State.Move()`ve açıklama durumundan çıkarmanız `this.State.Move(true)`. Merhaba hizmet yükseltildikten sonra bu değişiklik hello nesnesini döndürür.

Ayrıca tooupdate hello ihtiyacımız *ServiceManifest.xml* hello proje dosyası (altında PackageRoot) **VisualObjects.ActorService**. Güncelleştirme hello *CodePackage* hizmeti sürüm too2.0 hello ve karşılık gelen satırda hello hello *ServiceManifest.xml* dosya.
Visual Studio hello kullanabilirsiniz *bildirim dosyaları düzenleme* hello çözüm toomake hello bildirim dosyası değişiklikleri sağ sonra seçeneği.

Merhaba değişiklikler yapıldıktan sonra hello bildirimi hello aşağıdaki gibi görünmelidir (vurgulanan bölümleri göster hello değişiklikleri):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Şimdi hello *ApplicationManifest.xml* dosyası (Merhaba altında bulunan **VisualObjects** projesi hello altında **VisualObjects** çözüm) güncelleştirilmiş tooversion 2.0 hello olduğu **VisualObjects.ActorService** projesi. Ayrıca, hello uygulama 1.0.0.0 gelen güncelleştirilmiş too2.0.0.0 sürümüdür. Merhaba *ApplicationManifest.xml* hello görünümlü aşağıdaki kod parçacığında:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Şimdi, yalnızca hello seçerek Merhaba Projeyi derlemek **ActorService** proje ve ardından sağ tıklayıp hello seçerek **yapı** Visual Studio'daki seçeneği. Seçerseniz **tüm yeniden**, nedeniyle hello kod değişmiş hello sürümleri tüm projeleri için güncelleştirmeniz gerekir. Daha sonra şirketinizdeki üzerinde sağ tıklayarak paketi hello uygulama güncelleştirilmiş ***VisualObjectsApplication***, hello Service Fabric menü seçilerek ve **paket**. Bu eylem, dağıtılabilir bir uygulama paketi oluşturur.  Dağıtılan hazır toobe, güncelleştirilmiş uygulamasıdır.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>3. adım: sistem durumu ilkeleri karar verin ve yükseltme parametreleri
Merhaba ile öğrenmeniz [uygulama yükseltme parametreleri](service-fabric-application-upgrade-parameters.md) ve hello [yükseltme işlemi](service-fabric-application-upgrade.md) tooget çeşitli yükseltme parametreleri, zaman aşımları ve sistem durumu ölçüt uygulanan hello iyi anlamış . Bu kılavuzda hello hizmet sistem durumu değerlendirme ölçütü ayarlamak toohello varsayılan (ve önerilen) tüm hizmetleri ve örnekleri gerektiği anlamına gelir değerleri *sağlıklı* hello yükselttikten sonra.  

Ancak, şimdi hello artırmanız *HealthCheckStableDuration* too60 saniye (toohello hello yükseltme devam etmeden önce en az 20 saniye sonra etki alanını güncelleştirmek için hello Hizmetleri sağlıklı; böylece).  Şimdi de hello ayarlayın *UpgradeDomainTimeout* toobe 1200 saniye ve hello *UpgradeTimeout* toobe 3000 saniye.

Son olarak, şimdi de hello ayarlayın *UpgradeFailureAction* toorollback. Merhaba yükseltme sırasında herhangi bir sorunla karşılaşırsa, bu seçenek Service Fabric tooroll geri hello uygulama toohello önceki sürümünü gerektirir. Bu nedenle, hello yükseltmesinde (4. adım) başlatma sırasında hello aşağıdaki parametreler belirtildi:

FailureAction geri alma =

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec 1200 =

UpgradeTimeout 3000 =

## <a name="step-4-prepare-application-for-upgrade"></a>4. adım: Uygulama yükseltme için hazırlama
Merhaba uygulaması şimdi oluşturulur ve hazır toobe yükseltildi. Bir yöneticiyseniz ve türü bir PowerShell penceresi açarsanız [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), uygulama türü 1.0.0.0 olduğunu size bildirmek **VisualObjects** dağıtılan.  

Merhaba uygulama paketi hello aşağıdaki altında depolanan sıkıştırılmamış burada hello Service Fabric SDK - göreli yol *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. Hello uygulama paketinin depolandığı bu dizinde bir "Paketi" klasörü bulmanız gerekir. Merhaba zaman damgaları tooensure hello son sürüme (toomodify hello yollar uygun şekilde de gerekebilir) olduğunu denetleyin.

Şimdi uygulama paketi toohello Service Fabric (Merhaba uygulama paketlerini Service Fabric tarafından depolandığı) görüntü kopyası hello güncelleştirilmiş artık. parametre hello *ApplicationPackagePathInImageStore* Service Fabric burada da bulabilir hello uygulama paketi bildirir. Biz güncelleştirilmiş Merhaba uygulaması yerleştirdiğiniz "VisualObjects\_V2" Merhaba (ihtiyacınız olabilecek toomodify yollar uygun şekilde yeniden) komutu aşağıdaki ile.

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

Merhaba sonraki adıma tooregister hello kullanılarak gerçekleştirilebilir Service Fabric bu uygulamayla olan [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) komutu:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Merhaba yukarıdaki komut başarılı değil, tüm hizmetleri yeniden gereksinim olasıdır. Adım 2'de belirtildiği gibi Web hizmeti sürümü de tooupdate olabilir.

## <a name="step-5-start-hello-application-upgrade"></a>5. adım: Başlangıç hello uygulama yükseltme
Şimdi, tüm kümesi toostart hello uygulama dileriz hello kullanarak yükseltme [başlangıç ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) komutu:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Merhaba uygulama adı olduğu hello aynı hello açıklanan *ApplicationManifest.xml* dosya. Service Fabric hangi uygulamanın yükseltilir bu adı tooidentify kullanır. Merhaba zaman aşımlarını toobe çok kısa ayarlarsanız, durumları sorun hello bir hata iletisi karşılaşabilirsiniz. Toohello sorun giderme bölümüne bakın veya hello zaman aşımlarını artırın.

Şimdi, uygulama yükseltme devam eder hello gibi Service Fabric Explorer kullanarak izleyebileceğiniz veya hello kullanarak [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell komutunu: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

PowerShell komutu, önceki hello kullanarak aldığınız hello durumu birkaç dakika içinde durum tüm güncelleştirme etki alanları yükseltilen (tamamlandı). Ve tarayıcı penceresinde hello görsel nesneleri döndürme başlatılmış olduğunu bulmanız gerekir!

Sürüm 2 tooversion 3 veya sürüm 2 tooversion 1 bir alıştırma olarak yükseltme deneyebilirsiniz. Sürüm 2 tooversion 1 ' taşıma yükseltme kabul edilir. Zaman aşımları ve sistem durumu ilkeleri toomake kendiniz bunları aşina yürütün. Tooan Azure küme dağıtırken hello parametreleri gerek toobe kümesi uygun şekilde. İyi tooset hello zaman aşımlarını ölçülü olur.

## <a name="next-steps"></a>Sonraki adımlar
[Visual Studio kullanarak uygulamanızı yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[konuları Gelişmiş](service-fabric-application-upgrade-advanced.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [uygulama yükseltme sorunlarını giderme](service-fabric-application-upgrade-troubleshooting.md).

