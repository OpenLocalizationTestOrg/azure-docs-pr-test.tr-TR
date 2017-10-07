---
title: "Azure Site Recovery ile tooAzure kopyalayan fiziksel sunucular için aaaEnable çoğaltma | Microsoft Docs"
description: "Hello Azure Site Recovery hizmetini kullanarak tooenable çoğaltma tooAzure fiziksel sunucuları için gereken hello adımları özetler"
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
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>10. adım: Fiziksel sunucuları tooAzure için çoğaltmayı etkinleştirme


Bu makalede nasıl tooenable çoğaltma için Windows/Linux içi hello kullanarak fiziksel sunucuları tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

- Sunucuları hello olmalıdır [Mobility hizmeti bileşeninin yüklü](physical-walkthrough-install-mobility.md).
- Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde hello işlem sunucusu otomatik olarak hello Mobility hizmetini yükler.
- Bir makine için çoğaltma etkinleştirdiğinizde, Azure kullanıcı hesabınızın belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure, mümkün toouse Azure depolama olduğunuz ve Azure Vm'leri oluşturun.
- Ekleyin veya sunucularının IP adreslerini değiştirin, onu too15 dakika veya daha uzun değişiklikler tootake etkisi ve bunları alabilir tooappear hello Portalı'nda.


## <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır. [Daha fazla bilgi](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Çoğaltma sunucuları

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.
2. İçinde **kaynak**seçin hello yapılandırma sunucusu.
3. İçinde **makine türü**seçin **fiziksel makineleri**.
4. Merhaba işlem sunucusunu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu hello yapılandırma sunucusu olacaktır. Daha sonra, **Tamam**'a tıklayın.
5. İçinde **hedef**hello aboneliği seçin ve hello vm'lerinde toocreate hello istediğiniz kaynak grubunu. Toouse (Yönetim), Klasik veya resource azure'da hello vm'lerinde için istediğiniz hello dağıtım modelini seçin.
6. Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin. Toouse ayarlamış bir hesap istemiyorsanız, yeni bir tane oluşturabilirsiniz.
7. Select hello **Azure ağ** ve **alt** toowhich Azure Vm'lerinin yük devretme sonrasında bağlanın. Seçin **seçili makineler için Şimdi Yapılandır** seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı. Varolan bir ağ toouse istemiyorsanız, bir tane oluşturabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. İçinde **fiziksel makineleri**, tıklatın **+ fiziksel makine** ve hello girin **adı** ve **IP adresi**. Merhaba işletim sistemi seçin hello makinenin tooreplicate istiyor. Makineler bulunan ve hello listede gösterilen kadar birkaç dakika sürer.
9. İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello işlem sunucusu tooautomatically tarafından kullanılacak hello hesap hello makinede hello Mobility hizmeti yükleyin.
10. Varsayılan olarak tüm diskler çoğaltılır. Tıklatın **tüm diskleri** ve tooreplicate istemediğiniz tüm diskleri temizleyin. Daha sonra, **Tamam**'a tıklayın. Ek VM özellikleri daha sonra ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın. Bir ilkeyi değiştirirseniz, değişiklikler uygulanan tooreplicating makine ve toonew makineleri olacaktır.
12. Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.
    * Böylece, iş yüklerini yansıtma fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek iş yükü performansını etkileyebilir ve yalnızca makineler hello çalışıyorsa kullanılmalıdır aynı iş yükünü ve tutarlılık gerekir.

13. Tıklatın **çoğaltmasını etkinleştir**. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[11. adım: yük devretme testi çalıştırma](physical-walkthrough-test-failover.md)
