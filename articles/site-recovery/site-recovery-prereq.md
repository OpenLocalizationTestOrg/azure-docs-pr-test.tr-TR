---
title: "Azure Site Recovery kullanarak çoğaltma tooAzure aaaPrerequisites | Microsoft Docs"
description: "Hello Azure Site Recovery hizmetini kullanarak sanal makineleri ve fiziksel makineler tooAzure çoğaltma hello önkoşulları hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Site Recovery kullanarak şirket içi tooAzure Çoğaltmada için Önkoşullar

> [!div class="op_single_selector"]
> * [Azure tooAzure çoğaltma](site-recovery-azure-to-azure-prereq.md)
> * [Şirket içi tooAzure çoğaltma](site-recovery-prereq.md)

Azure Site Recovery, bir Azure sanal makine (VM) tooanother Azure bölgesi çoğaltılmasını düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize destek yardımcı olabilir. Site Recovery, şirket içi fiziksel sunucuların ve sanal makineleri toohello buluta (Azure'a) veya tooa ikincil veri merkezine de çoğaltır. Kesinti birincil konumunuzda meydana gelirse, tooa ikincil konum tookeep uygulamalar ve iş yüklerini kullanılabilir başarısız olabilir. Merhaba birincil konumu toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız olabilir. Site Recovery hakkında daha fazla bilgi için bkz: [Site Recovery nedir?](site-recovery-overview.md).

Bu makalede, bir şirket içi makineyi tooAzure Site Recovery Çoğaltmada başlayan hello önkoşulları özetler.

Merhaba makalenin hello altındaki tüm yorumlar nakledebilirsiniz. Ayrıca hello içinde teknik sorular sorabilirsiniz [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Azure gereksinimleri

**Gereksinim** | **Ayrıntılar**
--- | ---
**Azure hesabı** | A [Microsoft Azure hesabı](http://azure.microsoft.com/). [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
**Site Recovery hizmeti** | Azure Site Recovery hizmeti hello için fiyatlandırma hakkında daha fazla bilgi için bkz: [Site Recovery fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Azure Depolama** | Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir. Merhaba depolama hesabı hello olmalıdır hello aynı bölgede Azure kurtarma Hizmetleri kasası. Yük devretme durumunda azure Vm'leri oluşturulur.<br/><br/> Merhaba kaynak modeline bağlı olarak Azure VM yük devretme için toouse istiyorsanız, bir hesap hello kullanarak ayarlayabilirsiniz [Azure Resource Manager dağıtım modeli](../storage/common/storage-create-storage-account.md) veya hello [Klasik dağıtım modeli](../storage/common/storage-create-storage-account.md).<br/><br/>[Coğrafi olarak yedekli depolama](../storage/common/storage-redundancy.md#geo-redundant-storage) veya yerel olarak yedekli depolama kullanabilirsiniz. Coğrafi olarak yedekli depolama kullanmanızı öneririz. Coğrafi olarak yedekli depolama ile veri bölgesel bir kesinti oluşursa ya da hello birincil bölgenin kurtarılamaması esnektir.<br/><br/> Bir standart Azure depolama hesabı kullanabilir veya Azure Premium Storage kullanabilirsiniz. [Premium depolama](https://docs.microsoft.com/azure/storage/storage-premium-storage) genellikle sürekli olarak yüksek g/ç performans ve düşük gecikme gerektiren VM'ler için kullanılır. Premium depolama ile bir VM g/Ç kullanımı yoğun iş yükleri barındırabilir. Çoğaltılan veriler için premium depolama kullanırsanız, ayrı bir standart depolama hesabı gerekir. Standart depolama hesabı sürekli değişikliklerin tooon içi verilerini yakalama çoğaltma günlükleri depolar.<br/><br/>
**Depolama sınırlamaları** | Site Recovery tooa farklı kaynak grubunda kullandığınız depolama hesapları taşınamıyor veya başka bir abonelik ile tooor kullanım taşıyın.<br/><br/> Şu anda, Orta Hindistan ve Güney Hindistan toopremium depolama hesapları çoğaltma kullanılamıyor.
**Azure ağı** | Bir Azure ağı gerekir, yük devretme sonrasında toowhich Azure VM'ler bağlanın. Hello Azure ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.<br/><br/> Hello Azure portal, hello kullanarak bir Azure ağı oluşturabilirsiniz [Resource Manager dağıtım modeli](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) veya hello [Klasik dağıtım modeli](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> System Center Virtual Machine Manager (VMM) tooAzure çoğaltma yaparsanız Azure ağları ve VMM VM ağları arasında ağ eşlemesi ayarlamanız gerekir. Bu, yük devretme sonrasında Azure Vm'lerinin tooappropriate ağlara bağlanmak sağlar.
**Ağ sınırlamaları** | Site Recovery tooa farklı kaynak grubunda kullandığınız ağ hesapları taşınamıyor veya başka bir abonelik ile tooor kullanım taşıyın.
**Ağ eşlemesi** | VMM bulutlarındaki Microsoft Hyper-V Vm'lerini çoğaltma, ağ eşlemesi ayarlamanız gerekir. Bu, yük devretme sonrasında oluşturulduğunda Azure VM'ler tooappropriate ağlara bağlanmak sağlar.

> [!NOTE]
> Merhaba aşağıdaki bölümlerde hello müşteri ortamının çeşitli bileşenlerini hello önkoşulları açıklanmaktadır. Merhaba belirli yapılandırmalar için desteği hakkında daha fazla bilgi için bkz: [destek matrisi](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>VMware Vm'lerini veya fiziksel Windows veya Linux sunucuları tooAzure olağanüstü durum kurtarma
Merhaba bileşenleri aşağıdaki VMware Vm'lerini veya fiziksel Windows veya Linux sunucularının olağanüstü durum kurtarma için gerekli değildir. Ayrıca olanları açıklanan toohello bunlar [Azure gereksinimleri](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Yapılandırma sunucusu veya ek işlem sunucusu

Bir şirket içi makineyi hello yapılandırma sunucusu tooorchestrate hello şirket içi site ile Azure arasındaki iletişimi olarak ayarlayın. Merhaba şirket içi makineyi veri çoğaltma da yönetir. <br/></br>

*   **VMware vCenter veya vSphere ana bilgisayar önkoşulları**

    | **Bileşen** | **Gereksinimleri** |
    | --- | --- |
    | **vSphere** | Bir veya daha fazla VMware vSphere hiper olması gerekir.<br/><br/>Hiper yöneticilerin vSphere sürüm 6.0, 5.5 veya 5.1, en son güncelleştirmeleri hello çalıştırması gerekir.<br/><br/>VSphere ana bilgisayarları ve her ikisi de hello vCenter sunucuları aynı hello işlem sunucusu olarak ağ öneririz. Adanmış işlem sunucusu ayarlamadıysanız ayarladınız sürece bu hello yapılandırma sunucusunun bulunduğu hello ağdır. |
    | **vCenter** | Bir VMware vCenter server toomanage vSphere ana bilgisayarlarınız dağıtmanızı öneririz. VCenter sürüm 6.0 veya 5.5 hello en son güncelleştirmeleri ile çalışmalıdır.<br/><br/>**Sınırlama**: Site Recovery vCenter VMotion'ı örnekleri arasında çoğaltmayı desteklemez. Ayrıca bir ana hedef VM, depolama DRS ve depolama VMotion'ı, sonra yeniden koruma işlemi desteklenmez.||

* **Çoğaltılmış makine önkoşulları**

    | **Bileşen** | **Gereksinimleri** |
    | --- | --- |
    | **Şirket içi makineler** (VMware VM) | Çoğaltılan VM'ler VMware araçları yüklü ve çalışıyor olması gerekir.<br/><br/> Sanal makineleri karşılamalıdır [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) bir Azure VM oluşturmak için.<br/><br/>Disk kapasitesi, korunan her makinede 1,023 GB'den fazla olamaz. <br/><br/>Bir en az 2 GB kullanılabilir alan hello yükleme sürücüsünde bileşen yüklemesi için gereklidir.<br/><br/>Tooenable çoklu VM tutarlılığını istiyorsanız, bağlantı noktası 20004 hello VM Yerel Güvenlik Duvarı'nı açık olması gerekir.<br/><br/>Makine adlarının (harf, rakam ve kısa çizgi kullanabilirsiniz) 1 ile 63 karakter uzunluğunda olması gerekir. Hello ad bir harf veya sayı ile başlamalı ve bir harf veya sayı ile bitmelidir. <br/><br/>Makine için çoğaltmayı etkinleştirdikten sonra hello Azure adı değiştirebilirsiniz.<br/><br/> |
    | **Windows makine** (fiziksel veya VMware) | Merhaba makine desteklenen hello aşağıdakilerden birini çalıştırması gerekir 64-bit işletim sistemleri: <br/>-Windows Server 2012 R2<br/>-Windows Server 2012<br/>-Windows Server 2008 R2 SP1 veya sonraki bir sürümü<br/><br/> Merhaba işletim sistemi olmalıdır sürücüsüdür hello işletim sistemi disk üzerinde yüklü bir Windows temel disk olması gerekir ve dinamik değil. Merhaba veri diski dinamik olabilir.<br/><br/>|
    | **Linux makineler** (fiziksel veya VMware) | Merhaba makine desteklenen hello aşağıdakilerden birini çalıştırması gerekir 64-bit işletim sistemleri: <br/>-Red Hat Enterprise Linux 7.2, 7.1, 6,8 veya 6.7<br/>-Centos 7.2, 7.1, 7.0, 6,8, 6.7, 6.6 veya 6.5<br/>-Ubuntu 14.04 LTS sunucu (Ubuntu için desteklenen çekirdek sürümlerinin listesi için bkz: [desteklenen işletim sistemleri](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Oracle Enterprise ya da hello kırmızı çalıştırılan Linux 6.5 veya 6.4, Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3)<br/>-SUSE Linux Enterprise Server 11 SP4 veya SUSE Linux Enterprise Server 11 SP3<br/><br/>/ Etc/hosts dosyalarınızı korumalı makinelerdeki tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin girişleri olması gerekir.<br/><br/>Tooconnect tooan bir güvenli Kabuk (SSH) istemcisi kullanarak Linux çalıştıran bir Azure VM istiyorsanız, yük devretme sonrasında korunan hello makinedeki hello SSH hizmeti toostart otomatik olarak sistem başlangıç ayarlandığından emin olun. Ayrıca güvenlik duvarı kuralları bir SSH bağlantısı korumalı toohello makine izin verdiğinden emin olun.<br/><br/>Merhaba ana bilgisayar adı, bağlama noktaları, aygıt adları ve Linux sistem yolu ve dosya adları (örneğin, /etc/ ve/usr) İngilizce yalnızca olmalıdır.<br/><br/>Merhaba dizinleri (varsa ayrı bölüm olarak ayarlayın veya dosya sistemleri) tüm hello üzerinde olmalıdır hello kaynak sunucudaki aynı diski (Merhaba işletim sistemi diski):<br/>- / (root)<br/>- / önyükleme<br/>-/ usr<br/>-/ usr/yerel<br/>-/var<br/>- / vb.<br/><br/>Şu anda, meta veri sağlama gibi XFS v5 özellikleri XFS dosya sistemlerinde Site Recovery tarafından desteklenmez. XFS dosya sistemleri v5 özellikleri kullanmadığınız emin olun. Merhaba xfs_info yardımcı programı toocheck hello XFS Süper blok kullanarak hello bölüm için kullanabilirsiniz. Varsa **ftype** çok ayarlanır**1**, XFS v5 özellikleri kullanılmaktadır.<br/><br/>Red Hat Enterprise Linux 7 ve CentOS 7 sunucularda hello lsof yardımcı programı yüklü ve kullanılabilir olmalıdır.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Olağanüstü durum kurtarma Hyper-V sanal makineleri tooAzure (VMM yok)

Aşağıdaki bileşenleri hello VMM bulutlarındaki Hyper-V sanal makineleri, olağanüstü durum kurtarma için gerekli değildir. Ayrıca olanları açıklanan toohello bunlar [Azure gereksinimleri](#azure-requirements).

| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Hyper-V konağı** |Bir veya daha fazla şirket içi sunucular Windows Server 2012 R2 hello en son güncelleştirmeleri ve hello Hyper-V rolü etkin veya Microsoft Hyper-V Server 2012 R2 çalıştırması gerekir.<br/><br/>Hyper-V sunucuları, bir veya daha fazla VM olması gerekir.<br/><br/>Hyper-V sunucularının, doğrudan veya bir proxy üzerinden bağlı toohello Internet olması gerekir.<br/><br/>Hyper-V sunucuları hello Bilgi Bankası makalesinde açıklanan hello düzeltmeler olmalıdır [2961977](https://support.microsoft.com/kb/2961977) yüklü.
|**Sağlayıcı ve aracı**| Site Recovery dağıtımı sırasında hello Azure Site Recovery sağlayıcısını yükleyin. Merhaba sağlayıcısı yükleme de hello Azure kurtarma Hizmetleri aracısını yükler VM'ler çalıştıran her Hyper-V sunucusuna tooprotect istiyor. <br/><br/>Bir Site kurtarma kasası olmalıdır tüm Hyper-V sunucuları hello hello sağlayıcısı ve hello aracı aynı sürümleri.<br/><br/>Merhaba sağlayıcısının hello Internet üzerinden tooconnect tooSite kurtarma gerekir. Trafik, doğrudan veya bir proxy üzerinden gönderilebilir. HTTPS tabanlı proxy desteklenmiyor. Merhaba proxy sunucusu aşağıdaki URL'lere erişim toohello izin vermeniz gerekir:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>IP adresi tabanlı güvenlik duvarı kuralları hello sunucuda varsa, hello kuralları iletişim tooAzure izin verdiğinden emin olun.<br/><br/> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)hem de HTTPS (443 numaralı bağlantı noktası).<br/><br/> IP adres aralıklarını hello (erişim denetimi ve kimlik yönetimi için kullanılan) Batı ABD ve hello aboneliğinizin Azure bölgesi için izin verir.


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>VMM Bulutları tooAzure Hyper-V sanal makineleri, olağanüstü durum kurtarma

Aşağıdaki bileşenleri hello VMM bulutlarındaki Hyper-V sanal makineleri, olağanüstü durum kurtarma için gerekli değildir. Ayrıca olanları açıklanan toohello bunlar [Azure gereksinimleri](#azure-requirements).

| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Sanal Makine Yöneticisi** |System Center 2012 R2 veya sonraki bir sürümünü çalıştıran bir veya daha fazla VMM sunucusu olmalıdır. Her bir VMM sunucusunun bir veya daha fazla bulut yapılandırılmış olması gerekir. <br/><br/>Bir buluta sahip olmanız gerekir:<br/>-Bir veya daha fazla VMM ana bilgisayar grubu.<br/>-Bir veya daha fazla Hyper-V ana bilgisayar sunucuları veya kümeleri her konak grubundaki.<br/><br/>VMM bulutlarını ayarlama hakkında daha fazla bilgi için bkz: [nasıl toocreate bir bulutta Sanal Makine Yöneticisi 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Hyper-V ana bilgisayar sunucularının en az çalıştırmalıdır hello Hyper-V rolü etkin ya da Microsoft Hyper-V Server 2012 R2 ile Windows Server 2012 R2. Merhaba en son güncelleştirmelerin yüklü olmalıdır.<br/><br/> Bir Hyper-V sunucusu bir veya daha fazla VM olması gerekir.<br/><br/> Bir Hyper-V konak sunucusu veya tooreplicate istediğiniz Vm'leri içeren küme bir VMM bulutunda yönetilmesi gerekir.<br/><br/>Hyper-V sunucularının, doğrudan veya bir proxy üzerinden bağlı toohello Internet olması gerekir.<br/><br/>Hyper-V sunucuları hello Bilgi Bankası makalesinde açıklanan hello düzeltmeler olmalıdır [2961977](https://support.microsoft.com/kb/2961977) yüklü.<br/><br/>Hyper-V ana bilgisayar sunucuları veri çoğaltma tooAzure için Internet erişimi gerekir. |
| **Sağlayıcı ve aracı** |Azure Site Recovery dağıtımı sırasında Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin. Kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin. Merhaba sağlayıcı ve aracı tooconnect tooAzure hello Internet üzerinden doğrudan veya bir proxy üzerinden gerekir. HTTPS tabanlı ara sunucular desteklenmez. Merhaba VMM sunucusu ve Hyper-V konakları Hello proxy sunucusuna erişimi izni vermelidir: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Merhaba VMM sunucusunda IP adresi tabanlı güvenlik duvarı kuralları varsa hello kuralları iletişim tooAzure izin verdiğinden emin olun.<br/><br/> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve HTTPS (443 numaralı bağlantı noktası).<br/><br/>IP adresi aralıklarını hello Azure bölgesi (erişim denetimi ve kimlik yönetimi için kullanılan) hello Batı ABD ve aboneliğiniz için izin verir.<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Çoğaltılmış makine önkoşulları

| **Bileşen** | **Ayrıntılar** |
| --- | --- |
| **Korumalı VM'ler** | Site Recovery tarafından desteklenen tüm işletim sistemlerini destekliyor [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Sanal makineleri hello karşılamalıdır [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) bir Azure VM oluşturmak için. Makine adlarının (harf, rakam ve kısa çizgi kullanabilirsiniz) 1 ile 63 karakter uzunluğunda olması gerekir. Hello ad bir harf veya sayı ile başlamalı ve bir harf veya sayı ile bitmelidir. <br/><br/>Çoğaltma hello VM için etkinleştirdikten sonra hello VM adını değiştirebilirsiniz. <br/><br/> Korunan her makine için disk kapasiteleri 1,023 GB'den fazla olamaz. Bir VM yukarı too16 diskleri (yukarı too16 TB) olabilir.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Müşteri ait VMM Bulutları tooa sitedeki Hyper-V Vm'lerini olağanüstü durum kurtarma

Aşağıdaki bileşenleri hello müşteri ait VMM Bulutları tooa sitedeki Hyper-V Vm'lerini olağanüstü durum kurtarması için gereklidir. Ayrıca olanları açıklanan toohello bunlar [Azure gereksinimleri](#azure-requirements).

| **Bileşen** | **Ayrıntılar** |
| --- | --- |
| **Sanal Makine Yöneticisi** |  Merhaba birincil site ve hello ikincil sitenin VMM sunucusunda dağıtmanızı öneririz.<br/><br/> Yapabilecekleriniz [tek bir VMM sunucusundaki Bulutlar arasında çoğaltma](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate tek bir VMM sunucusundaki Bulutlar arasında hello VMM sunucusunda yapılandırılmış en az iki bulut gerekir.<br/><br/> VMM sunucusu en az çalıştırmalıdır hello en son güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/> Her bir VMM sunucusunun bir veya daha fazla bulut olması gerekir. Tüm bulutlar Hyper-V Kapasite profili kümesi hello olması gerekir. <br/><br/>Bulut bir veya daha fazla VMM konak grubu olması gerekir. VMM bulutlarını ayarlama hakkında daha fazla bilgi için bkz: [hazırlamak için Azure Site Recovery dağıtımı](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 ile Merhaba Hyper-V rolü etkin ve hello son güncelleştirmelerin yüklü olması.<br/><br/> Bir Hyper-V sunucusu bir veya daha fazla VM olması gerekir.<br/><br/>  Hyper-V ana bilgisayar sunucuları konak grupları hello birincil ve ikincil VMM bulutlarında yer almalıdır.<br/><br/> Windows Server 2012 R2'de bir kümede Hyper-V çalıştırırsanız, Bilgi Bankası makalesinde açıklanan hello güncelleştirmesini yüklemenizi öneririz [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Windows Server 2012'de bir kümede Hyper-V çalıştıran ve bir statik IP adresi tabanlı küme varsa, küme Aracısı otomatik olarak oluşturulmaz. Merhaba küme Aracısı el ile yapılandırmanız gerekir. Merhaba küme Aracısı hakkında daha fazla bilgi için bkz: [yapılandırma hello çoğaltma aracısı rolünün kümeden kümeye çoğaltma için](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Sağlayıcı** | Site Recovery dağıtımı sırasında VMM sunucularına hello Azure Site Recovery sağlayıcısını yükleyin. Merhaba sağlayıcı HTTPS (443 numaralı) tooorchestrate çoğaltma Site Recovery ile iletişim kurar. Veri çoğaltma hello birincil ve ikincil Hyper-V sunucuları arasında hello LAN üzerinden veya bir VPN bağlantısı üzerinden gerçekleşir.<br/><br/> Merhaba VMM sunucusunda çalışan hello sağlayıcısı toohello aşağıdaki URL'lere erişim:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Merhaba Site kurtarma sağlayıcısı hello VMM sunucuları toohello gelen güvenlik duvarı iletişimi izin vermelidir [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (bağlantı noktası 443) protokolüne izin verin. |


## <a name="url-access"></a>URL erişimi
Bu URL'leri VMware, VMM ve Hyper-V ana bilgisayar sunucuları kullanılabilir olmalıdır:

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **Hyper-V tooAzure** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | İzin Ver | İzin Ver | İzin Ver | İzin Ver |
|``*.backup.windowsazure.com`` | Gerekli değil | İzin Ver | İzin Ver | İzin Ver |
|``*.hypervrecoverymanager.windowsazure.com`` | İzin Ver | İzin Ver | İzin Ver | İzin Ver |
|``*.store.core.windows.net`` | İzin Ver | İzin Ver | İzin Ver | İzin Ver |
|``*.blob.core.windows.net`` | Gerekli değil | İzin Ver | İzin Ver | İzin Ver |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Gerekli değil | Gerekli değil | Gerekli değil | SQL indirme için izin ver |
|``time.windows.com`` | İzin Ver | İzin Ver | İzin Ver | İzin Ver|
|``time.nist.gov`` | İzin Ver | İzin Ver | İzin Ver | İzin Ver |
