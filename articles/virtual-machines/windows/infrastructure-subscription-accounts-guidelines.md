---
title: "aaaSubscription ve azure'da Windows sanal makineleri için hesapları | Microsoft Docs"
description: "Merhaba abonelikleri ve Azure ile ilgili hesapları için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
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
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Windows sanal makineleri Azure aboneliği ve hesapları yönergeleri

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede tooapproach aboneliği ve hesabı yönetim ortamı ve kullanıcı temel olarak nasıl genişletileceğini anlamaya odaklanır.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Abonelikler ve hesapları için uygulama rehberi
Kararları:

* Hangi abonelikleri ve hesapları toohost BT iş yükü veya altyapı ihtiyacınız var?
* Nasıl toobreak hello hiyerarşi toofit aşağı kuruluşunuz?

Görevler:

* Toomanage istediğiniz gibi mantıksal kuruluş hiyerarşinizi tanımlayın, bir abonelik düzeyinden.
* toomatch bu mantıksal hiyerarşi gereken hello hesaplar ve abonelikler her hesap altında tanımlayın.
* Merhaba birtakım abonelikleri ve adlandırma kuralınızın kullanarak hesapları oluşturun.

## <a name="subscriptions-and-accounts"></a>Abonelik ve hesaplar
toowork Azure ile bir veya daha fazla Azure aboneliği gerekir. Sanal ağlar bu abonelikleri mevcut veya sanal makineleri (VM'ler) kaynakları gibi.

* Kurumsal müşteriler genellikle hello hiyerarşideki hello en üstteki kaynaktır ve ilişkili tooone ya da daha fazla hesapları olan bir işletme kaydı, vardır.
* Tüketiciler ve kurumsal kayıt olmadan müşteriler için hello en üstteki kaynak hello hesabıdır.
* İlişkili tooaccounts abonelikleri olan ve hesap başına bir veya daha fazla abonelik olabilir. Fatura hello abonelik düzeyinde bilgileri azure kaydeder.

Toohello sınırı hello hesabı/aboneliği ilişkisindeki iki hiyerarşi düzeylerinde, önemli tooalign hello adlandırma kuralı gereksinimlerini faturalama hesaplar ve abonelikler toohello'dir. Örneği için bir genel şirket Azure kullanıyorsa, her bölge toohave bir hesap seçebilirsiniz ve abonelikleri adresindeki yönetilen hello bölge düzeyi:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Örneğin, yapı izlenerek hello kullanabilirsiniz:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Bir abonelik ilişkili tooa belirli grubu birden çok toohave bir bölge karar verirse, hello adlandırma kuralı bir şekilde tooencode eklemeniz gerekir hello hello hesabı ya da hello abonelik adı ek veriler. Bu kuruluşunuzun fatura veri toogenerate hello yeni hiyerarşi düzeyleri Fatura raporları sırasında massaging olanak sağlar:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Merhaba kuruluş aşağıdaki örneğine hello gibi görünebilir:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Bir Kurumsal Anlaşma aracılığıyla indirilebilir bir dosyayı veya tüm hesapları tek bir hesap için ayrıntılı faturalama sunuyoruz.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

