---
title: "Azure yük dengeleyici için IPv6 aaaOverview | Microsoft Docs"
description: "IPv6 desteği Azure yük dengeleyici ve yük dengeli sanal makineleri anlama."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>IPv6 Azure yük dengeleyici için genel bakış

Internet'e yönelik Yük Dengeleyici, bir IPv6 adresi ile dağıtılabilir. Ayrıca tooIPv4 bağlantısı, bu özellikler aşağıdaki hello sağlar:

* Yerel uçtan uca IPv6 bağlantısı ortak Internet istemcileri ve Azure sanal makineleri (VM'ler) arasında hello yük dengeleyici üzerinden.
* Yerel uçtan uca IPv6 giden bağlantı VM'ler ve ortak Internet IPv6 özellikli istemciler arasında.

Resim aşağıdaki hello Azure yük dengeleyici için hello IPv6 işlevselliği gösterilmektedir.

![IPv6 Azure yük dengeleyici](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Uygulama dağıtıldıktan sonra bir IPv4 veya IPv6 özellikli Internet istemcisi hello ortak IPv4 veya IPv6 adresleri (veya ana bilgisayar adları) hello Azure Internet'e yönelik Yük Dengeleyici ile iletişim kurabilir. Merhaba yük dengeleyici yolların IPv6 paketlerini toohello özel IPv6 adreslerini ağ adresi çevirisi (NAT) kullanarak hello VM'ler hello. Merhaba IPv6 Internet istemcisi doğrudan hello hello VM'ler IPv6 adresini'ile iletişim kuramıyor.

## <a name="features"></a>Özellikler

Azure Resource Manager aracılığıyla dağıtılan VM'ler için yerel IPv6 desteği sağlar:

1. Yük dengeli IPv6 Hizmetleri hello Internet üzerindeki IPv6 istemciler için
2. Yerel IPv6 ve IPv4 uç noktaları vm'lerde ("Yığılmış çift")
3. Gelen ve giden başlatılan yerel IPv6 bağlantılar
4. TCP, UDP ve HTTP (S) gibi desteklenen protokoller eksiksiz bir hizmet mimarileri etkinleştir

## <a name="benefits"></a>Avantajlar

Bu işlev hello aşağıdaki avantajları sağlar:

* Yeni uygulamalar erişilebilir yalnızca tooIPv6 istemcileri olmasını gerektiren karşılayan kamu düzenlemeleri
* Büyüyen mobil & IOT pazarda etkinleştir mobil ve nesnelerin interneti (IOT) geliştiriciler toouse çift yığın (IPv4 + IPv6) Azure sanal makineleri tooaddress hello

## <a name="details-and-limitations"></a>Ayrıntılar ve sınırlamalar

Ayrıntılar

* Hello Azure DNS hizmeti, bir IPv4 ve IPv6 AAAA ad kayıtlarını içerir ve hello yük dengeleyici için her iki kayıt ile yanıt verir. Merhaba istemci ile hangi adresi (IPv4 veya IPv6) toocommunicate seçer.
* VM bir bağlantı tooa ortak Internet IPv6 bağlı cihaz başlattığında hello VM'in IPv6 adresi ağ adresi hello yük dengeleyici (NAT) toohello genel IPv6 adresi çevrilen kaynağıdır.
* Merhaba Linux işletim sistemi çalıştıran VM'ler yapılandırılmış tooreceive DHCP aracılığıyla bir IPv6 IP adresi olmalıdır. Merhaba Linux Azure Galerisi olan zaten hello görüntülerinde çoğunu toosupport IPv6 değişiklik yapmadan yapılandırılmış. Daha fazla bilgi için bkz: [yapılandırma DHCPv6 Linux VM'ler](load-balancer-ipv6-for-linux.md)
* Seçerseniz bir sistem durumu araştırma, yük dengeleyici ile toouse bir IPv4 araştırması oluşturup hello IPv4 ve IPv6 uç noktaları ile kullanabilirsiniz. VM Hello hizmette kullanılamaz hale gelirse hello IPv4 ve IPv6 uç noktalar dışında döndürme alınır.

Sınırlamalar

* IPv6 Yük Dengeleme kuralları hello Azure portal ekleyemezsiniz. Merhaba kuralları yalnızca CLI, PowerShell gibi hello şablonu aracılığıyla oluşturulabilir.
* Var olan sanal makineleri toouse IPv6 adreslerini yükseltme değil. Yeni VM'ler dağıtmanız gerekir.
* Tek bir IPv6 adresi her VM tooa tek ağ arabirimine atanabilir.
* Merhaba genel IPv6 adresi tooa VM atanamaz. Tooa yük dengeleyici yalnızca atanabilir.
* Merhaba ters DNS araması, genel IPv6 adresleri için yapılandıramazsınız.
* Merhaba VM'ler hello IPv6 adresleri ile bir Azure bulut hizmeti üyesi olamaz. Bağlı tooan Azure sanal ağ (VNet) olması ve IPv4 adresleri birbirleriyle iletişim.
* Özel IPv6 adresleri, bir kaynak grubunda tek tek sanal makineleri üzerinde dağıtılabilir ancak ölçek kümeleri aracılığıyla bir kaynak grubuna dağıtılamıyor.
* Azure VM'ler, IPv6 tooother VM'ler, diğer Azure hizmetlerine veya şirket içi cihazlar bağlanamıyor. Bunlar yalnızca hello Azure yük dengeleyici ile IPv6 üzerinden iletişim kurabilir. Ancak, IPv4 kullanarak bu diğer kaynaklarla iletişim kurabilir.
* Ağ güvenlik grubu (NSG) koruma IPv4 için ikili yığını (IPv4 + IPv6) dağıtımlarda desteklenir. Nsg'ler toohello IPv6 uç noktaları geçerli değildir.
* VM değil hello Hello IPv6 uç noktada kullanıma doğrudan toohello Internet. Bir yük dengeleyicinin arkasına olur. Yalnızca hello bağlantı noktalarını Hello yük dengeleyici kurallarında belirtilen IPv6 üzerinden erişilebilir.
* Değiştirme hello IdleTimeout parametre IPv6 için **şu anda desteklenmiyor**. Merhaba, dört dakika varsayılandır.
* Değiştirme hello loadDistributionMethod parametresi IPv6 için **şu anda desteklenmiyor**.
* Ayrılan IPv6 IP'leri (burada Ipallocationmethod statik =) olan **şu anda desteklenmiyor**.

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl toodeploy IPv6 olan yük dengeleyici.

* [Bölgeye göre IPv6 kullanılabilirliği](https://go.microsoft.com/fwlink/?linkid=828357)
* [Bir şablonu kullanarak bir yük dengeleyici IPv6 ile dağıtma](load-balancer-ipv6-internet-template.md)
* [Azure PowerShell kullanarak bir yük dengeleyici IPv6 ile dağıtma](load-balancer-ipv6-internet-ps.md)
* [Azure CLI kullanarak bir yük dengeleyici IPv6 ile dağıtma](load-balancer-ipv6-internet-cli.md)
