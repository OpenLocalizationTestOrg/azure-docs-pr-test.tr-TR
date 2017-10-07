---
title: Azure DNS aaaOverview | Microsoft Docs
description: "DNS barındırma hizmeti Microsoft Azure ile ilgili genel bakış. Microsoft Azure etki alanınızda barındırır."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Azure DNS'ye genel bakış

Merhaba etki alanı adı sistemi ya da DNS, çevirmek için sorumlu (veya çözme) bir Web sitesi veya hizmet name tooits IP adresi. Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir. Azure etki alanlarınızı barındırarak DNS sunucunuzun yönetebilirsiniz kullanarak kayıtları, diğer Azure hizmetleriyle aynı kimlik bilgileri, API'leri, Araçlar ve faturalama hello.

![DNS'ye genel bakış](./media/dns-overview/scenario.png)

## <a name="features"></a>Özellikler

* **Güvenilirlik ve performans** -Azure DNS'de DNS etki alanı, Azure'nın genel DNS ad sunucuları ağda barındırılır. Böylece her DNS sorgusu hello en yakın kullanılabilir DNS sunucusu tarafından yanıtlanan her noktaya yayın ağ kullanın. Bu, etki alanınız için yüksek kullanılabilirlik ve hızlı performans sağlar.

* **Sorunsuz tümleştirme** -hello Azure DNS hizmeti kullanılan toomanage Azure hizmetlerinizi için DNS kayıtlarını olabilir ve kullanılan tooprovide DNS dış kaynaklar da olabilir. Azure DNS hello Azure portal tümleştirilmiştir ve diğer Azure hizmetlerinizi kullandığı aynı kimlik bilgilerini, faturalama ve destek sözleşmesi hello.

* **Güvenlik** -hello Azure DNS hizmeti, Azure Resource Manager dayanır. Bu nedenle, rol tabanlı erişim denetimi, denetim günlüklerini ve kaynak kilitleme gibi Resource Manager özelliklerinden yararlanır. Etki alanları ve kayıtları hello Azure portal, Azure PowerShell cmdlet'leri, yönetilebilir ve platformlar arası Azure CLI hello. Otomatik DNS Yönetimi gerektiren uygulamalar hello hizmetiyle hello üzerinden REST API ve SDK'ları tümleştirebilirsiniz.

Azure DNS, etki alanı adlarını satın alma şu anda desteklemiyor. Toopurchase etki alanları istiyorsanız, bir üçüncü taraf etki alanı adı kayıt toouse gerekir. Merhaba Kaydedici genellikle küçük bir yıllık ücret ister. Merhaba etki alanları için DNS kayıtlarını Yönetimi sonra Azure DNS'de barındırılabilir. Bkz: [bir etki alanı tooAzure DNS temsilci](dns-domain-delegation.md) Ayrıntılar için.

## <a name="pricing"></a>Fiyatlandırma

DNS faturalama Azure ve DNS sorgularının hello sayısı tarafından barındırılan DNS bölgeleri hello sayısını temel alır. toolearn ziyaret fiyatlandırma hakkında daha fazla [Azure DNS fiyatlandırma](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>SSS

Azure DNS hakkında sık sorulan sorular için bkz: Merhaba [Azure DNS ile ilgili SSS](dns-faq.md).

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret ederek DNS bölgeleri ve kayıtlar hakkında bilgi edinin: [DNS bölgeleri ve genel bakış kayıtları](dns-zones-records.md).

Nasıl çok öğrenin[bir DNS bölgesi oluşturma](./dns-getstarted-create-dnszone-portal.md) Azure DNS'de.

Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.

