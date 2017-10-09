---
title: "bir Azure ağı erişim denetimi listesi aaaWhat mi?"
description: "Azure'daki erişim denetim listeleri hakkında bilgi edinin"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Bir uç noktası erişim denetimi listesi nedir?

> [!IMPORTANT]
> Azure sahip iki farklı [dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) oluşturmak ve kaynaklarla çalışmak için: Resource Manager ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager dağıtım modeli kullanmanızı önerir. 

Bir uç noktası erişim denetimi listesi (ACL) Azure dağıtımınız için kullanılabilir bir güvenlik yeniliktir. Bir ACL veya bir sanal makine uç noktası için trafiği reddetmeye hello özelliği tooselectively izin sağlar. Bu paket filtreleme özelliği, ek bir güvenlik katmanı sağlar. Yalnızca uç noktaları için ağ ACL'leri belirtebilirsiniz. Bir sanal ağ veya bir sanal ağda bulunan belirli bir alt ağ için bir ACL belirtemezsiniz. ACL'ler yerine, mümkün olduğunda toouse ağ güvenlik grupları (Nsg'ler) önerilir. toolearn Nsg'ler, hakkında daha fazla bilgi görmek [ağ güvenlik grubu genel bakış](virtual-networks-nsg.md)

ACL, PowerShell veya hello Azure portalı kullanılarak yapılandırılabilir. tooconfigure PowerShell kullanarak bir ağ ACL bkz [yönetme erişim denetim listeleri için PowerShell kullanarak uç noktaları](virtual-networks-acl-powershell.md). tooconfigure kullanarak bir ağ ACL hello Azure portal, bkz: [nasıl tooset uç noktaları tooa sanal makineyi](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Ağ ACL'leri kullanarak bunu yapabilirsiniz hello aşağıdaki:

* Seçmeli olarak izin vermek veya uzak alt IPv4 adres aralığı tooa sanal makine giriş uç noktası göre gelen trafiği engelle.
* Kara liste IP adresleri
* Sanal makine uç noktası başına birden çok kural oluşturma
* Tooensure hello doğru kuralları kümesi bir belirtilen sanal makine uç noktası (en düşük toohighest) üzerinde uygulanan sıralama kuralı kullanın
* Belirli bir uzak alt IPv4 adresi için bir ACL belirtin.

Merhaba bkz [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) ACL sınırları için makale.

## <a name="how-acls-work"></a>ACL'ler nasıl çalışır
Bir ACL kuralları listesini içeren bir nesnedir. Bir ACL oluşturmak ve tooa sanal makine uç noktası geçerli olduğunda, paket filtreleme hello ana bilgisayar düğümündeki VM gerçekleşir. Başka bir deyişle, uzak IP adreslerinden gelen hello trafiğine hello ana bilgisayar düğümü yerine eşleşen ACL kuralları, VM için filtrelenir. Bu, VM paket filtreleme hello değerli CPU döngülerini harcama önler.

Bir sanal makine oluşturulduğunda, varsayılan bir ACL tüm gelen trafiği yer tooblock yerleştirilir. (3389 bağlantı noktası için) bir uç nokta oluşturduysanız, ancak ardından ACL hello varsayılan tooallow Bu uç nokta için tüm gelen trafiği değiştirdi. Uzak bir alt ağdan gelen trafiği sonra toothat endpoint izin verilir ve hiçbir güvenlik duvarı sağlama gereklidir. Uç noktalar için bu bağlantı noktalarını oluşturulan sürece diğer tüm bağlantı noktalarına gelen trafik için engellenir. Giden trafik, varsayılan olarak izin verilir.

**Örnek varsayılan ACL tablo**

| **Kuralı #** | **Uzak alt ağ** | **Uç noktası** | **İzin ver ve Reddet** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |İzin ver |

## <a name="permit-and-deny"></a>İzin ve reddetme
Seçmeli olarak izin vermek veya "izin ver" belirten kuralları veya "Reddet" oluşturarak sanal makine giriş uç noktası için ağ trafiğini engellemek. Bir uç noktası oluşturulduğunda, varsayılan olarak, toohello endpoint tüm trafiğe izin verildiğini önemli toonote olur. Bu nedenle, toounderstand nasıl toocreate izin verme/reddetme kurallarını ve hello ağ üzerinde ayrıntılı denetim isterseniz, bunları hello uygun öncelik sırasına göre yerleştirmek trafiği, önemli tooallow tooreach hello sanal makine uç noktası seçin.

Noktaları tooconsider:

1. **Hiçbir ACL –** bir uç noktası oluşturulduğunda, varsayılan olarak biz tüm hello uç noktası için izin verir.
2. **İzin ver -** bir veya daha fazla "izin ver" aralıkları eklediğinizde, varsayılan olarak tüm aralıklarını engelleme. Yalnızca IP aralığı izin verilen hello paketler hello sanal makine uç noktası ile mümkün toocommunicate olacaktır.
3. **Reddetme -** bir veya daha fazla "Reddet" aralıkları eklediğinizde, varsayılan olarak tüm trafiği aralıklarına vermiş olursunuz.
4. **İzin verme ve reddetme - birleşimi** aralığı izin verilen veya reddedilen toobe "belirli bir IP çıkışı toocarve istediğinizde reddet" ve "izin ver" bir birleşimini kullanabilirsiniz.

## <a name="rules-and-rule-precedence"></a>Kurallar ve kural önceliği
Ağ ACL'leri belirli bir sanal makine uç noktalarda ayarlanabilir. Örneğin, bir sanal makineye hangi kilitleri erişim tuşunu belirli IP adresleri oluşturulan bir RDP uç noktası için ACL ağ belirtebilirsiniz. Merhaba tabloda gösterir şekilde toogrant erişim toopublic belirli aralığı toopermit erişim RDP sanal IP (VIP). Diğer uzak IP'leri engellenir. Biz izleyin bir *en düşük öncelik kazanır* kural sırası.

### <a name="multiple-rules"></a>Birden çok kural
Yalnızca iki ortak IPv4 adres aralıklarından (65.0.0.0/8 ve 159.0.0.0/8), tooallow erişim toohello RDP uç noktası istiyorsanız hello aşağıdaki örnekte, bu iki belirterek elde edebilirsiniz *izin* kuralları. Bu durumda, varsayılan olarak bir sanal makine için RDP oluşturulduğundan, erişim toohello RDP bağlantı noktası uzak bir alt ağa datalı aşağı toolock isteyebilirsiniz. Merhaba aşağıdaki örnek gösterir şekilde toogrant erişim toopublic belirli aralığı toopermit erişim RDP sanal IP (VIP). Diğer uzak IP'leri engellenir. Bu, belirli bir sanal makine uç noktası için ağ ACL'leri ayarlanabilir ve varsayılan olarak erişimi reddedilir çünkü çalışır.

**Örnek – birden çok kural**

| **Kuralı #** | **Uzak alt ağ** | **Uç noktası** | **İzin ver ve Reddet** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |İzin ver |
| 200 |159.0.0.0/8 |3389 |İzin ver |

### <a name="rule-order"></a>Kural sırası
Birden çok kural için bir uç nokta belirtilebilir çünkü hangi kuralın önceliklidir sipariş toodetermine içinde bir şekilde tooorganize kuralları olmalıdır. Merhaba kural sırası önceliği belirtir. ACL'ler izleyin ağ bir *en düşük öncelik kazanır* kural sırası. Merhaba aşağıdaki örnekte, bağlantı noktası 80 üzerinde hello endpoint erişim tooonly seçmeli olarak verilen belirli IP adresi aralıkları. tooconfigure Bu, bir reddetme kuralı sahibiz (kural \# 100) hello 175.1.0.1/24 alan adres. İkinci bir kural sonra öncelik verir diğer adresler 175.0.0.0/8 altında tooall erişim 200 ile belirtilir.

**Örnek – kural önceliği**

| **Kuralı #** | **Uzak alt ağ** | **Uç noktası** | **İzin ver ve Reddet** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Reddet |
| 200 |175.0.0.0/8 |80 |İzin ver |

## <a name="network-acls-and-load-balanced-sets"></a>Ağ ACL'leri ve yük dengeli ayarlar
Ağ ACL'leri bir yük dengeli kümesi uç noktasında belirtilebilir. Yük dengelenmiş bir küme için bir ACL belirtilirse, hello ACL uygulanan tooall sanal makine bu yük dengelenmiş küme ağdır. Örneğin, "Bağlantı noktası 80" Yük dengelenmiş bir küme oluşturulur ve 3 VM'ler, "VM otomatik olarak ayarlanır birini bağlantı noktası 80" noktadaki ACL oluşturulan hello ağ hello yük dengelenmiş küme içeriyorsa toohello diğer VM'ler uygulayın.

![Ağ ACL'leri ve yük dengeli ayarlar](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Sonraki Adımlar
[PowerShell kullanarak uç noktalar için erişim denetim listeleri yönetme](virtual-networks-acl-powershell.md)

