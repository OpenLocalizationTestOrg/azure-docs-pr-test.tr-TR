---
title: "Hizmet yapılandırma dosyasında DNS ayarlarını aaaSpecifying | Microsoft Docs"
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
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="3e4af-103">Bir hizmet yapılandırma dosyasında DNS ayarlarını belirtme</span><span class="sxs-lookup"><span data-stu-id="3e4af-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="3e4af-104">DNS öğeleri</span><span class="sxs-lookup"><span data-stu-id="3e4af-104">DNS elements</span></span>
<span data-ttu-id="3e4af-105">Hizmet yapılandırma dosyası hello hizmetini kullanacak olan hello etki alanı adı sistemi (DNS) sunucuları için IPv4 adresleri listesi olan bir DnsServers öğesi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3e4af-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="3e4af-106">Merhaba hizmet yapılandırma dosyası ayarlarında ayarları hello ağ yapılandırma dosyasında daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="3e4af-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="3e4af-107">Daha fazla bilgi için bkz: [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e4af-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="3e4af-108">**NetworkConfiguration öğesi**</span><span class="sxs-lookup"><span data-stu-id="3e4af-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="3e4af-109">Merhaba **adı** hello özniteliğinde **DnsServer** öğe yalnızca bir başvuru adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e4af-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="3e4af-110">Merhaba hello DNS sunucusu için konak adı göstermiyor.</span><span class="sxs-lookup"><span data-stu-id="3e4af-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="3e4af-111">Her **DnsServer** öznitelik değeri benzersiz olmalıdır hello tüm Microsoft Azure aboneliği arasında.</span><span class="sxs-lookup"><span data-stu-id="3e4af-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="3e4af-112">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="3e4af-112">See Also</span></span>
[<span data-ttu-id="3e4af-113">Azure hizmet yapılandırma şeması (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="3e4af-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="3e4af-114">Azure Virtual Network yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="3e4af-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="3e4af-115">Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3e4af-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="3e4af-116">Merhaba Yönetim Portalı sanal ağ ayarları hakkında</span><span class="sxs-lookup"><span data-stu-id="3e4af-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

