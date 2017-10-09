---
title: "aaaAzure Service Fabric, Linux ve Windows farkları | Microsoft Docs"
description: "Hello Azure Service Fabric Önizleme Linux ve Windows Azure Service Fabric arasındaki farklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a>Linux (önizleme) ve Windows (genel kullanıma açık) üzerindeki Service Fabric arasındaki farklar

Linux üzerinde Service Fabric önizleme aşamasında olduğundan, Windows’ta desteklenip Linux’ta henüz desteklenmeyen bazı özellikler mevcuttur. Sonuç olarak, Service Fabric Linux üzerinde genel kullanıma sunulduğunda hello özellik kümeleri eşlik olacaktır. Gelecek sürümlerle birlikte bu özellik farkı azalacaktır. Merhaba aşağıdaki hello en son kullanılabilir sürümleri farklar (diğer bir deyişle, sürüm 5.6 Windows ve Linux 5.5 sürümünde arasında): 

* Güvenilir Koleksiyonlar (ve Güvenilir Durum Bilgisi Olan Hizmetler) 
* Ters ara sunucu 
* Tek başına yükleyici 
* Bildirim dosyaları için XML şema doğrulaması 
* Konsol yeniden yönlendirmesi 
* Merhaba hataya Analiz Hizmeti (SK'lar)
* Kapsayıcılar için Docker Compose, birim ve günlük sürücüleri 
* Kapsayıcılar ve hizmetler için kaynak idaresi 
* DNS hizmeti
* Azure Active Directory desteği
* Belirli PowerShell komutlarının CLI komutu eşdeğerleri 
* Powershell komutları yalnızca bir kısmı (Merhaba sonraki bölümde genişletilmiş gibi) bir Linux kümesi karşı çalıştırabilirsiniz.

>[!NOTE]
>Konsol yönlendirmesi, Windows’ta bile üretim kümelerinde desteklenmez.

Geliştirme araçları da Windows ile Linux arasında farklılık gösterir. VisualStudio, Powershell, VSTS ve ETW özellikleri Windows üzerinde kullanılabilirken, Linux üzerinde Yeoman, Eclipse, Jenkins ve LTTng kullanılabilir.

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>Linux Service Fabric kümesinde çalışmayan PowerShell cmdlet'leri

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Cmd
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-linux.md)
* [OSX üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-mac.md)
* [Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-create-your-first-linux-application-with-java.md)
* [Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md)
* [Linux üzerinde ilk CSharp uygulamanızı oluşturma](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Merhaba Service Fabric CLI toomanage uygulamalarınızı kullanın](service-fabric-application-lifecycle-sfctl.md)
