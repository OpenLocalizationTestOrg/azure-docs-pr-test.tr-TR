---
title: "Olağanüstü durum kurtarma gereksinimleri için Azure bölgeler arasında Azure Vm'lerini çoğaltma: Azure tooAzure | Microsoft Docs"
description: "Olağanüstü durum kurtarma gereksinimleri için hello Azure Site Recovery hizmeti ile Azure bölgeler (Azure-Azure) arasında tooreplicate Azure VM'ler gereken hello adımları özetler."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma

>[!NOTE]
>
> Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.

Nasıl kullanarak Azure bölgeler arasında Azure VM'ler tooreplicate hello bu makalede [Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Azure olağanüstü durum kurtarma

Yerleşik Azure altyapı yetenekleri ve özellikleri Azure Vm'lerinde çalışan iş yüklerini tooa sağlam ve esnek kullanılabilir stratejiyi katkıda. Ancak, birçok nedenden neden tooplan Azure bölgeler arasında olağanüstü durum kurtarma için kendiniz ihtiyacınız vardır:

- Belirli uygulamalar ve iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize gerektiren iş yükleri için toomeet uyumluluk yönergelerine gerekir.
- Azure VM'ler, iş kararları göre ve değil yalnızca yerleşik Azure işlevselliğine bağlı kurtarmak ve hello özelliği tooprotect istiyorsunuz.
- Üretim üzerinde hiçbir etkisi olmadan, iş ve uyumluluk gereksinimlerinize uygun olarak tootest yük devretme ve kurtarma gerekir.
- Geri toohello özgün kaynak bölge sorunsuz bir şekilde başarısız ve hello olayı bir olağanüstü durum kurtarma bölgede toohello üzerinden toofail gerekir.

Site Recovery kullanan tüm bu görevleri gerçekleştirmek için Azure Azure VM çoğaltma toohelp.


## <a name="why-use-site-recovery"></a>Neden Site Recovery kullanmalısınız?      

Site Recovery basit yol tooreplicate bölgeler arasında Azure VM'ler sunar:

- **Otomatik dağıtım**. Etkin-etkin çoğaltma modeli, ikincil bölge'hello pahalı ve karmaşık bir altyapıda için gerek yoktur. Çoğaltmayı etkinleştirmek, Site Recovery otomatik olarak hello gerekli kaynakları hello hedef bölgede Kaynak bölgesi ayarlarınızı temel alan oluşturur.
- **Denetim bölgeleri**. Site Recovery ile bir kıtada içinde hiçbir bölge tooany bölgesinden çoğaltabilirsiniz. Bu standart arasında zaman uyumsuz olarak çoğaltır okuma erişimli coğrafi olarak yedekli depolama karşılaştırmak [eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) yalnızca. Coğrafi olarak yedekli depolamaya okuma erişimi hello hedef bölgede salt okunur erişim toohello verileri sağlar.
- **Çoğaltma otomatik**. Site Recovery otomatik sürekli çoğaltma sağlar. Yük devretme ve yeniden çalışma tek bir tıklatmayla tetiklenebilir.
- **RTO ve RPO**. Site Recovery bölgeleri tookeep bağlayan hello Azure ağ altyapısı avantajlarından yararlanır RTO ve RPO çok düşük.
- **Sınama**. Olağanüstü durum kurtarma ayrıntısına gerektiğinde, üretim iş yükleri veya devam eden çoğaltmayı etkilemeden gereken isteğe bağlı yük devretme testlerini çalıştırabilirsiniz.
- **Kurtarma planları**. Kurtarma planları tooorchestrate yük devretme ve yeniden çalışma hello tüm uygulamanın birden çok VM'ler üzerinde çalıştırılan kullanabilirsiniz. Azure Otomasyonu runbook'ları ile zengin birinci sınıf tümleştirme Hello kurtarma planı özelliği vardır.


## <a name="deployment-summary"></a>Dağıtım özeti

İhtiyacınız olan bir özeti aşağıda verilmiştir toodo tooset VM'ler çoğaltma Azure bölgeler arasında:

1. Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası yapılandırma ayarlarını içeren çoğaltma ve yönetir.
2. Hello Azure VM'ler çoğaltmayı etkinleştirin.
3. Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.

