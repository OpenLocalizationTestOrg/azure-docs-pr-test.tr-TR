---
title: "3 düğümü dağıtma küme Deis | Microsoft Docs"
description: "3 düğümü oluşturma bu makalede Azure Resource Manager şablonu kullanarak azure'da küme Deis"
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
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="6e4a0-103">3 düğümünü yapılandırmak ve dağıtmak Azure kümesinde Deis</span><span class="sxs-lookup"><span data-stu-id="6e4a0-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="6e4a0-104">Bu makalede, sağlama aracılığıyla anlatan bir [Deis](http://deis.io/) Azure kümede.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="6e4a0-105">Dağıtma ve bir örnek ölçeklendirme için gerekli sertifikaları oluşturmasına tüm adımlar kapsanmaktadır **Git** yeni sağlanan kümede uygulama.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="6e4a0-106">Aşağıdaki diyagramda, dağıtılan Sistem mimarisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="6e4a0-107">Küme kullanarak bir Sistem Yöneticisi yönetir araçları gibi Deis **deis** ve **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="6e4a0-108">Bağlantıları bağlantıları üye birine Küme düğümlerinde ileten bir Azure yük dengeleyici üzerinden kurulur.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="6e4a0-109">İstemcilerin erişim uygulamalar da yük dengeleyici aracılığıyla dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="6e4a0-110">Bu durumda, yük dengeleyici için trafiğini bir kümede barındırılan karşılık gelen Docker kapsayıcıları trafiği daha fazla routs yönlendirici kafes Deis.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Dağıtılan Desis küme mimarisi diyagramı](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="6e4a0-112">Aşağıdaki adımlarda size çalıştırmak için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="6e4a0-113">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-113">An active Azure subscription.</span></span> <span data-ttu-id="6e4a0-114">Yoksa, ücretsiz izi alma [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="6e4a0-115">Azure kaynak gruplarını kullanmak için iş veya Okul kimliği.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="6e4a0-116">Kişisel hesap ve bir Microsoft kimliğiyle günlük varsa, gerek [bir iş kimliği, kişisel sunudan oluşturma](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="6e4a0-117">Ya da--bağlı olarak istemci işletim sistemi [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya [Mac, Linux ve Windows için Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="6e4a0-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="6e4a0-119">OpenSSL gerekli sertifikaları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="6e4a0-120">Git istemci gibi [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="6e4a0-121">Örnek uygulamayı test etmek için de bir DNS sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="6e4a0-122">Herhangi bir DNS sunucuları veya joker karakter A kayıtlarını destekleyen Hizmetleri'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="6e4a0-123">Çalıştırmak için bir bilgisayar istemci araçları Deis.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="6e4a0-124">Yerel makine veya sanal makine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="6e4a0-125">Neredeyse her Linux dağıtım noktasında bu araçları çalıştırabilirsiniz ancak Ubuntu aşağıdaki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="6e4a0-126">Küme sağlama</span><span class="sxs-lookup"><span data-stu-id="6e4a0-126">Provision the cluster</span></span>
<span data-ttu-id="6e4a0-127">Bu bölümde, kullanacağınız bir [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) açık kaynak havuzu şablonu [azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="6e4a0-128">İlk olarak, şablonu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-128">First, you'll copy down the template.</span></span> <span data-ttu-id="6e4a0-129">Ardından, kimlik doğrulama için yeni bir SSH anahtar çifti oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="6e4a0-130">Ve daha sonra küme için yeni bir tanımlayıcı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="6e4a0-131">Ve son olarak, kabuk betiği veya PowerShell Betiği kümesi sağlamak için kullanmanız.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="6e4a0-132">Depoyu kopyalayın: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="6e4a0-133">Şablon klasöre gidin:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="6e4a0-134">SSH-keygen kullanarak yeni bir SSH anahtar çifti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="6e4a0-135">Yukarıdaki özel anahtarı kullanarak bir sertifika oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="6e4a0-136">Git [https://discovery.etcd.io/new](https://discovery.etcd.io/new) yeni bir küme belirteci şuna benzer görünen oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="6e4a0-137">Bu ücretsiz hizmeti benzersiz bir belirtecinden her CoreOS küme olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="6e4a0-138">Lütfen bakın [CoreOS belgelerine](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="6e4a0-139">Değiştirme **bulut config.yaml** varolan dosyaya **bulma** yeni belirteci ile belirteci:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="6e4a0-140">Değiştirme **azuredeploy-parameters.json** dosya: bir metin düzenleyicisinde 4. adımda oluşturduğunuz sertifika açın.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="6e4a0-141">Arasındaki tüm metni kopyalayın `----BEGIN CERTIFICATE-----` ve `-----END CERTIFICATE-----` içine **sshKeyData** parametresi (tüm satırbaşı karakterlerini Kaldır gerekir).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="6e4a0-142">Değiştirme **newStorageAccountName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="6e4a0-143">Bu VM OS diskler için depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="6e4a0-144">Bu hesap adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="6e4a0-145">Değiştirme **publicDomainName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="6e4a0-146">Bu yük dengeleyici genel IP ile ilişkili DNS adının bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="6e4a0-147">Son FQDN biçimini olacaktır *[Bu parametrenin değeri]*. *[Bölge]* . cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="6e4a0-148">Örneğin, ad deishbai32 belirtirseniz ve kaynak grubu, Batı ABD bölgesi dağıtılır, ardından deishbai32.westus.cloudapp.azure.com yük dengeleyiciye son FQDN olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="6e4a0-149">Parametre dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-149">Save the parameter file.</span></span> <span data-ttu-id="6e4a0-150">Ve ardından Azure PowerShell kullanarak küme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="6e4a0-151">veya Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="6e4a0-152">Kaynak grubu sağlandıktan sonra gruptaki tüm kaynakların Azure Klasik portalında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="6e4a0-153">Aşağıdaki ekran görüntüsünde gösterildiği gibi bir sanal ağ aynı kullanılabilirlik kümesine katılan üç VM'ler ile kaynak grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="6e4a0-154">Grup ilişkili bir ortak IP sahip bir yük dengeleyici de içerir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Klasik Azure portalı üzerinde sağlanan kaynak grubu](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="6e4a0-156">İstemci Yükleme</span><span class="sxs-lookup"><span data-stu-id="6e4a0-156">Install the client</span></span>
<span data-ttu-id="6e4a0-157">Gereksinim duyduğunuz **deisctl** denetlemek için küme Deis.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="6e4a0-158">Deisctl tüm küme düğümlerinde otomatik olarak yüklenir ancak ayrı bir yönetim makinede deisctl kullanmak iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="6e4a0-159">Ayrıca, tüm düğümler yalnızca özel IP adresleri yapılandırıldığından, düğüm makinelere bağlanmak için bir ortak IP sahip yük dengeleyici üzerinden tünel SSH kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="6e4a0-160">Fiziksel bir ayrı Ubuntu üzerinde deisctl ya da sanal makineyi ayarlama adımları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="6e4a0-161">Yükleme deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="6e4a0-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="6e4a0-162">Özel anahtarınızı ssh aracı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="6e4a0-163">Deisctl yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="6e4a0-164">Şablon 1, 2224 örneğine 2 ve 3 örneğine 2225 örnek 2223 eşleme gelen NAT kuralları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="6e4a0-165">Bu deisctl aracını kullanmak için artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="6e4a0-166">Klasik Azure portalı aşağıdaki kurallara inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-166">You can examine these rules on Azure classic portal:</span></span>

![Yük Dengeleyici NAT kuralları](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="6e4a0-168">Şu anda şablonu yalnızca 3 düğümlü kümeler destekler.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="6e4a0-169">Azure Resource Manager şablonu döngü sözdizimi desteklemiyor NAT kuralı tanımını uygulamasındaki bir sınırlama nedeniyle budur.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="6e4a0-170">Yükleme ve başlangıç platform Deis</span><span class="sxs-lookup"><span data-stu-id="6e4a0-170">Install and start the Deis platform</span></span>
<span data-ttu-id="6e4a0-171">Artık yükleme ve başlangıç deisctl kullanarak platform Deis:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="6e4a0-172">Platform başlatma biraz zaman alır (10 dakika kadar).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="6e4a0-173">Özellikle, oluşturucu hizmeti başlatılıyor uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="6e4a0-174">Ve bazen başarılı olması için birkaç denemeden sürer: işlemi askıda görünüyorsa, yazmayı deneyin `ctrl+c` komutu yürütme ayırın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="6e4a0-175">Kullanabileceğiniz `deisctl list` tüm hizmetlerin çalışıp çalışmadığını doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-175">You can use `deisctl list` to verify if all services are running:</span></span>

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

<span data-ttu-id="6e4a0-176">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6e4a0-176">Congratulations!</span></span> <span data-ttu-id="6e4a0-177">Çalışan bir olduğuna artık Azure üzerinde clsuter Deis!</span><span class="sxs-lookup"><span data-stu-id="6e4a0-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="6e4a0-178">Ardından, şimdi örnek eylem kümede görmek için Git uygulama dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="6e4a0-179">Dağıtma ve Hello World uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="6e4a0-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="6e4a0-180">Aşağıdaki adımlar, bir "Hello World" dağıtma gösterir küme uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="6e4a0-181">Adımlar dayanır [belgelerine Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="6e4a0-182">Yönlendirme kafes düzgün çalışması bir joker karakter A kaydı yük dengeleyici genel IP için işaret eden bir etki alanınız için sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="6e4a0-183">Aşağıdaki ekran görüntüsü bir örnek etki alanı kaydı için A kaydı üzerinde GoDaddy gösterir:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A kaydı](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="6e4a0-185">Yükleme deis:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="6e4a0-186">Yeni bir SSH anahtarı oluşturun ve sonra GitHub için ortak anahtarı ekleyin (doğal olarak, aynı zamanda mevcut anahtarlarınızı yeniden kullanabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="6e4a0-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="6e4a0-187">Yeni bir SSH anahtar çifti oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="6e4a0-188">İd_rsa.pub veya tercih ettiğiniz ortak anahtar için GitHub ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="6e4a0-189">Bu, SSH anahtarları yapılandırma ekranında eklemek SSH anahtar düğmesini kullanarak yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub anahtarı](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="6e4a0-191">Yeni bir kullanıcı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="6e4a0-192">SSH anahtarı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="6e4a0-193">Bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="6e4a0-194">
8.Git itme, birkaç dakika sürer oluşturulan ve dağıtılan, Docker görüntüleri tetikler.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="6e4a0-195">My deneyimlerden bazen, adım 10 (özel deponuza Pushing görüntü) kilitlenebilir.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="6e4a0-196">Bu gerçekleştiğinde, işlemi durdurmak, kullanarak uygulamayı kaldırma ' uygulamaları deis: – a destroy <application name> ` to remove the application and try again. You can use `apps:list deis' uygulamanızı adını öğrenmek için.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="6e4a0-197">Her şeyi işe yararsa komut çıktılarını sonunda aşağıdaki gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="6e4a0-198">Uygulama çalışıp çalışmadığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="6e4a0-199">Şunu görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="6e4a0-200">Ölçek uygulama 3 örnekleri:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="6e4a0-201">Kullanabileceğiniz isteğe bağlı olarak, uygulamanızın ayrıntılarını incelemek için bilgi deis.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="6e4a0-202">Aşağıdaki çıktıları my uygulaması dağıtımından şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-202">The following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="6e4a0-203">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6e4a0-203">Next Steps</span></span>
<span data-ttu-id="6e4a0-204">Yeni bir sağlamak için tüm adımları gitti bu makalede Azure Resource Manager şablonu kullanarak azure'da küme Deis.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="6e4a0-205">Şablonu, Yük Dengeleme dağıtılan uygulamalar için yanı sıra bağlantıları tooling içinde artıklık destekler.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="6e4a0-206">Genel IP'ler değerli genel IP kaynakları kaydeder ve uygulamalarını barındırmak için daha güvenli bir ortam sağlayan üye düğümleri kullanarak şablonu de önler.</span><span class="sxs-lookup"><span data-stu-id="6e4a0-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="6e4a0-207">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="6e4a0-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="6e4a0-208">[Azure Resource Manager'a genel bakış][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="6e4a0-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="6e4a0-209">[Azure CLI kullanma][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="6e4a0-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="6e4a0-210">[Azure Resource Manager ile Azure PowerShell'i kullanma][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="6e4a0-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
