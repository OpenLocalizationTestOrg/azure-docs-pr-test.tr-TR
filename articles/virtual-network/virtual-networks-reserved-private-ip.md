---
title: "Statik iç özel IP - Azure VM - Klasik"
description: "Statik iç IP (Dıps) ve bunların nasıl yönetileceğini anlama"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="945df-103">PowerShell (Klasik) kullanarak statik iç özel bir IP adresi ayarlama</span><span class="sxs-lookup"><span data-stu-id="945df-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="945df-104">Çoğu durumda, sanal makine için statik iç IP adresi belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="945df-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="945df-105">Bir sanal ağdaki sanal makineleri otomatik olarak bir iç IP adresi, belirttiğiniz bir aralıktan alır.</span><span class="sxs-lookup"><span data-stu-id="945df-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="945df-106">Ancak bazı durumlarda, belirli bir VM için bir statik IP adresi belirtme mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="945df-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="945df-107">Örneğin, VM'yi DNS çalıştıracağınız ise veya bir etki alanı denetleyicisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="945df-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="945df-108">Statik iç IP adresi VM bile bir Dur/deprovision durumu ile birlikte kalır.</span><span class="sxs-lookup"><span data-stu-id="945df-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="945df-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="945df-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="945df-110">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="945df-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="945df-111">Microsoft, en yeni dağıtımların kullanmasını önerir [Resource Manager dağıtım modeli](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="945df-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="945df-112">Belirli bir IP adresi olup olmadığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="945df-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="945df-113">Olmadığını doğrulamak için IP adresi *10.0.0.7* adlı sanal ağ içinde kullanılabilir *TestVnet*, aşağıdaki PowerShell komutunu çalıştırın ve değerini doğrulamak *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="945df-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="945df-114">Yukarıdaki komut güvenli bir ortamda test etmek isterseniz yönergelere [bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-pportal.md) adlı bir vnet oluşturmak için *TestVnet* ve onu kullandığından emin olun *10.0.0.0/8*  adres alanı.</span><span class="sxs-lookup"><span data-stu-id="945df-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="945df-115">Bir VM oluşturulurken statik iç IP belirtme</span><span class="sxs-lookup"><span data-stu-id="945df-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="945df-116">Aşağıdaki PowerShell komut dosyası adlı yeni bir bulut hizmeti oluşturur *TestService*, Azure'dan bir görüntü alır sonra adlandırılmış bir VM'nin oluşturur *TestVM* alınan görüntü kullanarak yeni bulut hizmetinde ayarlar Adlı bir alt ağda olması VM *Subnet-1*ve ayarlar *10.0.0.7* VM için statik iç IP olarak:</span><span class="sxs-lookup"><span data-stu-id="945df-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="945df-117">Bir sanal makine için statik iç IP bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="945df-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="945df-118">Komut dosyası yukarıdaki VM oluşturulan için statik iç IP bilgilerini görüntülemek için aşağıdaki PowerShell komutunu çalıştırın ve değerlerini uyun *IPADDRESS*:</span><span class="sxs-lookup"><span data-stu-id="945df-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="945df-119">Bir sanal makineden bir statik iç IP kaldırma</span><span class="sxs-lookup"><span data-stu-id="945df-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="945df-120">Yukarıdaki komut dosyasındaki VM eklenen statik iç IP kaldırmak için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="945df-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="945df-121">Mevcut bir VM'yi statik iç IP ekleme</span><span class="sxs-lookup"><span data-stu-id="945df-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="945df-122">İç statik eklemek için VM IP çalışma yukarıdaki betik komutu aşağıdaki kullanılarak oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="945df-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="945df-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="945df-123">Next steps</span></span>
[<span data-ttu-id="945df-124">Ayrılmış IP</span><span class="sxs-lookup"><span data-stu-id="945df-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="945df-125">Örnek düzeyinde ortak IP (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="945df-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="945df-126">Ayrılmış IP REST API'leri</span><span class="sxs-lookup"><span data-stu-id="945df-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

