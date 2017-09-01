Azure uç noktaları yaklaşımı biraz Klasik ve Resource Manager dağıtım modelleri arasında farklı şekilde çalışır. Resource Manager dağıtım modelinde Vm'leriniz ve trafik akışını denetleme ağ filtreleri oluşturma esnekliğine sahip. Bu filtreler Klasik dağıtım modeli olduğu gibi basit bir uç noktası ötesinde karmaşık ağ ortamları oluşturmanızı sağlar. Bu makalede, ağ güvenlik grupları ve nasıl Klasik uç noktaları, bunlar filtreleme kuralları, oluşturma kullanmaktan farklı ve örnek dağıtım senaryolarına genel bakış sağlar.

## <a name="overview-of-resource-manager-deployments"></a>Resource Manager dağıtımları genel bakış
Uç noktaları Klasik dağıtım modelinde, ağ güvenlik grupları ve erişim denetimi listesi (ACL) kuralları tarafından değiştirilir. Ağ güvenlik grubu ACL kuralları uygulamak için hızlı adımlar şunlardır:

* Ağ güvenlik grubu oluşturun.
* İzin verilen veya reddedilen trafiği için ağ güvenlik grubu ACL kuralları tanımlayın.
* Bir ağ arabirimi veya sanal ağ alt ağ güvenlik grubu atayın.

Ayrıca bağlantı noktası iletme gerçekleştirmek isteyen, bir yük dengeleyici, VM önüne yerleştirin ve NAT kuralları kullanmak üzere gerekir. Bir yük dengeleyici ve NAT kurallarını uygulamak için hızlı adımlar aşağıdaki gibi olur:

* Bir yük dengeleyicisi oluşturun.
* Bir arka uç havuzu oluşturun ve Vm'lerinizi havuzuna ekleyin.
* Gerekli bağlantı noktası iletme için NAT kuralları tanımlayın.
* NAT kuralları, Vm'lere atayın.

