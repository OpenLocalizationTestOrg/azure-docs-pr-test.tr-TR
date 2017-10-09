## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Merhaba Klasik dağıtım modeli tooResource Yöneticisi Iaas kaynaklardan geçişini anlamını
Biz hello ayrıntılara detaya önce hello Iaas kaynaklarına veri düzlemi ve Yönetim düzeyi işlemlerini hello birbirinden bakalım.

* *Yönetim/denetim düzlemi* hello Yönetimi/denetim düzlemi veya hello API kaynakları değiştirmek için gelen hello çağrıları açıklar. Örneğin, bir VM oluşturma, bir VM'yi yeniden başlatırken ve yeni bir alt ağ ile sanal ağ güncelleştirme gibi işlemler kaynakları çalıştıran hello yönetin. Bunlar, doğrudan bağlanan toohello örnekleri etkilemez.
* *Veri düzlemi* (uygulama) hello çalışma zamanı hello uygulamanın kendisini açıklar ve etkileşim hello Azure API geçmez, örnekleri ile ilgilidir. Web sitenize erişme ya da çalışmakta olan bir SQL Server örneğinden veya MongoDB sunucusundan veri çekme işlemleri, veri düzlemi veya uygulama etkileşimi olarak görülür. Ayrıca bir depolama hesabından bir blob kopyalama ve bir ortak IP adresi tooRDP veya SSH hello sanal makinesine erişilirken veri düzlemi değildir. Bu işlemlerin işlem, ağ ve depolama üzerinde çalışan hello uygulama tutun.

Merhaba arka planda hello veri düzlemi olduğu hello hello Klasik dağıtım modeli ve Kaynak Yöneticisi yığını arasında aynı. Geçiş işlemi sırasında hello Klasik dağıtım modeli toothat hello Kaynak Yöneticisi yığınında hello kaynaklardan hello gösterimini çevir. Sonuç olarak, kaynaklarınızın hello Kaynak Yöneticisi yığınında toouse yeni araçları, API'leri, SDK'ları toomanage gerekir.

