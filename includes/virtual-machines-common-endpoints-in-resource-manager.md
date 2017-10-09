Merhaba yaklaşım tooAzure uç noktaları çalışır biraz farklı şekilde hello Klasik ve Resource Manager dağıtım modelleri arasında. Hello Resource Manager dağıtım modelinde hello Vm'leriniz ve trafik akışını denetleme hello esneklik toocreate ağ filtreleri sahip. Bu filtreler toocreate karmaşık ağ ortamları hello Klasik dağıtım modeli olduğu gibi basit bir uç noktası ötesinde izin verin. Bu makalede, ağ güvenlik grupları ve nasıl Klasik uç noktaları, bunlar filtreleme kuralları, oluşturma kullanmaktan farklı ve örnek dağıtım senaryolarına genel bakış sağlar.

## <a name="overview-of-resource-manager-deployments"></a>Resource Manager dağıtımları genel bakış
Uç noktaları hello Klasik dağıtım modelinde ağ güvenlik grupları tarafından değiştirilir ve erişim denetimi listesi (ACL) kuralları. Ağ güvenlik grubu ACL kuralları uygulamak için hızlı adımlar şunlardır:

* Ağ güvenlik grubu oluşturun.
* tooallow veya trafiği reddetmeye, ağ güvenlik grubu ACL kuralları tanımlayın.
* Ağ güvenlik grubu tooa ağ arabirimi veya sanal ağ alt atayın.

Tooalso isteyen bağlantı noktası iletme gerçekleştirmek, VM'yi önünde tooplace bir yük dengeleyici gerekir ve NAT kurallarını kullanın. Bir yük dengeleyici ve NAT kurallarını uygulamak için hızlı adımlar aşağıdaki gibi olur:

* Bir yük dengeleyicisi oluşturun.
* Bir arka uç havuzu oluşturabilir ve Vm'leri toohello havuzunuzun ekleyebilirsiniz.
* Merhaba gerekli bağlantı noktası iletme için NAT kuralları tanımlayın.
* NAT kuralları tooyour VM'ler atayın.

