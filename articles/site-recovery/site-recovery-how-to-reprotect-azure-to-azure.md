---
title: "gelen aaaHow tooReprotect başarısız Azure sanal makineleri geri tooprimary Azure bölgesi | Microsoft Docs"
description: "Yük devretmeyi VM'lerin sonra bir Azure bölgesi tooanother, Azure Site Recovery tooprotect hello makineler ters yönde kullanabilirsiniz. Merhaba adımları nasıl bilgi toodo bir yük devretme yeniden önce yeniden koruma."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Bir Azure bölgesine geri tooprimary bölge gelen yeniden koruma başarısız oldu



>[!NOTE]
>
> Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.


## <a name="overview"></a>Genel Bakış
Olduğunda, [yük devretme](site-recovery-failover.md) sanal makinelerden bir Azure bölgesi tooanother Merhaba, hello sanal makinelerdir korumasız bir durumda. Toobring istiyorsanız, bunları toohello birincil bölge yeniden, toofirst gerek hello sanal makineler ve yük devretme yeniden koruyun. Nasıl arasında fark yoktur, yük devretme bir yönü veya diğer. Benzer şekilde, hello sanal makinelerin korumasını etkinleştir işlemleri sonrasında, hello yeniden koruma post yük devretme veya sonrası yeniden çalışma arasında fark yoktur.
Doğu Asya bölge olarak hello birincil site hello korunan makinelerin ve hello kurtarma sitesi hello makineler Güneydoğu Asya bölge olarak tooexplain hello iş akışlarını yeniden koruma ve tooavoid Karışıklığı önlemek için kullanacağız. Yük devretme sırasında yük devretme hello sanal makineleri toohello Güneydoğu Asya bölge olur. Yeniden çalışma önce Güneydoğu Asya geri tooEast Asya tooreprotect hello sanal makinelerden gerekir. Bu makalede nasıl hello adımları tooreprotect.

> [!WARNING]
> Varsa [tamamlandı geçiş](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)taşınan hello sanal makine tooanother kaynak grubu veya silinen hello Azure sanal makine, yeniden çalışma bundan sonra olamaz.

Yeniden koruma tamamlandıktan ve hello korumalı sanal makineleri çoğaltmak, hello sanal makineleri toobring üzerinde bir yük devretme başlatabilirsiniz sonra bunları tooEast Asya bölge yedekleyin.

