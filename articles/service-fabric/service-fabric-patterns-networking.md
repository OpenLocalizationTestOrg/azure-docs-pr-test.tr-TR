---
title: "Azure Service Fabric için aaaNetworking desenleri | Microsoft Docs"
description: "Ortak ağ desenler için Service Fabric açıklar ve nasıl toocreate Azure ağ özelliklerini kullanarak bir küme."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="c46c7-103">Service Fabric ağ desenleri</span><span class="sxs-lookup"><span data-stu-id="c46c7-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="c46c7-104">Azure Service Fabric kümesi Azure diğer ağ özelliklerini ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="c46c7-105">Bu makalede, nasıl toocreate özellikler aşağıdaki bu kullanım hello kümeleri gösteriyoruz:</span><span class="sxs-lookup"><span data-stu-id="c46c7-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="c46c7-106">Var olan sanal ağ veya alt ağ</span><span class="sxs-lookup"><span data-stu-id="c46c7-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="c46c7-107">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="c46c7-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="c46c7-108">Yalnızca dahili yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c46c7-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="c46c7-109">İç ve dış yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c46c7-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="c46c7-110">Service Fabric standart sanal makine ölçek kümesindeki çalışır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="c46c7-111">Bir sanal makine ölçek kümesindeki kullanabileceğiniz herhangi bir işlevsellik, Service Fabric kümesi ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="c46c7-112">sanal makine ölçek kümeleri ve Service Fabric hello Azure Resource Manager şablonları ağ bölümlerini Hello aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="c46c7-113">Sanal ağ varolan tooan dağıttıktan sonra diğer kolay tooincorporate olan ağ Azure ExpressRoute, Azure VPN ağ geçidi, bir ağ güvenlik grubu ve sanal ağ eşlemesi gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="c46c7-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="c46c7-114">Service Fabric diğer ağ özelliklerini tek bir yönüne içinde benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="c46c7-115">Merhaba [Azure portal](https://portal.azure.com) dahili olarak kullandığı Service Fabric kaynak sağlayıcısı toocall tooa küme tooget düğümleri ve uygulamalar hakkında bilgi hello.</span><span class="sxs-lookup"><span data-stu-id="c46c7-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="c46c7-116">Hello Service Fabric kaynak sağlayıcı genel olarak erişilebilir gelen erişim toohello HTTP ağ geçidi bağlantı noktası (varsayılan olarak 19080, bağlantı noktası) hello yönetim uç nokta gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="c46c7-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="c46c7-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) kullanır, küme yönetim uç nokta toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="c46c7-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="c46c7-118">Merhaba Service Fabric kaynak sağlayıcısı ayrıca kümenizi, toodisplay hello Azure portal'ın bu bağlantı noktası tooquery bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="c46c7-119">Bağlantı noktası 19080 hello Service Fabric kaynak Sağlayıcısı'ndan erişilebilir durumda değilse, bir ileti ister *düğümleri bulunamadı* hello Portalı'nda görüntülenir ve düğüm ve uygulama listenizi boş görünür.</span><span class="sxs-lookup"><span data-stu-id="c46c7-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="c46c7-120">Hello Azure portal kümenizdeki toosee istiyorsanız, bir ortak IP adresi, yük dengeleyici kullanıma gerekir ve ağ güvenlik grubu gelen bağlantı noktası 19080 trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="c46c7-121">Kurulumunuzu bu gereksinimlerini karşılamıyorsa hello Azure portal kümenizi hello durumunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="c46c7-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="c46c7-122">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="c46c7-122">Templates</span></span>

