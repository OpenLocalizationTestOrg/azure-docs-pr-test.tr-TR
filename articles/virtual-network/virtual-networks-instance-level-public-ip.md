---
title: "aaaAzure örnek düzeyinde ortak IP (Klasik) adresleri | Microsoft Docs"
description: "Örnek düzeyinde ortak IP (ILPIP) adresleri anlamak ve nasıl toomanage bunları PowerShell kullanarak."
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
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="5944d-103">Örnek düzeyinde ortak IP (Klasik) genel bakış</span><span class="sxs-lookup"><span data-stu-id="5944d-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="5944d-104">Bir örnek düzeyinde ortak IP (ILPIP), VM veya rol örneğine bulunan toohello bulut hizmeti yerine tooa VM veya Bulut Hizmetleri rol örneği doğrudan atayabilir genel bir IP adresi ' dir.</span><span class="sxs-lookup"><span data-stu-id="5944d-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="5944d-105">Bir ILPIP tooyour bulut hizmetine atanan hello sanal IP (VIP) hello yerini almaz.</span><span class="sxs-lookup"><span data-stu-id="5944d-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="5944d-106">Bunun yerine, tooconnect kullanabileceğiniz ek bir IP adresi olduğundan doğrudan tooyour VM'deki veya rol örneği.</span><span class="sxs-lookup"><span data-stu-id="5944d-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5944d-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5944d-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="5944d-108">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="5944d-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5944d-109">Microsoft, VM'ler Resource Manager aracılığıyla oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="5944d-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="5944d-110">Anladığınızdan emin olun nasıl [IP adreslerini](virtual-network-ip-addresses-overview-classic.md) Azure içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5944d-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP VIP arasındaki fark](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="5944d-112">Şekil 1'de gösterildiği gibi hello bulut hizmeti, bir VIP kullanarak erişildiğinde, başlangıç sırasında tek tek sanal makineleri normalde VIP kullanılarak erişilir:&lt;bağlantı noktası numarası&gt;.</span><span class="sxs-lookup"><span data-stu-id="5944d-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="5944d-113">Bir ILPIP tooa atayarak, VM olabilir belirli VM, doğrudan bu IP adresi kullanılarak erişilir.</span><span class="sxs-lookup"><span data-stu-id="5944d-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="5944d-114">Azure'da bulut hizmeti oluşturduğunuzda, karşılık gelen DNS A kayıtlarını otomatik olarak tooallow erişim toohello hizmeti bir tam etki alanı adı (FQDN) aracılığıyla hello gerçek VIP kullanmak yerine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5944d-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="5944d-115">Merhaba erişim toohello VM'deki veya rol örneğindeki FQDN DEĞERİNE göre hello ILPIP yerine sağlayan bir ILPIP için aynı işlem gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="5944d-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="5944d-116">Örneğin, adlı bir bulut hizmeti oluşturursanız, *contosoadservice*, ve adında bir web rolü yapılandırma *contosoweb* iki örnekleriyle A aşağıdaki Azure yazmaçlar hello kayıtları hello örnekleri için:</span><span class="sxs-lookup"><span data-stu-id="5944d-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="5944d-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="5944d-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="5944d-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="5944d-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="5944d-119">Her VM veya rol örneği için yalnızca bir ILPIP atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5944d-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="5944d-120">Abonelik başına too5 ILPIPs kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5944d-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="5944d-121">ILPIPs multi-NIC VM'ler için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5944d-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="5944d-122">Bir ILPIP isteme neden?</span><span class="sxs-lookup"><span data-stu-id="5944d-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="5944d-123">Merhaba bulut kullanmak yerine VIP toobe mümkün tooconnect tooyour VM istediğiniz veya rol örneği bir IP adresi tarafından atanan doğrudan tooit, hizmet:&lt;bağlantı noktası numarası&gt;, VM veya rol örneği için bir ILPIP isteyin.</span><span class="sxs-lookup"><span data-stu-id="5944d-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="5944d-124">**Etkin FTP** -ILPIP tooa VM atayarak onu herhangi bir bağlantı noktasında trafik alabilir.</span><span class="sxs-lookup"><span data-stu-id="5944d-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="5944d-125">Uç noktaları hello VM tooreceive trafiği için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5944d-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="5944d-126">(Https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP Protokolü genel bakış] hello FTP Protokolü hakkında ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="5944d-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="5944d-127">**Giden IP** - VM hello giden trafiği eşlenen toohello hello kaynağı olarak ILPIP ve hello ILPIP benzersiz olarak tanımlayan hello VM tooexternal varlıklar.</span><span class="sxs-lookup"><span data-stu-id="5944d-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="5944d-128">Geçmiş Hello içinde bir ILPIP adresi başvurulan tooas genel bir IP (PIP) adresi oluştu.</span><span class="sxs-lookup"><span data-stu-id="5944d-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="5944d-129">Bir VM için bir ILPIP yönetme</span><span class="sxs-lookup"><span data-stu-id="5944d-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="5944d-130">görevleri aşağıdaki hello toocreate, Ata ve Kaldır vm'lerden ILPIPs etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="5944d-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="5944d-131">Nasıl toorequest PowerShell kullanarak VM oluşturma sırasında bir ILPIP</span><span class="sxs-lookup"><span data-stu-id="5944d-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="5944d-132">PowerShell Betiği aşağıdaki hello adlı bir bulut hizmeti oluşturur *FTPService*, Azure'dan bir görüntü alır, adlandırılmış bir VM'nin oluşturur *FTPInstance* bir ILPIP kümeleri hello VM toouse alınan hello görüntü kullanma ve hello VM toohello yeni hizmet ekler:</span><span class="sxs-lookup"><span data-stu-id="5944d-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="5944d-133">Nasıl bir VM için tooretrieve ILPIP bilgileri</span><span class="sxs-lookup"><span data-stu-id="5944d-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="5944d-134">tooview hello VM oluşturulan hello önceki komut dosyasıyla ILPIP bilgileri hello için hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *Publicıpaddress* ve *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="5944d-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="5944d-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5944d-135">Expected output:</span></span>
 
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

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="5944d-136">Nasıl tooremove bir VM'den bir ILPIP</span><span class="sxs-lookup"><span data-stu-id="5944d-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="5944d-137">tooremove hello ILPIP toohello VM hello aşağıdaki PowerShell komutunu çalıştırın hello önceki betikte eklendi:</span><span class="sxs-lookup"><span data-stu-id="5944d-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="5944d-138">Nasıl tooadd ILPIP tooan var olan VM</span><span class="sxs-lookup"><span data-stu-id="5944d-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="5944d-139">tooadd ILPIP toohello önceki, hello komut dosyası kullanılarak oluşturulan VM hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5944d-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="5944d-140">Bulut Hizmetleri rol örneği için bir ILPIP yönetme</span><span class="sxs-lookup"><span data-stu-id="5944d-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="5944d-141">tooadd ILPIP tooa bulut Hizmetleri rol örneği, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="5944d-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="5944d-142">Merhaba tamamlayarak hello bulut hizmeti hello adımları için hello .cscfg dosyasını indirin [tooConfigure Cloud Services nasıl](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makale.</span><span class="sxs-lookup"><span data-stu-id="5944d-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="5944d-143">Merhaba ekleyerek güncelleştirme hello .cscfg dosyası `InstanceAddress` öğesi.</span><span class="sxs-lookup"><span data-stu-id="5944d-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="5944d-144">Merhaba aşağıdaki örnek ekler adlı bir ILPIP *MyPublicIP* adlı tooa rol örneği *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="5944d-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="5944d-145">Merhaba tamamlayarak hello bulut hizmeti hello adımları hello .cscfg dosyasını karşıya [tooConfigure Cloud Services nasıl](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) makale.</span><span class="sxs-lookup"><span data-stu-id="5944d-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5944d-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5944d-146">Next steps</span></span>
* <span data-ttu-id="5944d-147">Anlamak nasıl [IP adresleme](virtual-network-ip-addresses-overview-classic.md) hello Klasik dağıtım modelinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5944d-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="5944d-148">Hakkında bilgi edinin [ayrılmış IP'ler](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5944d-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
