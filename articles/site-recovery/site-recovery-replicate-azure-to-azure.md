---
title: "aaaReplicate uygulamaları (Azure tooAzure) | Microsoft Docs"
description: "Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede bir Azure bölgesindeki Azure çok başka bir bölgede."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Azure sanal makineleri tooanother Azure bölgesi Çoğalt



>[!NOTE]
>
> Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.

Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede bir Azure bölgesi tooanother Azure bölgesi içinde.

## <a name="prerequisites"></a>Ön koşullar

* Merhaba makale zaten Site kurtarma ve kurtarma Hizmetleri kasası hakkında bildiğinizi varsayar. Toohave oluşturulan bir 'Kurtarma Hizmetleri Kasası' öncesi gerekir.

    >[!NOTE]
    >
    > Sanal makineleri tooreplicate istediğiniz hello konumda 'Kurtarma Hizmetleri Kasası' hello oluşturmanız önerilir. Örneğin, hedef konumu 'Orta ABD' ise 'Orta ABD' kasası oluşturun.

* Hello Azure Vm'leri üzerinde ağ güvenlik grupları (NSG) kuralları veya güvenlik duvarı proxy toocontrol erişim toooutbound internet bağlantısı kullanıyorsanız, bu, beyaz liste hello gerekli URL'leri veya IP'leri emin olun. Çok başvuran[Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md) daha fazla ayrıntı için.

* Bir ExpressRoute veya şirket içi ve hello arasında bir VPN bağlantısı varsa, kaynak Azure konumda, izleyin [Site kurtarma değerlendirmeleri Azure tooon içi ExpressRoute / VPN Yapılandırması](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) belge.

* Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesinin tooenable çoğaltma.

* Azure aboneliğinizde etkin toocreate VM'ler olmalıdır hello hedef konumda DR bölge olarak toouse istiyor. Destek tooenable hello gerekli kota başvurabilirsiniz.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Azure Site Recovery kasası çoğaltmayı etkinleştirin
Bu çizim için biz hello 'Doğu Asya' Azure konumu toohello ' Güneydoğu Asya ' konumu çalıştıran VM'ler çoğaltır. Merhaba adımlar aşağıdaki gibidir:

 Tıklatın **+ Çoğalt** hello kasa tooenable çoğaltma hello sanal makineler için.

1. **Kaynak:** toohello noktası bu durumda olan kaynak hello makinelerin başvurduğu **Azure**.

2. **Kaynak Konum:** tooprotect sanal makinelerinizi nereye istediğiniz Azure bölgesini hello değil. Bu çizim için 'Doğu Asya' hello kaynak konumu olacaktır

3. **Dağıtım modeli:** toohello Azure dağıtım modeli hello kaynak makinelerin başvuruyor. Her iki Klasik seçebilir veya Kaynak Yöneticisi ve toohello modele ait makineler hello sonraki adımda koruma için listelenir.

      >[!NOTE]
      >
      > Yalnızca klasik bir sanal makine çoğaltabilir ve klasik sanal makine olarak kurtarın. Resource Manager sanal makine olarak kurtaramazsınız.

4. **Kaynak grubu:** kaynak sanal makinelerinizi ait hello kaynak grubu toowhich kullanıcının. Merhaba sonraki adımda koruma için tüm hello VM'ler hello seçili kaynak grubu altında listelenir.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

İçinde **sanal makineleri > sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra Tamam'a tıklayın.
    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Ayarları bölümü altında hedef site özelliklerini yapılandırabilirsiniz.

1. **Hedef konumu:** bu burada kaynak sanal makine verilerinizi çoğaltılabilir hello konumdur. Seçili makineler konumuna bağlı olarak, Site Recovery uygun hedef bölgelerin listesi hello sağlar.

    > [!TIP]
    > Tookeep hedef konumu önerilen aynı itibariyle, Kurtarma Hizmetleri kasası.

