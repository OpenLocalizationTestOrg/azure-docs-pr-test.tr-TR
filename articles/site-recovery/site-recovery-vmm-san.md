---
title: Azure Site Recovery kullanarak Hyper-V Vm'lerini SAN ile vmm'de aaaReplicate | Microsoft Docs
description: "Bu makalede nasıl tooreplicate Hyper-V sanal makineleri iki site arasında SAN çoğaltması kullanılarak Azure Site Recovery ile."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>SAN kullanarak VMM Bulutları tooa Azure Site Recovery ile ikincil sitedeki Hyper-V Vm'lerini çoğaltma


Toodeploy istiyorsanız, bu makaleyi kullanın [Azure Site Recovery](site-recovery-overview.md) toomanage çoğaltma hello Klasik portalda Azure Site Recovery kullanarak Hyper-V sanal makineleri (System Center Virtual Machine Manager bulutlarında yönetilen) tooa ikincil VMM sitesi. Bu senaryo hello yeni Azure portalında kullanılamaz.



Bu makalenin hello sonunda yorumları gönderin. Hello tootechnical soruları cevaplar [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Neden SAN ve Site Recovery ile çoğaltabilir?

* SAN kuruluş düzeyi, ölçeklenebilir çoğaltma çözümünü sunar, böylece Hyper-V SAN ile içeren bir birincil site LUN tooa ikincil site SAN çoğaltabilirsiniz. Depolama VMM tarafından yönetildiğinden ve çoğaltma ve yük devretme Site Recovery ile düzenlenir.
* Site Kurtarma ile birkaç çalışılan [SAN depolama ortakları](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide çoğaltma Fiber Kanal ve iSCSI depolama arasında.  
* Hyper-V kümelerinde dağıtılan mevcut SAN altyapı tooprotect kritik uygulamalarınızı kullanın. N katmanlı uygulamalar yerine tutarlı bir şekilde çalışılabilir böylece sanal makineleri bir grup olarak çoğaltılabilir.
* SAN çoğaltması eşitlenmiş çoğaltma düşük RTO ve RPO için olan bir uygulama farklı katmanlar arasında çoğaltma tutarlılığı sağlar ve (bağlı olarak, depolama dizisi yeteneklerini) yüksek esneklik için çoğaltma zaman.  
* SAN depolama alanına hello VMM doku yönetebilir ve VMM toodiscover var olan depolama SMI-S kullanın.  

Şunlara dikkat edin:
- Siteden siteye çoğaltma SAN ile hello Azure portalında kullanılamaz. Merhaba Klasik portalda yalnızca kullanılabilir. Yeni kasa hello Klasik Portalı'nda oluşturulamıyor. Varolan kasalarını korunabilir.
- SAN tooAzure Çoğaltmada desteklenmiyor.
- Paylaşılan Vhdx'ler çoğaltılamıyor veya tooVMs iSCSI veya Fiber kanal üzerinden doğrudan mantıksal birimler (LUN'ler) bağlı. Konuk kümeleri çoğaltılabilir.


## <a name="architecture"></a>Mimari

![SAN mimarisi](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: hello Azure portalında Site Recovery kasasına ayarlayın.
- **SAN depolama alanı**: SAN depolama alanı hello VMM doku yönetilir. Merhaba depolama sağlayıcısını ekleyin, depolama sınıflandırması oluşturun ve depolama havuzları ayarlayın.
- **VMM ve Hyper-V**: her sitedeki VMM sunucusu öneririz. VMM özel bulut kurmak ve bu bulutlara Hyper-V kümeleri yerleştirin. Dağıtım sırasında hello Azure Site Recovery sağlayıcısı her VMM sunucusunda yüklü ve hello sunucu hello kasasında kayıtlı. Merhaba sağlayıcısı hello Site Recovery hizmeti toomanage çoğaltma, yük devretme ve yeniden çalışma ile iletişim kurar.
- **Çoğaltma**: depolama vmm'de ayarlama ve Site Recovery çoğaltma yapılandırdıktan sonra hello birincil ve ikincil SAN depolama alanı arasında çoğaltma gerçekleşir. Çoğaltma veri tooSite kurtarma gönderilmez.
- **Yük devretme**: yük devretme hello Site Recovery portalında etkinleştirin. Yoktur sıfır veri kaybı yük devretme sırasında çoğaltma zaman uyumlu olduğundan.
- **Yeniden çalışma**: toofail geri ters çoğaltma tootransfer delta değişiklikleri hello ikincil site toohello birincil sitesinden etkinleştir. Çoğaltmayı tersine çevirme işlemi tamamlandıktan sonra ikincil tooprimary planlanmış bir yük devretme çalıştırın. Bu planlanmış bir yük devretme hello çoğalma VM'ler hello ikincil sitede durdurur ve hello birincil sitede başlatır.


## <a name="before-you-start"></a>Başlamadan önce


**Önkoşullar** | **Ayrıntılar**
--- | ---
**Azure** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/). Bir Azure Site Recovery kasası tooconfigure oluşturun ve çoğaltma ve yük devretme yönetin.
**VMM** | Tek bir VMM sunucusu kullanın ve farklı Bulutlar arasında çoğaltılır, ancak bir VMM hello birincil sitedeki ve hello ikincil site birinde öneririz. VMM, bir fiziksel veya sanal bağımsız sunucu veya bir küme olarak dağıtılabilir. <br/><br/>Merhaba VMM sunucusu, System Center 2012 R2 çalıştırıyor olması veya üzeri hello en son toplu güncelleştirmelerine sahip.<br/><br/> Yapılandırılmış en az bir bulut gereksinim yük devretme için toouse istediğiniz tooprotect ve hello ikincil VMM sunucusunda yapılandırılan bir bulut istediğiniz hello birincil VMM sunucusunda.<br/><br/> Merhaba kaynak bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.<br/><br/> Tüm VMM Bulutları hello Hyper-V Kapasite profili kümesine sahip olması gerekir.<br/><br/> VMM bulutlarını ayarlama hakkında daha fazla bilgi için bkz: [bir VM Bulutu dağıtmak](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Bir veya daha fazla Hyper-V kümeleri birincil ve ikincil VMM bulutlarında gerekir.<br/><br/> Merhaba kaynak Hyper-V kümesindeki bir veya daha fazla VM içermesi gerekir.<br/><br/> Merhaba VMM konak grupları hello birincil ve ikincil sitelerdeki hello Hyper-V kümeleri en az birini içermelidir.<br/><br/>Merhaba Hyper-V rolü ve hello en son güncelleştirmeleri içeren sonraki yüklü veya Hello ana bilgisayarı ve hedef Hyper-V sunucuları Windows Server 2012 çalıştırıyor olması gerekir.<br/><br/> Bir kümede Hyper-V çalıştırıyorsanız ve bir statik IP adresi tabanlı küme varsa, küme aracısının otomatik olarak oluşturulmaz. Bunu el ile yapılandırmanız gerekir. Daha fazla bilgi için bkz: [Hyper-V çoğaltma için konak kümeleri hazırlama](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**SAN depolama alanı** | Konuk kümelenmiş sanal makineler iSCSI veya kanal depolama veya paylaşılan sanal sabit diskler (vhdx) kullanarak çoğaltabilirsiniz.<br/><br/> İki SAN Dizileri gerekir: biri hello birincil site ve bir giriş hello ikincil site.<br/><br/> Bir ağ altyapısı hello dizilerine ayarlanması. Eşleme ve çoğaltma yapılandırılması gerekir. Çoğaltma lisansları hello depolama dizisi gereksinimlerine uyacak şekilde ayarlanmış olması.<br/><br/>Konak iSCSI veya Fiber Kanal kullanarak depolama LUN'ları ile iletişim kurabilmesi için hello depolama dizisi ve hello Hyper-V ana bilgisayar sunucuları arasında ağ yukarı ayarlayın.<br/><br/> Denetleme [desteklenen depolama dizileri](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Depolama dizisi üreticileri SMI-S sağlayıcılarını yüklenmelidir ve hello SAN Dizileri hello sağlayıcı tarafından yönetilmelidir. Merhaba sağlayıcısı according toomanufacturer talimatlarını ayarlar.<br/><br/>Bu hello dizinin SMI-S sağlayıcı bir sunucuda bu hello VMM olduğundan emin olun sunucu IP adresi veya FQDN ile Merhaba ağ üzerinden erişebilirsiniz.<br/><br/> Her SAN dizisi, bir veya daha fazla kullanılabilir depolama havuzu olmalıdır.<br/><br/> Merhaba birincil VMM sunucusunun hello birincil dizi yönetmeniz gerekir ve hello ikincil VMM sunucusu hello ikincil dizi yönetmeniz gerekir.
**Ağ eşlemesi** | Böylece yük devretme sonrasında çoğaltılmış sanal makinelere en iyi şekilde ikincil Hyper-V ana bilgisayar sunucuları üzerinde yerleştirilir ve böylece bağlı tooappropriate VM ağları oldukları ağ eşlemesi ayarlayın. Ağ eşlemesini yapılandırmazsanız, çoğaltma sanal makineleri yük devretme sonrasında bağlı tooany ağ olmayacaktır.<br/><br/> Site Recovery dağıtımı sırasında ağ eşlemesini ayarlayabilirsiniz böylece VMM ağlarına doğru şekilde yapılandırıldığından emin olun. VMM, bağlı tooa VMM VM ağ hello VM'ler hello kaynak Hyper-V ana bilgisayarda olmalıdır. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.<br/><br/> Hello hedef bulut karşılık gelen VM ağı olmalıdır ve sırayla hello hedef Bulutu ile ilişkili olan bağlantılı tooa karşılık gelen mantıksal ağ olmalıdır.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>1. adım: hello VMM altyapıyı hazırlama
tooprepare VMM altyapınızı, gerekir:

1. VMM Bulutları doğrulayın.
2. Tümleştirme ve vmm'de SAN depolama Sınıflandır.
3. LUN oluşturun ve depolama alanı ayır.
4. Çoğaltma grupları oluşturun.
5. VM ağları ayarlayın.

### <a name="verify-vmm-clouds"></a>VMM Bulutları doğrulayın

Site Recovery dağıtımı başlamadan önce VMM Bulutları düzgün ayarlandığından emin olun.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Tümleştirme ve hello VMM doku SAN depolama Sınıflandır

1. Merhaba VMM konsolunda çok Git**doku** > **depolama** > **kaynak Ekle** > **depolama aygıtları**.
2. Merhaba, **depolama aygıtları ekleme** seçin **depolama sağlayıcısının türünü seçin** seçip **bulunan ve bir SMI-S sağlayıcısı tarafından yönetilen SAN ve NAS cihazları**.

    ![Sağlayıcı türü](./media/site-recovery-vmm-san/provider-type.png)

3. Merhaba üzerinde **belirtin protokolünü ve adresini hello depolama SMI-S sağlayıcısı** sayfasında, **SMI-S CIMXML** ve bağlantı toohello sağlayıcısının hello ayarlarını belirtin.
4. İçinde **sağlayıcı IP adresi veya FQDN** ve **TCP/IP bağlantı noktası**, bağlanan toohello sağlayıcısının hello ayarlarını belirtin. SMI-S CIMXML için yalnızca bir SSL bağlantısı kullanabilirsiniz.

    ![Sağlayıcı Bağlan](./media/site-recovery-vmm-san/connect-settings.png)
5. İçinde **farklı çalıştır hesabı**, erişen hello sağlayıcısı veya bir hesap oluşturun bir VMM farklı çalıştır hesabı belirtin.
6. Merhaba üzerinde **bilgi toplayın** sayfasında, VMM toodiscover ve içeri aktarma hello depolama cihazı bilgilerini otomatik olarak çalışır. tooretry bulma tıklatın **tarama sağlayıcısı**. Merhaba bulma işlemi başarılı olursa, depolama dizileri, depolama havuzları, üreticisini, model ve kapasite hello sayfasında listelenen hello buldu.

    ![Depolama Bul](./media/site-recovery-vmm-san/discover.png)
7. İçinde **depolama havuzları tooplace Yönetimi altında seçin ve bir sınıflandırma atamak**, VMM yönetmek ve bunları bir sınıflandırma atamak hello depolama havuzlarını seçin. LUN bilgileri hello depolama havuzlarından içeri aktarılır. Temel LUN'ları oluşturmak hello uygulamaları, tooprotect, kapasite gereksinimlerine ve gereksinimlerinizi tooreplicate birlikte ihtiyaç duyduğu için gerekir.

    ![Depolama Sınıflandır](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>LUN'ları oluşturma ve depolama alanı Ayır

Temel LUN'ları oluşturmak hello uygulamaları, tooprotect, kapasite gereksinimlerini ve gereksinimlerinizi tooreplicate birlikte ihtiyaç duyduğu için gerekir.

1. Merhaba depolama hello VMM doku göründükten sonra şunları yapabilirsiniz [LUN sağlamak](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > VHD'ler hello için çoğaltma tooLUNs etkin VM için eklemeyin. Bu LUN'ları bir Site Recovery çoğaltma grubunda değilse, Site Recovery tarafından algılanmaz.
     >

2. Depolama kapasitesi toohello Hyper-V konak kümesi, VMM sanal makine veri sağlanan toohello depolama dağıtabileceğiniz atayın:

   * Depolama toohello küme ayırma önce tooallocate gerekir, küme üzerinde hangi hello bulunduğu toohello VMM konak grubu. Daha fazla bilgi için bkz: [nasıl tooallocate depolama mantıksal birimleri tooa konak grubunun vmm'de](https://technet.microsoft.com/library/gg610686.aspx) ve [nasıl VMM konak grubunda tooa tooallocate depolama havuzları](https://technet.microsoft.com/library/gg610635.aspx).
   * Depolama kapasitesi toohello küme açıklandığı gibi tahsis [nasıl tooconfigure depolama bir Hyper-V ana bilgisayar üzerindeki küme VMM'de](https://technet.microsoft.com/library/gg610692.aspx).

    ![Sağlayıcı türü](./media/site-recovery-vmm-san/provider-type.png)
3. İçinde **belirtin protokolünü ve adresini hello depolama SMI-S sağlayıcısı**seçin **SMI-S CIMXML**. Toohello sağlayıcısı bağlanmak için Hello ayarlarını belirtin. Bir SSL bağlantısı yalnızca SMI-S CIMXML için kullanabilirsiniz.

    ![Sağlayıcı Bağlan](./media/site-recovery-vmm-san/connect-settings.png)
4. İçinde **farklı çalıştır hesabı**, erişen hello sağlayıcısı veya bir hesap oluşturun bir VMM farklı çalıştır hesabı belirtin.
5. İçinde **toplamanız bilgiler**, VMM toodiscover ve içeri aktarma hello depolama cihazı bilgilerini otomatik olarak çalışır. Tooretry gerekiyorsa, tıklatın **tarama sağlayıcısı**. Merhaba depolama dizileri, Hello bulma işlemi başarılı olduğunda depolama havuzları, üreticisini, model ve kapasite hello sayfasında listelenir.

    ![Depolama Bul](./media/site-recovery-vmm-san/discover.png)
7. İçinde **depolama havuzları tooplace Yönetimi altında seçin ve bir sınıflandırma atamak**, VMM yönetmek ve bir sınıflandırma atamak, hello depolama havuzlarını seçin. LUN bilgileri hello depolama havuzlarından içeri aktarılır.

    ![Depolama Sınıflandır](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Çoğaltma grupları oluşturma

Tooreplicate birlikte gerekir tüm hello LUN'lar içeren bir çoğaltma grubu oluşturun.

1. Merhaba Hello VMM konsolunda Aç **çoğaltma grupları** hello depolama dizisi özellikleri ve ardından sekmesinde **yeni**.
2. Merhaba çoğaltma grubu oluşturun.

    ![SAN çoğaltma grubu](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Ağları ayarlayın

Tooconfigure ağ eşlemesi istiyorsanız, aşağıdaki hello:

1. Site Recovery ağ eşlemesi bakın.
2. VMM'de VM ağlarına için hazırlık yapın:

   * [Mantıksal ağlar ayarlayın](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [VM ağları ayarlayın](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>2. adım: bir kasa oluşturma

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello VMM sunucusundan hello kasadaki tooregister istiyor.
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri**ve ardından **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler Bkz [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
6. **Kasa Oluştur**'a tıklayın.

    ![Yeni Kasa](./media/site-recovery-vmm-san/create-vault.png)

Kasa hello onay hello durum çubuğu tooconfirm başarıyla oluşturuldu. Merhaba kasası listelenir **etkin** hello ana üzerinde **kurtarma Hizmetleri** sayfası.

### <a name="register-hello-vmm-servers"></a>Merhaba VMM sunucularını kaydetme

1. Açık hello **Hızlı Başlangıç** hello sayfasından **kurtarma Hizmetleri** sayfası. Hızlı Başlangıç, herhangi bir zamanda hello simgesini seçerek de açılabilir.

    ![Hızlı Başlangıç Simgesi](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Merhaba açılan kutusunda **arasında Hyper-V şirket içi dizi çoğaltma kullanarak site**.

    ![Kayıt anahtarı](./media/site-recovery-vmm-san/select-san.png)
3. İçinde **VMM sunucularını hazırla**, hello hello Azure Site Recovery sağlayıcısı yükleme dosyasının en son sürümünü indirin.
4. Bu dosya hello kaynak VMM sunucusunda çalıştırın. VMM bir kümede dağıtılmışsa ve sağlayıcı Merhaba hello ilk kez yüklüyorsanız, hello sağlayıcısı etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın. Daha sonra hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin. Merhaba sağlayıcısı yükseltiyorsanız, aynı sağlayıcı sürümlerinin yüklü hello böylece tüm düğümlerde tooupgrade gerekir.
5. Merhaba yükleyici gereksinimleri ve istekleri izni toostop hello VMM hizmeti toobegin Sağlayıcısı Kurulumu denetler. Kurulum bittiğinde hello hizmeti otomatik olarak yeniden başlatılır. Bir VMM kümesinde sorarak toostop hello küme rolünü olması.
6. İçinde **Microsoft Update**güncelleştirmeleri de seçebilirsiniz ve sağlayıcı güncelleştirmeleri tooyour Microsoft Update ilkenize göre yüklenir.

    ![Microsoft Güncelleştirmeleri](./media/site-recovery-vmm-san/ms-update.png)

7. Varsayılan olarak, hello yükleme hello sağlayıcısı konumudur <SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin. Tıklatın **yükleme** toobegin.

    ![Yükleme konumu](./media/site-recovery-vmm-san/install-location.png)

8. Merhaba sağlayıcı yüklendikten sonra tıklatın **kaydetmek** hello kasadaki tooregister hello VMM sunucusu.

    ![Yükleme tamamlandı](./media/site-recovery-vmm-san/install-complete.png)

9. İçinde **Internet bağlantısı**, hello sağlayıcısı toohello Internet nasıl bağlandığını belirtin. Seçin **varsayılan sistem Ara sunucu ayarlarını kullan** hello sunucusundaki toouse hello varsayılan Internet bağlantısı ayarları istiyorsanız.

    ![İnternet Ayarları](./media/site-recovery-vmm-san/proxy-details.png)

   * Toouse özel bir ara sunucu istiyorsanız hello sağlayıcı yüklemeden önce bunu ayarlayın. Özel ara sunucu ayarlarını yapılandırdığınızda, bir test toocheck hello proxy bağlantısı'nı çalıştırır.
   * Özel bir ara sunucu kullanırsanız veya varsayılan ara sunucunuz kimlik doğrulaması gerektiriyorsa, hello adresi ve bağlantı noktası gibi hello proxy ayrıntıları girmeniz gerekir.
   * Merhaba URL'leri hello VMM sunucusundan erişilebilir olmalıdır gereklidir.
   * Özel bir ara sunucu kullanırsanız, bir VMM farklı çalıştır hesabı (DRAProxyAccount) otomatik olarak belirtilen hello kullanılarak oluşturulan proxy kimlik bilgileri. Bu hesap doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba farklı çalıştır hesabı ayarlarını hello VMM konsolundaki değiştirebilirsiniz (**ayarları** > **güvenlik** > **farklı çalıştır hesapları**  >  **DRAProxyAccount**). Merhaba değişikliğin tootake hello VMM hizmetini yeniden başlatmanız gerekir.
10. İçinde **kayıt anahtarı**seçin hello portal ve kopyalanan toohello VMM sunucusundan indirilen hello anahtarı.
11. İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın.

    ![Sunucu kaydı](./media/site-recovery-vmm-san/vault-creds.png)
12. Merhaba şifreleme ayarı yalnızca VMM tooAzure çoğaltma için kullanılır. Onu yok sayabilirsiniz.

    ![Sunucu kaydı](./media/site-recovery-vmm-san/encrypt.png)
13. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
14. İçinde **ilk bulut meta verileri eşitleme**hello VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istediğinizi seçin. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu ayrı ayrı hello hello VMM konsolundaki bulut özellikleri eşitleyin.

    ![Sunucu kaydı](./media/site-recovery-vmm-san/friendly-name.png)

15. Tıklatın **sonraki** toocomplete hello işlemi. Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu görüntülenir **sunucuları** > **VMM sunucuları** hello kasasında.

### <a name="command-line-installation"></a>Komut satırı yüklemesi

Hello Azure Site Recovery sağlayıcısı komut satırından aşağıdaki hello kullanarak da yüklenebilir. Bu yöntem, sunucu çekirdek Windows Server 2012 R2 için kullanılan tooinstall hello sağlayıcısında olabilir.

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örneğin, C:\ASR.
2. Merhaba VMM hizmetini durdurun.
3. Merhaba sağlayıcı yükleyicisini ayıklayın. Bu komutlar bir yönetici olarak çalıştırın:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Merhaba sağlayıcısı yükleyin:

        C:\ASR> setupdr.exe /i
5. Merhaba sağlayıcısını Kaydet:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parametreler:

* **/ Credentials**: gerekli parametre için hangi hello kayıt anahtarı dosyasının bulunduğu başlangıç konumu.  
* **/ FriendlyName**: hello adı hello Azure Site Recovery portalında görünen hello Hyper-V konak sunucusu için gerekli parametre.
* **/ EncryptionEnabled**: yalnızca VMM tooAzure çoğaltırken kullanılan isteğe bağlı parametre.
* **/ proxyaddress**: hello proxy sunucusunun hello adresini belirten isteğe bağlı parametre.
* **/ proxyport**: hello proxy sunucusunun hello bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername**: (Merhaba proxy kimlik doğrulaması gerektiriyorsa) hello Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword**: (Merhaba proxy kimlik doğrulaması gerektiriyorsa) hello proxy sunucusu ile kimlik doğrulaması için hello parolayı belirten isteğe bağlı parametre.

## <a name="step-3-map-storage-arrays-and-pools"></a>3. adım: depolama dizileri ve havuzları eşleme

Birincil ve ikincil diziler toospecify hangi ikincil depolama havuzu hello birincil havuzundan çoğaltma verileri alan eşleyin. Çoğaltma, yapılandırmadan önce çoğaltma gruplarında korumayı etkinleştirdiğinizde hello eşleme bilgilerini kullanıldığından depolama eşleyin.

Başlamadan önce VMM Bulutları hello kasasına olup olmadığını denetleyin. Bulut sağlayıcısı yükleme sırasında tüm Bulutları eşitlemek olduğunda veya hello VMM konsolundaki belirli bir bulut eşitlediğinizde algılanır.

1. Tıklatın **kaynakları** > **sunucu depolama** > **harita kaynak ve hedef dizilerinin**.
    ![Sunucu kaydı](./media/site-recovery-vmm-san/storage-map.png)

2. Merhaba depolama dizileri hello birincil sitede seçin ve bunları toostorage diziler hello ikincil sitede eşleyin. İçinde **depolama havuzları**, bir kaynak seçin ve depolama havuzu toomap hedefleyin.

    ![Sunucu kaydı](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>4. adım: çoğaltma ayarlarını yapılandırın

VMM sunucusu kayıtlı sonra bulut koruma ayarlarını yapılandırın.

1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **VMM Bulutları için koruma ayarlama**.
2. Merhaba üzerinde **korunan öğeler** sekmesinde, seçin hello bulut **yapılandırma**.
3. İçinde **hedef**seçin **VMM**.
4. İçinde **hedef konum**seçin kurtarma için istediğiniz toouse hello bulut yöneten hello VMM sunucusu.
5. İçinde **hedef bulut**, hello hedef bulut VM yük devretme için toouse istediğinizi seçin.
   * Koruduğunuz hello sanal makineleri kurtarma gereksinimlerini karşılayan bir hedef bulut seçmenizi öneririz.
   * Bir buluta yalnızca tooa tek bulut çifti--bir birincil veya bir hedef bulut olarak ait olabilir.
6. Site Recovery bulut erişim tooSAN depolama ve bu hello depolama dizileri eşlenen sahip olduğunu doğrular.
7. Doğrulama, başarılı olursa **çoğaltma türü**seçin **SAN**.

Hello ayarlarını kaydettikten sonra bir iş oluşturulur üzerinde hello izlenebilir **işleri** sekmesi. Üzerinde hello ayarları değiştirilebilir **yapılandırma** sekmesi. Toomodify hello hedef konumu veya hedef bulut istiyorsanız, hello bulut yapılandırmasını kaldırın ve hello Bulutu yeniden yapılandırmanız gerekir.

## <a name="step-5-enable-network-mapping"></a>5. adım: ağ eşlemesini etkinleştir

1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **ağları Eşle**.
2. Merhaba kaynak VMM sunucusunu seçin ve ardından ağların eşleneceği hello hedef VMM sunucusu toowhich hello seçin. Hello kaynak ağların ve ilişkili hedef ağlarının listesi görüntülenir. Boş bir değer eşlenmemiş ağlar için gösterilir. Merhaba bilgi simgesi sonraki toohello kaynak ve hedef ağ adları tooview hello her ağın alt ağlarını'ı tıklatın.
3. Bir ağ seçin **kaynak üzerinde ağ**ve ardından **harita**. Merhaba hizmet hello hedef sunucu üzerindeki hello VM ağlarını algılar ve görüntüler.

    ![SAN mimarisi](./media/site-recovery-vmm-san/network-map1.png)
4. Merhaba VM ağları birini hello hedef VMM sunucusunu seçin.

    ![SAN mimarisi](./media/site-recovery-vmm-san/network-map2.png)

5. Hedef ağ seçtiğinizde, hello hello kaynak ağı kullanan korumalı Bulutlar gösterilir. Kullanılabilir hedef ağlar da görüntülenir. Çoğaltma için kullanmakta olduğunuz kullanılabilir tooall hello Bulutlar olduğu bir hedef ağ seçmeniz önerilir.
6. Merhaba onay işareti toocomplete hello eşleme işlemini'ı tıklatın. Bir işin ilerleme durumunu izleyen başlatır. Merhaba üzerinde görüntülemek **işleri** sekmesi.

## <a name="step-6-enable-replication-for-replication-groups"></a>6. adım: çoğaltma grupları için çoğaltma etkinleştirme

Sanal makineler için korumayı etkinleştirmeden önce depolama çoğaltma grupları için tooenable çoğaltma gerekir.

1. Merhaba üzerinde **özellikleri** hello birincil bulut hello Site Recovery portalında, açık hello sayfasının **sanal makineleri** sekmesinde **çoğaltma grubuna Ekle**.
2. Merhaba Bulutu ile ilişkili olan select bir veya daha fazla VMM çoğaltma grupları hello kaynak ve hedef diziler doğrulayın ve hello çoğaltma sıklığı belirtin.

Site Recovery, VMM ve hello SMI-S sağlayıcıları hello hedef site depolama LUN sağlamak ve depolama çoğaltmayı etkinleştirin. Merhaba çoğaltma grubu zaten çoğaltılır, Site Recovery hello mevcut çoğaltma ilişkisinin yeniden kullanır ve bilgi güncelleştirmeleri hello.

## <a name="step-7-enable-protection-for-virtual-machines"></a>7. adım: sanal makineler için korumayı etkinleştir


Bir depolama grubu çoğaltırken VM'ler için korumayı hello VMM konsolundaki yöntemler aşağıdaki hello biriyle etkinleştirin:

* **Yeni sanal makine**: VM oluşturduğunuzda, çoğaltmayı etkinleştirip hello VM hello çoğaltma grubuyla ilişkilendirin.
  Bu seçenek ile VMM hello çoğaltma grubunun hello LUN'lara akıllı yerleştirme toooptimally yer hello VM depolama kullanır. Site Recovery gölge hello ikincil sitedeki VM hello oluşturulmasını düzenleyen ve böylece yük devretme sonrasında çoğaltma sanal makineleri başlatılabilir kapasite ayırır.
* **Var olan sanal makine**: bir sanal makine VMM'de dağıtılırsa, çoğaltmayı etkinleştirmek ve bir depolama geçişi tooa çoğaltma grubu gerçekleştirin. Tamamlama, VMM ve Site Recovery algılamak sonra yeni VM hello ve Site kurtarma yönetmeye başlama. Gölge VM hello ikincil sitede oluşturulur ve bu hello çoğaltma VM yük devretme sonrasında başlatılabilmesi kapasitesi ayrılır.

![Korumayı etkinleştir](./media/site-recovery-vmm-san/enable-protect.png)

Sanal makineleri çoğaltma için etkinleştirildikten sonra bunlar hello Site Recovery konsolunda görüntülenir. VM özelliklerini görüntüleme, izleme durumu ve birden fazla VM içermesi yük devretme çoğaltma grupları izlemek. SAN Çoğaltmada, çoğaltma grubuyla ilişkili tüm sanal makineleri birlikte yük devri gerekir. Yük devretme hello depolama katmanında önce gerçekleşirse olmasıdır. Bu, çoğaltma düzgün grupları ve yalnızca ilişkili VM'ler yerleştirmek önemli toogroup olur.

> [!NOTE]
> Bir sanal makine için çoğaltmayı etkinleştirdikten sonra bir Site Recovery çoğaltma grubunda bulundukları sürece, VHD tooLUNs eklemeyin. Bir Site Recovery çoğaltma grubunda bulunuyorsa VHD'ler yalnızca Site Recovery tarafından algılanır.
>
>

Merhaba üzerinde hello ilk çoğaltma dahil olmak üzere ilerleme durumunu izleyebilirsiniz **işleri** sekmesi. Merhaba korumayı Sonlandır işini çalıştıktan sonra hello sanal makine yük devretme için hazır olur.

![Sanal makine koruma işi](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>8. adım: Test hello dağıtımı

Sanal makineleri üzerinde beklendiği gibi başarısız emin, dağıtım toomake sınayın. toodo Bu, bir kurtarma planı oluşturabilir ve yük devretme testi çalıştırabilirsiniz.

1. Merhaba üzerinde **kurtarma planları** sekmesini tıklatın, **kurtarma planı oluşturma**.
2. Merhaba kurtarma planı için bir ad belirtin ve kaynak ve hedef VMM sunucuları seçin. Merhaba kaynak sunucu yük devretme ve kurtarma için etkinleştirilmiş sanal makineleri olması gerekir. Seçin **SAN** SAN çoğaltması için yapılandırılmış tooview tek bulut.

    ![Kurtarma planı oluşturma](./media/site-recovery-vmm-san/r-plan.png)

3. İçinde **sanal makineleri seçin**, çoğaltma gruplarını seçin. Merhaba grubuyla ilişkili tüm VM'ler toohello kurtarma planı eklenir. Bu sanal makineleri toohello kurtarma planının varsayılan grubu (Grup 1) eklenir. Gerekirse, daha fazla grup ekleyebilirsiniz. Çoğaltma işleminden sonra sanal makineleri toohello hello kurtarma planı grupların sırasını göre numaralandırılır.

    ![Sanal makineleri seçin](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Merhaba kurtarma planı oluşturulduktan sonra hello hello listede görünür **kurtarma planları** sekmesi. Merhaba planı seçin ve Seç **yük devretme testi**.
5. Merhaba üzerinde **onaylayın yük devretme testi** sayfasında, **hiçbiri**. Bu seçeneği etkinleştirdiğinizde, bağlı tooany ağ çoğaltma vm'lerinde hello olmayacaktır. Bu sanal makineleri beklendiği gibi yük devri bu hello sınar, ancak hello ağ ortamında test değil. Diğer ağ seçenekleri hakkında daha fazla bilgi için bkz: [Site Recovery yük devretme](site-recovery-failover.md).

    ![Select test ağı](./media/site-recovery-vmm-san/test-fail1.png)

6. Merhaba test VM aynı VM hangi hello kopyada mevcut hello konağına hello oluşturulur. Hangi hello çoğaltma VM bulunduğu toohello bulut eklenmez.
2. Çoğaltma işleminden sonra hello çoğaltma VM hello birincil sanal makine daha farklı bir IP adresi gerekir. DHCP'den adresleri veren, otomatik olarak güncelleştirilir. DHCP kullanmıyorsanız ve hello istiyorsanız aynı adresleri, toorun birkaç komut dosyalarının gerekir.
3. Bu komut dosyası tooretrieve başlangıç IP adresi çalıştırın:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Bu örnek komut dosyası tooupdate DNS çalıştırın. Başlangıç IP adresi, alınan belirtin.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Sonraki adımlar

Ortamınızı çalışan bir test yük devretme toocheck beklendiği gibi çalıştırdıktan sonra bkz: [Site Recovery yük devretme](site-recovery-failover.md) toolearn yerine farklı türleri hakkında.
