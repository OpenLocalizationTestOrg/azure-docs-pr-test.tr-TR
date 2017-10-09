# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Klasik tooAzure Resource Manager Iaas kaynaklardan Platform desteklenen geçişini
Bu makalede, biz altyapı geçiş hello Klasik tooResource Manager dağıtım modellerinde hizmet (Iaas) kaynaklardan olarak nasıl etkinleştirme açıklanmaktadır. Daha fazla bilgi edinebilirsiniz [Azure Kaynak Yöneticisi özellikleri ve avantajları](../articles/azure-resource-manager/resource-group-overview.md). Siteden siteye ağ geçitleri nasıl ağ tooconnect kaynaklarını aboneliğinizde sanal kullanarak arada hello iki dağıtım modelinden detaylandırır.

## <a name="goal-for-migration"></a>Geçiş için hedef
Resource Manager şablonları aracılığıyla karmaşık uygulamaları dağıtma sağlar, VM uzantıları kullanarak sanal makineleri yapılandırır ve erişim yönetimi ve etiketleme içerir. Azure Resource Manager kullanılabilirlik kümeleri içinde sanal makineler için ölçeklenebilir, paralel dağıtım içerir. Merhaba yeni dağıtım modeli de bağımsız olarak işlem, ağ ve depolama yaşam döngüsü yönetimi sağlar. Son olarak, bir sanal ağdaki sanal makinelerin hello zorlama ile varsayılan güvenlik etkinleştirmek için bir odak yoktur.

İşlem, ağ ve depolama altında Azure Resource Manager için desteklenen hello Klasik dağıtım modelinden neredeyse tüm hello özellikleri. toobenefit hello yeni özelliklerden Azure Kaynak Yöneticisi'nde hello Klasik dağıtım modeli dağıtımlarını varolan geçirebilirsiniz.

## <a name="supported-resources-for-migration"></a>Geçiş için desteklenen kaynaklar
Geçiş sırasında bu Klasik Iaas kaynakları desteklenir

* Virtual Machines
* Kullanılabilirlik Kümeleri
* Cloud Services
* Depolama Hesapları
* Sanal Ağlar
* VPN Gateway’leri
* Rota ağ geçitleri express _(Merhaba, yalnızca aynı abonelik sanal ağ olarak)_
* Ağ Güvenlik Grupları 
* Yönlendirme Tabloları 
* Ayrılmış IP’ler 

## <a name="supported-scopes-of-migration"></a>Desteklenen kapsamları geçiş
İşlem, ağ ve depolama kaynaklarını toocomplete geçişini 4 farklı yolu vardır. Bunlar 

