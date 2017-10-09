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
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="94d5e-103">Windows Server çalıştıran Azure sanal makineler ile üç düğümü tek başına Service Fabric kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="94d5e-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="94d5e-104">Nasıl toocreate Windows tabanlı Azure sanal makineleri (VM'ler) kümede bir kullanarak hello tek başına Service Fabric yükleyici için bu makalede Windows Server.</span><span class="sxs-lookup"><span data-stu-id="94d5e-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="94d5e-105">Merhaba senaryodur, özel bir durum [oluşturma ve Windows Server'da çalışan bir kümeyi yönetmek](service-fabric-cluster-creation-for-windows-server.md) hello VM'ler nerede [Azure Windows Server çalıştıran VM'ler](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), oluşturduğunuz değil ancak [Azure bulut tabanlı Service Fabric kümesi](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94d5e-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="94d5e-106">bulut tabanlı Azure Service Fabric kümeleri hello yönetilir ve Service Fabric hello tarafından yükseltilmiş ise aşağıdaki adımları hello tarafından oluşturulan bu hello tek başına Service Fabric kümesi tamamen sizin tarafınızdan yönetilen bu deseni takip içinde hello ayrım ilgilidir Kaynak sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="94d5e-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="94d5e-107">Adımları toocreate hello tek başına küme</span><span class="sxs-lookup"><span data-stu-id="94d5e-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="94d5e-108">Toohello Azure portalında oturum açın ve yeni bir Windows Server 2012 R2 Datacenter veya Windows Server 2016 Datacenter VM bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="94d5e-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="94d5e-109">Merhaba makale okuma [hello Azure portalında bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="94d5e-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="94d5e-110">Daha fazla birkaç VM'ler toohello eklemek aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="94d5e-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="94d5e-111">Her hello VM'ler sahip Merhaba, aynı yönetici kullanıcı adı ve parola oluşturduğunuzda emin olun.</span><span class="sxs-lookup"><span data-stu-id="94d5e-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="94d5e-112">Oluşturduktan sonra hello tüm üç Vm'lerde gördüğünüz aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="94d5e-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="94d5e-113">Merhaba VM'ler tooeach bağlayın ve devre dışı hello hello kullanarak Windows Güvenlik Duvarı'nı açın [Sunucu Yöneticisi, yerel sunucu Panosu](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="94d5e-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="94d5e-114">Bu, hello ağ trafiğini hello makineler arasında iletişim kurabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d5e-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="94d5e-115">Bir komut istemi'ni açıp yazarak bağlı tooeach makine, başlangıç IP adresi al `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="94d5e-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="94d5e-116">Alternatif olarak, hello IP görebilirsiniz hello sanal ağ kaynağı hello kaynak grubu için seçerek ve her bu makineleri için oluşturulan hello ağ arabirimleri denetimi hello portal her makinede adresidir.</span><span class="sxs-lookup"><span data-stu-id="94d5e-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="94d5e-117">Merhaba VM'ler tooone bağlanın ve ping atabilir test hello diğer iki VM başarıyla.</span><span class="sxs-lookup"><span data-stu-id="94d5e-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="94d5e-118">Merhaba VM'ler tooone bağlanmak ve [hello tek başına Service Fabric paketi indirmek için Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) hello üzerinde yeni bir klasöre makine ve hello paket ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="94d5e-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="94d5e-119">Açık hello *ClusterConfig.Unsecure.MultiMachine.json* dosyasını Not Defteri'nde ve her düğüm hello makinelerin hello üç IP adresleriyle düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="94d5e-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="94d5e-120">Merhaba üstünde Hello küme adını değiştirin ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="94d5e-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="94d5e-121">Merhaba küme bildiriminde kısmi bir örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94d5e-121">A partial example of hello cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="94d5e-122">Bu toobe güvenli küme düşünüyorsanız, hello hello adımları izleyin ve gibi toouse hello güvenlik önlemi ilişkili bağlantı karar verin: [X509 sertifika](service-fabric-windows-cluster-x509-security.md) veya [Windows Güvenliği](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="94d5e-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="94d5e-123">Windows güvenliği kullanarak hello kümeyi ayarlamadan bir Active Directory etki alanı denetleyicisi toomanage yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d5e-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="94d5e-124">Service Fabric bir etki alanı denetleyicisi makine kullanarak düğüm desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="94d5e-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="94d5e-125">Açık bir [PowerShell ISE penceresi](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="94d5e-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="94d5e-126">Burada hello indirilen tek başına yükleyici paketi ayıklanan ve hello küme yapılandırma dosyasını kaydettiğiniz toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="94d5e-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="94d5e-127">PowerShell komut toodeploy hello küme aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="94d5e-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="94d5e-128">Merhaba betik hello Service Fabric kümesi uzaktan yapılandırır ve aracılığıyla dağıtım yapar gibi ilerleme bildirmelidir.</span><span class="sxs-lookup"><span data-stu-id="94d5e-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="94d5e-129">Yaklaşık bir dakika, toohello bağlanarak hello küme işletimsel olup olmadığını denetleyebilirsiniz sonra Service Fabric Explorer hello makinenin IP birini kullanarak, örneğin kullanarak adresleri `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="94d5e-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="94d5e-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94d5e-130">Next steps</span></span>
* [<span data-ttu-id="94d5e-131">Windows Server veya Linux’ta tek başına Service Fabric kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="94d5e-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="94d5e-132">Ekleme veya düğümleri tooa tek başına Service Fabric kümesi kaldırma</span><span class="sxs-lookup"><span data-stu-id="94d5e-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="94d5e-133">Tek başına Windows kümesi için yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="94d5e-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="94d5e-134">Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli</span><span class="sxs-lookup"><span data-stu-id="94d5e-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="94d5e-135">Tek başına küme X509 kullanarak Windows güvenli sertifikaları</span><span class="sxs-lookup"><span data-stu-id="94d5e-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

