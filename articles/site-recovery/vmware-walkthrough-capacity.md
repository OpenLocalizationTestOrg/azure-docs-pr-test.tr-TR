---
title: "Kapasite ve Azure Site Recovery ile VMware çoğaltma tooAzure için ölçeklendirme aaaPlan | Microsoft Docs"
description: "Bu makale tooplan kapasite ve ölçek Azure Site Recovery ile VMware Vm'lerini tooAzure çoğaltırken kullanın"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 551533ab7090d85c216be242ea92781deb8287ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-tooazure-replication"></a>3. adım: kapasite ve VMware tooAzure çoğaltma için ölçeklendirme planlama

Bu makale toofigure için kapasite planlaması ve ölçeklendirme, şirket içi VMware Vm'lerini ve fiziksel sunucuları tooAzure ile çoğaltırken kullanmak [Azure Site Recovery](site-recovery-overview.md).

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="how-do-i-start-capacity-planning"></a>Kapasite planlama nasıl başlamanız gerekir?

Çoğaltma ortamınız hakkında bilgi toplamak ve bu makalede vurgulanmış hello konuları birlikte bu bilgileri kullanarak kapasite planlama.


## <a name="gather-information"></a>Bilgileri toplayın

1. Merhaba karşıdan [dağıtım planlayıcısı aracı](https://aka.ms/asr-deployment-planner) VMware çoğaltma için.
2. [Bu makaleyi okuyun](site-recovery-deployment-planner.md) toounderstand nasıl toorun hello aracı.
3. Merhaba aracını kullanarak, uyumlu ve uyumsuz VM'ler, VM başına disk hakkında bilgi toplamak ve disk başına veri karmaşıklığı. Hello aracı ayrıca ağ bant genişliği gereksinimlerini ve hello başarılı çoğaltma ve test yük devretme için gereken Azure altyapı kapsar.

## <a name="replication-considerations"></a>Çoğaltma konuları

Dağıtıma başlamadan önce bu noktalar göz önünde bulundurun:

**Bileşen** | **Ayrıntılar** |
--- | --- | ---
**Çoğaltma** | **Maksimum günlük değişim oranı:** korumalı makine yalnızca bir işlem sunucusunu kullanabilir ve tek işlem sunucusu bir günlük değişikliği oranını too2 TB işleyebilir. Bu nedenle 2 TB hello maksimum günlük veri korumalı bir makine için desteklenen oranı değiştirmektir.<br/><br/> **En yüksek verimlilik:** çoğaltılmış bir makineden Azure depolama hesabında tooone ait olabilir. Standart depolama hesabı 20.000 istekleri saniye başına maksimum işleyebilir ve bir kaynak makine too20 arasında 000 girdi/çıktı işlemleri (IOPS) saniyede hello sayısı tutmanızı öneririz. Örneğin, kaynak makine 5 disklerle varsa ve 120 IOPS (8 K boyut) hello kaynak makinedeki her disk oluşturur, ardından bunu hello Azure başına 500 disk IOPS sınırı içinde olacaktır. (Merhaba gerekli depolama hesapları tarafından 20.000 bölünmüş eşit toohello toplam kaynak makine IOPS, sayısıdır.)

## <a name="configuration-server-capacity"></a>Yapılandırma sunucusu kapasite

Merhaba yapılandırma sunucusu mümkün toohandle hello günlük değişikliği oranı kapasite korumalı makinelerde çalışan tüm iş yükleri arasında olmalı ve yeterli bant genişliği toocontinuously veri tooAzure depolama çoğaltılması.

En iyi uygulama, hello yapılandırma sunucusu üzerinde hello bulun. aynı ağ ve LAN kesimi olarak hello tooprotect istediğiniz makineler. Farklı bir ağ, ancak tooprotect Katman 3 ağ görünürlük tooit olmalıdır istediğiniz makineler üzerinde bulunabilir.

## <a name="sizing-recommendations"></a>Boyutlandırma önerileri

Merhaba tablo CPU üzerinde göre boyutlandırma önerileri özetler.

**CPU** | **Bellek** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler**
--- | --- | --- | --- | ---
8 Vcpu'lar (2 yuva * 2,5 gigahertz [GHz] @ 4 çekirdek) | 16 GB | 300 GB | 500 GB veya daha az | 100'den az makineler çoğaltılır.
12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) | 18 GB | 600 GB | 500 GB too1 TB | 100-150 makineler arasında çoğaltılır.
16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek) | 32 GB | 1 TB | 1 TB too2 TB | 150-200 makineler arasında çoğaltılır.
Başka bir işlem sunucusu Dağıt | | | > 2 TB | Ek işlem sunucusu 200'den fazla makineleri çoğaltma yapıyorsanız ya da hello günlük verileri değiştirirseniz oranı 2 TB aştığında dağıtın.

