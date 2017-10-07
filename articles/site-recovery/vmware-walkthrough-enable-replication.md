---
title: "VMware Vm'leri tooAzure Azure Site Recovery ile çoğaltmak için aaaEnable çoğaltma | Microsoft Docs"
description: "Tooenable çoğaltma tooAzure hello Azure Site Recovery hizmetini kullanarak VMware Vm'leri için gereken hello adımları özetler"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>11. adım: VMware sanal makineleri tooAzure için çoğaltmayı etkinleştirme


Nasıl hello kullanarak tooAzure tooenable çoğaltma için şirket içi VMware sanal makineleri bu makalede [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

- VMware Vm'leri hello olmalıdır [Mobility hizmeti bileşeninin yüklü](vmware-walkthrough-install-mobility.md). -Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde hello işlem sunucusu otomatik olarak hello Mobility hizmetini yükler.
- Azure kullanıcı hesabınızın belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) VM tooAzure tooenable çoğaltması
- Ekleyin veya VM'ler değiştirdiğinizde, too15 dakika veya daha uzun değişiklikler tootake etkisi ve bunları alabilir tooappear hello Portalı'nda.
- VM için en son bulunan hello zaman denetimi **yapılandırma sunucularına** > **en son kişi**.
- Merhaba zamanlanmış bulma Vurgu hello yapılandırma sunucusu bekleyen olmadan VM'ler tooadd (tıklatın yok), tıklatıp **yenileme**.



## <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır. [Daha fazla bilgi](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Vm'lerini çoğaltma

Başlamadan önce hızlı bir video genel bakış izleyin

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.
2. İçinde **kaynak**seçin hello yapılandırma sunucusu.
3. İçinde **makine türü**seçin **sanal makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**hello vSphere ana yöneten hello vCenter sunucusu seçin veya hello konak seçin.
5. Merhaba işlem sunucusunu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu hello yapılandırma sunucusu olacaktır. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. İçinde **hedef**hello aboneliği seçin ve hello vm'lerinde toocreate hello istediğiniz kaynak grubunu. Toouse (Yönetim), Klasik veya resource azure'da hello vm'lerinde için istediğiniz hello dağıtım modelini seçin.


7. Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin. Toouse ayarlamış bir hesap istemiyorsanız, yeni bir tane oluşturabilirsiniz.

8. Yük devretme sonrasında oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır. Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı. Varolan bir ağ toouse istemiyorsanız, bir tane oluşturabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello işlem sunucusu tooautomatically tarafından kullanılacak hello hesap hello makinede hello Mobility hizmeti yükleyin.
11. Varsayılan olarak tüm diskler çoğaltılır. Tıklatın **tüm diskleri** ve tooreplicate istemediğiniz tüm diskleri temizleyin. Daha sonra, **Tamam**'a tıklayın. Ek VM özellikleri daha sonra ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın. Bir ilkeyi değiştirirseniz, değişiklikler uygulanan tooreplicating makine ve toonew makineleri olacaktır.
12. Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.
    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek iş yükü performansını etkileyebilir ve yalnızca makineler hello çalışıyorsa kullanılmalıdır aynı iş yükünü ve tutarlılık gerekir.

    ![Çoğaltmayı etkinleştirme](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Tıklatın **çoğaltmasını etkinleştir**. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)