![Yönetim/denetim düzlemi ile veri düzlemi arasındaki farkı gösteren ekran görüntüsü](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> Bazı yükseltme senaryolarında hello Azure platformu durdurur, kaldırır ve sanal makinelerinizi yeniden başlatır. Bu durum, kısa bir veri düzlemi kapalı kalma süresine yol açar.
>

## <a name="hello-migration-experience"></a>Merhaba geçiş deneyimi
Merhaba geçiş deneyimi başlamadan önce hello aşağıdaki önerilir:

* Merhaba kaynakları toomigrate istediğiniz herhangi bir desteklenmeyen özellikler veya yapılandırmaları kullanmayın emin olun. Genellikle hello platform bu sorunları algılar ve bir hata oluşturur.
* Bir sanal ağda olmayan VM'ler varsa, bunlar durduruldu ve olması hello parçası işlemi hazırlanırken serbest bırakıldı. Toolose hello genel IP adresi istemiyorsanız hello tetiklemeden önce başlangıç IP adresi ayırma içine görünüm işlemi hazırlayın. Merhaba VM'ler içinde bir sanal ağ varsa, ancak bunlar durduruldu serbest ve değil.
* Geçiş sırasında gerçekleşebilir beklenmeyen hatalar için İş dışı saatlerde tooaccommodate sırasında geçişinizi planlayın.
* Merhaba yapılandırmasına Vm'leriniz PowerShell, komut satırı arabirimi (CLI) komutları veya REST API'leri toomake hello hazırladıktan sonra adım doğrulama için daha kolay tamamlanmadan kullanarak yükleyin.
* Merhaba geçiş başlamadan önce Otomasyon/operationalization betikleri toohandle hello Resource Manager dağıtım modeli güncelleştirin. İsteğe bağlı olarak yapabileceğiniz hello kaynakları hello durumu hazır olduğunda alma işlemleri.
* Merhaba Klasik Iaas kaynaklarına yapılandırılır ve hello geçiş tamamlandıktan sonra planlama hello RBAC ilkeleri değerlendirin.

Merhaba geçiş iş akışı aşağıdaki gibidir

![Merhaba geçiş iş akışını gösteren ekran görüntüsü](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Aşağıdaki bölümlerde hello açıklanan tüm hello ıdempotent işlemleridir. Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hello yeniden deneme önerilir hazırlamak, iptal etmek veya yürütme işlemi. Hello Azure platformu hello eylemi yeniden dener.
>
>

### <a name="validate"></a>Doğrulama
Merhaba doğrulama işlemi hello geçiş işleminde hello ilk adımdır. Merhaba bu adımın amacı, tooanalyze hello hello Klasik dağıtım modelinde toomigrate istiyor ve hello kaynakları geçişini özellikli başarı/hata döndürür hello kaynakları durumudur.

(Bir sanal ağda değilse), hello sanal ağ veya bir bulut hizmeti için geçiş toovalidate istediğinizi seçin.

* Merhaba kaynak geçişini yeteneğine sahip değilse, hello Azure platformu neden için geçiş desteklenmiyor tüm hello nedenleri listeler.

#### <a name="checks-not-done-in-validate"></a>Doğrulama'nda yapılmadı denetler

Doğrulama işlemi yalnızca hello kaynakları hello Klasik dağıtım modelinde hello durumunu analiz eder. Tüm hataları ve desteklenmeyen senaryolar toovarious yapılandırmaları hello Klasik dağıtım modelinde son kontrol. Azure Kaynak Yöneticisi yığını hello kaynaklardaki geçiş sırasında zorunlu tuttukları hello tüm sorunlar için olası toocheck değil. Geçiş, diğer bir deyişle, hazırlama hello sonraki adımda dönüşümü Hello kaynakları uygulanabilecek olduğunda bu sorunlar yalnızca denetlenir. Merhaba tabloda doğrulama'nda denetlenmedi tüm hello sorunları listeler.


|Doğrula'ndaki Ağ denetimleri|
|-|
|ER ve VPN ağ geçitleri sahip bir sanal ağ|
|Sanal ağ geçidi bağlantısı durumu bağlantısını kesme|
|Önceden geçirilmiş tooAzure Kaynak Yöneticisi yığınında tüm ER devreler olan|
|Diğer bir deyişle, statik genel IP, dinamik genel IP'ler, yük dengeleyici, ağ güvenlik grupları, yol tablolarını, ağ arabirimleri gibi ağ kaynakları için Azure Kaynak Yöneticisi kota denetler |
| Dağıtım/VNET arasında tüm yük dengeleyici kuralları geçerli olup olmadığını denetleyin |
| Merhaba Vm'lerde Dur serbest arasında çakışan özel IP'ler için aynı denetleyin VNET |

### <a name="prepare"></a>Hazırlama
Merhaba Hazırlama işlemi hello ikinci hello geçiş işlemi adımdır. Merhaba bu adımın amacı, Iaas kaynaklarından Klasik dağıtım modeli tooResource Yöneticisi hello toosimulate hello dönüşümü gerçekleşir ve bu yan yana sizin için toovisualize sunar.

> [!NOTE] 
> Klasik kaynaklar bu adım sırasında değiştirilmez. Dolayısıyla geçiş çalışıyorsanız güvenli adım toorun taşır. 

(Bir sanal ağ değilse) hello sanal ağ veya hello bulut hizmeti için geçiş tooprepare istediğinizi seçin.

* Merhaba kaynak geçişini yeteneğine sahip değilse, hello Azure platformu hello geçiş işlemi durdurur ve neden hello Hazırlama işlemi başarısız oldu hello neden listeler.
* Merhaba kaynak geçişini yeteneğine sahipse, hello Azure platformu hello Yönetim düzeyi işlemleri geçiş altında hello kaynaklar için ilk kilitleyen. Örneğin, size mümkün tooadd geçiş altında bir veri diski tooa VM değildir.

Hello Azure platformu sonra hello geçiş meta veri kaynakları geçirme hello için Klasik dağıtım modeli tooResource Yöneticisi başlar.

Hello hazırladıktan sonra işlemi tamamlandığında, hello kaynaklara Klasik dağıtım modeli ve Resource Manager görselleştirme hello seçeneğiniz vardır. Her bir bulut hizmeti için hello Klasik dağıtım modelinde, hello Azure platformu hello düzenine sahip bir kaynak grubu adı oluşturur `cloud-service-name>-Migrated`.

> [!NOTE]
> Olası tooselect hello adı geçirilen kaynakları için oluşturulan kaynak grubunun değil (yani "-geçişi"), ancak geçiş tamamlandıktan sonra Azure Resource Manager taşıma özelliği toomove kaynakları tooany istediğiniz kaynak grubunu kullanabilirsiniz. Bunu hakkında daha fazla tooread [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../articles/resource-group-move-resources.md)

Burada, yürütmeye sonra Hazırlama işlemi hello sonucu göster iki ekranda bulunmaktadır. İlk ekranda hello özgün bulut hizmeti içeren bir kaynak grubu gösterir. İkinci ekranı hello yeni gösterir "-geçişi" Merhaba eşdeğer Azure Resource Manager kaynaklarını içeren kaynak grubu.

![Portal klasik bulut hizmetini gösteren ekran görüntüsü](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Hazırlama aşamasında Portal Azure Resource Manager kaynaklarını gösteren ekran görüntüsü](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Hazırlama aşamasında hello tamamlandıktan sonra kaynaklarınızı Perde Arkası göz İşte. Merhaba kaynak hello veri düzlemi olduğuna dikkat edin olduğu hello aynı. Hem hello Yönetim düzeyi (Klasik dağıtım modeli) hem de hello denetim düzlemi (Resource Manager) gösterilir.

![Merhaba arka planda hazırlama aşamasında](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Klasik sanal ağ içinde olmayan sanal makineleri durduruldu-serbest, geçişin bu aşamasında.
>

### <a name="check-manual-or-scripted"></a>Denetim (el ile veya betikle)
Merhaba onay adımda, önceki toovalidate hello geçiş doğru görünüyorsa indirdiğiniz hello yapılandırma isteğe bağlı olarak kullanabilirsiniz. Alternatif olarak, meta veri geçiş iyi görünür toohello portal ve nokta onay hello özelliklerini ve kaynaklarını toovalidate kaydolabilirsiniz.

Sanal ağ geçişi yapıyorsanız, sanal makinelerin çoğu yapılandırması yeniden başlatılmaz. Bu sanal makineleri üzerinde uygulamalar için hello uygulama hala çalışır durumda olduğunu doğrulayabilirsiniz.

Merhaba VM'ler beklendiği gibi güncelleştirilmiş komut dosyalarınızı doğru çalışıyorsanız çalışıyorsanız ve izleme otomasyon ve işletimsel betikleri toosee test edebilirsiniz. Yalnızca GET işlemler Hello kaynakları hello durumu hazır olduğunda desteklenir.

Önce toocommit hello geçiş gereken kümesi zaman penceresi yok. Bu durumdayken dilediğiniz kadar bekleyebilirsiniz. Ancak, iptal etmek veya yürütme kadar hello Yönetim düzeyi bu kaynaklar için kilitlendi.

Herhangi bir sorun görürseniz, her zaman hello geçiş iptal etmek ve toohello Klasik dağıtım modeli geri dönün. Geri dönün sonra bu vm'lerde hello Klasik dağıtım modelinde normal işlemler devam edebilmeniz için hello Azure platformu hello kaynaklar üzerinde hello Yönetim düzeyi işlemlerine açar.

### <a name="abort"></a>Durdurma
Abort toorevert, değişiklikleri toohello Klasik dağıtım modeli kullanır ve hello geçişi durdurmanız isteğe bağlı bir adımdır. Bu işlem hello Resource Manager hello önceki hazırlama adımda oluşturulan meta veri kaynaklarınız için siler. 

![Merhaba arka planda durdurma aşamasında](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Merhaba kaydetme işlemi tetiklemesi sonra bu işlem yürütülemiyor.     
>

### <a name="commit"></a>İşleme
Merhaba doğrulama işlemini tamamladıktan sonra hello geçiş onaylayabilirsiniz. Kaynaklar Klasik dağıtım modelinde artık görünmez ve yalnızca hello Resource Manager dağıtım modelinde kullanılabilir. Merhaba geçirilen kaynakların hello yeni portalında yalnızca yönetilebilir.

> [!NOTE]
> Bu, bir kere etkili olan bir işlemdir. Başarısız olursa hello işlemi yeniden deneyin önerilir. Toofail devam ederse, destek bileti oluşturun veya bir forum oluşturmak üzerinde ClassicIaaSMigration etiketle post bizim [VM Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Merhaba arka planda tamamlama aşamasındadır](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Burada toobegin geçiş?

Gösteren akış grafiği İşte nasıl tooproceed geçiş

![Merhaba geçiş adımlarını gösteren ekran görüntüsü](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Klasik dağıtım modeli tooAzure Resource Manager kaynaklarını çevirisi
Aşağıdaki tablonun hello hello Klasik dağıtım modeli ve Resource Manager gösterimlerini hello kaynakları bulabilirsiniz. Diğer özellikler ve kaynaklar şu an desteklenmemektedir.

| Klasik gösterim | Resource Manager gösterimi | Ayrıntılı notlar |
| --- | --- | --- |
| Bulut hizmeti adı |DNS adı |Geçiş sırasında her bir bulut hizmeti ile Merhaba adlandırma deseni için yeni bir kaynak grubu oluşturulur `<cloudservicename>-migrated`. Bu kaynak grubu tüm kaynaklarınızı içerir. Merhaba bulut hizmeti adı hello ortak IP adresi ile ilişkili bir DNS adı olur. |
| Sanal makine |Sanal makine |Sanal makineye özgü özellikler değiştirilmeden geçirilir. Bilgisayar adı gibi belirli osProfile bilgileri hello Klasik dağıtım modelinde depolanmaz ve geçiş sonrasında boş kalır. |
| Disk kaynakları tooVM bağlı |Örtük diskleri tooVM bağlı |Diskleri en üst düzey kaynak hello Resource Manager dağıtım modeli olarak Modellenen değil. Merhaba VM altında örtük diskleri olarak geçirilir. Olan diskleri VM şu anda desteklenen tooa bağlı. Resource Manager sanal makineleri Klasik depolama hesaplarını hello diskleri toobe herhangi bir güncelleştirme kolayca geçişi sağlayan artık kullanabilirsiniz. |
| VM uzantıları |VM uzantıları |XML uzantıları dışındaki tüm hello kaynak uzantıları hello Klasik dağıtım modelinden geçirilir. |
| Sanal makine sertifikaları |Azure Key Vault’ta Sertifikalar |Bir bulut hizmeti hizmet sertifikaları içeriyorsa, yeni bir Azure anahtar kasası bulut hizmeti ve taşır sertifikaları hello anahtar kasasını hello. Merhaba VM'ler güncelleştirilmiş tooreference hello hello anahtar Kasası'ndan sertifikalardır. <br><br> **Not:** , başarısız bir duruma hello VM toogo neden olabileceği hello keyvault Lütfen silmeyin. Böylece anahtar kasalarını güvenli bir şekilde silindi veya VM tooa yeni abonelik hello birlikte taşınan hello arka uç noktalar geliştirmeye çalışıyoruz. |
| WinRM yapılandırması |osProfile altındaki WinRM yapılandırması |Windows Uzaktan Yönetimi yapılandırma taşınır, değişmeden hello geçişin bir parçası. |
| Kullanılabilirlik kümesi özelliği |Kullanılabilirlik kümesi kaynağı | Kullanılabilirlik kümesi belirtimi hello VM hello Klasik dağıtım modelinde bir özellik oluştu. Kullanılabilirlik kümeleri en üst düzey bir kaynak hello geçiş işleminin parçası olarak haline gelir. Merhaba aşağıdaki yapılandırmaları desteklenmez: kullanılabilirlik kümeleri bulut hizmeti veya bir veya daha fazla kullanılabilirlik kümeleri ile birlikte bir bulut hizmetinde kullanılabilirlik olmayan VM'ler birden fazla. |
| Bir VM’deki ağ yapılandırması |Birincil ağ arabirimi |Bir VM ağ yapılandırmasını geçişten sonra hello birincil ağ arabirimi kaynak olarak temsil edilir. Bir sanal ağda olmayan VM'ler için geçiş sırasında hello iç IP adresini değiştirir. |
| Bir VM’de birden çok ağ arabirimi |Ağ arabirimleri |Bir VM ile ilişkili birden çok ağ arabirimi varsa, her bir ağ arabirimine en üst düzey bir kaynak tüm hello özelliklerinin yanı sıra hello Resource Manager dağıtım modelinde hello geçiş işleminin parçası olarak haline gelir. |
| Yük dengeli uç nokta kümesi |Yük dengeleyici |Merhaba Klasik dağıtım modelinde, her bir bulut hizmeti için örtük yük dengeleyici hello platform atanır. Geçiş sırasında yeni bir yük dengeleyici kaynak oluşturulur ve yük dengeleyici kuralları hello Yük Dengeleme uç nokta kümesi olur. |
| Gelen NAT kuralları |Gelen NAT kuralları |Hello VM üzerinde tanımlanan giriş uç noktaları dönüştürülmüş tooinbound ağ adresi çevirisi hello yük dengeleyici altındaki hello geçiş sırasında kurallardır. |
| VIP adresi |DNS adına sahip genel IP adresi |Merhaba sanal IP adresi genel bir IP adresi olur ve hello yük dengeleyici ile ilişkilidir. Tooit atanmış bir giriş uç noktası ise bir sanal IP yalnızca geçirilebilir. |
| Sanal ağ |Sanal ağ |Merhaba sanal ağ, tüm özellikleriyle birlikte toohello Resource Manager dağıtım modeli geçirilir. Yeni bir kaynak grubu hello adıyla oluşturulur `-migrated`. |
| Ayrılmış IP’ler |Statik ayırma yöntemi kullanan genel IP adresi |Ayrılmış IP'ler Hello yük dengeleyici ile ilişkili geçirilir, hello bulut hizmeti ya da hello sanal makineyi birlikte hello geçişi. İlişkili olmayan ayrılmış IP geçişi şu an desteklenmemektedir. |
| VM başına genel IP adresi |Dinamik ayırma yöntemi kullanan genel IP adresi |VM hello ayırma yöntemi kümesi toostatic sahip ortak bir IP adresi kaynak olarak dönüştürülür hello ilişkili hello genel IP adresi. |
| NSG'ler |NSG'ler |Bir alt ağ ile ilişkilendirilmiş ağ güvenlik grupları hello geçiş toohello Resource Manager dağıtım modelinde bir parçası olarak kopyalandığı. Merhaba NSG hello Klasik dağıtım modelinde hello geçiş sırasında kaldırılmaz. Ancak, Hello geçiş işlemi sürdüğünden, hello Yönetim düzeyi işlemleri hello NSG için engellenir. |
| DNS sunucuları |DNS sunucuları |DNS sunucularının bir sanal ağ ile ilişkilendirilmiş veya hello VM hello karşılık gelen kaynak geçişi, tüm hello özelliklerinin yanı sıra bir parçası olarak geçirilir. |
| UDR’ler |UDR’ler |Bir alt ağ ile ilişkilendirilmiş kullanıcı tanımlı yollar hello geçiş toohello Resource Manager dağıtım modelinde bir parçası olarak kopyalandığı. Merhaba UDR hello Klasik dağıtım modelinde hello geçiş sırasında kaldırılmaz. Merhaba geçiş işlemi sürdüğünden, hello Yönetim düzeyi işlemleri hello UDR için engellenir. |
| Bir sanal makinenin ağ yapılandırmasında IP iletme özelliği |Merhaba NIC özellikte iletme IP |Merhaba IP iletme özelliği bir VM'de dönüştürülmüş tooa hello ağ arabiriminde hello geçiş sırasında özelliğidir. |
| Birden çok IP’si olan yük dengeleyici |Birden çok genel IP kaynağı olan yük dengeleyici |Merhaba yük dengeleyici ile ilişkili her genel IP dönüştürülmüş tooa ortak IP kaynak ve geçiş sonrasında hello yük dengeleyici ile ilişkili. |
| Merhaba VM iç DNS adları |Merhaba NIC iç DNS adları |Geçiş sırasında geçirilen tooa salt okunur özellik hello NIC üzerinde "Dnssettings'de" adlı hello iç DNS sonekleri hello VM'ler için olan Geçişten sonra Hello soneki değişmez ve VM çözümleme olarak daha önce toowork devam etmelidir. |
| Sanal Ağ Geçidi |Sanal Ağ Geçidi |Sanal Ağ Geçidi özellikleri değişmeden geçirilir. Merhaba hello ağ geçidiyle ilişkili VIP ya da değiştirmez. |
| Yerel ağ sitesi |Yerel Ağ Geçidi |Yerel ağ sitesi özellikleri, yerel ağ geçidi olarak adlandırılan geçirilen değişmeden tooa yeni kaynaktır. Bu, şirket içi adres ön eklerini ve uzak ağ geçidi IP’sini temsil eder. |
| Bağlantı başvuruları |Bağlantı |Ağ yapılandırmasında ağ geçidi ile yerel ağ sitesi arasındaki bağlantı başvuruları, geçişten sonra Resource Manager’da yeni oluşturulan Bağlantı adlı bir kaynakla temsil edilir. Tüm ağ yapılandırma dosyalarında bağlantı başvurusu yeni oluşturulan kopyalanan değişmeden toohello bağlantı kaynağı özellikleridir. Klasik VNet tooVNet bağlantısı toolocal ağ siteleri hello sanal ağlar temsil eden iki IPSec tüneli oluşturarak elde edilir. Bu dönüştürülmüş tooVnet2Vnet bağlantısıdır yerel ağ geçitleri gerektirmeden resource manager modelinde türü. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Değişiklikleri tooyour Otomasyonu ve geçiş sonrasında araçları
Kaynaklarınızı hello Klasik dağıtım modeli toohello Resource Manager dağıtım modeli geçiş işleminin parçası olarak, var olan Otomasyon veya onu toowork hello geçişten sonra devam araç tooensure tooupdate sahip.
