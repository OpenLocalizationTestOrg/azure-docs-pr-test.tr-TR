---
title: "Azure Service Fabric için ağ desenleri | Microsoft Docs"
description: "Service Fabric ve Azure ağ özellikleri kullanılarak bir küme oluşturma için ortak ağ desenleri açıklar."
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
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="517cf-103">Service Fabric ağ desenleri</span><span class="sxs-lookup"><span data-stu-id="517cf-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="517cf-104">Azure Service Fabric kümesi Azure diğer ağ özelliklerini ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="517cf-105">Bu makalede, sizi, aşağıdaki özellikleri kullanan bir küme nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="517cf-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="517cf-106">Var olan sanal ağ veya alt ağ</span><span class="sxs-lookup"><span data-stu-id="517cf-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="517cf-107">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="517cf-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="517cf-108">Yalnızca dahili yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="517cf-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="517cf-109">İç ve dış yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="517cf-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="517cf-110">Service Fabric standart sanal makine ölçek kümesindeki çalışır.</span><span class="sxs-lookup"><span data-stu-id="517cf-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="517cf-111">Bir sanal makine ölçek kümesindeki kullanabileceğiniz herhangi bir işlevsellik, Service Fabric kümesi ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="517cf-112">Sanal makine ölçek kümeleri ve Service Fabric için Azure Resource Manager şablonları ağ bölümlerini aynıdır.</span><span class="sxs-lookup"><span data-stu-id="517cf-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="517cf-113">Mevcut bir sanal ağa dağıttıktan sonra Azure ExpressRoute, Azure VPN ağ geçidi, bir ağ güvenlik grubu ve sanal ağ eşlemesi gibi diğer ağ özelliklerini içerecek şekilde kolaydır.</span><span class="sxs-lookup"><span data-stu-id="517cf-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="517cf-114">Service Fabric diğer ağ özelliklerini tek bir yönüne içinde benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="517cf-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="517cf-115">[Azure portal](https://portal.azure.com) dahili olarak bir küme düğümlerini ve uygulamalar hakkında bilgi almak için aranacak Service Fabric kaynak sağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="517cf-116">Service Fabric kaynak sağlayıcısı yönetim uç HTTP ağ geçidi bağlantı noktası (varsayılan olarak 19080, bağlantı noktası) için genel olarak erişilebilir gelen erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="517cf-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="517cf-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) kümenizi yönetmek için yönetim uç noktası kullanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="517cf-118">Service Fabric kaynak sağlayıcısı bu bağlantı noktası için küme hakkında bilgileri sorgulama Azure portalında görüntülemek için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="517cf-119">Bağlantı noktası 19080 Service Fabric kaynak sağlayıcısından erişilebilir durumda değilse, bir ileti ister *düğümleri bulunamadı* Portalı'nda görüntülenir ve düğüm ve uygulama listenizi boş görünür.</span><span class="sxs-lookup"><span data-stu-id="517cf-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="517cf-120">Kümenizi Azure portalında görmek istiyorsanız, bir ortak IP adresi, yük dengeleyici kullanıma gerekir ve ağ güvenlik grubu gelen bağlantı noktası 19080 trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="517cf-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="517cf-121">Azure portalı kurulumunuzu bu gereksinimlerini karşılamıyorsa, küme durumunu görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="517cf-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="517cf-122">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="517cf-122">Templates</span></span>

<span data-ttu-id="517cf-123">Tüm Service Fabric şablonları bulunan [bir yükleme dosyası](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="517cf-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="517cf-124">Şablon olarak dağıtamaz olmalıdır-aşağıdaki PowerShell komutlarını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="517cf-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="517cf-125">Var olan Azure Virtual Network şablonu veya statik genel IP şablonu dağıtıyorsanız, önce okuma [ilk kurulum](#initialsetup) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="517cf-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="517cf-126">İlk kurulumu</span><span class="sxs-lookup"><span data-stu-id="517cf-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="517cf-127">Var olan sanal ağ</span><span class="sxs-lookup"><span data-stu-id="517cf-127">Existing virtual network</span></span>

<span data-ttu-id="517cf-128">Aşağıdaki örnekte, biz ExistingRG-vnet adlı varolan bir sanal ağı Başlat **ExistingRG** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="517cf-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="517cf-129">Alt ağ varsayılan olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="517cf-129">The subnet is named default.</span></span> <span data-ttu-id="517cf-130">Standart bir sanal makine (VM) oluşturmak için Azure Portalı'nı kullandığınızda bu varsayılan kaynakları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="517cf-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="517cf-131">VM oluşturmak zorunda kalmadan sanal ağ ve alt oluşturabilirsiniz, ancak mevcut bir sanal ağa bir kümeyi eklemeyi ana amacı diğer VM'ler için ağ bağlantısı sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="517cf-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="517cf-132">VM oluşturma, varolan bir sanal ağı genellikle nasıl kullanıldığını, iyi bir örnek verir.</span><span class="sxs-lookup"><span data-stu-id="517cf-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="517cf-133">Service Fabric kümesi yalnızca bir iç yük dengeleyici, genel bir IP adresi olmadan kullanıyorsa, VM ve genel IP güvenli kullanabileceğiniz *kutusunu atlama*.</span><span class="sxs-lookup"><span data-stu-id="517cf-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="517cf-134">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="517cf-134">Static public IP address</span></span>

<span data-ttu-id="517cf-135">Bir statik genel IP adresi, genellikle için atanan VM ya da sanal makineleri ayrı olarak yönetilen ayrılmış bir kaynak değil.</span><span class="sxs-lookup"><span data-stu-id="517cf-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="517cf-136">(Kendisini Service Fabric küme kaynağı grubuna aygıtlardır), ayrılmış bir ağ kaynak grubunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="517cf-137">Aynı ExistingRG kaynak grubunda, Azure portalında veya PowerShell kullanarak staticIP1 adlı bir statik genel IP adresi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="517cf-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="517cf-138">Service Fabric şablonu</span><span class="sxs-lookup"><span data-stu-id="517cf-138">Service Fabric template</span></span>

<span data-ttu-id="517cf-139">Bu makaledeki örneklerde, Service Fabric template.json kullanırız.</span><span class="sxs-lookup"><span data-stu-id="517cf-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="517cf-140">Küme oluşturmadan önce şablonu portalından karşıdan yüklemek için standart portal Sihirbazı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="517cf-141">Şablonlardan birini de kullanabilirsiniz [Şablon Galerisi](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric)gibi [beş düğümlü Service Fabric kümesi](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="517cf-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="517cf-142">Var olan sanal ağ veya alt ağ</span><span class="sxs-lookup"><span data-stu-id="517cf-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="517cf-143">Alt parametre mevcut alt adını değiştirin ve ardından mevcut bir sanal ağ başvurmak için iki yeni parametreler ekleyin:</span><span class="sxs-lookup"><span data-stu-id="517cf-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

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


2. <span data-ttu-id="517cf-144">Değişiklik `vnetID` varolan bir sanal ağa işaret edecek şekilde değişkeni:</span><span class="sxs-lookup"><span data-stu-id="517cf-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="517cf-145">Kaldırma `Microsoft.Network/virtualNetworks` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="517cf-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="517cf-146">Sanal ağdan çıkışı açıklama `dependsOn` özniteliği `Microsoft.Compute/virtualMachineScaleSets`, yeni bir sanal ağ oluşturma ile ilgili bağımlı yok:</span><span class="sxs-lookup"><span data-stu-id="517cf-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="517cf-147">Şablon dağıtma:</span><span class="sxs-lookup"><span data-stu-id="517cf-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="517cf-148">Dağıtımdan sonra sanal ağınızı yeni içermelidir ölçek kümesi VM.</span><span class="sxs-lookup"><span data-stu-id="517cf-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="517cf-149">Sanal makine ölçek kümesi düğüm türü, varolan sanal ağ ve alt göstermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="517cf-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="517cf-150">Sanal ağ zaten olan VM erişmek için Uzak Masaüstü Protokolü (RDP) de kullanabilirsiniz ve yeni ölçek ping işlemi yapmak için sanal makineleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="517cf-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="517cf-151">Başka bir örnek için bkz: [Service Fabric belirli olmayan bir](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="517cf-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="517cf-152">Statik genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="517cf-152">Static public IP address</span></span>

1. <span data-ttu-id="517cf-153">Mevcut bir statik IP kaynak grubunun adı, adı ve tam etki alanı adı (FQDN) parametreleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="517cf-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="517cf-154">Kaldırma `dnsName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="517cf-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="517cf-155">(Statik IP adresi zaten varsa.)</span><span class="sxs-lookup"><span data-stu-id="517cf-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="517cf-156">Var olan bir statik IP adresi başvurusu için bir değişken ekleyin:</span><span class="sxs-lookup"><span data-stu-id="517cf-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="517cf-157">Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="517cf-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="517cf-158">IP adresinden çıkışı açıklama `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok:</span><span class="sxs-lookup"><span data-stu-id="517cf-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="517cf-159">İçinde `Microsoft.Network/loadBalancers` kaynak, değişiklik `publicIPAddress` öğesinin `frontendIPConfigurations` varolan statik IP adresi yerine yeni oluşturulan bir başvurmak için:</span><span class="sxs-lookup"><span data-stu-id="517cf-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="517cf-160">İçinde `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` statik IP adresinin DNS FQDN için.</span><span class="sxs-lookup"><span data-stu-id="517cf-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="517cf-161">Güvenli bir küme kullanıyorsanız, değiştirdiğinizden emin olun *http://* için *https://*.</span><span class="sxs-lookup"><span data-stu-id="517cf-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="517cf-162">(Bu adım yalnızca Service Fabric kümeleri için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="517cf-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="517cf-163">Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="517cf-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="517cf-164">Şablon dağıtma:</span><span class="sxs-lookup"><span data-stu-id="517cf-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="517cf-165">Dağıtımdan sonra Yük Dengeleyici diğer bir kaynak grubundan ortak statik IP adresine bağlı olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="517cf-166">Service Fabric istemci bağlantı uç noktasının ve [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) DNS FQDN uç noktasına statik IP adresi.</span><span class="sxs-lookup"><span data-stu-id="517cf-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="517cf-167">Yalnızca dahili yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="517cf-167">Internal-only load balancer</span></span>

<span data-ttu-id="517cf-168">Bu senaryo varsayılan Service Fabric şablonunda dış yük dengeleyici yalnızca iç yük dengeleyici ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="517cf-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="517cf-169">Azure portal ve Service Fabric kaynak sağlayıcısı için uygulamaları için önceki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="517cf-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="517cf-170">Kaldırma `dnsName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="517cf-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="517cf-171">(Bu gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="517cf-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="517cf-172">İsteğe bağlı olarak, statik ayırma yöntemi kullanırsanız, bir statik IP adresi parametre ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="517cf-173">Dinamik ayırma yöntemini kullanırsanız, bu adımı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="517cf-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="517cf-174">Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:</span><span class="sxs-lookup"><span data-stu-id="517cf-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="517cf-175">IP adresini kaldırın `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok.</span><span class="sxs-lookup"><span data-stu-id="517cf-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="517cf-176">Sanal ağ ekleme `dependsOn` yük dengeleyici şimdi alt ağdan sanal ağa bağımlı olduğundan dolayı özniteliği:</span><span class="sxs-lookup"><span data-stu-id="517cf-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

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

5. <span data-ttu-id="517cf-177">Yük dengeleyicinin değiştirme `frontendIPConfigurations` kullanımından ayarını bir `publicIPAddress`, bir alt ağ kullanarak ve `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="517cf-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="517cf-178">`privateIPAddress`önceden tanımlanmış statik iç IP adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="517cf-179">Dinamik IP adresi kullanmak için kaldırmak `privateIPAddress` öğesini ve ardından değişiklik `privateIPAllocationMethod` için **dinamik**.</span><span class="sxs-lookup"><span data-stu-id="517cf-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

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

6. <span data-ttu-id="517cf-180">İçinde `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` iç yük dengeleyici adresine yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="517cf-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="517cf-181">Güvenli bir küme kullanıyorsanız, değiştirdiğiniz emin olun *http://* için *https://*.</span><span class="sxs-lookup"><span data-stu-id="517cf-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="517cf-182">(Bu adım yalnızca Service Fabric kümeleri için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="517cf-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="517cf-183">Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="517cf-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="517cf-184">Şablon dağıtma:</span><span class="sxs-lookup"><span data-stu-id="517cf-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="517cf-185">Dağıtımdan sonra yük dengeleyicisi statik 10.0.0.250 özel IP adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="517cf-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="517cf-186">Bu aynı sanal ağdaki başka bir makine varsa, iç ağa gidebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uç noktası.</span><span class="sxs-lookup"><span data-stu-id="517cf-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="517cf-187">Yük dengeleyicinin arkasındaki düğümlerinden biri bağlanır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="517cf-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="517cf-188">İç ve dış yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="517cf-188">Internal and external load balancer</span></span>

<span data-ttu-id="517cf-189">Bu senaryoda, var olan tek bir düğüm türü dış yük dengeleyici ile başlatın ve aynı düğüm türü için iç yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="517cf-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="517cf-190">Yalnızca bir tek yük dengeleyici arka uç adres havuzuna bağlı bir arka uç bağlantı noktası atanabilir.</span><span class="sxs-lookup"><span data-stu-id="517cf-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="517cf-191">Hangi yük dengeleyici, uygulama bağlantı noktaları sahip ve hangi yük dengeleyici Yönetimi noktalarınızı (bağlantı noktaları 19000 ve 19080) sahip seçin.</span><span class="sxs-lookup"><span data-stu-id="517cf-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="517cf-192">İç yük dengeleyici ile ilgili yönetim uç noktalarının yerleştirirseniz, Service Fabric kaynak sağlayıcısı kısıtlamaları makalenin önceki bölümlerinde açıklanan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="517cf-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="517cf-193">Örnekte kullanıyoruz, yönetim uç noktaları dış yük dengeleyici üzerinde kalır.</span><span class="sxs-lookup"><span data-stu-id="517cf-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="517cf-194">Ayrıca bir bağlantı noktası 80 uygulama bağlantı noktası eklemek ve iç yük dengeleyicide yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="517cf-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="517cf-195">İki düğüm türü kümedeki bir düğüm üzerinde dış yük dengeleyici türüdür.</span><span class="sxs-lookup"><span data-stu-id="517cf-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="517cf-196">Bir düğüm türü için iç yük dengeleyicide ' dir.</span><span class="sxs-lookup"><span data-stu-id="517cf-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="517cf-197">İki düğüm türü küme (sahip iki yük dengeleyici desteklemektedir) portal tarafından oluşturulan iki düğüm türü şablonunda kullanmak için ikinci yük dengeleyici için bir iç yük dengeleyici geçin.</span><span class="sxs-lookup"><span data-stu-id="517cf-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="517cf-198">Daha fazla bilgi için bkz: [yalnızca dahili yük dengeleyici](#internallb) bölümü.</span><span class="sxs-lookup"><span data-stu-id="517cf-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="517cf-199">Statik iç yük dengeleyici IP adresi parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="517cf-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="517cf-200">(Dinamik bir IP adresi kullanmayla ilgili notlar için bu makalenin önceki bölümlerinde bkz.)</span><span class="sxs-lookup"><span data-stu-id="517cf-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="517cf-201">Bir uygulama bağlantı noktası 80 parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="517cf-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="517cf-202">Var olan iç sürümleri kopyalamak ve yapıştırmak değişkenleri, ağ ekleyin ve eklemek için "-Int" adı:</span><span class="sxs-lookup"><span data-stu-id="517cf-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

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

4. <span data-ttu-id="517cf-203">Uygulama bağlantı noktası 80 portal tarafından oluşturulan şablonla başlatırsanız, varsayılan portal şablonu AppPort1 ekler (bağlantı noktası 80) dış yük dengeleyici üzerinde.</span><span class="sxs-lookup"><span data-stu-id="517cf-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="517cf-204">Bu durumda, AppPort1 dış yük dengeleyiciden kaldırın `loadBalancingRules` ve iç yük dengeleyiciye ekleyebilmek araştırmalar:</span><span class="sxs-lookup"><span data-stu-id="517cf-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

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
        } /* Remove AppPort1 from the external load balancer.
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
        } /* Remove AppPort1 from the external load balancer.
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

5. <span data-ttu-id="517cf-205">İkinci bir ekleme `Microsoft.Network/loadBalancers` kaynak.</span><span class="sxs-lookup"><span data-stu-id="517cf-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="517cf-206">Oluşturulan iç yük dengeleyiciye benzer [yalnızca dahili yük dengeleyici](#internallb) bölüm, ancak kullanır "-Int" Yük Dengeleyici değişkenleri ve yalnızca uygulama bağlantı noktası 80 uygular.</span><span class="sxs-lookup"><span data-stu-id="517cf-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="517cf-207">Bu da kaldırır `inboundNatPools`, genel yük dengeleyiciye üzerinde RDP uç noktaları korumak için.</span><span class="sxs-lookup"><span data-stu-id="517cf-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="517cf-208">İç yük dengeleyici üzerinde RDP istiyorsanız taşıyın `inboundNatPools` dışarıdan yük dengeleyici bu dahili yük dengeleyici için:</span><span class="sxs-lookup"><span data-stu-id="517cf-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
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
                                /* Switch from Public to Private IP address
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
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
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
                    /* Add the probe for the app port. */
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

6. <span data-ttu-id="517cf-209">İçinde `networkProfile` için `Microsoft.Compute/virtualMachineScaleSets` kaynak, iç arka uç adres havuzu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="517cf-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

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

7. <span data-ttu-id="517cf-210">Şablon dağıtma:</span><span class="sxs-lookup"><span data-stu-id="517cf-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="517cf-211">Dağıtımdan sonra kaynak grubunda iki yük dengeleyici görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="517cf-212">Yük Dengeleyici göz atarsanız, genel IP adresi atanmış ortak IP adresi ve yönetim uç noktalar (bağlantı noktaları 19000 ve 19080) görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="517cf-213">İç yük dengeleyiciye atanan statik iç IP adresi ve uygulama uç noktası (bağlantı noktası 80) de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="517cf-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="517cf-214">Her iki yük dengeleyicisi, aynı sanal makine ölçek kümesi arka uç havuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="517cf-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="517cf-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="517cf-215">Next steps</span></span>
[<span data-ttu-id="517cf-216">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="517cf-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
