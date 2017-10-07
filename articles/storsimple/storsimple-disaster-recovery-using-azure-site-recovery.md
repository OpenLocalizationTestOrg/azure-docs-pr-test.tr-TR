---
title: aaaAutomate StorSimple fileshare DR Azure Site Recovery ile | Microsoft Docs
description: "Merhaba adımları ve Microsoft Azure StorSimple depolama alanında barındırılan dosya paylaşımları için olağanüstü durum kurtarma çözümü oluşturmak için en iyi uygulamaları açıklar."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>StorSimple üzerinde barındırılan dosya paylaşımları için Azure Site RECOVERY'yi kullanarak otomatikleştirilmiş olağanüstü durum kurtarma çözümü
## <a name="overview"></a>Genel Bakış
Microsoft Azure StorSimple adresleri genellikle dosya paylaşımları ile ilgili yapılandırılmamış veriler karmaşıklığını hello bir karma bulut depolama çözümüdür. Merhaba uzantısı şirket içi çözüm ve şirket içi depolama ve bulut depolama arasında otomatik olarak veri katmanlarını gibi StorSimple bulut depolama kullanır. Veri koruma, yerel ile tümleşik ve bulut anlık görüntüleri, sprawling bir depolama altyapısını hello gereksinimini ortadan kaldırır.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) çoğaltma, yük devretme ve kurtarma sanal makinelerin düzenleyerek olağanüstü durum kurtarma (DR) özellikleri sağlayan bir Azure tabanlı bir hizmettir. Azure Site Recovery çoğaltma teknolojileri tooconsistently replicate destekler, korumak ve sorunsuz bir şekilde sanal makineler ve uygulamaları tooprivate/ortak veya barındırılan bulut başarısız.

Azure Site Recovery, sanal makine çoğaltma ve StorSimple bulut anlık görüntü yetenekleri kullanarak hello tam dosya sunucusu ortamı koruyabilirsiniz. Kesilme Hello olayda dosyanızı Azure'da yalnızca birkaç dakika içinde çevrimiçi paylaşır. tek tıklatmayla toobring kullanabilirsiniz.

Bu belge, nasıl bir olağanüstü durum kurtarma çözümü StorSimple depolama alanında barındırılan, dosya paylaşımları oluşturabilir ve planlanmış, Planlanmayan gerçekleştirmek ve test yük devretmeleri tek tıklatmayla kurtarma planı kullanarak ayrıntılı olarak açıklanmaktadır. Esas olarak, nasıl hello Kurtarma planlaması, Azure Site Recovery kasası tooenable StorSimple yerine olağanüstü durum senaryoları sırasında değiştirebileceğiniz gösterir. Ayrıca, desteklenen yapılandırmalar ve önkoşulları açıklanmaktadır. Bu belge, Azure Site Recovery ve StorSimple mimarileri hello temelleri ile bildiğinizi varsayar.