* (Değil, sanal ağ için) sanal makinelerin geçişi
* (Sanal ağındaki) sanal makinelerin geçişi
* Depolama hesapları geçişi
* Eklenmemiş kaynaklar (ağ güvenlik grupları, yol tablolarını & ayrılmış IP'ler)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>(Değil, sanal ağ için) sanal makinelerin geçişi
Merhaba Resource Manager dağıtım modelinde güvenlik uygulamalarınız için varsayılan olarak uygulanır. Tüm sanal makineleri hello Resource Manager modelinde bir sanal ağdaki toobe gerekir. Hello Azure platformu yeniden (`Stop`, `Deallocate`, ve `Start`) VM'ler hello geçişin bir parçası hello. Sanal makineler hello hello sanal ağlar için geçişi için iki seçeneğiniz vardır:

* Merhaba platform toocreate yeni bir sanal ağ isteyin ve hello yeni sanal ağınıza hello sanal makineyi geçirin.
* Mevcut sanal ağda Kaynak Yöneticisi'nde hello sanal makine geçirebilirsiniz.

> [!NOTE]
> Bu geçiş kapsamında hem de Yönetim düzeyi işlemleri hello ve hello veri düzlemi işlemleri hello geçiş sırasında bir süre için izin verilmeyebilir.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>(Sanal ağındaki) sanal makinelerin geçişi
VM yapılandırmaların çoğu için meta veri hello hello Klasik ve Resource Manager dağıtım modelleri arasında geçiriyor. temel alınan VM'lerin hello üzerinde çalıştığı hello aynı donanımda, aynı ağ ve ile aynı hello hello depolama. Merhaba Yönetim düzeyi işlemleri zaman hello geçiş sırasında belirli bir süre için izin verilmeyebilir. Ancak, hello veri düzlemi toowork devam eder. Diğer bir deyişle, (Klasik) VM'ler üzerinde çalıştırılan uygulamalarınızın kapalı kalma süresi hello geçiş sırasında tabi değil.

aşağıdaki yapılandırmalar hello şu anda desteklenmemektedir. Destek hello gelecekteki eklediyseniz, bu yapılandırmada bazı VM'ler kapalı kalma süresi neden olabilecek (Dur ayırması ve VM işlemlerini yeniden Git).

* Birden fazla kullanılabilirlik tek bulut hizmetinde kümesi vardır.
* Bir veya daha fazla kullanılabilirlik kümeleri ve bir kullanılabilirlik kümesinde tek bulut hizmetinde olmayan VM'ler var.

> [!NOTE]
> Bu geçiş kapsamda hello Yönetim düzeyi hello geçiş sırasında bir süre için izin verilmeyebilir. Veri düzlemi kapalı kalma süresinin daha önce açıklandığı gibi yapılandırmalar belirli.
>
>

### <a name="storage-accounts-migration"></a>Depolama hesapları geçişi
tooallow sorunsuz geçiş, Resource Manager sanal makineleri Klasik depolama hesabında dağıtabilirsiniz. Bu özelliği, işlem ve ağ kaynaklarını olabilir ve depolama hesapları bağımsız olarak geçirilmelidir. Sanal makineler ve sanal ağ üzerinden geçirmek sonra depolama hesapları toocomplete hello geçiş işleminizi toomigrate gerekir.

> [!NOTE]
> Merhaba Resource Manager dağıtım modeli Klasik görüntüler ve diskleri hello kavramı yoktur. Hello depolama hesabıdır geçirilen, Klasik görüntüler ve diskleri hello Kaynak Yöneticisi yığını ancak yedekleme hello görünür değildir VHD'ler hello depolama hesabında kalır.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Eklenmemiş kaynaklar (ağ güvenlik grupları, yol tablolarını & ayrılmış IP'ler)
Ağ güvenlik grupları, yol tablolarını & olmayan ayrılmış IP'ler sanal makineler ve sanal ağlar bağımsız olarak geçirilebilir tooany bağlı.

<br>

## <a name="unsupported-features-and-configurations"></a>Desteklenmeyen özellikler ve yapılandırmalar
Şu anda bazı özellikler ve yapılandırmalar desteklemiyoruz. Aşağıdaki bölümlerde hello etrafında bizim önerileri açıklar.

### <a name="unsupported-features"></a>Desteklenmeyen özellikler
özellikler aşağıdaki hello şu anda desteklenmemektedir. İsteğe bağlı olarak bu ayarları kaldırabilir, hello Vm'leri geçirme ve hello Resource Manager dağıtım modelinde hello ayarlarını yeniden etkinleştirin.

