---
title: "Bir hizmet yapılandırma dosyasında DNS ayarlarını belirtme | Microsoft Docs"
description: "sanal ağ için hizmet yapılandırma dosyası kullanarak özel DNS ayarlarını belirtme"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="1e8ff-103">Bir hizmet yapılandırma dosyasında DNS ayarlarını belirtme</span><span class="sxs-lookup"><span data-stu-id="1e8ff-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="1e8ff-104">DNS öğeleri</span><span class="sxs-lookup"><span data-stu-id="1e8ff-104">DNS elements</span></span>
<span data-ttu-id="1e8ff-105">Hizmet yapılandırma dosyası hizmetini kullanacak olan etki alanı adı sistemi (DNS) sunucuları için IPv4 adresleri listesi olan bir DnsServers öğesi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="1e8ff-106">Hizmet yapılandırma dosyası ayarlarında ayarları ağ yapılandırma dosyasında daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="1e8ff-107">Daha fazla bilgi için bkz: [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e8ff-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="1e8ff-108">**NetworkConfiguration öğesi**</span><span class="sxs-lookup"><span data-stu-id="1e8ff-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="1e8ff-109">**Adı** özniteliğini **DnsServer** öğe yalnızca bir başvuru adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="1e8ff-110">DNS sunucusu için konak adı göstermiyor.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="1e8ff-111">Her **DnsServer** öznitelik değeri benzersiz olmalıdır tüm Microsoft Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="1e8ff-112">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1e8ff-112">See Also</span></span>
[<span data-ttu-id="1e8ff-113">Azure hizmet yapılandırma şeması (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="1e8ff-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="1e8ff-114">Azure Virtual Network yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="1e8ff-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="1e8ff-115">Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e8ff-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="1e8ff-116">Yönetim Portalı'nda sanal ağ ayarları hakkında</span><span class="sxs-lookup"><span data-stu-id="1e8ff-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

