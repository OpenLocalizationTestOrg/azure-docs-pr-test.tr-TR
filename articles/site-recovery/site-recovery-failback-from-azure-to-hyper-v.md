---
title: "Hyper-v sanal makineleri için Azure Site kurtarma aaaFailback | Microsoft Docs"
description: "Azure Site Recovery hello çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Azure tooon içi veri merkezi gelen yeniden çalışma hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Site kurtarma Hyper-V sanal makineleri için yeniden çalışma

Bu makalede Site Recovery tarafından korunan nasıl toofailback sanal makine açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
1. Bu hello birincil site VMM sunucusu/Hyper-V sunucusu bağlı emin olun.
2. Gerçekleştirilen **yürütme** hello sanal makine üzerinde.

## <a name="why-is-there-no-button-called-failback"></a>Neden geri dönme adlı bir düğme var mı?
Merhaba portalında yeniden çalışma adlı hiçbir açık hareketi yoktur. Yeniden çalışma, toohello birincil siteye geri dönün burada bir adımdır. Yük devretme hello sanal makinelerden primary(on-premises) site toorecovery (Azure) ve yeniden çalışma, yük devretme hello sanal makineleri kurtarma tooprimary yedeklediğinizde tanım olarak, yük devretme olur.

Bir yük devretme başlatın, hello dikey penceresinde hello iş hello yönü hakkında sizi bilgilendirir. Merhaba yönü Azure tooOn içi ise, bir yeniden çalışma olur.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Neden yalnızca bir planlı yük devretme hareketi toofailback var mı?
Azure yüksek oranda kullanılabilir bir ortamdır ve sanal makinelerinizin her zaman kullanılabilir olur. Yeniden çalışma hello iş yükleri şirket içi yeniden çalıştırmayı başlayabilmeniz için burada tootake kısa bir kapalı kalma süresi karar planlı bir etkinliktir. Bu, veri kaybı bekliyor. Bu nedenle yalnızca bir planlı yük devretme hareketi kullanılabilir ve, azure'da hello VM kapatmak, hello en son değişiklikleri indirir ve veri kaybı olduğundan emin olun.

## <a name="initiate-failback"></a>Yeniden başlatma
Yük devretme hello birincil toosecondary konumdan sonrasında çoğaltılmış sanal makinelere Site Recovery tarafından korunmayan ve hello ikincil konum şimdi hello etkin konumu olarak çalışıyor. Bu yordamlar toofail geri toohello özgün birincil site izleyin. Bu yordam açıklar nasıl toorun planlanmış bir yük devretme için bir kurtarma planı. Alternatif olarak hello üzerinde tek bir sanal makine için yük devretme hello çalıştırabilirsiniz **sanal makineleri** sekmesi.

1. Seçin **kurtarma planları** > *recoveryplan_name*. Tıklatın **yük devretme** > **planlanan yük devretme**.
2. Merhaba üzerinde ** planlı yük devretme onaylayın ** sayfasında, hello kaynak ve hedef konumların seçin. Merhaba yük devretme yönü unutmayın. Birincil Hello devretmeyi çalışılan olarak beklediğiniz ve bu yalnızca bilgi amaçlıdır hello ikincil konumdaki tüm sanal makineler demektir.
3. Yeniden çalıştırma işlemini gerçekleştiriyorsanız ayarlarında seçin **veri eşitleme**:

   * **Yük devretme (yalnızca Eşitle delta değişiklikleri) önce verileri eşitlemek**— kapatmadan bunları eşitlediği bu seçeneği sanal makineler için kapalı kalma süresi en aza indirir. Aşağıdaki hello:
     * 1. Aşama: Azure'da hello sanal makinenin anlık görüntüsünü alır ve toohello şirket içi Hyper-V konağına kopyalar. Merhaba makine Azure'da çalışan devam eder.
     * 2. Aşama: yeni değişiklik yok gerçekleşmesi azure'da hello sanal makine kapatır. Merhaba son delta değişiklikleri kümesidir aktarılan toohello şirket içi sunucu ve hello şirket içi sanal makine başlatıldı.

    - **Verileri (tam yükleme) yalnızca yük devretme sırasında eşitleme**— Azure üzerinde uzun bir süredir çalışan, bu seçeneği kullanın. Bu seçenek daha hızlı çünkü hello disk çoğunu değişti ve biz sağlama toplamı hesaplama toospend zamanında istemiyorsanız bekliyoruz. Merhaba diskin yükleme gerçekleştirir. Merhaba şirket içi sanal makine silindiğinde de yararlıdır.

    >[!NOTE]
    >Kullanıyorsanız bu seçenek Azure bir süre için çalışır durumda öneririz (ayda bir veya daha fazla) veya hello şirket içi sanal makine silindi. Bu seçenek, sağlama toplamı hesaplamaları gerçekleştirmez.
    >
    >




