---
title: "Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure Azure Site Recovery ile çoğaltmak için aaaEnable çoğaltma | Microsoft Docs"
description: "Hyper-V sanal makineleri hello Azure Site Recovery hizmetini kullanarak için tooenable çoğaltma tooAzure gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>10. adım: Hyper-V sanal makinelerini tooAzure çoğaltmak için çoğaltmayı etkinleştirme


Bu makalede nasıl tooenable çoğaltma için Hyper-V sanal makineleri (System Center VMM tarafından yönetilmediğinden) şirket içi hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Başlamadan önce

Başlamadan önce Azure kullanıcı hesabınızın gerekli hello sahip olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.

## <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır. [Daha fazla bilgi](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Vm'lerini çoğaltma

VM'ler için çoğaltma gibi etkinleştirin:          

1. Tıklatın **uygulama çoğaltma** > **kaynak**. Çoğaltma hello için ilk kez ayarladıktan sonra tıklayabilirsiniz **+ Çoğalt** ilave makineler için tooenable çoğaltma.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. İçinde **kaynak**seçin hello Hyper-V sitesi. Daha sonra, **Tamam**'a tıklayın.
3. İçinde **hedef**hello kasa abonelik seçin ve hello yük devretme sonrasında Azure (Klasik veya resource management) toouse istediğiniz yük devretme modeli.
4. Toouse istediğiniz hello depolama hesabını seçin. Toouse istediğiniz bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-storage-account). Daha sonra, **Tamam**'a tıklayın.
5. Yük devretme oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır.

    - etkinleştirmeniz tooapply hello ağ ayarlarını tooall makineleri çoğaltma için seçin **seçili makineler için Şimdi Yapılandır**.
    - Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı.
    - Toouse istediğiniz ağ yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-network). Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.

   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. İçinde **özellikleri** > **özelliklerini yapılandırma**, seçili hello VM'ler için hello işletim sistemini seçin ve işletim sistemi diski hello.
8. Bu hello Azure VM adı (hedef) uyumlu ile doğrulayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Varsayılan olarak tüm hello diskleri hello VM, çoğaltma için seçilir. Clear diskleri tooexclude bunları.
10. Tıklatın **Tamam** toosave değişiklikler. Daha sonra ek özellikleri ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, istediğiniz tooapply hello VM'ler korumalı hello çoğaltma ilkesi seçin. Daha sonra, **Tamam**'a tıklayın. Merhaba Çoğaltma İlkesi'nde değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Uyguladığınız değişiklikler, zaten çoğaltılmış olan makinelere ve yeni makinelere uygulanır.


   ![Çoğaltmayı etkinleştirme](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.


## <a name="next-steps"></a>Sonraki adımlar


Çok Git[11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)
