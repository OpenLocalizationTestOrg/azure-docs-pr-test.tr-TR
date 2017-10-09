---
title: "bir tek başına Azure Service Fabric kümesi aaaCreate | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi oluşturmayı herhangi bir makinede (fiziksel veya sanal) şirket içi olup olmadığını veya tüm bulut Windows Server'ı çalıştıran."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Windows Server çalıştıran tek başına kümesi oluşturma
Azure Service Fabric toocreate Service Fabric kümeleri tüm sanal makineler veya Windows Server çalıştıran bilgisayarlarda kullanabilirsiniz. Yani, dağıtmak ve Service Fabric uygulamaları birbirine bağlı bir Windows Server bilgisayarlar kümesi içeren herhangi bir ortamda çalıştırılabilir, şirket içinde veya herhangi bir bulut sağlayıcısına sahip olabilir. Service Fabric kümeleri kurulum paketi toocreate hello tek başına Windows Server paket adlı Service Fabric sağlar.

Bu makalede, tek başına Service Fabric kümesi oluşturma hello adım adım anlatılmaktadır.

> [!NOTE]
> Bu tek başına Windows Server paketi ticari olarak kullanılabilir ve üretim dağıtımları için kullanılabilir. Bu paket, "Önizleme"aşamasında olan yeni Service Fabric özellikler içerebilir. Çok aşağı kaydırarak"[Önizleme bu paketinde bulunan özellikler](#previewfeatures_anchor)." hello Önizleme özellikleri bölümüne hello listesi. Yapabilecekleriniz [hello EULA bir kopyasını indirin](http://go.microsoft.com/fwlink/?LinkID=733084) şimdi.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Merhaba Windows Server için Service Fabric paketi için destek alma
* Merhaba topluluğa hello Service Fabric tek başına paketi hakkında Windows Server için hello sor [Azure Service Fabric Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* İçin bilet [Service Fabric profesyonel desteği](http://support.microsoft.com/oas/default.aspx?prid=16146).  Microsoft Profesyonel desteği hakkında daha fazla bilgi [burada](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* Ayrıca destek bu paket için bir parçası olarak alabilirsiniz [Microsoft Premier Destek](https://support.microsoft.com/en-us/premier).
* Daha fazla ayrıntı için lütfen bkz. [Azure Service Fabric destek seçenekleri](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* Merhaba çalıştırma desteği amacıyla toocollect günlükleri [Service Fabric tek başına günlük Toplayıcı](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Merhaba Windows Server için Service Fabric paketi yükle
toocreate hello küme, kullanım hello Windows Server için Service Fabric paketi (Windows Server 2012 R2 ve daha yeni) burada bulundu: <br>
[Bağlantı - Service Fabric tek başına paketi - Windows Server'ı karşıdan yükle](http://go.microsoft.com/fwlink/?LinkId=730690)

Merhaba paket içeriğine ayrıntılarını bulun [burada](service-fabric-cluster-standalone-package-contents.md).

Merhaba Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir. Bir makineden dağıtma değil toohello bağlıysa Internet, lütfen bant dışı hello çalışma zamanı paketini buradan indirin: <br>
[Bağlantı - Service Fabric çalışma zamanı - Windows Server'ı karşıdan yükle](https://go.microsoft.com/fwlink/?linkid=839354)

Tek başına küme yapılandırma örnekleri adresindeki bulun: <br>
[Tek başına küme yapılandırma örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Merhaba kümesi oluşturma
Service Fabric, dağıtılan tooa bir makine geliştirme küme hello kullanarak olabilir *ClusterConfig.Unsecure.DevCluster.json* dahil dosya [örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Merhaba tek başına paket tooyour makine, kopyalama hello örnek yapılandırma dosyasını toohello yerel makine, ardından çalışma hello paketini açma *CreateServiceFabricCluster.ps1* hello tek başına bir yönetici PowerShell oturumundan aracılığıyla Paket klasörü:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Adım 1A: Güvenli olmayan yerel geliştirme kümesi oluşturun
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Bkz: Merhaba ortam Kurulumu kısmına [planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md) ayrıntıları sorun giderme.

Çalışan geliştirme senaryolarını tamamladığınızda, hello Service Fabric kümesi hello makineden bölümünde toosteps bakarak kaldırabilirsiniz "[bir kümesini kaldırmak](#removecluster_anchor)". 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Adım 1B: çoklu makine bir küme oluşturun
Merhaba planlama aracılığıyla ilerlemiş sonra aşağıdaki bağlantıdaki, hello adresindeki hazırlık adımları ayrıntılı olursunuz toocreate küme yapılandırma dosyanızı kullanarak, üretim kümeniz hazır. <br>
[Planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md)

1. Merhaba çalıştırarak yazdığınız hello yapılandırma dosyasını doğrulamak *TestConfiguration.ps1* hello tek başına paket klasörüne betikten:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Bir çıktı görmeniz gerekir aşağıdaki gibi. Merhaba altındaki alanda "Başarılı" "True" olarak döndürülürse, sağlamlık denetimleri geçtikten ve hello küme toobe dağıtılabilir hello giriş yapılandırmasına bağlı olarak görünür.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Merhaba küme oluşturma: hello çalıştırmak *CreateServiceFabricCluster.ps1* betik toodeploy hello Service Fabric kümesi hello yapılandırmasındaki her makine arasında. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Dağıtım izlemeleri toohello VM/makine hello CreateServiceFabricCluster.ps1 PowerShell Betiği çalıştırdığınız yazılır. Bunlar hangi hello komut dosyasını çalıştırmak hello dizininde dayalı hello alt DeploymentTraces, bulunabilir. Service Fabric olduysa toosee tooa makine doğru şekilde dağıtıldığını, yüklü hello dosyaları (göre varsayılan c:\ProgramData\SF) hello küme yapılandırma dosyasındaki FabricSettings bölümünde ayrıntılı olarak hello FabricDataRoot dizininde bulabilir. De FabricHost.exe ve Fabric.exe işlemleri Görev Yöneticisi'nde çalışan görülebilir.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Adım 1C: Çevrimdışı (internet kesilmiş) küme oluşturma
Merhaba Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir. Ne zaman bir küme toomachines dağıtma değil izin ver bağlı toohello Internet toodownload hello Service Fabric çalışma zamanı ayrı olarak paketini ve küme oluşturma sırasında hello yolu tooit sağlamak gerekir.
Merhaba çalışma zamanı paketi ayrı olarak yüklenebilen, başka bir makineden toohello bağlı Internet adresindeki [karşıdan yükleme bağlantısı - Service Fabric çalışma zamanı - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Merhaba çevrimdışı kümeden dağıtma ve çalıştırarak hello küme oluşturma hello çalışma zamanı paketi toowhere kopyalama `CreateServiceFabricCluster.ps1` hello ile `-FabricRuntimePackagePath` dahil, aşağıda gösterildiği gibi parametre: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
Burada `.\ClusterConfig.json` ve `.\MicrosoftAzureServiceFabric.cab` hello yolları toohello küme yapılandırmasını ve hello çalışma zamanı .cab dosyası sırasıyla şunlardır.


### <a name="step-2-connect-toohello-cluster"></a>2. adım: toohello kümesine bağlanın
tooconnect tooa güvenli küme, bkz: [Service fabric bağlanmak toosecure küme](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan güvenli olmayan küme, hello aşağıdaki PowerShell komutunu çalıştırın:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Örnek:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>3. adım: Service Fabric Explorer Getir
Service Fabric Explorer ya da doğrudan hello makineler http://localhost:19080/Explorer/index.html veya uzaktan http://< biri ile toohello küme bağlanabilir artık*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Ekleme ve düğümlerini Kaldır
Ekleme veya düğümleri tooyour tek başına Service Fabric kümesi, iş gereksinimleriniz değiştikçe kaldırın. Bkz: [ekleme veya kaldırma düğümleri tooa Service Fabric tek başına küme](service-fabric-cluster-windows-server-add-remove-nodes.md) ayrıntılı adımlar için.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Bir küme Kaldır
Merhaba çalıştırmak tooremove bir küme *RemoveServiceFabricCluster.ps1* PowerShell Betiği hello paket klasörüne ve hello yol toohello JSON yapılandırma dosyası geçirin. İsteğe bağlı olarak hello silme hello günlük için bir konum belirtebilirsiniz.

Bu komut dosyası düğümleriyle hello küme yapılandırma dosyasında listelenen yönetici erişimi tooall hello makinelerin bulunduğu herhangi bir makinede çalıştırılabilir. Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Toplanan telemetri verileri nasıl ve ne tooopt onu dışında
Varsayılan olarak, hello ürün telemetri hello Service Fabric kullanım tooimprove hello üründe toplar. Merhaba hello kurulumunun bir parçası için bağlantı çok denetler olarak çalıştırılan en iyi yöntem Çözümleyicisi[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Erişilebilir durumda değilse, telemetri dışında tercih sürece hello kurulum başarısız olur.

1. Merhaba telemetri ardışık düzen çalıştığında veri çok aşağıdaki tooupload hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) günde bir kez. En yüksek çaba karşıya yükleme ve hello küme işlevselliğini üzerinde hiçbir etkisi olmaz. Merhaba telemetri çalıştığı Yük Devretme Yöneticisi birincil hello hello düğümden yalnızca gönderilir. Başka bir düğüm telemetri gönderir.
2. Merhaba telemetri hello şunlardan oluşur:

* Hizmetlerin sayısı
* ServiceTypes sayısı
* Uygulama sayısı
* ApplicationUpgrades sayısı
* Sistemdeki yük devretme birimi sayısı
* Inbuildfailoverunits sayısı
* UnhealthyFailoverUnits sayısı
* Çoğaltmaların sayısı
* InBuildReplicas sayısı
* StandByReplicas sayısı
* OfflineReplicas sayısı
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Düğüm sayısı
* IsContextComplete: True/False
* ClusterId: Her küme için rastgele oluşturulmuş bir GUID budur
* ServiceFabricVersion
* Merhaba sanal makine ya da hangi hello telemetri karşıya Makine IP adresi

toodisable telemetri çok hello ekleyin*özellikleri* yapılandırmada, küme: *enableTelemetry: yanlış*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Bu pakete dahil önizleme özellikleri
yok.


> [!NOTE]
> Merhaba ile yeni başlangıç [hello tek başına küme Windows Server için GA sürümü (sürüm 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), küme toofuture sürümler, el ile veya otomatik olarak yükseltme yapabilirsiniz. Çok başvuran[bir tek başına Service Fabric kümesi sürümüne yükseltmenizi](service-fabric-cluster-upgrade-windows-server.md) Ayrıntılar için belge.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Dağıtma ve PowerShell kullanarak uygulamaları kaldırma](service-fabric-deploy-remove-applications.md)
* [Tek başına Windows kümesi için yapılandırma ayarları](service-fabric-cluster-manifest.md)
* [Ekleme veya düğümleri tooa tek başına Service Fabric kümesi kaldırma](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Bir tek başına Service Fabric kümesi sürümüne yükseltme](service-fabric-cluster-upgrade-windows-server.md)
* [Azure VM'ler Windows çalıştıran bir tek başına Service Fabric kümesi oluştur](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-windows-security.md)
* [Tek başına küme X509 kullanarak Windows güvenli sertifikaları](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
