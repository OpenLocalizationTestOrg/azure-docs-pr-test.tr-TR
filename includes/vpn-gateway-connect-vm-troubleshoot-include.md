VPN bağlantısı üzerinden tooa sanal makineye bağlanma ile ilgili sorunlar yaşıyorsanız, hello aşağıdakileri denetleyin:

- VPN bağlantınızın başarılı olduğunu doğrulayın.
- Merhaba VM için özel IP adresi toohello bağlandığınızdan emin olun.
- Toohello VM bağlanabiliyorsa hello özel IP kullanan adres, ancak bilgisayar adı Merhaba değil, DNS düzgün şekilde yapılandırdığınızdan emin olun. VM’ler için ad çözümlemesinin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [VM'ler için Ad Çözümlemesi](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Noktası Site bağlandığınızda, aşağıdaki ek öğelerindeki hello denetleyin:

- 'İpconfig' toocheck hello toohello Ethernet Bağdaştırıcısı bağlanmakta olduğunuz hello bilgisayara atanan IPv4 adresini kullanın. Başlangıç IP adresi hello bağlandığınız VNet hello adres aralığı içinde ya da sizin VPNClientAddressPool hello adres aralığı içinde ise, başvurulan tooas çakışan adres alanı budur. Bu şekilde, adres alanı çakışıyor olduğunda hello ağ trafiğini Azure ulaşmak değil, hello yerel ağ üzerinde kalır.
- Merhaba DNS sunucusu IP adreslerini Merhaba VNet belirtilmiş sonra o hello VPN istemcisi yapılandırma paketini oluşturulan doğrulayın. Merhaba DNS sunucusu IP adreslerini güncelleştirdiyseniz oluşturmak ve yeni bir VPN istemcisi yapılandırma paketini yükleyin.

Bir RDP bağlantı sorunlarını giderme hakkında daha fazla bilgi için bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
