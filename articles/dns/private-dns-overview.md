---
title: "Özel etki alanları için Azure DNS kullanarak | Microsoft Docs"
description: "Özel DNS barındırma hizmeti Microsoft Azure ile ilgili genel bakış."
services: dns
documentationcenter: na
author: KumudD
manager: jennoc
editor: 
ms.assetid: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/20/2017
ms.author: kumud
ms.openlocfilehash: 95cf8ab2bd34e698e12452e062687219bad49eb6
ms.sourcegitcommit: 4ea06f52af0a8799561125497f2c2d28db7818e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/21/2017
---
# <a name="using-azure-dns-for-private-domains"></a>Azure DNS için özel etki alanlarını kullanma
Etki alanı adı sistemi ya da DNS, çevirmek için sorumludur (veya çözme) IP adresi için bir hizmet adı. Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir.  İnternet'e yönelik DNS etki alanı yanı sıra Azure DNS şimdi ayrıca özel DNS etki alanı bir önizleme özelliği olarak destekler.  
 
Azure DNS, yönetmek ve özel DNS çözüm eklemek zorunda kalmadan sanal bir ağ etki alanı adları çözümlemek için bir güvenilir, güvenli DNS hizmeti sağlar. Özel DNS bölgeleri günümüzün Azure tarafından sağlanan adları yerine kendi özel etki alanı adlarını kullanmanızı sağlar.  Özel etki alanı adlarını kullanarak, sanal ağ Mimarinizi en iyi karşılayacak şekilde uyarlamak için kuruluşunuzun gereksinimlerine yardımcı olur. Bu ad çözümlemesi VM'ler için sanal ağlar arasında ve sanal ağ sağlar. Ayrıca, özel ve ortak bir DNS bölgesi aynı adı paylaşan izin vererek bir bölme görünümü ile - bölgeleri adları yapılandırabilirsiniz.

![DNS'ye genel bakış](./media/private-dns-overview/scenario.png)

[!INCLUDE [private-dns-preview-notice](../../includes/private-dns-preview-notice.md)]

## <a name="benefits"></a>Avantajlar

* **Özel DNS çözümler gereksinimini ortadan kaldırır.** Daha önce sanal ağlarındaki DNS bölgeleri yönetmek için özel DNS çözümler birçok müşteri oluşturuldu.  DNS bölge Yönetimi artık yapılabilir oluşturma & özel DNS çözümleri yönetmek yükünü kaldırır Azure'nın yerel altyapısını kullanarak.

* **Tüm yaygın DNS kayıt türlerini kullanın.**  Azure DNS A, AAAA, CNAME, MX, NS, PTR, SOA, SRV ve TXT kaydı destekler.

* **Otomatik ana bilgisayar adı kayıt yönetimi.** Özel DNS kayıtlarınızı barındırma yanı sıra, Azure belirtilen sanal ağ içindeki VM'ler için ana bilgisayar kayıtları otomatik olarak bulundurur.  Bu, gerek kalmadan özel DNS çözümler oluşturmak veya uygulama değiştirmek için kullandığınız etki alanı adları en iyi duruma getirme sağlar.

* **Ana bilgisayar adı çözümlemesi sanal ağlar arasında.** Azure tarafından sağlanan ana bilgisayar adları farklı olarak, özel DNS bölgeleri sanal ağlar arasında paylaşılabilir.  Bu özellik, sanal ağ eşlemesi gibi arası ağ ve hizmet bulma senaryolar basitleştirir.

* **Tanıdık Araçlar ve kullanıcı deneyimi.** Öğrenme eğrisi azaltmak için bu yeni sunum zaten tanınmış Azure DNS araçları (PowerShell, Resource Manager şablonları, REST API) kullanır.

* **Yatay bölme DNS desteği.** Azure DNS bölgeleri farklı yanıtlardan bir sanal ağ içinde ve ortak Internet'ten çözümlemek aynı ada sahip oluşturmanıza olanak sağlar.  Yatay bölme DNS tipik bir senaryo, ayrılmış bir sanal ağınız içinde kullanmak için bir hizmet sürümü sağlamaktır.


## <a name="pricing"></a>Fiyatlandırma

Özel DNS bölgeleri yönetilen Önizleme sırasında ücretsiz. Genel kullanılabilirlik sırasında bu özellik bir kullanım tabanlı fiyatlandırma modelini teklifi mevcut Azure DNS için benzer kullanır. 


## <a name="next-steps"></a>Sonraki adımlar

Bilgi edinmek için nasıl [özel bir DNS bölgesi oluşturma](./private-dns-getstarted-powershell.md) Azure DNS'de.

Ziyaret ederek DNS bölgeleri ve kayıtlar hakkında bilgi edinin: [DNS bölgeleri ve genel bakış kayıtları](dns-zones-records.md).

Azure'un diğer önemli [ağ özelliklerinden](../networking/networking-overview.md) bazıları hakkında bilgi edinin.