Konumlar:

* Her kaynak makine 3 100 GB disk ile yapılandırılır.
* 10 bin RPM, 8 SAS sürücüleri Kıyaslama depolanmasını RAID 10 ile için önbellek disk ölçümleri kullandık.

## <a name="process-server-capacity"></a>İşlem sunucusu kapasite


Merhaba işlem sunucusu korunan makinelerden çoğaltma verilerini alıp ve önbelleğe alma, sıkıştırma ve şifreleme iyileştirir. Ardından hello veri tooAzure gönderir.

- Merhaba işlem Sunucu makinesi yeterli kaynakları tooperform bu görevleri olması gerekir.
- Merhaba ilk işlem sunucusu hello yapılandırma sunucusuna varsayılan olarak yüklenir. Ortamınıza ek işlem sunucuları tooscale dağıtabilirsiniz.
- Merhaba işlem sunucusu disk tabanlı önbelleği kullanır. 600 GB veya daha fazla toohandle veri değişiklikleri, bir ağ sorununu veya kesinti hello olayda depolanan ayrı önbelleği disk kullanın.
- 200'den fazla makinelerin tooprotect gerekir veya hello günlük değişim oranı 2 TB'den büyükse, işlem sunucuları toohandle hello çoğaltma yük ekleyebilirsiniz. tooscale çıkış şunları yapabilirsiniz:
    - Yapılandırma sunucularına Hello sayısını artırın. Örneğin, iki yapılandırma sunucularına too400 makinelerle koruyabilirsiniz.
    - Daha fazla işlem sunucusu ekleyebilir ve bu toohandle trafiği yerine (veya ek olarak) hello yapılandırma sunucusu kullanabilirsiniz.


### <a name="example-process-server-scaling"></a>Örnek sunucu işlemi ölçeklendirme

Aşağıdaki tablonun hello bir senaryoda açıklanmaktadır:

* Toouse hello yapılandırma sunucusuna işlem sunucusu olarak planlamanız durumunda değil.
* Bir ek işlem sunucusu ayarlamadıysanız ayarladınız.
* Korumalı sanal makineleri toouse hello ek işlem sunucusu yapılandırdıktan.
* Her korumalı kaynak makine üç 100 GB disk ile yapılandırılır.

**Yapılandırma sunucusu** | **Ek işlem sunucusu** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler**
--- | --- | --- | --- | ---
8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB bellek | 4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB bellek | 300 GB | 250 GB veya daha az | 85 veya daha az makineler çoğaltılır.
8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB bellek | 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB bellek | 600 GB | 250 GB too1 TB | 85 150 makineler arasında çoğaltılır.
12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek), 18 GB bellek | 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB bellek | 1 TB | 1 TB too2 TB | 150-225 makineler arasında çoğaltılır.

sunucularınızın ölçeklendirme hello büyütme veya genişleme modeli için tercihinizi bağlıdır.  Bazı gelişmiş yapılandırma ve işlem sunucuları dağıtarak ölçeği veya daha az kaynak ile daha fazla sunucu dağıtarak ölçeğini. Örneğin, tooprotect 220 makineler gerekiyorsa, hello aşağıdakilerden birini yapabilirsiniz:

* Merhaba yapılandırma sunucusuyla 12 vCPU, 18 GB bellek ve ek işlem sunucusu 12 vCPU, 24 GB bellek ile ayarlayın. Korumalı makineler toouse hello ek işlem sunucusu yalnızca yapılandırın.
* İki yapılandırma sunucularına (2 x 8 vCPU, 16 GB RAM) ve iki ek işlem sunucusu (1 x 8 vCPU ve 4 vCPU x 1 toohandle 135 + 85 [220] makineler) ayarlayın. Korumalı makineler toouse hello ek işlem yalnızca sunucuları yapılandırın.

## <a name="deploy-additional-process-servers"></a>Ek işlem sunucusu dağıtın

Bu yönergeler tooset bir ek işlem sunucusu izleyin. Kaynak makine toouse geçirmek Hello sunucuyu ayarladıktan sonra onu.

