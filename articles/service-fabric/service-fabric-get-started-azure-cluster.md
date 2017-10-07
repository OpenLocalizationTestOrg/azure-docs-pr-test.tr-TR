---
title: "Azure Service Fabric kümesi aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="ecf2d-103">Azure’da ilk Service Fabric kümenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf2d-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="ecf2d-104">[Service Fabric kümesi](service-fabric-deploy-anywhere.md), mikro hizmetlerin dağıtılıp yönetildiği, ağa bağlı bir sanal veya fiziksel makine kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="ecf2d-105">Bu hızlı başlangıç toocreate hello Windows veya Linux çalıştıran beş düğümlü bir küme, yardımcı [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) veya [Azure portal](http://portal.azure.com) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="ecf2d-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="ecf2d-107">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf2d-107">Use hello Azure portal</span></span>

<span data-ttu-id="ecf2d-108">Azure Portalı ' toohello oturum [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ecf2d-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="ecf2d-109">Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf2d-109">Create hello cluster</span></span>

1. <span data-ttu-id="ecf2d-110">Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="ecf2d-111">Seçin **işlem** hello gelen **yeni** dikey ve ardından **Service Fabric kümesi** hello gelen **işlem** dikey.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="ecf2d-112">Service Fabric Hello dolgu **Temelleri** formu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="ecf2d-113">İçin **işletim sistemi**seçin Windows veya Linux istediğiniz küme düğümleri toorun hello hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="ecf2d-114">Merhaba kullanıcı adı ve parola buraya girilen toohello sanal makinede kullanılan toolog olur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="ecf2d-115">**Kaynak grubu** için yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="ecf2d-116">Kaynak grubu, Azure kaynaklarının oluşturulup toplu olarak yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="ecf2d-117">İşlem tamamlandığında **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-117">When complete, click **OK**.</span></span>

    ![Küme kurulumu çıktısı][cluster-setup-basics]

4. <span data-ttu-id="ecf2d-119">Merhaba dolgu **küme yapılandırması** formu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="ecf2d-120">**Düğüm türü sayısı** için "1" değerini girin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="ecf2d-121">Seçin **düğüm türü 1 (birincil)** ve hello doldurun **düğüm türü yapılandırması** formu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="ecf2d-122">Düğüm türü adı girin ve hello [dayanıklılık katmanı](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) çok "Bronz."</span><span class="sxs-lookup"><span data-stu-id="ecf2d-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="ecf2d-123">VM boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-123">Select a VM size.</span></span>

    <span data-ttu-id="ecf2d-124">Bu tür VM'ler için diğer ayarları hello ve hello VM boyutu, VM'ler, özel uç noktaları, düğüm türleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="ecf2d-125">Tanımlanan her bir düğüm türünde kullanılan toodeploy ve yönetilen sanal makineleri bir küme olarak olan ayrı sanal makine ölçek kümesi olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="ecf2d-126">Her düğüm türünün ölçeği birbirinden bağımsız olarak artırılabilir veya azaltılabilir, her düğüm türünde farklı bağlantı noktası kümeleri açık olabilir ve farklı kapasite ölçümleri yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="ecf2d-127">Merhaba ilk ya da birincil düğüm türü burada Service Fabric Sistem Hizmetleri barındırılır ve beş veya daha fazla VM olmalıdır ' dir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="ecf2d-128">Herhangi bir üretim dağıtımı için [kapsite planlaması](service-fabric-cluster-capacity.md) önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="ecf2d-129">Ancak, bu hızlı başlangıçta uygulama çalıştırmadığınız için bir *DS1_v2 Standart* VM boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="ecf2d-130">Merhaba "Gümüş" seçin [güvenilirlik katmanı](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) ve bir ilk sanal makine ölçek kümesi kapasitesi 5.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="ecf2d-131">Merhaba küme üzerinde çalışan uygulamalar ile bağlantı kurabilmesi için özel uç noktaları hello Azure yük dengeleyici bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="ecf2d-132">Yukarı bağlantı noktası 80 ve 8172 "80, 8172" tooopen girin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="ecf2d-133">Merhaba denetleme **Gelişmiş ayarları Yapılandır** TCP/HTTP yönetim uç noktaları, uygulama bağlantı noktası aralıkları özelleştirmek için kullanılan kutusunu [kısıtlamalarından](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), ve [kapasitesi Özellikler](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ecf2d-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="ecf2d-134">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-134">Select **OK**.</span></span>

