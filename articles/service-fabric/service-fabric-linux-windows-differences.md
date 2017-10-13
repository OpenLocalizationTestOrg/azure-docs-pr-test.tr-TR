---
title: "Linux ile Windows arasındaki Azure Service Fabric farkları | Microsoft Docs"
description: "Linux üzerindeki Azure Service Fabric ile Windows üzerindeki Azure Service Fabric arasındaki farklar."
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
ms.date: 09/19/2017
ms.author: subramar
ms.openlocfilehash: 25976ba919454e26f1dd7965de5db7c4f80b9355
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="differences-between-service-fabric-on-linux-and-windows"></a>Linux ve Windows üzerindeki Service Fabric arasındaki farklar

Windows'da desteklenip Linux'ta henüz desteklenmeyen bazı özellikler mevcuttur. Bu nedenle özellik kümeleri birbirinden farklı olacak ve bu fark yeni sürümlerle azalacaktır. Mevcut son sürümler arasında (diğer bir deyişle Windows üzerindeki 6.0 sürümü ve Linux üzerindeki 6.0 sürümü arasında) aşağıdaki farklar mevcuttur: 

* Tüm programlama modelleri önizleme sürümündedir (Java/C# Reliable Actors, Güvenilir Durum Bilgisi Olmayan Hizmetler ve Güvenilir Durum Bilgisi Olan Hizmetler)
* Envoy (ReverseProxy), Linux'ta önizleme sürümündedir
* Linux için tek başına yükleyici, Linux üzerinde kullanılamaz
* Konsol yönlendirmesi (Linux veya Windows üretim kümelerinde desteklenmez)
* Linux'ta Hata Analizi Hizmeti (FAS)
* Service Fabric hizmetleri için DNS hizmeti (DNS hizmeti Linux üzerindeki kapsayıcılar için desteklenir)
* Belirli Powershell komutlarının CLI komutu eşdeğerleri (liste aşağıda verilmiştir, komutların çoğu yalnızca tek başına kümeler için geçerlidir)

Geliştirme araçları da Windows ile Linux arasında farklılık gösterir. Visual Studio, Powershell, VSTS ve ETW özellikleri Windows üzerinde kullanılabilirken, Linux üzerinde Yeoman, Eclipse, Jenkins ve LTTng kullanılabilir.

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
* [Uygulamalarınızı yönetmek için Service Fabric CLI'yı kullanma](service-fabric-application-lifecycle-sfctl.md)