>[!IMPORTANT]
>
> Merhaba denetleyebilirsiniz [Azure VM çoğaltması için destek matrisi](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Merhaba tooconfigure hello ağ giden bağlantı Azure VM'ler için Site Recovery çoğaltma için nasıl gereken hakkında daha fazla bilgi için bkz [Ağ Kılavuzu belge](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Başlamadan önce

* Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesinin tooenable çoğaltma.
* Azure aboneliğinizde etkin toocreate VM'ler toouse hello olağanüstü durum kurtarma bölge olarak istediğiniz hello hedef konumda olmalıdır. Desteğe başvurun tooenable hello gerekli kotası.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Merhaba kurtarma Hizmetleri kasası, VM'ler tooreplicate istediğiniz hello konumda oluşturmanızı öneririz. Hedef konumunuz olan hello Orta BİZE, örneğin, hello kasasına oluşturun **Orta ABD**.

## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

İçinde **kurtarma Hizmetleri kasaları**, hello kasa adını tıklatın. Merhaba Hello kasaya tıklayın **+ Çoğalt** düğmesi.

### <a name="step-1-configure-hello-source"></a>1. Adım Merhaba kaynağı yapılandırın
1. İçinde **kaynak**seçin **Azure - Önizleme**.
2. İçinde **kaynak konumu**seçin hello kaynak çalışmakta her yere Vm'lerinizi Azure bölgesi.
3. Select hello dağıtım modeli, VM'lerin: **Resource Manager** veya **Klasik**.
4. Select hello **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.

    ![Merhaba kaynağı yapılandırın](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>2. Adım Sanal makineleri seçin

* Tooreplicate istediğiniz ve ardından hello VM'ler seçin **Tamam**.

    ![Sanal makineleri seçin](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>3. Adım Ayarları yapılandırma

1. toooverride hello varsayılan hedef ayarları ve hello ayarlarını belirtme, seçimine tıklayın **Özelleştir**. Daha fazla bilgi için bkz: [hedef kaynakları özelleştirme](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Ayarları yapılandırma](./media/site-recovery-azure-to-azure/settings.png)


2. Varsayılan olarak, Site Recovery uygulamayla tutarlı anlık görüntüleri 4 saatte alır ve 24 saat için kurtarma noktalarını korur bir çoğaltma ilkesi oluşturur. toocreate farklı ayarlara sahip bir ilke tıklatın **Özelleştir** sonraki çok**Çoğaltma İlkesi**.

    ![İlke özelleştirme](./media/site-recovery-azure-to-azure/customize-policy.png)

3. toostart sağlama hello hedef kaynaklar,'ı **hedef kaynakları oluşturmak**. Sağlama veya bunu bir dakika sürer. Sağlama işlemi sırasında Hello dikey penceresini kapatmayın veya üzerinden toostart gerek vardır.

4. Merhaba tootrigger çoğaltmasını seçili VM, tıklatın **çoğaltmasını etkinleştir**.

5. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.

6. İçinde **ayarları** > **çoğaltılan öğeler**, VM'lerin hello durumunu görüntüleyin ve ilk çoğaltma işleminin ilerleme durumunu hello. Merhaba VM toodrill ayarlarına farklı Kapat'ı tıklatın.

## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

Her şeyi ayarladıktan sonra bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırın:

1. tek bir makineye üzerinden toofail içinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklatın **+ yük devretme testi** simgesi.

2. bir kurtarma üzerinden toofail planlama **ayarları** > **kurtarma planları**, sağ hello planı **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md). 

3. İçinde **yük devretme testi**seçin hello hedef Azure sanal ağı toowhich Azure VM'ler hello yük devretme gerçekleştikten sonra bağlanır.

4. toostart yük devretme Merhaba, tıklatın **Tamam**. tootrack ilerleme, hello VM tooopen, Özellikler'i tıklatın. Veya hello tıklatabilirsiniz **yük devretme testi** hello kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.

5. Merhaba sonra Yük devretme, hello çoğaltma Azure makine hello Azure portalında görünür bittikten > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olun.

6. toodelete hello hello test yük devretmesi sırasında oluşturulan VM'ler tıklatın **temizleme yük devretme sınaması** öğesi veya hello kurtarma planı üzerinde hello yinelenmiş. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. 

[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.


## <a name="next-steps"></a>Sonraki adımlar

Sonra hello dağıtımı test etme:

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine farklı türleri hakkında ve nasıl toorun bunları.
- Daha fazla bilgi edinmek [kurtarma planlarına kullanarak](site-recovery-create-recovery-plans.md) tooreduce RTO.
