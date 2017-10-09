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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Bir sanal ağ yapılandırma dosyasında DNS ayarlarını belirtme
Bir ağ yapılandırma dosyası toospecify etki alanı adı sistemi (DNS) ayarlarını kullanabileceğiniz iki öğe vardır: **DnsServers** ve **DnsServerRef**. IP adreslerini belirterek DNS sunucularının bir listesini ekleyin ve başvuru adları toohello **DnsServers** öğesi. Daha sonra kullanabileceğiniz bir **DnsServerRef** öğesi toospecify hangi DNS sunucusu girdileri hello DnsServers öğeden, sanal ağ içindeki farklı ağ siteleri için kullanılır.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Klasik dağıtım modeli yer almaktadır.

Merhaba ağ yapılandırma dosyası öğeleri aşağıdaki hello içerebilir. her öğenin Hello başlık değer ayarları hello öğesi hakkında ek bilgi sağlayan bağlantılı tooa sayfasıdır.

> [!IMPORTANT]
> Nasıl tooconfigure hello ağ yapılandırma dosyası hakkında daha fazla bilgi için bkz: [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md). Merhaba ağ yapılandırma dosyasında yer alan her öğe hakkında daha fazla bilgi için bkz: [Azure sanal ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[DNS öğesi](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Merhaba **adı** hello özniteliğinde **DnsServer** öğe Merhaba yalnızca başvuru olarak kullanılır **DnsServerRef** öğesi. Merhaba hello DNS sunucusu için konak adı göstermiyor. Her **DnsServer** öznitelik değeri benzersiz olmalıdır hello tüm Microsoft Azure aboneliği arasında
> 
> 

[Sanal ağ site öğesi](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> İçinde hello sanal ağ site öğesi için bu ayarı toospecify sipariş, daha önce hello DNS öğesinde tanımlanmalıdır. Merhaba DnsServerRef *adı* hello sanal ağ siteleri için DnsServer hello DNS öğesinde belirtilen tooa adı değeri öğesi başvurmalıdır *adı*.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba anlamak [Azure sanal ağ yapılandırma şeması](http://go.microsoft.com/fwlink/?LinkId=248093).
* Merhaba anlamak [Azure hizmet yapılandırma şeması](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Ağ yapılandırma dosyalarını kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md).

