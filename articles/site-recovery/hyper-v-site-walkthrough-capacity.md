---
title: "Kapasite ve Hyper-V VM (VMM olmadan) çoğaltma tooAzure Azure Site Recovery ile ölçeklendirme aaaPlan | Microsoft Docs"
description: "Bu makale tooplan kapasite ve ölçek Azure Site Recovery ile Hyper-V sanal makineleri tooAzure çoğaltırken kullanın"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a>3. adım: kapasite ve Hyper-V tooAzure çoğaltma için ölçeklendirme planlama

Bu makale toofigure için kapasite planlaması ve ölçeklendirme, şirket içi Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure ile çoğaltırken kullanmak [Azure Site Recovery](site-recovery-overview.md).

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Kapasite planlama nasıl başlamanız gerekir?


Çoğaltma ortamınız hakkında bilgi toplamak ve bu makalede vurgulanmış hello konuları birlikte bu bilgileri kullanarak kapasite planlama.


## <a name="gather-information"></a>Bilgileri toplayın

1. VM'ler, VM başına disk ve disk başına depolama dahil olmak üzere çoğaltma ortamınız hakkında bilgi toplayın.
2. Çoğaltılan veriler için günlük değişim (dalgalanma) oranı tanımlayın. Merhaba karşıdan [Hyper-V kapasite planlama aracı](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello değişim oranı. Ortalamalar hafta toocapture bu aracı çalıştırın öneririz.
 

## <a name="figure-out-capacity"></a>Kapasitesi Şekil

Toplama seçtiğiniz hello bilgilere dayanarak hello çalıştırmak [Site kurtarma kapasite planlayıcısı aracı](http://aka.ms/asr-capacity-planner-excel) tooanalyze kaynak ortamınız ve iş yükleri, bant genişliği gereksinimlerini ve sunucu kaynaklarını hello kaynak konumu için tahmin etmek ve hello Merhaba hedef konumda gereken kaynakları (sanal makineler ve depolama vb.). Merhaba aracı modları birkaç içinde çalıştırabilirsiniz:

- Hızlı planlama: hello aracı tooget ağ ve sunucu tahminleri ortalama bir VM'ler, diskleri, depolama ve değişim oranı sayısına göre bu modda çalıştırın.
- Ayrıntılı planlama: Bu modda hello aracını çalıştırın ve her iş yükü VM düzeyinde ayrıntılarını sağlayın. VM uyumluluk çözümlemek ve ağ ve sunucu tahminleri alın.

Şimdi hello aracını çalıştırın:

1. Merhaba karşıdan [aracı](http://aka.ms/asr-capacity-planner-excel)
2. toorun hello hızlı Planlayıcısı izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-quick-planner)ve select hello senaryo **Hyper-V tooAzure**.
3. toorun Merhaba ayrıntılı Planlayıcısı, izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-detailed-planner)ve select hello senaryo **Hyper-V tooAzure**.

## <a name="control-network-bandwidth"></a>Ağ bant genişliğini denetlemek

Gereksinim duyduğunuz hesaplanan hello bant genişliği sonra birkaç hello çoğaltma için kullanılan bant genişliği miktarını kontrol eden için seçenekler vardır:

* **Bant genişliğini kısıtlama**: tooAzure çoğaltır Hyper-V trafiği belirli bir Hyper-V ana bilgisayar üzerinden gider. Merhaba ana bilgisayar sunucusunda bant genişliğini kısıtlayabilirsiniz.
* **Bant genişliği üzerinde etki**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan hello bant genişliği etkileyebilir.

### <a name="throttle-bandwidth"></a>Bant genişliğini kısıtlama
1. Merhaba Hyper-V konak sunucusunda Hello Microsoft Azure Backup MMC eklentisini açın. Varsayılan olarak Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir durumdadır.
2. Merhaba ek bileşeninde tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **azaltma** sekmesini seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**, iş için hello sınırını ayarlama ve saat İş dışı. Geçerli aralıklar saniye başına 512 Kbps too102 Mbps arasındadır.

    ![Bant genişliğini kısıtlama](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

Merhaba de kullanabilirsiniz [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset cmdlet azaltma. Bu ayara ilişkin örneği aşağıda bulabilirsiniz:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.

### <a name="influence-network-bandwidth"></a>Ağ bant genişliği üzerinde etki oluşturma
1. Merhaba kayıt defterinde çok gidin**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * bir çoğaltma diskte tooinfluence hello bant genişliği trafiği değiştirebilir hello değeri hello **UploadThreadsPerVM**, veya yoksa hello anahtar oluşturun.
   * Azure, yeniden çalışma trafiği için tooinfluence hello bant genişliği değiştirme hello değeri **DownloadThreadsPerVM**.
2. Merhaba varsayılan değer 4'tür. "Fazla sağlanan" bir ağda, bu kayıt defteri anahtarları hello varsayılan değerlerinin değiştirilmesi. Merhaba en fazla 32'dir. Trafik toooptimize hello değeri izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).