## <a name="supported-azure-site-recovery-deployment-options"></a>Desteklenen Azure Site Recovery dağıtım seçenekleri
Müşteriler fiziksel sunucularda veya Hyper-V veya VMware üzerinde çalışan sanal makineler (VM'ler) olarak dosya sunucuları dağıtmak ve StorSimple depolama dışında yontulmuş birimlerden dosya paylaşımları oluşturun. Azure Site Recovery hem fiziksel ve sanal dağıtımları tooeither bir ikincil site veya tooAzure koruyabilirsiniz. Bu belge VM Hyper-V üzerinde barındırılan bir dosya sunucusu için hello kurtarma sitesi olarak Azure ile StorSimple depolama dosya paylaşımlarında DR çözüm ayrıntılarını içerir. Hangi hello dosya sunucusunda VM VMware VM veya fiziksel makinesi üzerinde diğer senaryolar benzer şekilde uygulanabilir.

## <a name="prerequisites"></a>Ön koşullar
StorSimple depolama alanında barındırılan dosya paylaşımları için Azure Site Recovery kullanan bir tek tıklamayla olağanüstü durum kurtarma çözümü uygulamaya hello aşağıdaki önkoşullar vardır:

* Şirket içi Hyper-V veya VMware veya fiziksel bir makine üzerinde VM barındırılan Windows Server 2012 R2 dosya sunucusu
* StorSimple depolama aygıtı şirket içi Azure StorSimple Yöneticisi ile kayıtlı
* (Bu kapatma durumunda tutulabilir) hello Azure StorSimple Yöneticisi'nde oluşturulan StorSimple bulut uygulaması
* Merhaba StorSimple depolama aygıtında yapılandırılmış hello birimlerde barındırılan dosya paylaşımları
* [Azure Site kurtarma Hizmetleri kasası](../site-recovery/site-recovery-vmm-to-vmm.md) Microsoft Azure aboneliği için oluşturulan

Azure kurtarma sitenizi ise, ayrıca, hello çalıştırın [Azure sanal makine hazırlık Değerlendirme Aracı](http://azure.microsoft.com/downloads/vm-readiness-assessment/) Azure Vm'leri ve Azure Site Recovery ile uyumlu olduklarından VM'ler tooensure Hizmetleri.

(yüksek maliyetleri de neden olabilir) tooavoid gecikmesi sorunlarını, StorSimple bulut aygıtınızın, automation hesabı oluşturma ve depolama hesapları aynı bölgede hello emin olun.

## <a name="enable-dr-for-storsimple-file-shares"></a>StorSimple dosya paylaşımları için DR etkinleştir
Her bir bileşeninin hello ortamın korumalı toobe tooenable tam çoğaltma ve kurtarma gerekir şirket içi. Bu bölümde açıklanmıştır nasıl yapılır:

* Active Directory ve DNS çoğaltmayı ayarlama (isteğe bağlı) ayarlayın
* Azure Site Recovery tooenable koruması hello dosya sunucusunun VM kullanın
* StorSimple birimleri korumayı etkinleştir
* Merhaba ağ yapılandırma

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Active Directory ve DNS çoğaltmayı ayarlama (isteğe bağlı) ayarlayın
İsterseniz tooexplicitly ihtiyacınız hello DR sitede kullanılabilir olacak şekilde, Active Directory ve DNS çalışan makineler tooprotect hello korunmak (Merhaba dosya sunucuları kimlik doğrulaması ile yük devretme sonrasında erişilebilir; böylece). Merhaba müşterinin şirket içi ortamına hello kapsamına bağlı iki önerilen seçenek vardır.

#### <a name="option-1"></a>seçenek 1
Hello müşteri az sayıda uygulamayı varsa, tek etki alanı denetleyicisi hello tüm şirket içi site ve Azure Site Recovery çoğaltma tooreplicate hello etki alanı denetleyicisi makine kullanmanızı öneririz sonra hello tüm site başarısız tooa ikincil site (Bu siteden siteye ve site Azure için geçerlidir).

#### <a name="option-2"></a>Seçenek 2
Merhaba müşteri çok sayıda uygulama olduğundan, bir Active Directory ormanı çalıştıran ve birkaç uygulamalar üzerinde aynı anda başarısız durumunda hello DR sitesi ek etki alanı denetleyicisinde ayarlama öneririz (ikincil bir site veya Azure).

Lütfen çok başvurun[Active Directory ve Azure Site Recovery kullanarak DNS için otomatik DR çözüm](../site-recovery/site-recovery-active-directory.md) bir etki alanı denetleyicisi hello DR sitesinde yaparken, yönergeler için. Merhaba belgenin geri kalanında bu için bir etki alanı denetleyicisi hello DR sitesinden edinilebilir varsayacağız.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Azure Site Recovery tooenable koruması hello dosya sunucusunun VM kullanın
Bu adım, hello şirket içi dosya sunucusu ortamınızı hazırlayın, oluşturma ve bir Azure Site Recovery kasası hazırlamak ve hello VM dosya korumayı olduğunu gerektirir.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>tooprepare hello şirket içi dosya sunucusu ortamı
1. Set hello **kullanıcı hesabı denetimi** çok**hiçbir zaman uyarma**. Böylece Azure Site Recovery tarafından devralınırsa başarısız sonra Azure Otomasyon betikleri tooconnect hello iSCSI hedefleri kullanabilirsiniz, bu gereklidir.

   1. Merhaba Windows tuşu + Q tuşlarına basın ve arama **UAC**.
   2. Seçin **değişiklik kullanıcı hesabı denetimi ayarlarını**.
   3. Sürükleme hello toohello alt çubuğu **hiçbir zaman uyarma**.
   4. Tıklatın **Tamam** ve ardından **Evet** istendiğinde.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Merhaba VM Aracısı her hello dosya sunucusu sanal makineleri yükleyin. Böylece Azure Otomasyon betikleri vm'lerinde hello çalıştırabilirsiniz, bu gereklidir.

   1. [Merhaba Aracısı'nı indirme](http://aka.ms/vmagentwin) çok`C:\\Users\\<username>\\Downloads`.
   2. Windows PowerShell Yönetici modunda (yönetici olarak çalıştır) açın ve ardından komut toonavigate toohello indirme konumu aşağıdaki hello girin:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > Merhaba dosya adı hello sürümüne bağlı olarak değişebilir.
      >
      >
3. **İleri**’ye tıklayın.
4. Merhaba kabul **sözleşmesi koşulları** ve ardından **sonraki**.
5. **Son**'a tıklayın.
6. StorSimple depolama dışında yontulmuş birimleri kullanarak dosya paylaşımları oluşturun. Daha fazla bilgi için bkz: [hello StorSimple Yöneticisi hizmet toomanage birimler kullanmak](storsimple-manage-volumes.md).

   1. Şirket içi Vm'leriniz hello Windows tuşu + Q tuşlarına basın ve arama **iSCSI**.
   2. Seçin **iSCSI başlatıcısı**.
   3. Select hello **yapılandırma** sekmesi ve kopyalama hello Başlatıcı adı.
   4. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
   5. Select hello **StorSimple** sekmesini ve ardından seçin hello fiziksel cihaz içeren bir StorSimple Yöneticisi hizmeti hello.
   6. Birim kapsayıcısı/kapsayıcıları ve ardından birim oluşturun. (Bu birimler hello dosya paylaşımlar hello dosya sunucusundaki VM'ler adı verilir). Merhaba Başlatıcı adı kopyalayın ve hello birimleri oluşturduğunuzda hello erişim denetimi kayıtları için uygun bir ad verin.
   7. Select hello **yapılandırma** sekmesi ve hello aygıtın hello IP adresini not.
   8. Şirket içi Vm'leriniz toohello Git **iSCSI başlatıcısı** yeniden ve hello hızlı Connect Bölümü hello IP girin. Tıklatın **Hızlı Bağlan** (Merhaba aygıt şimdi bağlanması).
   9. Açık hello Azure portal ve select hello **birimleri ve aygıtları** sekmesi. Tıklatın **otomatik yapılandır**. Yeni oluşturduğunuz hello birim görüntülenmesi gerekir.
   10. Merhaba Hello Portalı'nda seçin **aygıtları** sekmesini ve ardından **yeni bir sanal cihaz oluşturma.** (Bir yük devretme gerçekleşirse bu sanal aygıt kullanılır). Bu yeni sanal cihaz bir çevrimdışı duruma tooavoid tutulabilir ek maliyetlerden. tootake hello sanal aygıt çevrimdışı, Git toohello **sanal makineleri** bölümünde hello portalı üzerinde ve bilgisayarı kapat.
   11. Toohello şirket içi sanal makineleri geri dönün ve Disk Yönetimi'ni açın (Merhaba Windows tuşu + X tuşlarına basın ve seçin **Disk Yönetimi**).
   12. Bazı ek diskleri (bağlı olarak, oluşturduğunuz birimlerin sayısı hello) fark edeceksiniz. Sağ tıklatın, birinci Merhaba, seçin **diski başlatma**seçip **Tamam**. Sağ hello **Unallocated** bölümünde, select **yeni basit birim**, bir sürücü harfi atamak ve hello Sihirbazı tamamlayın.
   13. L tüm hello diskler için tekrarlayın. Şimdi tüm hello diskleri üzerinde gördüğünüz **bu PC** hello Windows Explorer'ın.
   14. Merhaba dosya ve Depolama Hizmetleri rolü toocreate dosya paylaşımları, bu birimlerdeki kullanın.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate ve bir Azure Site Recovery kasası hazırlama
Toohello başvuran [Azure Site Recovery belgelerine](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget hello dosya sunucusu VM korumadan önce Azure Site Recovery ile başlatıldı.

#### <a name="tooenable-protection"></a>tooenable koruma
1. Merhaba iSCSI bağlantısını hello gelen hedeflere şirket içi Azure Site Recovery aracılığıyla tooprotect istediğiniz sanal makineleri:

   1. Windows tuşu + Q tuşlarına basın ve arama **iSCSI**.
   2. Seçin **iSCSI başlatıcısı ayarlayın**.
   3. Daha önce bağlanmış hello StorSimple cihazı bağlantısını kesin. Alternatif olarak, devre dışı hello dosya sunucusu için bir kaç dakika geçebilirsiniz koruma etkinleştirilirken.

   > [!NOTE]
   > Bu hello dosya paylaşımları toobe geçici olarak devre dışı neden olur.
   >
   >
2. [Sanal makine korumayı etkinleştirin](../site-recovery/site-recovery-hyper-v-site-to-azure.md) hello Azure Site kurtarma portalından hello dosya sunucusunun VM.
3. Merhaba ilk eşitleme başladığında hello hedef yeniden bağlanabilirsiniz. Toohello iSCSI başlatıcısı gidin, hello StorSimple cihazı seçin ve tıklayın **Bağlan**.
4. Ne zaman hello eşitleme tamamlandıktan ve hello VM hello durumudur **korumalı**, hello VM seçin, hello **yapılandırma** sekmesini tıklatın ve hello hello VM ağının güncellemenize (Bu, hello ağ sanal makine üzerinde başarısız oldu, hello bir parçası olur). Merhaba ağ gösterilmesini, hello eşitleme hala işaretleneceğini anlamına gelir.

### <a name="enable-protection-of-storsimple-volumes"></a>StorSimple birimleri korumayı etkinleştir
Merhaba seçmediyseniz **bu birim için varsayılan yedeklemeyi etkinleştir** seçeneği hello StorSimple birimler için çok Git**yedekleme ilkeleri** hello StorSimple Yöneticisi hizmeti ve uygun bir yedekleme oluşturun ilke tüm hello birimler için. Toosee hello uygulama için istediğiniz yedekleme toohello kurtarma noktası hedefi (RPO) hello sıklığını ayarlamanızı öneririz.

### <a name="configure-hello-network"></a>Merhaba ağ yapılandırma
Merhaba VM ağları, yük devretme sonrasında ekli toohello doğru DR ağ; böylece hello dosya sunucusu VM için Azure Site Recovery ağ ayarlarını yapılandırın.

Hello hello VM seçebilirsiniz **öğeleri çoğaltılan** hello aşağıdaki çizimde gösterildiği gibi tooconfigure hello ağ ayarları sekmesinde.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma
ASR tooautomate hello yük devretme işleminde hello dosya paylaşımları, bir kurtarma planı oluşturabilirsiniz. Bir kesinti oluşursa hello dosya paylaşımları yalnızca tek bir tıklatmayla birkaç dakika içinde getirebilir. tooenable bu Otomasyonu, Azure automation hesabı gerekir.

#### <a name="toocreate-an-automation-account"></a>toocreate bir Otomasyon hesabı
1. Toohello Azure portalına gidin &gt; **Otomasyon** bölümü.
2. Tıklatın **+ Ekle** düğmesi, aşağıda dikey penceresi açılır.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Name - yeni bir Otomasyon hesabı girin
   * Abonelik - abonelik seçin
   * Kaynak Grup - yeni seçin/kaynak grubu mevcut oluşturma
   * Konumu - konum seçin, hello tutmak aynı coğrafi/bölge hangi hello StorSimple bulut uygulaması ve depolama hesapları oluşturulmuş.
   * Azure farklı çalıştır hesabı - create Select **Evet** seçeneği.

3. Toohello Otomasyon hesabı gidin, tıklatın **Runbook'lar** &gt; **Gözat galeri** tüm hello tooimport hello Otomasyon dikkate runbook'lar gerekli.
4. Runbook'ları bularak aşağıdaki hello eklemek **olağanüstü durum kurtarma** hello galerisinde etiketi:

   * Test yük devretme (TFO sonra) StorSimple birimlerini temizleme
   * Yük devretme StorSimple birim kapsayıcıları
   * Birimler yük devretme sonrasında StorSimple cihazında bağlama
   * Azure VM'deki özel betik uzantısı kaldırma
   * StorSimple sanal gereç Başlat

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Merhaba automation hesabında hello runbook seçerek tüm hello betikler yayımlamak ve tıklatın **Düzenle** &gt; **Yayımla** ve ardından **Evet** toohello doğrulama İleti. Bu adımdan sonra hello **Runbook'lar** sekmesinde aşağıdaki gibi görünür:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Hello automation hesabında hello seçin **varlıklar** sekmesini &gt; tıklatın **değişkenleri** &gt; **değişken Ekle** ve değişkenleri aşağıdaki hello ekleyin. Bu varlıklar tooencrypt seçebilirsiniz. Bu kurtarma planı – özel değişkenlerdir. Kurtarma (hangi hello sonraki adımda oluşturacağınız) düşünüyorsanız TestPlan adıdır, ardından değişkenlerinizi TestPlan StorSimRegKey, TestPlan AzureSubscriptionName ve benzeri olmalıdır.

   * *RecoveryPlanName***- StorSimRegKey**: Merhaba StorSimple Yöneticisi hizmeti için kayıt anahtarını hello.
   * *RecoveryPlanName***- AzureSubscriptionName**: hello Azure aboneliği hello adı.
   * *RecoveryPlanName***- ResourceName**: hello hello StorSimple cihazı olan StorSimple kaynağın hello adı.
   * *RecoveryPlanName***- DeviceName**: devredilir toobe hello cihaz.
   * *RecoveryPlanName***- VolumeContainers**: birim kapsayıcıları virgülle ayrılmış dizesi volcon1, volcon2, volcon3 toobe başarısız üzerinde; örneğin, gereken hello aygıtta sunmak.
   * *RecoveryPlanName***- TargetDeviceName**: StorSimple bulut üzerinde hangi hello kapsayıcılardır toobe uygulaması başarısız üzerinden hello.
   * *RecoveryPlanName***- TargetDeviceDnsName**: hello hedef aygıt hello hizmet adı (Bu hello bulunabilir **sanal makine** bölüm: Merhaba hizmet adı olduğu hello aynı hello DNS adı).
   * *RecoveryPlanName***- StorageAccountName**: hello depolama hesabı adı hangi hello komut dosyasındaki (hangi toorun hello üzerinde başarısız oldu VM) depolanır. Bu, bazı alanı toostore hello betik geçici olarak sahip herhangi bir depolama hesabı olabilir.
   * *RecoveryPlanName***- StorageAccountKey**: depolama hesabı yukarıda hello hello erişim anahtarı.
   * *RecoveryPlanName***- ScriptContainer**: hello hangi hello betik hello bulutta depolanacağı hello kapsayıcısının adı. Merhaba kapsayıcı yoksa, oluşturulur.
   * *RecoveryPlanName***- VMGUIDS**: VM koruma sonra Azure Site Recovery her VM VM başarısız hello hello ayrıntılarını verir benzersiz bir kimliği atar. tooobtain hello VMGUID, select hello **kurtarma Hizmetleri** sekmesinde **korumalı öğe** &gt; **koruma grupları** &gt; **Makineler** &gt; **özellikleri**. Birden çok VM varsa, hello GUID'ler virgülle ayrılmış bir dize olarak ekleyin.
   * *RecoveryPlanName***- AutomationAccountName** – Merhaba, eklediğiniz hello runbook'ları ve hello varlıklar hello Otomasyon hesabının adı.

  Örneğin, hello hello kurtarma planının adı fileServerpredayRP, ise sonra **kimlik bilgileri** & **değişkenleri** sekmeleri tüm hello varlıklar ekledikten sonra aşağıdaki gibi görünmelidir.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Toohello Git **kurtarma Hizmetleri** bölümü ve daha önce oluşturduğunuz select hello Azure Site Recovery kasası.
8. Select hello **kurtarma planları (Site Recovery)** gelen seçeneği **Yönet** grup ve yeni bir kurtarma planı gibi oluşturun:

   a.  Tıklatın **+ kurtarma planı** düğmesi, aşağıda dikey penceresi açılır.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Kurtarma planı adını girin, kaynak, hedef & dağıtım modeli değerlerini seçin.

   c.  Merhaba kurtarma planında ve'ı tıklatın tooinclude istediğiniz hello koruma grubundan Hello VM'ler seçin **Tamam** düğmesi.

   d.  Daha önce oluşturduğunuz kurtarma planı seçin, **Özelleştir** tooopen hello kurtarma planı özelleştirme Görünümü düğmesine tıklayın.

   e.  Sağ tıklayın **tüm grupları kapatma** tıklatıp **öncesi eylem eklemek**.

   f.  Açılır Ekle eylem dikey penceresinde, bir ad girin, seçin **birincil tarafı** burada toorun seçeneği (hangi eklediğiniz hello runbook'ları) Otomasyon hesabı seçin ve ardından hello seçin seçeneği  **Yük devretme StorSimple birim kapsayıcıları** runbook.

   g.  Sağ tıklayın **Grup 1: Başlangıç** tıklatıp **Ekle korunan öğeler** seçeneğini ardından hello kurtarma planında ve'ı tıklatın korunan toobe olan hello VM'ler seçin **Tamam** düğmesi. Zaten ise isteğe bağlı, VM'ler seçili.

   h.  Sağ tıklayın **Grup 1: Başlangıç** tıklatıp **sonrası eylemi** seçeneği ardından tüm hello komut dosyaları ekleyin:

   * Start-StorSimple-sanal-gereç runbook
   * StorSimple birim kapsayıcıları üzerinden runbook başarısız
   * Yük sonra bağlama birimleri runbook
   * Kaldırma-özel-betik-uzantısı runbook

   ı.  4 yukarıda Hello hello aynı komutlar sonra el ile bir eylem eklemek **Grup 1: sonrası adımları** bölümü. Bu eylem, her şeyi düzgün çalıştığını doğrulayabilirsiniz başlangıç noktasıdır. Bu eylem yalnızca yük devretme testi bir parçası olarak eklenen toobe gerekir (Bu nedenle yalnızca select hello **yük devretme testi** onay kutusunu).

   j.  Merhaba el ile eylemden sonra hello eklemek **Temizleme** kullanarak komut dosyası hello hello için kullandığınız yordamın aynısını diğer runbook'ları. **Kaydet** hello kurtarma planı.

    > [!NOTE]
    > Hello temizleme bir parçası olarak hello hedef cihazda klonlanmış hello StorSimple birimlerini Hello el ile işlem tamamlandığında silinecek çünkü bir yük devretme testi çalıştırırken, her şeye hello işlemi el ile adım doğrulamanız gerekir.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Bir sınama yük devretmesi gerçekleştirme
Toohello başvuran [Active Directory DR çözüm](../site-recovery/site-recovery-active-directory.md) yardımcı kılavuz hello yük devretme testi sırasında konuları belirli tooActive dizin için. Merhaba şirket içi Kurulum Hello test yük devretme durumunda tüm dağıtılmış bir dosya değil. bağlı StorSimple birimlerini hello toohello şirket içi VM olan kopyalanan toohello azure'da StorSimple bulut uygulaması. Azure'da VM test amaçları için hazırlanmıştır ve hello kopyalanan birimlerin olduğundan ekli toohello VM.

#### <a name="tooperform-hello-test-failover"></a>Yük devretme tooperform hello testi
1. Hello Azure portal'da, site recovery kasası seçin.
2. Merhaba dosya sunucusu VM için oluşturulan hello kurtarma planı'ı tıklatın.
3. Tıklatın **yük devretme testi**.
4. Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlanması hello Azure sanal ağı toowhich seçin.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **Test yük devretme işini** kasa adı &gt; **işleri** &gt; **Site Recovery işleri**.
6. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine hello Azure portalında görünür &gt; **sanal makineleri**. Doğrulama gerçekleştirebilirsiniz.
7. Merhaba doğrulamaları tamamladıktan sonra tıklatın **doğrulamaları tam**. Bu işlem temizleme hello StorSimple birimlerini ve kapatma hello StorSimple bulut uygulaması.
8. İşiniz bittiğinde tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde. Yük devretme notları kaydındaki ve hello ile ilişkili gözlemlerinizi kaydetmek sınayın. Bu yük devretme testi sırasında oluşturulan hello sanal makine siler.

## <a name="perform-a-planned-failover"></a>Planlanmış bir yük devretme gerçekleştirin
   Planlanmış bir yük devretme sırasında hello şirket içi dosya sunucusu VM düzgün biçimde kapatılamadı ve Bulutu StorSimple cihazı hello birimlerin yedekleme anlık görüntüsü alınır. Merhaba StorSimple birimlerini toohello sanal cihaz, Azure üzerinde VM getirilene bir çoğaltma devredildi ve ekli toohello VM hello birimlerdir.

#### <a name="tooperform-a-planned-failover"></a>tooperform planlanmış bir yük devretme
1. Hello Azure portal, seçin **kurtarma Hizmetleri** kasa &gt; **kurtarma planlarına (Site recovery)** &gt; **recoveryplan_name** için oluşturulan Merhaba dosya sunucusu VM.
2. Merhaba kurtarma planı dikey penceresinde **daha fazla** &gt; **planlanan yük devretme**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Merhaba üzerinde **planlı yük devretme onaylayın** dikey penceresinde hello kaynak ve hedef konumları ve select hedef ağ seçin ve hello onay simgesi ✓ toostart hello yük devretme işlemi'ı tıklatın.
4. Çoğaltma sanal makineleri oluşturulduktan sonra yürütme bekleme durumuna demektir. Tıklatın **yürütme** toocommit hello yük devretme.
5. Çoğaltma tamamlandıktan sonra hello sanal makineleri hello ikincil konumda Başlat.

## <a name="perform-a-failover"></a>Bir yük devretme gerçekleştirin.
Planlanmamış bir yük devretme sırasında ekli toohello VM hello birimlerdir ve toohello sanal cihaz, Azure üzerinde getirilebilmesi VM bir çoğaltma üzerinde hello StorSimple birimlerini başarısız oldu.

#### <a name="tooperform-a-failover"></a>tooperform bir yük devretme
1. Hello Azure portal, seçin **kurtarma Hizmetleri** kasa &gt; **kurtarma planlarına (Site recovery)** &gt; **recoveryplan_name** için oluşturulan Merhaba dosya sunucusu VM.
2. Merhaba kurtarma planı dikey penceresinde **daha fazla** &gt; **yük devretme**.  
3. Merhaba üzerinde **onaylayın yük devretme** dikey penceresinde hello kaynağını seçin ve hedef konumları.
4. Seçin **sanal makineleri kapatın ve hello en son verileri eşitleyin** Site Recovery korumalı hello sanal makine aşağı tooshut deneyin ve hello hello veri en son sürümünü olacak şekilde hello veri eşitleyin toospecify üzerinde başarısız oldu.
5. Merhaba yük devretme işleminden sonra yürütme bekleme durumuna hello sanal makine yok. Tıklatın **yürütme** toocommit hello yük devretme.


## <a name="perform-a-failback"></a>Bir yeniden çalışma gerçekleştirme
Bir yedeklemenin sonra bir yeniden çalışma sırasında geri toohello fiziksel aygıt üzerinden StorSimple birim kapsayıcıları başarısız olan.

#### <a name="tooperform-a-failback"></a>tooperform bir yeniden çalışma
1. Hello Azure portal, seçin **kurtarma Hizmetleri** kasa &gt; **kurtarma planlarına (Site Recovery)** &gt; **recoveryplan_name** için oluşturulan Merhaba dosya sunucusu VM.
2. Merhaba kurtarma planı dikey penceresinde **daha fazla** &gt; **planlı yük devretme**.  
3. Merhaba kaynak ve hedef konumların, select hello ilgili veri eşitleme ve VM oluşturma seçenekleri seçin.
4. Tıklatın **Tamam** düğmesini toostart hello yeniden çalışma işlemi.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>En İyi Uygulamalar
### <a name="capacity-planning-and-readiness-assessment"></a>Kapasite planlama ve hazırlık değerlendirme
#### <a name="hyper-v-site"></a>Hyper-V sitesi
Kullanım hello [kullanıcı kapasite planlayıcısı aracı](http://www.microsoft.com/download/details.aspx?id=39057) toodesign hello sunucu, depolama ve Hyper-V çoğaltma ortamınız için ağ altyapısı.

#### <a name="azure"></a>Azure
Merhaba çalıştırabilirsiniz [Azure sanal makine hazırlık Değerlendirme Aracı](http://azure.microsoft.com/downloads/vm-readiness-assessment/) Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu olduklarından VM'ler tooensure üzerinde. Merhaba hazırlık Değerlendirme Aracı VM yapılandırmaları denetler ve yapılandırmaları Azure ile uyumsuz olduğunda sizi uyarır. Örneğin, C: sürücüsündeki 127 GB'den büyükse bir uyarı verir.

Kapasite planlama en az iki önemli işlemden oluşur:

* Eşleme Hyper-V sanal makineleri tooAzure VM boyutları (örneğin, A6, A7, A8 ve A9) şirket içi.
* Merhaba belirleme Internet bant genişliği gerekli.

## <a name="limitations"></a>Sınırlamalar
* Şu anda yalnızca 1 StorSimple cihazı yük Devredilebilen (tooa tek StorSimple bulut uygulaması). Merhaba senaryo birkaç StorSimple cihaz yayılan bir dosya sunucusu henüz desteklenmiyor.
* Bir sanal makine için koruma etkinleştirilirken bir hata alırsanız, hello iSCSI hedefleri kesmiş emin olun.
* Birim kapsayıcıları yayılan yedekleme ilkeleri nedeniyle birlikte gruplandırılmış tüm hello birim kapsayıcıları üzerinden birlikte devredilir.
* Merhaba birim kapsayıcıları seçmiş olduğunuz tüm hello birimlerinde üzerinden başarısız.
* Tek bir StorSimple bulut uygulaması Hello en fazla kapasitesi 64 TB olduğundan 64 TB yük devretmenin olamaz daha toomore eklemek birimler.
* Merhaba planlanan/planlanmamış yük devretme başarısız olursa ve hello sanal makineleri Azure üzerinde oluşturulan değil temizleme sonra VM'ler hello. Bunun yerine, bir yeniden çalışma yapın. Merhaba VM'ler silerseniz ardından hello VM'ler yeniden açılamaz şirket içi.
* Bir yük devretme sonrasında mümkün değilse toosee hello birimler, toohello VM'ler gidin, Disk Yönetimi'ni açın, hello diskleri yeniden tarayın ve ardından bunları çevrimiçi duruma getirmeden.
* Bazı durumlarda, hello sürücü harflerini hello DR sitedeki hello harf şirket içi farklı olabilir. Bu gerçekleşirse, hello yük devretme tamamlandıktan sonra toomanually doğru hello sorun gerekir.
* Çok faktörlü kimlik doğrulaması hello hello Otomasyon hesabındaki bir varlık olarak girilen Azure kimlik bilgisi devre dışı bırakılmalıdır. Bu kimlik doğrulaması devre dışı değil, komut dosyaları toorun otomatik olarak izin verilmez ve hello kurtarma planı başarısız olur.
* Yük devretme iş zaman aşımı: Merhaba StorSimple komut dosyası zaman aşımına birim kapsayıcıları hello yük devretme betiği (şu anda 120 dakika) başına hello Azure Site Recovery sınırdan daha uzun sürerse olur.
* Yedekleme işi zaman aşımı: Merhaba StorSimple komut dosyası zaman aşımına birimlerini hello yedekleme betiği (şu anda 120 dakika) başına hello Azure Site Recovery sınırdan daha uzun sürerse.

  > [!IMPORTANT]
  > Merhaba yedekleme hello Azure portal ' el ile çalıştırın ve hello kurtarma planı yeniden çalıştırın.

* İş zaman aşımı kopyalama: Merhaba StorSimple komut dosyası zaman aşımına hello birimlerin kopyalama komut dosyası (şu anda 120 dakika) başına hello Azure Site Recovery sınırdan daha uzun sürerse.
* Zaman eşitleme hatası: Merhaba StorSimple komutlar hello yedekleme hello Portalı'nda başarılı olsa bile hello yedeklemeler başarısız belirten çıkışı hataları. Olası bir nedeni, bu hello StorSimple Gereci 's zaman hello saat dilimindeki geçerli saati hello ile eşitlenmiş olabilir olabilir.

  > [!IMPORTANT]
  > Eşitleme hello Gereci süresiyle hello hello saat dilimindeki geçerli saati.

* Gereci yük devretme hatası: Merhaba StorSimple komut dosyası varsa bir gereç yük devretme hello kurtarma planı çalışırken başarısız olabilir.

  > [!IMPORTANT]
  > Merhaba Gereci yük devretme işlemi tamamlandıktan sonra hello kurtarma planı yeniden çalıştırın.


## <a name="summary"></a>Özet
Azure Site Recovery kullanarak, bir dosya sunucusu VM için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz StorSimple depolama alanında barındırılan dosya paylaşımları sahip. Her yerden saniye içinde hello yük devretme başlatabilirsiniz hello kesilme olayı ve birkaç dakika içinde çalışır hello uygulama alın.