<span data-ttu-id="c46c7-123">Tüm Service Fabric şablonları bulunan [bir yükleme dosyası](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="c46c7-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="c46c7-124">Merhaba şablon olarak kullanabilirsiniz toodeploy olmalıdır-hello aşağıdaki PowerShell komutlarını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="c46c7-125">Dağıtıyorsanız hello olan Azure Virtual Network şablonu veya hello statik genel IP şablonu, ilk hello okuma [ilk kurulum](#initialsetup) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="c46c7-126">İlk kurulumu</span><span class="sxs-lookup"><span data-stu-id="c46c7-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="c46c7-127">Var olan sanal ağ</span><span class="sxs-lookup"><span data-stu-id="c46c7-127">Existing virtual network</span></span>

<span data-ttu-id="c46c7-128">Aşağıdaki örneğine hello biz ExistingRG-vnet, hello adlı varolan bir sanal ağı Başlat **ExistingRG** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="c46c7-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="c46c7-129">Merhaba alt ağ varsayılan olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-129">hello subnet is named default.</span></span> <span data-ttu-id="c46c7-130">Hello Azure portal toocreate standart bir sanal makine (VM) kullandığınızda, bu varsayılan kaynakları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c46c7-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="c46c7-131">Merhaba VM oluşturmadan hello sanal ağ ve alt ağ oluşturabilirsiniz, ancak küme tooan varolan sanal ağ ekleme hello ana tooprovide ağ bağlantısı tooother VM'ler hedeftir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="c46c7-132">Oluşturma hello VM varolan bir sanal ağı genellikle nasıl kullanıldığını, iyi bir örnek verir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="c46c7-133">Service Fabric kümesi yalnızca bir iç yük dengeleyici, genel bir IP adresi olmadan kullanıyorsa kullanabileceğiniz VM ve güvenli olarak ortak IP hello *kutusunu atlama*.</span><span class="sxs-lookup"><span data-stu-id="c46c7-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="c46c7-134">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="c46c7-134">Static public IP address</span></span>

<span data-ttu-id="c46c7-135">Bir statik genel IP adresi, genellikle hello VM veya atandığı VM'ler gelen ayrı olarak yönetilen ayrılmış bir kaynak değil.</span><span class="sxs-lookup"><span data-stu-id="c46c7-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="c46c7-136">Bu ayrılmış bir ağ kaynak grubunda (karşılıklı tooin hello Service Fabric küme kaynak grubu kendisi) sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="c46c7-137">Merhaba staticIP1 adlı bir statik genel IP adresi oluşturma hello Azure portal veya PowerShell kullanarak aynı ExistingRG kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="c46c7-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="c46c7-138">Service Fabric şablonu</span><span class="sxs-lookup"><span data-stu-id="c46c7-138">Service Fabric template</span></span>

<span data-ttu-id="c46c7-139">Bu makalede Hello örneklerde hello Service Fabric template.json kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c46c7-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="c46c7-140">Küme oluşturmadan önce hello standart portal Sihirbazı toodownload hello hello portal şablondan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="c46c7-141">Merhaba şablonlarından birini de hello kullanabilirsiniz [Şablon Galerisi](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), hello gibi [beş düğümlü Service Fabric kümesi](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="c46c7-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="c46c7-142">Var olan sanal ağ veya alt ağ</span><span class="sxs-lookup"><span data-stu-id="c46c7-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="c46c7-143">Hello alt parametre toohello hello mevcut alt adını değiştirin ve sonra iki yeni parametreleri tooreference hello var olan bir sanal ağ ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c46c7-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="c46c7-144">Değişiklik hello `vnetID` değişken toopoint toohello var olan sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="c46c7-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="c46c7-145">Kaldırma `Microsoft.Network/virtualNetworks` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="c46c7-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="c46c7-146">Açıklama hello sanal ağdan hello çıkışı `dependsOn` özniteliği `Microsoft.Compute/virtualMachineScaleSets`, yeni bir sanal ağ oluşturma ile ilgili bağımlı yok:</span><span class="sxs-lookup"><span data-stu-id="c46c7-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="c46c7-147">Merhaba şablonunu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="c46c7-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="c46c7-148">Dağıtımdan sonra sanal ağınızı içermelidir hello yeni ölçek kümesi VM.</span><span class="sxs-lookup"><span data-stu-id="c46c7-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="c46c7-149">Merhaba sanal makine ölçek kümesi düğüm türü hello varolan sanal ağ ve alt göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="c46c7-150">Sanal makineleri tooping hello yeni ölçek kümesi ve Uzak Masaüstü Protokolü (RDP) tooaccess hello sanal ağda zaten olan VM hello de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c46c7-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="c46c7-151">Başka bir örnek için bkz: [belirli tooService doku olmayan bir](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c46c7-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="c46c7-152">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="c46c7-152">Static public IP address</span></span>

1. <span data-ttu-id="c46c7-153">Statik IP kaynak grubu, adı ve tam etki alanı adı (FQDN) mevcut hello hello adını parametrelerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c46c7-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="c46c7-154">Merhaba kaldırmak `dnsName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c46c7-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="c46c7-155">(Merhaba statik IP adresi zaten varsa.)</span><span class="sxs-lookup"><span data-stu-id="c46c7-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="c46c7-156">Değişken tooreference hello varolan statik bir IP adresi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c46c7-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="c46c7-157">Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="c46c7-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="c46c7-158">Açıklama hello hello IP adresinden çıkışı `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok:</span><span class="sxs-lookup"><span data-stu-id="c46c7-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="c46c7-159">Merhaba, `Microsoft.Network/loadBalancers` kaynak, değişiklik hello `publicIPAddress` öğesinin `frontendIPConfigurations` tooreference hello yeni oluşturulan bir yerine var olan statik IP adresi:</span><span class="sxs-lookup"><span data-stu-id="c46c7-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="c46c7-160">Merhaba, `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` toohello hello statik IP adresi DNS FQDN'si.</span><span class="sxs-lookup"><span data-stu-id="c46c7-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="c46c7-161">Güvenli bir küme kullanıyorsanız, değiştirdiğinizden emin olun *http://* çok*https://*.</span><span class="sxs-lookup"><span data-stu-id="c46c7-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="c46c7-162">(Bu adım yalnızca tooService yapı kümeleri geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c46c7-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="c46c7-163">Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="c46c7-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="c46c7-164">Merhaba şablonunu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="c46c7-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="c46c7-165">Dağıtımdan sonra Yük Dengeleyici ilişkili toohello ortak statik IP adresi hello olduğunu görebilirsiniz diğer kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="c46c7-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="c46c7-166">Service Fabric istemci bağlantı uç noktasının hello ve [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uç noktası toohello hello statik IP adresi DNS FQDN'si.</span><span class="sxs-lookup"><span data-stu-id="c46c7-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="c46c7-167">Yalnızca dahili yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c46c7-167">Internal-only load balancer</span></span>

<span data-ttu-id="c46c7-168">Bu senaryo hello dış yük dengeleyici hello varsayılan Service Fabric şablonunda yalnızca iç yük dengeleyici ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="c46c7-169">Hello Azure portal ve hello Service Fabric kaynak sağlayıcısı için uygulamaları için önceki bölümde hello bakın.</span><span class="sxs-lookup"><span data-stu-id="c46c7-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="c46c7-170">Merhaba kaldırmak `dnsName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c46c7-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="c46c7-171">(Bu gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="c46c7-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="c46c7-172">İsteğe bağlı olarak, statik ayırma yöntemi kullanırsanız, bir statik IP adresi parametre ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="c46c7-173">Dinamik ayırma yöntemini kullanırsanız, bu adımı toodo gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c46c7-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="c46c7-174">Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="c46c7-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="c46c7-175">Başlangıç IP adresini kaldırın `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok.</span><span class="sxs-lookup"><span data-stu-id="c46c7-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="c46c7-176">Merhaba sanal ağ ekleme `dependsOn` hello yük dengeleyici şimdi hello alt hello sanal ağdan bağımlı olduğundan dolayı özniteliği:</span><span class="sxs-lookup"><span data-stu-id="c46c7-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="c46c7-177">Değiştirme hello yük dengeleyicisinin `frontendIPConfigurations` kullanımından ayarını bir `publicIPAddress`, toousing bir alt ağ ve `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="c46c7-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="c46c7-178">`privateIPAddress`önceden tanımlanmış statik iç IP adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="c46c7-179">toouse dinamik bir IP adresi kaldırmak hello `privateIPAddress` öğesini ve ardından değişiklik `privateIPAllocationMethod` çok**dinamik**.</span><span class="sxs-lookup"><span data-stu-id="c46c7-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="c46c7-180">Merhaba, `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` toopoint toohello iç yük dengeleyici adresi.</span><span class="sxs-lookup"><span data-stu-id="c46c7-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="c46c7-181">Güvenli bir küme kullanıyorsanız, değiştirdiğiniz emin olun *http://* çok*https://*.</span><span class="sxs-lookup"><span data-stu-id="c46c7-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="c46c7-182">(Bu adım yalnızca tooService yapı kümeleri geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c46c7-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="c46c7-183">Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="c46c7-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="c46c7-184">Merhaba şablonunu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="c46c7-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="c46c7-185">Dağıtımdan sonra Yük Dengeleyici hello özel statik 10.0.0.250 IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="c46c7-186">Bu aynı sanal ağdaki başka bir makine varsa, iç toohello gidebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uç noktası.</span><span class="sxs-lookup"><span data-stu-id="c46c7-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="c46c7-187">Merhaba yük dengeleyicinin arkasındaki hello düğümlerinin tooone bağladığı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c46c7-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="c46c7-188">İç ve dış yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c46c7-188">Internal and external load balancer</span></span>

<span data-ttu-id="c46c7-189">Bu senaryoda, hello var olan tek bir düğüm türü dış yük dengeleyici ile başlatın ve hello için bir iç yük dengeleyici eklemek aynı düğüm türü.</span><span class="sxs-lookup"><span data-stu-id="c46c7-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="c46c7-190">Yalnızca tooa tek yük dengeleyici arka uç bağlantı noktası bağlı tooa arka uç adres havuzu atanabilir.</span><span class="sxs-lookup"><span data-stu-id="c46c7-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="c46c7-191">Hangi yük dengeleyici, uygulama bağlantı noktaları sahip ve hangi yük dengeleyici Yönetimi noktalarınızı (bağlantı noktaları 19000 ve 19080) sahip seçin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="c46c7-192">Merhaba iç yük dengeleyicide hello yönetim uç noktalarının yerleştirirseniz göz hello Service Fabric kaynak sağlayıcısı kısıtlamaları hello makalenin önceki bölümlerinde açıklanan tutun.</span><span class="sxs-lookup"><span data-stu-id="c46c7-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="c46c7-193">Kullanırız hello örnekte hello yönetim uç noktalarının hello dış yük dengeleyici üzerinde kalır.</span><span class="sxs-lookup"><span data-stu-id="c46c7-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="c46c7-194">Ayrıca bir bağlantı noktası 80 uygulama bağlantı noktası eklemek ve hello iç yük dengeleyicide yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="c46c7-195">İki düğüm türü kümedeki bir düğüm üzerinde hello dış yük dengeleyici türüdür.</span><span class="sxs-lookup"><span data-stu-id="c46c7-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="c46c7-196">Merhaba diğer düğümü hello iç yük dengeleyicide türüdür.</span><span class="sxs-lookup"><span data-stu-id="c46c7-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="c46c7-197">toouse (sahip iki yük dengeleyici gelen) hello portal tarafından oluşturulan iki düğüm türü şablonu, bir iki düğüm türü kümede hello ikinci yük dengeleyici tooan iç yük dengeleyici geçin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="c46c7-198">Daha fazla bilgi için bkz: Merhaba [yalnızca dahili yük dengeleyici](#internallb) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c46c7-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="c46c7-199">Merhaba statik iç yük dengeleyici IP adresi parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="c46c7-200">(Notları ilgili toousing için dinamik bir IP adresi, bu makalenin önceki bölümlerinde bkz.)</span><span class="sxs-lookup"><span data-stu-id="c46c7-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="c46c7-201">Bir uygulama bağlantı noktası 80 parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c46c7-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="c46c7-202">Merhaba varolan tooadd iç sürümlerini kopyalama değişkenleri, ağ ve kopyalayıp yapıştırın ve Ekle "-Int" toohello adı:</span><span class="sxs-lookup"><span data-stu-id="c46c7-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="c46c7-203">Uygulama bağlantı noktası 80 kullanan hello portal tarafından oluşturulan şablon ile başlatırsanız, hello varsayılan portal şablonu AppPort1 ekler (bağlantı noktası 80) hello dış yük dengeleyici üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c46c7-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="c46c7-204">Bu durumda, AppPort1 hello dış yük dengeleyiciden kaldırın `loadBalancingRules` ve araştırmalar toohello iç yük dengeleyici eklemek için:</span><span class="sxs-lookup"><span data-stu-id="c46c7-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="c46c7-205">İkinci bir ekleme `Microsoft.Network/loadBalancers` kaynak.</span><span class="sxs-lookup"><span data-stu-id="c46c7-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="c46c7-206">Hello oluşturulan benzer toohello iç yük dengeleyici görünüyor [yalnızca dahili yük dengeleyici](#internallb) bölüm, ancak kullanan hello "-Int" dengeleyici değişkenleri ve uygular yalnızca hello uygulama bağlantı noktası 80'i yükler.</span><span class="sxs-lookup"><span data-stu-id="c46c7-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="c46c7-207">Bu da kaldırır `inboundNatPools`, hello genel yük dengeleyiciye üzerindeki tookeep RDP uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="c46c7-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="c46c7-208">Merhaba iç yük dengeleyici üzerinde RDP istiyorsanız taşıyın `inboundNatPools` hello dış yük dengeleyici toothis iç yük dengeleyici:</span><span class="sxs-lookup"><span data-stu-id="c46c7-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="c46c7-209">İçinde `networkProfile` hello için `Microsoft.Compute/virtualMachineScaleSets` kaynak hello iç arka uç adres havuzu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c46c7-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="c46c7-210">Merhaba şablonunu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="c46c7-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="c46c7-211">Dağıtımdan sonra hello kaynak grubunda iki yük dengeleyici görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="c46c7-212">Merhaba yük dengeleyici göz atarsanız, hello genel IP adresi ve yönetim atanan uç noktaları (ve bağlantı noktaları 19000 19080) toohello genel IP adresi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c46c7-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="c46c7-213">Merhaba statik iç IP adresi ve uygulama atanan uç noktasını (bağlantı noktası 80) toohello iç de görebilirsiniz yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="c46c7-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="c46c7-214">Yük Dengeleyici kullanın hello aynı sanal makine ölçek kümesi arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="c46c7-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c46c7-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c46c7-215">Next steps</span></span>
[<span data-ttu-id="c46c7-216">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="c46c7-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