2. **Hedef kaynak grubu:** tüm çoğaltılmış sanal makinelere ait olur hello kaynak grubu toowhich değil. Varsayılan olarak ASR yeni bir kaynak grubu hello hedef bölgede "asr" sonekine sahip adıyla oluşturur. ASR tarafından önceden oluşturulmuş kaynak grubu mevcut olmaması durumunda, yeniden kullanılır. Toocustomize de seçebilirsiniz, hello bölümünde aşağıda gösterildiği gibi.    
3. **Hedef sanal ağ:** varsayılan olarak, ASR yeni bir sanal ağ hello hedef bölgede "asr" sonekine sahip adıyla oluşturur. Bu eşlenen tooyour kaynak ağ olacaktır ve gelecekteki tüm koruma için kullanılır.

    > [!NOTE]
    > [Ağ ayrıntıları denetlemek](site-recovery-network-mapping-azure-to-azure.md) tooknow ağ eşlemesi hakkında daha fazla bilgi.

4. **Depolama hesapları hedef:** varsayılan olarak, ASR kaynak VM depolama yapılandırmanızı mimicking hello yeni hedef depolama hesabı oluşturur. ASR tarafından önceden oluşturulmuş depolama hesabı mevcut olmaması durumunda, yeniden kullanılır.

5. **Depolama hesapları önbelleğe:** ASR önbellek depolama hello kaynak bölgede adlı ek depolama alanı hesabı gerekiyor. Tüm kaynak VM'ler izlenen ve bu toohello hedef konumu çoğaltma önce toocache depolama hesabı gönderilen üzerinde hello gerçekleştiği değişiklikleri hello.

6. **Kullanılabilirlik kümesi:** varsayılan olarak, ASR hello hedef bölgede kümesi "asr" sonekine sahip adı ile yeni bir kullanılabilirlik oluşturur. Kullanılabilirlik kümesi zaten ASR tarafından oluşturulan mevcut olmaması durumunda, yeniden kullanılır.

7.  **Çoğaltma İlkesi:** kurtarma noktası bekletme geçmişi ve uygulama tutarlılığı anlık görüntü sıklığı hello ayarlarını tanımlar. Varsayılan olarak, ASR ' 24 saattir kurtarma noktası bekletme ve ' 60 dakika uygulama tutarlılığı anlık görüntü sıklığı için varsayılan ayarlarla yeni bir çoğaltma ilkesi oluşturur.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Hedef kaynakları özelleştirme

ASR tarafından kullanılan toochange hello Varsayılanları olasılığına gereksinimlerinize göre hello ayarlarını değiştirebilirsiniz.

1. **Özelleştir:** toochange tıklatın hello varsayılanlar ASR tarafından kullanıldı.

2. **Hedef kaynak grubu:** hello abonelik içindeki hello hedef konumda var olan tüm hello kaynak gruplarının hello listeden hello kaynak grubunu seçin.

3. **Hedef sanal ağ:** hello hedef konumda bulunan tüm hello sanal ağ hello listesini bulabilirsiniz.

4. **Kullanılabilirlik kümesi:** kullanılabilirlik kaynak bölgede bir parçası olan kullanılabilirlik kümeleri ayarları toohello sanal makineleri yalnızca ekleyebilirsiniz.

5. **Hedef depolama hesapları:**

![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/customize.PNG) tıklayın **hedef kaynak oluşturma** ve çoğaltmayı etkinleştirme


Korunan sanal makine sonra hello altında VM'ler sağlık durumunu kontrol edebilirsiniz **çoğaltılan öğeler**

>[!NOTE]
>Başlangıç sırasında zaman toorefresh durumunu alır ve bir süre için ilerleme görmüyorsanız olasılığı, ilk çoğaltma başlatılamadı. Merhaba dikey tooget hello en son durum hello üstte hello Yenile düğmesini tıklatabilirsiniz.
>

![Çoğaltmayı etkinleştirme](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Sonraki adımlar
- [Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme testi çalıştırma hakkında.
- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.
- Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Daha fazla bilgi edinmek [Azure sanal makineleri yeniden korumayı](site-recovery-how-to-reprotect.md) yük devretme sonrasında.
