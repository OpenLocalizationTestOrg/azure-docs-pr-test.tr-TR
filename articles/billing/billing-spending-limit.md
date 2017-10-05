---
title: "Azure harcama sınırı anlama | Microsoft Docs"
description: "Azure harcama sınırı nasıl çalıştığını ve nasıl kaldırılacağı açıklanır"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: a2743ef34bde0faabb3afd2ace27acddd59d3d70
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="understand-azure-spending-limit-and-how-to-remove-it"></a>Azure harcama sınırı ve nasıl kaldırılacağı anlama

Azure harcama sınırı, Azure aboneliğinizin ne kadar harcayabilir üzerinde sınırıdır. Kaydolan deneme teklifi veya birden çok ay içinde krediler içeren teklifler için tüm yeni müşteriler varsayılan olarak açıktır harcama sınırı vardır. Harcama sınırını $0'dır. Değiştirilemez. Harcama limiti; Kullandıkça Öde abonelikleri ve taahhüt planları gibi abonelik türlerinde kullanılamaz. Bkz: [Azure teklifleri ve harcama sınırını kullanılabilirliğini tam listesi](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-the-spending-limit"></a>Harcama limitine ulaştığımda ne olur?

Dağıttığınız Hizmetleri kullanım sonuçlarınızda aylık tutarlar tüketebilir ücretleri kullanımınız teklifinize dahil, o faturalama ayına geri kalanı için devre dışı bırakılır. Örneğin, dağıttığınız Bulut Hizmetleri üretimden kaldırılır, ayrıca Azure sanal makineleriniz durdurulur ve serbest bırakılır. Hizmetlerinizin devre dışı bırakılmasını önlemek için harcama limitinizi kaldırabilirsiniz. Hizmetlerinizin devre dışı bırakıldığında, depolama hesapları ve veritabanları veriler salt okunur şekilde Yöneticiler için kullanılabilir. Teklifiniz birden fazla ay krediler içeriyorsa sonraki fatura ayının başlangıcında aboneliğinizi yeniden etkin olacaktır. Ardından, bulut hizmetlerinize dağıtmanız ve depolama hesapları ve veritabanları tam erişimi vardır.

Ücretsiz deneme aboneliği harcama sınırına ulaştığında sonra aboneliği yeniden etkinleştirin ve otomatik olarak sahip [bizim standart Kullandıkça Öde teklif yükseltme](billing-upgrade-azure-subscription.md) 90 gün içinde.

Teklifiniz için harcama sınırına olduğunda bildirim alırsınız. Oturum [Azure hesap Merkezi](https://account.windowsazure.com)seçin **hesap**ve ardından **abonelikleri**. Harcama sınırına abonelikleri hakkında bildirimler bakın.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Etkin bir harcama sınırına sahip olsanız bile için ücretlendirilirsiniz noktalar

Bazı Azure Hizmetleri ve [Market satın](https://azure.microsoft.com/marketplace/) bir harcama sınırına ayarlanmış olsa bile, ödeme yöntemini (CC) altında bir ücrete tabi. Visual studio lisansları, Azure Active Directory premium, destek planları ve Market üzerinden satılan Hizmetleri markalı çoğu üçüncü taraf örnektir.


## <a name="when-not-to-use-the-spending-limit"></a>Harcama limitinin kullanılmaması gereken durumlar

Harcama limiti, belirli Market ve Microsoft hizmetlerini dağıtmanızı veya kullanmanızı engelleyebilir. Aboneliğinizdeki harcama limitini kaldırmanızı gerektiren senaryolar aşağıda belirtilmiştir.

- Oracle gibi birinci taraf görüntülerini ve Visual Studio Team Services gibi hizmetleri dağıtmayı planlıyorsunuz. Bu senaryo, harcama limitine hemen aşmasına neden olur ve aboneliğiniz devre dışı bırakılmasına neden olur.

- Kesintiye uğramaması gereken hizmetleriniz var.

- Sanal IP adresleri gibi ayarlar içeren, kaybetmek istemediğiniz hizmet ve kaynaklarınız var. Bu ayarlar, hizmet ve kaynakları serbest zaman kaybolur.


## <a name="remove-the-spending-limit"></a>Harcama limitini kaldırma

Aboneliğinizle ilişkili geçerli bir ödeme yöntemi olduğu sürece, harcama limitini istediğiniz zaman kaldırabilirsiniz. Birden çok aya yayılan kredi içeren tekliflerde, bir sonraki fatura döneminin başlangıcında harcama limitini yeniden etkinleştirebilirsiniz.

Harcama limitini kaldırmak için şu adımları izleyin:

1. Oturum [Azure hesap Merkezi](https://account.windowsazure.com).

2. Bir abonelik seçin.

3. Abonelik, Harcama Limitine ulaşılması nedeniyle devre dışı bırakılmışsa şu bildirime tıklayın: "Abonelik, Harcama Limitine ulaştı ve ücretleri önlemek için devre dışı bırakıldı." Aksi takdirde tıklatın **harcama sınırı Kaldır** içinde **ABONELİK durumunu** alanı.

4. Size uygun bir seçenek belirleyin.

|Seçenek|Etki|
|-------|-----|
|Harcama limitini süresiz olarak kaldırma|Harcama limiti kaldırılır ve bir sonraki fatura döneminin başlangıcında otomatik olarak yeniden açılmaz.|
|Geçerli fatura dönemi için harcama limitini kaldırma|Harcama limiti kaldırılır ve bir sonraki fatura döneminin başlangıcında otomatik olarak yeniden açılır.|

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.