## <a name="network-security-group-overview"></a>Ağ güvenlik grubu genel bakış
Ağ güvenlik grupları, tooallow belirli bağlantı noktaları için bir güvenlik katmanı ve alt ağları tooaccess Vm'leriniz sağlar. Genellikle her zaman bu VM'ler ve hello world dışında arasında güvenlik katmanı sağlayarak bir ağ güvenlik grubu sahip. Ağ güvenlik grupları uygulanan tooa sanal ağ alt ağı veya belirli bir ağ arabiriminde bir VM için olabilir. Uç nokta ACL kuralları oluşturmak yerine, ağ güvenlik grubu ACL kuralları şimdi oluşturun. Bu ACL kuralları yalnızca bir uç nokta tooforward verilen bağlantı noktası oluşturma daha çok daha fazla denetim sağlar. Daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Ağ güvenlik grupları toomultiple alt ağ veya ağ arabirimleri atayabilirsiniz. 1:1 eşlemesi yok. ACL kuralları ortak bir dizi ağ güvenlik grubu oluşturun ve toomultiple alt ağ veya ağ arabirimleri uygulayın. Ayrıca, ağ güvenlik grubu uygulanan tooresources aboneliğinizi arasında olabilir (temel [rol tabanlı erişim denetimlerini](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Yük Dengeleyici genel bakış
Merhaba Klasik dağıtım modelinde Azure tüm hello ağ adresi çevirisi (NAT) gerçekleştirmek ve sizin için bir bulut hizmeti üzerinde iletme bağlantı noktası. Bir uç nokta oluştururken hello dış bağlantı noktası tooexpose hello iç bağlantı noktası toodirect trafiği için birlikte belirtmeniz gerekir. Ağ güvenlik grupları kendileri tarafından bu aynı NAT ve bağlantı noktası iletme gerçekleştirmeyin. 

tooallow toocreate NAT kuralları iletme, bu tür bağlantı noktası için oluşturduğunuz Azure yük dengeleyici kaynak grubunda. Yeniden hello yük dengeleyici ayrıntılı yeterli tooonly gerekirse toospecific VM'ler uygulayın. Daha fazla esneklik ve bulut Hizmeti uç noktalarını kullanarak ulaşılabilir olandan denetim Hello Azure yük dengeleyici NAT kuralları iş ağ güvenlik grubu ACL kuralları tooprovide yanında. Daha fazla bilgi için bkz: Merhaba [yük dengeleyici genel bakış](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Ağ güvenlik grubu ACL kuralları
ACL kuralları, hangi trafik ve belirli bağlantı noktaları, bağlantı noktası aralıkları veya protokolleri göre VM dışındaki akabilir tanımlamanıza olanak sağlar. Kuralları tooindividual VM'ler veya tooa alt atanır. Ekran aşağıdaki Merhaba, ortak bir Web sunucusu için ACL kuralları örneğidir:

![Ağ güvenlik grubu listesinde ACL kuralları](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

ACL kuralları belirttiğiniz - öncelik ölçüm hello yüksek hello değeri, hello düşük hello önceliği göre uygulanır. Her ağ güvenlik grubu üç varsayılan sahip olan kuralları tasarlanmış toohandle hello açık bir ile Azure ağ trafiği akışını `DenyAllInbound` hello son bir kural olarak. Varsayılan ACL kuralları olan bir düşük öncelik toonot müdahale oluşturduğunuz kurallar.

## <a name="assigning-network-security-groups"></a>Ağ güvenlik grupları atama
Bir ağ güvenlik grubu tooa alt ağ veya ağ arabirimi atayın. Bu yaklaşım toobe tooonly belirli bir VM'de, ACL uygulama kuralları zaman gerektiği gibi ayrıntılı sağlar ya da ortak olun ACL uygulanan tooall bir alt ağın parçası VM'ler kurallar şunlardır:

![Nsg'ler toonetwork arabirimleri veya alt Uygula](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

Ağ güvenlik grubu hello Hello davranışını tooa alt ağı veya bir ağ arabirimine atanmış bağlı olarak değiştirmez. Ortak dağıtım senaryosu tooa alt tooensure uyumluluk tüm VM'ler ekli toothat alt ağın ağ güvenlik grubu atanan hello sahiptir. Daha fazla bilgi için bkz: [ağ güvenliği uygulama grupları tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Ağ güvenlik grupları varsayılan davranışı
Nasıl ve ne zaman, ağ güvenlik grubu oluşturma bağlı olarak, Windows Vm'lerini toopermit RDP erişim 3389 numaralı TCP bağlantı noktası için varsayılan kuralları oluşturulabilir. Linux VM'ler için varsayılan kurallar, TCP bağlantı noktası 22 SSH erişimine. Bu otomatik ACL kuralları koşullar aşağıdaki hello altında oluşturulur:

* Bir Windows VM hello Portalı aracılığıyla oluşturma ve hello varsayılan eylem toocreate bir ağ güvenlik grubu kabul ederseniz, bir ACL kuralı tooallow TCP bağlantı noktası'nın 3389 (RDP) oluşturulur.
* Merhaba portal aracılığıyla bir Linux VM oluşturma ve hello varsayılan eylem toocreate bir ağ güvenlik grubu kabul ederseniz, bir ACL kuralı tooallow TCP bağlantı noktası'nın 22 (SSH) oluşturulur.

Diğer tüm koşullar altında bu varsayılan ACL kuralları oluşturulmaz. Uygun ACL kuralları hello oluşturmadan tooyour VM bağlanamıyor. Bu koşullar Genel eylemleri aşağıdaki hello şunlardır:

* Bir ağ güvenlik grubu hello portal üzerinden ayrı eylemi toocreating hello VM oluşturuluyor.
* Program aracılığıyla PowerShell, Azure CLI, Rest API'leri, vb. ile ağ güvenlik grubu oluşturuluyor.
* Bir VM oluşturma ve önceden tanımlanmış hello uygun ACL kuralı yok ağ güvenlik grubu mevcut tooan atama.

Tüm hello durumlarda önceki toocreate ACL kuralları VM tooallow hello uygun uzak yönetim bağlantılarınız için gerekir.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Ağ güvenlik grubu olmayan bir VM varsayılan davranışı
Bir ağ güvenlik grubu oluşturmadan VM oluşturabilirsiniz. Bu durumlarda tooyour VM bağlanabilir herhangi ACL kuralları oluşturmadan RDP veya SSH kullanarak. Bağlantı noktası 80 üzerinde bir web hizmeti yüklü değilse, benzer şekilde, bu hizmeti uzaktan otomatik olarak erişilebilir. Merhaba VM tüm bağlantı noktalarının açık vardır.

> [!NOTE]
> Yine toohave bir ortak IP adresi atanmış tooa VM tüm uzak bağlantılar için sırayla gerekir. Merhaba alt ağ veya ağ arabirimi için ağ güvenlik grubu olmamasından hello VM tooany dış trafiğin açığa çıkarmıyor. Merhaba portal aracılığıyla bir VM oluşturulurken hello varsayılan toocreate yeni bir ortak IP eylemdir. PowerShell, Azure CLI veya Resource Manager şablonu gibi bir VM oluşturma tüm diğer formları için bir ortak IP otomatik olarak açıkça istenen sürece oluşturulmaz. Merhaba varsayılan hello portal üzerinden de toocreate bir ağ güvenlik grubu eylemdir. Bu varsayılan eylem, yerinde filtreleme hiçbir ağ sahip kullanıma sunulan bir VM ile bir durumda şunun döndürmemelidir anlamına gelir.

## <a name="understanding-load-balancers-and-nat-rules"></a>Yük Dengeleyici ve NAT kurallarını anlama
Merhaba Klasik dağıtım modelinde, ayrıca bağlantı noktası iletme gerçekleştirilen uç noktaları oluşturabilirsiniz. Merhaba Klasik dağıtım modelinde bir VM oluştururken RDP veya SSH için ACL kuralları otomatik olarak oluşturulan. Bu kurallar 3389 numaralı TCP bağlantı noktası veya TCP bağlantı noktası 22 sırasıyla etkilenmez toohello world dışında. Bunun yerine, bir yüksek değerli TCP bağlantı noktası toohello uygun dahili bağlantı noktası eşleşen açık. Benzer şekilde, kendi ACL kuralları da oluşturabilirsiniz, sunmaya gibi bir Web sunucusu numaralı TCP bağlantı noktası 4280 toohello world dışında. Bu ACL kuralları ve bağlantı noktası eşlemelerini hello Klasik Portalı'ndan ekran aşağıdaki hello de görebilirsiniz:

![Bağlantı noktası iletme Klasik uç noktaları](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Ağ güvenlik gruplarıyla, bu bağlantı noktası iletme işlevi bir yük dengeleyici tarafından işlenir. Daha fazla bilgi için bkz: [yük dengeleyici azure'da](../articles/load-balancer/load-balancer-overview.md). Merhaba aşağıdaki örnekte bir NAT kuralı tooperform bağlantı noktası iletme TCP bağlantı noktası 4222 toohello iç TCP bağlantı noktası 22 olan bir yük dengeleyici VM gösterilmektedir:

![Yük Dengeleyici NAT kuralları için bağlantı noktası iletme](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Bir yük dengeleyici uyguladığınızda, genellikle atamama genel bir IP adresi VM kendisini hello. Bunun yerine, bir ortak IP adresi atanmış tooit hello yük dengeleyici sahiptir. Yine toocreate ve bu moddan VM, ağ güvenlik grubu ve ACL kuralları toodefine hello trafik akışını gerekir. Hello yük dengeleyici NAT yalnızca hangi bağlantı noktalarının hello yük dengeleyici ve bunlar hello arka uç VM'ler arasında nasıl dağıtılmış aracılığıyla izin toodefine kurallardır. Bu nedenle, hello yük dengeleyici üzerinden trafik tooflow için toocreate bir NAT kuralı gerekir. tooallow hello trafiği tooreach hello VM, bir ağ güvenlik grubu ACL kuralı oluşturun.
