---
title: "aaaVPN ağ geçidi Klasik tooResource Yöneticisi geçiş | Microsoft Docs"
description: "Bu sayfa hello VPN ağ geçidi Klasik tooResource Yöneticisi geçiş genel bir bakış sağlar."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>VPN ağ geçidi Klasik tooResource Manager geçişi
VPN ağ geçitleri şimdi Klasik tooResource Yöneticisi dağıtım modelinden geçirilebilir. Daha fazla bilgiyi Azure Kaynak Yöneticisi hakkında [özellikler ve sunduğu yararlar](../azure-resource-manager/resource-group-overview.md). Bu makalede, nasıl toomigrate Klasik dağıtımlar toonewer Kaynak Yöneticisi'nden tabanlı modeli detaylandırır. 

VPN ağ geçitleri, sanal ağ geçişini Klasik tooResource Yöneticisi bir parçası olarak geçirilir. Bu geçiş bir kerede bir VNet yapılır. Araçlar veya önkoşul toomigration açısından ek gereksinimi yoktur. Geçiş adımları aynı tooexisting VNet geçiş işlemleri ve adresinde belgelenen [Iaas kaynaklar geçiş sayfası](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Geçiş sırasında hiçbir veri yolu kapalı kalma süresi olduğunu ve bu nedenle var olan iş yükleri şirket içi bağlantı kaybı olmadan toofunction geçiş sırasında devam eder. hello Hello VPN ağ geçidi ile ilişkili ortak IP adresi hello geçiş işlemi sırasında değiştirmez. Bu, hello geçiş tamamlandıktan sonra tooreconfigure'ı şirket içi yönlendiricinizi gerekmez anlamına gelir.  

Kaynak Yöneticisi'nde Hello modeli Klasik modelinden farklıdır ve sanal ağ geçitleri, yerel ağ geçitleri ve bağlantı kaynaklarını oluşur. Bunlar hello VPN ağ geçidi kendisini temsil eder, yerel site hello iki arasında bağlantı ve şirket içi adres alanı üzerinde sırasıyla temsil eden hello. Geçiş tamamlandıktan sonra ağ geçitleri Klasik modelde kullanılabilir olmaz ve Resource Manager modelini kullanarak sanal ağ geçitleri, yerel ağ geçitleri ve bağlantı nesneleri tüm yönetim işlemlerinin gerçekleştirilmesi gerekir.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
En yaygın VPN bağlantısı senaryoları Klasik tooResource Yöneticisi geçiş tarafından ele alınmıştır. desteklenen hello senaryolar da dahil-

* Bağlantı noktası toosite
* VPN ağ geçidi ile site toosite bağlantı tooon şirket içi konumuna bağlı
* VPN ağ geçitleri kullanarak iki Vnet arasında VNet tooVNet bağlantısı
* Şirket içi konumunda toosame birden çok sanal ağlara bağlı
* Çok siteli bağlantı
* Zorlamalı tünel sanal ağlar etkin

Desteklenmeyen senaryolar da dahil-  

* Sanal ağ ExpressRoute ağ geçidi ve VPN ağ geçidi ile şu anda desteklenmiyor.
* VM uzantıları bağlı tooon içi sunucularının olduğu senaryolar geçiş. Transit VPN bağlantısı sınırlamalar aşağıda açıklanmıştır.

> [!NOTE]
> Resource Manager modelinde CIDR doğrulama klasik bir başlangıç daha katı modelidir. Geçirmeden önce Klasik adres aralıklarını verilen hello geçiş işlemine başlamadan önce toovalid CIDR biçimi uygun emin olun. CIDR tüm ortak CIDR doğrulayıcıları kullanılarak doğrulanabilir. VNet veya geçişi olduğunda geçersiz CIDR aralıkları ile yerel siteleri başarısız durumda neden olur.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>VNet tooVNet bağlantısı geçiş
Klasik VNet tooVNet bağlantısı elde hello gösterimini VNet bağlı bir yerel site oluşturarak. Müşteriler, toobe gerekli iki sanal ağlar birbirlerine bağlı hello temsil gerekli toocreate iki yerel site yoktu. Bunlar bundan sonra iki sanal ağlar hello sanal ağlar arasında IPSec tünel tooestablish bağlantısı kullanarak karşılık gelen bağlı toohello. Bir sanal ağ adres aralığı değişiklikler de hello karşılık gelen yerel site gösterimi korunmalıdır beri bu modeli yönetilebilirlik sorunları vardır. Resource Manager modelinde, bu geçici çözüm artık gerekli değildir. iki Vnet doğrudan bağlantı kaynağında 'Vnet2Vnet' bağlantı türü kullanılarak sağlanabilir hello arasındaki Hello bağlantı. 

![Sanal ağ ekran tooVNet geçiş.](./media/vpn-gateway-migration/migration1.png)

Bağlı varlık hello biz algılamak VNet geçiş sırasında toocurrent sanal ağınızın VPN ağ geçidi başka bir VNet olduğunu ve her iki sanal ağlar, geçiş tamamlandıktan sonra artık hello temsil eden iki yerel site diğer Vnet'in görür emin olun. Merhaba Klasik iki VPN ağ geçitleri, iki yerel site ve aralarında iki bağlantı dönüştürülmüş tooResource Yöneticisi modeliyle iki VPN ağ geçitleri ve iki bağlantı türü Vnet2Vnet modelidir.

## <a name="transit-vpn-connectivity"></a>Transit VPN bağlantısı
VPN ağ geçitleri bir VNet için şirket içi bağlantı tooanother doğrudan bağlı tooon içi VNet bağlanarak gerçekleştirilir gibi bir topolojisinde yapılandırabilirsiniz. İlk VNet durumlarda doğrudan bağlı tooon içi bağlı VNet transit toohello VPN ağ geçidi aracılığıyla bağlı tooon içi kaynaklara nerede transit VPN bağlantısı budur. tooachieve Klasik dağıtım modeli Bu yapılandırmada, iki bağlı hello VNet ve şirket içi adres alanını temsil eden önekleri toplanan bir yerel site toocreate gerekir. Bağlı toohello VNet tooachieve transit sonra bağlantı bu temsili yerel sitedir. Şirket içi adres aralığındaki herhangi bir değişiklik, sanal ağ ve şirket içi bir hello toplamasını temsil eden hello yerel sitesinde korunmalıdır beri bu Klasik modeli benzer yönetilebilirlik güçlükler de vardır. Resource Manager'ın desteklenen ağ geçidi BGP desteği giriş Hello bağlı ağ geçitleri şirket içi el ile değiştirilmesi tooprefixes olmadan yolları öğrenebilirsiniz yönetilebilirlik kolaylaştırır.

![Transit yönlendirme senaryosu ekran görüntüsü.](./media/vpn-gateway-migration/migration2.png)

Biz yerel siteleri gerek kalmadan VNet tooVNet bağlantı dönüştürme beri hello geçiş senaryosu dolaylı olarak bağlantılı tooon içi VNet için şirket içi bağlantı kaybeder. Merhaba bağlantı kaybı iki yoldan aşağıdaki hello azaltılabilir geçiş tamamlandıktan sonra - 

* BGP, birbirine bağlı olan VPN ağ geçitleri ve tooon içi etkinleştirin. Yollar hakkında bilgi edindiniz ve sanal ağ geçitleri arasında tanıtılan beri BGP etkinleştirme bağlantısı herhangi bir yapılandırma değişikliği olmadan geri yükler. BGP seçeneği yalnızca standart ve daha yüksek SKU'larında kullanılabilir olduğunu unutmayın.
* Etkilenen VNet toohello yerel ağ geçidi şirket içi konumu temsil eden bir açık bağlantısı kurun. Bu ayrıca hello şirket içi yönlendirici toocreate yapılandırmasına değiştirilmesini gerektiren ve hello IPSec tüneli yapılandırın.

## <a name="next-steps"></a>Sonraki adımlar
VPN ağ geçidi geçiş desteği hakkında daha fazla bilgi sonra çok Git[Klasik tooResource Yöneticisi Iaas kaynaklardan platform desteklenen geçişini](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget başlatıldı.