4. Veri şifreleme hello bulut için etkinleştirilmişse **şifreleme anahtarı** hello VMM sunucusunda Sağlayıcı yükleme sırasında veri şifrelemesi etkin olduğunda, verilen seçim hello sertifika.
5. Merhaba yük devretme başlatın. Merhaba üzerinde hello yük devretme işleminin ilerleyişini izleyebilirsiniz **işleri** sekmesi.
6. Merhaba seçeneği toosynchronize hello veri hello yük devretme, bir kez veri eşitleme tamamlandıktan ve sizin gerçekten, azure'da hello sanal makineler aşağı hazır tooshut ilk hello önce seçtiyseniz tıklayın **işleri** planlı yük devretme iş adı **Tamamlamak yük devretme**. Bu Azure makine Merhaba, aktarımları hello toohello şirket içi sanal makineyi en son değişiklikleri ve içi VM başlatıldığında hello kapanır.
7. Artık oturum hello sanal makine toovalidate beklendiği gibi kullanılabilir.
8. yürütme bekleme durumuna Hello sanal makine kullanılıyor. Tıklatın **yürütme** toocommit hello yük devretme.
9. Sırayla toocomplete hello geri dönme tıklatın artık **ters çoğaltma** hello birincil sitede hello sanal makine koruma toostart.

## <a name="failback-tooan-alternate-location"></a>Yeniden çalışma tooan alternatif bir konum
Koruması arasında dağıttıktan sonra bir [Hyper-V sitesi ve Azure](site-recovery-hyper-v-site-to-azure.md) Azure tooan alternatif şirket içi konumdan tooability toofailback sahip. Bu yeni şirket içi donanım yukarı tooset gerektiğinde kullanışlı olur. Bunun nasıl yapılacağı aşağıda verilmiştir.

1. Yeni donanım ayarlıyorsanız Windows Server 2012 R2 yükleyin ve Hyper-V rolünü hello sunucuda hello.
2. Merhaba hello özgün sunucuda olan aynı ad ile bir sanal ağ anahtarı oluşturun.
3. Seçin **korunan öğeler** -> **koruma grubu**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> geri toofail istediğiniz ve seçin **planlanmış Yük devretme**.
4. İçinde **planlı yük devretme onaylayın** seçin **oluşturma şirket içi sanal makine değil mevcut değilse**.
5. İçinde **ana bilgisayar adı** hello tooplace hello sanal makine istediğiniz yeni Hyper-V konak sunucusu seçin.
6. Veri eşitlemesi hello seçeneğini belirleyin olan öneririz **hello yük devretme önce hello verileri eşitlemek**. Kapatmadan bunları eşitlediği, sanal makineler için kapalı kalma süresi daha en aza indirir. Aşağıdaki hello:

   * 1. Aşama: Azure'da hello sanal makinenin anlık görüntüsünü alır ve toohello şirket içi Hyper-V konağına kopyalar. Merhaba makine Azure'da çalışan devam eder.
   * 2. Aşama: yeni değişiklik yok gerçekleşmesi azure'da hello sanal makine kapatır. Merhaba son değişiklikler kümesidir aktarılan toohello şirket içi sunucu ve hello şirket içi sanal makine başlatıldı.
7. Merhaba onay işareti toobegin hello yük devretme (yeniden çalışma) tıklayın.
8. Merhaba ilk eşitleme tamamlandıktan sonra azure'da hello sanal makinede aşağı hazır tooshut olduğunuz, tıklatın **işleri** > <planned failover job> > **yük devretmeyi tamamlamak**. Bu hello Azure makine kapatan, aktarımları hello en son değişiklikleri toohello şirket içi sanal makine ve başlar.
9. Merhaba şirket içi sanal makine tooverify her şeyin beklendiği gibi çalıştığını oturum açabilir. Ardından **yürütme** toofinish hello yük devretme.
10. Tıklatın **ters çoğaltma** hello şirket içi sanal makine koruma toostart.

    > [!NOTE]
    > Veri Eşitleme adımda durumdayken hello yeniden çalışma işinin iptal ederseniz hello VM bozuk durumda olacaktır şirket içi. Veri Eşitleme hello en son verileri Azure VM diskleri toohello şirket içi veri disklerinden kopyalar ve hello eşitleme tamamlanana kadar hello disk verileri tutarlı bir durumda olmayabilir nedeni budur. Veri Eşitleme iptal edildikten sonra hello şirket içi VM önyüklendiğinde, önyüklenemez. Yük devretme toocomplete hello veri eşitlemeyi yeniden tetikleyin.
    >
    >



## <a name="next-steps"></a>Sonraki Adımlar

Merhaba yeniden çalışma işlemini tamamladıktan sonra **yürütme** hello sanal makine. Yürütme hello Azure sanal makinesi ve onun diskleri siler ve yeniden korunan hello VM toobe hazırlar.

Sonra **yürütme**, hello başlatabilirsiniz *ters çoğaltma*. Bu, şirket içi geri tooAzure hello sanal makine koruma başlatır. Bu olacağı yalnızca çoğaltma hello değişiklikler yalnızca VM Azure'da devre dışı ve bu nedenle fark gönderir hello değiştirir beri unutmayın.
