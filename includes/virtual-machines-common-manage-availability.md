## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>VM Yeniden Başlatma İşlemlerini Anlama - bakım ve kapalı kalma süresi
Toovirtual makine etkilenip Azure'da neden olabilecek üç senaryo vardır: planlanmamış donanım bakım, beklenmeyen kapalı kalma süresi ve planlı Bakım.

* **Planlanmamış donanım bakım olayı** hello Azure platformu tahmin hello donanım tüm platform bileşeni ilişkili tooa fiziksel makine mi hakkında toofail oluşur. Bir hata Hello platform tahmin, bir planlanmamış donanım bakım olayı tooreduce hello etkisi toohello bu donanım üzerinde barındırılan sanal makineleri gönderirsiniz. Azure donanım tooa sağlıklı fiziksel makine başarısız hello gelen dinamik geçiş teknolojisi toomigrate hello sanal makineler kullanır. Dinamik geçiş işlemi yalnızca duraklatır sanal makine kısa bir süre hello saklayan bir VM'dir. Bellek, açık dosyalar ve ağ bağlantıları korunur, ancak önce ve/veya hello olayından sonra performansı azalabilir. Dinamik geçiş burada kullanılamaz durumda aşağıda açıklandığı gibi hello VM beklenmeyen kapalı kalma süresi yaşar.


* **Beklenmeyen bir kapalı kalma süresi** hello donanım ya da sanal makineniz için temel alınan fiziksel altyapı hello herhangi bir yolla hatalı nadiren gerçekleşir. Buna yerel ağ hataları, yerel disk hataları veya raf düzeyinde diğer hatalar dahildir. Bu tür bir arıza tespit edildiğinde hello Azure platformu otomatik olarak geçirir (heals), sanal makine tooa sağlıklı fiziksel makine. Yordam iyileştirme hello sırasında sanal makineleri deneyimi kapalı kalma süresi (yeniden başlatma) ve bazı durumlarda kaybına hello geçici sürücü. işletim sistemi Hello bağlı ve veri diskleri her zaman korunur. 

