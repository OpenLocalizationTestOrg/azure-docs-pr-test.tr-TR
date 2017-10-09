---
title: "Azure VM'ler tooanother Azure Site Recovery ile Azure bölgesi için aaaEnable çoğaltma | Microsoft Docs"
description: "Tooenable çoğaltma tooanother Azure bölgesi hello Azure Site Recovery hizmetini kullanan Azure VM'ler için gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>5. adım: Azure VM'ler için çoğaltma etkinleştirme


Ayarladıktan sonra bir [kurtarma Hizmetleri kasası](azure-to-azure-walkthrough-vault.md), bu makale tooenable çoğaltma sanal makineleri (VM'ler) tooanother Azure bölgesi kullanmak [Azure Site Recovery](site-recovery-overview.md). tooenable çoğaltma, kaynak ve hedef ayarlar, hello çoğaltma ilkesini doğrulamak ve tooreplicate istediğiniz sanal makineleri seçin.

- Merhaba makale, Azure Vm'leriniz tamamladığınızda toohello ikincil Azure bölgesi çoğaltılması.
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.


## <a name="select-hello-source"></a>Merhaba kaynağını seçin 

1. Kurtarma Hizmetleri kasalarının içinde hello kasa adına tıklayın > **+ Çoğalt**.
2. İçinde **kaynak**seçin **Azure - Önizleme**.
2. İçinde **kaynak konumu**seçin hello kaynak çalışmakta her yere Vm'lerinizi Azure bölgesi.
3. Select hello **Azure sanal makine dağıtım modeli** VM'ler için: **Resource Manager** veya **Klasik**.
4. Select hello **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.
5. Tıklatın **Tamam** toosave hello ayarları.

    ![Merhaba kaynağı yapılandırın](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Merhaba sanal makineleri seçin

Site Recovery hello VM'ler hello abonelik ve kaynak grubu/bulut hizmeti ile ilişkili bir listesini alır.

1. İçinde **sanal makineleri**, tooreplicate istediğiniz hello sanal makineleri seçin.
2. **Tamam** düğmesine tıklayın.

    ![Sanal makineleri seçin](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Ayarları yapılandırma

Site Recovery (Merhaba Kaynak bölgesi ayarlarına dayanarak) hello hedef bölgesi için varsayılan ayarları sağlar ve hello Çoğaltma İlkesi:

   - **Hedef konum**: hello hedef bölgesi olağanüstü durum kurtarma için toouse istiyor. Merhaba hedef konumu hello Site Recovery kasası hello konumunu eşleştiğini öneririz.
   - **Hedef kaynak grubu**: kaynak grubu toowhich hello hedef bölgede Azure Vm'lerinin yük devretme sonrasında ait olur. Varsayılan olarak, Site Recovery "asr" soneki ile Merhaba hedef bölgede yeni bir kaynak grubu oluşturur. 
   - **Hedef sanal ağ**: hello hangi Azure Vm'lerde içinde hedef bölgesi konumlandırılacağı yük devretme sonrasında hello ağ. Varsayılan olarak, Site Recovery, bir "asr" soneki ile Merhaba hedef bölgede yeni bir sanal ağ (ve alt ağlar) oluşturur. Bu ağ eşlenen tooyour kaynak ağdır. VM yük devretme sonrasında belirli bir IP adresi atayabilirsiniz, tooretain hello gerekiyorsa aynı IP adresi hello kaynak ve hedef konumların dikkat edin. 
   - **Önbellek depolama hesapları**: hello kaynak bölgede Site Recovery kullanan bir depolama hesabı. Kaynak VM'ler üzerindeki değişiklikler önce çoğaltma toohello hedef konumu toothis hesabı gönderilir. 
   - **Hedef depolama hesapları**: varsayılan olarak, Site Recovery yeni bir depolama hesabı hello hedef bölgesi toomirror hello kaynak VM depolama hesabı oluşturur.
   -  **Hedef kullanılabilirlik kümeleri**: varsayılan olarak, Site Recovery hello "asr" soneki ile Merhaba hedef bölgede yeni bir kullanılabilirlik oluşturur. 
   - **Çoğaltma İlkesi adı**: İlke adı.
   - **Kurtarma noktası bekletme**: varsayılan olarak Site Recovery kurtarma noktalarına 24 saat tutar. 1 ila 72 saat arasında bir değer yapılandırabilirsiniz.
   - **Uygulamayla tutarlı anlık görüntü sıklığı**: varsayılan olarak Site Recovery 4 saatte bir uygulamayla tutarlı anlık görüntü alır. 1 ve 12 saat arasında herhangi bir değer yapılandırabilirsiniz. Verileri sürekli olarak çoğaltılır:
    - Kilitlenme tutarlı kurtarma noktalarına tutarlı veri yazma-sırası oluşturduğunuzda korur. Bu tür bir kurtarma noktası, uygulamanızın veri tutarsızlıkları olmadan bir kilitlenme gelen tasarlanmış toorecover ise genellikle yeterli olur
    - Kilitlenme tutarlı kurtarma noktalarına birkaç dakikada üretilir. Bu kurtarma noktaları toofail kullanılarak üzerinden ve kurtarma Vm'leriniz bir kurtarma noktası hedefi (RPO) dakika hello sırasına sağlar.
    - Uygulamayla tutarlı kurtarma noktaları (içinde toplama toowrite sipariş tutarlılık) çalışan uygulamalar tüm işlemleri tamamlamak ve arabellekleri toodisk (uygulama sessiz moda) flush emin olun. SQL Server, Oracle ve Exchange gibi veritabanı uygulamaları için bu kurtarma noktalarını kullanmanızı öneririz.
        
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Ayarları değiştirme

Toomodify hedef ve çoğaltma ilkesi ayarları istiyorsanız, aşağıdaki hello:

1. tooview veya hedef ayarlarını değiştir, tıklatın **ayarları**.
2. toooverride hello varsayılan hedef ayarlar'ı **Özelleştir**. Hedef kaynak grubu, sanal ağ, kullanılabilirlik kümesi ve hedef depolama hesabı belirtebilirsiniz. Sanal makineleri hello kaynak bölge kümesinde parçası ise yalnızca kullanılabilirlik kümeleri ekleyebilirsiniz.

    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Kurtarma noktaları ve uygulamayla tutarlı anlık görüntüler için toooverride çoğaltma ayarları **Özelleştir** sonraki çok**Çoğaltma İlkesi**.
 
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. toostart sağlama hello hedef kaynaklar,'ı **hedef kaynakları oluşturmak**. Sağlama veya bunu bir dakika sürer. Sağlama işlemi sırasında Hello dikey penceresini kapatmayın veya üzerinden toostart sahip olacaksınız.




## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

1. İçinde **ayarları**, tıklatın **çoğaltmasını etkinleştir**. Merhaba, seçili VM'ler ilk çoğaltmasını sağlar. İlk çoğaltma durumu bazı zaman toorefresh alabilir. Tıklatın **yenileme** tooget hello son durumu.

2. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.

3. İçinde **ayarları** > **çoğaltılan öğeler**, VM'lerin hello durumunu görüntüleyin ve ilk çoğaltma işleminin ilerleme durumunu hello. Merhaba VM toodrill ayarlarına farklı Kapat'ı tıklatın.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)
