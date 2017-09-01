Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Yük dengeleyici, gelen trafiği bulut hizmetlerindeki sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

Bir yük dengeleyiciyi aşağıdakileri yapacak şekilde yapılandırabilirsiniz:

* Gelen İnternet trafiği yükünü sanal makineler (VM’ler) arasında dengeleme. Bu senaryodaki bir yük dengeleyiciye [İnternet’e yönelik yük dengeleyici](../articles/load-balancer/load-balancer-internet-overview.md) diyoruz.
* Trafiği bir sanal ağdaki (VNet) VM’ler arasında, bulut hizmetlerindeki VM’ler arasında veya şirket içi bilgisayarlar ile şirketler arası bir sanal ağdaki VM’ler arasında dengeleme. Bu senaryodaki bir yük dengeleyiciye [iç yük dengeleyici (ILB)](../articles/load-balancer/load-balancer-internal-overview.md) diyoruz.
* Dış trafiği belirli bir VM örneğine iletme.
