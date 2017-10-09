---
title: "aaaAdd veya kaldırma düğümleri tooa tek başına Service Fabric kümesi | Microsoft Docs"
description: "Nasıl tooadd veya kaldırma düğümleri tooan Azure Service Fabric kümesi bir fiziksel veya şirket içi olarak Windows Server çalıştıran sanal makine üzerinde veya tüm bulut bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Windows Server'da çalışan düğümleri tooa tek başına Service Fabric kümesi Ekle Kaldır
Sonra [Windows Server makinelerde tek başına Service Fabric kümesi oluşturulan](service-fabric-cluster-creation-for-windows-server.md), iş gereksinimlerinize değiştirebilir ve düğümler tooyour kümesini kaldırmak veya tooadd ihtiyacınız olabilir. Bu makalede bu ayrıntılı adımlar tooachieve sağlar. Lütfen Ekle/Kaldır düğümü işlevselliği yerel geliştirme kümelerinde desteklenmez unutmayın.

## <a name="add-nodes-tooyour-cluster"></a>Tooyour küme düğümleri Ekle
1. Prepare hello VM/makine hello bahsedilen hello adımları izleyerek tooadd tooyour küme istediğiniz [hazırlama hello makineleri Küme dağıtımı için toomeet hello Önkoşullar](service-fabric-cluster-creation-for-windows-server.md) bölümü
2. Hangi hata etki alanı ve bu VM/makineye giderek tooadd olduğunuz yükseltme etki alanını tanımlayın
3. Uzak Masaüstü (RDP) hello VM/makine tooadd toohello küme istediğiniz başlatın
4. Kopyalama veya [Windows Server için Service Fabric hello tek başına paketini indirin](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/makine ve hello paketin sıkıştırmasını açın
5. PowerShell yükseltilmiş ayrıcalıklarla çalıştırın ve hello sıkıştırması açılmış paketi toohello konumu gidin
6. Merhaba çalıştırmak *AddNode.ps1* betik hello yeni düğümü tooadd açıklayan hello parametrelere sahip. Aşağıdaki Hello örnek VM5 olarak adlandırılan yeni bir düğüm ekler, türüyle NodeType0 ve IP 182.17.34.52, UD1 ve fd halinde adresi: / dc1/r0. Merhaba *ExistingClusterConnectionEndPoint* hello mevcut kümede zaten bir bağlantı uç noktası bir düğüme hello IP adresini olabilen *herhangi* hello kümedeki düğüm.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Hello betik çalışması bittikten sonra hello yeni düğüm hello çalıştırarak eklenip eklenmediğini denetleyebilirsiniz [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet'i.

7. tooensure tutarlılık hello kümedeki farklı düğümleri arasındaki yapılandırma yükseltme başlatması gerekir. Çalıştırmak [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello son yapılandırma dosyasını ve hello yeni eklenen düğüm çok Ekle "Düğümleri" bölümü. Ayrıca tooalways hello son küme yapılandırması tooredploy hello kümeyle duyduğunuz hello durumda kullanılabilir olması önerilir aynı yapılandırma.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz. Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Windows güvenliği kullanarak gMSA düğümleri tooclusters yapılandırılmış ekleme
Grup yönetilen hizmet Account(gMSA) ile (https://technet.microsoft.com/library/hh831782.aspx) yapılandırılmış kümeler için yapılandırma yükseltme kullanarak yeni bir düğüm eklenebilir:
1. Çalıştırma [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) varolan herhangi bir hello düğüme tooget hello son yapılandırma dosyasını ve ayrıntılarını Ekle tooadd hello "düğümleri" bölümünde istediğiniz hello yeni düğümü. Merhaba Yeni düğümün bir parçası olduğundan emin olun hello aynı grup yönetilen hesabı. Bu hesap tüm makinelerde yönetici olmanız gerekir.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz. Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Düğüm türleri tooyour kümesi Ekle
İçinde yeni düğüm türü tooadd sipariş, yapılandırma tooinclude hello yeni düğüm türü "Özellikler" altında "NodeTypes" bölümündeki değiştirmek ve bir yapılandırmaya başlamadan kullanarak yükseltme [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Merhaba yükseltme işlemi tamamlandıktan sonra bu düğüm türü ile yeni düğümler tooyour küme ekleyebilirsiniz.

## <a name="remove-nodes-from-your-cluster"></a>Kümeden düğüm kaldırma
Bir yapılandırma yükseltme şekilde aşağıdaki hello kullanarak bir kümeden bir düğümü kaldırılabilir:

1. Çalıştırma [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello son yapılandırma dosyasını ve *kaldırmak* "Düğümleri" bölümünden hello düğümü.
Merhaba "NodesToBeRemoved" eklemek parametre çok "Kurulum" Bölüm "FabricSettings" bölüm içinde. Merhaba "value" kaldırılan toobe gereken düğümleri düğüm adlarının virgülle ayrılmış bir listesi olmalıdır.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz. Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> Düğümleri kaldırma birden fazla yükseltme başlatabilir. Bazı düğümler işaretlenir `IsSeedNode=”true”` etiketi ve hello küme sorgulayarak tanımlanabilir kullanarak bildirim `Get-ServiceFabricClusterManifest`. Merhaba çekirdek düğümleri gibi senaryolarda taşınmış toobe gerekeceğinden bu düğümleri kaldırılmasını diğerlerinden daha uzun sürebilir. Merhaba küme en az 3 birincil düğüm türü düğümleri bulundurmanız gerekir.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Düğüm türleri, kümeden kaldırma
Merhaba düğüm türü başvuran tüm düğümleri varsa bir düğüm türü kaldırmadan önce çift gözden geçirin. Bu düğümler hello karşılık gelen düğüm türü kaldırmadan önce kaldırın. Tüm ilgili düğümleri kaldırıldıktan sonra hello NodeType hello küme yapılandırmasından kaldırmak ve bir yapılandırmaya başlamadan kullanarak yükseltme [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Birincil düğüm kümenizin değiştirin
birincil düğüm Hello değiştirme ardına toplu olarak ekleme ve kaldırma yerine gerçekleştirilen bir düğüm olmalıdır.


## <a name="next-steps"></a>Sonraki adımlar
* [Tek başına Windows kümesi için yapılandırma ayarları](service-fabric-cluster-manifest.md)
* [Tek başına küme X509 kullanarak Windows güvenli sertifikaları](service-fabric-windows-cluster-x509-security.md)
* [Azure VM'ler Windows çalıştıran bir tek başına Service Fabric kümesi oluştur](service-fabric-cluster-creation-with-windows-azure-vms.md)