6. <span data-ttu-id="ecf2d-135">Merhaba, **küme yapılandırması** formunda, ayarlamak **tanılama** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="ecf2d-136">Bu Hızlı Başlangıç, tooenter herhangi gerekmez [ayarı doku](service-fabric-cluster-fabric-settings.md) özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="ecf2d-137">İçinde **Fabric sürümü**seçin **otomatik** yükseltme modu böylece Microsoft hello küme çalışan hello doku kodu hello sürümünü otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="ecf2d-138">Başlangıç modu çok ayarlamak**el ile** çok istiyorsanız[desteklenen bir sürüm seçin](service-fabric-cluster-upgrade.md) tooupgrade için.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Düğüm türü yapılandırması][node-type-config]

    <span data-ttu-id="ecf2d-140">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-140">Select **OK**.</span></span>

7. <span data-ttu-id="ecf2d-141">Merhaba dolgu **güvenlik** formu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="ecf2d-142">Bu hızlı başlangıç için **Güvenli olmayan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="ecf2d-143">Yüksek oranda olan herkes anonim olarak tooan güvenli olmayan küme bağlanabilir ve yönetim işlemleri beri toocreate üretim iş yükleri için güvenli bir küme ancak önerilir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="ecf2d-144">Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="ecf2d-145">Sertifikaların Service Fabric’te kullanılmasıyla ilgili daha fazla bilgi için bkz. [Service Fabric kümesi güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="ecf2d-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="ecf2d-146">Azure Active Directory veya sertifikaları kurma tooset uygulama güvenliği için kullanarak tooenable kullanıcı kimlik doğrulaması [bir Resource Manager şablonu bir küme oluşturmak](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ecf2d-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="ecf2d-147">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-147">Select **OK**.</span></span>

8. <span data-ttu-id="ecf2d-148">Gözden geçirme hello Özet.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-148">Review hello summary.</span></span>  <span data-ttu-id="ecf2d-149">Toodownload isterseniz hello ayarlarından yerleşik bir Resource Manager şablonu girdiğiniz, seçin **karşıdan şablonu ve parametre**.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="ecf2d-150">Seçin **oluşturma** toocreate hello küme.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="ecf2d-151">Merhaba oluşturma ilerlemesi hello Bildirimlerde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="ecf2d-152">(Hello durum çubuğu, ekranınızın sağ üst hello en yakın hello "zil" simgesine tıklayın.) Tıkladıysanız **PIN tooStartboard** gördüğünüz hello küme oluştururken **Service Fabric kümesi dağıtma** toohello sabitlenmiş **Başlat** Panosu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="ecf2d-153">Küme durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ecf2d-153">View cluster status</span></span>
<span data-ttu-id="ecf2d-154">Kümenizi oluşturduktan sonra kümenizde hello inceleyebilirsiniz **genel bakış** dikey penceresinde hello portal.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="ecf2d-155">Şimdi kümenizi hello kümenin ortak uç noktası ve bağlantı tooService Fabric Explorer dahil olmak üzere hello panosundaki hello ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Küme durumu][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ecf2d-157">Service Fabric explorer'ı kullanarak hello küme Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="ecf2d-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="ecf2d-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), kümenizi görselleştirmek ve uygulamaları yönetmek için iyi bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="ecf2d-159">Service Fabric Explorer hello kümede çalışan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="ecf2d-160">Merhaba tıklayarak bir web tarayıcısı kullanarak erişim **Service Fabric Explorer** bağlantı hello kümesinin **genel bakış** hello portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="ecf2d-161">Merhaba adresini doğrudan hello tarayıcısına girebilirsiniz: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Gezgini](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="ecf2d-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="ecf2d-162">Merhaba küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="ecf2d-163">Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="ecf2d-164">Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="ecf2d-166">PowerShell kullanarak toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="ecf2d-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="ecf2d-167">Bu hello küme PowerShell kullanarak bağlanarak çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="ecf2d-168">Merhaba ServiceFabric PowerShell modülü ile Merhaba yüklü [Service Fabric SDK](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ecf2d-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="ecf2d-169">Merhaba [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i bir bağlantı toohello kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="ecf2d-170">Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) bağlanan tooa kümenin diğer örnekler için.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="ecf2d-171">Bağlantı toohello küme sonra hello kullanmak [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello küme ve durum bilgilerini her düğüm için düğüm listesi.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="ecf2d-172">Her düğüm için **HealthState** değerinin *OK* olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-172">**HealthState** should be *OK* for each node.</span></span>

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

### <a name="remove-hello-cluster"></a><span data-ttu-id="ecf2d-173">Merhaba küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="ecf2d-173">Remove hello cluster</span></span>
<span data-ttu-id="ecf2d-174">Service Fabric kümesi diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ecf2d-175">Toocompletely silmek için Service Fabric kümesi tüm kaynakları, yapılan hello toodelete de olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="ecf2d-176">Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="ecf2d-177">Diğer yolları toodelete bir küme veya toodelete bazı (ancak tüm) hello kaynakları bir kaynak grubunda görmek için [bir küme silme](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="ecf2d-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="ecf2d-178">Hello Azure portalında bir kaynak grubunda Sil:</span><span class="sxs-lookup"><span data-stu-id="ecf2d-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="ecf2d-179">Toodelete istediğiniz toohello Service Fabric kümesi gidin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="ecf2d-180">Merhaba tıklatın **kaynak grubu** hello küme essentials sayfasında adı.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="ecf2d-181">Merhaba, **kaynak grubu Essentials** sayfasında, **kaynak grubu Sil** ve bu sayfa toocomplete hello hello kaynak grubunun silinmesi üzerinde hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="ecf2d-182">![Merhaba kaynak grubunu silme][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="ecf2d-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="ecf2d-183">Azure Powershell toodeploy güvenli bir küme kullanın</span><span class="sxs-lookup"><span data-stu-id="ecf2d-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="ecf2d-184">Merhaba karşıdan [Azure Powershell modülü sürüm 4.0 veya üstü](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) makinenizde.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="ecf2d-185">Çalışma hello komut aşağıdaki gibi Windows PowerShell penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="ecf2d-186">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="ecf2d-188">Oturum açma tooAzure ve toocreate hello kümenin istediğinizi seçin hello abonelik toowhich</span><span class="sxs-lookup"><span data-stu-id="ecf2d-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="ecf2d-189">Komut toonow aşağıdaki çalışma hello güvenli bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="ecf2d-190">Toocustomize hello parametreleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="ecf2d-191">Merhaba komutu herhangi bir yere hello ucunda 10 dakika too30 dakika toocomplete gelen alabilir, bir çıktı benzer toohello aşağıdaki almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="ecf2d-192">Merhaba çıktı hello sertifikası, hello olduğu için yüklenen KeyVault hakkında bilgi sahiptir ve burada hello sertifika kopyalanır yerel klasör hello.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="ecf2d-194">Merhaba tüm çıktı kopyalayın ve toorefer tooit ihtiyacımız gibi tooa metin dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="ecf2d-195">Merhaba çıktısını bilgisinden hello not edin.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="ecf2d-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="ecf2d-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="ecf2d-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="ecf2d-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="ecf2d-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="ecf2d-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="ecf2d-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="ecf2d-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="ecf2d-200">Merhaba sertifika yerel makinenize yükleyin</span><span class="sxs-lookup"><span data-stu-id="ecf2d-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="ecf2d-201">tooconnect toohello küme hello geçerli kullanıcının (My) kişisel deposuna hello tooinstall hello sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="ecf2d-202">PowerShell aşağıdaki hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ecf2d-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="ecf2d-203">Hazır tooconnect tooyour güvenli küme sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="ecf2d-204">Tooa güvenli kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="ecf2d-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="ecf2d-205">PowerShell komut tooconnect tooa güvenli küme aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="ecf2d-206">Merhaba sertifika ayrıntıları kullanılan tooset hello kümesi olan bir sertifika ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="ecf2d-207">Aşağıdaki örnekte gösterildiği hello hello parametreleri tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="ecf2d-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ecf2d-208">Bağlı ve hello küme sağlıklı olduğundan komut toocheck aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="ecf2d-209">Visual Studio, uygulamaları tooyour kümenizden yayımlama</span><span class="sxs-lookup"><span data-stu-id="ecf2d-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="ecf2d-210">Bir Azure küme ayarlama, Visual Studio'dan uygulamaları tooit aşağıdaki hello tarafından yayımlayabilirsiniz [Yayımla tooan küme](service-fabric-publish-app-remote-cluster.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="ecf2d-211">Merhaba küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="ecf2d-211">Remove hello cluster</span></span>
<span data-ttu-id="ecf2d-212">Bir küme diğer Azure kaynaklarını toohello küme kaynağı kendisi ayrıca oluşur.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ecf2d-213">Merhaba en basit yolu toodelete hello küme içereceği tükettiği tüm hello kaynakları ise toodelete hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ecf2d-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="ecf2d-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ecf2d-214">Next steps</span></span>
<span data-ttu-id="ecf2d-215">Geliştirme küme ayarlama, hello aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="ecf2d-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="ecf2d-216">Merhaba Portalı'nda güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf2d-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="ecf2d-217">Şablondan küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecf2d-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="ecf2d-218">PowerShell kullanarak uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="ecf2d-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