POST yorumlarınızı ve sorularınızı bu makalenin veya hello hello sonunda [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Ön koşullar
1. Merhaba sanal makineleri kaydedilmiş.
2. Merhaba hedef site - bu durumda hello Doğu Asya Azure bölgesini kullanılabilir olması gerekir ve bu bölgede yeni kaynaklar mümkün tooaccess/oluşturma olması gerekir.

## <a name="steps-tooreprotect"></a>Adımları tooreprotect

Aşağıdaki olan hello adımları tooreprotect hello varsayılanları kullanarak bir sanal makine.

1. İçinde **kasa** > **öğeleri çoğaltılan**devredilen hello sanal makineye sağ tıklayın ve ardından **yeniden koruma**. Merhaba seçin ve makine tıklatarak **yeniden koruma** hello komut düğmeleri gelen.

![Tooreprotect sağ tıklayın](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. Bu koruma, hello yönünü Hello dikey penceresinde, fark **Güneydoğu Asya tooEast Asya**, zaten seçilidir.

![Dikey koruyun](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Gözden geçirme hello **kaynak grubu, ağ, depolama ve kullanılabilirlik kümeleri** bilgi ve Tamam'ı tıklatın. (Yeni) olarak işaretlenmiş kaynakları varsa, bunlar koruyun hello bir parçası olarak oluşturulur.

Bu tetikleyici bir işi yeniden koruyun hello hedef site (Bu durumda SEA) ilk belirleyeceği iş hello son verilerle ve tamamlar, çoğaltma işlemi bir kez hello farkları, yük devretme önce tooSoutheast Asya yedekleyin.

### <a name="reprotect-customization"></a>Özelleştirme koruyun
Toochoose istiyorsanız hello sırasında extract depolama hesabı veya hello ağ koruyun, hello kullanarak özelleştirin hello yeniden koruma dikey penceresinde sağlanan seçeneği bunu.

![Seçenek özelleştirme](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

He hedef sanal makinenin özelliklerini yeniden koruma sırasında aşağıdaki hello özelleştirebilirsiniz.

![Dikey penceresini özelleştirme](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Özellik |Notlar  |
|---------|---------|
|Hedef kaynak grubu     | Th sanal makine oluşturulacak toochange hello hedef kaynak grubu seçebilirsiniz. Merhaba parçası olarak yeniden koruma, hello hedef sanal makine silinir, bu nedenle, yeni bir kaynak grubu altında hello VM post yük devretme oluşturabilirsiniz seçebilirsiniz         |
|Hedef sanal ağ     | Ağ hello yeniden koruma sırasında değiştirilemez. toochange hello ağ, hello ağ eşlemesi yineleyin.         |
|Hedef depolama     | Oluşturulan post yük devretme toowhich hello sanal makine olacaktır hello depolama hesabı değiştirebilirsiniz.         |
|Önbellek depolama     | Çoğaltma sırasında kullanılacak bir önbellek depolama hesabı belirtebilirsiniz. Merhaba öndeğerlerini giderseniz, zaten yoksa, yeni bir önbellek depolama hesabı oluşturulur.         |
|Kullanılabilirlik Kümesi     |Doğu Asya Hello sanal makinede bir kullanılabilirlik kümesinin parçası ise, Güneydoğu Asya hello hedef sanal makine için ayarlanmış kullanılabilirlik seçebilirsiniz. Varsayılanları hello varolan SEA kullanılabilirlik kümesini bulmak ve toouse deneyin. Özelleştirme sırasında tamamen yeni bir AV kümesi belirtebilirsiniz.         |


### <a name="what-happens-during-reprotect"></a>Yeniden koruma sırasında ne olur?

Yalnızca hello sonra ilk korumayı etkinleştirme gibi hello Varsayılanları kullanıyorsanız, oluşturulan hello artefacts aşağıda verilmiştir.
1. Önbellek depolama hesabı hello Doğu Asya bölgede oluşturulan.
2. Merhaba hedef depolama hesabı (Merhaba özgün depolama hesabına hello Güneydoğu Asya VM) mevcut değilse yeni bir tane oluşturulur. Merhaba, "ile asr" sonekine hello Doğu Asya sanal makinenin depolama hesabının adıdır.
3. Merhaba hedef AV kümesi yok ve hello bir parçası olarak oluşturulur, yeni AV ayarlayın, toocreate gereken hello Varsayılanları algılamak işi yeniden koruyun. Özelleştirdiyseniz hello koruyun ve ardından seçili hello AV kümesi kullanılacak.
4.

Hello, yeniden koruma işi tetikleyeceğinden, bu adımlar hello listesi verilmiştir. Sanal makine var. hello servis talebi hello hedef tarafta budur.

1. Merhaba artefacts yeniden koruma bir parçası oluşturulan gereklidir. Ardından zaten varsa, bunlar yeniden kullanılır.
2. çalışıyorsa hello hedef tarafı (Güneydoğu Asya) sanal makine önce devre dışı bırakılır.
3. Merhaba hedef tarafı sanal makinenin disk Azure Site Recovery tarafından bir kapsayıcıya çekirdek blob olarak kopyalanır.
4. Merhaba hedef tarafı sanal makine ardından silinir.
5. Merhaba çekirdek blob hello geçerli kaynak tarafı (Doğu Asya) sanal makine tooreplicate tarafından kullanılır. Bu, yalnızca farkları çoğaltılır sağlar.
6. Merhaba önemli değişiklikler hello kaynak disk ve hello çekirdek blob arasında eşitlenir. Bu işlem biraz zaman toocomplete alabilir.
7. Hello koruyun sonra işi tamamlandığında, bir kurtarma noktası hello İlkesi göredir oluşturan hello değişim çoğaltması başlar.

> [!NOTE]
> Bir kurtarma planı düzeyde koruyamaz. Konumundaki yalnızca koruyun bir VM gerçekleştiriliyordu.

Merhaba koruyun sonra başarılı, hello sanal makinenin korumalı bir duruma girer.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba sanal makinenin korumalı bir duruma geçtiğini sonra bir yük devretme işlemi başlatabilirsiniz. Merhaba yük devretme Doğu Asya Azure bölgesindeki hello sanal makineyi kapatın ve ardından oluşturur ve hello Güneydoğu Asya bölge sanal makine önyükleme. Bu nedenle Merhaba uygulaması için kısa bir kapalı kalma süresi yok. Uygulamanızı bir kapalı kalma süresi dayanabileceği bu nedenle, yük devretme hello süresini seçin. Yük devretme hello sanal makine toomake bunu doğru şekilde, bir yük devretmeyi başlatmadan önce geldiği emin önce test önerilir.

-   [Adımları tooinitiate hello sanal makinenin yük devretme testi](site-recovery-test-failover-to-azure.md)

-   [Merhaba sanal makinenin adımları tooinitiate yük devretme](site-recovery-failover.md)