## <a name="network-security-group-overview"></a>Ağ güvenlik grubu genel bakış
Ağ güvenlik grupları, belirli bağlantı noktalarını ve alt ağları Vm'leriniz erişmesine izin vermek bir güvenlik katmanı sağlar. Genellikle her zaman bu Vm'leriniz ve dış dünya arasında güvenlik katmanı sağlayarak bir ağ güvenlik grubu sahip. Ağ güvenlik grupları için bir VM sanal ağ alt ağı veya belirli ağ arabirimi için uygulanabilir. Uç nokta ACL kuralları oluşturmak yerine, ağ güvenlik grubu ACL kuralları şimdi oluşturun. Bu ACL kuralları yalnızca belirli bir bağlantı noktasını iletmek için bir uç nokta oluşturma daha çok daha fazla denetim sağlar. Daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Birden çok alt ağları veya ağ arabirimleri için ağ güvenlik grupları atayabilirsiniz. 1:1 eşlemesi yok. ACL kuralları ortak bir dizi ağ güvenlik grubu oluşturun ve birden çok alt ağları veya ağ arabirimleri için geçerlidir. Aboneliğinizi arasında daha fazla ağ güvenlik grubu kaynaklara uygulanabilir (temel [rol tabanlı erişim denetimlerini](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Yük Dengeleyici genel bakış
Azure Klasik dağıtım modelinde, tüm ağ adresi çevirisi (NAT) ve bağlantı noktası sizin için bir bulut hizmetinde iletme gerçekleştirebilirsiniz. Bir uç nokta oluştururken, trafiği yönlendirmek için dahili bağlantı noktası ile birlikte kullanıma sunmak için dış bağlantı noktasını belirtmeniz gerekir. Ağ güvenlik grupları kendileri tarafından bu aynı NAT ve bağlantı noktası iletme gerçekleştirmeyin. 

İletme gibi bağlantı noktası için NAT kuralları oluşturmanıza izin vermek için Azure yük dengeleyici kaynak grubunuzdaki oluşturun. Yine, yük dengeleyici yalnızca belirli VM'ler gerekirse uygulamak için ayrıntılı. Daha fazla esneklik ve bulut Hizmeti uç noktalarını kullanarak ulaşılabilir olandan denetim sağlamak için ağ güvenlik grubu ACL kuralları yanı sıra Azure yük dengeleyici NAT kuralları çalışır. Daha fazla bilgi için bkz: [yük dengeleyici genel bakış](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Ağ güvenlik grubu ACL kuralları
ACL kuralları, hangi trafik ve belirli bağlantı noktaları, bağlantı noktası aralıkları veya protokolleri göre VM dışındaki akabilir tanımlamanıza olanak sağlar. Kuralları tek tek sanal makineleri veya bir alt ağa atanır. Aşağıdaki ekran görüntüsünde, ortak bir Web sunucusu için ACL kuralları örneğidir:

![Ağ güvenlik grubu listesinde ACL kuralları](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

ACL kuralları belirttiğiniz - öncelik ölçüm değer arttıkça, düşük önceliğe göre uygulanır. Her ağ güvenlik grubu açık bir ile Azure ağ trafiği akışını işlemek üzere tasarlanmış üç varsayılan kuralları sahip `DenyAllInbound` son bir kural olarak. Varsayılan ACL kuralları oluşturduğunuz kurallar ile etkileşime değil düşük bir öncelik verilir.

## <a name="assigning-network-security-groups"></a>Ağ güvenlik grupları atama
Bir alt ağ veya ağ arabirimi için ağ güvenlik grubu atayın. Bu yaklaşım, ACL kuralları yalnızca belirli bir VM'yi uygularken gerektiği gibi ayrıntılı veya ACL kuralları ortak bir dizi tüm sanal makineleri bir alt ağın parçası için uygulanan olun sağlar:

![Nsg'leri ağ arabirimlerine veya alt ağlar için geçerlidir](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

Ağ güvenlik grubu davranışını bir alt ağ veya ağ arabirimi atanan bağlı olarak değiştirmez. Yaygın bir dağıtım senaryo o alt ağına bağlı tüm VM'lerin uyumluluğu sağlamak için bir alt ağa atanan ağ güvenlik grubu vardır. Daha fazla bilgi için bkz: [kaynaklar için ağ güvenlik grupları uygulama](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Ağ güvenlik grupları varsayılan davranışı
Nasıl ve ne zaman, ağ güvenlik grubu oluşturma bağlı olarak, TCP bağlantı noktası 3389 üzerinde RDP erişimine izin vermek üzere Windows VM'ler için varsayılan kuralları oluşturulabilir. Linux VM'ler için varsayılan kurallar, TCP bağlantı noktası 22 SSH erişimine. Bu otomatik ACL kuralları aşağıdaki koşullar altında oluşturulur:

* Bir Windows VM Portalı aracılığıyla oluşturma ve bir ağ güvenlik grubu oluşturmak için varsayılan eylem kabul ederseniz, TCP bağlantı noktası 3389 (RDP) izin veren bir ACL kuralı oluşturulur.
* Portal üzerinden bir Linux VM oluşturun ve bir ağ güvenlik grubu oluşturmak için varsayılan eylem kabul ederseniz, TCP bağlantı noktası 22 (SSH) izin veren bir ACL kuralı oluşturulur.

Diğer tüm koşullar altında bu varsayılan ACL kuralları oluşturulmaz. Uygun ACL kuralları oluşturmadan VM'nize bağlanamıyor. Bu koşullar aşağıdaki genel eylemler şunlardır:

* VM oluşturmak için ayrı bir eylem olarak portal üzerinden ağ güvenlik grubu oluşturuluyor.
* Program aracılığıyla PowerShell, Azure CLI, Rest API'leri, vb. ile ağ güvenlik grubu oluşturuluyor.
* Bir VM oluşturma ve var olan ağ güvenlik zaten tanımlı uygun ACL kuralı olmayan grubuna atama.

Tüm önceki durumlarda, uygun uzaktan yönetim bağlantılara izin vermek, VM için ACL kuralları oluşturmanız gerekir.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Ağ güvenlik grubu olmayan bir VM varsayılan davranışı
Bir ağ güvenlik grubu oluşturmadan VM oluşturabilirsiniz. Bu durumlarda, ACL kuralları oluşturmadan RDP veya SSH kullanarak VM bağlanabilirsiniz. Bağlantı noktası 80 üzerinde bir web hizmeti yüklü değilse, benzer şekilde, bu hizmeti uzaktan otomatik olarak erişilebilir. VM tüm bağlantı noktalarının açık vardır.

> [!NOTE]
> Hala bir VM sırada tüm uzak bağlantılar için atanan genel bir IP adresi olması gerekir. Alt ağ veya ağ arabirimi için ağ güvenlik grubu olmaması, herhangi bir dış trafiği VM'ye açığa çıkarmıyor. Yeni bir genel IP Portalı aracılığıyla bir VM oluştururken, varsayılan eylem oluşturulmasıdır. PowerShell, Azure CLI veya Resource Manager şablonu gibi bir VM oluşturma tüm diğer formları için bir ortak IP otomatik olarak açıkça istenen sürece oluşturulmaz. Ayrıca varsayılan eylem portal üzerinden bir ağ güvenlik grubu oluşturmaktır. Bu varsayılan eylem, yerinde filtreleme hiçbir ağ sahip kullanıma sunulan bir VM ile bir durumda şunun döndürmemelidir anlamına gelir.

## <a name="understanding-load-balancers-and-nat-rules"></a>Yük Dengeleyici ve NAT kurallarını anlama
Klasik dağıtım modeli de bağlantı noktası iletme gerçekleştirilen uç noktaları oluşturabilirsiniz. Klasik dağıtım modelinde bir VM oluştururken RDP veya SSH için ACL kuralları otomatik olarak oluşturulan. Bu kurallar, TCP bağlantı noktası 3389 veya TCP bağlantı noktası 22 sırasıyla dış dünya etkilenmez. Bunun yerine, bir yüksek değerli TCP bağlantı noktası uygun iç bağlantı noktasına eşlenen açık. Benzer şekilde, sunmaya TCP bağlantı noktası 4280 dış dünya üzerindeki bir Web sunucusu gibi kendi ACL kuralları da oluşturabilirsiniz. Bu ACL kuralları ve bağlantı noktası eşlemelerini Klasik Portalı'ndan aşağıdaki ekran görüntüsünde görebilirsiniz:

![Bağlantı noktası iletme Klasik uç noktaları](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Ağ güvenlik gruplarıyla, bu bağlantı noktası iletme işlevi bir yük dengeleyici tarafından işlenir. Daha fazla bilgi için bkz: [yük dengeleyici azure'da](../articles/load-balancer/load-balancer-overview.md). Aşağıdaki örnek, bir VM iç TCP bağlantı noktası 22 bağlantı noktası iletme TCP bağlantı noktası 4222 gerçekleştirmek için NAT kuralı ile bir yük dengeleyici gösterir:

![Yük Dengeleyici NAT kuralları için bağlantı noktası iletme](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Bir yük dengeleyici uyguladığınızda, genellikle bir genel IP adresi VM atamayın. Bunun yerine, yük dengeleyici kendisine atanmış bir ortak IP adresi vardır. Hala VM'nizi ve trafik akışını tanımlamak için ağ güvenlik grubu ve ACL kuralları oluşturmanız gerekir. Yük Dengeleyici NAT kuralları yalnızca yük dengeleyici üzerinden hangi bağlantı noktalarına izin verilir ve bunlar VM'ler arka uç arasında nasıl dağıtılmış tanımlayın üzeresiniz. Bu nedenle, yük dengeleyici üzerinden akışına için NAT kuralı oluşturmanız gerekir. VM ulaşmak trafiğe izin veren bir ağ güvenlik grubu ACL kuralı oluşturun.
