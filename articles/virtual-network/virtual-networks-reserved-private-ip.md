---
title: "aaaStatic iç özel IP - Azure VM - Klasik"
description: "Statik iç IP (Dıps) Anlama ve nasıl toomanage bunları"
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
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="41392-103">Nasıl tooset statik iç özel IP adresi (Klasik) PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="41392-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="41392-104">Çoğu durumda, sanal makine için statik iç IP adresi toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="41392-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="41392-105">Bir sanal ağdaki sanal makineleri otomatik olarak bir iç IP adresi, belirttiğiniz bir aralıktan alır.</span><span class="sxs-lookup"><span data-stu-id="41392-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="41392-106">Ancak bazı durumlarda, belirli bir VM için bir statik IP adresi belirtme mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="41392-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="41392-107">Örneğin, VM'yi giderek toorun DNS veya bir etki alanı denetleyicisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41392-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="41392-108">Statik iç IP adresi hello VM bile bir Dur/deprovision durumu ile birlikte kalır.</span><span class="sxs-lookup"><span data-stu-id="41392-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="41392-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="41392-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="41392-110">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="41392-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="41392-111">Microsoft en yeni dağıtımların hello kullanmanızı önerir [Resource Manager dağıtım modeli](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="41392-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="41392-112">Nasıl belirli bir IP adresi olup olmadığını tooverify</span><span class="sxs-lookup"><span data-stu-id="41392-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="41392-113">Merhaba, tooverify IP adresi *10.0.0.7* adlı sanal ağ içinde kullanılabilir *TestVnet*hello aşağıdaki PowerShell komutunu çalıştırın ve hello değerini doğrulamak *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="41392-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="41392-114">Güvenli bir ortamda yukarıda tootest hello komutu istiyorsanız hello yönergeleri izleyin [bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-pportal.md) toocreate adlı bir vnet *TestVnet* ve hello kullandığından emin olun  *10.0.0.0/8* adres alanı.</span><span class="sxs-lookup"><span data-stu-id="41392-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="41392-115">Nasıl toospecify bir VM oluşturulurken statik iç IP</span><span class="sxs-lookup"><span data-stu-id="41392-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="41392-116">Merhaba aşağıdaki PowerShell komut dosyası adlı yeni bir bulut hizmeti oluşturur *TestService*, Azure'dan bir görüntü alır sonra adlandırılmış bir VM'nin oluşturur *TestVM* hello alınan hello görüntü kullanarak yeni bulut hizmetinde ayarlar hello adlı bir alt ağdaki VM toobe *Subnet-1*ve ayarlar *10.0.0.7* hello VM için statik iç IP olarak:</span><span class="sxs-lookup"><span data-stu-id="41392-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="41392-117">Nasıl tooretrieve statik iç IP bilgileri bir VM için</span><span class="sxs-lookup"><span data-stu-id="41392-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="41392-118">VM yukarıdaki hello betiği ile oluşturulan tooview hello statik iç IP bilgileri hello hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *IPADDRESS*:</span><span class="sxs-lookup"><span data-stu-id="41392-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="41392-119">Nasıl tooremove bir VM'den statik iç IP</span><span class="sxs-lookup"><span data-stu-id="41392-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="41392-120">tooremove hello statik iç IP toohello VM yukarıdaki hello betik eklenen hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41392-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="41392-121">Nasıl tooadd bir statik iç IP tooan var olan VM</span><span class="sxs-lookup"><span data-stu-id="41392-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="41392-122">bir statik iç IP toohello komutu aşağıdaki yukarıdaki çalışma hello komut dosyası kullanılarak oluşturulan VM tooadd:</span><span class="sxs-lookup"><span data-stu-id="41392-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="41392-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41392-123">Next steps</span></span>
[<span data-ttu-id="41392-124">Ayrılmış IP</span><span class="sxs-lookup"><span data-stu-id="41392-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="41392-125">Örnek düzeyinde ortak IP (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="41392-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="41392-126">Ayrılmış IP REST API'leri</span><span class="sxs-lookup"><span data-stu-id="41392-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

