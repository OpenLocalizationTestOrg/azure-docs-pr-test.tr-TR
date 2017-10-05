---
title: "Azure Service Fabric kümesi ayarlama | Microsoft Docs"
description: "Hızlı başlangıç- Azure’da bir Windows veya Linux Service Fabric kümesi oluşturun."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="287c6-103">Azure’da ilk Service Fabric kümenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="287c6-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="287c6-104">[Service Fabric kümesi](service-fabric-deploy-anywhere.md), mikro hizmetlerin dağıtılıp yönetildiği, ağa bağlı bir sanal veya fiziksel makine kümesidir.</span><span class="sxs-lookup"><span data-stu-id="287c6-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="287c6-105">Bu hızlı başlangıç, [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) veya [Azure portalı](http://portal.azure.com) üzerinden yalnızca birkaç dakika içinde Windows veya Linux üzerinde çalışan beş düğümlü bir küme oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="287c6-105">This quickstart helps you to create a five-node cluster, running on either Windows or Linux, through the [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="287c6-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="287c6-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-the-azure-portal"></a><span data-ttu-id="287c6-107">Azure portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="287c6-107">Use the Azure portal</span></span>

<span data-ttu-id="287c6-108">[http://portal.azure.com](http://portal.azure.com) sayfasından Azure portalda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="287c6-108">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-the-cluster"></a><span data-ttu-id="287c6-109">Kümeyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="287c6-109">Create the cluster</span></span>

1. <span data-ttu-id="287c6-110">Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="287c6-111">**Yeni** dikey penceresinden **İşlem**’i seçin ve ardından **İşlem** dikey penceresinden **Service Fabric Kümesi**’ni belirleyin.</span><span class="sxs-lookup"><span data-stu-id="287c6-111">Select **Compute** from the **New** blade and then select **Service Fabric Cluster** from the **Compute** blade.</span></span>
3. <span data-ttu-id="287c6-112">Service Fabric **Temel Bilgileri** formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="287c6-112">Fill out the Service Fabric **Basics** form.</span></span> <span data-ttu-id="287c6-113">**İşletim sistemi** için küme düğümlerinin çalışmasını istediğiniz Windows veya Linux sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-113">For **Operating system**, select the version of Windows or Linux you want the cluster nodes to run.</span></span> <span data-ttu-id="287c6-114">Burada girilen kullanıcı adı ve parola, sanal makinede oturum açarken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="287c6-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="287c6-115">**Kaynak grubu** için yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="287c6-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="287c6-116">Kaynak grubu, Azure kaynaklarının oluşturulup toplu olarak yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="287c6-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="287c6-117">İşlem tamamlandığında **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-117">When complete, click **OK**.</span></span>

    ![Küme kurulumu çıktısı][cluster-setup-basics]

4. <span data-ttu-id="287c6-119">**Küme yapılandırması** formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="287c6-119">Fill out the **Cluster configuration** form.</span></span>  <span data-ttu-id="287c6-120">**Düğüm türü sayısı** için "1" değerini girin.</span><span class="sxs-lookup"><span data-stu-id="287c6-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="287c6-121">**Düğüm türü 1 (Birincil)**’i seçip **Düğüm türü yapılandırma** formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="287c6-121">Select **Node type 1 (Primary)** and fill out the **Node type configuration** form.</span></span>  <span data-ttu-id="287c6-122">Düğüm türü adını girin ve [Dayanıklılık katmanı](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) için "Bronz" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="287c6-122">Enter a node type name and set the [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) to "Bronze."</span></span>  <span data-ttu-id="287c6-123">VM boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-123">Select a VM size.</span></span>

    <span data-ttu-id="287c6-124">Düğüm türleri VM boyutunu, VM sayısını, özel uç noktaları ve aynı türdeki VM’lerin diğer ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="287c6-124">Node types define the VM size, number of VMs, custom endpoints, and other settings for the VMs of that type.</span></span> <span data-ttu-id="287c6-125">Tanımlanan her düğüm türü, sanal makineleri küme olarak dağıtıp yönetmek için kullanılan ayrı bir sanal makine ölçek kümesi olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="287c6-125">Each node type defined is set up as a separate virtual machine scale set, which is used to deploy and managed virtual machines as a set.</span></span> <span data-ttu-id="287c6-126">Her düğüm türünün ölçeği birbirinden bağımsız olarak artırılabilir veya azaltılabilir, her düğüm türünde farklı bağlantı noktası kümeleri açık olabilir ve farklı kapasite ölçümleri yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="287c6-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="287c6-127">Birinci veya birincil düğüm türü, Service Fabric sistem hizmetlerinin barındırıldığı yerdir ve beş ya da daha fazla VM içermelidir.</span><span class="sxs-lookup"><span data-stu-id="287c6-127">The first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="287c6-128">Herhangi bir üretim dağıtımı için [kapsite planlaması](service-fabric-cluster-capacity.md) önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="287c6-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="287c6-129">Ancak, bu hızlı başlangıçta uygulama çalıştırmadığınız için bir *DS1_v2 Standart* VM boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="287c6-130">[Güvenilirlik katmanı](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) için "Gümüş" seçeneğini belirleyin ve sanal makine ölçek kümesinin başlangıç kapasitesini 5 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-130">Select "Silver" for the [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="287c6-131">Özel uç noktalar Azure Load Balancer’da bağlantı noktaları açtığı için, küme üzerinde çalışan uygulamalarla bağlantı kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-131">Custom endpoints open up ports in the Azure load balancer so that you can connect with applications running on the cluster.</span></span>  <span data-ttu-id="287c6-132">80 ve 8172 bağlantı noktalarını açmak için "80, 8172" girin.</span><span class="sxs-lookup"><span data-stu-id="287c6-132">Enter "80, 8172" to open up ports 80 and 8172.</span></span>

    <span data-ttu-id="287c6-133">TCP/HTTP yönetim uç noktalarını, uygulama bağlantı noktası aralıklarını, [yerleştirme kısıtlamalarını](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) ve [kapasite özelliklerini](service-fabric-cluster-resource-manager-metrics.md) özelleştirmek için kullanılan **Gelişmiş ayarları yapılandır** kutusunu işaretlemeyin.</span><span class="sxs-lookup"><span data-stu-id="287c6-133">Do not check the **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="287c6-134">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-134">Select **OK**.</span></span>

6. <span data-ttu-id="287c6-135">**Küme yapılandırması** formunda **Tanılama** ayarını **Açık** olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="287c6-135">In the **Cluster configuration** form, set **Diagnostics** to **On**.</span></span>  <span data-ttu-id="287c6-136">Bu hızlı başlangıçta herhangi bir [yapı ayarı](service-fabric-cluster-fabric-settings.md) özelliği girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="287c6-136">For this quickstart, you do not need to enter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="287c6-137">Microsoft’un kümeyi çalıştıran yapı kodu sürümünü otomatik olarak güncelleştirmesi için **Fabric sürümü** menüsünde **Otomatik** yükseltme modunu seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates the version of the fabric code running the cluster.</span></span>  <span data-ttu-id="287c6-138">Yükseltmenin yapılacağı [desteklenen bir sürüm seçmek](service-fabric-cluster-upgrade.md) istiyorsanız modu **El ile** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-138">Set the mode to **Manual** if you want to [choose a supported version](service-fabric-cluster-upgrade.md) to upgrade to.</span></span> 

    ![Düğüm türü yapılandırması][node-type-config]

    <span data-ttu-id="287c6-140">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-140">Select **OK**.</span></span>

7. <span data-ttu-id="287c6-141">**Güvenlik** formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="287c6-141">Fill out the **Security** form.</span></span>  <span data-ttu-id="287c6-142">Bu hızlı başlangıç için **Güvenli olmayan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="287c6-143">Ancak, güvenli olmayan bir kümeye herhangi bir kişi anonim olarak bağlanıp yönetim işlemlerini gerçekleştirebileceğinden, üretim iş yükleri için güvenli bir küme oluşturmanız önemle tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="287c6-143">It is highly recommended to create a secure cluster for production workloads, however, since anyone can anonymously connect to an unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="287c6-144">Sertifikalar, Service Fabric’te bir küme ile uygulamalarının çeşitli yönlerini güvenli hale getirmek üzere kimlik doğrulaması ve şifreleme sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="287c6-144">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="287c6-145">Sertifikaların Service Fabric’te kullanılmasıyla ilgili daha fazla bilgi için bkz. [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="287c6-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="287c6-146">Azure Active Directory kullanarak kullanıcı kimlik doğrulamasını etkinleştirmek veya uygulama güvenliği için sertifika ayarlamak üzere [bir Resource Manager şablonundan küme oluşturun](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="287c6-146">To enable user authentication using Azure Active Directory or to set up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="287c6-147">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-147">Select **OK**.</span></span>

8. <span data-ttu-id="287c6-148">Özeti gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="287c6-148">Review the summary.</span></span>  <span data-ttu-id="287c6-149">Girdiğiniz ayarlarla oluşturulmuş bir Resource Manager şablonu indirmek isterseniz, **Şablon ve parametreleri indir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="287c6-149">If you'd like to download a Resource Manager template built from the settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="287c6-150">**Oluştur**’u seçerek kümeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="287c6-150">Select **Create** to create the cluster.</span></span>

    <span data-ttu-id="287c6-151">Oluşturma işleminin ilerleme durumunu bildirimler bölümünden görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-151">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="287c6-152">(Ekranınızın sağ üst köşesindeki durum çubuğunun yanında bulunan "Zil" simgesine tıklayın.) Kümeyi oluştururken **Başlangıç Panosuna Sabitle**’ye tıkladıysanız, **Service Fabric Kümesi Dağıtılıyor** öğesinin **Başlangıç** panosuna sabitlendiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="287c6-152">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="287c6-153">Küme durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="287c6-153">View cluster status</span></span>
<span data-ttu-id="287c6-154">Kümeniz oluşturulduktan sonra, portaldaki **Genel Bakış** dikey penceresinden kümenizi inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-154">Once your cluster is created, you can inspect your cluster in the **Overview** blade in the portal.</span></span> <span data-ttu-id="287c6-155">Kümenin genel uç noktası ve bir Service Fabric Explorer bağlantısıyla birlikte kümenizin ayrıntılarını panoda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-155">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

![Küme durumu][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="287c6-157">Service Fabric Explorer’ı kullanarak kümeyi görselleştirme</span><span class="sxs-lookup"><span data-stu-id="287c6-157">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="287c6-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), kümenizi görselleştirmek ve uygulamaları yönetmek için iyi bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="287c6-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="287c6-159">Service Fabric Explorer, kümede çalışan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="287c6-159">Service Fabric Explorer is a service that runs in the cluster.</span></span>  <span data-ttu-id="287c6-160">Bir web tarayıcısı ile portaldaki kümeye **Genel Bakış** sayfasının **Service Fabric Explorer** bağlantısına tıklayarak bu hizmete erişin.</span><span class="sxs-lookup"><span data-stu-id="287c6-160">Access it using a web browser by clicking the **Service Fabric Explorer** link of the cluster **Overview** page in the portal.</span></span>  <span data-ttu-id="287c6-161">Ayrıca adresi doğrudan tarayıcıya girebilirsiniz: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="287c6-161">You can also enter the address directly into the browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="287c6-162">Küme panosu, kümenize uygulama ve düğüm durumunun özetini de içeren bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="287c6-162">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="287c6-163">Düğüm görünümü, kümenin fiziksel düzenini gösterir.</span><span class="sxs-lookup"><span data-stu-id="287c6-163">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="287c6-164">Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a><span data-ttu-id="287c6-166">PowerShell kullanarak kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="287c6-166">Connect to the cluster using PowerShell</span></span>
<span data-ttu-id="287c6-167">PowerShell ile bağlanarak kümenin çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-167">Verify that the cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="287c6-168">ServiceFabric PowerShell modülü, [Service Fabric SDK’sı](service-fabric-get-started.md) ile birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="287c6-168">The ServiceFabric PowerShell module is installed with the [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="287c6-169">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet’i, kümeyle bir bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="287c6-169">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="287c6-170">Bir kümeye bağlanmayla ilgili diğer örnekler için bkz. [Güvenli bir kümeye bağlanma](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="287c6-170">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="287c6-171">Kümeye bağlandıktan sonra, kümedeki düğümlerin listesini ve her bir düğümün durum bilgilerini görüntülemek için [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet’ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="287c6-171">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="287c6-172">Her düğüm için **HealthState** değerinin *OK* olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="287c6-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-the-cluster"></a><span data-ttu-id="287c6-173">Kümeyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="287c6-173">Remove the cluster</span></span>
<span data-ttu-id="287c6-174">Service Fabric kümesi, küme kaynağının yanı sıra diğer Azure kaynaklarından oluşur.</span><span class="sxs-lookup"><span data-stu-id="287c6-174">A Service Fabric cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="287c6-175">Bu nedenle, bir Service Fabric kümesini tamamen silmek için onu oluşturan tüm kaynakları da silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="287c6-175">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span> <span data-ttu-id="287c6-176">Kümeyi ve kullandığı tüm kaynakları silmenin en basit yolu, kaynak grubunun silinmesidir.</span><span class="sxs-lookup"><span data-stu-id="287c6-176">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> <span data-ttu-id="287c6-177">Bir kümeyi veya bir kaynak grubundaki bazı (tümü değil) kaynakları silmenin diğer yolları için bkz. [Küme silme](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="287c6-177">For other ways to delete a cluster or to delete some (but not all) the resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="287c6-178">Azure portalında bir kaynak grubunu silin:</span><span class="sxs-lookup"><span data-stu-id="287c6-178">Delete a resource group in the Azure portal:</span></span>
1. <span data-ttu-id="287c6-179">Silmek istediğiniz Service Fabric kümesine gidin.</span><span class="sxs-lookup"><span data-stu-id="287c6-179">Navigate to the Service Fabric cluster you want to delete.</span></span>
2. <span data-ttu-id="287c6-180">Küme temel bileşenleri sayfasında **Kaynak Grubu** adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-180">Click the **Resource Group** name on the cluster essentials page.</span></span>
3. <span data-ttu-id="287c6-181">**Kaynak Grubu Temel Bileşenleri** sayfasında **Kaynak grubunu sil**’e tıklayın ve bu sayfadaki yönergeleri izleyerek kaynak grubu silme işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-181">In the **Resource Group Essentials** page, click **Delete resource group** and follow the instructions on that page to complete the deletion of the resource group.</span></span>
    <span data-ttu-id="287c6-182">![Kaynak grubunu silme][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="287c6-182">![Delete the resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a><span data-ttu-id="287c6-183">Azure PowerShell'i kullanarak güvenli küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="287c6-183">Use Azure Powershell to deploy a secure cluster</span></span>
1. <span data-ttu-id="287c6-184">[Azure Powershell modülü sürüm 4.0 veya üzerini](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) makinenize indirin.</span><span class="sxs-lookup"><span data-stu-id="287c6-184">Download the [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="287c6-185">Bir PowerShell penceresi açıp aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="287c6-185">Open a Windows PowerShell window, Run the following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="287c6-186">Aşağıdakine benzer bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="287c6-186">You should see an output similar to the following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="287c6-188">Azure’da oturum açıp kümeyi oluşturmak istediğiniz aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="287c6-188">Login to Azure and Select the subscription to which you want to create the cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="287c6-189">Güvenli bir küme oluşturmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="287c6-189">Run the following command to now create a secure cluster.</span></span> <span data-ttu-id="287c6-190">Parametreleri özelleştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="287c6-190">Do not forget to customize the parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="287c6-191">Komutun tamamlanması 10 dakika ile 30 dakika arasında sürer ve bu süre sonunda aşağıdakine benzer bir çıktı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="287c6-191">The command can take anywhere from 10 minutes to 30 minutes to complete, at the end of it, you should get an output similar to the following.</span></span> <span data-ttu-id="287c6-192">Çıktıda, sertifikayla ilgili bilgiler, sertifikanın yüklendiği anahtar kasası ve sertifikanın kopyalandığı yerel klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="287c6-192">The output has information about the certificate, the KeyVault where it was uploaded to, and the local folder where the certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="287c6-194">Tüm çıktıyı kopyalayın ve daha sonra başvurulması gerekeceğinden bir metin dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="287c6-194">Copy the entire output and save to a text file as we need to refer to it.</span></span> <span data-ttu-id="287c6-195">Çıktıda aşağıdaki bilgileri not edin.</span><span class="sxs-lookup"><span data-stu-id="287c6-195">Make a note of the following information from the output.</span></span> 

    - <span data-ttu-id="287c6-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="287c6-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="287c6-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="287c6-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="287c6-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="287c6-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="287c6-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="287c6-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-the-certificate-on-your-local-machine"></a><span data-ttu-id="287c6-200">Sertifikayı yerel makinenize yükleme</span><span class="sxs-lookup"><span data-stu-id="287c6-200">Install the certificate on your local machine</span></span>
  
<span data-ttu-id="287c6-201">Kümeye bağlanmak için sertifikayı geçerli kullanıcının Kişisel (My) deposuna yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="287c6-201">To connect to the cluster, you need to install the certificate into the Personal (My) store of the current user.</span></span> 

<span data-ttu-id="287c6-202">Aşağıdaki PowerShell komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="287c6-202">Run the following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="287c6-203">Şimdi güvenli kümenize bağlanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="287c6-203">You are now ready to connect to your secure cluster.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="287c6-204">Güvenli bir kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="287c6-204">Connect to a secure cluster</span></span> 

<span data-ttu-id="287c6-205">Güvenli bir kümeye bağlanmak için aşağıdaki PowerShell komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="287c6-205">Run the following PowerShell command to connect to a secure cluster.</span></span> <span data-ttu-id="287c6-206">Sertifika ayrıntıları, kümeyi oluşturmak için kullanılan bir sertifikayla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="287c6-206">The certificate details must match a certificate that was used to set up the cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="287c6-207">Aşağıdaki örnekte, tamamlanmış parametreler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="287c6-207">The following example shows the completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="287c6-208">Bağlı olup olmadığınızı ve kümenin sağlıklı olup olmadığını denetlemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="287c6-208">Run the following command to check that you are connected and the cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a><span data-ttu-id="287c6-209">Uygulamalarınızı Visual Studio’dan kümenize yayımlama</span><span class="sxs-lookup"><span data-stu-id="287c6-209">Publish your apps to your cluster from Visual Studio</span></span>

<span data-ttu-id="287c6-210">Bir Azure kümesi oluşturduktan sonra, [Kümede yayımlama](service-fabric-publish-app-remote-cluster.md) belgesini izleyerek bu uygulamayı Visual Studio’dan kümeye yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="287c6-210">Now that you have set up an Azure cluster, you can publish your applications to it from Visual Studio by following the [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-the-cluster"></a><span data-ttu-id="287c6-211">Kümeyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="287c6-211">Remove the cluster</span></span>
<span data-ttu-id="287c6-212">Küme, küme kaynağının yanı sıra diğer Azure kaynaklarından oluşur.</span><span class="sxs-lookup"><span data-stu-id="287c6-212">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="287c6-213">Kümeyi ve kullandığı tüm kaynakları silmenin en basit yolu, kaynak grubunun silinmesidir.</span><span class="sxs-lookup"><span data-stu-id="287c6-213">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="287c6-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="287c6-214">Next steps</span></span>
<span data-ttu-id="287c6-215">Artık bir geliştirme kümesi ayarladığınıza göre aşağıdakileri deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="287c6-215">Now that you have set up a development cluster, try the following:</span></span>
* [<span data-ttu-id="287c6-216">Portalda güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="287c6-216">Create a secure cluster in the portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="287c6-217">Şablondan küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="287c6-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="287c6-218">PowerShell kullanarak uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="287c6-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
