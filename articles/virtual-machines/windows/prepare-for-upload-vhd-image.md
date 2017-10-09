---
title: aaaPrepare Windows VHD tooupload tooAzure | Microsoft Docs
description: "Nasıl tooAzure karşıya yüklemeden önce tooprepare Windows VHD veya VHDX"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Bir Windows VHD veya VHDX tooupload tooAzure hazırlama
Bir Windows sanal makinelerden (VM) şirket içi tooMicrosoft Azure karşıya yüklemeden önce hello sanal sabit disk (VHD veya VHDX) hazırlamanız gerekir. Azure hello VHD dosya biçimi'nde ve bir sabit boyutlu disk varsa yalnızca 1. nesil sanal makineleri destekler. Merhaba en büyük boyutu Merhaba VHD 1,023 GB izin verilir. Merhaba VHDX 1 VM'den sistem tooVHD dosyası ve bir dinamik olarak genişletilen gelen toofixed boyutlu disk oluşturma dönüştürebilirsiniz. Ancak, bir sanal makinenin oluşturma değiştiremezsiniz. Daha fazla bilgi için bkz: [kuşak 1 veya 2 oluşturmanız gerekir Hyper-V'de VM](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Azure VM için hello destek ilkesi hakkında daha fazla bilgi için bkz: [Microsoft Azure sanal makineleri için Microsoft sunucu yazılımı desteği](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> Bu makaledeki yönergeleri Hello toohello 64-bit sürümünü Windows Server 2008 R2 ve sonraki Windows server işletim sistemi uygulayın. Azure işletim sisteminde çalışan 32 bit sürümü hakkında daha fazla bilgi için bkz: [Azure sanal makinelerde 32-bit işletim sistemleri için destek](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Merhaba sanal disk tooVHD ve sabit boyutlu disk dönüştürme 
Tooconvert ihtiyacınız varsa, sanal disk toohello biçimi Azure, bu bölümdeki hello yöntemlerden birini kullanın için gereklidir. Merhaba sanal disk dönüştürme işlemi çalıştırın ve bu hello Windows VHD hello yerel sunucuda doğru çalıştığından emin olun önce VM hello yedekleyin. Tooconvert deneyin veya tooAzure karşıya önce hello VM kendisini içindeki tüm hataları giderin.

Merhaba disk dönüştürdükten sonra dönüştürülmüş hello disk kullanan bir VM oluşturun. Başlatma ve oturum açma toohello VM toofinish hello VM karşıya yükleme için hazırlanıyor.

### <a name="convert-disk-using-hyper-v-manager"></a>Hyper-V Yöneticisi'ni kullanarak diski Dönüştür
1. Hyper-V Yöneticisi'ni açın ve yerel bilgisayarınıza hello soldaki seçin. Merhaba bilgisayar listesi yukarıda Hello menüde tıklatın **eylem** > **Düzenle Disk**.
2. Merhaba üzerinde **sanal sabit diski bulma** ekranında, bulun ve sanal disk seçin.
3. Merhaba üzerinde **eylemine** ekran ve ardından **Dönüştür** ve **sonraki**.
4. VHDX gelen tooconvert gereksinim duyarsanız, seçin **VHD** ve ardından **sonraki**
5. Dinamik olarak genişleyen bir diskten tooconvert gereksinim duyarsanız, seçin **boyutu sabit** ve ardından **sonraki**
6. Bulun ve yol toosave hello yeni bir VHD dosyasını seçin.
7. **Son**'a tıklayın.

>[!NOTE]
>Bu makalede Hello komutları yükseltilmiş bir PowerShell oturumunda çalıştırmanız gerekir.

### <a name="convert-disk-by-using-powershell"></a>PowerShell kullanarak diski Dönüştür
Hello kullanarak bir sanal disk dönüştürebilirsiniz [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) Windows PowerShell komutu. Seçin **yönetici olarak çalıştır** PowerShell başlattığınızda. 

Merhaba aşağıdaki örnek komut, bir dinamik olarak genişletilen disk toofixed boyutu ve VHDX tooVHD dönüştürür:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
Bu komutta hello değerini değiştirin "-yolu" Merhaba yolu toohello sanal sabit diskiyle tooconvert ve hello değer için istediğiniz "-HedefYolu" Merhaba yeni yolu ve adı hello ile disk dönüştürülür.

### <a name="convert-from-vmware-vmdk-disk-format"></a>VMware VMDK disk biçiminden Dönüştür
Bir Windows VM görüntüsü hello varsa [VMDK dosya biçimi](https://en.wikipedia.org/wiki/VMDK), hello kullanarak tooa VHD Dönüştür [Microsoft VM dönüştürücüsü](https://www.microsoft.com/download/details.aspx?id=42497). Daha fazla bilgi için hello blog makalesine bakın [nasıl tooConvert VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Azure için Windows yapılandırmalarını ayarlama

Tüm komutları hello aşağıdakileri çalıştırın tooupload tooAzure adımları Hello planladığınız VM üzerinde bir [yükseltilmiş bir komut istemi penceresi](https://technet.microsoft.com/library/cc947813.aspx):

1. Merhaba yönlendirme tablosundaki statik herhangi kalıcı yol kaldırın:
   
   * çalıştırmak, tooview hello rota tablosu `route print` hello komut isteminde.
   * Merhaba denetleyin **Kalıcılık yollar** bölümler. Kalıcı bir yol ise kullanın [rota delete](https://technet.microsoft.com/library/cc739598.apx) tooremove onu.
2. Merhaba WinHTTP proxy kaldırın:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Merhaba disk SAN ilkesi çok ayarlamak[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Merhaba açık komut istemi penceresinde hello aşağıdaki komutları yazın:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Windows için Eşgüdümlü Evrensel Saat (UTC) saati ayarlayın ve hello (w32time) Windows Saat hizmeti başlangıç türü çok hello**otomatik olarak**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Ayarlama hello Güç profili toohello **yüksek performanslı**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Merhaba Windows hizmetlerini denetle
Her Windows Hizmetleri aşağıdaki hello toohello ayarlandığından emin olun **Windows varsayılan değerlerin**. Bunlar hello minimum toomake bu hello VM bağlantısı olduğundan emin olarak ayarlanmalıdır Hizmetleri numaralarıdır. Merhaba aşağıdaki komutları çalıştırın tooreset hello başlangıç ayarları:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Uzak Masaüstü kayıt defteri ayarlarını güncelleştirme
Ayarları aşağıdaki o hello için Uzak Masaüstü Bağlantısı doğru şekilde yapılandırıldığından emin olun:

>[!Note] 
>Merhaba çalıştırdığınızda bir hata iletisi alabilirsiniz **kümesi ItemProperty-yolu ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Hizmetleri - adı &lt;nesne adı&gt; &lt;değeri&gt;** aşağıdaki adımları. Merhaba hata iletisini güvenle yoksayılabilir. Bu, yalnızca o hello etki alanı Grup İlkesi nesnesi aracılığıyla bu yapılandırma Ftp'den değil anlamına gelir.
>
>

1. Uzak Masaüstü Protokolü (RDP) etkinleştirilir:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Merhaba RDP bağlantı noktası ayarlandığından doğru (varsayılan bağlantı noktası 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Bir VM dağıttığınızda, hello varsayılan kuralları 3389 numaralı bağlantı noktasına göre oluşturulur. Toochange hello bağlantı noktası numarası istiyorsanız, Azure'da hello VM dağıtıldıktan sonra yapın.

3. her ağ arabiriminde Hello dinleyicisinin dinleme yaptığı:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Merhaba ağ düzeyinde kimlik doğrulama modu hello RDP bağlantıları için yapılandırın:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Merhaba tutma değerini ayarlayın:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Yeniden bağlanma:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Merhaba eşzamanlı bağlantı sayısını sınırla:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Varsa herhangi bir otomatik olarak imzalanan sertifika toohello RDP dinleyicisini bağlanır, bunları kaldırın:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Bu toomake hello VM dağıttığınızda hello başında bağlanabildiğinden emin olur. Ayrıca bu sonraki aşaması üzerinde VM Azure'da gerekirse dağıtılan hello sonra gözden geçirebilirsiniz.

9. Merhaba VM bir etki alanının parçası olacaksa, tüm ayarları toomake hello eski ayarları değil döndürülür emin aşağıdaki hello denetleyin. denetlenmelidir hello ilkeleri hello şunlardır:
    
    - RDP etkinleştirilir:

         Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\ Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Oturum Ana Bilgisayarı\Bağlantılar:
         
         **Uzak Masaüstü'nü kullanarak kullanıcıların tooconnect uzaktan izin ver**

    - NLA Grup İlkesi:

        Settings\Administrative Templates\Components\Remote Masaüstü Hizmetleri\Uzak Masaüstü Oturumu Ana Bilgisayarı\Güvenlik: 
        
        **Ağ düzeyinde kimlik doğrulama kullanarak uzak bağlantılar için kullanıcı kimlik doğrulaması gerektirir**
    
    - Canlı ayarları tutun:

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Oturum Ana Bilgisayarı\Bağlantılar: 
        
        **Tutma bağlantı aralığını Yapılandır**

    - Ayarları yeniden bağlanın:

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Oturum Ana Bilgisayarı\Bağlantılar: 
        
        **Otomatik yeniden bağlanma**

    - Bağlantı ayarlarını Hello sayısı sınırı:

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Oturum Ana Bilgisayarı\Bağlantılar: 
        
        **Bağlantı sayısını sınırla**

## <a name="configure-windows-firewall-rules"></a>Windows Güvenlik duvarı kurallarını yapılandırma
1. Windows Güvenlik Duvarı'nı üç hello profilleri (etki alanı, standart ve genel) açın:

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Hello üç güvenlik duvarı profilleri (etki alanı, özel ve genel) aracılığıyla PowerShell tooallow WinRM komutunda aşağıdaki hello çalıştırın ve PowerShell uzaktan hizmet hello etkinleştirin:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Güvenlik duvarı kuralları tooallow hello RDP trafiğine aşağıdaki hello etkinleştir 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Merhaba VM tooa ping komutu hello sanal ağ içinde yanıt vermesini sağlayabilirsiniz hello dosya ve yazıcı paylaşımı kuralını etkinleştirin:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Merhaba VM bir etki alanının parçası olacaksa, ayarları toomake hello eski ayarları değil döndürülür emin aşağıdaki hello denetleyin. denetlenmelidir hello AD ilkeleri hello şunlardır:

    - Merhaba Windows Güvenlik duvarı profillerini etkinleştirme

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Güvenlik Duvarı: **tüm ağ bağlantılarını korumaya**

       Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Güvenlik Duvarı: **tüm ağ bağlantılarını korumaya**

    - RDP etkinleştir 

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Güvenlik Duvarı: **gelen Uzak Masaüstü özel durumlara izin ver**

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Güvenlik Duvarı: **gelen Uzak Masaüstü özel durumlara izin ver**

    - ICMP V4 etkinleştir

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Güvenlik Duvarı: **ICMP özel durumlarına izin ver**

        Bilgisayar Yapılandırması\İlkeler\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Güvenlik Duvarı: **ICMP özel durumlarına izin ver**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>VM'yi sağlıklı, güvenli ve RDP ile erişilebilir olduğunu doğrulayın 
1. toomake emin hello disk sağlıklı ve tutarlı, hello sonraki VM yeniden başlatma sırasında bir onay disk işlemini çalıştırın:

    ```PowerShell
    Chkdsk /f
    ```
    Merhaba rapor disk temiz ve Sağlıklı gösterdiğinden emin olun.

2. Merhaba önyükleme yapılandırma verileri (BCD) ayarlar. 

    > [!Note]
    > Yükseltilmiş bir komut penceresinde bu komutları çalıştırdığınızdan emin olun ve **değil** PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Bu hello Windows Yönetim Alt Yapısı'nın deposu tutarlı olduğunu doğrulayın. tooperform komutu aşağıdaki Bu, çalışma hello:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Merhaba deposu bozuk olup [WMI: deposu bozulma veya](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Başka bir uygulama başlangıç bağlantı noktası 3389 kullanmadığından emin olun. Bu bağlantı noktası hello Azure RDP hizmetinde için kullanılır. Çalıştırabilirsiniz **netstat - anob** hangi bağlantı noktalarının içinde kullanılan hello VM üzerinde toosee:

    ```PowerShell
    netstat -anob
    ```

5. Merhaba Windows tooupload istediğiniz VHD bir etki alanı denetleyicisi ise, şu adımları izleyin:

    A. İzleyin [bu ek adımları](https://support.microsoft.com/kb/2904015) tooprepare hello disk.

    B. Belirli bir noktada DSRM modunda toostart hello VM olması durumunda hello DSRM parolasını bildiğinizden emin olun. Toorefer toothis tooset hello bağlamak isteyebilirsiniz [DSRM parolasını](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Merhaba yerleşik yönetici hesabı ve parolası tooyou bilinen emin olun. Tooreset hello geçerli yerel yönetici parolasını istediğiniz ve bu hesabı toosign tooWindows hello RDP bağlantısı üzerinden de kullanabileceğiniz emin olun. Bu erişim izni hello "oturum Uzak Masaüstü Hizmetleri üzerinden izin ver" Grup İlkesi nesnesi tarafından denetlenir. Bu nesne hello yerel Grup İlkesi Düzenleyicisi'ni görüntüleyebilirsiniz altında:

    Bilgisayar Yapılandırması\Windows Ayarları\Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Ataması

7. AD aşağıdaki onay hello toomake RDP erişiminizi RDP aracılığıyla veya hello ağdan engelleme değil emin ilkeler:

    - Bilgisayar Yapılandırması\Windows Ayarları\Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Assignment\Deny erişim toothis hello ağ bilgisayardan

    - Uzak Masaüstü Hizmetleri üzerinden Bilgisayar Yapılandırması\Windows Ayarları\Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Assignment\Deny oturum açma


8. Yeniden başlatma hello VM toomake Windows hala sağlıklı olduğundan emin hello RDP bağlantısı kullanılarak erişilebilir. Bu noktada VM tamamen başlayarak, yerel Hyper-V toomake emin hello toocreate VM istediğiniz ve RDP erişilebilir olup olmadığını sınayın.

9. TCP çözümler yazılım gibi ek bir aktarım sürücüsü arabirimi filtreleri, kaldırma paketler ya da ek güvenlik duvarları. Ayrıca bu sonraki aşaması üzerinde VM Azure'da gerekirse dağıtılan hello sonra gözden geçirebilirsiniz.

10. Herhangi bir üçüncü taraf yazılım ve ilgili toophysical bileşenleri ya da başka bir sanallaştırma teknolojisi sürücü kaldırın.

### <a name="install-windows-updates"></a>Windows güncelleştirmelerini yükleme
Merhaba ideal yapılandırmadır çok**son hello hello makinenin hello düzeltme eki düzeyine sahip**. Bu mümkün değilse, şu güncelleştirmeleri bu hello yüklü olduğundan emin olun:

|                       |                   |           |                                       En düşük dosya sürümü x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Bileşen               | İkili            | Windows 7 ve Windows Server 2008 R2 | Windows 8 ve Windows Server 2012             | Windows 8.1 ve Windows Server 2012 R2 | Windows 10 ve Windows Server 2016 RS1 | Windows 10 RS2             |
| Depolama                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | Storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | NTFS.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | Partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | MSDSM.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Ağ                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | Mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | Tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | HTTP.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Çekirdek                    | Ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Uzak Masaüstü Hizmetleri | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | Termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | Rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Güvenlik                | Son tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Zaman toouse sysprep<a id="step23"></a>    

Sysprep, hello yükleme hello sisteminin sıfırlar ve bir "Merhaba kutu dışı deneyimi" tüm kişisel verilerini kaldırma ve çeşitli bileşenleri sıfırlama sağlayacak bir windows yüklemesinden içine çalışabilecek bir işlemdir. Toocreate istiyorsanız genellikle bunu belirli bir yapılandırmaya sahip birden fazla VM içinden dağıtabileceğiniz bir şablon. Bu adlı bir **görüntü genelleştirilmiş**.

Bunun yerine, yalnızca toocreate bir istiyorsanız, VM bir diskten toouse sysprep yok. Bu durumda, yalnızca ne VM'den olarak bilinir hello oluşturabileceğiniz bir **özel görüntü**.

Özelleştirilmiş bir diskten VM toocreate nasıl gördükleri hakkında daha fazla bilgi için:

- [Özelleştirilmiş bir diskten VM oluşturma](create-vm-specialized.md)
- [Özel bir VHD diskten bir VM oluşturma](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Toocreate genelleştirilmiş bir yansıma istiyorsanız toorun sysprep gerekir. Sysprep hakkında daha fazla bilgi için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx). 

Her rol ya da Windows tabanlı bir bilgisayarda yüklü uygulamayı bu Genelleştirme destekler. Bu nedenle önce bu yordamı çalıştırmadan, makale toomake emin aşağıdaki toohello bakın, bu bilgisayarın bu hello rolü sysprep tarafından desteklenir. Daha fazla bilgi için [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Adımları toogeneralize VHD

>[!NOTE]
> Aşağıdaki adımları belirtilen hello sysprep.exe çalıştırdıktan sonra VM hello devre dışı bırakma ve görüntünün ondan Azure içinde oluşturduğunuz kadar yeniden açmak değil.

1. Toohello Windows VM oturum açın.
2. Çalıştırma **komut istemi** yönetici olarak. 
3. Değişiklik hello dizinine: **%windir%\system32\sysprep**ve ardından çalıştırın **sysprep.exe**.
3. Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.

    ![Sistem Hazırlama Aracı](media/prepare-for-upload-vhd-image/syspre.png)
4. İçinde **kapatma seçenekleri**seçin **kapatma**.
5. **Tamam** düğmesine tıklayın.
6. Sysprep tamamlandığında VM hello kapatın. Kullanmayın **yeniden** tooshut hello VM kapalı.
7. Merhaba VHD karşıya hazır toobe sunulmuştur. Genelleştirilmiş bir diskten VM toocreate nasıl görürüm hakkında daha fazla bilgi için [genelleştirilmiş bir VHD yüklemek ve Azure'da toocreate yeni VM'ler kullanmak](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Önerilen yapılandırmaları tamamlayın
ayarları aşağıdaki hello VHD karşıya etkilemez. Ancak, bunları yapılandırılmış öneririz.

* Merhaba yüklemek [Azure VM Aracısı](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Ardından, VM uzantıları etkinleştirebilirsiniz. Merhaba VM uzantıları, RDP yapılandırma, parola sıfırlama gibi Vm'leriniz ile toouse istediğiniz vb. hello kritik işlevselliğinin uygulayın. Daha fazla bilgi için bkz.

    - [VM aracısı ve uzantılar – bölüm 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [VM aracısı ve uzantılar – bölüm 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* Merhaba döküm günlük Windows kilitlenme sorunları gidermenize yardımcı olabilir. Merhaba döküm günlük toplama etkinleştirin:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Alırsanız hataları sırasında herhangi bir hello yordamsal adımlar bu makalede, bu hello kayıt defteri anahtarlarını zaten anlamına gelir. Bu durumda, komutları bunun yerine aşağıdaki hello kullan:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Azure'da Hello VM oluşturulduktan sonra Başlangıç disk belleği dosyası hello "Zamana bağlı sürücüsü" birim tooimprove performansına put öneririz. Bu aşağıdaki gibi ayarlayabilirsiniz:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Ekli toohello VM hiçbir veri diski ise hello zamana bağlı sürücü birimin sürücü harfi genellikle "D". Bu atama hello sayısı kullanılabilir sürücüleri ve yaptığınız hello ayarlarını bağlı olarak farklı olabilir.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir Windows VM görüntüsünü tooAzure Resource Manager dağıtımları için karşıya yükleme](upload-generalized-managed.md)

