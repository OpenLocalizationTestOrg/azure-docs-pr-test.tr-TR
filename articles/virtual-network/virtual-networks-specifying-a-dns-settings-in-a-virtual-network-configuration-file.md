---
title: "Bir sanal ağ yapılandırma dosyasında DNS ayarlarını belirtme | Microsoft Docs"
description: "Klasik dağıtım modelinde bir sanal ağ yapılandırma dosyası kullanarak bir sanal ağ içinde DNS sunucusu ayarlarını değiştirme"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: ec33268915a1888509834ce6a5b2bc782a12ce4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="d3fb6-103">Bir sanal ağ yapılandırma dosyasında DNS ayarlarını belirtme</span><span class="sxs-lookup"><span data-stu-id="d3fb6-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="d3fb6-104">Bir ağ yapılandırma dosyası, etki alanı adı sistemi (DNS) ayarlarını belirlemek için kullanabileceğiniz iki öğe vardır: **DnsServers** ve **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="d3fb6-105">IP adreslerini belirterek DNS sunucularının bir listesini ekleyin ve başvuru adlarına **DnsServers** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span></span> <span data-ttu-id="d3fb6-106">Daha sonra kullanabileceğiniz bir **DnsServerRef** öğesi hangi DNS sunucusu girdileri DnsServers öğeden, sanal ağ içindeki farklı ağ siteleri için kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d3fb6-107">Bu makale, klasik dağıtım modelini kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-107">This article covers the classic deployment model.</span></span>

<span data-ttu-id="d3fb6-108">Ağ yapılandırma dosyası, aşağıdaki öğeleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-108">The network configuration file may contain the following elements.</span></span> <span data-ttu-id="d3fb6-109">Her öğe başlığı öğesi değer ayarları hakkında ek bilgi sağlayan bir sayfasında bağlantılıdır.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-109">The title of each element is linked to a page that provides additional information about the element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3fb6-110">Ağ yapılandırma dosyası yapılandırma hakkında daha fazla bilgi için bkz: [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="d3fb6-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="d3fb6-111">Ağ yapılandırma dosyasında yer alan her öğe hakkında daha fazla bilgi için bkz: [Azure sanal ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3fb6-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="d3fb6-112">DNS öğesi</span><span class="sxs-lookup"><span data-stu-id="d3fb6-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="d3fb6-113">**Adı** özniteliğini **DnsServer** öğe yalnızca başvuru olarak kullanılır **DnsServerRef** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span></span> <span data-ttu-id="d3fb6-114">DNS sunucusu için konak adı göstermiyor.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-114">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="d3fb6-115">Her **DnsServer** öznitelik değeri benzersiz olmalıdır tüm Microsoft Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="d3fb6-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="d3fb6-116">Sanal ağ site öğesi</span><span class="sxs-lookup"><span data-stu-id="d3fb6-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="d3fb6-117">Sanal ağ site öğesi için bu ayarı belirtmek için daha önce DNS öğesinde tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span></span> <span data-ttu-id="d3fb6-118">DnsServerRef *adı* sanal ağ siteleri öğesi DnsServer için DNS öğesinde belirtilen bir ad değeri başvurmalıdır. *adı*.</span><span class="sxs-lookup"><span data-stu-id="d3fb6-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d3fb6-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3fb6-119">Next steps</span></span>
* <span data-ttu-id="d3fb6-120">Anlamak [Azure Virtual Network yapılandırma şeması](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="d3fb6-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="d3fb6-121">Anlamak [Azure hizmet yapılandırma şeması](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="d3fb6-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="d3fb6-122">[Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="d3fb6-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

