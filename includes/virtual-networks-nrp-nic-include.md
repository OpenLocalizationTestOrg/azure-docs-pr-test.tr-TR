## <a name="nic"></a><span data-ttu-id="331e5-101">NIC</span><span class="sxs-lookup"><span data-stu-id="331e5-101">NIC</span></span>
<span data-ttu-id="331e5-102">Bir ağ arabirimi kartı (NIC) kaynak ağ bağlantısı tooan mevcut alt VNet kaynak sağlar.</span><span class="sxs-lookup"><span data-stu-id="331e5-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="331e5-103">Tek başına nesne olarak bir NIC oluşturabilseniz de tooassociate gerekir, tooanother nesne tooactually bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="331e5-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="331e5-104">Bir NIC kullanılan tooconnect VM tooa alt ağı, bir ortak IP adresi veya bir yük dengeleyici olabilir.</span><span class="sxs-lookup"><span data-stu-id="331e5-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="331e5-105">Özellik</span><span class="sxs-lookup"><span data-stu-id="331e5-105">Property</span></span> | <span data-ttu-id="331e5-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="331e5-106">Description</span></span> | <span data-ttu-id="331e5-107">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="331e5-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="331e5-108">**sanal makinesi**</span><span class="sxs-lookup"><span data-stu-id="331e5-108">**virtualMachine**</span></span> |<span data-ttu-id="331e5-109">VM hello NIC ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="331e5-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="331e5-110">/Subscriptions/{guid}/../microsoft.COMPUTE/virtualMachines/VM1</span><span class="sxs-lookup"><span data-stu-id="331e5-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="331e5-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="331e5-111">**macAddress**</span></span> |<span data-ttu-id="331e5-112">Merhaba NIC MAC adresi</span><span class="sxs-lookup"><span data-stu-id="331e5-112">MAC address for hello NIC</span></span> |<span data-ttu-id="331e5-113">4 ile 30 arasında herhangi bir değer</span><span class="sxs-lookup"><span data-stu-id="331e5-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="331e5-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="331e5-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="331e5-115">İlişkili NSG toohello NIC</span><span class="sxs-lookup"><span data-stu-id="331e5-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="331e5-116">/Subscriptions/{guid}/../microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="331e5-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="331e5-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="331e5-117">**dnsSettings**</span></span> |<span data-ttu-id="331e5-118">Merhaba NIC için DNS ayarları</span><span class="sxs-lookup"><span data-stu-id="331e5-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="331e5-119">bkz: [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="331e5-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="331e5-120">Bir ağ arabirim kartı veya NIC, ilişkili tooa sanal makine (VM) olabilir bir ağ arabirimi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="331e5-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="331e5-121">Bir VM, bir veya birden çok NIC olabilir.</span><span class="sxs-lookup"><span data-stu-id="331e5-121">A VM can have one or more NICs.</span></span>

![NIC kişinin tek bir VM'de](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="331e5-123">IP yapılandırması</span><span class="sxs-lookup"><span data-stu-id="331e5-123">IP configurations</span></span>
<span data-ttu-id="331e5-124">Nıc'lerinin adlı bir alt nesne **Ipconfigurations** aşağıdaki özelliklere hello içeren:</span><span class="sxs-lookup"><span data-stu-id="331e5-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="331e5-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="331e5-125">Property</span></span> | <span data-ttu-id="331e5-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="331e5-126">Description</span></span> | <span data-ttu-id="331e5-127">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="331e5-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="331e5-128">**alt ağ**</span><span class="sxs-lookup"><span data-stu-id="331e5-128">**subnet**</span></span> |<span data-ttu-id="331e5-129">Alt ağ hello NIC için onnected ' dir.</span><span class="sxs-lookup"><span data-stu-id="331e5-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="331e5-130">/Subscriptions/{guid}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="331e5-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="331e5-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="331e5-131">**privateIPAddress**</span></span> |<span data-ttu-id="331e5-132">Hello NIC hello alt ağ için IP adresi</span><span class="sxs-lookup"><span data-stu-id="331e5-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="331e5-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="331e5-133">10.0.0.8</span></span> |
| <span data-ttu-id="331e5-134">**privateıpallocationmethod değeri**</span><span class="sxs-lookup"><span data-stu-id="331e5-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="331e5-135">IP ayırma yöntemi</span><span class="sxs-lookup"><span data-stu-id="331e5-135">IP allocation method</span></span> |<span data-ttu-id="331e5-136">Dinamik veya statik</span><span class="sxs-lookup"><span data-stu-id="331e5-136">Dynamic or Static</span></span> |
| <span data-ttu-id="331e5-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="331e5-137">**enableIPForwarding**</span></span> |<span data-ttu-id="331e5-138">Merhaba NIC yönlendirme için kullanılıp kullanılamayacağını</span><span class="sxs-lookup"><span data-stu-id="331e5-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="331e5-139">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="331e5-139">true or false</span></span> |
| <span data-ttu-id="331e5-140">**birincil**</span><span class="sxs-lookup"><span data-stu-id="331e5-140">**primary**</span></span> |<span data-ttu-id="331e5-141">Merhaba NIC olup hello VM için birincil NIC hello</span><span class="sxs-lookup"><span data-stu-id="331e5-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="331e5-142">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="331e5-142">true or false</span></span> |
| <span data-ttu-id="331e5-143">**Publicıpaddress**</span><span class="sxs-lookup"><span data-stu-id="331e5-143">**publicIPAddress**</span></span> |<span data-ttu-id="331e5-144">PIP Hello NIC ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="331e5-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="331e5-145">bkz: [DNS ayarları](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="331e5-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="331e5-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="331e5-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="331e5-147">Bitiş adresi havuzları hello NIC ile ilişkili geri</span><span class="sxs-lookup"><span data-stu-id="331e5-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="331e5-148">**Loadbalancerınboundnatrules**</span><span class="sxs-lookup"><span data-stu-id="331e5-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="331e5-149">Yük Dengeleyici NAT kuralları hello NIC ile ilişkili gelen</span><span class="sxs-lookup"><span data-stu-id="331e5-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="331e5-150">Örnek genel IP adresi JSON biçiminde:</span><span class="sxs-lookup"><span data-stu-id="331e5-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="331e5-151">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="331e5-151">Additional resources</span></span>
* <span data-ttu-id="331e5-152">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163579.aspx) NIC'ler için.</span><span class="sxs-lookup"><span data-stu-id="331e5-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

