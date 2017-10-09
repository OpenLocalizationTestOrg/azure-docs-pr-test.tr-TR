---
title: "tek başına Azure Service Fabric kümesi aaaSet | Microsoft Docs"
description: "Merhaba üzerinde çalışan üç düğümü ile geliştirme tek başına küme oluşturma aynı bilgisayar. Bu kurulumu tamamladıktan sonra hazır toocreate çoklu makine bir küme olacaktır."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>İlk tek başına Service Fabric kümenizi oluşturma
Herhangi bir sanal makineler veya Windows Server 2012 R2 veya Windows Server 2016, şirket içi çalıştıran bilgisayarlar üzerinde veya hello bulutta bir Service Fabric tek başına kümesi oluşturabilirsiniz. Bu hızlı başlangıç toocreate geliştirme tek başına küme yalnızca birkaç dakika içinde yardımcı olur.  Kılavuzu tamamladığınızda, uygulama dağıtabileceğiniz tek bir bilgisayarda çalışan üç düğümlü bir kümeniz olur.

## <a name="before-you-begin"></a>Başlamadan önce
Service Fabric paketi toocreate Service Fabric tek başına kümelerinin bir kurulum sağlar.  [Merhaba Kurulum paketini indirin](http://go.microsoft.com/fwlink/?LinkId=730690).  Merhaba bilgisayarınıza veya sanal makine hello kurulum paketi tooa klasörü hello geliştirme küme burada ayarladığınız sıkıştırmasını açın.  Merhaba Kurulum paketini Merhaba içeriğine ayrıntılı olarak açıklanmıştır [burada](service-fabric-cluster-standalone-package-contents.md).

dağıtma ve hello küme yapılandırma hello Küme Yöneticisi hello bilgisayar üzerinde yönetici ayrıcalıklarına sahip olmalıdır. Service Fabric’i bir etki alanı denetleyicisine yükleyemezsiniz.

## <a name="validate-hello-environment"></a>Merhaba ortamı doğrula
Merhaba *TestConfiguration.ps1* bir küme belirli bir ortamda dağıtılabilir olup olmadığını hello tek başına paketindeki komut dosyası en iyi yöntemler Çözümleyicisi toovalidate kullanılır. [Dağıtımı hazırlığı](service-fabric-cluster-standalone-deployment-preparation.md) listeleri hello ön koşullar ve ortam gereksinimleri. Merhaba geliştirme küme oluşturup oluşturamayacağını hello betik tooverify çalıştırın:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Merhaba kümesi oluşturma
Birkaç örnek küme yapılandırma dosyaları hello kurulum paketi ile yüklenir. *ClusterConfig.Unsecure.DevCluster.json* hello basit küme yapılandırması: tek bir bilgisayarda çalışan bir güvenli olmayan, üç düğümlü küme.  Diğer yapılandırma dosyalarında X.509 sertifikalarıyla ya da Windows güvenliğiyle korunan tek veya çok makineli kümeler açıklanır.  Toomodify hello varsayılan yapılandırma ayarlarından herhangi birini Bu öğretici için gereken ancak hello yapılandırma dosyası aracılığıyla bakın ve hello ayarları ile tanışın yok.  Merhaba **düğümleri** bölüm hello kümede üç düğüm hello açıklar: adı, IP adresi [düğüm türü, hata etki alanı ve yükseltme etki alanı](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Merhaba **özellikleri** bölümü tanımlar hello [güvenlik, güvenilirlik düzeyi, tanılama koleksiyonu ve düğüm türlerini](service-fabric-cluster-manifest.md#cluster-properties) hello kümesi için.

Bu küme güvenli değildir.  Herkes anonim olarak bağlanıp yönetim işlemleri gerçekleştirebileceğinden, üretim kümeleri her zaman X.509 sertifikaları veya Windows güvenliği kullanılarak güvenli hale getirilmelidir.  Güvenlik yalnızca küme oluşturma sırasında yapılandırılır ve hello Küme oluşturulduktan sonra olası tooenable güvenlik değil.  Okuma [bir küme güvenli](service-fabric-cluster-security.md) toolearn Service Fabric kümesi güvenliği hakkında daha fazla bilgi.  

Merhaba çalıştırmak, toocreate hello üç düğümü geliştirme küme *CreateServiceFabricCluster.ps1* bir yönetici PowerShell oturumunda komut dosyası:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Merhaba Service Fabric çalışma zamanı paketini otomatik olarak indirilir ve küme oluşturma sırasında yüklenir.

## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın
Üç düğümlü geliştirme kümeniz artık çalışıyor. Merhaba ServiceFabric PowerShell modülü hello çalışma zamanı ile yüklenir.  Bu hello küme hello çalışan doğrulayabilirsiniz aynı bilgisayarda veya uzak bir bilgisayardan hello Service Fabric çalışma zamanı.  Merhaba [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i bir bağlantı toohello kümesi oluşturur.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) bağlanan tooa kümenin diğer örnekler için. Bağlantı toohello küme sonra hello kullanmak [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello küme ve durum bilgilerini her düğüm için düğüm listesi. Her düğüm için **HealthState** değerinin *OK* olması gerekir.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Service Fabric explorer'ı kullanarak hello küme Görselleştirme
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), kümenizi görselleştirmek ve uygulamaları yönetmek için iyi bir araçtır.  Service Fabric Explorer hizmettir çok giderek bir tarayıcı kullanarak erişim hello kümede çalışan bir[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). 

Merhaba küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar. Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir. Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Merhaba küme Kaldır
Merhaba çalıştırmak tooremove bir küme *RemoveServiceFabricCluster.ps1* PowerShell Betiği hello paket klasörüne ve hello yol toohello JSON yapılandırma dosyası geçirin. İsteğe bağlı olarak hello silme hello günlük için bir konum belirtebilirsiniz.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

PowerShell Betiği hello paket klasöründen aşağıdaki hello çalıştırmak hello bilgisayardan tooremove hello Service Fabric çalışma.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Sonraki adımlar
Geliştirme tek başına küme ayarlama, makaleler hello deneyin:
* [Çok makineli tek başına küme ayarlama](service-fabric-cluster-creation-for-windows-server.md) ve güvenliği etkinleştirme.
* [PowerShell kullanarak uygulama dağıtma](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
