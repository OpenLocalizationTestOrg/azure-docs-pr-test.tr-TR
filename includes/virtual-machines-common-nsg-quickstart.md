Bir bağlantı noktasını açın ya da bir uç nokta oluşturma tooa bir alt ağ veya VM ağ arabirimine bir ağ filtre oluşturarak azure'da sanal makine (VM). Gelen ve giden trafiği denetleyen bu filtreler hello trafiği alan bir bağlı ağ güvenlik grubu toohello kaynakta yerleştirin.

Bağlantı noktası 80 üzerinde web trafiği yaygın bir örneği kullanalım. Yapılandırılmış tooserve web isteği hello standart TCP bağlantı noktası 80 üzerinde bir VM sahip olduğunda (toostart hello uygun hizmetlerin unutmayın ve tüm işletim sistemi güvenlik duvarı kurallarını da hello VM üzerinde açın), siz:

1. Ağ güvenlik grubu oluşturun.
2. Trafiğe izin bir gelen kuralı oluşturun:
   * "80" Merhaba hedef bağlantı noktası aralığı
   * Kaynak bağlantı noktası aralığını Hello "*" (tüm kaynak bağlantı izin verme)
   * daha az 65,500 (toobe hello varsayılan catch tümünü Reddet gelen kuralı öncelik daha fazla) öncelik değeri
3. Ağ güvenlik grubu Hello hello VM ağ arabirimine veya alt ağ ile ilişkilendirebilirsiniz.

Ağ güvenlik gruplarını ve kurallarını kullanarak, ortamınız karmaşık ağ yapılandırmaları toosecure oluşturabilirsiniz. Bizim örneğimizde HTTP trafiği veya uzaktan yönetim izin yalnızca bir veya iki kurallarını kullanır. Merhaba aşağıdaki daha fazla bilgi için bkz: ['Daha fazla bilgi'](#more-information-on-network-security-groups) bölüm veya [bir ağ güvenlik grubu nedir?](../articles/virtual-network/virtual-networks-nsg.md)

