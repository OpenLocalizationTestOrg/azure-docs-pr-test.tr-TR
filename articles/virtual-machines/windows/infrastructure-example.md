---
title: "aaaExample Azure altyapı gözden geçirme | Microsoft Docs"
description: "Bir örnek altyapısını Azure'a dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a>Windows VM'ler için örnek Azure altyapı gözden geçirme

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede örnek uygulama altyapısı oluşturmaya anlatılmaktadır. Biz tüm hello yönergeleri ve adlandırma kuralları, kullanılabilirlik kümeleri, sanal ağlar ve yük dengeleyici kararları bir araya getirir basit bir çevrimiçi mağaza için bir altyapı tasarlama ve gerçekte sanal makineleri (VM'ler) dağıtma ayrıntılı olarak açıklanmaktadır.

## <a name="example-workload"></a>Örnek iş yükü
Adventure Works Cycles toobuild bir çevrimiçi mağaza uygulamasına oluşan Azure istiyor:

* Bir web katmanı ön uç Hello istemci çalıştıran iki IIS sunucuları
* Veri ve uygulama katmanına siparişler işleme iki IIS sunucuları
* Ürün veri ve siparişler bir veritabanı katmanı depolamak için AlwaysOn Kullanılabilirlik grupları (iki SQL sunucuları ve Çoğunluk düğüm tanığı) ile iki Microsoft SQL Server örnekleri
* Müşteri hesapları ve bir kimlik doğrulama katmanı sağlayıcıları için iki Active Directory etki alanı denetleyicisi
* Tüm hello sunucuları iki alt ağ içinde bulunur:
  * Merhaba web sunucuları için ön uç bir alt ağ 
  * Merhaba uygulama sunucuları, SQL kümesi ve etki alanı denetleyicileri için bir arka uç alt ağ

![Uygulama altyapısı için farklı katmanlara diyagramı](./media/infrastructure-example/example-tiers.png)

Güvenli gelen web trafiği olması hello web sunucuları arasında Yük Dengelemesi müşteriler hello çevrimiçi mağaza göz atın. Merhaba biçiminde hello Web sunucuları hello uygulama sunucuları arasında dengelenmelidir HTTP isteklerini işleme trafiği sipariş. Ayrıca, hello altyapı yüksek kullanılabilirlik için tasarlanmış olması gerekir.

Merhaba elde edilen tasarım eklemeniz gerekir:

* Bir Azure aboneliği ve hesabı
* Tek bir kaynak grubu
* Azure Yönetilen Diskleri
* İki alt ağa sahip bir sanal ağ
* Merhaba VM'ler ile benzer bir rolü için kullanılabilirlik kümeleri
* Sanal makineler

Yukarıdaki tüm hello adlandırma kurallarına izleyin:

* Adventure Works Cycles kullandığı **[BT iş yükü]-[konum]-[Azure kaynak]** öneki olarak
  * Bu örneğin, "**azos**" (Azure çevrimiçi mağaza) iş yükü adı hello ve "**kullanmak**" (Doğu ABD 2) hello konumudur
* Sanal ağları kullanın AZOS kullanım VN**[sayı]**
* Kullanılabilirlik kümeleri kullanan azos-kullanın-olarak-**[rol]**
* Sanal makine adları azos kullanın-kullanın-vm -**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Azure abonelikleri ve hesapları
Adventure Works Cycles, Adventure Works Kurumsal abonelik, bu BT iş yükü için faturalama tooprovide adlı kurumsal aboneliğini kullanıyor.

## <a name="storage"></a>Depolama
Adventure Works Cycles Azure yönetilen diskleri kullanması gerektiğini belirledi. Sanal makineleri oluştururken, her iki depolama kullanılabilir depolama katmanları kullanılır:

* **Standart depolama** hello web sunucuları, uygulama sunucuları ve etki alanı denetleyicileri ve kendi veri diskleri için.
* **Premium depolama** hello SQL Server VM'ler ve kendi veri diskleri için.

## <a name="virtual-network-and-subnets"></a>Sanal ağ ve alt ağlar
Merhaba sanal ağ sürekli bağlantı toohello Adventure iş döngüsü şirket içi ağ gerekmediği için bir yalnızca bulut sanal ağda karar verdi.

Bunlar yalnızca bulut sanal ağ ayarlarını hello Azure portal kullanarak aşağıdaki hello ile oluşturulan:

* Name: Kullanım AZOS VN01
* Konumu: Doğu ABD 2
* Sanal ağ adres alanı: 10.0.0.0/8
* İlk alt ağ:
  * Ad: ön uç
  * Adres alanı: 10.0.1.0/24
* İkinci alt ağ:
  * Ad: arka uç
  * Adres alanı: 10.0.2.0/24

## <a name="availability-sets"></a>Kullanılabilirlik kümeleri
Adventure Works Cycles dört kullanılabilirlik kümesi üzerinde kampanyanızın çevrimiçi kendi deposunun tüm dört katmanların toomaintain yüksek kullanılabilirlik:

* **web olarak azos kullanım** hello web sunucuları için
* **uygulama olarak azos kullanım** hello uygulama sunucuları için
* **sql olarak azos kullanım** hello SQL sunucuları için
* **dc olarak azos kullanım** hello etki alanı denetleyicileri için

## <a name="virtual-machines"></a>Sanal makineler
Adventure Works Cycles Azure Vm'leri için adlarından hello karar:

* **Kullanım vm web01 azos** hello ilk web sunucusu için
* **Kullanım vm web02 azos** hello ikinci web sunucusu için
* **Kullanım vm app01 azos** hello ilk uygulama sunucusu için
* **Kullanım vm app02 azos** hello ikinci uygulama sunucusu için
* **Kullanım vm sql01 azos** hello küme hello ilk SQL Server sunucusu için
* **Kullanım vm sql02 azos** hello küme hello ikinci SQL Server sunucusu için
* **Kullanım vm dc01 azos** hello ilk etki alanı denetleyicisi için
* **Kullanım vm dc02 azos** hello ikinci etki alanı denetleyicisi için

Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.

![Azure üzerinde dağıtılan son uygulama altyapısı](./media/infrastructure-example/example-config.png)

Bu yapılandırma bir araya getirir:

* Bir yalnızca bulut sanal ağla iki alt ağ (ön uç ve arka uç)
* Azure yönetilen diskleri standart ve Premium diskleri
* Bir hello çevrimiçi deposunun her katman için dört kullanılabilirlik kümeleri
* Merhaba dört katmanları için Hello sanal makineler
* Bir dış yük dengeli küme hello Internet toohello web sunucularından HTTPS tabanlı web trafiği için
* Bir iç yük dengeli küme hello web sunucuları toohello uygulama sunucularından şifrelenmemiş web trafiği için
* Tek bir kaynak grubu