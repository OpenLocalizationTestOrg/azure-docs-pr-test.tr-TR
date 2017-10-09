Önemli toorealize olduğunu iki yolu tooconfigure bir kullanılabilirlik grubu dinleyicisi Azure'da olur. Merhaba yolları hello hello dinleyicisi oluştururken kullandığınız Azure yük dengeleyici türünde farklılık gösterir. Aşağıdaki tablonun hello hello farklar açıklanmaktadır:

| Yük Dengeleyici türü | Uygulama | Şu durumlarda kullanın: |
| --- | --- | --- |
| **Dış** |Kullandığı hello *genel sanal IP adresi* hello sanal makineleri (VM'ler) barındıran hello bulut hizmetinin. |Tooaccess hello dinleyicisi Internet hello dahil dış hello sanal ağı gerekir. |
| **İç** |Kullanan bir *iç yük dengeleyici* hello dinleyici için özel bir adresine sahip. |Merhaba içinde yalnızca hello dinleyicisi erişebilirsiniz aynı sanal ağ. Bu erişim siteden siteye VPN karma senaryolar içerir. |

> [!IMPORTANT]
> Dinleyici için hello bulut hizmetin genel VIP (Dış yük dengeleyici) hello istemci, dinleyiciyi ve veritabanları uzun olan kullandığı aynı Azure bölgesinde Merhaba, çıkış ücret uygulanmaz. Aksi takdirde, herhangi bir veri dinleyicisi çıkış olarak kabul edilir ve normal veri aktarım ücretleri temel alınarak hello döndürdü. 
> 
> 

Bir ILB yalnızca sanal ağları bölgesel kapsama ile yapılandırılabilir. Bir benzeşim grubu için yapılandırılmış olan sanal ağlar bir ILB kullanamazsınız. Daha fazla bilgi için bkz: [iç yük dengeleyiciye genel bakış](../articles/load-balancer/load-balancer-internal-overview.md).

