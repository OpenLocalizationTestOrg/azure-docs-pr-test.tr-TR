---
title: "Azure Site Kurtarma'yı kullanarak Azure Premium depolama alanına geçirme | Microsoft Docs"
description: "Varolan sanal makinelerinizi Site Kurtarma'yı kullanarak Azure Premium depolama alanına geçirin. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
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
ms.openlocfilehash: cc364bdae49068a50ec86c537c3b878670b8b8b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-premium-storage-using-azure-site-recovery"></a>Azure Site Recovery kullanarak Premium Depolamaya geçiş

[Azure Premium Storage](storage-premium-storage.md) g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler (VM'ler) için yüksek performanslı, düşük gecikmeli disk desteği sunar. Bu kılavuzun amacı kullanıcıların kendi VM diskleri kullanarak bir standart depolama hesabından bir Premium depolama hesabına geçirmek yardımcı olmaktır [Azure Site Recovery](../site-recovery/site-recovery-overview.md).

Site Recovery, şirket içi fiziksel sunucuların ve sanal makineleri buluta (Azure'a) veya ikincil veri merkezine çoğaltılmasını düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma stratejinize katkı sağlayan bir Azure hizmetidir. Kesinti birincil konumunuzda meydana gelirse uygulamaları ve iş yüklerini kullanılabilir durumda tutmak için ikincil konuma yük devredersiniz. Normal çalışmasına geri döndüğünde birincil konumunuz başarısız. Site Recovery, üretim ortamlarını etkilemeden olağanüstü durum kurtarma ayrıntılarını desteklemek için yük devretme testlerini sağlar. Beklenmeyen olağanüstü için en düşük düzeyde veri kaybı (bağlı olarak çoğaltma sıklığı) ile yük devretmeler çalıştırabilirsiniz. Premium depolama alanına geçiş senaryosunda, kullandığınız [Site Recovery yük](../site-recovery/site-recovery-failover.md) hedef diskler bir Premium depolama hesabına geçirmek için Azure Site kurtarma.

Bu seçenek en az kapalı kalma sağlar ve diskleri kopyalama ve yeni VM oluşturma el ile yürütme önler için Site RECOVERY'yi kullanarak Premium depolama alanına geçirme öneririz. Site Recovery sistematik olarak disklerinizi kopyalayın ve yük devretme sırasında yeni VM'ler oluşturun. Site Recovery türdeki yük devretme kümelemesiyle en az bir sayı veya kapalı kalma süresi destekler. Kapalı kalma süresini ayarlamanıza ve veri kaybı tahmin etmek için bkz: [yük devretme türlerini](../site-recovery/site-recovery-failover.md) Site Recovery tablosunda. Varsa, [yük devretme sonrasında Azure Vm'lerine bağlanmak hazırlama](../site-recovery/site-recovery-vmware-to-azure.md), yük devretme işleminden sonra RDP kullanarak Azure VM bağlanabiliyor olmalıdır.

![][1]

## <a name="azure-site-recovery-components"></a>Azure Site Recovery bileşenleri

Bu geçiş senaryosu için uygun olan Site Recovery bileşenleri şunlardır.

* **Yapılandırma sunucusu** iletişimi düzenler ve veri çoğaltma ve kurtarma işlemleri yöneten bir Azure VM. Bu VM yapılandırma sunucusu ve çoğaltma ağ geçidi olarak bir işlem sunucusu olarak adlandırılan bir ek bileşeni yüklemek için bir tek kurulum dosyasını çalıştırın. Hakkında bilgi edinin [yapılandırma sunucusu önkoşulları](../site-recovery/site-recovery-vmware-to-azure.md). Yapılandırma sunucusu yalnızca bir kez yapılandırılması gerekir ve aynı bölgeye tüm geçişler için kullanılabilir.

* **İşlem sunucusu** VM'ler kaynağından çoğaltma verileri alan bir çoğaltma ağ geçidi veri önbelleğe alma, sıkıştırma ve şifreleme ile en iyi duruma getirir ve bir depolama hesabına gönderir. Ayrıca kaynak VM'ler mobilite hizmetinin göndermeli yüklemesi işler ve VM'ler kaynağının otomatik bulma işlemini gerçekleştirir. Varsayılan işlem sunucusu yapılandırma sunucusuna yüklenir. Dağıtımınız ölçeklendirmek için ek tek başına işlem sunucuları dağıtabilirsiniz. Hakkında bilgi edinin [işlem sunucusu dağıtımı için en iyi uygulamaları](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) ve [ek işlem sunucuları dağıtma](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). İşlem sunucusu yalnızca bir kez yapılandırılması gerekir ve aynı bölgeye tüm geçişler için kullanılabilir.

* **Mobility hizmeti** çoğaltmak istediğiniz her standart VM üzerinde dağıtılan bir bileşenidir. Yakalar ve standart VM'de veri yazar ve işlem sunucusuna gönderir. Hakkında bilgi edinin [makine önkoşulları çoğaltılan](../site-recovery/site-recovery-vmware-to-azure.md).

Bu grafik, bu bileşenlerin nasıl etkileşim gösterir.

![][15]

> [!NOTE]
> Site Recovery, depolama alanları disklerini geçişini desteklemez.

Diğer senaryolar için ek bileşenler için lütfen [senaryo mimarisinin](../site-recovery/site-recovery-vmware-to-azure.md).

## <a name="azure-essentials"></a>Azure temelleri

Bu geçiş senaryosu için Azure gereksinimleri şunlardır.

* Bir Azure aboneliği
* Çoğaltılan verileri depolamak için bir Azure Premium storage hesabı
* Yük devretme sırasında oluşturulduğunda VM'ler bağlanacağı bir Azure sanal ağı (VNet). Azure sanal Site Recovery çalıştığı biri ile aynı bölgede olması gerekir
* Bir Azure standart depolama hesabı çoğaltma günlüklerini depolamak üzere. Bu Geçirilmekte olan VM diskleri aynı depolama hesabıyla olabilir

## <a name="prerequisites"></a>Ön koşullar

* Önceki bölümde ilgili geçiş senaryosu bileşenlerini anlama
* Hakkında bilgi edinerek, kesinti planlama [Site kurtarma yük devretme](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Kurulum ve geçiş adımları

Azure Iaas Vm'leri aynı bölgedeki veya bölgeler arasında geçirmek için Site Recovery kullanabilirsiniz. Aşağıdaki yönergeler makaleden bu geçiş senaryosu için hazırlanmış [çoğaltmak VMware Vm'lerini veya fiziksel sunucuları azure'a](../site-recovery/site-recovery-vmware-to-azure.md). Lütfen ayrıntılı için bağlantıları izleyin bu makaledeki yönergeleri için ek adımları.

1. **Kurtarma Hizmetleri kasası oluşturma**. Oluşturma ve yönetme üzerinden Site Recovery kasası [Azure portal](https://portal.azure.com). Tıklatın **yeni** > **Yönetim** > **yedekleme** ve **konum Kurtarma (OMS)**. Alternatif olarak tıklayabilirsiniz **Gözat** > **kurtarma Hizmetleri kasası** > **Ekle**. VM'ler, bu adımda belirttiğiniz bölgeye çoğaltılır. Aynı bölgede geçiş amacıyla, kaynak VM'ler ve kaynak depolama hesaplarının bulunduğu bölgeyi seçin. Premium depolama hesapları için geçiş içinde yalnızca desteklendiğini unutmayın [Azure portal](https://portal.azure.com)değil [Klasik portal](https://manage.windowsazure.com).

2. Aşağıdaki adımlar yardımcı **koruma hedeflerinizi seçme**.

    2a. Yapılandırma sunucusu yüklemek istediğiniz VM üzerinde açmak [Azure portal](https://portal.azure.com). Git **kurtarma Hizmetleri kasaları** > **ayarları**. Altında **ayarları**seçin **Site Recovery**. Altında **Site Recovery**seçin **1. adım: altyapıyı hazırlama**. Altında **altyapıyı hazırlama**seçin **koruma hedefi**.

    ![][2]

    2B. Altında **koruma hedefi**, ilk açılan listeden seçin **için Azure**. İkinci aşağı açılan listesinde seçin **değil sanallaştırılmış / diğer**ve ardından **Tamam**.

    ![][3]

3. Aşağıdaki adımlar yardımcı **(yapılandırma sunucusu) kaynak ortamını ayarlama**.

    3a. Karşıdan **Azure Site Recovery birleşik Kurulumu** ve **kasa kayıt anahtarını** giderek **altyapıyı hazırlama** > **kaynağı** > **Sunucu Ekle** dikey. Birleşik Kur'u çalıştırmak için kasa kayıt anahtarı gerekir. Anahtar, oluşturulduktan sonra 5 gün boyunca geçerlidir.

    ![][4]

    3B. Yapılandırma sunucusunda eklemek **Sunucu Ekle** dikey.

    ![][5]

    3c. VM yapılandırma sunucusu olarak kullanıyorsanız, birleşik yapılandırma sunucusu ve işlem sunucusu yüklemek için Kurulumu çalıştırın. Ekran görüntüleri yol [burada](../site-recovery/site-recovery-vmware-to-azure.md) yüklemeyi tamamlayın. Bu geçiş senaryosu için belirtilen adımları için aşağıdaki ekran görüntüleri başvurabilirsiniz.

    **Başlamadan önce** bölümünde **Yapılandırma sunucusu ve işlem sunucusunu yükle**’yi seçin.

    ![][6]

    3B. İçinde **kayıt**göz atın ve kasadan indirdiğiniz kayıt anahtarı seçin.

    ![][7]

    3E. **Ortam Ayrıntıları**’nda VMware sanal makinelerini çoğaltıp çoğaltmayacağınızı seçin. Bu geçiş senaryosu için seçme **Hayır**.

    ![][8]

    3F. Yükleme tamamlandıktan sonra göreceksiniz **Microsoft Azure Site kurtarma yapılandırma sunucusu** penceresi. Kullanmak **hesaplarını yönetme** sekmesi, Site kurtarma hesabı oluşturmak için otomatik bulma için kullanabilirsiniz. (Fiziksel makineleri koruma hakkında senaryosu, hesap kurma ilgili değildir ancak aşağıdaki adımlardan birini etkinleştirmek için en az bir hesabı gerekir. Bu durumda, tüm parola ve hesap adı verebilirsiniz.) Kullanım **kasa kayıt** için kasa kimlik bilgilerini karşıya yüklemek için sekmesi.

    ![][9]

4. **Hedef ortamını ayarlama**. Tıklatın **altyapıyı hazırlama** > **hedef**ve yük devretme sonrasında VM'ler için kullanmak istediğiniz dağıtım modelini belirtin. Seçebileceğiniz **Klasik** veya **Resource Manager**senaryonuza bağlı olarak.

    ![][10]

    Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler. Çoğaltılan veriler için bir Premium depolama hesabı kullanıyorsanız, çoğaltma günlüklerini depolamak için bir ek bir standart depolama hesabı ayarlamanız gerektiğini unutmayın.

5. **Çoğaltma ayarlarını belirleme**. Lütfen izleyin [çoğaltma ayarlarını belirleme](../site-recovery/site-recovery-vmware-to-azure.md) yapılandırma sunucusu oluşturduğunuz çoğaltma ilkesiyle başarıyla ilişkilendirildi olduğunu doğrulamak için.

6. **Kapasite planlama**. Kullanım [kapasite Planlayıcısı](../site-recovery/site-recovery-capacity-planner.md) ağ bant genişliği, depolama ve diğer gereksinimler, çoğaltma karşılamak için doğru şekilde tahmin gerekiyor. İşiniz bittiğinde seçin **Evet** içinde **kapasite planlamasını tamamladınız?**.

    ![][11]

7. Aşağıdaki adımlar yardımcı **mobilite hizmetinin yüklenmesi ve çoğaltmayı etkinleştirme**.

    7A. Seçebileceğiniz [anında yükleme](../site-recovery/site-recovery-vmware-to-azure.md) kaynak Vm'leriniz veya çok [mobility hizmeti el ile yüklemeniz](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) kaynağınız VM'ler üzerinde. Yükleme ve el ile yükleyici yolu sağlanan bağlantıyı Ftp'den zorunluluğu bulabilirsiniz. El ile yükleme yapıyorsanız, yapılandırma sunucusu bulmak için bir iç IP adresi kullanmanız gerekebilir.

    ![][12]

    Başarısız üzerinden VM iki geçici disk olacaktır: birincil VM ve diğer VM kurtarma bölgede hazırlama sırasında oluşturulan birinden. Geçici disk çoğaltma önce dışlamak için çoğaltma etkinleştirmeden önce mobility hizmetini yükleyin. Geçici disk hariç hakkında daha fazla bilgi için bkz [Çoğaltmada diskleri Dışla](../site-recovery/site-recovery-vmware-to-azure.md).

    7B. Şimdi aşağıda belirtilen şekilde çoğaltmayı etkinleştirin:
      * Tıklatın **uygulama çoğaltma** > **kaynak**. Çoğaltma ilk kez etkinleştirdikten sonra ilave makineler için çoğaltmayı etkinleştirmek için kasada çoğaltmak + tıklayın.
      * 1. adımda kaynak, işlem sunucusu olarak ayarlayın.
      * Adım 2'de, yük devretme sonrası dağıtım modeli, geçirmek için Premium depolama hesabı, günlükleri ve başarısız bir sanal ağı kaydetmek için bir standart depolama hesabı belirtin.
      * 3. adımda (bunları bulmak için bir iç IP adresi gerekebilir) IP adresine göre korumalı sanal makineleri ekleyin.
      * 4. adımda, işlem sunucusunda önceden ayarlanmış hesaplarının seçerek özelliklerini yapılandırın.
      * 5. adımda, çoğaltma ayarlarını belirleme, daha önce oluşturduğunuz çoğaltma ilkesi seçin.
      Tıklatın **Tamam** ve çoğaltmayı etkinleştirin.

    > [!NOTE]
    > Bir Azure VM serbest ve yeniden başlatıldığı zaman aynı IP adresi al garantisi yoktur. Yapılandırma sunucusu/işlem sunucusunun veya korumalı Azure sanal makinelerini IP adresini değiştirirseniz, bu senaryoda çoğaltma düzgün çalışmayabilir.

    ![][13]

    Azure depolama ortamınızı tasarlarken, bir kullanılabilirlik kümesindeki her bir VM için ayrı bir depolama hesapları kullanmanızı öneririz. Depolama katmanı için en iyi uygulamada izlemenizi öneririz [her kullanılabilirlik kümesi için birden çok depolama hesabı kullanmak](../virtual-machines/windows/manage-availability.md). Birden çok depolama hesabı VM diskleri dağıtma, depolama alanı kullanılabilirliği artırmaya yardımcı olur ve g/ç Azure depolama altyapınız genelinde dağıtır. Diskleri tüm VM'lerin bir storage hesabınıza çoğaltmak yerine bir kullanılabilirlik kümesinde Vm'leriniz varsa böylece sanal makineleri aynı kullanılabilirlik kümesindeki tek bir depolama hesabına paylaşmaz birden çok kez birden çok VM geçirme öneririz. Kullanım **çoğaltmayı etkinleştirme** dikey her sanal makine için bir kerede bir hedef depolama hesabı ayarlama. Gereksiniminize uygun bir yük devretme sonrası dağıtım modeli seçebilirsiniz. Kaynak Yöneticisi (RM), yük devretme sonrası dağıtım modeli seçerseniz, RM VM RM VM devredebildiğini veya Klasik VM RM VM devredebilir.

8. **Bir yük devretme testi**. Çoğaltma tam olup olmadığını denetlemek için Site Kurtarma'yı tıklatın ve ardından **ayarları** > **çoğaltılan öğeler**. Çoğaltma işleminizi yüzdesi ve durumu görürsünüz. İlk çoğaltma sonrasında, çoğaltma stratejinizi doğrulamak için yük devretme testi çalıştırmak, tamamlanır. Yük devretme testi ayrıntılı adımlar için lütfen [Site kurtarma için yük devretme testi çalıştırmak](../site-recovery/site-recovery-vmware-to-azure.md). Yük devretme testi durumunu görebilirsiniz **ayarları** > **işleri** > **YOUR_FAILOVER_PLAN_NAME**. Dikey penceresinde adımlar ve başarı/hata sonuçları bir dökümünü görürsünüz. Yük devretme sınaması herhangi bir adımda başarısız olursa, hata iletisi denetlemek için adım'ı tıklatın. VM'ler ve çoğaltma stratejisi bir yük devretme çalıştırmadan önce gereksinimleri karşıladığınızdan emin olun. Okuma [Azure Site kurtarma sınama yük devretmesi](../site-recovery/site-recovery-test-failover-to-azure.md) daha fazla bilgi ve yönergeler test yük devretme.

9. **Yük devretme gerçekleştirme**. Test sonra disklerinizi Premium depolama alanına geçirmek ve VM örnekleri çoğaltmak için yük devretme gerçekleştirme yük devretme tamamlanır. Lütfen ayrıntılı adımları [yük devretme gerçekleştirme](../site-recovery/site-recovery-failover.md#run-a-failover). Seçtiğinizden emin olun **sanal makineleri kapatın ve en son verileri eşitleyin** korumalı sanal makineleri kapatın ve böylece verilerin en son sürümünü devredilir verileri eşitlemek Site Recovery denemelisiniz belirtmek için. Bu seçeneği seçmeyin veya denemesi başarılı olmayan yük devretme VM için en son kullanılabilir kurtarma noktası arasında olacaktır. Site Recovery, aynı veya benzer bir Premium depolama özellikli VM türü olan bir VM örneği oluşturur. Giderek çeşitli VM örnekleri fiyat ve performans denetleyebilirsiniz [Windows sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) veya [Linux sanal makineleri fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Geçiş sonrası adımlar

1. **Çoğaltılmış VM'ler varsa kullanılabilirlik için yapılandırma**. Site Recovery kullanılabilirlik kümesi ile birlikte geçirme sanal makineleri desteklemez. Çoğaltılmış VM'yi dağıtım bağlı olarak aşağıdakilerden birini yapın:
  * Klasik dağıtım modeli kullanılarak oluşturulmuş bir VM için: VM kullanılabilirlik Azure portalında kümesini ekleyin. Ayrıntılı adımlar için Git [var olan bir sanal makine bir kullanılabilirlik kümesine ekleme](../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Resource Manager dağıtım modeli için: VM yapılandırmanızı kaydetmek ve ardından silin ve kullanılabilirlik kümesindeki sanal makineleri yeniden oluşturun. Bunu yapmak için komut kullanın [Azure Kaynak Yöneticisi'ni VM kullanılabilirlik Set](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Bu komut dosyası sınırlandırılmasıdır denetleyin ve komut dosyasını çalıştırmadan önce kapalı kalma süresi planlayın.

2. **Eski VM'ler ve diskleri silme**. Bunlar silmeden önce lütfen Premium disklerin kaynak diskler ile tutarlı ve yeni VM'ler VM'ler kaynak ile aynı işlevi gerçekleştirir emin olun. Kaynak Yöneticisi (RM) dağıtım modelinde VM ve Azure portalındaki kaynak depolama hesaplarınızdan diskleri silin. Klasik dağıtım modelinde, Klasik portalında veya Azure portal diskleri ve VM silebilirsiniz. Hangi disk silinmez VM silinmiş olsa bile bir sorun varsa, lütfen bkz [VHD'ler sildiğinizde hatalarında sorun giderme](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Azure Site Recovery altyapısı temiz**. Site Recovery artık gereksinim duyulmuyorsa, çoğaltılan öğeler, yapılandırma sunucusunu ve kurtarma ilkesi silme ve Azure Site Recovery kasası silme alt yapısına temizleyebilirsiniz.

## <a name="troubleshooting"></a>Sorun giderme

* [İzleme ve sanal makineleri ve fiziksel sunucuları için koruması sorunlarını giderme](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Microsoft Azure Site Recovery Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Sonraki adımlar

Sanal makineleri geçirmek için belirli senaryolar için aşağıdaki kaynaklara bakın:

* [Azure sanal makineleri depolama hesapları arasında geçiş](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Oluşturun ve Windows Server VHD Azure'a yükleyin.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Oluşturma ve Linux işletim sistemini içeren bir Sanal Sabit Disk karşıya yükleme](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Geçirme sanal makinelerden Amazon AWS Microsoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Ayrıca, Azure Storage ve Azure sanal makineler hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

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
