---
title: aaaAzure Backup ile ilgili SSS | Microsoft Docs
description: "Hakkında toocommon soruları yanıtlar: Kurtarma Hizmetleri kasaları, ne da yedekleyebilirsiniz, nasıl çalıştığını, şifreleme ve sınırları dahil olmak üzere Azure yedekleme özellikleri. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "yedekleme ve olağanüstü durum kurtarma; backup hizmeti"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Hello Azure Backup hizmeti hakkında sorular
Bu makalede yanıtlar toocommon sorular toohelp hızlı bir şekilde hello Azure Backup bileşenlerini anlama sahiptir. Bazı hello yanıtlar kapsamlı bilgiler bağlantılar toohello makaleler vardır. Tıklayarak Azure yedekleme hakkında sorular sorabilirsiniz **açıklamaları** (toohello sağ). Açıklamalar, bu makalenin hello alt kısmında görüntülenir. Gerekli toocomment Livefyre hesabıdır. Hello Azure Backup hizmeti hakkında sorular hello nakledebilirsiniz [tartışma Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly tarama hello bu makalede, bölümlere hello bağlantılar toohello sağ altında **bu makalede**.


## <a name="recovery-services-vault"></a>Kurtarma hizmetleri kasası

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Her Azure aboneliğinizde oluşturduğunuz kasalarını hello sayısına bir sınır var mıdır? <br/>
Evet. Eylül 2016’dan itibaren abonelik başına 25 Kurtarma Hizmeti veya yedekleme kasası oluşturabilirsiniz. Too25 kurtarma Hizmetleri kasaları her desteklenen Azure Yedekleme'nin Abonelikteki bölge başına oluşturabilirsiniz. Daha fazla kasaya ihtiyacınız varsa başka bir abonelik oluşturun.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Her kasa için kaydedilebilen kayıtlı sunucuları/makineler hello sayısına bir sınır var mıdır? <br/>
Evet, kasa başına too50 makine kaydedebilirsiniz. Azure Iaas sanal makineler için hello kasa başına 200 VM sınırıdır. Daha fazla makine tooregister ihtiyacınız varsa, başka bir kasa oluşturun.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Kuruluşumun bir kasası varsa veri geri yükleme sırasında bir sunucunun verilerini başka bir sunucudan nasıl ayırabilirim?<br/>
Aynı kasaya kurtarabilirsiniz kayıtlı toohello olan tüm sunucuları hello diğer sunucular tarafından yedeklenen verileri *kullanan hello aynı parolayı*. Tooisolate istediğiniz yedekleme verilerini sunucularınız varsa, kuruluşunuzdaki diğer sunucularından bu sunucular için belirlenmiş bir parola kullanın. Örneğin, insan kaynakları sunucuları bir şifreleme parolası kullanırken, muhasebe sunucuları ve depolama sunucuları farklı birer şifreleme parolası kullanabilir.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Yedekleme verilerimin veya kasamın abonelikler arasında "geçişini" sağlayabilir miyim? <br/>
Hayır. Merhaba kasa abonelik düzeyinde oluşturulur ve oluşturulduktan sonra yeniden atanan tooanother abonelik olamaz.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Kurtarma Hizmetleri kasaları Resource Manager tabanlıdır. Backup kasaları (Klasik mod) hala destekleniyor mu? <br/>
Merhaba tüm yedekleme kasalarında [Klasik portal](https://manage.windowsazure.com) desteklenen toobe devam edin. Bununla birlikte, artık hello Klasik portal toodeploy yeni yedekleme kasaları kullanabilirsiniz. Microsoft, gelecekteki geliştirmeleri tooRecovery Hizmetleri kasalarının, yalnızca geçerli olduğundan kurtarma Hizmetleri kasaları tüm dağıtımlar için kullanılmasını önerir. Toocreate hello Klasik Portalı'nda bir yedekleme kasası çalışırsanız, yeniden yönlendirilen toohello olacaktır [Azure portal](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Bir yedekleme kasası tooa kurtarma Hizmetleri kasasına geçişini sağlayabilir miyim? <br/>
Ne yazık ki Hayır, Kurtarma Hizmetleri kasası bir yedekleme kasası tooa Merhaba içeriğine geçişi yapamazsınız. Bu işlevi eklemeye yönelik çalışmalarımız devam ediyor ancak işlev şu anda kullanılamıyor.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Klasik VM’lerimi bir Backup kasasına yedekledim. Miyim Vm'lerimin Klasik modda tooResource Yöneticisi modundan geçirmek ve bir kurtarma Hizmetleri kasasına koruyun?
Klasik tooResource Yöneticisi modu hello VM taşıdığınızda bir yedekleme kasası Klasik VM kurtarma noktalarını otomatik olarak tooa kurtarma Hizmetleri kasası geçirme. Bu adımları tootransfer VM Yedeklemelerinizin izleyin:

1. Toohello Hello yedekleme kasasına gidin **korunan öğeler** sekmesinde ve hello VM seçin. [Korumayı Durdur](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)’a tıklayın. *İlişkili yedekleme verilerini sil* seçeneğini **işaretlenmemiş** olarak bırakın.
2. Merhaba yedekleme/anlık görüntü uzantısını VM hello silin.
3. Klasik mod tooResource Yöneticisi modundan Hello sanal makineyi geçirin. Karşılık gelen toohello sanal makine de hello depolama ve ağ bilgileri tooResource Yöneticisi modu geçirilen emin olun.
4. Kurtarma Hizmetleri kasası oluşturma ve yapılandırma hello üzerinde Yedekleme kullanarak sanal makine geçişi **yedekleme** kasa Panosu üzerinde eylem. Bir VM tooa kurtarma hizmetlerini yedekleme hakkında ayrıntılı bilgi için kasa, hello makalesine bakın [korumak Azure Vm'leri bir kurtarma Hizmetleri kasası ile](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Azure Backup aracısı
Soruların ayrıntılı listesini [Azure dosya-klasör yedekleme hakkında SSS](backup-azure-file-folder-backup-faq.md) altında bulabilirsiniz.

## <a name="azure-vm-backup"></a>Azure VM yedeklemesi
Soruların ayrıntılı listesini [Azure VM yedeklemesi hakkında SSS](backup-azure-vm-backup-faq.md) altında bulabilirsiniz.

## <a name="back-up-vmware-servers"></a>VMware sunucularını yedekleme

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>VMware vCenter sunucuları tooAzure geri yükleyebileceğiniz?

Evet. Azure yedekleme sunucusu tooback VMware vCenter ve ESXi tooAzure kullanabilirsiniz. Desteklenen hello VMware sürüm hakkında daha fazla bilgi için hello makalesine bakın [Azure yedekleme sunucusu koruma matris](backup-mabs-protection-matrix.md). Adım adım yönergeler için bkz: [bir VMware sunucusu kullanım Azure yedekleme sunucusu tooback](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup Sunucusu ve System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Azure yedekleme sunucusu toocreate tam kurtarma (BMR) yedekleme için bir fiziksel sunucuda kullanabilir miyim? <br/>
Evet.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>My DPM sunucusu toomultiple kasa kayıt mi? <br/>
Hayır. Bir DPM veya MABS sunucusu kayıtlı tooonly bir kasa olabilir.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>System Center Data Protection Manager’ın hangi sürümü desteklenir? <br/>
Merhaba yüklemenizi öneririz [son](http://aka.ms/azurebackup_agent) hello en son güncelleştirme paketi (UR) System Center Data Protection Manager (DPM) için Azure Backup aracısını. Ağustos 2016 itibariyle güncelleştirme toplaması 11 hello son güncelleştirmesidir.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Azure Yedekleme aracısı tooprotect dosya ve klasörlerimi yüklü. Artık Azure Yedekleme aracısı tooprotect şirket içi uygulama/VM iş yüklerini tooAzure ile System Center DPM toowork yükleyebilir miyim? <br/>
toouse Azure yedekleme ile System Center Data Protection Manager (DPM), DPM ilk yükleyin ve ardından Azure Yedekleme aracısı yükleyin. Bu sırada Hello Azure Backup bileşenleri yüklemeyi hello Azure Yedekleme aracısı DPM ile çalışmasını sağlar. DPM yüklemeden önce yükleme hello Azure Yedekleme aracısı önerilmez ve desteklenmez.


## <a name="how-azure-backup-works"></a>Azure Backup nasıl çalışır?
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Başlatıldıktan sonra bir yedekleme işi iptal ederseniz, hello aktarılan yedekleme verileri silinir mi? <br/>
Hayır. Merhaba yedekleme işi iptal edilmeden önce hello kasaya aktarılan tüm verilerin hello kasasına kalır. Bir denetim noktası mekanizması toooccasionally ekleme sırasında denetim noktaları toohello yedek verileri azure yedekleme kullanır yedekleme hello. Merhaba yedekleme verilerinde denetim noktaları bulunduğundan hello sonraki yedekleme işlemi hello hello dosyaların bütünlüğünü doğrulayabilir. önceden yedeklediğiniz artımlı toohello veri Hello sonraki yedekleme işi olacaktır. Artımlı yedeklemeler yalnızca bant genişliği kullanımını toobetter karşılık gelir, yeni veya değiştirilmiş veri aktarın.

Bir Azure VM’ye yönelik bir yedekleme işini iptal ederseniz aktarılan tüm veriler yoksayılır. Merhaba sonraki yedekleme işi hello son başarılı yedekleme işinden artımlı veri aktarır.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Bir yedekleme işinin ne zaman veya kaç kez zamanlanabileceğine yönelik sınırlar var mıdır?<br/>
Evet. Yedekleme işlerini Windows Server veya Windows iş istasyonları toothree kez günde yukarı çalıştırabilirsiniz. Tootwice günde bir yedekleme, yedekleme işlerini System Center DPM üzerinde çalıştırabilirsiniz. Bir yedekleme işini IaaS VM'ler için günde bir kez çalıştırabilirsiniz. Windows Server veya Windows iş istasyonu toospecify için zamanlama ilkesi hello kullanabilirsiniz günlük veya haftalık zamanlama. System Center DPM'yi kullanarak günlük, haftalık, aylık ve yıllık zamanlamalar belirtebilirsiniz.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Neden yedeklenen hello veri daha küçük kurtarma Hizmetleri kasası hello aktarılan verilerin toohello hello boyutunu mi?<br/>
 Azure Yedekleme aracısı veya SCDPM veya Azure yedekleme sunucusu, yedeklenen tüm hello verileri sıkıştırılmış ve aktarılmadan önce şifrelenir. Merhaba sıkıştırma ve şifreleme uygulandıktan sonra hello hello yedekleme kasasında % 30-40 daha küçük verilerdir.

## <a name="what-can-i-back-up"></a>Neleri yedekleyebilirim?
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Azure Backup hangi işletim sistemlerini destekler? <br/>
Azure yedekleme yedeklenmesi işletim sistemlerinin listesi aşağıdaki hello destekler: dosyaları ve klasörleri ve Azure yedekleme sunucusu ve System Center Data Protection Manager (DPM) kullanılarak korunan iş yükü uygulamaları.

| İşletim Sistemi | Platform | SKU |
|:--- | --- |:--- |
| Windows 8 ve en son SP'ler |64 bit |Enterprise, Pro |
| Windows 7 ve en son SP'ler |64 bit |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 ve en son SP'ler |64 bit |Enterprise, Pro |
| Windows 10 |64 bit |Enterprise, Pro, Home |
| Windows Server 2016 |64 bit |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 ve en son SP'ler |64 bit |Standard, Datacenter, Foundation |
| Windows Server 2012 ve en son SP'ler |64 bit |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 ve en son SP'ler |64 bit |Standard, Workgroup | 
| Windows Storage Server 2012 R2 ve en son SP'ler |64 bit |Standard, Workgroup |
| Windows Storage Server 2012 ve en son SP'ler |64 bit |Standard, Workgroup |
| Windows Server 2012 R2 ve en son SP'ler |64 bit |Essential |
| Windows Server 2008 R2 SP1 |64 bit |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bit |Standard, Enterprise, Datacenter, Foundation |

**Azure VM yedeklemesi için:**

* **Linux**: Azure Backup, [Azure tarafından onaylanan bir dağıtım listesini](../virtual-machines/linux/endorsed-distros.md) (CoreOS Linux hariç) destekler.  Diğer Getir-bilgisayarınızı-kendi-Linux dağıtımları da hello VM Aracısı hello sanal makinede kullanılabilir olduğu sürece çalışır ve Python var. desteği.
* **Windows Server**:  Windows Server 2008 R2’den eski sürümler desteklenmez.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Bir sınır hello boyutu yedeklenmekte olan her veri kaynağı üzerinde var mıdır? <br/>
Merhaba tooa kasasını yedekleyebilirsiniz veri miktarına bir sınır yoktur. Azure yedekleme hello hello veri kaynağı için en büyük boyutu sınırlar, ancak bu sınırları büyük. Ağustos 2015'ten itibaren hello desteklenen işletim sistemleri için bir veri kaynağı için maksimum boyut hello şöyledir:

| S.No | İşletim sistemi | En büyük veri kaynağı boyutu |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 veya üzeri |54.400 GB |
| 2 |Windows 8 veya üzeri |54.400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Aşağıdaki tablonun hello her veri kaynağı boyutunun nasıl belirlendiği açıklanmaktadır.

| Veri kaynağı | Ayrıntılar |
|:---:|:--- |
| Birim |Merhaba tek bir sunucu veya istemci makinenin biriminden yedeklenmekte olan verilerin miktarı |
| Hyper-V sanal makine |Tüm hello VHD hello sanal makinenin yedeklenmekte olan verilerin toplamı |
| Microsoft SQL Server veritabanı |Yedeklenmekte olan tek bir SQL veritabanının boyutu |
| Microsoft SharePoint |Yedeklenmekte olan bir SharePoint grubu içinde hello içerik ve yapılandırma veritabanlarının toplamı |
| Microsoft Exchange |Yedeklenmekte olan bir Exchange sunucusundaki tüm Exchange veritabanlarının toplamı |
| BMR/Sistem Durumu |BMR veya sistem durumu hello makinenin yedeklenmekte olan her ayrı kopyası |

Azure VM yedekleme için her bir VM her veri diski boyutu 1023 GB veya daha az olan ile too16 veri diskleri sahip olabilir. 

## <a name="retention-policy-and-recovery-points"></a>Bekletme ilkesi ve kurtarma noktaları
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Merhaba bekletme ilkesi DPM ve Windows Server/istemcisi arasında bir fark yoktur (diğer bir deyişle, üzerinde Windows Server DPM olmadan)?<br/>
Hayır, hem DPM hem de Windows Server/istemcisi günlük, haftalık, aylık ve yıllık bekletme ilkelerine sahiptir.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Bekletme ilkelerimi seçerek yapılandırabilir miyim? Başka bir deyişle, haftalık ve günlük yapılandırmaya olanak tanırken yıllık ve aylık yapılandırmayı engelleyebilir miyim?<br/>
Evet, hello Azure Backup bekletme yapısı gereksinimlerinizi hello bekletme ilkesini tanımlama toohave tam esneklik sağlar.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Saat 18:00 için “bir yedekleme zamanlayıp” farklı bir saat için de "bekletme ilkeleri" belirtebilir miyim?<br/>
Hayır. Bekletme ilkeleri, yalnızca yedekleme noktalarında uygulanabilir. Görüntü aşağıdaki hello hello bekletme ilkesi 00: 00 ve 6 pm alınan yedeklemeler için belirtilmiş. <br/>

![Yedekleme ve Bekletmeyi Zamanlama](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Yedekleme için uzun bir süre tutulursa daha fazla zaman toorecover eski bir veri noktasının sürer? <br/>
Hayır – toorecover eski hello veya yeni noktanın hello hello zaman olan hello aynı. Her kurtarma noktası bir tam nokta gibi davranır.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Her kurtarma noktası bir tam nokta gibi ise, hello toplam faturalanabilir yedekleme alanını etkiler mi?<br/>
Genel uzun vadeli bekletme noktası ürünleri, yedekleme verilerini tam noktalar olarak depolar. Merhaba tam noktalarıdır depolama *verimsiz* ancak daha kolay ve hızlı toorestore. Artımlı kopyalarıdır depolama *verimli* ancak toorestore kurtarma süresini etkileyecek veri zinciri gerektirir. En iyi şekilde hızlı geri yüklemeler için verilerin depolanması ve düşük depolama maliyetleri oluşturarak iki açıdan da hello azure yedekleme depolama mimarisi sağlar. Bu veri depolama yaklaşımı, giriş ve çıkış bant genişliğinizin verimli şekilde kullanılmasını sağlar. Hem hello süreyi veri depolama ve hello toorecover hello veri gerekli, tooa minimum tutulur. [Artımlı yedeklemenin](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/) ne kadar verimli olduğu hakkında daha fazla bilgi edinin.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Oluşturulabilecek kurtarma noktalarının hello sayısına bir sınır var mıdır?<br/>
Korumalı örneği başına too9999 kurtarma noktası oluşturabilirsiniz. Bir korumalı bir bilgisayar, sunucu (fiziksel veya sanal) veya yapılandırılmış iş yükü tooback veri tooAzure yukarı örneğidir. Merhaba açıklamalarını daha fazla bilgi için bkz: [yedekleme ve bekletme](./backup-introduction-to-azure-backup.md#backup-and-retention), ve [korumalı bir örneği nedir](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>TooAzure yedeklenen hello veriler üzerinde kaç kurtarma gerçekleştirebilir miyim?<br/>
Azure yedekleme kurtarma hello sayısı sınırı yoktur.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Verileri geri yüklerken ı Azure'dan hello çıkış trafiği için ödeme yaparım? <br/>
Hayır. Kurtarma işlemleriniz ücretsizdir ve hello çıkış trafiği için sizden ücret değil.

## <a name="azure-backup-encryption"></a>Azure Backup şifrelemesi
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Merhaba veri şifrelenir tooAzure gönderilir? <br/>
Evet. Veriler AES256 kullanılarak hello şirket içi sunucu/istemci/SCDPM makinede şifrelenir ve hello veriler güvenli bir HTTPS bağlantısı üzerinden gönderilir.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Merhaba yedekleme verileri de şifreli Azure üzerinde mi?<br/>
Evet. gönderilen Merhaba veri tooAzure (Bekleyen) şifreli olarak kalır. Microsoft hello herhangi bir noktada yedekleme verilerinin şifresini çözmez. Bir Azure VM'yi yedekleme konusunda, Azure Backup hello sanal makinenin şifrelemesini kullanır. Örneğin, Azure Backup, VM Azure Disk şifrelemesi veya başka bir şifreleme teknolojisi kullanılarak şifrelenir, verilerinizi bu şifreleme toosecure kullanır.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Merhaba şifreleme anahtarının minimum uzunluğu nedir tooencrypt yedekleme verilerini kullanılıyor? <br/>
Azure Yedekleme aracısı kullanırken hello şifreleme anahtarı en az 16 karakter olmalıdır. Azure VM'ler için hiçbir sınır toolength Azure KeyVault tarafından kullanılan anahtarların yoktur. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Merhaba şifreleme anahtarı misplace ne olur? Merhaba veri kurtarma yapabilirsiniz (veya) Microsoft hello verileri kurtarabilir mi? <br/>
Merhaba anahtar kullanılan tooencrypt hello yedekleme verileri yalnızca hello müşterinin şirketinde bulunur. Microsoft azure'da bir kopyasını tutmaz ve hiçbir erişim toohello anahtarı yok. Merhaba müşteri hello anahtarı kaybederse Microsoft hello yedekleme verilerini kurtaramaz.
