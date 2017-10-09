Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

Bir yük dengeleyiciyi aşağıdakileri yapacak şekilde yapılandırabilirsiniz:

* Bakiye gelen Internet trafiği toovirtual makineleri (VM'ler) yükleyin. Biz tooa yük dengeleyici Bu senaryoda başvuran bir [Internet'e yönelik Yük Dengeleyici](../articles/load-balancer/load-balancer-internet-overview.md).
* Trafiği bir sanal ağdaki (VNet) VM’ler arasında, bulut hizmetlerindeki VM’ler arasında veya şirket içi bilgisayarlar ile şirketler arası bir sanal ağdaki VM’ler arasında dengeleme. Biz tooa yük dengeleyici Bu senaryoda başvuran bir [iç yük dengeleyiciye (ILB)](../articles/load-balancer/load-balancer-internal-overview.md).
* Dış trafiğin tooa belirli VM örneği iletin.
