---
title: "Aboneliği ve azure'da Windows sanal makineleri için hesapları | Microsoft Docs"
description: "Abonelikleri ve Azure ile ilgili hesapları için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b54e18ed6ecef26a059a6ce742bca03a6434183
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Windows sanal makineleri Azure aboneliği ve hesapları yönergeleri

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede ortamınızın olarak abonelik ve hesap yönetim yaklaşımını nasıl anlamaya odaklanır ve kullanıcı tabanını büyür.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Abonelikler ve hesapları için uygulama rehberi
Kararları:

* Hangi birtakım abonelikleri ve hesapları BT iş yükü veya altyapı barındırmak için ihtiyacınız?
* Kuruluşunuz uyacak şekilde hiyerarşide aşağıda ayırmak nasıl?

Görevler:

* Bir abonelik düzeyinden yönetmek istediğiniz gibi mantıksal kuruluş hiyerarşinizi tanımlayın.
* Bu mantıksal hiyerarşi eşleştirmek için gereken hesaplar ve abonelikler her hesap altında tanımlayın.
* Abonelikler ve adlandırma kuralınızın kullanarak hesapları kümesi oluşturun.

## <a name="subscriptions-and-accounts"></a>Abonelik ve hesaplar
Azure ile çalışmak için bir veya daha fazla Azure aboneliği gerekir. Sanal ağlar bu abonelikleri mevcut veya sanal makineleri (VM'ler) kaynakları gibi.

* Kurumsal müşteriler, hiyerarşideki en üst kaynaktır ve bir veya daha fazla hesaplarına ilişkili olan bir işletme kaydı, genellikle vardır.
* Tüketiciler ve kurumsal kayıt olmadan müşteriler için en üstteki kaynak hesabıdır.
* Abonelik hesaplarına ilişkilendirilmiş ve hesap başına bir veya daha fazla abonelik olabilir. Abonelik düzeyinde bilgi faturalama azure kaydeder.

Hesabı/aboneliği ilişkisindeki iki hiyerarşi düzeyleri sınırı nedeniyle, hesapları ve fatura gereksinimlerine abonelikleri adlandırma kuralı hizalamak önemlidir. Örneğin, genel şirket Azure kullanıyorsa, bir hesap bölge başına sahip olmayı seçebilirsiniz ve Abonelikleri, yönetilen bölge düzeyi:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Örneğin, aşağıdaki yapısını kullanabilirsiniz:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Bir bölge belirli bir gruba ilişkili birden fazla aboneliğiniz varsa karar verirse, adlandırma kuralı hesabı ya da abonelik adını üzerindeki fazladan verileri kodlamak için bir yol eklemeniz gerekir. Bu kuruluş hiyerarşi yeni düzeylerini sırasında fatura raporlar üretmek için faturalama verisi massaging sağlar:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Kuruluş aşağıdaki gibi görünebilir:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Bir Kurumsal Anlaşma aracılığıyla indirilebilir bir dosyayı veya tüm hesapları tek bir hesap için ayrıntılı faturalama sunuyoruz.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

