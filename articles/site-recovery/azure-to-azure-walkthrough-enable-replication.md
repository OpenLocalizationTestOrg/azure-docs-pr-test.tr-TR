---
title: "Azure Site Recovery ile başka bir Azure bölgesine Azure VM'ler için çoğaltma etkinleştirme | Microsoft Docs"
description: "Azure Site Recovery hizmetini kullanan Azure VM'ler için başka bir Azure bölgesine çoğaltmayı etkinleştirmek için gereken adımları özetler"
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
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>5. adım: Azure VM'ler için çoğaltma etkinleştirme


Ayarladıktan sonra bir [kurtarma Hizmetleri kasası](azure-to-azure-walkthrough-vault.md), başka bir Azure bölgesine, sanal makineleri (VM'ler), çoğaltılması etkinleştirmek için bu makaleyi kullanın [Azure Site Recovery](site-recovery-overview.md). Çoğaltmayı etkinleştirmek için kaynak ve hedef ayarlarını yapın, çoğaltma ilkesini doğrulayın ve çoğaltmak istediğiniz sanal makineleri seçin.

- Makale, Azure Vm'leriniz tamamladığınızda ikincil bir Azure bölgesine çoğaltılması.
- Bu makalenin sonundaki yorumları gönderin ya da sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.


## <a name="select-the-source"></a>Bir kaynak seçin 

1. Kurtarma Hizmetleri kasalarının kasa adını tıklatın > **+ Çoğalt**.
2. İçinde **kaynak**seçin **Azure - Önizleme**.
2. İçinde **kaynak konumu**, çalışmakta her yere Vm'lerinizi Azure bölgesinde bir kaynak seçin.
3. Seçin **Azure sanal makine dağıtım modeli** VM'ler için: **Resource Manager** veya **Klasik**.
4. Seçin **kaynak kaynak grubu** Resource Manager VM'ler için veya **bulut hizmeti** Klasik VM'ler için.
5. Ayarları kaydetmek için **Tamam**’a tıklayın.

    ![Kaynak yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a>Sanal makineleri seçin

Site Recovery abonelik ve kaynak grubu/bulut hizmeti ile ilişkili sanal makinelerin listesini alır.

1. İçinde **sanal makineleri**, çoğaltmak istediğiniz sanal makineleri seçin.
2. **Tamam** düğmesine tıklayın.

    ![Sanal makineleri seçin](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Ayarları yapılandırma

Varsayılan ayarlar (Kaynak bölgesi ayarlarına dayanarak) hedef bölgesi ve çoğaltma ilkesi için site kurtarma sağlar:

   - **Hedef konum**: olağanüstü durum kurtarma için kullanmak istediğiniz hedef bölgesi. Hedef konumu Site Recovery kasası konumu eşleştiğini öneririz.
   - **Hedef kaynak grubu**: hedef Azure vm'lerinin bölgeye ait olur yük devretme işleminden sonra kaynak grubu. Varsayılan olarak, Site Recovery "asr" soneki ile hedef bölgede yeni bir kaynak grubu oluşturur. 
   - **Hedef sanal ağ**: hedef hangi Azure VM'de bölge konumlandırılacağı yük devretme sonrasında ağ. Varsayılan olarak, Site Recovery, bir "asr" soneki ile hedef bölgede yeni bir sanal ağ (ve alt ağlar) oluşturur. Bu ağ kaynağı ağınıza eşlenir. Kaynak ve hedef konumları aynı IP adresi silmemeniz gerekiyorsa, bir VM yük devretme sonrasında belirli bir IP adresi atayabilirsiniz unutmayın. 
   - **Önbellek depolama hesapları**: kaynak bölgede Site Recovery kullanan bir depolama hesabı. Kaynak VM'ler üzerindeki değişiklikler çoğaltma hedef konumu için önce bu hesaba gönderilir. 
   - **Hedef depolama hesapları**: varsayılan olarak, Site Recovery VM depolama hesabı kaynak yansıtmak üzere hedef bölgede yeni bir depolama hesabı oluşturur.
   -  **Hedef kullanılabilirlik kümeleri**: varsayılan olarak, Site Recovery hedef bölgesindeki "asr" son ekini içeren yeni bir kullanılabilirlik oluşturur. 
   - **Çoğaltma İlkesi adı**: İlke adı.
   - **Kurtarma noktası bekletme**: varsayılan olarak Site Recovery kurtarma noktalarına 24 saat tutar. 1 ila 72 saat arasında bir değer yapılandırabilirsiniz.
   - **Uygulamayla tutarlı anlık görüntü sıklığı**: varsayılan olarak Site Recovery 4 saatte bir uygulamayla tutarlı anlık görüntü alır. 1 ve 12 saat arasında herhangi bir değer yapılandırabilirsiniz. Verileri sürekli olarak çoğaltılır:
    - Kilitlenme tutarlı kurtarma noktalarına tutarlı veri yazma-sırası oluşturduğunuzda korur. Bu tür bir kurtarma noktası uygulamanızı çökmeyle veri tutarsızlıkları olmadan kurtarılır tasarlandıysa genellikle yeterli olur
    - Kilitlenme tutarlı kurtarma noktalarına birkaç dakikada üretilir. Yük devri ve Vm'lerinizi kurtarmak için bu kurtarma noktalarını kullanarak bir kurtarma noktası hedefi (RPO) dakika sırasına göre sağlar.
    - Uygulamayla tutarlı kurtarma noktaları (ek olarak yazma sipariş tutarlılık) çalışan uygulamalar tüm işlemleri tamamlamak ve arabellekler (uygulama sessiz moda) diske temizleme emin olun. SQL Server, Oracle ve Exchange gibi veritabanı uygulamaları için bu kurtarma noktalarını kullanmanızı öneririz.
        
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Ayarları değiştirme

Hedef ve çoğaltma ilkesi ayarlarını değiştirmek istiyorsanız aşağıdakileri yapın:

1. Hedef ayarlarını görüntülemek veya değiştirmek için tıklatın **ayarları**.
2. Varsayılan hedefi ayarlarını geçersiz kılmak için tıklatın **Özelleştir**. Hedef kaynak grubu, sanal ağ, kullanılabilirlik kümesi ve hedef depolama hesabı belirtebilirsiniz. Vm'leri kaynak bölge kümesinde parçası ise yalnızca kullanılabilirlik kümeleri ekleyebilirsiniz.

    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Kurtarma noktaları ve uygulamayla tutarlı anlık görüntüler için çoğaltma ayarlarını geçersiz kılmak için tıklatın **Özelleştir** yanına **Çoğaltma İlkesi**.
 
    ![Ayarları yapılandırma](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. Hedef kaynakları hazırlamaya başlamak için tıklatın **hedef kaynakları oluşturmak**. Sağlama veya bunu bir dakika sürer. Sağlama işlemi sırasında dikey pencereyi kapatmayın veya baştan başlamak zorunda kalırsınız.




## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

1. İçinde **ayarları**, tıklatın **çoğaltmasını etkinleştir**. Bu, seçili sanal makinelerin ilk çoğaltmasının sağlar. İlk çoğaltma durumunu yenilemek için biraz zaman alabilir. Tıklatın **yenileme** en son durumunu almak için.

2. İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**.

3. İçinde **ayarları** > **çoğaltılan öğeler**, VM'ler ve ilk çoğaltma ilerleme durumunu görüntüleyebilirsiniz. VM ayarlarına detaya gitmek için tıklayın.



## <a name="next-steps"></a>Sonraki adımlar

Git [6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)
