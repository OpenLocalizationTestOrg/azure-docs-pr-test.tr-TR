---
title: "3 düğümü Deis aaaDeploy küme | Microsoft Docs"
description: "Bu makalede nasıl toocreate 3 düğümü Deis bir Azure Resource Manager şablonu kullanarak azure'da küme"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="079f4-103">3 düğümünü yapılandırmak ve dağıtmak Azure kümesinde Deis</span><span class="sxs-lookup"><span data-stu-id="079f4-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="079f4-104">Bu makalede, sağlama aracılığıyla anlatan bir [Deis](http://deis.io/) Azure kümede.</span><span class="sxs-lookup"><span data-stu-id="079f4-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="079f4-105">Merhaba gerekli sertifikaları toodeploying oluşturma ve bir örnek ölçeklendirme hello adımların tümünü kapsayan **Git** hello yeni sağlanan kümede uygulama.</span><span class="sxs-lookup"><span data-stu-id="079f4-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="079f4-106">Merhaba Aşağıdaki diyagramda dağıtılan hello sistemin hello mimarisi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="079f4-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="079f4-107">Küme hello kullanarak bir Sistem Yöneticisi yönetir araçları gibi Deis **deis** ve **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="079f4-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="079f4-108">Bağlantıları hello bağlantıları tooone hello üyesinin hello küme düğümlerinde ileten bir Azure yük dengeleyici üzerinden kurulur.</span><span class="sxs-lookup"><span data-stu-id="079f4-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="079f4-109">Merhaba istemcileri erişim uygulamalar da hello yük dengeleyici aracılığıyla dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="079f4-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="079f4-110">Bu durumda, hello yük dengeleyici hello trafiği tooa iletir daha fazla trafik toocorresponding Docker kapsayıcıları hello kümede barındırılan routs yönlendirici kafes Deis.</span><span class="sxs-lookup"><span data-stu-id="079f4-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Dağıtılan Desis küme mimarisi diyagramı](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="079f4-112">Aşağıdaki adımları hello aracılığıyla sipariş toorun ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="079f4-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="079f4-113">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="079f4-113">An active Azure subscription.</span></span> <span data-ttu-id="079f4-114">Yoksa, ücretsiz izi alma [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="079f4-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="079f4-115">Bir iş veya Okul kimlik toouse Azure kaynak gruplarını.</span><span class="sxs-lookup"><span data-stu-id="079f4-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="079f4-116">Kişisel hesap ve bir Microsoft kimliğiyle günlük varsa, çok ihtiyacınız[bir iş kimliği, kişisel sunudan oluşturma](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="079f4-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="079f4-117">Ya da--istemci işletim sistemine bağlı olarak--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello [Mac, Linux ve Windows için Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="079f4-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="079f4-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="079f4-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="079f4-119">OpenSSL kullanılan toogenerate hello gerekli sertifikaları olur.</span><span class="sxs-lookup"><span data-stu-id="079f4-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="079f4-120">Git istemci gibi [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="079f4-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="079f4-121">tootest Merhaba örnek uygulaması, bir DNS sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="079f4-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="079f4-122">Herhangi bir DNS sunucuları veya joker karakter A kayıtlarını destekleyen Hizmetleri'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079f4-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="079f4-123">Bir bilgisayar toorun istemci araçları Deis.</span><span class="sxs-lookup"><span data-stu-id="079f4-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="079f4-124">Yerel makine veya sanal makine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079f4-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="079f4-125">Neredeyse her Linux dağıtım noktasında bu araçları çalıştırabilirsiniz ancak hello aşağıdaki yönergeleri kullanın Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="079f4-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="079f4-126">Sağlama hello küme</span><span class="sxs-lookup"><span data-stu-id="079f4-126">Provision hello cluster</span></span>
<span data-ttu-id="079f4-127">Bu bölümde, kullanacağınız bir [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) hello açık kaynak havuzu şablonu [azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="079f4-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="079f4-128">İlk olarak, hello şablonu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="079f4-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="079f4-129">Ardından, kimlik doğrulama için yeni bir SSH anahtar çifti oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="079f4-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="079f4-130">Ve daha sonra küme için yeni bir tanımlayıcı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="079f4-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="079f4-131">Ve son olarak, hello Kabuk betiği veya hello PowerShell komut dosyası tooprovision hello küme kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="079f4-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="079f4-132">Kopya hello deposu: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="079f4-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="079f4-133">Toohello şablon klasöre gidin:</span><span class="sxs-lookup"><span data-stu-id="079f4-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="079f4-134">SSH-keygen kullanarak yeni bir SSH anahtar çifti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="079f4-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="079f4-135">Özel anahtarı yukarıda Hello kullanarak bir sertifika oluşturun:</span><span class="sxs-lookup"><span data-stu-id="079f4-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="079f4-136">Çok Git[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate yeni bir küme belirteç görünen şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="079f4-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="079f4-137">Her CoreOS küme toohave bu ücretsiz hizmetinden benzersiz bir belirteç gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="079f4-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="079f4-138">Lütfen bakın [CoreOS belgelerine](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="079f4-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="079f4-139">Merhaba değiştirme **bulut config.yaml** tooreplace hello varolan dosya **bulma** hello yeni belirteci ile belirteci:</span><span class="sxs-lookup"><span data-stu-id="079f4-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="079f4-140">Merhaba değiştirme **azuredeploy-parameters.json** dosya: bir metin düzenleyicisinde 4. adımda oluşturduğunuz açık hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="079f4-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="079f4-141">Arasındaki tüm metni kopyalayın `----BEGIN CERTIFICATE-----` ve `-----END CERTIFICATE-----` hello içine **sshKeyData** (gerekir tooremove tüm satırbaşı karakterlerini) parametre.</span><span class="sxs-lookup"><span data-stu-id="079f4-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="079f4-142">Merhaba değiştirme **newStorageAccountName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="079f4-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="079f4-143">VM OS diskler için depolama hesabı hello budur.</span><span class="sxs-lookup"><span data-stu-id="079f4-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="079f4-144">Bu hesap adı toobe genel benzersiz sahiptir.</span><span class="sxs-lookup"><span data-stu-id="079f4-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="079f4-145">Merhaba değiştirme **publicDomainName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="079f4-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="079f4-146">Bu hello yük dengeleyici genel IP ile ilişkili hello DNS adının bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="079f4-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="079f4-147">Merhaba son FQDN hello biçimi olacaktır *[Bu parametrenin değeri]*. *[Bölge]* . cloudapp.azure.com. Örneğin, deishbai32 hello adı belirtin ve hello kaynak grubu dağıtılan toohello Batı ABD bölgesi sonra hello son ise FQDN tooyour yük dengeleyici deishbai32.westus.cloudapp.azure.com olabilir.</span><span class="sxs-lookup"><span data-stu-id="079f4-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="079f4-148">Merhaba parametre dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="079f4-148">Save hello parameter file.</span></span> <span data-ttu-id="079f4-149">Ve ardından Azure PowerShell kullanarak hello küme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="079f4-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="079f4-150">veya Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="079f4-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="079f4-151">Merhaba kaynak grubu sağlandıktan sonra Azure Klasik portalında hello gruptaki tüm hello kaynakların görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079f4-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="079f4-152">Aşağıdaki ekran, hello hello kaynak grubu içeren bir sanal ağ üç VM'ler ile gösterildiği gibi toohello birleştirilir aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="079f4-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="079f4-153">Merhaba grubunun ilişkili bir ortak IP sahip bir yük dengeleyici de içerir.</span><span class="sxs-lookup"><span data-stu-id="079f4-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Klasik Azure portalı üzerinde Hello sağlanan kaynak grubu](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="079f4-155">Merhaba istemcisini yükleme</span><span class="sxs-lookup"><span data-stu-id="079f4-155">Install hello client</span></span>
<span data-ttu-id="079f4-156">Gereksinim duyduğunuz **deisctl** toocontrol, küme Deis.</span><span class="sxs-lookup"><span data-stu-id="079f4-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="079f4-157">Deisctl tüm hello küme düğümlerinde otomatik olarak yüklenir ancak ayrı bir yönetim makinede iyi bir uygulama toouse deisctl var.</span><span class="sxs-lookup"><span data-stu-id="079f4-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="079f4-158">Ayrıca, tüm düğümler yalnızca özel IP adresleriyle yapılandırılmış olmadığından toouse tooconnect toohello düğümü makineler ortak bir IP hello yük dengeleyici ile SSH tünel gerekir.</span><span class="sxs-lookup"><span data-stu-id="079f4-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="079f4-159">Merhaba aşağıdaki deisctl ayrı bir Ubuntu fiziksel veya sanal makine kurma hello adımlardır.</span><span class="sxs-lookup"><span data-stu-id="079f4-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="079f4-160">Yükleme deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="079f4-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="079f4-161">Özel anahtar toossh aracınızı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="079f4-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="079f4-162">Deisctl yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="079f4-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="079f4-163">Merhaba şablonu tanımlar 2223 tooinstance 1, eşleme gelen NAT kuralları 2224 tooinstance 2 ve 3 2225 tooinstance.</span><span class="sxs-lookup"><span data-stu-id="079f4-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="079f4-164">Bu, hello deisctl aracını kullanmak için artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="079f4-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="079f4-165">Klasik Azure portalı aşağıdaki kurallara inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="079f4-165">You can examine these rules on Azure classic portal:</span></span>

![Merhaba yük dengeleyicisi NAT kuralları](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="079f4-167">Şu anda hello şablonu yalnızca 3 düğümlü kümeler destekler.</span><span class="sxs-lookup"><span data-stu-id="079f4-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="079f4-168">Azure Resource Manager şablonu döngü sözdizimi desteklemiyor NAT kuralı tanımını uygulamasındaki bir sınırlama nedeniyle budur.</span><span class="sxs-lookup"><span data-stu-id="079f4-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="079f4-169">Yükleme ve hello Başlat platform Deis</span><span class="sxs-lookup"><span data-stu-id="079f4-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="079f4-170">Deisctl tooinstall kullanın ve hello Başlat artık platform Deis:</span><span class="sxs-lookup"><span data-stu-id="079f4-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="079f4-171">Başlangıç hello platform biraz zaman alır (10 dakika kadar).</span><span class="sxs-lookup"><span data-stu-id="079f4-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="079f4-172">Özellikle, hello Oluşturucu hizmeti başlatılıyor uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="079f4-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="079f4-173">Ve bazen birkaç denemeden toosucceed sürer: hello işlemi toohang görünüyorsa, yazmayı deneyin `ctrl+c` toobreak yürütülmesi hello komutu ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="079f4-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="079f4-174">Kullanabileceğiniz `deisctl list` tüm hizmetleri çalıştırılıyorsa tooverify:</span><span class="sxs-lookup"><span data-stu-id="079f4-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="079f4-175">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="079f4-175">Congratulations!</span></span> <span data-ttu-id="079f4-176">Çalışan bir olduğuna artık Azure üzerinde clsuter Deis!</span><span class="sxs-lookup"><span data-stu-id="079f4-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="079f4-177">Ardından, şimdi örnek Git uygulama toosee hello eylem kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="079f4-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="079f4-178">Dağıtma ve Hello World uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="079f4-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="079f4-179">Merhaba aşağıdaki adımları nasıl toodeploy "Hello World" Git Göster uygulama toohello kümesi.</span><span class="sxs-lookup"><span data-stu-id="079f4-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="079f4-180">Merhaba adımları temel [belgelerine Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="079f4-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="079f4-181">Merhaba yönlendirme kafes toowork için düzgün şekilde hello yük dengeleyicinin genel IP toohello işaret eden etki alanınız için toohave bir joker karakter A kaydı gerekir.</span><span class="sxs-lookup"><span data-stu-id="079f4-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="079f4-182">Merhaba aşağıdaki ekran görüntüsü bir örnek etki alanı kaydı için hello A kaydı üzerinde GoDaddy gösterir:</span><span class="sxs-lookup"><span data-stu-id="079f4-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A kaydı](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="079f4-184">Yükleme deis:</span><span class="sxs-lookup"><span data-stu-id="079f4-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="079f4-185">Yeni bir SSH anahtarı oluşturun ve sonra hello ortak anahtar tooGitHub ekleyin (doğal olarak, aynı zamanda mevcut anahtarlarınızı yeniden kullanabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="079f4-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="079f4-186">Yeni bir SSH anahtar çifti, toocreate kullanın:</span><span class="sxs-lookup"><span data-stu-id="079f4-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="079f4-187">İd_rsa.pub veya tercih ettiğiniz, tooGitHub hello ortak anahtarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="079f4-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="079f4-188">Bu, SSH anahtarları yapılandırma ekranında hello eklemek SSH anahtar düğmesini kullanarak yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="079f4-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub anahtarı](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="079f4-190">Yeni bir kullanıcı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="079f4-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="079f4-191">Merhaba SSH anahtarını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="079f4-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="079f4-192">Bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="079f4-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="079f4-193">
8.Merhaba git itme, birkaç dakika sürer oluşturulan ve dağıtılan, Docker görüntüleri toobe tetikler.</span><span class="sxs-lookup"><span data-stu-id="079f4-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="079f4-194">My deneyimlerden bazen, adım 10 (Pushing görüntü tooprivate depo) kilitlenebilir.</span><span class="sxs-lookup"><span data-stu-id="079f4-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="079f4-195">Bu gerçekleştiğinde, hello işlemi durdurabilirsiniz Kaldır hello kullanılarak uygulama ' uygulamaları deis: – a destroy <application name> ` tooremove hello application and try again. You can use `apps:list deis' toofind uygulamanızın hello adı çıkışı.</span><span class="sxs-lookup"><span data-stu-id="079f4-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="079f4-196">Her şeyi işe yararsa komut çıktılarını hello sonunda hello aşağıdaki gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="079f4-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="079f4-197">Merhaba uygulaması çalışıp çalışmadığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="079f4-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="079f4-198">Şunu görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="079f4-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="079f4-199">Ölçek hello uygulama too3 örnekleri:</span><span class="sxs-lookup"><span data-stu-id="079f4-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="079f4-200">İsteğe bağlı olarak kullanabileceğiniz bilgi tooexamine Ayrıntılar, uygulamanızın deis.</span><span class="sxs-lookup"><span data-stu-id="079f4-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="079f4-201">Merhaba aşağıdaki çıktıları my uygulaması dağıtımından şunlardır:</span><span class="sxs-lookup"><span data-stu-id="079f4-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="079f4-202">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="079f4-202">Next Steps</span></span>
<span data-ttu-id="079f4-203">Yeni bir Deis tüm hello adımları tooprovision gitti bu makalede Azure Resource Manager şablonu kullanarak azure'da küme.</span><span class="sxs-lookup"><span data-stu-id="079f4-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="079f4-204">Merhaba şablonu Yük Dengeleme dağıtılan uygulamalar için yanı sıra bağlantıları tooling içinde artıklık destekler.</span><span class="sxs-lookup"><span data-stu-id="079f4-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="079f4-205">Genel IP'ler değerli genel IP kaynakları kaydeder ve toohost uygulamaları daha güvenli bir ortam sağlayan üye düğümlerinde kullanarak Hello şablon de önler.</span><span class="sxs-lookup"><span data-stu-id="079f4-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="079f4-206">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="079f4-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="079f4-207">[Azure Resource Manager'a genel bakış][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="079f4-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="079f4-208">[Nasıl toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="079f4-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="079f4-209">[Azure Resource Manager ile Azure PowerShell'i kullanma][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="079f4-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
