---
title: "tek başına Azure Service Fabric kümesi Windows Server'da aaaUpgrade | Microsoft Docs"
description: "Hello Azure Service Fabric kod ve/veya hello küme güncelleştirme modu ayarı dahil olmak üzere bir tek başına Service Fabric kümesi çalıştıran yapılandırma yükseltin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Windows Server kümesi, tek başına Azure Service Fabric yükseltme
> [!div class="op_single_selector"]
> * [Azure küme](service-fabric-cluster-upgrade.md)
> * [Tek başına küme](service-fabric-cluster-upgrade-windows-server.md)
>
>

Tüm modern, hello özelliği tooupgrade anahtar toohello uzun vadeli başarı ürününüzün sistemidir. Azure Service Fabric kümesi sahip olduğunuz bir kaynaktır. Bu makalede, bu hello küme Service Fabric kod ve yapılandırmaları desteklenen sürümleri her zaman çalışır nasıl emin olabileceğiniz açıklanır.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Kümenizde çalışan denetim hello Service Fabric sürüm
Küme toodownload güncelleştirmeleri tooset hizmet Microsoft kümesi hello yeni bir sürümü yayımlandığında dokusu **fabricClusterAutoupgradeEnabled** yapılandırma tootrue küme. tooselect, küme toobe üzerinde kümesi hello istediğiniz desteklenen bir sürümünü Service Fabric **fabricClusterAutoupgradeEnabled** yapılandırma toofalse küme.

