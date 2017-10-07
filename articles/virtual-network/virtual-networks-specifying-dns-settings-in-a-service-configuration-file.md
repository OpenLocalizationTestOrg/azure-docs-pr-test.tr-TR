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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Bir hizmet yapılandırma dosyasında DNS ayarlarını belirtme
## <a name="dns-elements"></a>DNS öğeleri
Hizmet yapılandırma dosyası hello hizmetini kullanacak olan hello etki alanı adı sistemi (DNS) sunucuları için IPv4 adresleri listesi olan bir DnsServers öğesi içerebilir. Merhaba hizmet yapılandırma dosyası ayarlarında ayarları hello ağ yapılandırma dosyasında daha önceliklidir. Daha fazla bilgi için bkz: [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**NetworkConfiguration öğesi**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Merhaba **adı** hello özniteliğinde **DnsServer** öğe yalnızca bir başvuru adı kullanılır. Merhaba hello DNS sunucusu için konak adı göstermiyor. Her **DnsServer** öznitelik değeri benzersiz olmalıdır hello tüm Microsoft Azure aboneliği arasında.
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Azure hizmet yapılandırma şeması (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Azure Virtual Network yapılandırma şeması](http://go.microsoft.com/fwlink/?LinkId=248093)

[Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma](http://go.microsoft.com/fwlink/?LinkId=248094)

[Merhaba Yönetim Portalı sanal ağ ayarları hakkında](http://go.microsoft.com/fwlink/?LinkId=248092)

