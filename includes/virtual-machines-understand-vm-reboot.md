Azure sanal makineleri (VM'ler) bazen yok, hello yeniden başlatma işlemi başlatılan, kanıt olmadan belirgin bir nedenle yeniden başlatılması. Bu makalede hello eylemleri ve VM'ler tooreboot neden olabilir ve nasıl tooavoid beklenmeyen sorunları yeniden başlatın veya bu tür sorunları hello etkisini azaltmak Insight sağlayan olayları listelenmektedir.

## <a name="configure-hello-vms-for-high-availability"></a>Merhaba VM'ler yüksek kullanılabilirlik için yapılandırma
Merhaba en iyi şekilde tooprotect bir VM'ye karşı Azure üzerinde çalışan bir uygulama yeniden başlatıldıktan ve kapalı kalma süresi yüksek kullanılabilirlik için tooconfigure hello VM'ler.

tooprovide artıklık tooyour uygulamasının bu düzey, bir kullanılabilirlik kümesinde iki veya daha fazla VM Grup öneririz. Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir VM kullanılabilir karşılıyor hello 99,95 yüzde olmasını sağlar ve [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Kullanılabilirlik kümeleri hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Sanal makineleri Hello kullanılabilirliğini yönetme](../articles/virtual-machines/windows/manage-availability.md)
- [Sanal makineleri kullanılabilirliği yapılandırma](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Kaynak sistem durumu bilgileri 
Azure kaynak durumu hello Azure kaynakların durumunu gösterir ve sorun giderme tıklatılabilir ilişkin yönergeler sağlar bir hizmettir. Burada olası toodirectly erişim sunucularını veya altyapı öğeleri değil, bir bulut ortamında hello kaynak durumu sorunlarını gidermeyle ilgili harcadığınız tooreduce hello zaman hedefidir. Özellikle, hello AIM hello kök hello sorununun Merhaba uygulaması veya bir olayı hello içinde Azure platformu arasındadır olup olmadığını belirleme harcadığı tooreduce hello saattir. Daha fazla bilgi için bkz: [anlayın ve kullanım kaynak durumu](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Eylemleri ve hello VM tooreboot neden olan olayları

### <a name="planned-maintenance"></a>Planlı bakım
Microsoft Azure güncelleştirmeleri Merhaba Dünya tooimprove hello güvenilirlik, performans ve güvenlik VM'ler altını çizen hello konak altyapısının arasında düzenli olarak gerçekleştirir. Bellek koruma güncelleştirmeleri dahil olmak üzere bu güncelleştirmeler, birçoğu, sanal makineleri üzerinde hiçbir etkisi olmadan gerçekleştirilen veya Bulut Hizmetleri.

Ancak, bazı güncelleştirmeler yeniden başlatma gerektirir. Böyle durumlarda, hello VM'ler biz hello altyapı düzeltme eki, hello VM'ler durdurulup yeniden başlatılırken kapatılır.

toounderstand hangi Azure planlanan Bakım ve Linux Vm'lerinizi hello kullanılabilirliğini nasıl etkileyebileceğini burada listelenen hello makalelere bakın. Merhaba makaleler hello Azure planlı bakım işlemi hakkında arka plan ve nasıl tooschedule bakım toofurther planlanan hello etkisini azaltmak sağlar.

- [Azure VM'ler için planlı bakım](../articles/virtual-machines/windows/planned-maintenance.md)
- [Tooschedule nasıl planlı Azure Vm'lerinde İleri bakım](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Bellek koruma güncelleştirmeleri   
Microsoft Azure güncelleştirmelerinde Bu sınıf için kullanıcılar çalışan Vm'leri üzerinde hiçbir etkisi yaşar. Çoğu, aşağıdaki güncelleştirmelerden toocomponents veya örneğini çalıştıran hello ile engellemeden güncelleştirilebilir Hizmetleri bulunur. Merhaba VM'ler başlatmadan uygulanabilir hello ana bilgisayar işletim sistemi platformu altyapı güncelleştirmeleri bazılarıdır.

Bu bellek koruma güncelleştirmeleri yerinde dinamik geçiş olanağını sunar teknolojisi ile yapılır. Güncelleştirilmekte zaman hello VM yerleştirilen bir *duraklatıldı* durumu. Bu durum Hello altta yatan ana bilgisayar işletim sistemi hello gerekli güncelleştirmeleri ve düzeltme eklerini alırken RAM hello bellekte korur. Merhaba VM duraklatıldıktan sonra 30 saniye içinde devam ettirilir. VM sürdürüldü hello sonra kendi saati otomatik olarak eşitlenir.

Merhaba kısa duraklatma süresi nedeniyle, bu mekanizma büyük ölçüde güncelleştirmeleri dağıtmak hello VM'ler hello etkisini azaltır. Ancak, güncelleştirmelerinin tümü yok, bu şekilde dağıtılabilir. 

Çok örnekli (bir kullanılabilirlik kümesinde VM'ler için) uygulanan bir güncelleştirme etki alanı aynı anda güncelleştirmelerdir.

> [!NOTE]
> Eski çekirdek sürümlerde Linux makineler, bu güncelleştirme yöntemi sırasında çekirdek Panik tarafından etkilenir. tooavoid Bu sorun, güncelleştirme tookernel sürüm 3.10.0-327.10.1 veya sonraki bir sürümü. Daha fazla bilgi için bkz: [3.10 tabanlı çekirdek bir Azure Linux VM'de panics bir ana bilgisayar düğümü yükseltmeden sonra](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Kullanıcı tarafından başlatılan yeniden başlatma veya kapatma Eylemler
 
Hello Azure portal, Azure PowerShell, komut satırı arabirimi ya da sıfırlama API yeniden başlatma işlemi gerçekleştirirseniz, hello olay hello bulabilirsiniz [Azure etkinlik günlüğü](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Merhaba VM'in işletim sisteminden hello eylem gerçekleştirirseniz hello sistem günlüklerine hello olay bulabilirsiniz.

Genellikle hello VM tooreboot neden diğer senaryolar birden fazla yapılandırma değişikliği eylemleri içerir. Normalde, belirli bir eylemi yürütürken belirten bir uyarı iletisi hello VM bir yeniden başlatma sonuçlanır görürsünüz. Örnekler hello hello yönetici hesabının parolasını değiştirme ve bir statik IP adresi ayarı VM yeniden boyutlandırma işlemleri içerir.

### <a name="azure-security-center-and-windows-update"></a>Azure Güvenlik Merkezi ve Windows Update
Azure Güvenlik Merkezi, işletim sistemi güncelleştirmeleri eksik günlük Windows ve Linux VM'ler izler. Güvenlik Merkezi hizmeti bağlı olarak bir Windows VM üzerinde yapılandırıldığı Windows Update veya Windows Server Update Services (WSUS) kullanılabilir güvenlik ve kritik güncelleştirmeler listesini alır. Güvenlik Merkezi ayrıca Linux sistemlerine hello en son güncelleştirmeleri denetler. VM'yi bir sistem güncelleştirmesi eksikse, Güvenlik Merkezi sistem güncelleştirmeleri uygulamanızı önerir. Bu sistem güncelleştirmeleri Merhaba uygulaması hello Güvenlik Merkezi hello Azure portal aracılığıyla denetlenir. Bazı güncelleştirmeler uygulandıktan sonra VM yeniden başlatma gerekli olabilir. Daha fazla bilgi için bkz: [Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulamak](../articles/security-center/security-center-apply-system-updates.md).

Bu makineler, kullanıcılar tarafından yönetilen hedeflenen toobe olduğundan gibi şirket içi sunucular, Azure güncelleştirmeleri Windows Update tooWindows Azure VM'ler, göndermez. Ancak, etkin tooleave hello otomatik Windows Update ayarını teşvik. Merhaba güncelleştirmeleri uygulandıktan sonra Windows Update'ten güncelleştirmeleri otomatik olarak yüklenmesini de yeniden başlatmalar toooccur neden olabilir. Daha fazla bilgi için bkz: [Windows Update SSS](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Merhaba, VM kullanılabilirliğini etkileyen diğer durumlar
Hangi Azure etkin olarak bir VM hello kullanımını askıya diğer durumlar vardır. Bu eylem önce temel sorunları hello fırsat tooresolve gerekir böylece e-posta bildirimi alırsınız. Güvenlik ihlalleri ve ödeme yöntemleri hello sona erme tarihi VM kullanılabilirliği etkileyen sorunlar örneklerindendir.

### <a name="host-server-faults"></a>Ana bilgisayar sunucu hataları 
Merhaba VM, Azure veri merkezi içinde çalıştıran fiziksel bir sunucuda barındırılır. Merhaba fiziksel sunucu çalıştığında aracı bir toplama tooa hello konak Aracısı birkaç Azure bileşenlerle çağrılır. Bu Azure yazılım bileşenleri hello fiziksel sunucuda yanıt veremez duruma geldiğinde sistem izleme hello hello ana bilgisayar sunucu tooattempt kurtarma yeniden tetikler. Merhaba VM beş dakika içinde yeniden genellikle kullanılabilir ve daha önce aynı ana bilgisayar hello üzerinde toolive devam eder.

Sunucu hatalarının genellikle hello başarısızlığını bir sabit disk veya katı hal sürücüsü gibi donanım hatası nedeniyle oluşur. Azure sürekli olarak bu örnekleri izler, hello temel alınan hataları tanımlar ve hello azaltma uygulanan ve test sonra güncelleştirmeleri yapar.

Bazı ana bilgisayar sunucu hatalarının belirli toothat sunucu olabileceğinden, yinelenen bir VM yeniden başlatma durumu hello VM tooanother ana bilgisayar sunucusuna el ile taşıyacak yeniden dağıtma işlemiyle geliştirilmiş. Bu işlem hello kullanarak tetiklenebilir **dağıtmanız** seçeneği'hello VM hello Ayrıntıları sayfasında ya da durdurup yeniden başlatarak VM hello Azure portal hello.

### <a name="auto-recovery"></a>Otomatik Kurtarma
Merhaba ana bilgisayar sunucusu için herhangi bir nedenle yeniden olamaz, hello Azure platformu bir otomatik kurtarma eylemi tootake hello hatalı ana bilgisayar sunucusunda daha fazla araştırma için döndürme dışında başlatır. 

Bu konaktaki tüm sanal makineleri otomatik olarak yeniden tooa farklı, sağlıklı bir ana sunucuyu belirtir. Bu işlem 15 dakika içinde genellikle tamamlanır. toolearn hello otomatik kurtarma işlemi hakkında daha fazla bilgi görmek [otomatik kurtarma VM'lerin](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Plansız bakım
Nadir durumlarda, tooperform bakım etkinlikleri tooensure hello Azure platformu genel durumunu hello Azure işlemleri takım hello. Bu davranış VM kullanılabilirliğini etkileyebilir ve bu genellikle hello aynı sonuçları daha önce açıklandığı gibi otomatik kurtarma eylemi.  

Planlanmamış maintenances hello şunları içerir:

- Acil düğümü birleştirme
- Acil ağ anahtarı güncelleştirmeleri

### <a name="vm-crashes"></a>VM çökme (Crash)
Sanal makineleri hello VM kendisini içinde sorunları nedeniyle yeniden başlatılabilir. Merhaba iş yükü veya VM hello üzerinde çalışan rolü hello konuk işletim sistemi içinde bir hata denetimi tetikleyebilir. Hello kilitlenme hello nedeni belirleme konusunda yardım için Windows VM'ler için hello sistem ve uygulama günlüklerini görüntülemek ve Linux VM'ler için seri günlükleri hello.

### <a name="storage-related-forced-shutdowns"></a>Depolama ilgili zorla kapatma
Azure'da Vm'leri sanal diskler işletim sistemi ve hello Azure depolama altyapısını barındırılan veri depolama için kullanır. Merhaba kullanılabilirlik veya hello VM ile ilişkili hello sanal diskler arasında bağlantı 120 saniyeden fazla bir süre için etkilenen her hello Azure platformu hello VM'ler tooavoid veri bozulması zorunlu bir kapatma gerçekleştirir. Depolama bağlantı geri yüklendikten sonra hello sanal makineleri otomatik olarak geri güç sağlar. 

Merhaba kapatma Hello süresi beş dakikadan kısa olabilir ancak önemli ölçüde uzun olabilir. Merhaba aşağıdaki depolama ilgili zorla kapatma ile ilişkili hello belirli durumlarda biridir: 

**G/ç aşan sınırlar**

Merhaba birimi (IOPS) saniye başına g/ç işlemlerinin hello disk için hello g/ç sınırları aştığından g/ç istekleri tutarlı bir şekilde kısıtlanan VM'ler geçici olarak kapatıldığında. (Standart disk depolama sınırlıdır too500 IOPS.) toomitigate Bu sorun, disk şeritleme kullanın veya hello depolama alanı hello iş yüküne bağlı olarak hello Konuk VM içinde yapılandırın. Ayrıntılar için bkz [yapılandırma Azure VM'ler için en iyi depolama performansı](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Daha yüksek IOPS sınırları too80, 000 IOPS Azure Premium Storage ile aracılığıyla kullanılabilir. Daha fazla bilgi için bkz: [yüksek performanslı Premium depolama](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Diğer olaylar
Nadir durumlarda, Azure veri merkezinde birden çok sunucuya yaygın sorun etkileyebilir. Bu sorun oluşursa hello Azure ekibi e-posta bildirimleri toohello etkilenen abonelikler gönderir. Merhaba denetleyebilirsiniz [Azure hizmet durumu Panosu](https://azure.microsoft.com/status/) ve devam eden kesintiler ve olaylar geçmiş hello durumunu için Azure portalı hello.
