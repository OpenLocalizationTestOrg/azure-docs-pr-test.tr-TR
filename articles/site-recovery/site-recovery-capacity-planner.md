---
title: "Azure aaaEstimate çoğaltma kapasite | Microsoft Docs"
description: "Bu makale tooestimate kapasite Azure Site Recovery ile çoğaltırken kullanın"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Sanal makineler ve Azure Site kurtarma fiziksel sunucuları koruma için kapasite planlaması

Hello Azure Site kurtarma kapasite planlayıcısı aracı kapasite gereksinimlerinizi çıkışı toofigure Hyper-V sanal makineleri, VMware sanal makinelerini ve Windows/Linux fiziksel sunucuları, Azure Site Recovery ile çoğaltırken yardımcı olur.

Bant genişliği gereksinimlerini ve sunucu kaynaklarını hello kaynak konumu için gerekir ve hello hedef ihtiyacınız olan hello kaynakları (sanal makineler ve depolama vb.), tahmin, kaynak ortamınız ve iş yükleri Hello Site kurtarma kapasite Planlayıcısı tooanalyze kullanın konum.

Merhaba aracı modları birkaç içinde çalıştırabilirsiniz:

* **Hızlı planlama**: hello aracı tooget ağ ve sunucu tahminleri ortalama bir VM'ler, diskleri, depolama ve değişim oranı sayısına göre bu modda çalıştırın.
* **Planlama ayrıntılı**: Bu modda hello aracını çalıştırın ve her iş yükü VM düzeyinde ayrıntılarını sağlayın. VM uyumluluk çözümlemek ve ağ ve sunucu tahminleri alın.

## <a name="before-you-start"></a>Başlamadan önce


