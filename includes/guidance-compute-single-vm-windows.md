Bu makalede, Azure'da Windows sanal makine (VM) çalıştıran, dikkat tooscalability, kullanılabilirlik, yönetilebilirlik ve güvenlik ödeme kanıtlanmış yöntemler kümesi özetlenmektedir.

> [!NOTE]
> Azure iki farklı dağıtım modeline sahiptir: [Azure Resource Manager] [ resource-manager-overview] ve klasik. Bu makalede, Microsoft’un yeni dağıtımlar için önerdiği Resource Manager modeli kullanılır.
>
>

Tek sanal makine kullanıldığında tek bir hata noktası oluştuğundan, görev açısından kritik iş yükleri için tek makine kullanılmasını önermeyiz. Daha yüksek kullanılabilirlik için bir [kullanılabilirlik kümesinde][availability-set] birden çok sanal makine dağıtın. Daha fazla bilgi edinmek için bkz. [Azure’da birden çok sanal makine çalıştırma][multi-vm].

## <a name="architecture-diagram"></a>Mimari diyagramı

Azure'da VM sağlama yalnızca VM kendisini hello daha fazla hareketli bölümleri içerir. İşlem, ağ ve depolama öğe daha vardır.

> Bu mimari diyagramı içeren Visio belgesine hello karşıdan [Microsoft Yükleme Merkezi'nden][visio-download]. "İşlem - tek VM" Merhaba üzerinde bu diyagramıdır sayfası.
>
>

![[0]][0]

* **Kaynak grubu.** [*Kaynak grubu*][resource-manager-overview], ilgili kaynakları barındıran bir kapsayıcıdır. Bir kaynak grubu toohold hello kaynakları bu VM için oluşturun.
* **Sanal makine**. Bir VM yayımlanan görüntülerinin listesinden veya bir sanal sabit disk (VHD) dosyasını tooAzure Blob Depolama karşıya yükle sağlayabilirsiniz.
* **İşletim sistemi diski.** Merhaba OS disktir depolanmış VHD [Azure Storage][azure-storage]. Merhaba ana makine çökmesi durumunda bile devam ederse anlamına gelir.
* **Geçici disk.** Merhaba VM geçici bir disk ile oluşturulur (Merhaba `D:` Windows sürücüsünde). Bu diski fiziksel bir sürücü hello konak makinesi üzerinde depolanır. Azure Depolama’ya *kaydedilmez* ve yeniden başlatma işlemleri ya da diğer sanal makine yaşam döngüsü olayları sırasında silinebilir. Bu diski yalnızca sayfa veya takas dosyaları gibi geçici veriler için kullanın.
* **Veri diskleri.** [Veri diski][data-disk], uygulama verileri için kullanılan kalıcı bir VHD’dir. Veri diskleri hello işletim sistemi diski gibi Azure Storage'da depolanır.
* **Sanal ağ (VNet) ve alt ağ.** Azure'daki her sanal makine, kendi içinde alt ağlara ayrılan bir sanal ağa dağıtılır.
* **Genel IP adresleri.** Gerekli toocommunicate hello VM ile bir ortak IP adresi olduğundan&mdash;örneğin Uzak Masaüstü (RDP) üzerinden.
* **Ağ arabirimi (NIC)**. Merhaba NIC hello VM toocommunicate hello sanal ağ ile sağlar.
* **Ağ güvenlik grubu (NSG)**. Merhaba [NSG] [ nsg] kullanılan tooallow/reddetme ağ trafiği toohello alt ağıdır. NSG’yi tek başına bir NIC ya da alt ağ ile ilişkilendirebilirsiniz. Bir alt ağ ile ilişkilendirirseniz hello NSG kuralları bu alt ağdaki tooall VM'ler uygulayın.
* **Tanılama.** Tanılama günlük kaydını, yönetme ve hello VM sorun giderme için önemlidir.

## <a name="recommendations"></a>Öneriler

aşağıdaki önerileri hello çoğu senaryoları için geçerlidir. Bu önerileri geçersiz kılan belirli bir gereksiniminiz olmadığı sürece izlemeniz önerilir.

### <a name="vm-recommendations"></a>Sanal makine önerileri

Azure birçok farklı sanal makine boyutlarını sunar, ancak bu makine boyutlarını desteklediğinden hello DS - ve GS serisi öneririz [Premium depolama][premium-storage]. Yüksek performanslı bilgi işlem gibi özel bir iş yükünüz yoksa bu sanal makine boyutlarından birini seçin. Ayrıntılar için bkz. [sanal makine boyutları][virtual-machine-sizes].

Var olan bir iş yükü tooAzure taşıyorsanız, başlangıç hello en yakın eşleşme tooyour hello VM boyutu ile sunucuları şirket içi. Ardından ölçü hello ile gerçek, İş yükünüzün performansını tooCPU, bellek ve disk girdi/çıktı işlemleri (IOPS) saniyede saygı ve gerekirse hello boyutunu ayarlayın. VM için birden çok NIC gerektiriyorsa, hello en fazla sayıda NIC hello bir işlevi olduğunu unutmayın [VM boyutu][vm-size-tables].   

Merhaba VM ve diğer kaynakları hazırlarken bir bölge belirtmeniz gerekir. Genellikle, en yakın tooyour iç kullanıcılar bir bölge seçin veya müşterilerin. Ancak, tüm VM boyutları tüm bölgelerde kullanılabilir olabilir. Ayrıntılar için bkz [bölgeye göre Hizmetleri][services-by-region]. toosee hello VM boyutları kullanılabilir Azure komut satırı arabirimi (CLI) komutu aşağıdaki hello çalıştırmak, belirli bir bölgedeki listesi:

```
azure vm sizes --location <location>
```

Yayımlanmış bir VM görüntüsü seçme hakkında daha fazla bilgi için bkz: [gidin ve Azure Powershell veya CLI ile select Windows sanal makine görüntüleri][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Disk ve depolama önerileri

En iyi disk g/ç performansı öneririz [Premium depolama][premium-storage], katı hal sürücüleri (SSD) verileri depolar. Maliyet hello hello sağlanan disk boyutuna dayanır. IOPS ve üretilen iş ayrıca disk boyutuna bağlı bir disk sağladığınızda, bu nedenle tüm üç faktöre (kapasite, IOPS ve üretilen iş) göz önünde bulundurun.

Depolama hesapları için hello IOPS sınırları basarsa sipariş tooavoid her VM toohold hello sanal sabit diskleri (VHD) için ayrı bir Azure depolama hesapları oluşturun.

Bir veya daha fazla veri diski ekleyin. Yeni bir VHD oluşturduğunuzda, biçimlendirilmemiş. Merhaba VM tooformat hello diskine oturum açın. Çok sayıda veri diski varsa, hello toplam g/ç sınırları hello depolama hesabının unutmayın. Daha fazla bilgi edinmek için bkz. [sanal makine disk limitleri][vm-disk-limits].

Mümkün olduğunda, uygulamaları hello işletim sistemi diski bir veri diski yükleyin. Ancak, bazı eski uygulamalarını hello C: sürücüsündeki tooinstall bileşenlerini gerekebilir. Bu durumda, şunları yapabilirsiniz [hello işletim sistemi disk yeniden boyutlandırma] [ resize-os-disk] PowerShell kullanarak.

En iyi performans için toohold tanılama günlükleri ayrı bir depolama hesabı oluşturun. Tanılama günlükleri için standart bir yerel olarak yedekli depolama (LRS) yeterlidir.

### <a name="network-recommendations"></a>Ağ önerileri

Merhaba genel IP adresi dinamik veya statik olabilir. Merhaba varsayılan, dinamik bir işlemdir.

* Ayrılmış bir [statik IP adresi] [ static-ip] değişmeyeceği sabit bir IP adresi gerekip gerekmediğini &mdash; Örneğin, toocreate gerekiyorsa bir A kaydı DNS'de veya IP adresi toobe eklenen tooa güvenli listesi hello.
* Başlangıç IP adresi için bir tam etki alanı adı (FQDN) de oluşturabilirsiniz. Ardından kaydedebilirsiniz bir [CNAME kaydı] [ cname-record] toohello FQDN işaret eden DNS'deki. Daha fazla bilgi için bkz: [hello Azure portalında bir tam etki alanı adı oluşturma][fqdn].

Tüm NSG’ler, tüm gelen İnternet trafiğini engelleyen bir kuralın da dahil olduğu bir [varsayılan kurallar][nsg-default-rules] kümesi içerir. Merhaba varsayılan kurallar silinemez ancak diğer kuralları geçersiz kılabilirsiniz. tooenable Internet trafiğini toospecific bağlantı noktalarına gelen trafiğe izin verecek kuralları oluşturma &mdash; Örneğin, HTTP için bağlantı noktası 80 '.  

RDP, tooenable tooTCP 3389 numaralı bağlantı noktasına gelen trafiğe izin veren bir NSG kuralı ekleyin.

## <a name="scalability-considerations"></a>Ölçeklenebilirlik konusunda dikkat edilmesi gerekenler

Bir VM yukarı veya aşağı tarafından ölçeklendirmek [hello VM boyutunu değiştirme](../articles/virtual-machines/windows/sizes.md). out tooscale iki veya daha fazla VM'nin kullanılabilirlik kümesi bir yük dengeleyicinin arkasına yatay yerleştirin. Ayrıntılar için bkz [ölçeklenebilirlik ve kullanılabilirlik için birden çok sanal makineleri Azure üzerinde çalışan][multi-vm].

## <a name="availability-considerations"></a>Kullanılabilirlik konusunda dikkat edilmesi gerekenler

Daha yüksek kullanılabilirlik için bir kullanılabilirlik kümesinde birden çok sanal makine dağıtın. Bu da daha yüksek sağlar [hizmet düzeyi sözleşmesi] [ vm-sla] (SLA).

Sanal makineniz [planlı bakım][planned-maintenance] veya [plansız bakımdan][manage-vm-availability] etkilenebilir. Kullanabileceğiniz [VM yeniden başlatma günlükleri] [ reboot-logs] olup bir VM yeniden başlatma tarafından planlı bakım nedeni toodetermine.

VHD’ler [Azure depolama alanında][azure-storage] saklanır ve Azure depolama alanı dayanıklılık ve kullanılabilirlik sağlamak amacıyla çoğaltılır.

tooprotect (örneğin, kullanıcı hatası nedeniyle) normal işlemler sırasında yanlışlıkla veri kaybına karşı kullanarak, zaman içinde nokta yedeklemeler de uygulamanız gerekir [blob anlık görüntüleri] [ blob-snapshot] veya başka bir araç.

## <a name="manageability-considerations"></a>Yönetilebilirlik konusunda dikkat edilmesi gerekenler

**Kaynak grupları.** Sıkı şekilde bağlı kaynakları put aynı yaşam döngüsü içine o paylaşımı hello hello aynı [kaynak grubu][resource-manager-overview]. Kaynak grupları ve kaynak grubu tarafından maliyetleri faturalama yukarı alma grup olarak toodeploy ve İzleyici kaynakları izin verin. Kaynakları bir küme halinde silme imkanınız da olur ve test dağıtımları için bu özellik çok kullanışlıdır. Kaynaklara anlamlı adlar verin. Daha kolay toolocate belirli bir kaynak kolaylaştırır ve rolü anlayın. Bkz. [Azure Kaynakları için Önerilen Adlandırma Kuralları][naming conventions].

**Sanal makine tanılama.** Temel sistem durumu ölçümleri, tanılama altyapısı günlükleri ve [önyükleme tanılaması][boot-diagnostics] gibi izleme ve tanılama özelliklerini etkinleştirin. Önyükleme Tanılaması, VM nonbootable durumuna alır, bir önyükleme hatası tanılamanıza yardımcı olabilir. Daha fazla bilgi edinmek için bkz. [İzleme ve tanılamayı etkinleştirme][enable-monitoring]. Kullanım hello [Azure günlük toplama] [ log-collector] uzantısı toocollect Azure platformu günlüğe kaydeder ve onları tooAzure depolama yükleme.   

CLI komutu aşağıdaki hello tanılama sağlar:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Sanal makineyi durdurma.** Azure’da “durduruldu” ile “serbest bırakıldı” durumları birbirinden farklıdır. VM durumu hello durdurulduğunda, ancak hello VM deallocated olmadığında sizden ücret kesilir.

CLI komutu toodeallocate VM aşağıdaki hello kullan:

```
azure vm deallocate <resource-group> <vm-name>
```

Hello Azure portal, hello **durdurmak** düğmesi hello VM kaldırır. Ancak, hello oturum açtığınızda işletim sistemi aracılığıyla kapatma hello VM durdurulur ancak *değil* hala ücret şekilde, serbest bırakıldı.

**Sanal makineyi silme.** Bir VM silerseniz, hello VHD'ler silinmez. Merhaba VM verilerini kaybetmeden güvenle silebilirsiniz anlamına gelir. Ancak, depolama ücretlendirilmeye devam edersiniz. toodelete hello VHD'yi Sil hello dosyasından [Blob storage][blob-storage].

tooprevent yanlışlıkla silinmesi, kullanım bir [kaynak kilidi] [ resource-lock] toolock hello tüm kaynak grubu veya kilidi tek tek gibi kaynaklar hello VM.

## <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler

Kullanım [Azure Güvenlik Merkezi] [ security-center] tooget hello Azure kaynaklarınızın güvenlik durumunu Merkezi görünümü. Güvenlik Merkezi olası güvenlik sorunlarını izler ve dağıtımınızın hello güvenlik durumu, kapsamlı bir görünümünü sağlar. Güvenlik Merkezi, Azure abonelik başına yapılandırılır. Bölümünde açıklandığı gibi güvenlik veri toplamayı etkinleştirmek [Güvenlik Merkezi'ni kullanın]. Veri toplama etkinleştirilmişse, Güvenlik Merkezi Bu abonelik altında oluşturulan tüm sanal makineleri otomatik olarak tarar.

**Düzeltme Eki Yönetimi.** Etkinleştirilirse, Güvenlik Merkezi güvenlik ve kritik güncelleştirmeleri eksik olup olmadığını denetler. Kullanım [Grup İlkesi ayarlarını] [ group-policy] hello VM tooenable otomatik sistem güncelleştirmeleri.

**Kötü amaçlı yazılımdan koruma.** Etkinleştirilirse, Güvenlik Merkezi, kötü amaçlı yazılımdan koruma yazılımı yüklü olup olmadığını denetler. Güvenlik Merkezi tooinstall kötü amaçlı yazılımdan koruma yazılımlarını içinde de kullanabilirsiniz Azure portal hello.

**İşlemler.** Kullanım [rol tabanlı erişim denetimi] [ rbac] (RBAC) toocontrol erişim toohello Azure dağıttığınız kaynakları. RBAC yetkilendirme rolleri toomembers DevOps ekibinizin atamanıza olanak tanır. Örneğin, hello okuyucu rolüne Azure kaynaklarını görüntüleyebilir ancak değil oluşturmak, yönetmek veya silebilirsiniz. Bazı roller, belirli tooparticular Azure kaynak türleridir. Örneğin, hello sanal makine katkıda bulunan rolü yeniden başlatın veya VM serbest bırakma, hello yönetici parolasını sıfırla, yeni bir VM oluşturun ve benzeri. Bu başvuru mimarisi için kullanışlı olabilecek diğer [yerleşik RBAC rolleri][rbac-roles] [DevTest Labs Kullanıcısı][rbac-devtest] ve [Ağ Katılımcısı][rbac-network]’dır. Bir kullanıcı toomultiple rolleri atanabilir ve daha ayrıntılı izinler için özel roller oluşturabilirsiniz.

> [!NOTE]
> RBAC bir VM'de oturum oturum açmış kullanıcının gerçekleştirebileceği hello Eylemler sınırlamaz. Bu izinleri hello hesap türüne hello konuk işletim sistemi tarafından belirlenir.   
>
>

Merhaba çalıştırmak, tooreset hello yerel yönetici parolasını `vm reset-access` Azure CLI komutu.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Kullanım [denetim günlüklerini] [ audit-logs] toosee Eylemler ve diğer VM olayları sağlama.

**Veri şifreleme.** Göz önünde bulundurun [Azure Disk şifrelemesi] [ disk-encryption] tooencrypt hello işletim sistemi ve veri diskleri gerekiyorsa.

## <a name="solution-deployment"></a>Çözüm dağıtımı

Bir dağıtım için bu başvuru mimarisinin kullanılabilir [GitHub][github-folder]. Bir sanal ağ, NSG ve tek bir sanal makine içerir. toodeploy Merhaba mimarisi, şu adımları izleyin:

1. Aşağıdaki başlangıç düğmesine sağ tıklayın ve ya da "açık bağlantı yeni sekmede" seçin veya "Bağlantıyı yeni pencerede aç."  
   [![TooAzure dağıtma](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Merhaba bağlantı hello Azure portal açtıktan sonra bazı hello ayarları için değerleri girmeniz gerekir:

   * Merhaba **kaynak grubu** adı hello parametre dosyasında, böylece select zaten tanımlı **Yeni Oluştur** ve girin `ra-single-vm-rg` hello metin kutusuna.
   * Merhaba SELECT hello bölgesinden **konumu** açılan kutusu.
   * Merhaba düzenlemeyin **şablonu kök URI** veya hello **parametresi kök URI** metin kutuları.
   * Seçin **windows** hello içinde **işletim sistemi türü** açılan kutusu.
   * Merhaba hüküm ve koşulları gözden geçirin ve ardından hello **toohello hüküm ve koşullar yukarıda belirtildiği kabul** onay kutusu.
   * Tıklatın hello üzerinde **satın alma** düğmesi.
3. Merhaba dağıtım toocomplete bekleyin.
4. bir sabit kodlanmış yönetici kullanıcı adı ve parola Hello parametre dosyaları dahil etme ve, hemen her ikisi de değiştirmeniz önerilir. Merhaba adlı VM üzerinde'ı tıklatın `ra-single-vm0 `hello Azure Portalı'nda. Ardından, tıklatın **parola sıfırlama** hello içinde **destek + sorun giderme** dikey. Seçin **parola sıfırlama** hello içinde **modu** açılır kutusunda, ardından yeni bir **kullanıcı adı** ve **parola**. Merhaba tıklatın **güncelleştirme** düğmesini toopersist hello yeni bir kullanıcı adı ve parola.

Başka bir yolu toodeploy hakkında bilgi için bu başvuru mimarisi, hello hello Benioku dosyasına bakın [Kılavuzu tek vm][github-folder]] GitHub klasör.

## <a name="customize-hello-deployment"></a>Merhaba dağıtım özelleştirme
Gereksinimlerinize toochange hello dağıtım toomatch gerekiyorsa, hello'ndaki hello yönergeleri izleyin [Benioku][github-folder].

## <a name="next-steps"></a>Sonraki adımlar
Daha yüksek kullanılabilirlik elde etmek için bir yük dengeleyicisinin arkasında iki veya daha fazla sanal makine dağıtın. Daha fazla bilgi edinmek için bkz. [Azure’da birden çok sanal makine çalıştırma][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Güvenlik Merkezi'ni kullanın]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Azure'da tek bir Windows VM mimarisi"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
