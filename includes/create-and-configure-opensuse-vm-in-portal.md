1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com).  
2. Merhaba komut çubuğunda hello pencerenin hello altındaki **yeni**.
3. Altında **işlem**, tıklatın **sanal makine**ve ardından **Galeri'den**.
   
    ![Yeni bir sanal makine oluşturma][Image1]
4. Merhaba altında **SUSE** grup, bir OpenSUSE sanal makine görüntüsü seçin ve hello ok toocontinue'ye tıklayın.
5. Merhaba üzerinde ilk **sanal makine yapılandırması** sayfa:
   
   * Tür a **sanal makine adı**, "testlinuxvm" gibi. Merhaba adı gerekir 3 ile 15 karakter arasında içeren, yalnızca harf, rakam ve tire içerebilir ve gerekir bir harfle başlamalı ve harf veya sayı ile bitmelidir.
   * Merhaba doğrulayın **katmanı** ve çekme bir **boyutu**. Merhaba katmanı aralarından seçim yapabileceğiniz hello boyutları belirler. Merhaba, yanı sıra kaç tane veri diskleri gibi yapılandırma seçeneklerini kullanarak hello maliyetini iliştirebilirsiniz boyutunu etkiler. Ayrıntılar için bkz [sanal makineler için Boyutlar](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Tür a **yeni bir kullanıcı adı**, veya hello varsayılan kabul **azureuser**. Bu ad toohello Sudoers listeyi dosyası eklenir.
   * Hangi tür karar **kimlik doğrulaması** toouse. Genel parola yönergeler için bkz: [güçlü parolalar](http://msdn.microsoft.com/library/ms161962.aspx).
6. Merhaba üzerinde sonraki **sanal makine yapılandırması** sayfa:
   
   * Merhaba varsayılan kullanmak **yeni bir bulut hizmeti oluşturma**.
   * Merhaba, **DNS adı** benzersiz bir DNS adı toouse "testlinuxvm" gibi hello adresi bir parçası olarak yazın.
   * Merhaba, **bölge/benzeşim grubu/sanal ağ** kutusunda, bu sanal görüntü nerede barındırılacağı bir bölge seçin.
   * Altında **uç noktaları**, hello SSH bitiş noktasını saklayın. Başkalarının şimdi, ekleyin veya eklemek, değiştirmek veya hello sanal makine oluşturulduktan sonra silebilirsiniz.
     
     > [!NOTE]
     > Bir sanal makine toouse bir sanal ağ istiyorsanız, **gerekir** hello sanal makine oluşturduğunuzda hello sanal ağ belirtin. Merhaba sanal makineyi oluşturduktan sonra bir sanal makine tooa sanal ağ ekleyemezsiniz. Daha fazla bilgi için bkz: [Virtual Network'e genel bakış](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. Merhaba üzerinde son **sanal makine yapılandırması** sayfasında hello varsayılan ayarları koruyun ve hello onay işareti toofinish'ye tıklayın.

Merhaba portal listeler hello yeni sanal makinenin altında **sanal makineleri**. Merhaba durumu olarak bildirilen sırada **(hazırlama)**, hello sanal makine ayarlanıyor. Ne zaman hello durum bildirilir olarak **çalıştıran**, üzerinde toohello sonraki adıma geçebilirsiniz.

## <a name="connect-toohello-virtual-machine"></a>Toohello sanal makineye bağlanma
SSH veya PuTTY tooconnect toohello sanal makine, gelen bağlanacağım hello bilgisayarda hello işletim sistemine bağlı olarak kullanacaksınız:

* Linux çalıştıran bir bilgisayardan SSH kullanın. Merhaba komut satırına aşağıdakini yazın:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Merhaba kullanıcının parolasını yazın.
* Windows çalıştıran bir bilgisayardan PuTTY kullanın. Yüklü yoksa, hello karşıdan [PuTTY indirme sayfası][PuTTYDownload].
  
    Kaydet **putty.exe** bilgisayarınızda tooa dizin. Bir komut istemi açın, toothat klasörüne gidin ve Çalıştır **putty.exe**.
  
    "Testlinuxvm.cloudapp.net" gibi hello ana bilgisayar adını yazıp hello için "22" **bağlantı noktası**.
  
    ![PuTTY ekran][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Güncelleştirme hello sanal makine (isteğe bağlı)
1. Bağlı toohello sanal makine girdikten sonra sistem güncelleştirmelerini ve düzeltme eklerini isteğe bağlı olarak yükleyebilirsiniz. toorun hello güncelleştirmesi, türü:
   
    `$ sudo zypper update`
2. Seçin **yazılım**, ardından **çevrimiçi güncelleştirme** toolist kullanılabilir güncelleştirmeleri. Seçin **kabul** toostart hello yükleme ve (isteğe bağlı olanları hello dışında) tüm yeni kullanılabilir düzeltme eklerinin uygulayın.
3. Yükleme tamamlandıktan sonra seçin **son**.  Sisteminizin toodate sunulmuştur.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
