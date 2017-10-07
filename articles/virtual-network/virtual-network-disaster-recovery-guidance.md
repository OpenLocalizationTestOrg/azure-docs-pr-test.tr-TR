---
title: "Azure sanal ağlar etkileyen bir Azure hizmet kesintisi hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure sanal ağlar etkileyen bir Azure hizmet kesintisi hello olayı içinde hangi toodo öğrenin."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Sanal ağ – iş sürekliliği
## <a name="overview"></a>Genel Bakış
Bir sanal ağ (VNet) hello bulut ağınızdaki mantıksal bir gösterimidir. Kendi özel IP adres alanı ve segment hello alt ağ toodefine sağlar. Sanal ağlar işlem kaynaklarınızı Azure sanal makineler ve bulut Hizmetleri (web/çalışan rolleri) gibi bir güven sınırı toohost görev yapar. VNet içinde barındırılan hello kaynaklar arasında doğrudan özel IP iletişim sağlar. Bir sanal ağ bağlantılı tooan şirket içi ağ üzerinden bir VPN ağ geçidi veya ExpressRoute gibi hello karma seçeneklerden birini de olabilir.

Bir VNet hello bir bölge kapsamında oluşturulur. İki farklı bölgelerdeki aynı adres alanı ile sanal ağlar oluşturabilirsiniz (yani BİZE Doğu ve Batı ABD bunları tooone bağlanamıyor, ancak başka bir doğrudan). 

## <a name="business-continuity"></a>İş Sürekliliği
Uygulamanızı kesintiye birkaç farklı yolu olabilir. Belirli bir bölgedeki tooa doğal afet veya birden çok aygıt/hizmetlerini tooa hatası nedeniyle kısmi bir olağanüstü durum nedeniyle tamamen kesilebilir. Merhaba VNet hizmeti Hello etkisini her bu durumlarda farklıdır.

**S: bir kesinti tooan tüm bölgeyi hello olayda ne yapacaksınız? yani bir bölge tooa doğal afet tamamen kesme ise? Sanal ağlar hello bölgede barındırılan toohello ne olur?**

Y: hello sanal ağ ve hello kaynaklarında hello bölge kalır hello hizmet kesintisi hello süre boyunca erişilemez etkilenen.

![Basit sanal ağ diyagramı](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**S: neler yapabilirim toodo yeniden oluşturma, farklı bir bölgede aynı sanal ağ hello?**

Y: sanal ağ (VNet) oldukça basit kaynaktır. Azure API toocreate VNet çağırabileceği hello ile aynı adres alanı farklı bir bölgede. toore-hello oluşturmak hello yoktu aynı ortamda etkilenen bölge, toomake API çağrıları toore sahip-bulut Hizmetleri (web/çalışan rolleri) ve sahip olduğunuz sanal makineler dağıtabilirsiniz. Ayrıca, bir VPN ağ geçidi ayarlama ve şirket içi bağlantı (bir karma dağıtımı olduğu gibi) olsaydı tooyour şirket içi ağ bağlanmak toospin sahip olur.

bir VNet oluşturmak için hello yönergeleri bulunduğunda [burada](virtual-networks-create-vnet-arm-pportal.md). 

**S: sanal ağ içinde belirli bir bölgedeki çoğaltmasını önceden başka bir bölgede yeniden oluşturulabilir?**

A: Evet hello kullanarak aynı özel IP adres alanı ve ilerisinde iki farklı bölgelerdeki kaynakları süresi iki sanal ağlar oluşturabilirsiniz. Bir müşteri hello VNet Hizmetleri'nde Internet'e barındırma varsa, bunlar etkin olan trafik Yöneticisi toogeo rota trafiği toohello bölgesini ayarlayın. Ancak, bir müşteri iki Vnet bağlanamıyor yönlendirme sorununa neden olacağından hello ile aynı alanı tootheir şirket içi ağ adresi. Bir olağanüstü durum başlangıç saatini ve bir bölgede bulunan bir sanal ağ kaybı, bir müşteri bağlanabilir diğer VNet ile eşleşen bir adres alanı tootheir şirket içi ağ hello kullanılabilir bölgede hello.

bir VNet oluşturmak için hello yönergeleri bulunduğunda [burada](virtual-networks-create-vnet-arm-pportal.md).