1. İçinde **Site Recovery sunucuları**, hello yapılandırma sunucusu tıklayın > **+ işlem sunucusu**.
2. İçinde **sunucu türü**, tıklatın **işlem sunucusu (şirket içi)**.

    ![İşlem sunucusu](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. Merhaba Site kurtarma birleşik kurulum dosyasını karşıdan yükleyin.
4. Kurulum tooinstall hello işlem sunucusu çalıştırın ve hello kasaya kaydedin.
5. İçinde **başlamadan önce**seçin **ek işlem sunucuları tooscale dağıtım çıkışı eklemek**.
6. İçinde **yapılandırma sunucusu ayrıntılarını**hello hello yapılandırma sunucusu IP adresini belirtin ve parola hello. Merhaba parola yoksa, çalıştırarak alın **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello yapılandırma sunucusundaki.

    ![Yapılandırma sunucusu](./media/vmware-walkthrough-capacity/add-ps2.png)
7. Merhaba kurulumunda hello geri kalanını tamamlamak hello yapılandırma sunucuyu ayarladığınızda yaptığınız şekilde.

### <a name="migrate-machines-toouse-hello-process-server"></a>Makineler toouse hello işlem sunucusu geçirme

1. İçinde **ayarları** > **Site Recovery sunucuları**, hello yapılandırma sunucusu tıklayın > **işlem sunucuları**.
2. Sağ hello işlem sunucusu şu anda kullanımda > **anahtar**.

    ![Anahtar işlem sunucusu](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. İçinde **Select hedef işlem sunucusunu**seçin toouse istediğiniz ve hello VM'ler seçin hello işlem sunucusu hello sunucu işleyecek.
4. Merhaba bilgi simgesine tıklayın. toohelp yaptığınız kararları yüklenemedi, her seçili VM toohello yeni işlem sunucusu görüntülenen tooreplicate gerekli olan ortalama alanı hello.
5. Merhaba onay işareti toostart çoğaltma toohello yeni işlem sunucusu tıklayın.

## <a name="control-network-bandwidth"></a>Ağ bant genişliğini denetlemek

Çalıştırdıktan sonra [hello dağıtım planlayıcısı aracı](site-recovery-deployment-planner.md) toocalculate hello bant genişliği (Merhaba ilk çoğaltma ve ardından değişim) çoğaltma için gereken, hello birkaç seçenekleri kullanarak çoğaltma için kullanılan bant genişliği miktarını kontrol edebilirsiniz:

* **Bant genişliğini kısıtlama**: tooAzure çoğaltır VMware trafiği belirli işlem sunucusu üzerinden gider. İşlem sunucusu olarak çalışan hello makineler üzerinde bant genişliğini kısıtlayabilirsiniz.
* **Bant genişliği üzerinde etki**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan hello bant genişliği etkileyebilir:
  * Merhaba **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** kayıt defteri değeri hello veri aktarımını bir disk için (başlangıç ve değişim çoğaltması) kullanılan iş parçacığı sayısını belirtir. Daha yüksek bir değer çoğaltma için kullanılan hello ağ bant genişliğini artırır.
  * Merhaba **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** hello yeniden çalışma sırasındaki veri aktarımı için kullanılan iş parçacığı sayısını belirtir.

### <a name="throttle-bandwidth"></a>Bant genişliğini kısıtlama

1. Azure Backup MMC ek bileşenini Hello hello makine hareket üzerinde hello işlem sunucusu olarak açın. Varsayılan olarak, yedekleme için bir kısayol hello masaüstünde veya klasör aşağıdaki hello kullanılabilir: C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda.
2. Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **azaltma** sekmesine **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**.
4. İş için Hello sınırlarını ayarlama ve saat İş dışı. Geçerli aralıklar saniye başına 512 Kbps too102 Mbps arasındadır.

    ![Kısıtlama](./media/vmware-walkthrough-capacity/throttle2.png)

Merhaba de kullanabilirsiniz [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset cmdlet azaltma. Bu ayara ilişkin örneği aşağıda bulabilirsiniz:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.

### <a name="influence-network-bandwidth-for-a-vm"></a>Bir VM için ağ bant genişliği üzerinde etki

1. Merhaba VM kayıt defterinde çok Git**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * bir çoğaltma diskte tooinfluence hello bant genişliği trafiği değiştirebilir hello değerini **UploadThreadsPerVM**, veya yoksa hello anahtar oluşturun.
   * Azure, yeniden çalışma trafiği için tooinfluence hello bant genişliği hello değerini değiştirmek **DownloadThreadsPerVM**.
2. Merhaba varsayılan değer 4'tür. Fazla sağlanan bir ağda, bu kayıt defteri anahtarları değiştirilmesi gerekir. Merhaba en fazla 32'dir. Trafik toooptimize hello değeri izleyin.




## <a name="next-steps"></a>Sonraki adımlar

Çok Git[4. adım: ağ planlama](vmware-walkthrough-network.md).
