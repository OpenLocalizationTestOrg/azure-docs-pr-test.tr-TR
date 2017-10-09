---
title: Premium Azure Site RECOVERY'yi kullanarak depolama aaaMigrating tooAzure | Microsoft Docs
description: "Var olan sanal makineleri tooAzure Premium Site RECOVERY'yi kullanarak depolama geçirin. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cb71c06e4a1a73d484e226a573d1ade48c87664d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery"></a>Geçirme tooPremium Azure Site Recovery kullanarak depolama

[Azure Premium Storage](storage-premium-storage.md) g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler (VM'ler) için yüksek performanslı, düşük gecikmeli disk desteği sunar. Bu kılavuzun amacı Hello olduğu toohelp kullanıcıların geçişini kendi VM diskleri bir standart depolama hesabı tooa Premium depolama hesabı kullanarak [Azure Site Recovery](../site-recovery/site-recovery-overview.md).

Olağanüstü durum kurtarma stratejiniz yönetme tarafından hello şirket içi fiziksel sunucuların ve sanal makineleri toohello buluta (Azure'a) veya tooa ikincil veri merkezine çoğaltma ve site kurtarma tooyour iş sürekliliği katkıda bulunan bir Azure hizmetidir. Kesinti birincil konumunuzda meydana toohello ikincil konum tookeep uygulamaları ve iş yüklerini kullanılabilir başarısız. Toonormal işlemi geri döndüğünde geri tooyour birincil konumu başarısız. Site Recovery, üretim ortamlarını etkilemeden toosupport olağanüstü durum kurtarma ayrıntılarını yük devretme sınaması işlemlerini sağlar. Beklenmeyen olağanüstü için en düşük düzeyde veri kaybı (bağlı olarak çoğaltma sıklığı) ile yük devretmeler çalıştırabilirsiniz. Merhaba senaryosunda tooPremium depolama geçişi, hello kullanabilirsiniz [Site Recovery yük](../site-recovery/site-recovery-failover.md) Azure Site Recovery toomigrate hedef diskleri tooa Premium depolama hesabı içinde.

Geçiş öneririz çünkü bu seçenek en az kapalı kalma sağlar ve diskleri kopyalama ve yeni VM oluşturma hello el ile yürütme önler Site Recovery kullanarak depolama tooPremium. Site Recovery sistematik olarak disklerinizi kopyalayın ve yük devretme sırasında yeni VM'ler oluşturun. Site Recovery türdeki yük devretme kümelemesiyle en az bir sayı veya kapalı kalma süresi destekler. tooplan, kapalı kalma süresi ve tahmin veri kaybı hello bkz [yük devretme türlerini](../site-recovery/site-recovery-failover.md) Site Recovery tablosunda. Varsa, [tooconnect tooAzure VM'ler yük devretme sonrasında hazırlama](../site-recovery/site-recovery-vmware-to-azure.md), mümkün tooconnect toohello Azure VM olmalıdır yük devretmeden sonra RDP kullanarak.

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery bileşenleri

İlgili toothis geçiş senaryosu hello Site Recovery bileşenleri şunlardır.

* **Yapılandırma sunucusu** iletişimi düzenler ve veri çoğaltma ve kurtarma işlemleri yöneten bir Azure VM. Bu VM tek kurulum dosyası tooinstall hello yapılandırma sunucusu ve işlem sunucusu, çoğaltma ağ geçidi olarak adlı bir ek bileşen çalışır. Hakkında bilgi edinin [yapılandırma sunucusu önkoşulları](../site-recovery/site-recovery-vmware-to-azure.md). Yapılandırma sunucusu yalnızca bir kez yapılandırılmış toobe gerekir ve tüm geçişler toohello için kullanılan aynı bölgede.

* **İşlem sunucusu** VM'ler kaynağından çoğaltma verileri alan bir çoğaltma ağ geçidi hello veri önbelleğe alma, sıkıştırma ve şifreleme ile en iyi duruma getirir ve tooa depolama hesabı gönderir. Ayrıca hello mobility hizmeti toosource VM'ler itme yüklemesini işler ve VM'ler kaynağının otomatik bulma işlemini gerçekleştirir. Merhaba varsayılan işlem sunucusu hello yapılandırma sunucusuna yüklenir. Dağıtımınıza ek tek başına işlem sunucuları tooscale dağıtabilirsiniz. Hakkında bilgi edinin [işlem sunucusu dağıtımı için en iyi uygulamaları](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) ve [ek işlem sunucuları dağıtma](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). İşlem sunucusu yalnızca bir kez yapılandırılmış toobe gerekir ve tüm geçişler toohello için kullanılan aynı bölgede.

* **Mobility hizmeti** , dağıtılan bir bileşen olan her standart VM tooreplicate istiyor. Veri yazma yakalar standart VM hello ve bunları toohello işlem sunucusuna iletir. Hakkında bilgi edinin [makine önkoşulları çoğaltılan](../site-recovery/site-recovery-vmware-to-azure.md).

Bu grafik, bu bileşenlerin nasıl etkileşim gösterir.

![][15]

> [!NOTE]
> Site Recovery, depolama alanları disklerini hello geçişini desteklemez.

Diğer senaryolar için ek bileşenler için çok başvurun[senaryo mimarisinin](../site-recovery/site-recovery-vmware-to-azure.md).

## <a name="azure-essentials"></a>Azure temelleri

Bunlar olan hello bu geçiş senaryosu için Azure gereksinimleri.

* Bir Azure aboneliği
* Verileri Azure Premium depolama hesabı toostore çoğaltılan
* Yük devretme sırasında oluşturulduğunda Azure sanal ağı (VNet) toowhich VM'ler bağlanır. Hello Azure VNet olması gerekir. bir Site Recovery hangi hello çalıştıran hello gibi aynı bölgede hello
* Bir standart Azure depolama hesabında hangi toostore çoğaltma günlükleri. Bu, Geçirilmekte olan hello VM diskleri gibi hello aynı depolama hesabı

## <a name="prerequisites"></a>Ön koşullar

* Önceki bölümde hello içinde Hello ilgili geçiş senaryosu bileşenlerini anlama
* Kesinti öğrenme tarafından hello hakkında planlama [Site kurtarma yük devretme](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Kurulum ve geçiş adımları

Site Recovery toomigrate Azure Iaas Vm'leri bölgeler arasında veya aynı bölge içinde kullanabilirsiniz. Merhaba aşağıdaki yönergeleri hello makalesinden bu geçiş senaryosu için özel olarak hazırlanmış [çoğaltmak VMware Vm'lerini veya fiziksel sunucuları tooAzure](../site-recovery/site-recovery-vmware-to-azure.md). Bu makalede ek toohello yönergelerinde ayrıntılı adımlar için hello bağlantıları izleyin.

1. **Kurtarma Hizmetleri kasası oluşturma**. Oluşturma ve yönetme hello Site Recovery kasası hello aracılığıyla [Azure portal](https://portal.azure.com). Tıklatın **yeni** > **Yönetim** > **yedekleme** ve **konum Kurtarma (OMS)**. Alternatif olarak tıklayabilirsiniz **Gözat** > **kurtarma Hizmetleri kasası** > **Ekle**. Sanal makineleri bu adımda belirttiğiniz çoğaltılmış toohello bölge olacaktır. Merhaba geçişte hello amacı için aynı bölge, kaynak VM'ler ve kaynak depolama hesapları nerede select hello bölgesi. Geçiş tooPremium depolama hesapları yalnızca desteklenir, hello Not [Azure portal](https://portal.azure.com), değil hello [Klasik portal](https://manage.windowsazure.com).

2. Merhaba aşağıdaki adımlar yardımcı **koruma hedeflerinizi seçme**.

    2a. Merhaba Hello tooinstall hello yapılandırma sunucusu istediğiniz VM, açık [Azure portal](https://portal.azure.com). Çok Git**kurtarma Hizmetleri kasaları** > **ayarları**. Altında **ayarları**seçin **Site Recovery**. Altında **Site Recovery**seçin **1. adım: altyapıyı hazırlama**. Altında **altyapıyı hazırlama**seçin **koruma hedefi**.

    ![][2]

    2B. Altında **koruma hedefi**, buna hello ilk açılan listeden, seçin **tooAzure**. Merhaba ikinci aşağı açılan listesinde seçin **değil sanallaştırılmış / diğer**ve ardından **Tamam**.

    ![][3]

3. Merhaba aşağıdaki adımlar yardımcı **hello kaynak ortamını (yapılandırma sunucusu) ayarlama**.

    3a. Merhaba karşıdan **Azure Site Recovery birleşik Kurulumu** ve hello **kasa kayıt anahtarını** giderek toohello tarafından **altyapıyı hazırlama**  >  **Kaynağı** > **Sunucu Ekle** dikey. Kasa kayıt anahtarı toorun birleşik hello Kurulum hello gerekir. Merhaba anahtar, oluşturulduktan sonra 5 gün boyunca geçerlidir.

    ![][4]

    3B. Yapılandırma sunucusu hello eklemek **Sunucu Ekle** dikey.

    ![][5]

    3c. Hello VM hello yapılandırma sunucusu olarak kullanıyorsanız, birleşik Kurulum tooinstall hello yapılandırma sunucusu ve hello işlem sunucusu çalıştırın. Merhaba ekran görüntüleri yol [burada](../site-recovery/site-recovery-vmware-to-azure.md) toocomplete hello yükleme. Ekran görüntüleri için bu geçiş senaryosu için belirtilen adımları izleyerek toohello başvurabilir.

    İçinde **başlamadan önce**seçin **yükleme hello yapılandırma sunucusu ve işlem sunucusu**.

    ![][6]

    3B. İçinde **kayıt**göz atın ve hello kasadan indirdiğiniz hello kayıt anahtarını seçin.

    ![][7]

    3E. İçinde **ortam ayrıntıları**tooreplicate VMware Vm'lerini oluşturacağız olup olmadığını seçin. Bu geçiş senaryosu için seçme **Hayır**.

    ![][8]

    3F. Merhaba yüklemesi tamamlandıktan sonra hello görürsünüz **Microsoft Azure Site kurtarma yapılandırma sunucusu** penceresi. Merhaba kullanmak **hesaplarını yönetme** sekmesinde toocreate hello otomatik bulma için Site Recovery kullanan bir hesap. (Merhaba senaryosu, fiziksel makineleri koruma hakkında hello hesabı kurma ilgili değildir ancak en az bir hesabı tooenable biri, aşağıdaki adımları hello gerekir. Bu durumda, hello hesap ve parola herhangi olarak adlandırabilirsiniz.) Kullanım hello **kasa kayıt** sekmesini tooupload hello kasa kimlik bilgileri dosyası.

    ![][9]

4. **Merhaba hedef ortamını ayarlama**. Tıklatın **altyapıyı hazırlama** > **hedef**ve istediğiniz toouse VM'ler için yük devretme sonrasında hello dağıtım modelini belirtin. Seçebileceğiniz **Klasik** veya **Resource Manager**senaryonuza bağlı olarak.

    ![][10]

    Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler. Çoğaltılan veriler için bir Premium depolama hesabı kullanıyorsanız, ek bir standart depolama hesabı toostore çoğaltma tooset gerektiğini unutmayın günlükleri.

5. **Çoğaltma ayarlarını belirleme**. Lütfen izleyin [çoğaltma ayarlarını belirleme](../site-recovery/site-recovery-vmware-to-azure.md) yapılandırma sunucusu oluşturduğunuz hello çoğaltma ilkesiyle başarıyla ilişkilendirildi tooverify.

6. **Kapasite planlama**. Kullanım hello [kapasite Planlayıcısı](../site-recovery/site-recovery-capacity-planner.md) tooaccurately tahmin ağ bant genişliği, depolama ve diğer gereksinimleri toomeet, çoğaltma gerekiyor. İşiniz bittiğinde seçin **Evet** içinde **kapasite planlamasını tamamladınız?**.

    ![][11]

7. Merhaba aşağıdaki adımlar yardımcı **mobilite hizmetinin yüklenmesi ve çoğaltmayı etkinleştirme**.

    7A. Çok seçebilirsiniz[anında yükleme](../site-recovery/site-recovery-vmware-to-azure.md) tooyour kaynak VM'ler veya çok[mobility hizmeti el ile yüklemeniz](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) kaynağınız VM'ler üzerinde. Sağlanan hello bağlantıdaki koymadan yüklemesinin hello gereksinim ve hello el ile yükleyici hello yolu bulabilirsiniz. El ile yükleme yapıyorsanız, bir iç IP adresi toofind hello yapılandırma sunucusu toouse gerekebilir.

    ![][12]

    Merhaba başarısız üzerinden VM iki geçici disk olacaktır: birinden hello birincil VM ve VM hello kurtarma bölgede hello hazırlama sırasında oluşturulan hello diğer. Çoğaltma önce tooexclude hello geçici disk çoğaltma etkinleştirmeden önce hello mobility hizmetini yükleyin. nasıl tooexclude hello geçici disk hakkında daha fazla toolearn başvurmak çok[Çoğaltmada diskleri Dışla](../site-recovery/site-recovery-vmware-to-azure.md).

    7B. Şimdi aşağıda belirtilen şekilde çoğaltmayı etkinleştirin:
      * Tıklatın **uygulama çoğaltma** > **kaynak**. Hello için çoğaltma ilk kez etkinleştirdikten sonra hello kasa tooenable çoğaltma ilave makineler için çoğaltma + tıklayın.
      * 1. adımda kaynak, işlem sunucusu olarak ayarlayın.
      * 2. adımda hello yük devretme sonrası dağıtım modeli, bir Premium depolama hesabı toomigrate, bir standart depolama hesabı toosave günlüklerine ve bir sanal ağ toofail belirtin.
      * 3. adımda IP adresine göre korumalı sanal makineleri ekleyin (bir iç IP adresi toofind gerekebilecek bunları).
      * 4. adımda hello işlem sunucusunda önceden ayarlanmış hello hesaplarının seçerek hello özelliklerini yapılandırın.
      * 5. adımda, çoğaltma ayarlarını belirleme, daha önce oluşturduğunuz hello çoğaltma ilkesi seçin.
      Tıklatın **Tamam** ve çoğaltmayı etkinleştirin.

    > [!NOTE]
    > Bir Azure VM serbest ve yeniden başlatılabilir olduğunda alır garanti hello aynı IP adresi. Azure VM'ler değişiklik Hello IP adresini hello yapılandırma sunucusu/işlem sunucusu veya hello korunan varsa, bu senaryoda hello çoğaltma düzgün çalışmayabilir.

    ![][13]

    Azure depolama ortamınızı tasarlarken, bir kullanılabilirlik kümesindeki her bir VM için ayrı bir depolama hesapları kullanmanızı öneririz. Merhaba depolama katmanı hello uygulamada çok izlemenizi öneririz[her kullanılabilirlik kümesi için birden çok depolama hesabı kullanmak](../virtual-machines/windows/manage-availability.md). VM diskleri toomultiple depolama hesapları dağıtma tooimprove depolama alanı kullanılabilirliği yardımcı olur ve hello g/ç hello Azure depolama altyapınız genelinde dağıtır. Diskleri tüm VM'lerin bir storage hesabınıza çoğaltmak yerine bir kullanılabilirlik kümesinde Vm'leriniz varsa hello Vm'lerde aynı hello böylece birden çok kez birden çok VM geçirme öneririz kullanılabilirlik kümesi, tek bir depolama hesabına paylaşmıyor. Kullanım hello **çoğaltmayı etkinleştirme** dikey tooset her sanal makine için bir seferde bir hedef depolama hesabı. Bir yük devretme sonrası dağıtım modeli tooyour gerek göre seçebilirsiniz. Kaynak Yöneticisi (RM), yük devretme sonrası dağıtım modeli seçerseniz, RM VM tooan RM VM başarısız olabilir veya Klasik VM tooan RM VM başarısız olabilir.

8. **Bir yük devretme testi**. toocheck, çoğaltma tamamlandıktan olup olmadığını, Site Kurtarma'yı tıklatın ve ardından **ayarları** > **çoğaltılan öğeler**. Merhaba durumu ve çoğaltma işleminizi yüzdesini görürsünüz. İlk çoğaltma sonrasında, çoğaltma stratejinizi tam, çalışma yük devretme testi toovalidate olur. Yük devretme testi ayrıntılı adımlar için lütfen çok başvurun[Site kurtarma için yük devretme testi çalıştırmak](../site-recovery/site-recovery-vmware-to-azure.md). Yük devretme testi hello durumunu görebilirsiniz **ayarları** > **işleri** > **YOUR_FAILOVER_PLAN_NAME**. Merhaba dikey penceresinde hello adımları ve başarı/hata sonuçları bir dökümünü görürsünüz. Herhangi bir adımda Hello yük devretme testi başarısız olursa, hello adım toocheck hello hata iletisi'ı tıklatın. Bir yük devretme çalıştırmadan önce VM'ler ve çoğaltma stratejisi hello gereksinimleri karşıladığından emin olun. Okuma [Site kurtarma sınama yük devretmesi tooAzure](../site-recovery/site-recovery-test-failover-to-azure.md) daha fazla bilgi ve yönergeler test yük devretme.

9. **Yük devretme gerçekleştirme**. Hello test yük devretmesi tamamlandıktan sonra diskleri tooPremium depolama yük devretme toomigrate çalıştırın ve hello VM örnekleri çoğaltma. Lütfen izleyin hello ayrıntılı adımları [yük devretme gerçekleştirme](../site-recovery/site-recovery-failover.md#run-a-failover). Seçtiğinizden emin olun **sanal makineleri kapatın ve hello en son verileri eşitleyin** toospecify Site Recovery korumalı hello VM'ler aşağı tooshut deneyin ve hello hello veri en son sürümünü devretme gerçekleştirilecek şekilde hello verileri eşitleyin. Bu seçeneği seçmeyin veya hello denemesi başarılı olmayan hello yük devretme hello VM için hello en son kullanılabilir kurtarma noktası arasında olacaktır. Site Recovery, aynı veya benzer tooa Premium depolama özellikli VM hello türü olan bir VM örneği oluşturur. Çok giderek hello performansı ve çeşitli VM örnekleri fiyat denetleyebilirsiniz[Windows sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) veya [Linux sanal makineleri fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Geçiş sonrası adımlar

1. **Çoğaltılan VM'ler toohello kullanılabilirlik varsa kümesi yapılandırma**. Site Recovery hello kullanılabilirlik kümesi ile birlikte geçirme sanal makineleri desteklemez. Çoğaltılmış VM'yi Hello dağıtımını bağlı olarak, hello aşağıdakilerden birini yapın:
  * Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş bir VM için: hello VM toohello kullanılabilirlik hello Azure portal kümesi ekleyin. Ayrıntılı adımlar için çok Git[ekleme varolan bir sanal makine tooan kullanılabilirlik kümesini](../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Merhaba Resource Manager dağıtım modeli için: hello VM yapılandırmanızı kaydedin ve ardından silin ve hello VM'ler hello kullanılabilirlik kümesindeki yeniden oluşturun. toodo, kullanın hello komut [Azure Kaynak Yöneticisi'ni VM kullanılabilirlik Set](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Bu komut dosyasının Hello sınırlaması denetleyin ve kapalı kalma süresi başlangıç betiği çalıştırmadan önce planlayın.

2. **Eski VM'ler ve diskleri silme**. Bunlar silmeden önce lütfen hello Premium diskleri kaynak diskleri ve yeni sanal makineleri aynı VM'ler hello kaynağı olarak işlevi hello gerçekleştirmek hello ile tutarlı olduğundan emin olun. Merhaba Kaynak Yöneticisi (RM) dağıtım modelinde hello VM ve hello Azure portal'ın kaynak depolama hesaplarınızdan hello diskleri silin. Merhaba Klasik dağıtım modelinde hello VM ve diskleri hello Klasik portalında veya Azure portal silebilirsiniz. Hangi hello disk hello VM silinmiş olsa bile silinmez bir sorun varsa, lütfen bkz [VHD'ler sildiğinizde hatalarında sorun giderme](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Temiz hello Azure Site Recovery altyapısı**. Site Recovery artık gereksinim duyulmuyorsa, çoğaltılan öğeler, hello yapılandırma sunucusu ve hello kurtarma ilkesi silme ve hello Azure Site Recovery kasası silme alt yapısına temizleyebilirsiniz.

## <a name="troubleshooting"></a>Sorun giderme

* [İzleme ve sanal makineleri ve fiziksel sunucuları için koruması sorunlarını giderme](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Sonraki adımlar

Sanal makineleri geçirmek için belirli senaryolar için kaynaklar aşağıdaki hello bakın:

* [Azure sanal makineleri depolama hesapları arasında geçiş](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Oluşturun ve Windows Server VHD tooAzure yükleyin.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Oluşturma ve bir Sanal Sabit Disk, Linux işletim sistemi içerir hello karşıya yükleme](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Amazon AWS tooMicrosoft Azure sanal makinelerden geçirme](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Ayrıca, Azure Storage ve Azure sanal makineler hakkında daha fazla kaynak toolearn aşağıdaki hello bakın:

* [Azure Depolama](https://azure.microsoft.com/documentation/services/storage/)
* [Azure sanal makineler](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