| Kaynak sağlayıcısı | Özellik | Öneri |
| --- | --- | --- |
| İşlem |İlişkilendirilmemiş sanal makine disklerini. | Merhaba depolama hesabı geçirildiğinde bu diskleri arkasında hello VHD bloblarının geçirilen |
| İşlem |Sanal makine görüntüler. | Merhaba depolama hesabı geçirildiğinde bu diskleri arkasında hello VHD bloblarının geçirilen |
| Ağ |Uç nokta ACL'lerini. | Uç nokta ACL'lerini kaldırın ve geçiş yeniden deneyin. |
| Ağ |Sanal ağ ExpressRoute ağ geçidi ve VPN ağ geçidi ile  | Geçiş işlemine başlamadan önce Hello VPN ağ geçidi kaldırın ve geçiş tamamlandıktan sonra hello VPN ağ geçidi yeniden oluşturun. Daha fazla bilgi edinmek [ExpressRoute geçiş](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Ağ |ExpressRoute ile yetkilendirme bağlantılar  | Geçişe başlamadan önce hello ExpressRoute bağlantı hattı toovirtaul ağ bağlantısı kaldırın ve geçiş tamamlandıktan sonra hello bağlantısını yeniden oluşturun. Daha fazla bilgi edinmek [ExpressRoute geçiş](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Ağ |Application Gateway | Geçiş işlemine başlamadan önce Hello uygulama ağ geçidi kaldırın ve geçiş tamamlandıktan sonra hello uygulama ağ geçidini yeniden oluşturun. |
| Ağ |VNet eşlemesi kullanarak sanal ağlar. | Sanal ağ tooResource Yöneticisi geçirme sonra eş. Daha fazla bilgi edinmek [VNet eşlemesi](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Desteklenmeyen yapılandırmalar
aşağıdaki yapılandırmalar hello şu anda desteklenmemektedir.

| Hizmet | Yapılandırma | Öneri |
| --- | --- | --- |
| Resource Manager |Rol tabanlı erişim denetimi (RBAC) Klasik kaynaklar için |Merhaba hello kaynakları URI'sini geçişten sonra değiştirdiğinden, geçişten sonra toohappen gerektiren hello RBAC İlkesi güncelleştirmeler plan yapmanız önerilir. |
| İşlem |Bir VM ile ilişkili birden çok alt ağı |Merhaba alt ağ yapılandırması tooreference yalnızca alt güncelleştirin. |
| İşlem |Sanal ağ tooa ait olan ancak atanan açık bir alt ağ yoksa sanal makineler |İsteğe bağlı olarak hello VM silebilirsiniz. |
| İşlem |Uyarılar, otomatik ölçeklendirme ilkeleri sanal makineler |Merhaba geçiş geçtiği ve bu ayarları bırakılır. Geçiş hello önce ortamınızı değerlendirmek önerilir. Alternatif olarak, geçiş tamamlandıktan sonra hello uyarı ayarlarını yapılandırabilirsiniz. |
| İşlem |XML VM Uzantıları (Bgınfo 1.*, Visual Studio hata ayıklayıcısı, Web dağıtımı ve uzaktan hata ayıklama) |Bu işlem desteklenmiyor. Bu uzantılar hello sanal makine toocontinue geçişini kaldırın veya hello geçiş işlemi sırasında otomatik olarak bırakılacak önerilir. |
| İşlem |Premium depolama ile önyükleme tanılama |Merhaba VM'ler için önyükleme tanılaması özelliğini geçirme işlemine devam etmeden önce devre dışı bırakın. Merhaba geçiş tamamlandıktan sonra önyükleme tanılaması hello Kaynak Yöneticisi yığınında yeniden etkinleştirebilirsiniz. Ayrıca, artık bu BLOB'lar için ücretlendirilirsiniz şekilde ekran ve seri günlükleri için kullanılan BLOB'ları silinmelidir. |
| İşlem |Web/çalışan rolü içeren bulut Hizmetleri |Bu şu anda desteklenmiyor. |
| Ağ |Sanal makineler ve web/çalışan rolleri içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Azure App Service |Uygulama hizmeti ortamları içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Azure Hdınsight |Hdınsight hizmetleri içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Microsoft Dynamics yaşam döngüsü Hizmetleri |Dynamics yaşam döngüsü Hizmetleri tarafından yönetilen sanal makineleri içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Azure AD Domain Services |Azure AD etki alanı hizmetleri içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Azure RemoteApp |Azure RemoteApp dağıtımlarını içeren sanal ağlar |Bu şu anda desteklenmiyor. |
| Azure API Management |Azure API Management dağıtımlarını içeren sanal ağlar |Bu şu anda desteklenmiyor. toomigrate hello Iaas VNET, lütfen hello hello herhangi bir kapalı kalma süresi işlemi API Management dağıtımında VNET değiştirin. |
| İşlem |Geçiş bağlantısı VPN ağ geçidi veya ExpressRoute ağ geçidi şirket içi DNS sunucusuyla sahip bir VNET ile Azure Güvenlik Merkezi uzantıları |Azure Güvenlik Merkezi otomatik olarak uzantıları, sanal makineleri toomonitor kendi güvenlik yükler ve uyarılar oluşturacak. Hello Azure Güvenlik Merkezi ilke hello abonelikte etkinse, bu uzantılar genellikle otomatik olarak yüklenir. ExpressRoute ağ geçidi geçişi şu anda desteklenmiyor ve VPN ağ geçitleri geçiş bağlantısı ile şirket içi erişim kaybeder. ExpressRoute silme ağ geçidi veya geçiş bağlantı geçirme VPN ağ geçidi hello geçişi gerçekleştirmeden ile etmeden zaman kayıp Internet erişimi tooVM depolama hesabı toobe neden olur. Merhaba Konuk Aracısı durumu blobu doldurulamaz gibi böyle bir durumda hello geçiş devam etmez. Geçiş işlemine devam etmeden önce 3 saat toodisable hello abonelikte Azure Güvenlik Merkezi ilke önerilir. |

