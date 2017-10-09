---
title: "Merhaba kaynak ve hedef Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için aaaSet | Microsoft Docs"
description: "Tooset yukarı hello kaynak ve ne zaman hedef nasıl açıklanmaktadır Hyper-V Vm'lerini çoğaltma toosecondary VMM site Azure Site Recovery ile."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>6. adım: hello çoğaltma kaynağı ve hedef ayarlama


Hyper-V çoğaltma tooa içeren ikincil VMM sitesi için bir kurtarma Hizmetleri oluşturduktan sonra kasa [Azure Site Recovery](site-recovery-overview.md), bu makale tooset hello kaynağını kullanın ve hedef çoğaltma konumları. 

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Hello Azure Site kurtarma sağlayıcısı VMM sunucularında yükleme ve bulmak ve sunucuları hello kasaya kaydetmek.

1. Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**.

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [Önkoşullar](#prerequisites).
4. Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.
5. Merhaba kayıt anahtarını indirin. Kurulumu çalıştırırken buna ihtiyacınız olur. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin. Gerekmeyen tooexplicitly herhangi bir şey Hyper-V ana bilgisayar sunucuları üzerinde yükleyin.


## <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery sağlayıcısı yükleme

1. Her VMM sunucusunda Hello sağlayıcı kurulum dosyasını çalıştırın. VMM bir kümede dağıtılıyorsa, yüklediğiniz ilk kez hello aşağıdaki hello yapın:
    -  Hello sağlayıcısı etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın.
    - Ardından, hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin. Küme düğümleri tüm çalışmalı hello hello sağlayıcısı aynı sürümü.
2. Kurulum, birkaç ön koşul denetimlerini çalıştırır ve izni toostop hello VMM hizmeti ister. Kurulum bittiğinde VMM hizmeti hello otomatik olarak yeniden başlatılır. Bir VMM kümesinde yüklerseniz, istendiğinde toostop hello küme rolünü demektir.
3. İçinde **Microsoft Update**, sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun yüklendiğini toospecify seçebilirsiniz.
4. İçinde **yükleme**kabul edin veya hello varsayılan yükleme konumunu değiştirmek ve tıklatın **yükleme**.

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Yükleme tamamlandıktan sonra tıklayın **kaydetmek** hello kasadaki tooregister hello sunucu.

    ![Yükleme konumu](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın. *İleri*’ye tıklayın.

    ![Sunucu kaydı](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. İçinde **Internet bağlantısı**, hello VMM sunucusunda çalışan hello sağlayıcısı tooAzure nasıl bağlandığını belirtin.

    ![İnternet Ayarları](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Bu hello sağlayıcısına bağlanmak doğrudan toohello belirtebilirsiniz Internet veya bir proxy üzerinden.
   - Gerekiyorsa proxy ayarlarını belirtin.
   - Bir proxy kullanıyorsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulan proxy kimlik bilgileri. Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir > **ayarları** > **güvenlik** > **farklı çalıştır hesapları**. Merhaba VMM hizmet tooupdate değişiklikleri yeniden başlatın.
8. İçinde **kayıt anahtarı**seçin hello anahtarı Azure Site Recovery'den indirdiğiniz ve toohello VMM sunucuya kopyalanır.
9. Merhaba şifreleme ayarı yalnızca VMM Bulutları tooAzure Hyper-V sanal makineleri çoğaltma yapıyorsanız kullanılır. İkincil site tooa çoğaltıyorsanız kullanılmaz.
10. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
11. İçinde **Eşitle bulut meta verileri**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istediğinizi seçin. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve hello hello VMM konsolundaki bulut özellikleri ayrı ayrı her Bulutu eşitleyin.
12. Tıklatın **sonraki** toocomplete hello işlemi. Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu üzerinde hello görüntülenen **VMM sunucuları** hello sekmesinde **sunucuları** hello kasası sayfasında.

    ![Sunucu](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Merhaba sunucu hello Site Recovery konsolunda kullanılabilir duruma getirildikten sonra **kaynak** > **kaynağı** hello VMM sunucusu ve select hello bulut hello Hyper-V ana bilgisayar bulunduğu seçin. Daha sonra, **Tamam**'a tıklayın.

Merhaba sağlayıcısı hello komut satırından da yükleyebilirsiniz:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Merhaba hedef VMM sunucusunu ve Bulutu seçin:

1. Tıklatın **altyapıyı hazırlama** > **hedef**ve toouse istediğiniz select hello hedef VMM sunucusu.
2. Site Recovery ile eşitlenmiş Bulutlar hello sunucuda görüntülenir. Merhaba hedef bulut seçin.

   ![Hedef](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 7: ağ eşlemesini yapılandırma](vmm-to-vmm-walkthrough-network-mapping.md).
