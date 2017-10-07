---
title: "Windows Server için Service Fabric tek başına paketi aaaAzure | Microsoft Docs"
description: "Açıklama ve Windows Server için hello Azure Service Fabric tek başına yükleme paketinin içeriğini."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Windows Server için Service Fabric tek başına paketinin içeriği
Merhaba, [indirilen](http://go.microsoft.com/fwlink/?LinkId=730690) Service Fabric tek başına paket, aşağıdaki dosyaları hello bulacaksınız:

| **Dosya adı** | **Kısa açıklama** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |ClusterConfig.json içinde hello ayarlarını kullanarak hello küme oluşturur bir PowerShell komut dosyası. |
| RemoveServiceFabricCluster.ps1 |ClusterConfig.json içinde hello ayarları kullanarak bir küme kaldıran bir PowerShell komut dosyası. |
| AddNode.ps1 |Düğüm varolan tooan eklemek için bir PowerShell Betiği küme hello geçerli makineye dağıtıldı. |
| RemoveNode.ps1 |Mevcut bir düğüm kaldırmak için bir PowerShell Betiği hello geçerli makine kümeden dağıtıldı. |
| CleanFabric.ps1 |Tek başına Service Fabric yüklemesini hello geçerli makineye devre dışı Temizleme için bir PowerShell Betiği. Kendi ilişkili uninstallers kullanarak önceki MSI yüklemeleri kaldırılması gerekir. |
| TestConfiguration.ps1 |Merhaba Cluster.json belirtildiği gibi hello altyapı çözümleme için bir PowerShell Betiği. |
| DownloadServiceFabricRuntimePackage.ps1 |Bağlı olan toohello makine dağıtma hello olduğu senaryolar için bant dışı hello son çalışma zamanı paketini karşıdan yüklemek için kullanılan bir PowerShell Betiği Internet. |
| DeploymentComponentsAutoextractor.exe |Dağıtım bileşenlerini içeren kendi kendine arşivinden hello tarafından tek başına paket betikleri kullanılır. |
| EULA_ENU.txt |Merhaba Hello lisans koşulları, Microsoft Azure Service Fabric tek başına Windows Server paketi kullanın. Yapabilecekleriniz [hello EULA bir kopyasını indirin](http://go.microsoft.com/fwlink/?LinkID=733084) şimdi. |
| Readme.txt |Bağlantı toohello sürüm notları ve temel yükleme yönergeleri. Bu belgedeki hello yönergeleri alt kümesidir. |
| ThirdPartyNotice.rtf |Merhaba paketteki üçüncü taraf yazılım dikkat edin. |
| Tools\Microsoft.Azure.ServiceFabric.windowsserver.SupportPackage.zip |İsteğe bağlı toocollect ve karşıya yükleme izleme üzerinde çalıştırıldığı StandaloneLogCollector.exe destek amaçla tooMicrosoft günlüğe kaydeder. |
| Tools\ServiceFabricUpdateService.zip |Bir aracı tooenable otomatik kod yükseltme internet erişimi olmayan kümeler için kullanılır. Daha fazla ayrıntı bulunabilir [burada](service-fabric-cluster-upgrade-windows-server.md)|

**Şablonlar** 
| **Dosya adı** | **Kısa açıklama** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Merhaba kümedeki her düğüm için hello bilgiler dahil olmak üzere bir güvenli, üç düğümlü tek makineli (veya sanal makine) geliştirme kümesi hello ayarlarını içeren bir küme yapılandırması örnek dosyası. |
| ClusterConfig.Unsecure.MultiMachine.json |Merhaba kümedeki her makine için hello bilgiler dahil olmak üzere bir güvenli, çok makineli (veya sanal makine) küme için hello ayarlarını içeren bir küme yapılandırması örnek dosyası. |
| ClusterConfig.Windows.DevCluster.json |Merhaba kümesinde bulunan her bir düğüm için hello bilgiler dahil olmak üzere tüm hello güvenli, üç düğümlü tek makineli (veya sanal makine) ayarlarını geliştirme kümesi içeren bir küme yapılandırması örnek dosyası. Merhaba küme kullanarak güvenli [Windows kimliklerini](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Merhaba güvenli kümedeki her makine için başlangıç bilgileri de dahil, Windows güvenliği kullanarak güvenli, çok makineli (veya sanal makine) küme için tüm hello ayarlarını içeren bir küme yapılandırması örnek dosyası. Merhaba küme kullanarak güvenli [Windows kimliklerini](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Tüm hello ayarlarını hello kümedeki her düğüm için hello bilgiler dahil olmak üzere güvenli, üç düğümlü tek makineli (veya sanal makine) geliştirme kümesi içeren bir küme yapılandırması örnek dosyası. Merhaba küme x509 güvenliğinin ile sertifikalar. |
| ClusterConfig.x509.MultiMachine.json |Merhaba güvenli kümedeki her düğüm için hello bilgiler dahil olmak üzere hello güvenli, çok makineli (veya sanal makine) küme için tüm hello ayarlarını içeren bir küme yapılandırması örnek dosyası. Merhaba küme x509 güvenliğinin ile sertifikalar. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Merhaba güvenli kümedeki her düğüm için hello bilgiler dahil olmak üzere hello güvenli, çok makineli (veya sanal makine) küme için tüm hello ayarlarını içeren bir küme yapılandırması örnek dosyası. Merhaba küme güvenliğinin ile [Grup yönetilen hizmet hesapları](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Küme yapılandırma örnekleri
Küme yapılandırması şablonları en son sürümlerini hello GitHub sayfasında bulunabilir: [tek başına küme yapılandırma örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Bağımsız çalışma zamanı paketi
Merhaba son çalışma zamanı paketini karşıdan otomatik olarak Küme dağıtımı sırasında [karşıdan yükleme bağlantısı - Service Fabric çalışma zamanı - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>İlgili
* [Tek başına Azure Service Fabric kümesi oluştur](service-fabric-cluster-creation-for-windows-server.md)
* [Service Fabric kümesi güvenlik senaryoları](service-fabric-windows-cluster-windows-security.md)
