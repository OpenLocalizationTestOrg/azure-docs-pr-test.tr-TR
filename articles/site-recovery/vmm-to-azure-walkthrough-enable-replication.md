---
title: "vmm'de Hyper-V sanal makineleri için aaaEnable çoğaltma tooAzure bulut Azure Site Recovery ile | Microsoft Docs"
description: "Nasıl tooenable çoğaltma tooAzure vmm'de Hyper-V VM'ler için Azure Site Recovery hizmeti hello ile Bulutlar açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>11. adım: VMM bulutlarındaki Hyper-V VM'ler için çoğaltma tooAzure etkinleştirme

Bir çoğaltma ilkesi ayarladıktan sonra System Center Virtual Machine Manager (VMM) bulutlarında yönetilen Bu makale tooenable şirket içi Hyper-V sanal makineleri (VM'ler) çoğaltması için), hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md)hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

Azure hesabınızda hello doğru olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VM'ler. [Daha fazla bilgi edinin](../active-directory/role-based-access-built-in-roles.md) Azure rol tabanlı erişim denetimi hakkında.

## <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır. [Daha fazla bilgi](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Vm'lerini çoğaltma

VM'ler için çoğaltma gibi etkinleştirin:  

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Hello için çoğaltma ilk kez etkinleştirdikten sonra tıklayın **+ Çoğalt** hello kasa tooenable çoğaltma ilave makineler için.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. Merhaba, **kaynak** dikey penceresinde, select hello VMM sunucusu ve hello bulut hello Hyper-V konakları konumlandırıldığını. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. İçinde **hedef**hello aboneliği, yük devretme sonrası dağıtım modeli seçin ve hello çoğaltılan veriler için kullandığınız depolama hesabı.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Toouse istediğiniz hello depolama hesabını seçin. Toouse sahip farklı bir depolama hesabı olandan isterseniz [oluşturmak](#set-up-an-azure-storage-account). Çoğaltılan veriler için bir premium depolama hesabı kullanıyorsanız, devam eden değişiklikler tooon içi data.toocreate yakalama hello Resource Manager modelini kullanarak bir depolama hesabı bir ek bir standart depolama hesabı toostore çoğaltma günlükleri tooselect gerekir tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, bunu [hello Azure portal'ın](../storage/common/storage-create-storage-account.md). Daha sonra, **Tamam**'a tıklayın.
5. Yük devretme sonrasında oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır. Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma**, tooselect hello makine başına Azure ağı. Toouse elinizde kullanılanlardan farklı bir ağ isterseniz [oluşturmak](#set-up-an-azure-network). kullanarak bir ağ toocreate hello Resource Manager modeli tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, bunu [hello Azure portal'ın](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.
6. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. İçinde **özellikleri** > **özelliklerini yapılandırma**, seçili hello VM'ler için hello işletim sistemini seçin ve işletim sistemi diski hello.

    - Bu hello Azure VM adı (hedef) uyumlu ile doğrulayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Varsayılan olarak tüm hello diskleri hello VM, çoğaltma için seçilir, ancak diskleri tooexclude temizleyebilirsiniz bunları.

        - Tooexclude diskleri tooreduce çoğaltma bant genişliği isteyebilirsiniz. Örneğin, geçici verileri tooreplicate disklerle istemeyebilirsiniz veya (pagefile.sys veya Microsoft SQL Server tempdb gibi) her zaman bir makine ya da uygulamaları yeniledi verileri yeniden başlatır. Merhaba disk unselecting hello disk tarafından çoğaltma dışında bırakabilirsiniz.
        - Yalnızca temel diskler dışarıda bırakılabilir. İşletim sistemi diskleri dışarıda bırakılamaz.
        - Dinamik diskleri dışarıda tutmamanızı öneririz. Site Recovery, konuk VM içerisindeki bir sanal sabit diskin temel mi yoksa dinamik mi olduğunu anlayamaz. Tüm bağımlı dinamik birimi disklerinin dışlanan olmayan varsa, hello korumalı dinamik disk hello VM yöneltilir ve bu disk üzerindeki hello verileri erişilebilir olmayacaktır başarısız disk olarak gösterir.
        - Çoğaltmayı etkinleştirdikten sonra çoğaltma için disk ekleme veya kaldırma gerçekleştiremezsiniz. Tooadd, veya bir disk dışlamak istiyorsanız Merhaba VM toodisable koruma gerektiren ve yeniden etkinleştirin.
        - Azure'da el ile oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üzerinde üç disk başarısız ve iki doğrudan Azure VM'deki oluşturursanız, üzerinden başarısız olan yalnızca hello üç disk geri Azure tooHyper-V ile başarısız. Yeniden çalışma veya Hyper-V tooAzure ters çoğaltmayı el ile oluşturulan diskleri ekleyemezsiniz.
        - Bir uygulama toooperate için gerekli olan bir disk bıraksanız sonra Yük devretme tooAzure azure'da uygulama bu hello çoğaltılan şekilde el ile çalıştırabilirsiniz toocreate gerekir. Alternatif olarak, bir kurtarma planı toocreate hello disk hello makinenin yük devretme sırasında Azure Otomasyon tümleştirin.

    Tıklatın **Tamam** toosave değişiklikler. Daha sonra ek özellikleri ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, istediğiniz tooapply hello VM'ler korumalı hello çoğaltma ilkesi seçin. Daha sonra, **Tamam**'a tıklayın. Merhaba Çoğaltma İlkesi'nde değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Uyguladığınız değişiklikler, zaten çoğaltılmakta olan makinelere ve yeni makinelere uygulanır.

   ![Çoğaltmayı etkinleştirme](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** işi çalıştırır, hello makine yük devretme için hazır.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 12: yük devretme testi çalıştırma](vmm-to-azure-walkthrough-test-failover.md)
