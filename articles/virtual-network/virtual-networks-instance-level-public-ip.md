---
title: "Azure örneği düzeyinde (Klasik) ortak IP adresleri | Microsoft Docs"
description: "Örnek düzeyinde ortak IP (ILPIP) yöneliktir ve bunların nasıl yönetileceğini anlamak PowerShell kullanarak."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="e00da-103">Örnek düzeyinde ortak IP (Klasik) genel bakış</span><span class="sxs-lookup"><span data-stu-id="e00da-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="e00da-104">Bir örnek düzeyinde ortak IP (ILPIP), VM veya Bulut Hizmetleri rol örneği için doğrudan yerine, VM'deki veya rol örneğindeki bulunan bulut hizmetine atayabilirsiniz genel bir IP adresi ' dir.</span><span class="sxs-lookup"><span data-stu-id="e00da-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="e00da-105">Bir ILPIP, sanal IP (bulut Hizmetinize atanmış VIP) yer almaz.</span><span class="sxs-lookup"><span data-stu-id="e00da-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="e00da-106">Bunun yerine, doğrudan, VM'deki veya rol örneğine bağlanmak için kullanabileceğiniz ek bir IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="e00da-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e00da-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e00da-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e00da-108">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="e00da-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e00da-109">Microsoft, VM'ler Resource Manager aracılığıyla oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="e00da-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="e00da-110">Anladığınızdan emin olun nasıl [IP adreslerini](virtual-network-ip-addresses-overview-classic.md) Azure içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e00da-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP VIP arasındaki fark](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="e00da-112">Şekil 1'de gösterildiği gibi bulut hizmeti bir VIP kullanırken, tek tek sanal makineleri, normalde VIP kullanılarak erişilir erişilir:&lt;bağlantı noktası numarası&gt;.</span><span class="sxs-lookup"><span data-stu-id="e00da-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="e00da-113">Belirli bir VM'yi bir ILPIP atayarak bu VM, bu IP adresi kullanarak doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="e00da-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="e00da-114">Azure'da bulut hizmeti oluşturduğunuzda, karşılık gelen DNS A kayıtlarını otomatik olarak bir tam etki alanı adı (FQDN) üzerinden hizmete erişmesine izin vermek için gerçek VIP kullanmak yerine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e00da-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="e00da-115">FQDN ILPIP yerine VM veya rol örneğine izin veren bir ILPIP için aynı işlem gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="e00da-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="e00da-116">Örneği için adlı bir bulut hizmeti oluşturursanız *contosoadservice*, ve adında bir web rolü yapılandırma *contosoweb* iki örnekleriyle aşağıdaki Azure kaydeder A kayıtlarını örnekleri için:</span><span class="sxs-lookup"><span data-stu-id="e00da-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="e00da-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e00da-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="e00da-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e00da-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="e00da-119">Her VM veya rol örneği için yalnızca bir ILPIP atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00da-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="e00da-120">Abonelik başına en fazla 5 ILPIPs kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e00da-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="e00da-121">ILPIPs multi-NIC VM'ler için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e00da-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="e00da-122">Bir ILPIP isteme neden?</span><span class="sxs-lookup"><span data-stu-id="e00da-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="e00da-123">Bulut kullanmak yerine VIP Doğrudan kendisine atanmış bir IP adresine göre VM'deki veya rol örneğine bağlanmak istiyorsanız, hizmet:&lt;bağlantı noktası numarası&gt;, VM veya rol örneği için bir ILPIP isteyin.</span><span class="sxs-lookup"><span data-stu-id="e00da-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="e00da-124">**Etkin FTP** -bir VM için bir ILPIP atayarak onu herhangi bir bağlantı noktasında trafik alabilir.</span><span class="sxs-lookup"><span data-stu-id="e00da-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="e00da-125">Uç noktaları VM trafiği almak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e00da-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="e00da-126">(Https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP Protokolü genel bakış] FTP protokolünü hakkında ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="e00da-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="e00da-127">**Giden IP** - sanal makineden giden trafiği ILPIP kaynağı olarak eşleştirilir ve ILPIP dış varlıklar VM benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e00da-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="e00da-128">Geçmişte, bir ILPIP adresi genel bir IP (PIP) adresi başvuruldu.</span><span class="sxs-lookup"><span data-stu-id="e00da-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="e00da-129">Bir VM için bir ILPIP yönetme</span><span class="sxs-lookup"><span data-stu-id="e00da-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="e00da-130">Aşağıdaki görevler oluşturun, atamak ve VM'lerin ILPIPs kaldırmak etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="e00da-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="e00da-131">PowerShell kullanarak VM oluşturma sırasında bir ILPIP istemek nasıl</span><span class="sxs-lookup"><span data-stu-id="e00da-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="e00da-132">Aşağıdaki PowerShell betiğini adlı bir bulut hizmeti oluşturur *FTPService*, Azure'dan bir görüntü alır, adlandırılmış bir VM'nin oluşturur *FTPInstance* alınan görüntü kullanarak bir ILPIP kullanmak için VM ayarlar ve ekler Yeni hizmet VM'ye:</span><span class="sxs-lookup"><span data-stu-id="e00da-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="e00da-133">Bir VM için ILPIP bilgi alma</span><span class="sxs-lookup"><span data-stu-id="e00da-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="e00da-134">Önceki komut dosyasıyla VM oluşturulan için ILPIP bilgileri görüntülemek için aşağıdaki PowerShell komutunu çalıştırın ve değerlerini uyun *Publicıpaddress* ve *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="e00da-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="e00da-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e00da-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="e00da-136">Bir sanal makineden bir ILPIP kaldırma</span><span class="sxs-lookup"><span data-stu-id="e00da-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="e00da-137">Önceki komut dosyasında VM eklenen ILPIP kaldırmak için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e00da-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="e00da-138">Mevcut bir VM'yi bir ILPIP ekleme</span><span class="sxs-lookup"><span data-stu-id="e00da-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="e00da-139">Önceki komut dosyası kullanılarak oluşturulan VM bir ILPIP eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e00da-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="e00da-140">Bulut Hizmetleri rol örneği için bir ILPIP yönetme</span><span class="sxs-lookup"><span data-stu-id="e00da-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="e00da-141">Bulut Hizmetleri rol örneği için bir ILPIP eklemek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e00da-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="e00da-142">İçindeki adımları tamamlayarak bulut hizmeti için .cscfg dosyasını indirin [bulut hizmetlerini yapılandırma](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e00da-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="e00da-143">.Cscfg dosyasını ekleyerek güncelleştirme `InstanceAddress` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e00da-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="e00da-144">Aşağıdaki örnek adlı bir ILPIP ekler *MyPublicIP* adlı bir rol örneği *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="e00da-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="e00da-145">İçindeki adımları tamamlayarak bulut hizmeti için .cscfg dosyasını karşıya [bulut hizmetlerini yapılandırma](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e00da-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e00da-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e00da-146">Next steps</span></span>
* <span data-ttu-id="e00da-147">Anlamak nasıl [IP adresleme](virtual-network-ip-addresses-overview-classic.md) Klasik dağıtım modelinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e00da-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="e00da-148">Hakkında bilgi edinin [ayrılmış IP'ler](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="e00da-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
