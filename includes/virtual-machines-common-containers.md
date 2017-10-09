Azure bulut çözümlerinin altyapısını, yazılım dağıtımlarının çevik olarak paketlenmesine ve kaynakların fiziksel donanımlara göre daha iyi birleştirilmesine imkan tanıyan sanal makineler (fiziksel bilgisayar donanımı öykünmesi) oluşturur. [Docker](https://www.docker.com) kapsayıcıları ve hello docker ekosistemi geliştirme sevk ve dağıtılmış yazılım yönetme önemli ölçüde genişletilmiş hello yolları vardır. Bir kapsayıcı uygulama kodunda VM hello ana bilgisayardan yalıtılmış ve diğer kapsayıcılarında aynı VM hello. Bu yalıtım sayesinde daha fazla geliştirme ve dağıtım çevikliğine sahip olursunuz.

Azure Docker değerleri aşağıdaki hello sunar:

* [Birçok](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [farklı](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yolları toocreate Docker durumunuza kapsayıcıları toosuit barındırır
* Merhaba [Azure kapsayıcı hizmeti](https://azure.microsoft.com/documentation/services/container-service/) orchestrators gibi kullanarak kapsayıcı konak kümeleri oluşturur **marathon** ve **swarm**.
* [Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md) ve [kaynak grubu şablonları](../articles/resource-group-authoring-templates.md) dağıtma ve karmaşık dağıtılmış uygulamalarda güncelleştirme toosimplify
* Hem özel hem de açık kaynaklı bir çok farklı yapılandırma yönetim aracı ile tümleştirme

Ve sanal makineleri ve Linux program aracılığıyla oluşturma kapsayıcıları Azure üzerinde de VM ve kapsayıcı kullanabilirsiniz *orchestration* araçları sanal makineleri (VM'ler) ve hem de Linux toodeploy uygulamalarında toocreate grupları kapsayıcılar ve şimdi [Windows kapsayıcıları](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

Bu kavramlar yüksek bir düzeyde değil yalnızca bu makalede ele, ürünleri Azure toocontainer ve küme kullanımı ile ilgili ve bilgilerin bağlantıları toomore, öğreticiler, ton de içerir. Tüm bu bilmeniz ve yalnızca hello bağlantılar istiyorsanız burada adresindeki olup olmadıklarını [ile kapsayıcıları çalışma araçları](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>sanal makineler ve kapsayıcılar arasındaki Hello fark
Sanal makineler, bir [hiper yönetici](http://en.wikipedia.org/wiki/Hypervisor) tarafından sağlanan yalıtılmış bir donanım sanallaştırma ortamı içinde çalışır. Azure'da hello [sanal makineleri](https://azure.microsoft.com/services/virtual-machines/) hizmet tanıtıcıları tüm bu sizin için: hello işletim sistemi seçme ve yapılandırma sanal makineler oluşturma &mdash;veya özel bir VM görüntüsü yükleyerek. Sanal makineler olduğunda time-tested, "var olma Savaşının sıkı" teknolojisi ve birçok aracı kullanılabilir toomanage hello işletim sistemi ve uygulamaları içerir.  Bir VM uygulamalarında hello konak işletim sistemi gizlenir. Merhaba açısından bir uygulama ya da kullanıcının bir VM'de, hello VM toobe otonom bir fiziksel bilgisayar görünür.

[Linux kapsayıcıları](http://en.wikipedia.org/wiki/LXC) ve bu oluşturulur ve docker araçlarını kullanarak barındırılan kullanmaz hiper yönetici tooprovide yalıtım. İle kapsayıcıları, hello kapsayıcı ana işlem dosya sistemi yalıtım hello Linux çekirdek tooexpose toohello kapsayıcı özelliklerini, kendi uygulamaları, belirli çekirdek özellikleri ve kendi yalıtılmış dosya sistemi kullanır. Merhaba açısından bakıldığında, bir kapsayıcı içinde çalışan bir uygulamanın, hello kapsayıcı toobe benzersiz bir işletim sistemi örneği görüntülenir. Kapsanan bir uygulama, kapsayıcısı dışındaki işlemleri veya diğer kaynakları göremez.

Bir Docker kapsayıcısında, bir VM’dekinden çok daha az kaynak kullanılır. Docker kapsayıcıları, hello çekirdek hello Docker konağının paylaşmaz bir uygulama yalıtımı ve yürütme modeli kullanın. Merhaba kapsayıcı sahip dahil değildir gibi daha düşük disk ayak izini tüm işletim sistemi hello. Bir VM’ye göre başlangıç süresi ve gerekli disk alanı çok daha düşüktür.
Windows kapsayıcılar hello Windows üzerinde çalışan uygulamalar için Linux kapsayıcı olarak aynı avantajları sağlar. Merhaba Docker resim biçimi ve Docker API Windows kapsayıcıları destekler, ancak bunlar ayrıca PowerShell kullanılarak yönetilebilir. Windows Kapsayıcılarıyla iki kapsayıcı çalışma zamanı kullanılabilir: Windows Server Kapsayıcıları ve Hyper-V Kapsayıcıları. Hyper-V Kapsayıcıları, her kapsayıcıyı maksimum düzeyde iyileştirilmiş bir sanal makinede barındırarak fazladan bir yalıtım katmanı sağlar. Windows kapsayıcıları hakkında daha fazla toolearn [hakkında Windows kapsayıcıları](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). Windows Azure, kapsayıcılarında kullanmaya tooget öğrenin nasıl çok[Azure kapsayıcı hizmeti kümesini dağıtma](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Kapsayıcılar hangi alanlarda kullanıma uygundur?

Kapsayıcılar şu iyileştirmeleri yapabilir:

* Merhaba hızı uygulama kodu geliştirilen ve yaygın olarak paylaşılan
* Merhaba hızı ve bir uygulamayı test edilebilir güven
* Merhaba hızı ve bir uygulama dağıtılabilir güven

Kapsayıcılar, bir kapsayıcı konağı (işletim sistemi) ile Azure üzerinde, yani bir Azure Sanal Makinesinde yürütülür. (Olup hello kapsayıcı bir Linux veya Windows istediği rağmen Merhaba kapsayıcılara fikrini zaten memnuniyet Merhaba kapsayıcılara barındırma VM altyapısını tooneed hala oluşturacağız ancak kapsayıcıları değil verdiğiniz hello yararlar şunlardır olsa bile VM çalıştırdıkları Yürütme Ortamı örneğin önemli olacaktır).


## <a name="what-are-containers-good-for"></a>Kapsayıcılar hangi alanlarda kullanıma uygundur?
Pek çok için harika, ancak bunlar teşvik&mdash;gibi [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) ve [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;hello tek hizmet, mikro hizmet odaklı oluşturma dağıtılmış uygulamalar, uygulama, daha fazla küçük, birleştirilebilir bölümleri yerine daha büyük ve daha güçlü bağlı bileşenleri tasarım temel alır.

Bu durum, özellikle de dilediğiniz zaman ve yerde sanal makine kiralayabileceğiniz Azure gibi genel bulut ortamları için geçerlidir. Yalnızca yalıtım, hızlı dağıtım ve düzenleme araçlarına sahip olmakla kalmaz, daha verimli uygulama altyapısı kararları alabilirsiniz.

Örneğin, yüksek oranda kullanılabilir ve dağıtılmış bir uygulama için büyük boyutlu 9 Azure sanal makinesinden bir dağıtımınız var diyelim. Bu uygulamanın Hello bileşenleri kapsayıcılarında dağıtılabilir kullanıyorsanız mümkün toouse yalnızca 4 VM'ler olması ve uygulama bileşenlerinizin artıklık ve Yük Dengeleme için 20 kapsayıcılar içinde dağıtabilirsiniz.

Yalnızca bir örnek doğal olarak, ancak bunu senaryonuzda yapabilirsiniz, daha fazla Azure VM'ler yerine, daha fazla kapsayıcı ile toousage ani ayarlayın ve genel CPU yükünü daha önce çok daha verimli bir şekilde kalan hello kullanın.

Ayrıca, kendilerini tooa mikro yaklaşım ödünç değil birçok senaryo vardır; mikro ve kapsayıcıları yardımcı olacak olup olmadığını en iyi bilirsiniz.

### <a name="container-benefits-for-developers"></a>Geliştiriciler için kapsayıcı avantajları
Genel olarak, bir adım ileri kapsayıcı teknolojidir, ancak daha belirli avantajları da vardır kolay toosee değil. Docker kapsayıcıları hello örneği atalım. Bu konuda iç Docker şimdi daha yakından inceleyin değil (okuma [Docker nedir?](https://www.docker.com/whatisdocker/) bu hikaye için veya [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), ancak Docker ve kendi ekosistemi inanılmaz tooboth geliştiriciler yararlar ve BT uzmanları.

Yukarıdaki tüm Linux ve Windows kapsayıcıları kullanmayı kolaylaştırır çünkü geliştiriciler tooDocker kapsayıcıları hızla alın:

* Basit, artımlı komutları toocreate kolay toodeploy olduğu sabit bir görüntü kullanabilirsiniz ve bir dockerfile kullanarak bu görüntüleri oluşturma otomatik hale getirebilirsiniz
* Bu görüntüleri kolayca basit kullanarak paylaşabilirsiniz [git](https://git-scm.com/)-stil itme ve komutlar çok çekme[ortak](https://registry.hub.docker.com/) veya [özel docker kayıt defterleri](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Bilgisayarlar yerine yalıtılmış uygulama bileşenlerini göz önünde bulundurabiliyorlar
* Docker kapsayıcılarını ve farklı temel görüntüleri anlayan çok sayıda aracı kullanabiliyorlar

### <a name="container-benefits-for-operations-and-it-professionals"></a>İşlemler ve BT uzmanları için kapsayıcı avantajları
BT ve işlemleri uzmanları Merhaba kapsayıcılara ve bileşiminden sanal makineler de yararlanabilir.

* Kapsanan hizmetler sanal makine konak yürütme ortamından yalıtılır
* Kapsanan kod doğrulanabilir şekilde özdeştir
* Kapsanan hizmetler başlatılabilir, durdurulabilir ve geliştirme, test ve üretim ortamları arasında hızla taşınabilir

Bunlar gibi özellikler&mdash;ve daha fazla&mdash;kurulan işletmeler, profesyonel bilgi teknolojisi kuruluşlar hello iş sığdırma kaynakların olduğu toplayan&mdash;saf işleme gücünü dahil olmak üzere&mdash; toohello görevleri gerekli toonot yalnızca iş Kal ancak müşteri memnuniyetini artırmak ve onlara. Küçük işletmeler, ISV ve başlatmalar sahip tam olarak hello aynı gereksinimi, ancak bunlar tanımlamak, farklı.

## <a name="what-are-virtual-machines-good-for"></a>Sanal makineler hangi kullanım alanları için uygundur?
Sanal makineler hello omurga bulut bilgi işlem sağlayın ve bu değiştirmez. Sanal makineler daha yavaş başlatmak, daha büyük bir disk ayak izini varsa ve doğrudan tooa mikro mimarisi eşlemediğinden, bunlar çok önemli avantajlara sahiptir:

1. Varsayılan olarak konak bilgisayar için çok daha dayanıklı varsayılan güvenlik korumalarına sahiptir
2. Önde gelen tüm işletim sistemlerini ve uygulama yapılandırmalarını destekler
3. Komut ve denetim için uzun süredir geliştirilmekte olan bir araç ekosistemleri var
4. Merhaba yürütme ortamı toohost kapsayıcıları sağlarlar

belirli bir işletim sistemine ve CPU türü içerdiği uygulama hala gerektirdiğinden, hello son öğeyi önemlidir Merhaba uygulaması yapacak hello çağrıları bağlı olarak. Bu önemli tooremember toodeploy istediğiniz hello uygulamalarını içerdiklerinden kapsayıcıları Vm'lerinde yükleme olur; kapsayıcıları VM'ler veya işletim sistemleri için değişiklik değildir.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Sanal makineler ile kapsayıcıların üst düzey özellik karşılaştırması
Merhaba aşağıdaki tabloda bir çok yüksek açıklanmaktadır özelliği düzeyi hello tür farkları&mdash;çok fazla iş olmadan&mdash;kapsayıcıları Linux VM'ler arasında mevcut. Kendi uygulama olabilir fazla veya az tercih bağlı olarak bazı özellikler gerekir ve tüm yazılımıyla gibi ek iş sağlar güvenlik hello alanında özellikle özellik desteği artan unutmayın.

| Özellik | VM'ler | Kapsayıcılar |
|:--- | --- | --- |
| "Varsayılan" güvenlik desteği |tooa büyük ölçüde |tooa biraz daha düşük derece |
| Diskte bellek gerekir |Tam işletim sistemi ve uygulamalar |Yalnızca uygulama gereksinimleri |
| Toostart harcanan süre |Önemli Ölçüde Daha Uzun: İşletim sisteminin başlatılması ve uygulamanın yüklenmesi |Önemli ölçüde daha kısa: çekirdek zaten çalıştığından uygulamaları toostart yalnızca |
| Taşınabilirlik |Uygun Hazırlıkla Taşınabilir |Görüntü biçimi içinde taşınabilir; genellikle daha küçüktür |
| Görüntü Otomasyonu |İşletim sistemine ve uygulamalara bağlı olarak büyük oranda değişiklik gösterir |[Docker kayıt defteri](https://registry.hub.docker.com/); diğerleri |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Sanal makine ve kapsayıcı gruplarının oluşturulması ve yönetilmesi
Bu noktada bir mimar, geliştirici ya da BT işlemleri uzmanı "Bunların HEPSİNİ otomatikleştirebilirim; bu GERÇEKTEN Hizmet Olarak Veri Merkezi!" diye düşünüyor olabilir.

Doğru, bu olabilir ve ya da Azure Vm'lerde gruplarını yönetebilir ve komut dosyaları, genellikle ile hello kullanarak özel kod ekleme birçok nedeni zaten kullanıyorsanız, sistemleri, herhangi bir sayıda vardır [CustomScriptingExtension for Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) veya Merhaba [CustomScriptingExtension Linux için](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Azure dağıtımlarınızı PowerShell ya da Azure CLI betiklerini kullanarak otomatikleştirebilirsiniz (bunu daha önce yapmış da olabilirsiniz).

Bu yetenekler sıklıkla olmayan sonra geçirilen tootools ister [Puppet](https://puppetlabs.com/) ve [Chef](https://www.chef.io/) tooautomate hello oluşturulmasını ve ölçekte VM'ler için yapılandırma. (İşte bazı bağlantılar çok[Azure ile bu araçları kullanarak](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Azure kaynak grubu şablonları
Azure hello daha yakın zamanda yayımlanan [Azure kaynak yönetimi](../articles/resource-manager-deployment-model.md) REST API ve güncelleştirilmiş PowerShell ve Azure CLI araçlarını toouse bunu kolayca. Dağıt, değiştirme veya kullanarak tüm uygulama topolojiler dağıtmanız [Azure Resource Manager şablonları](../articles/resource-group-authoring-templates.md) hello Azure kaynak yönetimi API kullanarak:

* Merhaba [şablonları kullanarak Azure portalında](https://github.com/Azure/azure-quickstart-templates)&mdash;ipucu, hello "DeployToAzure" düğmesini kullanın
* Merhaba [Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Azure sanal makine ve kapsayıcı gruplarının bütünlüklü olarak dağıtımı ve yönetimi
Sanal makine gruplarını bütünlüklü olarak dağıtabilen ve bunlara otomatikleştirilebilen bir grup olarak Docker’ı (veya diğer Linux kapsayıcı konak sistemleri) yükleyebilen çeşitli popüler sistemler mevcuttur. Merhaba doğrudan bağlantılar için bkz: [kapsayıcıları ve araçları](#containers-and-vm-technologies) bölümü, aşağıda. Bu tooa küçük veya büyük ölçüde yapmak birkaç sistemleri vardır ve bu liste geniş kapsamlı değildir. Bunlar, becerilerinize ve senaryolarınıza bağlı olarak sizin için kullanışlı olabilir veya olmayabilir.

Docker kendi sanal makine oluşturma araçları ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) kümesine ve yük dengeleyen bir docker kapsayıcı kümesi yönetim aracına ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) sahiptir. Ayrıca, hello [Azure Docker VM uzantısı](https://github.com/Azure/azure-docker-extension/blob/master/README.md) varsayılan desteği ile birlikte [ `docker-compose` ](https://docs.docker.com/compose/), uygulama kapsayıcıları arasında birden çok kapsayıcı yapılandırılmış hangi dağıtabilirsiniz.

Ayrıca, [Mesosphere tarafından sunulan Data Center Operating System (DCOS)](http://docs.mesosphere.com) ürününü deneyebilirsiniz. DCOS hello açık kaynak üzerinde temel [mesos](http://mesos.apache.org/) "merkeziniz adreslenebilir bir hizmet olarak, tootreat sağlayan dağıtılmış sistemlerin çekirdek". DCOS’de [Spark](http://spark.apache.org/) ve [Kafka](http://kafka.apache.org/) (ve diğerleri) gibi çeşitli önemli sistemler ve [Marathon](https://mesosphere.github.io/marathon/) (kapsayıcı denetleme sistemi) ve [Chronos](https://mesos.github.io/chronos/) (dağıtılmış zamanlayıcı) gibi yerleşik hizmetlere yönelik yerleşik paketler vardır. Mesos sistemi Twitter, AirBnb ve diğer web ölçeğindeki işletmelerden alınan derslerden türetilmiştir. Aynı zamanda **swarm** hello düzenleme altyapısı olarak.

Ayrıca, Google’dan alınan derslerden türetilen, sanal makine ve kapsayıcı grubu yönetimi için açık kaynaklı bir sistem olan [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) de kullanılabilir. Hatta kullanabilirsiniz [ile kubernetes weave tooprovide ağ desteği](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) açık bir "Hizmet olarak Platform-a-kolay toodeploy kolaylaştıran" (PaaS) kaynak ve kendi sunucularınızda uygulamalarını yönetme. Docker ve CoreOS tooprovide Heroku neden olacak bir iş akışı ile basit bir PaaS bağlı derlemeleri deis.

Kapladığı alan, Docker desteği ve kendine ait [rkt](https://github.com/coreos/rkt) adlı kapsayıcı sistemiyle iyileştirilmiş bir Linux dağıtımı olan [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), [fleet](https://coreos.com/fleet/docs/latest/) adlı bir kapsayıcı grubu yönetim aracına da sahiptir.

Bir başka popüler Linux dağıtımı olan Ubuntu Docker’ı çok iyi desteklemekle birlikte [Linux (LXC stili) kümelerini](https://help.ubuntu.com/lts/serverguide/lxc.html) de destekler.

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Azure sanal makineleri ve kapsayıcıları ile çalışmaya yönelik araçlar
Kapsayıcılarla ve Azure sanal makineleriyle çalışılırken çeşitli araçlar kullanılır. Bu bölümde hello en kullanışlı veya önemli kavramlar ve kapsayıcılar, gruplar ve hello büyük yapılandırma araçları ve bunlarla kullanılan düzenleme araçları yalnızca bazılarını bir listesini sağlar.

> [!NOTE]
> Bu alan son hızla değişen ve bu konu ve onun bağlantılar toodate bizim en iyi tookeep gerçekleştiririz olsa da, iyi mümkün olmayan bir görev olabilir. Toodate yukarı ilginç konuları tookeep üzerinde arama emin olun!
>
>

### <a name="containers-and-vm-technologies"></a>Kapsayıcılar ve sanal makine teknolojileri
Bazı Linux kapsayıcısı teknolojileri:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS ve rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Windows Kapsayıcısı bağlantıları:

* [Windows Kapsayıcıları](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Visual Studio Docker bağlantıları:

* [Docker için Visual Studio Araçları](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Docker araçları:

* [Docker daemon](https://docs.docker.com/installation/#installation)
* Docker istemcileri
  * [Chocolatey’de Windows Docker İstemcisi](https://chocolatey.org/packages/docker)
  * [Docker yükleme yönergeleri](https://docs.docker.com/installation/#installation)

Microsoft Azure’da Docker:

* [Azure’da Linux için Docker Sanal Makine Uzantısı](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Docker Sanal Makine Uzantısı Kullanıcı Kılavuzu](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Merhaba Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI) gelen kullanma](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Merhaba Docker VM uzantısı hello Azure Portalı'ndan kullanma](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Nasıl toouse docker-Azure makinede](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Nasıl toouse docker swarm azure'da ile](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure’da Docker ve Compose Kullanmaya Başlama](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Bir Azure kaynak grubu şablonu toocreate Docker ana bilgisayar üzerinde Azure hızlı bir şekilde kullanma](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Merhaba için yerleşik destek `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) içerdikleri uygulamalar için
* [Azure’da Docker özel kayıt defteri uygulama](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Linux dağıtımları ve Azure örnekleri:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Yapılandırma, küme yönetimi ve kapsayıcı düzenleme:

* [CoreOS üzerinde Fleet](https://coreos.com/fleet/docs/latest/)
* Deis

  * [CoreOS ve dokuya Kılavuzu tooautomated Kubernetes Küme dağıtımı tamamlandı](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Mesosphere tarafından sunulan Data Center Operating System (DCOS)](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) ve [Hudson](http://hudson-ci.org/)

  * [Azure için Jenkins VM Aracısı eklentisi](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [GitHub deposu: Azure için Jenkins Depolama Eklentisi](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Üçüncü Taraf: Azure için Hudson Bağımlı Eklentisi](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Üçüncü Taraf: Azure için Hudson Depolama Eklentisi](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Otomasyonu](https://azure.microsoft.com/services/automation/)

  * [Video: Nasıl tooUse Linux VM'ler ile Azure Otomasyonu](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Linux için PowerShell DSC

  * [Blog: Nasıl toodo Linux için Powershell DSC](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Docker İstemcisi DSC](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Sonraki adımlar
[Docker](https://www.docker.com) ve [Windows Kapsayıcıları](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)’nı inceleyin.

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
