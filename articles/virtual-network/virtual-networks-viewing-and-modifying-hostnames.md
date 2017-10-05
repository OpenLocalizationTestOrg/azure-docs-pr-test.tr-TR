---
title: "Görüntüleme ve ana bilgisayar adları değiştirme | Microsoft Docs"
description: "Nasıl görüntülemek ve Azure sanal makineleri için ana bilgisayar adlarını değiştirmek, web ve çalışan rolleri ad çözümlemesi için"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 9a3a1e1b58dcb828e2d2d09c18f1aab6d46051aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="8056e-103">Görüntüleme ve ana bilgisayar adları değiştirme</span><span class="sxs-lookup"><span data-stu-id="8056e-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="8056e-104">Ana bilgisayar adına göre başvurulacak rolü örneklerinizi izin vermek için her bir rol hizmeti yapılandırma dosyasında ana bilgisayar adı değeri ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8056e-104">To allow your role instances to be referenced by host name, you must set the value for the host name in the service configuration file for each role.</span></span> <span data-ttu-id="8056e-105">İstenen konak adına ekleyerek bunu **vmName** özniteliği **rol** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8056e-105">You do that by adding the desired host name to the **vmName** attribute of the **Role** element.</span></span> <span data-ttu-id="8056e-106">Değeri **vmName** özniteliği her rol örneği ana bilgisayar adı için temel olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8056e-106">The value of the **vmName** attribute is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="8056e-107">Örneğin, varsa **vmName** olan *webrole* ve bu rol üç örneği vardır, ana bilgisayar adlarını örneklerinin olacaktır *webrole0*, *webrole1*, ve *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="8056e-107">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="8056e-108">Sanal makine adına dayalı bir sanal makine için konak adı doldurulmuş için sanal makineler için bir konak adı yapılandırma dosyasında belirtmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8056e-108">You do not need to specify a host name for virtual machines in the configuration file, because the host name for a virtual machine is populated based on the virtual machine name.</span></span> <span data-ttu-id="8056e-109">Bir Microsoft Azure hizmet yapılandırma hakkında daha fazla bilgi için bkz: [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="8056e-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="8056e-110">Ana bilgisayar adları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="8056e-110">Viewing hostnames</span></span>
<span data-ttu-id="8056e-111">Sanal makineler ve rol örnekleri ana bilgisayar adlarını aşağıdaki araçlardan birini kullanarak bir bulut hizmetinde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8056e-111">You can view the host names of virtual machines and role instances in a cloud service by using any of the tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8056e-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8056e-112">Azure Portal</span></span>
<span data-ttu-id="8056e-113">Kullanabileceğiniz [Azure portal](http://portal.azure.com) genel bakış dikey penceresinde bir sanal makine için sanal makineleri ana bilgisayar adlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="8056e-113">You can use the [Azure portal](http://portal.azure.com) to view the host names for virtual machines on the overview blade for a virtual machine.</span></span> <span data-ttu-id="8056e-114">Dikey için bir değer gösterir göz önünde bulundurmanız **adı** ve **ana bilgisayar adı**.</span><span class="sxs-lookup"><span data-stu-id="8056e-114">Keep in mind that the blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="8056e-115">Bunlar başlangıçta aynı olsa da, ana bilgisayar adının değiştirilmesi sanal makine veya rol örneği adı değişmez.</span><span class="sxs-lookup"><span data-stu-id="8056e-115">Although they are initially the same, changing the host name will not change the name of the virtual machine or role instance.</span></span>

<span data-ttu-id="8056e-116">Rol örneklerine de Azure portalında görüntülenebilir, ancak bir bulut hizmeti örnekleri listelediğinizde, ana bilgisayar adı görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="8056e-116">Role instances can also be viewed in the Azure portal, but when you list the instances in a cloud service, the host name is not displayed.</span></span> <span data-ttu-id="8056e-117">Her örneği için bir ad görürsünüz, ancak bu ad ana bilgisayar adını temsil etmiyor.</span><span class="sxs-lookup"><span data-stu-id="8056e-117">You will see a name for each instance, but that name does not represent the host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="8056e-118">Hizmet yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="8056e-118">Service configuration file</span></span>
<span data-ttu-id="8056e-119">Dağıtılan bir hizmet için hizmet yapılandırma dosyası indirebilirsiniz **yapılandırma** Azure portalında hizmetin dikey.</span><span class="sxs-lookup"><span data-stu-id="8056e-119">You can download the service configuration file for a deployed service from the **Configure** blade of the service in the Azure portal.</span></span> <span data-ttu-id="8056e-120">Ardından arayabileceğiniz **vmName** için öznitelik **rol adı** ana bilgisayar adı görmek için öğesi.</span><span class="sxs-lookup"><span data-stu-id="8056e-120">You can then look for the **vmName** attribute for the **Role name** element to see the host name.</span></span> <span data-ttu-id="8056e-121">Bu ana bilgisayar adı, her rol örneği ana bilgisayar adı için temel olarak kullanıldığını aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8056e-121">Keep in mind that this host name is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="8056e-122">Örneğin, varsa **vmName** olan *webrole* ve bu rol üç örneği vardır, ana bilgisayar adlarını örneklerinin olacaktır *webrole0*, *webrole1*, ve *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="8056e-122">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="8056e-123">Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="8056e-123">Remote Desktop</span></span>
<span data-ttu-id="8056e-124">Uzak Masaüstü'nü (Windows), Windows PowerShell uzaktan iletişimini (Windows) ya da sanal makineleri veya rol örneklerini (Linux ve Windows) SSH bağlantısını etkinleştirdikten sonra etkin bir Uzak Masaüstü bağlantı ana bilgisayar adından çeşitli şekillerde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8056e-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections to your virtual machines or role instances, you can view the host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="8056e-125">Komut istemi veya SSH terminal ana bilgisayar adını yazın.</span><span class="sxs-lookup"><span data-stu-id="8056e-125">Type hostname at the command prompt or SSH terminal.</span></span>
* <span data-ttu-id="8056e-126">(Yalnızca Windows) tüm komut satırında/ipconfig yazın.</span><span class="sxs-lookup"><span data-stu-id="8056e-126">Type ipconfig /all at the command prompt (Windows only).</span></span>
* <span data-ttu-id="8056e-127">Bilgisayar adı, sistem ayarları (yalnızca Windows) görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8056e-127">View the computer name in the system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="8056e-128">Azure Hizmet Yönetimi REST API'si</span><span class="sxs-lookup"><span data-stu-id="8056e-128">Azure Service Management REST API</span></span>
<span data-ttu-id="8056e-129">Bir REST istemciden aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="8056e-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="8056e-130">Azure Portalı'na bağlanmak için bir istemci sertifikası olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8056e-130">Ensure that you have a client certificate to connect to the Azure portal.</span></span> <span data-ttu-id="8056e-131">Bir istemci sertifikası edinmek için sunulan adımları izleyin [nasıl yapılır: indirme ve yayımlama ayarları içeri aktarma ve abonelik bilgileri](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="8056e-131">To obtain a client certificate, follow the steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="8056e-132">X-ms-version değeri 2013-11-01 adlı bir üstbilgi girişi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8056e-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="8056e-133">Aşağıdaki biçimde bir istek gönderin: https://management.core.windows.net/\<subscrition kimliği\>/services/hostedservices/\<hizmet adı\>? katıştırmak ayrıntı = true</span><span class="sxs-lookup"><span data-stu-id="8056e-133">Send a request in the following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="8056e-134">Ara **ana bilgisayar adı** öğesini her **RoleInstance** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8056e-134">Look for the **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="8056e-135">Ayrıca iç etki alanı soneki bulut hizmetinizden REST çağrısı yanıt için denetleyerek görüntüleyebilirsiniz **InternalDnsSuffix** öğesi veya ipconfig çalıştırarak/tüm bir komut isteminden kullanarak veya bir Uzak Masaüstü oturumunda (Windows) cat /etc/resolv.conf bir SSH terminal (Linux) çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="8056e-135">You can also view the internal domain suffix for your cloud service from the REST call response by checking the **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="8056e-136">Bir ana bilgisayar adını değiştirme</span><span class="sxs-lookup"><span data-stu-id="8056e-136">Modifying a hostname</span></span>
<span data-ttu-id="8056e-137">Değiştirilen hizmet yapılandırma dosyası karşıya ya da Uzak Masaüstü oturumu bilgisayardan yeniden adlandırma herhangi bir sanal makine veya rol örneği için ana bilgisayar adını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8056e-137">You can modify the host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming the computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8056e-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8056e-138">Next steps</span></span>
[<span data-ttu-id="8056e-139">Ad çözümlemesi (DNS)</span><span class="sxs-lookup"><span data-stu-id="8056e-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="8056e-140">Azure hizmet yapılandırma şeması (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="8056e-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="8056e-141">Azure Virtual Network yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="8056e-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="8056e-142">Ağ yapılandırma dosyalarını kullanarak DNS ayarlarını belirtin</span><span class="sxs-lookup"><span data-stu-id="8056e-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

