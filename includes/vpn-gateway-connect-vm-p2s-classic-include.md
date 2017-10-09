Uzak Masaüstü Bağlantısı tooyour VM oluşturarak dağıtılan tooyour VNet olan VM tooa bağlanabilir. Merhaba en iyi şekilde tooinitially doğrulayın VM tarafından tooconnect olan tooyour bağlanabilir kullanarak kendi özel IP adresi, bilgisayar adı yerine. Bu şekilde bağlanabilirsiniz, ad çözümlemesi olup düzgün yapılandırılmamış toosee test ediyorsunuz. 

1. Merhaba özel IP adresi, VM için bulun. Bir VM hello özel IP adresini ya da hello VM hello Azure portal ile Merhaba özelliklerini bakarak veya PowerShell kullanarak bulabilirsiniz.
2. Bağlı tooyour hello noktası siteye VPN kullanarak VNet olduğundan emin olun bağlantı. 
3. Uzak Masaüstü Bağlantısı hello görev çubuğunda hello arama kutusuna "RDP" veya "Uzak Masaüstü Bağlantısı" yazarak açın, ardından Uzak Masaüstü bağlantısı seçin. Uzak Masaüstü Bağlantısı PowerShell'de hello 'mstsc' komutunu kullanarak da açabilirsiniz. 
3. Uzak Masaüstü Bağlantısı'nda hello VM hello özel IP adresini girin. "Seçenekleri Göster" tooadjust ek ayarlar'ı tıklatın, ardından bağlayın.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot bir RDP bağlantı tooa VM

VPN bağlantısı üzerinden tooa sanal makineye bağlanma ile ilgili sorunlar yaşıyorsanız, kontrol edebilirsiniz birkaç nokta vardır. Daha fazla sorun giderme bilgileri için bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- VPN bağlantınızın başarılı olduğunu doğrulayın.
- Merhaba VM için özel IP adresi toohello bağlandığınızdan emin olun.
- 'İpconfig' toocheck hello toohello Ethernet Bağdaştırıcısı bağlanmakta olduğunuz hello bilgisayara atanan IPv4 adresini kullanın. Başlangıç IP adresi hello bağlandığınız VNet hello adres aralığı içinde ya da sizin VPNClientAddressPool hello adres aralığı içinde ise, başvurulan tooas çakışan adres alanı budur. Bu şekilde, adres alanı çakışıyor olduğunda hello ağ trafiğini Azure ulaşmak değil, hello yerel ağ üzerinde kalır.
- Toohello VM bağlanabiliyorsa hello özel IP kullanan adres, ancak bilgisayar adı Merhaba değil, DNS düzgün şekilde yapılandırdığınızdan emin olun. VM’ler için ad çözümlemesinin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [VM'ler için Ad Çözümlemesi](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Merhaba DNS sunucusu IP adreslerini Merhaba VNet belirtilmiş sonra o hello VPN istemcisi yapılandırma paketini oluşturulan doğrulayın. Merhaba DNS sunucusu IP adreslerini güncelleştirdiyseniz oluşturmak ve yeni bir VPN istemcisi yapılandırma paketini yükleyin.
