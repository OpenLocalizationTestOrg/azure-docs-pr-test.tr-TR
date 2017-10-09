Uzak Masaüstü Bağlantısı tooyour VM oluşturarak dağıtılan tooyour VNet olan VM tooa bağlanabilir. Merhaba en iyi şekilde tooinitially doğrulayın VM tarafından tooconnect olan tooyour bağlanabilir kullanarak kendi özel IP adresi, bilgisayar adı yerine. Bu şekilde bağlanabilirsiniz, ad çözümlemesi olup düzgün yapılandırılmamış toosee test ediyorsunuz.

1. Merhaba özel IP adresini bulun. Bir VM hello özel IP adresini ya da hello VM hello Azure portal ile Merhaba özelliklerini bakarak veya PowerShell kullanarak bulabilirsiniz.

  - Azure portal - hello Azure portal, sanal makinenize bulun. Merhaba VM Hello özelliklerini görüntüleyin. Merhaba özel IP adresi listelenir.

  - PowerShell - kullanım hello örnek tooview VM'ler ve kaynak gruplarınızı özel IP adresleri listesi. Kullanmadan önce bu örnek toomodify gerekmez.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Bağlı tooyour hello noktası siteye VPN kullanarak VNet olduğundan emin olun bağlantı.
3. Açık **Uzak Masaüstü Bağlantısı** "RDP" veya "Uzak Masaüstü Bağlantısı" Merhaba görev çubuğunda hello arama kutusuna yazarak, ardından Uzak Masaüstü bağlantısı seçin. Uzak Masaüstü Bağlantısı PowerShell'de hello 'mstsc' komutunu kullanarak da açabilirsiniz. 
4. Uzak Masaüstü Bağlantısı'nda hello VM hello özel IP adresini girin. "Seçenekleri Göster" tooadjust ek ayarlar'ı tıklatın, ardından bağlayın.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot bir RDP bağlantı tooa VM

VPN bağlantısı üzerinden tooa sanal makineye bağlanma ile ilgili sorunlar yaşıyorsanız, hello aşağıdakileri denetleyin:

- VPN bağlantınızın başarılı olduğunu doğrulayın.
- Merhaba VM için özel IP adresi toohello bağlandığınızdan emin olun.
- 'İpconfig' toocheck hello toohello Ethernet Bağdaştırıcısı bağlanmakta olduğunuz hello bilgisayara atanan IPv4 adresini kullanın. Başlangıç IP adresi hello bağlandığınız VNet hello adres aralığı içinde ya da sizin VPNClientAddressPool hello adres aralığı içinde ise, başvurulan tooas çakışan adres alanı budur. Bu şekilde, adres alanı çakışıyor olduğunda hello ağ trafiğini Azure ulaşmak değil, hello yerel ağ üzerinde kalır.
- Toohello VM bağlanabiliyorsa hello özel IP kullanan adres, ancak bilgisayar adı Merhaba değil, DNS düzgün şekilde yapılandırdığınızdan emin olun. VM’ler için ad çözümlemesinin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [VM'ler için Ad Çözümlemesi](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Merhaba DNS sunucusu IP adreslerini Merhaba VNet belirtilmiş sonra o hello VPN istemcisi yapılandırma paketini oluşturulan doğrulayın. Merhaba DNS sunucusu IP adreslerini güncelleştirdiyseniz oluşturmak ve yeni bir VPN istemcisi yapılandırma paketini yükleyin.
- RDP bağlantılarıyla ilgili daha fazla bilgi için bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
