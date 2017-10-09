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
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="14938-104">İlk tek başına Service Fabric kümenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="14938-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="14938-105">Herhangi bir sanal makineler veya Windows Server 2012 R2 veya Windows Server 2016, şirket içi çalıştıran bilgisayarlar üzerinde veya hello bulutta bir Service Fabric tek başına kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14938-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="14938-106">Bu hızlı başlangıç toocreate geliştirme tek başına küme yalnızca birkaç dakika içinde yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="14938-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="14938-107">Kılavuzu tamamladığınızda, uygulama dağıtabileceğiniz tek bir bilgisayarda çalışan üç düğümlü bir kümeniz olur.</span><span class="sxs-lookup"><span data-stu-id="14938-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="14938-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="14938-108">Before you begin</span></span>
<span data-ttu-id="14938-109">Service Fabric paketi toocreate Service Fabric tek başına kümelerinin bir kurulum sağlar.</span><span class="sxs-lookup"><span data-stu-id="14938-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="14938-110">[Merhaba Kurulum paketini indirin](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="14938-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="14938-111">Merhaba bilgisayarınıza veya sanal makine hello kurulum paketi tooa klasörü hello geliştirme küme burada ayarladığınız sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="14938-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="14938-112">Merhaba Kurulum paketini Merhaba içeriğine ayrıntılı olarak açıklanmıştır [burada](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="14938-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="14938-113">dağıtma ve hello küme yapılandırma hello Küme Yöneticisi hello bilgisayar üzerinde yönetici ayrıcalıklarına sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="14938-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="14938-114">Service Fabric’i bir etki alanı denetleyicisine yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="14938-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="14938-115">Merhaba ortamı doğrula</span><span class="sxs-lookup"><span data-stu-id="14938-115">Validate hello environment</span></span>
<span data-ttu-id="14938-116">Merhaba *TestConfiguration.ps1* bir küme belirli bir ortamda dağıtılabilir olup olmadığını hello tek başına paketindeki komut dosyası en iyi yöntemler Çözümleyicisi toovalidate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14938-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="14938-117">[Dağıtımı hazırlığı](service-fabric-cluster-standalone-deployment-preparation.md) listeleri hello ön koşullar ve ortam gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="14938-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="14938-118">Merhaba geliştirme küme oluşturup oluşturamayacağını hello betik tooverify çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="14938-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="14938-119">Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="14938-119">Create hello cluster</span></span>
<span data-ttu-id="14938-120">Birkaç örnek küme yapılandırma dosyaları hello kurulum paketi ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="14938-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="14938-121">*ClusterConfig.Unsecure.DevCluster.json* hello basit küme yapılandırması: tek bir bilgisayarda çalışan bir güvenli olmayan, üç düğümlü küme.</span><span class="sxs-lookup"><span data-stu-id="14938-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="14938-122">Diğer yapılandırma dosyalarında X.509 sertifikalarıyla ya da Windows güvenliğiyle korunan tek veya çok makineli kümeler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="14938-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="14938-123">Toomodify hello varsayılan yapılandırma ayarlarından herhangi birini Bu öğretici için gereken ancak hello yapılandırma dosyası aracılığıyla bakın ve hello ayarları ile tanışın yok.</span><span class="sxs-lookup"><span data-stu-id="14938-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="14938-124">Merhaba **düğümleri** bölüm hello kümede üç düğüm hello açıklar: adı, IP adresi [düğüm türü, hata etki alanı ve yükseltme etki alanı](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="14938-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="14938-125">Merhaba **özellikleri** bölümü tanımlar hello [güvenlik, güvenilirlik düzeyi, tanılama koleksiyonu ve düğüm türlerini](service-fabric-cluster-manifest.md#cluster-properties) hello kümesi için.</span><span class="sxs-lookup"><span data-stu-id="14938-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="14938-126">Bu küme güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="14938-126">This cluster is unsecure.</span></span>  <span data-ttu-id="14938-127">Herkes anonim olarak bağlanıp yönetim işlemleri gerçekleştirebileceğinden, üretim kümeleri her zaman X.509 sertifikaları veya Windows güvenliği kullanılarak güvenli hale getirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="14938-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="14938-128">Güvenlik yalnızca küme oluşturma sırasında yapılandırılır ve hello Küme oluşturulduktan sonra olası tooenable güvenlik değil.</span><span class="sxs-lookup"><span data-stu-id="14938-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="14938-129">Okuma [bir küme güvenli](service-fabric-cluster-security.md) toolearn Service Fabric kümesi güvenliği hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="14938-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="14938-130">Merhaba çalıştırmak, toocreate hello üç düğümü geliştirme küme *CreateServiceFabricCluster.ps1* bir yönetici PowerShell oturumunda komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="14938-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="14938-131">Merhaba Service Fabric çalışma zamanı paketini otomatik olarak indirilir ve küme oluşturma sırasında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="14938-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="14938-132">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="14938-132">Connect toohello cluster</span></span>
<span data-ttu-id="14938-133">Üç düğümlü geliştirme kümeniz artık çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="14938-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="14938-134">Merhaba ServiceFabric PowerShell modülü hello çalışma zamanı ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="14938-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="14938-135">Bu hello küme hello çalışan doğrulayabilirsiniz aynı bilgisayarda veya uzak bir bilgisayardan hello Service Fabric çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="14938-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="14938-136">Merhaba [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i bir bağlantı toohello kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="14938-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="14938-137">Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) bağlanan tooa kümenin diğer örnekler için.</span><span class="sxs-lookup"><span data-stu-id="14938-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="14938-138">Bağlantı toohello küme sonra hello kullanmak [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello küme ve durum bilgilerini her düğüm için düğüm listesi.</span><span class="sxs-lookup"><span data-stu-id="14938-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="14938-139">Her düğüm için **HealthState** değerinin *OK* olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="14938-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="14938-140">Service Fabric explorer'ı kullanarak hello küme Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="14938-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="14938-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), kümenizi görselleştirmek ve uygulamaları yönetmek için iyi bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="14938-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="14938-142">Service Fabric Explorer hizmettir çok giderek bir tarayıcı kullanarak erişim hello kümede çalışan bir[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="14938-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="14938-143">Merhaba küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="14938-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="14938-144">Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir.</span><span class="sxs-lookup"><span data-stu-id="14938-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="14938-145">Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14938-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="14938-147">Merhaba küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="14938-147">Remove hello cluster</span></span>
<span data-ttu-id="14938-148">Merhaba çalıştırmak tooremove bir küme *RemoveServiceFabricCluster.ps1* PowerShell Betiği hello paket klasörüne ve hello yol toohello JSON yapılandırma dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="14938-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="14938-149">İsteğe bağlı olarak hello silme hello günlük için bir konum belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14938-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="14938-150">PowerShell Betiği hello paket klasöründen aşağıdaki hello çalıştırmak hello bilgisayardan tooremove hello Service Fabric çalışma.</span><span class="sxs-lookup"><span data-stu-id="14938-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="14938-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14938-151">Next steps</span></span>
<span data-ttu-id="14938-152">Geliştirme tek başına küme ayarlama, makaleler hello deneyin:</span><span class="sxs-lookup"><span data-stu-id="14938-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="14938-153">[Çok makineli tek başına küme ayarlama](service-fabric-cluster-creation-for-windows-server.md) ve güvenliği etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="14938-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="14938-154">PowerShell kullanarak uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="14938-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
