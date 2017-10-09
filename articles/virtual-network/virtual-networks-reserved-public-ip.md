---
title: "aaaManage Azure ayrılmış IP adresi (Klasik) - PowerShell | Microsoft Docs"
description: "Ayrılmış IP adresleri (Klasik) anlamak ve nasıl toomanage bunları PowerShell kullanarak."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="9c2b1-103">Ayrılmış IP adresleri (Klasik)</span><span class="sxs-lookup"><span data-stu-id="9c2b1-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c2b1-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9c2b1-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="9c2b1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c2b1-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="9c2b1-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9c2b1-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="9c2b1-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="9c2b1-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="9c2b1-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="9c2b1-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="9c2b1-109">Azure'daki IP adresleri iki kategoriye ayrılır: dinamik ve ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="9c2b1-110">Azure tarafından yönetilen ortak IP adresleri, varsayılan olarak dinamik.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="9c2b1-111">Bu IP adresi (VIP) verilen bulut hizmeti için kullanılan hello anlamına gelir veya tooaccess kaynakları kapatıldı veya durduruldu (serbest bırakıldığında) bir VM veya rol örneğine doğrudan (ILPIP) zaman tootime ' değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="9c2b1-112">değiştirmesini tooprevent IP adresleri, bir IP adresi ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="9c2b1-113">Ayrılmış IP'ler sağlayarak bu hello IP adresi kalır kaynakları kapatmak gibi aynı hello veya durduruldu (serbest bırakıldığında) hello bulut hizmeti için yalnızca bir VIP olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="9c2b1-114">Ayrıca, bir VIP tooa ayrılmış IP adresi olarak kullanılan varolan dinamik IP dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c2b1-115">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c2b1-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c2b1-116">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9c2b1-117">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9c2b1-118">Bir statik genel IP adresini kullanarak tooreserve nasıl hello öğrenin [Resource Manager dağıtım modeli](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9c2b1-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="9c2b1-119">IP hakkında daha fazla toolearn adresleri Azure'da, hello okuma [IP adreslerini](virtual-network-ip-addresses-overview-classic.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="9c2b1-120">Ayrılmış IP olduğunda gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="9c2b1-121">**IP hello tooensure aboneliğinizde ayrılmış istediğiniz**.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="9c2b1-122">Aboneliğiniz hiçbir koşulda tooreserve serbest bırakılmaz bir IP adresi istiyorsanız, ayrılmış bir genel IP kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="9c2b1-123">**Bulut hizmetiniz ile IP toostay bile çapraz durduruldu veya durumu (VM'ler) serbest istediğiniz**.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="9c2b1-124">Değişmez bir IP adresi kullanarak erişilen, hizmet toobe istiyorsanız bile hello VM bulut hizmeti kapatıldığından veya (serbest bırakıldığında) durdurun.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="9c2b1-125">**Azure giden trafiği tahmin edilebilir bir IP adresi kullanan tooensure istediğiniz**.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="9c2b1-126">Şirket içi, yapılandırılmış güvenlik duvarı tooallow yalnızca trafiğinizi belirli IP adresleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="9c2b1-127">Bir IP ayırarak hello kaynak IP bilmeniz adres ve tooan IP değişikliği, güvenlik duvarı kuralları tooupdate olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="9c2b1-128">SSS</span><span class="sxs-lookup"><span data-stu-id="9c2b1-128">FAQ</span></span>
1. <span data-ttu-id="9c2b1-129">Tüm Azure hizmetlerini bir ayrılmış IP kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="9c2b1-130">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-130">No.</span></span> <span data-ttu-id="9c2b1-131">Ayrılmış IP'ler yalnızca VM'ler ve bulut hizmeti örnek rolleriniz VIP kullanıma sunulan için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="9c2b1-132">Kaç tane ayrılmış IP'ler sahip olabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="9c2b1-133">Merhaba Ayrıntılar için bkz [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="9c2b1-134">Herhangi bir ücret için ayrılmış IP'ler var mı?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="9c2b1-135">Bazen.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-135">Sometimes.</span></span> <span data-ttu-id="9c2b1-136">Merhaba fiyatlandırma ayrıntıları için bkz: [ayrılmış IP adresi fiyatlandırma ayrıntıları](http://go.microsoft.com/fwlink/?LinkID=398482) sayfası.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="9c2b1-137">Bir IP adresi nasıl yedek?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="9c2b1-138">PowerShell hello kullanabileceğiniz [Azure Yönetimi REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), veya hello [Azure portal](https://portal.azure.com) tooreserve bir Azure bölgesindeki bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="9c2b1-139">Ayrılmış bir IP adresi ilişkili tooyour abonelik değil.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="9c2b1-140">Benzeşim grubu tabanlı sanal ağlar ile ayrılmış bir IP kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9c2b1-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="9c2b1-141">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-141">No.</span></span> <span data-ttu-id="9c2b1-142">Ayrılmış IP'ler yalnızca Bölgesel sanal ağlar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="9c2b1-143">Ayrılmış IP, benzeşim gruplarıyla ilişkili sanal ağlar için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="9c2b1-144">Merhaba VNet bir bölge veya benzeşim grubu ile ilişkilendirme hakkında daha fazla bilgi için bkz: [hakkında bölgesel sanal ağlara ve benzeşim grupları](virtual-networks-migrate-to-regional-vnet.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="9c2b1-145">Ayrılmış VIP'ler yönetme</span><span class="sxs-lookup"><span data-stu-id="9c2b1-145">Manage reserved VIPs</span></span>

<span data-ttu-id="9c2b1-146">Yüklenmesini ve PowerShell hello hello adımları tamamlayarak yapılandırılmış [yükleyin ve PowerShell yapılandırma](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="9c2b1-147">Ayrılmış IP'ler kullanmadan önce tooyour abonelik eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="9c2b1-148">toocreate genel IP hello havuzundan ayrılmış IP adresleri hello bulunan *Orta ABD* konumu, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="9c2b1-149">Ancak, IP yüklenmekte olan belirtemezsiniz fark ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="9c2b1-150">tooview hangi IP adresleri, aboneliğinizde hello aşağıdaki PowerShell komutunu çalıştırın, ayrılmış ve fark hello değerlerini *Reservedıpname* ve *adres*:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="9c2b1-151">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="9c2b1-152">PowerShell ile ayrılmış bir IP adresi oluşturduğunuzda, bir kaynak grubu toocreate hello ayrılmış IP belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="9c2b1-153">Bir kaynak grubu içine adlı azure yerler *varsayılan ağ* otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="9c2b1-154">Hello kullanarak hello ayrılmış IP oluşturursanız [Azure portal](http://portal.azure.com), seçtiğiniz herhangi bir kaynak grubu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="9c2b1-155">Merhaba ayrılmış IP bir kaynak grubunda dışında oluşturursanız, *varsayılan ağ* başvuru her ancak hello IP komutlarıyla gibi ayrılmış `Get-AzureReservedIP` ve `Remove-AzureReservedIP`, hello adı başvurmalıdır*Grup kaynak grubu adı ayrılmış-IP-name*.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="9c2b1-156">Adlı bir ayrılmış IP oluşturursanız, örneğin, *myReservedIP* bir kaynak grubunda adlı *myResourceGroup*, hello ayrılmış IP olarak hello adını başvurmalıdır *Grup myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="9c2b1-157">Bir IP ayrılmış sonra onu silene kadar ilişkili tooyour abonelik kalır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="9c2b1-158">toodelete ayrılmış bir IP aşağıdaki PowerShell komutunu çalıştırma hello:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="9c2b1-159">Var olan bir bulut hizmetinin başlangıç IP adresi ayırın</span><span class="sxs-lookup"><span data-stu-id="9c2b1-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="9c2b1-160">Merhaba ekleyerek, var olan bir bulut hizmetini hello IP adresi ayırabilirsiniz `-ServiceName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="9c2b1-161">bir bulut hizmeti tooreserve hello IP adresini *TestService* hello içinde *Orta ABD* konumu, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="9c2b1-162">Ayrılmış IP tooa yeni bir bulut hizmeti ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="9c2b1-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="9c2b1-163">Hello aşağıdaki betiği yeni bir ayrılmış IP oluşturur, ardından tooa adlı yeni bulut hizmeti ilişkilendirir *TestService*.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="9c2b1-164">Bir bulut hizmeti ile ayrılmış bir IP toouse oluşturduğunuzda, hala toohello VM başvurabilmek *VIP:&lt;bağlantı noktası numarası >* gelen iletişimi için.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="9c2b1-165">IP ayırma toohello VM doğrudan bağlanabilirsiniz anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="9c2b1-166">Merhaba ayrılmış IP toohello bulut atanmış VM dağıtılan için o hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="9c2b1-167">Tooconnect tooa VM IP tarafından doğrudan isterseniz, bir örnek düzeyinde ortak IP tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="9c2b1-168">Örnek düzeyinde ortak IP tooyour VM doğrudan atanmış (bir ILPIP olarak adlandırılır) genel IP türüdür.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="9c2b1-169">Ayrılamaz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-169">It cannot be reserved.</span></span> <span data-ttu-id="9c2b1-170">Daha fazla bilgi için hello okuma [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="9c2b1-171">Ayrılmış IP çalışan dağıtımdan kaldırın</span><span class="sxs-lookup"><span data-stu-id="9c2b1-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="9c2b1-172">tooremove ayrılmış IP hello aşağıdaki PowerShell komutunu çalıştırın tooa yeni bulut hizmeti, ekledi:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="9c2b1-173">Ayrılmış bir IP adresinden çalışan bir dağıtımını kaldırma hello ayırma aboneliğinizden kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="9c2b1-174">Yalnızca aboneliğiniz başka bir kaynak tarafından kullanılan hello IP toobe serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="9c2b1-175">Dağıtım çalıştıran ayrılmış bir IP tooa ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="9c2b1-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="9c2b1-176">Merhaba aşağıdaki komutları adlı bir bulut hizmeti Oluştur *TestService2* adlı yeni bir VM ile *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="9c2b1-177">ayrılmış IP'si adlı Hello varolan *MyReservedIP* ilişkili toohello bulut hizmeti olduğundan.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="9c2b1-178">Hizmet yapılandırma dosyası kullanarak bir ayrılmış IP tooa bulut hizmeti ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="9c2b1-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="9c2b1-179">Ayrıca, bir hizmet yapılandırma (CSCFG) dosyası kullanarak bir ayrılmış IP tooa bulut hizmeti ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="9c2b1-180">Merhaba aşağıdaki örnek xml nasıl tooconfigure bir bulut hizmeti toouse ayrılmış bir VIP adlı gösterir *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="9c2b1-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="9c2b1-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c2b1-181">Next steps</span></span>
* <span data-ttu-id="9c2b1-182">Anlamak nasıl [IP adresleme](virtual-network-ip-addresses-overview-classic.md) hello Klasik dağıtım modelinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9c2b1-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="9c2b1-183">Hakkında bilgi edinin [ayrılmış özel IP adresi](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9c2b1-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="9c2b1-184">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP) adresleri](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9c2b1-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

