---
title: "Yük Dengeleyici için Azure Resource Manager desteği | Microsoft Docs"
description: "Azure Resource Manager ile yük dengeleyici için PowerShell kullanma. Yük Dengeleyici için şablonları kullanma"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Azure Kaynak Yöneticisi desteği Azure yük dengeleyici ile kullanma

Azure Resource Manager Azure Hizmetleri için tercih edilen Yönetim çerçevedir. Azure yük dengeleyici, Azure Resource Manager tabanlı API'ler ve araçlar kullanılarak yönetilebilir.

## <a name="concepts"></a>Kavramlar

Resource Manager ile Azure yük dengeleyici aşağıdaki alt kaynakları içerir:

* Ön uç IP yapılandırmasını –, aksi halde sanal IP (VIP) bilinen bir veya daha fazla ön uç IP adresi bir yük dengeleyici içerebilir. Bu IP adresleri trafik için bir giriş işlevi görür.
* Arka uç adres havuzu – bu sanal makine ağ arabirim kartı (yük dağıtılacak NIC ile) ilişkili IP adresleridir.
* Yük Dengeleme kuralları – bir kural özelliğine verilen ön uç IP ve bağlantı noktası bileşimi için bir arka uç IP adresleri kümesini ve bağlantı noktası bileşimi eşler. Tek bir yük dengeleyici birden çok dengeleme kuralına sahip olabilir. Her kural, bir ön uç IP’si ile bağlantı noktasının ve arka uç IP’si ile VM’lerle ilişkilendirilmiş bağlantı noktasının birleşiminden oluşur.
* Araştırmalar – araştırmalar VM örnekleri durumunu izlemenize olanak sağlar. VM örneği bir sistem durumu araştırması başarısız olursa, döndürme dışında otomatik olarak gerçekleştirilecek.
* Gelen NAT kuralları – NAT kuralları önde gelen trafiği tanımlama IP sonlandırmak ve arka uç IP dağıtılır.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Hızlı başlangıç şablonları

Azure Resource Manager, uygulamalarınızı bildirim temelli bir şablon aracılığıyla sağlamanıza olanak tanır. Tek bir şablonda birden çok hizmeti bağımlılıklarıyla birlikte dağıtabilirsiniz. Uygulama yaşam döngüsünün her aşamasında uygulamanızı tekrar tekrar dağıtmak için aynı şablonu kullanırsınız.

Şablonları sanal makineler, sanal ağlar, kullanılabilirlik kümeleri, ağ arabirimlerine (NIC'ler), depolama hesapları, yük dengeleyici, ağ güvenlik grupları ve genel IP'ler için tanımları içerir. Şablonları ile karmaşık bir uygulama için gereksinim duyduğunuz her şeyi oluşturabilirsiniz. Şablon dosyası, sürüm denetimi ve işbirliği için içerik yönetim sistemi içine denetlenebilir.

[Şablonlar hakkında daha fazla bilgi edinin](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Ağ kaynakları hakkında daha fazla bilgi edinin](../virtual-network/resource-groups-networking.md)

Azure yük dengeleyici kullanarak hızlı başlangıç şablonlarını bulunabilir bir [GitHub deposunu](https://github.com/Azure/azure-quickstart-templates) oluşturulan topluluk şablonları kümesi barındırma.

Şablonları örnekleri:

* [Bir yük dengeleyici ve Yük Dengeleme kuralları içinde 2 VM](http://go.microsoft.com/fwlink/?LinkId=544799)
* [Bir iç yük dengeleyici ve yük dengeleyici kuralları sahip bir VNET içinde 2 VM](http://go.microsoft.com/fwlink/?LinkId=544800)
* [Bir yük dengeleyici içinde 2 VM üzerinde LB NAT kuralları yapılandırın](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>PowerShell veya CLI ile Azure yük dengeleyici ayarlama

Azure Resource Manager cmdlet'leri, komut satırı araçları ve REST API'leri kullanmaya başlama

* [Azure ağı cmdlet'lerini](https://msdn.microsoft.com/library/azure/mt163510.aspx) bir yük dengeleyici oluşturmak için kullanılabilir.
* [Azure Kaynak Yöneticisi'ni kullanarak bir yük dengeleyici oluşturma](load-balancer-get-started-ilb-arm-ps.md)
* [Azure kaynak yönetimi ile Azure CLI kullanma](../xplat-cli-azure-resource-manager.md)
* [Yük Dengeleyici REST API'leri](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Sonraki adımlar

Ayrıca [Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md) ve ne tür yapılandırma [dağıtım modu](load-balancer-distribution-mode.md) belirli yük dengeleyici ağ trafiği davranışı için.

Nasıl yöneteceğinizi öğrenmek [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md). Uygulamanızı bir yük dengeleyicinin arkasındaki sunucular için bağlantıları canlı gerektiğinde, bu önemlidir.