* **Planlı bakım etkinliği** Azure platformu tooimprove temel Microsoft toohello tarafından yapılan düzenli güncelleştirmeler genel güvenilirliğini, performansını ve sanal makinelerinizi çalıştıracağınız hello platform altyapısına güvenliğini. Bu güncelleştirmelerin çoğu Sanal Makine veya Bulut Hizmetlerinizi etkilemeden gerçekleştirilir (bkz. [VM Koruyucu Bakım](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Hello Azure platformu toouse VM koruma bakım içinde tüm olası durumlar çalışır, ancak bazı ender bu güncelleştirmeler, sanal makine tooapply hello gerekli güncelleştirmeleri toohello temel altyapısının yeniden başlatılması gerekir. Bu durumda, kendi VM'ler hello uygun zaman penceresinde hello bakım başlatarak Azure planlı bakım ile bakım dağıtın işlemi gerçekleştirebilir. Daha fazla bilgi için bkz. [Sanal Makineler için Planlı Bakım](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


kapalı kalma süresi son tooone veya daha fazla bu olayları tooreduce hello etkisi, yüksek kullanılabilirlik, sanal makineleriniz için en iyi uygulamaları izleyerek hello öneririz:

* [Bir kullanılabilirlik kümesindeki birden fazla sanal makineyi yedeklilik için yapılandırma]
* [Bir kullanılabilirlik kümesindeki VM’ler için yönetilen diskleri kullanma]
* [Olayları etkileyen zamanlanmış olayları tooproactively yanıt tooVM kullanın] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Her uygulama katmanını ayrı kullanılabilirlik kümeleri halinde yapılandırma]
* [Yük Dengeleyiciyi kullanılabilirlik kümeleri ile birleştirme]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Bir kullanılabilirlik kümesindeki birden fazla sanal makineyi yedeklilik için yapılandırma
tooprovide artıklık tooyour uygulama, bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir karşılıyor hello %99,95 olmasını sağlar ve Azure SLA. Daha fazla bilgi için bkz: Merhaba [sanal makineler için SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Tek örnekli bir sanal makineyi bir kullanılabilirlik kümesinde tek başına bırakmaktan kaçının. Bu yapılandırmadaki sanal makineler SLA garantisine uygun değildir ve tek bir VM’nin [Azure Premium Depolama](../articles/storage/common/storage-premium-storage.md) kullandığı durumlar dışında planlı Azure bakım olayları sırasında kapalı kalma süresiyle karşılaşır. Premium depolama kullanan tek VM'ler için hello Azure SLA geçerlidir.

Her bir sanal makine kullanılabilirlik kümenizdeki atanmış bir **güncelleştirme etki alanı** ve **hata etki alanı** Azure platformu için temel alınan hello tarafından. Verilen kullanılabilirlik kümesi için varsayılan olarak beş kullanıcı yapılandırılabilir olmayan güncelleme etki alanına atanan (Resource Manager dağıtımları too20 güncelleştirme etki alanları artan tooprovide sonra de olabilir) sanal makinelerin ve temel alınan fiziksel donanım tooindicate grupları yeniden Merhaba aynı anda. Beşten fazla sanal makine bir tek kullanılabilirlik kümesi içinde yapılandırıldığında hello altıncı sanal makine aynı etki alanı hello ilk sanal makine hello seventh aynı ikinci sanal makine hello gibi ve böylece etki alanı güncelleştirme hello güncelleştirme hello yerleştirilir . Merhaba sırasını güncelleştirme etki alanlarını yeniden başlatıldığı sırayla planlı bakım sırasında ilerleyebilirsiniz değil, ancak yalnızca tek bir güncelleştirme etki alanı, aynı anda yeniden başlatılıncaya kadar. Farklı güncelleştirme etki alanı üzerinde bakım başlatılmadan önce yeniden başlatılan güncelleştirme etki alanı 30 dakika toorecover verilir.

Hata etki alanları, sanal makinelerin, ortak bir güç kaynağı ve ağ anahtarı paylaşmak hello grubunu tanımlayın. Varsayılan olarak, kullanılabilirlik kümesi içinde yapılandırılmış hello sanal makineler arasında toothree hata etki alanları (iki etki alanları için Klasik arıza) Resource Manager dağıtımları için ayrılır. Sanal makinelerinizi bir kullanılabilirlik kümesine yerleştirme uygulamanız işletim sistemi veya uygulamaya özgü hataları korumaz olsa da, olası fiziksel donanım hataları, ağ kesintileri veya güç kesintilerinin hello etkisini sınırlayın.

<!--Image reference-->
   ![Merhaba güncelleştirme etki alanı ve hata etki alanı yapılandırmasını kavramsal çizimi](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Bir kullanılabilirlik kümesindeki VM’ler için yönetilen diskleri kullanma
Yönetilmeyen disklerle şu anda sanal makineleri kullanıyorsanız, yüksek oranda öneririz [sanal makineleri kullanılabilirlik kümesi toouse yönetilen disklerde Dönüştür](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Yönetilen diskleri](../articles/virtual-machines/windows/managed-disks-overview.md) kullanılabilirlik sağlayarak bir kullanılabilirlik kümesindeki sanal makineleri hello diskleri yeterince olan kümeleri birbirinden tooavoid tek hata noktaları bulundurmaktan yalıtılmış için daha iyi güvenilirlik sağlar. Bunu otomatik olarak farklı depolama kümelerde hello diskleri yerleştirerek yapar. Bir depolama kümesi toohardware veya yazılım hatası başarısız olursa, yalnızca hello VM örnekleri bu Damgalar disklerle başarısız.

![Yönetilen Disk FD’leri](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> hata etki alanlarını yönetilen kullanılabilirlik kümeleri için Hello sayısı değişir bölgeye göre - iki veya üç her bölge. Merhaba aşağıdaki tabloda hello numarasını bölge başına gösterir

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Toouse VM'ler ile planlıyorsanız [yönetilmeyen diskleri](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), aşağıdaki olarak sanal makineleri sanal sabit diskleri (VHD) depolandığı depolama hesapları için en iyi uygulamaları izleyin [sayfa blobları](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **VM hello ile ilişkili tüm diskleri (işletim sistemi ve veri) tutmak aynı depolama hesabı**
2. **Gözden geçirme hello [sınırları](../articles/storage/common/storage-scalability-targets.md) yönetilmeyen diskleri depolama hesabındaki hello sayısına** daha fazla VHD tooa depolama hesabı eklemeden önce
3. **Bir Kullanılabilirlik Kümesindeki her VM için ayrı depolama hesabı kullanın.** Depolama hesapları hello içinde birden çok VM ile paylaşmaz aynı kullanılabilirlik kümesi. En iyi yöntemler izlediyseniz farklı kullanılabilirlik kümeleri tooshare depolama hesaplarında VM'ler için kabul edilebilir

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Her uygulama katmanını ayrı kullanılabilirlik kümeleri halinde yapılandırma
Sanal makinelerinizi tüm neredeyse aynıdır ve hello hizmet aynı amaçla uygulamanız için uygulamanızı her katman için kullanılabilirlik kümesi yapılandırmanızı öneririz.  İki farklı yerleştirirseniz hello aynı katmanlarını kullanılabilirlik kümesi, aynı uygulama katmanı yeniden aynı anda hello tüm sanal makinelerin. Her katman için bir kullanılabilirlik kümesinde en az iki sanal makineyi yapılandırarak, her katmanda en az bir sanal makinenin kullanılabilir olmasını garanti edersiniz.

Örneğin, IIS, Apache, Nginx bir tek kullanılabilirlik kümesinde çalışan uygulamanızın hello ön uçtaki tüm hello sanal makineleri koyabilirsiniz. Yalnızca ön uç sanal makineler hello aynı yerleştirildiğinden emin olun kullanılabilirlik kümesi. Benzer şekilde, çoğaltılmış SQL Server sanal makineleriniz ya da MySQL sanal makineleriniz gibi yalnızca veri katmanı sanal makinelerinin kendi kullanılabilirlik kümelerine yerleştirildiğinden emin olun.

<!--Image reference-->
   ![Uygulama katmanları](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Yük dengeleyiciyi kullanılabilirlik kümeleri ile birleştirme
Merhaba birleştirmek [Azure yük dengeleyici](../articles/load-balancer/load-balancer-overview.md) kullanılabilirlik ile tooget hello çoğu uygulama dayanıklılığı ayarlayın. Hello Azure yük dengeleyici trafiği birden çok sanal makine arasında dağıtır. Bizim standart katman sanal makinelerde için hello Azure yük dengeleyici dahil edilir. Tüm sanal makine katmanları hello Azure yük dengeleyici içerir. Sanal makinelerinizde yük dengeleme hakkında daha fazla bilgi için bkz. [Sanal makinelerde yük dengeleme](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Merhaba yük dengeleyici değilse hello yalnızca trafik sunma sanal bir kesinti tooyour uygulama katmanı neden makine, herhangi bir planlı bakım olayı etkiler sonra toobalance trafiği birden çok sanal makine genelinde yapılandırılmış. Merhaba, birden çok sanal makine yerleştirme aynı aynı yük dengeleyici ve kullanılabilirlik kümesi etkinleştirir trafiği toobe sürekli olarak en az bir örneği tarafından sunulan hello altında katmanı.


<!-- Link references -->
[Bir kullanılabilirlik kümesindeki birden fazla sanal makineyi yedeklilik için yapılandırma]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Her uygulama katmanını ayrı kullanılabilirlik kümeleri halinde yapılandırma]: #configure-each-application-tier-into-separate-availability-sets
[Yük Dengeleyiciyi kullanılabilirlik kümeleri ile birleştirme]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Bir kullanılabilirlik kümesindeki VM’ler için yönetilen diskleri kullanma]: #use-managed-disks-for-vms-in-an-availability-set
