---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile Hyper-V çoğaltma tooAzure (System Center VMM olmadan) için yukarı aaaSet | Microsoft Docs"
description: "Azure Site Recovery ile Hyper-V sanal makineleri tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>8. adım: hello kaynak ve hedef Hyper-V çoğaltma tooAzure için ayarlama

Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi Hyper-V sanal makineleri (System Center VMM olmadan) tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba Hyper-V sitesini kurmak, hello Azure Site Recovery sağlayıcısı ve hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin ve hello site hello kasaya kaydetmek.

1. İçinde **altyapıyı hazırlama**, tıklatın **kaynak**. Hyper-V konakları veya kümeleri için kapsayıcı olarak yeni bir Hyper-V sitesi tooadd tıklatın **+ Hyper-V sitesi**.

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. İçinde **oluşturma Hyper-V sitesi**, başlangıç sitesi için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şimdi, oluşturduğunuz ve tıklatın hello siteyi seçin **+ Hyper-V Server** tooadd server toohello sitesi.

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. İçinde **Sunucu Ekle** > **sunucu türü**, denetleyin **Hyper-V server** görüntülenir.

    - İstediğiniz tooadd hello ile uyumlu hello Hyper-V sunucu emin olun [Önkoşullar](#on-premises-prerequisites), ve olduğu mümkün tooaccess hello belirtilen URL'leri.
    - Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin. Bu dosya tooinstall hello sağlayıcısı çalıştırın ve her Hyper-V ana kurtarma Hizmetleri aracısını hello.

    ![Kaynağı ayarlama](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Merhaba sağlayıcı ve aracı yükleme

1. Her ana bilgisayarda Hello sağlayıcı kurulum dosyasını çalıştırın toohello Hyper-V sitesi eklendi. Hyper-V kümesi üzerinde yüklüyorsanız, her küme düğümünde Kurulumu çalıştırın. Düğümleri arasında geçirmek olsa bile yükleme ve her Hyper-V küme düğümü kaydetme VM'ler korunduğunu sağlar.
2. **Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.
3. İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.
4. İçinde **kasa ayarlarını**, tıklatın **Gözat** indirdiğiniz tooselect hello kasa anahtarı dosyasını. Hello Azure Site Recovery abonelik hello kasa adı belirtin ve hello Hyper-V site toowhich hello Hyper-V sunucusuna ait.

    ![Sunucu kaydı](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. İçinde **Proxy ayarlarını**, Hyper-V konakları üzerinde çalışan sağlayıcı üzerinden Site Recovery tooAzure bağlanır hello hello Internet nasıl belirtin.

    * Merhaba sağlayıcısı tooconnect doğrudan select istiyorsanız **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.
    * Var olan ara sunucunuz kimlik doğrulaması gerektiren veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız, seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.
    * Bir proxy sunucu kullanıyorsanız:
        - Başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin
        - Hello açıklanan emin hello URL'leri olun [Önkoşullar](#prerequisites) hello proxy üzerinden izin verilir.

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Yükleme tamamlandıktan sonra tıklatın **kaydetmek** hello kasadaki tooregister hello sunucu.

    ![Yükleme konumu](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Kayıt tamamlandıktan sonra hello Hyper-V sunucusundan meta veriler, Azure Site Recovery tarafından alınır ve hello sunucu görüntülenir **Site Recovery altyapısı** > **Hyper-V konakları**.


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Çoğaltma için Hello Azure depolama hesabı belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.

1. Tıklatın **altyapıyı hazırlama** > **hedef**.
2. Merhaba abonelik ve yük devretme sonrasında toocreate hello Azure VM'ler istediğiniz hello kaynak grubunu seçin. Merhaba dağıtımı seçin model toouse (Klasik veya resource management) azure'da hello VM'ler istiyor.

3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

    - Bir depolama hesabınız yoksa tıklatın **+ depolama** toocreate bir Resource Manager tabanlı hesap satır içi. 
    - Bir Azure ağı yoksa tıklatın **+ ağ** toocreate bir Resource Manager tabanlı ağ satır içi.






## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)
