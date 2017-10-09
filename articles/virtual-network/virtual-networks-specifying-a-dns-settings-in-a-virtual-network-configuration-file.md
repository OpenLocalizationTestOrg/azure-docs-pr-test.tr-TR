---
title: "DNS ayarları bir sanal ağ yapılandırma dosyasındaki aaaSpecifying | Microsoft Docs"
description: "Merhaba Klasik dağıtım modelinde nasıl dosya toochange DNS sunucu ayarları bir sanal ağ yapılandırması'nı kullanarak bir sanal ağdaki"
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
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="9ced6-103">Bir sanal ağ yapılandırma dosyasında DNS ayarlarını belirtme</span><span class="sxs-lookup"><span data-stu-id="9ced6-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="9ced6-104">Bir ağ yapılandırma dosyası toospecify etki alanı adı sistemi (DNS) ayarlarını kullanabileceğiniz iki öğe vardır: **DnsServers** ve **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="9ced6-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="9ced6-105">IP adreslerini belirterek DNS sunucularının bir listesini ekleyin ve başvuru adları toohello **DnsServers** öğesi.</span><span class="sxs-lookup"><span data-stu-id="9ced6-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="9ced6-106">Daha sonra kullanabileceğiniz bir **DnsServerRef** öğesi toospecify hangi DNS sunucusu girdileri hello DnsServers öğeden, sanal ağ içindeki farklı ağ siteleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ced6-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="9ced6-107">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9ced6-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="9ced6-108">Merhaba ağ yapılandırma dosyası öğeleri aşağıdaki hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9ced6-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="9ced6-109">her öğenin Hello başlık değer ayarları hello öğesi hakkında ek bilgi sağlayan bağlantılı tooa sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="9ced6-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ced6-110">Nasıl tooconfigure hello ağ yapılandırma dosyası hakkında daha fazla bilgi için bkz: [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="9ced6-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="9ced6-111">Merhaba ağ yapılandırma dosyasında yer alan her öğe hakkında daha fazla bilgi için bkz: [Azure sanal ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ced6-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="9ced6-112">DNS öğesi</span><span class="sxs-lookup"><span data-stu-id="9ced6-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="9ced6-113">Merhaba **adı** hello özniteliğinde **DnsServer** öğe Merhaba yalnızca başvuru olarak kullanılır **DnsServerRef** öğesi.</span><span class="sxs-lookup"><span data-stu-id="9ced6-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="9ced6-114">Merhaba hello DNS sunucusu için konak adı göstermiyor.</span><span class="sxs-lookup"><span data-stu-id="9ced6-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="9ced6-115">Her **DnsServer** öznitelik değeri benzersiz olmalıdır hello tüm Microsoft Azure aboneliği arasında</span><span class="sxs-lookup"><span data-stu-id="9ced6-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="9ced6-116">Sanal ağ site öğesi</span><span class="sxs-lookup"><span data-stu-id="9ced6-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="9ced6-117">İçinde hello sanal ağ site öğesi için bu ayarı toospecify sipariş, daha önce hello DNS öğesinde tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ced6-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="9ced6-118">Merhaba DnsServerRef *adı* hello sanal ağ siteleri için DnsServer hello DNS öğesinde belirtilen tooa adı değeri öğesi başvurmalıdır *adı*.</span><span class="sxs-lookup"><span data-stu-id="9ced6-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9ced6-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ced6-119">Next steps</span></span>
* <span data-ttu-id="9ced6-120">Merhaba anlamak [Azure sanal ağ yapılandırma şeması](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="9ced6-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="9ced6-121">Merhaba anlamak [Azure hizmet yapılandırma şeması](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="9ced6-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="9ced6-122">[Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="9ced6-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