1. VM'ler, VM, disk başına depolama başına diskler dahil olmak üzere ortamınız hakkında bilgi toplayın.
2. Çoğaltılan veriler için günlük değişim (dalgalanma) oranı tanımlayın. toodo bu:

   * Hyper-V sanal makinelerini çoğaltıyorsanız hello karşıdan [Hyper-V kapasite planlama aracı](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello değişim oranı. [Daha fazla bilgi edinin](site-recovery-capacity-planning-for-hyper-v-replication.md) bu araç hakkında. Ortalamalar hafta toocapture bu aracı çalıştırın öneririz.
   * VMware sanal makinelerini çoğaltıyorsanız hello kullan [Azure Site Recovery dağıtımı Planlayıcısı](./site-recovery-deployment-planner.md) hello çıkışı toofigure karmaşıklığı oranı.
   * Fiziksel sunucuları çoğaltma yapıyorsanız, tooestimate el ile yapmanız gerekir.

## <a name="run-hello-quick-planner"></a>Merhaba hızlı Planlayıcısını çalıştırın
1. Karşıdan yükleyip açmak hello [Azure Site kurtarma kapasite Planlayıcısı](http://aka.ms/asr-capacity-planner-excel) aracı. Toorun makroları, böylece select tooenable düzenleme ve etkinleştirme istendiğinde içerik gerekir.
2. İçinde **Planlayıcısı türünü seçin** seçin **hızlı Planlayıcısı** hello liste kutusundan.

   ![Başlarken](./media/site-recovery-capacity-planner/getting-started.png)
3. Merhaba, **kapasite Planlayıcısı** çalışma hello gerekli bilgileri girin. Merhaba ekran görüntüsü aşağıda kırmızı daire içinde tüm hello alanlarını doldurmanız gerekir.

   * İçinde **senaryonuz seçin**, seçin **Hyper-V tooAzure** veya **VMware/fiziksel tooAzure**.
   * İçinde **ortalama günlük veri değişikliği oranı (%)**, hello bilgileri toplayın hello kullanarak put [Hyper-V kapasite planlama aracı](site-recovery-capacity-planning-for-hyper-v-replication.md) veya hello [Azure Site Recovery dağıtımı Planlayıcısı](./site-recovery-deployment-planner.md).  
   * **Sıkıştırma** yalnızca VMware Vm'lerini veya fiziksel sunucuları tooAzure çoğaltırken sunulan toocompression geçerlidir. % 30 veya daha fazla tahmin ediyoruz ancak hello ayarı gerektiği gibi değiştirebilirsiniz. Hyper-V sanal makineleri tooAzure sıkıştırma çoğaltmak için Riverbed gibi bir üçüncü taraf uygulaması kullanabilirsiniz.
   * İçinde **bekletme girişleri**, çoğaltmaları ne kadar süre tutulacağını belirtin. VMware veya fiziksel sunucuları çoğaltıyorsanız gün içinde hello değeri girin. Hyper-V çoğaltıyorsanız hello süresi saat cinsinden belirtin.
   * İçinde **hello toplu sanal makine için ilk çoğaltmanın saat sayısını tamamlamanız gereken** ve **ilk çoğaltma toplu iş başına sanal makine sayısını**, kullanılan ayarları giriş toocompute ilk çoğaltma gereksinimleri.  Site Recovery dağıttığınızda hello tüm ilk veri kümesi yüklenmelidir.

   ![Girişleri](./media/site-recovery-capacity-planner/inputs.png)
4. Merhaba kaynak ortamı için hello değerleri yerleştirdiğiniz sonra görüntülenen çıktının içerir:

   * **Delta çoğaltma için gereken bant genişliği** (MB/sn). Değişim çoğaltması için ağ bant genişliği hello ortalama günlük veri değişikliği hızını üzerinde hesaplanır.
   * **İlk çoğaltma için gereken bant genişliği** (MB/sn). İlk çoğaltma için ağ bant genişliği içine hello ilk çoğaltma değerleri hesaplanır.
   * **Depolama (GB) gerekli** hello toplam Azure depolama gerekli.
   * **Standart depolama hesaplarında IOPS toplam** 8 K IOPS birim boyutu hello toplam standart depolama hesaplarında temel alınarak hesaplanır.  Tüm hello kaynak VM'ler diskleri ve veri değişikliği hızını günlük Hello hızlı Planlayıcısı hello numarası temel alınarak hesaplanır. İçin ayrıntılı Planlayıcısı Merhaba, hesaplanan göre toplam sayısını eşlenen toostandard Azure VM'ler VM'ler hello sayıdır ve verileri bu VM'lerin oranına değiştirin.
   * **Standart depolama hesabı sayısı** hello VM'ler hello standart depolama hesapları gerekli tooprotect toplam sayısını sağlar. Standart depolama hesabı bir standart depolama birimindeki tüm hello VM'ler arasında too20000 IOPS tutun ve disk başına en fazla 500 IOPS desteklenir.
   * **Gerekli blob disk sayısını** hello Azure depolama alanında oluşturulacak disk sayısını verir.
   * **Premium depolama hesapları gerekli sayısı** hello VM'ler hello premium depolama hesapları gerekli tooprotect toplam sayısını sağlar. Bir kaynak VM yüksek IOPS (20000 büyük) ile bir premium depolama hesabı gerekiyor. Premium depolama hesabı too80000 IOPS basılı tutabilirsiniz.
   * **Premium depolama IOPS toplam** 256 K IOPS birim boyutu hello toplam premium depolama hesaplarında temel alınarak hesaplanır.  Tüm hello kaynak VM'ler diskleri ve veri değişikliği hızını günlük Hello hızlı Planlayıcısı hello numarası temel alınarak hesaplanır. İçin ayrıntılı Planlayıcısı Merhaba, hello sayısı hesaplanan göre hello toplam eşlenen toopremium Azure VM (DS ve GS serisi) olan VM'ler sayısıdır ve bu VM'lerin oranına hello veri değiştirin.
   * **Gerekli yapılandırma sunucularına sayısı** kaç yapılandırma sunucularına hello dağıtımı için gerekli olduğunu gösterir.
   * **Gerekli ek işlem sunucu sayısını** ek işlem sunucuları ekleme toohello işlem Server'daki hello yapılandırma sunucusu üzerinde varsayılan olarak çalışan gerekip gerekmediğini gösterir.
   * **% 100 ek depolama alanı hello kaynağında** ek depolama alanı hello kaynak konumda gerekli olup olmadığını gösterir.

   ![Çıktı](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Çalışma hello ayrıntılı Planlayıcısı

1. Karşıdan yükleyip açmak hello [Azure Site kurtarma kapasite Planlayıcısı](http://aka.ms/asr-capacity-planner-excel) aracı. Toorun makroları, böylece select tooenable düzenleme ve etkinleştirme istendiğinde içerik gerekir.
2. İçinde **Planlayıcısı türünü seçin**seçin **ayrıntılı Planlayıcısı** hello liste kutusundan.

   ![Başlarken](./media/site-recovery-capacity-planner/getting-started-2.png)
3. Merhaba, **iş yükü niteliğe** çalışma hello gerekli bilgileri girin. Alanlar olarak işaretlenmiş tüm hello doldurmanız gerekir.

   * İçinde **işlemci çekirdeği**, bir kaynak sunucuda hello toplam çekirdeği sayısını belirtin.
   * İçinde **MB bellek ayırma**, kaynak sunucu hello RAM boyutunu belirtin.
   * Merhaba **numarası, NIC**, bir kaynak sunucuda hello ağ bağdaştırıcılarının sayısını belirtin.
   * İçinde **toplam depolama (GB) cinsinden**, hello VM depolama hello toplam boyutu belirtin. Örneğin, 500 GB 3 disklerle Hello kaynak sunucusu varsa, toplam depolama boyutu 1500 GB olur.
   * İçinde **bağlı disk sayısı**, kaynak sunucunun disklerini hello toplam sayısını belirtin.
   * İçinde **Disk kapasitesi kullanımı**, hello ortalama kullanım belirtin.
   * İçinde **günlük oranı (%) değiştirme**, hello günlük veri değişikliği oranı kaynak sunucunun belirtin.
   * İçinde **eşleme Azure boyutu**, toomap istediğiniz hello Azure VM boyutu girin. Toodo bu işlemi el ile istemiyorsanız tıklayın **işlem Iaas Vm'leri**. El ile ayarlama giriş ve işlem Iaas Vm'leri ardından hello işlem işlemi otomatik olarak Azure VM boyutu en iyi eşleşme hello tanımladığından hello el ile ayarlama üzerine.

   ![İş yükü nitelik](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Tıklatırsanız **işlem Iaas Vm'leri** İşte ne yapar:

   * Merhaba zorunlu girişleri doğrular.
   * IOPS hesaplar ve hello öneren en iyi Azure VM aize çoğaltma tooAzure için uygun olan her sanal makineleri eşleşmiyor. Azure VM uygun boyutta bir hata veren algılanamaz ise. Örneğin, disk Hello sayısı 65 içinde bağlıysa, hello en yüksek boyutu Azure VM 64 olduğundan hata verilir.
   * Bir Azure VM için kullanılabilir bir depolama hesabı önerir.
   * Standart depolama hesapları ve premium depolama hesapları hello iş yükü için gereken toplam sayısını Hello hesaplar. Tooview hello Azure depolama türünü ve kaynak sunucu için kullanılabilir hello depolama hesabı aşağı kaydırın.
   * Tamamlar ve hello rest Merhaba tablonun atanan bir VM ve bağlı diskler hello sayısı için gerekli depolama türü (standart veya premium) göre sıralar. Azure için hello gereksinimleri karşılayan tüm VM'ler için sütun hello **tam VM olduğu?** gösterir **Evet**. Bir VM tooAzure yedeklenemez durumunda bir hata gösterilir.

Sütunları AA tooAE çıktısı alınır ve her VM için bilgiler sağlar.

![İş yükü nitelik](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Örnek
Örneğin, hello tabloda gösterilen hello değerlerle altı VM'ler için hello aracı hesaplar ve hello en iyi Azure VM eşleşme ve hello Azure depolama gereksinimleri atar.

![İş yükü nitelik](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Merhaba örnek çıktıda hello aşağıdakileri göz önünde bulundurun:

  * Merhaba ilk sütun hello VM'ler, diskler ve karmaşıklık için bir doğrulama sütundur.
  * Beş VM'ler için iki standart depolama hesapları ve bir premium depolama hesabı gereklidir.
  * Bir veya daha fazla disk birden fazla 1 TB olduğundan VM3 koruma için uygun değil.
  * VM1 ve VM2 hello ilk standart depolama hesabı kullanabilirsiniz
  * VM4 hello ikinci standart depolama hesabı kullanabilirsiniz.
  * Premium depolama hesabı VM5 ve VM6 gerekir ve her ikisi de tek bir hesap kullanabilirsiniz.

    > [!NOTE]
    > Standart ve premium depolama IOPS hello VM düzeyi ve disk düzeyinde hesaplanır. Standart bir sanal makine, disk başına too500 IOPS yukarı işleyebilir. Bir disk için IOPS 500'den büyükse, premium depolama gerekir. Ancak, bir disk için IOPS 500'den fazla ancak hello toplam VM diskleri içinde hello için standart Azure VM sınırları (VM boyutunu, disk, bağdaştırıcılar, CPU, bellek sayısı sayısı), IOPS'yi destekler hello Planlayıcısı standart VM ve değil hello DS veya GS serisi seçer. Uygun DS veya GS serisi VM ile toomanually güncelleştirme hello eşleme Azure boyutu hücre gerekir.


Tüm hello ayrıntıları hazır olduktan sonra tıklatın **gönderme veri toohello planlayıcısı aracı** tooopen hello **kapasite Planlayıcısı** iş yüklerinin vurgulanmış, tooshow bunlar veya koruma için uygun olup olmadığını.

### <a name="submit-data-in-hello-capacity-planner"></a>Merhaba kapasite Planlayıcısı verileri gönderme
1. Merhaba açtığınızda **kapasite Planlayıcısı** doldurulmuş çalışma göre belirttiğiniz hello ayarları. Merhaba 'İş yükü' hello görünür word **Infra girişleri kaynak** hücre, giriş hello tooshow olduğunda hello **iş yükü niteliğe** çalışma sayfası.
2. Toomake değişiklikleri istiyorsanız, toomodify hello gerekir **iş yükü niteliğe** çalışma sayfası ve tıklatın **gönderme veri toohello planlayıcısı aracı** yeniden.  

   ![Kapasite Planlayıcısı](./media/site-recovery-capacity-planner/capacity-planner.png)
