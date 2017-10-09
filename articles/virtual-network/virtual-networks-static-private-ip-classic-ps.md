---
title: "aaaConfigure özel IP adresleri VM'ler (Klasik) - Azure PowerShell | Microsoft Docs"
description: "PowerShell kullanarak sanal makineleri için (Klasik) nasıl tooconfigure özel IP adresleri öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a><span data-ttu-id="18455-103">PowerShell kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="18455-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="18455-104">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="18455-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="18455-105">Ayrıca [hello Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="18455-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="18455-106">Merhaba örnek PowerShell komutlarını aşağıdaki önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="18455-106">hello sample PowerShell commands below expect a simple environment already created.</span></span> <span data-ttu-id="18455-107">Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [VNet oluşturma](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="18455-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="18455-108">Nasıl belirli bir IP adresi olup olmadığını tooverify</span><span class="sxs-lookup"><span data-stu-id="18455-108">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="18455-109">Merhaba, tooverify IP adresi *192.168.1.101* adlı sanal ağ içinde kullanılabilir *TestVNet*hello aşağıdaki PowerShell komutunu çalıştırın ve hello değerini doğrulamak *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="18455-109">tooverify if hello IP address *192.168.1.101* is available in a VNet named *TestVNet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

<span data-ttu-id="18455-110">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="18455-110">Expected output:</span></span>

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="18455-111">Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken</span><span class="sxs-lookup"><span data-stu-id="18455-111">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="18455-112">Merhaba aşağıdaki PowerShell komut dosyası adlı yeni bir bulut hizmeti oluşturur *TestService*, sonra görüntüyü Azure'dan alır, adlandırılmış bir VM'nin oluşturur *DNS01* alınan hello görüntüsünü kullanarak hello yeni bulut hizmeti, ayarlar adlı bir alt ağdaki VM toobe hello *ön uç*ve ayarlar *192.168.1.7* hello VM için statik bir özel IP adresi olarak:</span><span class="sxs-lookup"><span data-stu-id="18455-112">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

<span data-ttu-id="18455-113">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="18455-113">Expected output:</span></span>

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="18455-114">Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi</span><span class="sxs-lookup"><span data-stu-id="18455-114">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="18455-115">tooview hello statik özel IP adres bilgilerinin hello için VM oluşturulan yukarıdaki hello komut dosyasıyla hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *IPADDRESS*:</span><span class="sxs-lookup"><span data-stu-id="18455-115">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name DNS01 -ServiceName TestService

<span data-ttu-id="18455-116">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="18455-116">Expected output:</span></span>

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="18455-117">Nasıl tooremove bir statik özel IP adresi bir sanal makineden</span><span class="sxs-lookup"><span data-stu-id="18455-117">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="18455-118">tooremove hello statik özel IP adresi toohello VM üzerinde aşağıdaki PowerShell komutunu çalıştırma hello hello betikteki eklendi:</span><span class="sxs-lookup"><span data-stu-id="18455-118">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

<span data-ttu-id="18455-119">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="18455-119">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="18455-120">Nasıl tooadd statik özel IP adresi VM varolan tooan</span><span class="sxs-lookup"><span data-stu-id="18455-120">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="18455-121">bir statik özel IP adresi toohello komutu aşağıdaki yukarıdaki çalışma hello komut dosyası kullanılarak oluşturulan VM tooadd:</span><span class="sxs-lookup"><span data-stu-id="18455-121">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

<span data-ttu-id="18455-122">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="18455-122">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a><span data-ttu-id="18455-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18455-123">Next steps</span></span>
* <span data-ttu-id="18455-124">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="18455-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="18455-125">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="18455-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="18455-126">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="18455-126">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