> [!NOTE]
> Kümenizi desteklenen bir Service Fabric sürümü her zaman çalıştığından emin olun. Service Fabric yeni bir sürümünü hello sürüm Microsoft sunar, hello önceki sürümü en az 60 gün hello duyuru başlangıç tarihinden sonra destek sona ermesi için işaretlenir. Yeni sürümler duyurdu [hello Service Fabric ekip blogunda](https://blogs.msdn.microsoft.com/azureservicefabric/). Merhaba yeni kullanılabilir toochoose bu noktada sürümüdür.
>
>

Her Service Fabric düğümü ayrı fiziksel veya sanal makine üzerinde nerede ayrılmış bir üretim stili düğüm yapılandırması yalnızca kullanıyorsanız, küme toohello yeni sürüm yükseltme yapabilirsiniz. Birden fazla Service Fabric düğümü tek bir fiziksel veya sanal makine üzerinde olduğu bir geliştirme kümeniz varsa hello yeni sürümü hello kümeye yeniden oluşturmanız gerekir.

İki ayrı iş akışları, küme toohello en son sürümünü veya desteklenen bir Service Fabric sürüme yükseltebilirsiniz. Bir iş akışı bağlantı toodownload hello en son sürüme otomatik olarak sahip kümeler için kullanılıyor. Merhaba diğer bağlantı toodownload hello son Service Fabric sürümü olmayan kümeler için iş akışıdır.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Bağlantı toodownload hello en son kod ve yapılandırma kümeleri yükseltme
Küme düğümlerinizi çok Internet bağlantınız varsa bu adımları tooupgrade küme desteklenen tooa sürümünüzü kullanın[http://download.microsoft.com](http://download.microsoft.com).

Çok bağlantınız kümeleri için[http://download.microsoft.com](http://download.microsoft.com), Microsoft düzenli olarak yeni Service Fabric sürümler için hello kullanılabilirliğini denetler.

Yeni bir Service Fabric sürümü kullanılabilir olduğunda, hello paket toohello küme yerel olarak yüklenir ve yükseltme için sağlanmış. Ayrıca, tooinform hello müşteri bu yeni sürümün hello sistem aşağıdaki benzer toohello olan bir açık küme sistem durumu uyarısı gösterir:

"hello geçerli küme sürümü [version #] desteği [Date] sonlandırır."

Merhaba küme hello en son sürümünü çalıştırdıktan sonra hello uyarı kaybolduktan.

#### <a name="cluster-upgrade-workflow"></a>Küme yükseltme iş akışı
Merhaba küme sistem durumu uyarısı gördükten sonra aşağıdaki hello:

1. Merhaba kümedeki düğümler olarak listelenen yönetici erişimi tooall hello makineleri herhangi makineden toohello kümesine bağlanın. Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Merhaba yükseltmeden Service Fabric sürümlerinin listesini alın.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Bir çıkış benzer toothis almanız gerekir:

    ![Doku sürümlerini alma][getfabversions]
3. Küme yükseltme tooan kullanılabilir sürüm başlamayı [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor hello ilerleme hello yükseltme durumunu Service Fabric Explorer veya Windows PowerShell komutunu aşağıdaki çalışma hello kullanabilirsiniz.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. toospecify özel sistem durumu ilkeleri hello için **başlangıç ServiceFabricClusterUpgrade** komutu, belgelerine bakın [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Hello geri alma sonuçlandı hello sorunları giderdikten sonra aynı adımları daha önce açıklandığı gibi aşağıdaki hello tarafından hello yükseltmeyi yeniden başlatın.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Sahip kümeler yükseltme <U>hiç bağlantı</u> toodownload hello en son kod ve yapılandırma
Küme düğümlerinizi Internet bağlantısı çok yoksa bu adımları tooupgrade küme desteklenen tooa sürümünüzü kullanmak[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Bağlı toohello Internet olmayan bir küme çalıştırıyorsanız, yeni bir sürümü hakkında toomonitor hello Service Fabric ekip blogu toolearn sahip olur. Merhaba sistem küme sistem durumu uyarı tooalert gösterme, yeni bir sürüm.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Otomatik sağlama vs el ile sağlama
tooenable otomatik karşıdan yükleme ve kayıt hello en son kod sürümü için Service Fabric güncelleştirme hizmeti ayarlayın. Toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt hello içinde başvurmak [tek başına paket](service-fabric-cluster-standalone-package-contents.md) yönergeler için.
El ile işlem için aşağıdaki hello yönergeleri izleyin.

Özellik toofalse yapılandırma yükseltmeye başlamadan önce aşağıdaki, küme yapılandırma tooset hello değiştirin.

        "fabricClusterAutoupgradeEnabled": false,

Çok başvuran[başlangıç ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) kullanım ayrıntıları için. Merhaba yapılandırma yükseltmeye başlamadan önce JSON emin tooupdate 'clusterConfigurationVersion' olun.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Küme yükseltme iş akışı

1. Get-ServiceFabricClusterUpgrade hello kümedeki hello düğümlerinden biri çalıştırın ve hello TargetCodeVersion dikkat edin.
2. Internet bağlantılı makine toolist çalışma hello aşağıdakini tüm hello geçerli sürümüyle uyumlu sürümlerini yükseltin ve hello ilişkili indirme bağlantıları paketinden karşılık gelen hello indirin.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Merhaba kümedeki düğümler olarak listelenen yönetici erişimi tooall hello makineleri herhangi makineden toohello kümesine bağlanın. Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Merhaba indirilen paketi hello küme görüntü deposuna kopyalayın.

5. Kopyalanan hello paketi kaydedin.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Küme yükseltme tooan kullanılabilir sürüm başlatın.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz veya hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır. toospecify özel sistem durumu ilkeleri hello için **başlangıç ServiceFabricClusterUpgrade** komutu, hello belgelerine bakın [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Hello geri alma sonuçlandı hello sorunları giderdikten sonra aynı adımları daha önce açıklandığı gibi aşağıdaki hello tarafından hello yükseltmeyi yeniden başlatın.


## <a name="upgrade-hello-cluster-configuration"></a>Yükseltme hello küme yapılandırması
Merhaba yapılandırma Yükseltmeyi başlatmadan önce hello tek başına paketinde hello powershell betiğini çalıştırarak, yeni küme yapılandırma json test edebilirsiniz.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
or

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Bazı yapılandırmalar olamaz, uç noktaları gibi küme adı, düğüm IP yükseltilmiş vb.. Merhaba yeni küme yapılandırma json hello eskisinin karşı test ve herhangi bir sorun varsa hello Powershell penceresinde hataları atar.

tooupgrade hello küme yapılandırması yükseltmesi çalıştırmak **başlangıç ServiceFabricClusterConfigurationUpgrade**. Merhaba yapılandırma yükseltme yükseltme etki alanı tarafından işlenen yükseltme etki alanıdır.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Küme sertifikası config yükseltme  
Küme sertifikası küme düğümleri arasında kimlik doğrulaması için kullanılan, hata küme düğümleri arasında hello iletişimi engeller çünkü hello sertifika geçir şekilde ek dikkatli gerçekleştirilmelidir.  
Teknik olarak, üç seçenekleri desteklenir:  

1. Tek sertifika yükseltme: hello yükseltme yolu ' (birincil) -> sertifika B (birincil) sertifika, sertifika C (birincil) -> ->...'.   
2. Double sertifika yükseltme: hello yükseltme yolu ' (birincil) -> sertifika sertifika (birincil) ve B (ikincil) sertifika B (birincil) -> -> (birincil) sertifika B ve C (ikincil) sertifika C (birincil) -> ->...'.
3. Sertifika türü yükseltme: sertifika parmak izi tabanlı yapılandırma <> – CommonName tabanlı sertifika yapılandırması. Örneğin, sertifika parmak izi (birincil) ve parmak izi B (ikincil) sertifika CommonName c ->


## <a name="next-steps"></a>Sonraki adımlar
* Bilgi nasıl toocustomize bazı [Service Fabric kümesi ayarlarını](service-fabric-cluster-fabric-settings.md).
* Nasıl çok öğrenin[kümenizi ölçeğini](service-fabric-cluster-scale-up-down.md).
* Hakkında bilgi edinin [uygulama yükseltmelerini](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
