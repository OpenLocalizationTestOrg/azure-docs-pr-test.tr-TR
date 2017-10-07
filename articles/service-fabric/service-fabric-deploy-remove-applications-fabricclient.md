---
title: "aaaAzure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "Merhaba FabricClient API'leri toodeploy kullanın ve Service Fabric uygulamaları kaldırın."
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
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Dağıtma ve FabricClient kullanarak uygulamaları kaldırma
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
Toohello küme oluşturarak bağlanabilecek bir [FabricClient](/dotnet/api/system.fabric.fabricclient) , herhangi bir hello bu makaledeki kod örnekleri çalıştırmadan önce örneği. Bağlantı tooa yerel geliştirme küme veya uzaktan küme veya küme Azure Active Directory, X509 kullanılarak güvenli örnekleri için sertifikalar veya Windows Active Directory bkz [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). Merhaba aşağıdaki komutu çalıştırarak tooconnect toohello yerel geliştirme kümesi:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Merhaba uygulama paketini karşıya yükleyin
Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio. Varsayılan olarak, "MyApplicationType" Merhaba ApplicationManifest.xml listelenen hello uygulama türü adı bağlıdır.  Merhaba hello gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\&lt; kullanıcı adı&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.

Karşıya yükleme hello uygulama paketi hello iç Service Fabric bileşenleri tarafından erişilebilen bir konumda koyar. Service Fabric hello uygulama paketi hello uygulama paketi hello kayıt sırasında doğrular. (Yani, yüklemeden önce) tooverify hello uygulama paketi yerel olarak istiyorsanız, ancak hello kullanın [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.

Merhaba [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API hello uygulama paketi toohello küme görüntü deposuna karşıya yükler. 

Merhaba uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package) ve PowerShell kullanarak toohello Image store kopyalayın. Merhaba sıkıştırma hello boyutunu ve dosya hello sayısını azaltır.

Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.

## <a name="register-hello-application-package"></a>YAZMAÇ hello uygulama paketi
Merhaba uygulama türü ve sürümü hello uygulama paketi kaydedildikten sonra kullanılabilir hale hello uygulama bildiriminde bildirildi. Merhaba sistem hello önceki adımda karşıya yüklenen hello paket okur hello paket doğrular, hello paket içeriğini işler ve işlenen hello paket tooan iç sistem konumuna kopyalar.  

Merhaba [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API yazmaçlar hello hello kümedeki uygulama türü ve dağıtım için kullanılabilir hale getirmek.

Merhaba [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API tüm başarıyla kayıtlı uygulama türleri hakkında bilgi sağlar. Merhaba kaydı yapıldığında bu API toodetermine kullanabilirsiniz.

## <a name="create-an-application-instance"></a>Uygulama örneğini oluşturma
Hello kullanarak başarıyla kaydettirildi herhangi bir uygulama türü'ten bir uygulamanın örneği [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. her uygulamanın Hello adı hello ile başlamalı *"fabric:"* düzen ve her uygulama örneği (küme içinde) benzersiz olmalıdır. Hello uygulama bildiriminde hello hedef uygulama türünün tanımlı hiçbir varsayılan hizmetleri de oluşturulur.

Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir. Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlemleri kümesi ile çalışır.

uygulamalar ve hizmetler olarak adlandırılan toosee hello çalıştırmak hello kümede çalışan [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) ve [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API'leri.

## <a name="create-a-service-instance"></a>Bir hizmet örneği oluşturma
Hello kullanarak bir hizmet türünün alanından bir hizmet örneği [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Merhaba hizmeti varsayılan hizmet hello uygulama bildiriminde olarak bildirilirse hello uygulama örneği oluşturulduğunda hello hizmet örneği.  Arama hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API zaten örneği bir hizmet için bir hata kodu FabricErrorCode.ServiceAlreadyExists değerini içeren FabricException türünde bir özel durum döndürür.

## <a name="remove-a-service-instance"></a>Bir hizmet örneği Kaldır
Bir hizmet örneği artık gerekli olmadığında, bu uygulama örneği tarafından arama hello çalıştıran hello kaldırabilirsiniz [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Bu işlem geri alınamaz ve hizmet durumu kurtarılamıyor.

## <a name="remove-an-application-instance"></a>Bir uygulama örneğini kaldırma
Uygulama örneğini artık gerekli olmadığında kalıcı olarak hello kullanarak adıyla kaldırabilirsiniz [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) tüm hizmet durumunu da, kalıcı olarak kaldırma toohello uygulama ait tüm hizmetleri otomatik olarak kaldırır.

> [!WARNING]
> Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.

## <a name="unregister-an-application-type"></a>Bir uygulama türü kaydını kaldırma
Belirli bir uygulama türü sürümü artık gerekli olmadığında bu belirli sürümü hello kullanarak hello uygulama türü kaydını [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Uygulama türü sürümleri depolama alanı hello Image store tarafından kullanılan kaydı siliniyor kullanılmayan sürümleri. Uygulama türü sürümü, uygulama bu hello uygulama türü sürümü karşı örneği ve hiçbir bekleyen uygulama yükseltmesi hello uygulama türü sürümünün başvurduğunuzdan sürece kaydı olabilir.

## <a name="remove-an-application-package-from-hello-image-store"></a>Bir uygulama paketi hello görüntü deposundan kaldırır
Bir uygulama paketi artık gerekli olmadığında hello görüntü deposu toofree hello kullanarak sistem kaynaklarının gelen silebilmek [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

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
Sorun: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API zaman aşımına uğruyor büyük uygulama paketi (GB sırasını).
Deneyin:
- Daha büyük zaman aşımını belirtmek [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) yöntemi ile `timeout` parametresi. Varsayılan olarak, hello zaman aşımı 30 dakikadır.
- Kaynak makine ve küme arasındaki Hello ağ bağlantısını denetleyin. Merhaba bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.
Merhaba istemci makine hello küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede hello küme olarak düşünün.
- Dış azaltma devreyi olmadığını denetleyin. Örneğin, Hello Image store yapılandırılmış toouse azure depolama olduğunda, karşıya yükleme kısıtlanan.

Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API zaman aşımına uğradı. Deneyin:
- [Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.
Hello sıkıştırma hello boyutunu azaltır ve hangi sırayla hello trafik miktarını azaltır ve bu Service Fabric çalışma hello dosya sayısı, gerçekleştirmeniz gerekir. Merhaba karşıya yükleme işlemi (özellikle hello sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak daha hızlı kaydedin ve kaydı hello uygulama türü.
- Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API'si ile `timeout` parametresi.

### <a name="deploy-application-package-with-many-files"></a>Birçok dosyalarıyla uygulama paketini dağıtma
Sorun: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).
Deneyin:
- [Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce. Merhaba sıkıştırma dosyaları hello sayısını azaltır.
- Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) ile `timeout` parametresi.

## <a name="code-example"></a>Kod örneği
Merhaba aşağıdaki örnek bir uygulama paketi toohello görüntü deposu kopyalar, hazırlar hello uygulama türü, uygulama örneğini oluşturur, hello uygulama türü, bir hizmet örneği, kaldırır hello Uygulama örneğinin kaydını hükümleri oluşturur ve Merhaba uygulama paketi hello görüntü deposundan kaldırır.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)

[Service Fabric sistem durumu giriş](service-fabric-health-introduction.md)

[Tanılama ve bir Service Fabric hizmeti sorun giderme](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulamada modeli](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
