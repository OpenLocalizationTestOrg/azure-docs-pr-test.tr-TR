---
title: "aaaCreate tek başına bir küme olan Azure Windows çalıştıran VM'ler | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Windows Server çalıştıran Azure sanal makinelerinde Azure Service Fabric kümesi yönetin."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Windows Server çalıştıran Azure sanal makineler ile üç düğümü tek başına Service Fabric kümesi oluşturma
Nasıl toocreate Windows tabanlı Azure sanal makineleri (VM'ler) kümede bir kullanarak hello tek başına Service Fabric yükleyici için bu makalede Windows Server. Merhaba senaryodur, özel bir durum [oluşturma ve Windows Server'da çalışan bir kümeyi yönetmek](service-fabric-cluster-creation-for-windows-server.md) hello VM'ler nerede [Azure Windows Server çalıştıran VM'ler](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), oluşturduğunuz değil ancak [Azure bulut tabanlı Service Fabric kümesi](service-fabric-cluster-creation-via-portal.md). bulut tabanlı Azure Service Fabric kümeleri hello yönetilir ve Service Fabric hello tarafından yükseltilmiş ise aşağıdaki adımları hello tarafından oluşturulan bu hello tek başına Service Fabric kümesi tamamen sizin tarafınızdan yönetilen bu deseni takip içinde hello ayrım ilgilidir Kaynak sağlayıcısı.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Adımları toocreate hello tek başına küme
1. Toohello Azure portalında oturum açın ve yeni bir Windows Server 2012 R2 Datacenter veya Windows Server 2016 Datacenter VM bir kaynak grubu oluşturun. Merhaba makale okuma [hello Azure portalında bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) daha fazla ayrıntı için.
2. Daha fazla birkaç VM'ler toohello eklemek aynı kaynak grubu. Her hello VM'ler sahip Merhaba, aynı yönetici kullanıcı adı ve parola oluşturduğunuzda emin olun. Oluşturduktan sonra hello tüm üç Vm'lerde gördüğünüz aynı sanal ağ.
3. Merhaba VM'ler tooeach bağlayın ve devre dışı hello hello kullanarak Windows Güvenlik Duvarı'nı açın [Sunucu Yöneticisi, yerel sunucu Panosu](https://technet.microsoft.com/library/jj134147.aspx). Bu, hello ağ trafiğini hello makineler arasında iletişim kurabilir sağlar. Bir komut istemi'ni açıp yazarak bağlı tooeach makine, başlangıç IP adresi al `ipconfig`. Alternatif olarak, hello IP görebilirsiniz hello sanal ağ kaynağı hello kaynak grubu için seçerek ve her bu makineleri için oluşturulan hello ağ arabirimleri denetimi hello portal her makinede adresidir.
4. Merhaba VM'ler tooone bağlanın ve ping atabilir test hello diğer iki VM başarıyla.
5. Merhaba VM'ler tooone bağlanmak ve [hello tek başına Service Fabric paketi indirmek için Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) hello üzerinde yeni bir klasöre makine ve hello paket ayıklayın.
6. Açık hello *ClusterConfig.Unsecure.MultiMachine.json* dosyasını Not Defteri'nde ve her düğüm hello makinelerin hello üç IP adresleriyle düzenleyin. Merhaba üstünde Hello küme adını değiştirin ve hello dosyasını kaydedin.  Merhaba küme bildiriminde kısmi bir örneği aşağıda verilmiştir.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Bu toobe güvenli küme düşünüyorsanız, hello hello adımları izleyin ve gibi toouse hello güvenlik önlemi ilişkili bağlantı karar verin: [X509 sertifika](service-fabric-windows-cluster-x509-security.md) veya [Windows Güvenliği](service-fabric-windows-cluster-windows-security.md). Windows güvenliği kullanarak hello kümeyi ayarlamadan bir Active Directory etki alanı denetleyicisi toomanage yukarı tooset gerekir. Service Fabric bir etki alanı denetleyicisi makine kullanarak düğüm desteklenmediğini unutmayın.
8. Açık bir [PowerShell ISE penceresi](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Burada hello indirilen tek başına yükleyici paketi ayıklanan ve hello küme yapılandırma dosyasını kaydettiğiniz toohello klasörüne gidin. PowerShell komut toodeploy hello küme aşağıdaki hello çalıştırın:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

Merhaba betik hello Service Fabric kümesi uzaktan yapılandırır ve aracılığıyla dağıtım yapar gibi ilerleme bildirmelidir.

9. Yaklaşık bir dakika, toohello bağlanarak hello küme işletimsel olup olmadığını denetleyebilirsiniz sonra Service Fabric Explorer hello makinenin IP birini kullanarak, örneğin kullanarak adresleri `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Sonraki adımlar
* [Windows Server veya Linux’ta tek başına Service Fabric kümeleri oluşturma](service-fabric-deploy-anywhere.md)
* [Ekleme veya düğümleri tooa tek başına Service Fabric kümesi kaldırma](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Tek başına Windows kümesi için yapılandırma ayarları](service-fabric-cluster-manifest.md)
* [Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-windows-security.md)
* [Tek başına küme X509 kullanarak Windows güvenli sertifikaları](service-fabric-windows-cluster-x509-security.md)

