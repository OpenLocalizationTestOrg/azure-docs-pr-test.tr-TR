---
title: "aaaViewing ve ana bilgisayar adları değiştirme | Microsoft Docs"
description: "Azure sanal makineleri için tooview ve değişiklik ana bilgisayar adları nasıl web ve çalışan rolleri ad çözümlemesi için"
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
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Görüntüleme ve ana bilgisayar adları değiştirme
tooallow rol örnekleri toobe ana bilgisayar adına göre başvurulan, hello hizmet yapılandırma dosyasında her rol için hello ana bilgisayar adı için başlangıç değerini ayarlamanız gerekir. İstenen hello ana bilgisayar adı toohello ekleyerek bunu **vmName** hello özniteliği **rol** öğesi. Merhaba hello değerini **vmName** özniteliği hello ana bilgisayar adını her rol örneği için temel olarak kullanılır. Örneğin, varsa **vmName** olan *webrole* ve bu rol üç örneği vardır, hello ana bilgisayar adlarını hello örneklerinin olacaktır *webrole0*, *webrole1* , ve *webrole2*. Bir sanal makine için konak adı Hello hello sanal makine adını temel alarak doldurulduğundan toospecify hello yapılandırma dosyası, sanal makineler için bir konak adı gerekmez. Bir Microsoft Azure hizmet yapılandırma hakkında daha fazla bilgi için bkz: [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Ana bilgisayar adları görüntüleme
Merhaba veritabanınızı aşağıdaki araçlardan birini kullanarak bir bulut hizmetinde hello ana bilgisayar adlarını sanal makineler ve rol örnekleri görüntüleyebilirsiniz.

### <a name="azure-portal"></a>Azure Portal
Merhaba kullanabilirsiniz [Azure portal](http://portal.azure.com) hello genel bakış dikey penceresinde bir sanal makine için sanal makineler için tooview hello konak adları. Dikey penceresinde hello unutmayın için bir değer gösterir **adı** ve **ana bilgisayar adı**. Başlangıçta hello olsa aynı hello ana bilgisayar adını değiştirme hello sanal makine veya rol örneğine hello adını değiştirmez.

Rol örnekleri hello Azure portal de görüntülenebilir, ancak bir bulut hizmeti hello durumlarda listelediğinizde hello ana bilgisayar adı görüntülenmez. Her örneği için bir ad görürsünüz, ancak bu ad hello ana bilgisayar adını temsil etmiyor.

### <a name="service-configuration-file"></a>Hizmet yapılandırma dosyası
Merhaba hizmet yapılandırma dosyası dağıtılan bir hizmet için hello indirebilirsiniz **yapılandırma** hello hizmetin dikey penceresinde hello Azure portalı. Merhaba sonra bakabilirsiniz **vmName** özniteliği hello için **rol adı** öğesi toosee hello ana bilgisayar adı. Bu ana bilgisayar adı her rol örneğinin hello ana bilgisayar adı için temel olarak kullanılan aklınızda bulundurun. Örneğin, varsa **vmName** olan *webrole* ve bu rol üç örneği vardır, hello ana bilgisayar adlarını hello örneklerinin olacaktır *webrole0*, *webrole1* , ve *webrole2*.

### <a name="remote-desktop"></a>Uzak Masaüstü
Uzak Masaüstü'nü (Windows), Windows PowerShell uzaktan iletişimini (Windows) veya SSH (Linux ve Windows) bağlantıları tooyour sanal makineleri veya rol örnekleri etkinleştirdikten sonra etkin bir Uzak Masaüstü bağlantı hello ana bilgisayar adından çeşitli şekillerde görüntüleyebilirsiniz:

* Merhaba komut istemi veya SSH terminal ana bilgisayar adını yazın.
* (Yalnızca Windows) tüm hello komut satırında/ipconfig yazın.
* Merhaba sistem görünümü hello bilgisayar adı ayarları (yalnızca Windows).

### <a name="azure-service-management-rest-api"></a>Azure Hizmet Yönetimi REST API'si
Bir REST istemciden aşağıdaki yönergeleri izleyin:

1. Bir istemci sertifikası tooconnect toohello Azure portal olduğundan emin olun. bir istemci sertifikası tooobtain adımları içinde sunulan hello [nasıl yapılır: indirme ve yayımlama ayarları içeri aktarma ve abonelik bilgileri](https://msdn.microsoft.com/library/dn385850.aspx). 
2. X-ms-version değeri 2013-11-01 adlı bir üstbilgi girişi ayarlayın.
3. Biçim aşağıdaki hello bir istek gönderin: https://management.core.windows.net/\<subscrition kimliği\>/services/hostedservices/\<hizmet adı\>? katıştırmak ayrıntı = true
4. Merhaba Ara **ana bilgisayar adı** öğesini her **RoleInstance** öğesi.

> [!WARNING]
> Ayrıca hello iç etki alanı soneki bulut hizmetinizden hello REST çağrısı yanıt için hello denetleyerek görüntüleyebilirsiniz **InternalDnsSuffix** öğesi veya ipconfig çalıştırarak/tüm bir komut isteminden bir Uzak Masaüstü oturumunda (Windows) veya bir SSH terminal (Linux) gelen çalışan kat /etc/resolv.conf.
> 
> 

## <a name="modifying-a-hostname"></a>Bir ana bilgisayar adını değiştirme
Değiştirilen hizmet yapılandırma dosyası karşıya ya da Uzak Masaüstü oturumundan hello bilgisayarı yeniden adlandırma hello ana bilgisayar adı herhangi bir sanal makine veya rol örneği için değiştirebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Ad çözümlemesi (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Azure hizmet yapılandırma şeması (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Azure Virtual Network yapılandırma şeması](http://go.microsoft.com/fwlink/?LinkId=248093)

[Ağ yapılandırma dosyalarını kullanarak DNS ayarlarını belirtin](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

