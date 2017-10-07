---
title: aaaPreparing, ortam tooback Azure sanal makineleri ayarlama | Microsoft Docs
description: "Azure sanal makineleri yedeklemek için ortamınızı hazır olduğundan emin olun"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: yedeklemeleri; Yedekleme;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Azure sanal makineleri yedeklemek, ortam tooback hazırlama
> [!div class="op_single_selector"]
> * [Resource Manager modeli](backup-azure-arm-vms-prepare.md)
> * [Klasik modeli](backup-azure-vms-prepare.md)
>
>

Bir Azure sanal makinesini (VM) yedekleyebilirsiniz önce bulunmalıdır üç koşullar vardır.

* Toocreate bir yedekleme kasası gerekir veya mevcut bir yedekleme kasası tanımlamak *hello içinde VM ile aynı bölgeye*.
* Azure genel Internet adresleri ve Azure depolama uç noktaları hello hello arasında ağ bağlantısı kurun.
* Merhaba VM Aracısı VM hello üzerinde yükleyin.

Bu koşullar zaten ortamınızda mevcut sonra toohello devam biliyorsanız [VM'ler Makalenizi yedekleme](backup-azure-vms.md). Aksi takdirde, okuyun, bu makalede, hello adımları tooprepare, ortam tooback bir Azure VM yukarı götürür.

##<a name="supported-operating-system-for-backup"></a>Yedekleme için desteklenen işletim sistemi
 * **Linux**: Azure Backup, [Azure tarafından onaylanan bir dağıtım listesini](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (CoreOS Linux hariç) destekler. _Diğer Getir-bilgisayarınızı-kendi-Linux dağıtımları da hello VM Aracısı hello sanal makinede kullanılabilir olduğu sürece çalışır ve Python var. desteği. Ancak, biz yedekleme için bu dağıtımları desteklemiyorsanız._
 * **Windows Server**:  Windows Server 2008 R2’den eski sürümler desteklenmez.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Yedekleme ve geri yükleme VM sınırlamaları
> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki dağıtım modeline sahiptir: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Merhaba aşağıdaki listede hello sınırlamaları hello Klasik modelde dağıtırken sağlar.
>
>

* 16'dan fazla veri diskleri içeren sanal makineleri yedekleme desteklenmiyor.
* Ayrılmış bir IP adresi ve tanımlanmış hiçbir uç nokta ile sanal makineleri yedekleme desteklenmiyor.
* Yedekleme verilerini bağlı ağ bağlı sürücüler tooVM içermez.
* Geri yükleme sırasında mevcut bir sanal makinenin değiştirilmesi desteklenmez. Merhaba varolan sanal makine ve ilişkili tüm diskleri silmeniz ve hello verileri yedekten geri yükleyin.
* Çapraz bölge yedekleme ve geri yükleme desteklenmez.
* Hello Azure Yedekleme hizmetini kullanarak sanal makineleri yedekleme tüm ortak Azure bölgelerde desteklenir (Merhaba bkz [denetim listesi](https://azure.microsoft.com/regions/#services) desteklenen bölgeler). Aradığınız hello bölge bugün desteklenmiyorsa, kasa oluşturma sırasında hello açılır listede görünmez.
* Hello Azure Yedekleme hizmetini kullanarak sanal makineleri yedekleme yalnızca select işletim sistemi sürümleri için desteklenir:
* Bir etki alanı denetleyicisini geri multi-DC yapılandırmasının bir parçası olan (DC) VM yalnızca PowerShell aracılığıyla desteklenir. Daha fazla bilgi edinin [multi-DC etki alanı denetleyicisini geri](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Özel ağ yapılandırmaları aşağıdaki hello sahip sanal makineleri geri yüklenmesi yalnızca PowerShell aracılığıyla desteklenir. Hello geri yükleme işlemi tamamlandıktan sonra hello hello geri yükleme iş akışı kullanarak oluşturduğunuz sanal makineleri bu ağ yapılandırmalarının UI sahip olmaz. toolearn daha, fazla [geri VM'ler özel ağ yapılandırmaları ile](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Sanal makineler yük dengeleyici yapılandırması (dahili ve harici)
  * Birden çok ayrılmış IP adreslerine sahip sanal makineler
  * Birden çok ağ bağdaştırıcısı ile sanal makineler

## <a name="create-a-backup-vault-for-a-vm"></a>Bir VM için bir yedekleme kasası oluşturun
Bir yedekleme kasası tüm hello yedeklemeleri ve zaman içinde oluşturulan kurtarma noktalarını depolayan bir varlıktır. Hello yedekleme kasası uygulanan toohello sanal makineler yedeklenen olacaktır hello yedekleme ilkelerini de içerir.

> [!IMPORTANT]
> Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz. Var olan yedekleme kasaları hala desteklenmektedir ve çok mümkündür[Azure PowerShell toocreate yedekleme kasaları kullanmak](./backup-client-automation-classic.md#create-a-backup-vault). Ancak, Microsoft, gelecekteki geliştirmeleri tooRecovery Hizmetleri kasalarının, yalnızca geçerli olduğundan tüm dağıtımlar için kurtarma Hizmetleri kasaları oluşturun önerir.


Bu görüntü çeşitli Azure Backup varlıkları hello hello arasındaki ilişkileri gösterir: ![Azure Backup varlıkları ve ilişkileri](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Ağ bağlantısı
Sipariş toomanage hello VM anlık görüntülerini, bağlantı toohello Azure hello backup uzantısı gereken genel IP adresleri. Merhaba sağ Internet bağlantısı hello sanal makinenin HTTP isteklerini zaman aşımına uğrar ve hello yedekleme işlemi başarısız olur. Dağıtımınızı (örneğin ağ güvenlik grubu (NSG)) aracılığıyla yerinde erişim sınırlamaları varsa, yedekleme trafiği için açık bir yol sağlamak için bu seçeneklerden birini seçin:

* [Beyaz liste hello Azure veri merkezi IP aralıkları](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -toowhitelist hello IP nasıl adresleri hello makaledeki yönergelere bakın.
* Yönlendirme trafiği için bir HTTP proxy sunucusu dağıtın.

Hangi seçeneği toouse karar verirken hello dengelemeler yönetilebilirlik, ayrıntılı bir denetim ve maliyet arasında ' dir.

| Seçenek | Avantajları | Olumsuz yönleri |
| --- | --- | --- |
| Beyaz liste IP aralıkları |Hiçbir ek maliyet.<br><br>Bir NSG erişim açmak için hello kullan <i>kümesi AzureNetworkSecurityRule</i> cmdlet'i. |Karmaşık toomanage etkilenen hello IP aralıkları değişikliği zamanla olarak.<br><br>Azure ve yalnızca depolama toohello tam erişim sağlar. |
| HTTP proxy |Merhaba depolama üzerinde ayrıntılı denetim hello proxy'de URL'lere izin. ayrıntılı bir denetim toosetup hello proxy'de https://\*.blob.core.windows.net/\* URL deseni toobe Güvenilenler listesine gerekiyor. toowhitelist yalnızca VM hello tarafından kullanılan depolama hesabı hello https://\<storageAccount\>.blob.core.windows.net/\* URL deseni toobe Güvenilenler listesine gerekiyor. <br>Tek noktası Internet erişimi tooVMs.<br>TooAzure IP adresi değişiklikleri edilmez. |Bir VM hello Ara yazılımıyla çalıştırmak için ek ücrete. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Beyaz liste hello Azure veri merkezi IP aralıkları
toowhitelist hello Azure veri merkezi IP aralıkları, lütfen hello bakın [Azure Web sitesi](http://www.microsoft.com/en-us/download/details.aspx?id=41653) hello IP aralıkları ve yönergeleri hakkında ayrıntılı bilgi için.

### <a name="using-an-http-proxy-for-vm-backups"></a>VM yedeklemeler için bir HTTP proxy kullanma
VM yedeklemesi zaman hello VM yedekleme uzantısını hello hello anlık görüntü yönetimi komutları tooAzure bir HTTPS API kullanarak depolama gönderir. Merhaba tek bileşen erişim toohello için yapılandırılmış olduğundan hello yedekleme uzantısını trafiğini hello HTTP proxy üzerinden yönlendirmek genel Internet.

> [!NOTE]
> Kullanılması gereken hello ara yazılım için hiçbir öneri yok. Giden sürekliliği olan proxy çekme emin olun ve hello yapılandırma adımları ile uyumludur. Üçüncü taraf program hello proxy ayarlarını değiştirmeyin emin olun
>
>

Aşağıdaki örnek görüntü Hello hello üç yapılandırma adımları gerekli toouse bir HTTP proxy gösterir:

* Uygulama VM yollar tüm HTTP trafiği için ilişkili ortak Internet Proxy VM üzerinden hello.
* Proxy VM hello sanal ağında Vm'lerden gelen trafiğine izin verir.
* Merhaba NSF kilitleme adlı ağ güvenlik grubu (NSG) bir güvenlik kuralı izin giden Internet trafiği Proxy VM gerekir.

![NSG ile HTTP proxy dağıtım diyagramı](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse bir HTTP proxy toocommunicating toohello genel Internet, şu adımları izleyin:

#### <a name="step-1-configure-outgoing-network-connections"></a>1. Adım Giden ağ bağlantılarını yapılandırma
###### <a name="for-windows-machines"></a>Windows makineler için
Bu, yerel sistem hesabı için proxy sunucusu yapılandırmasını Kurulum.

1. Karşıdan [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Yükseltilmiş isteminden şu komutu çalıştırın,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Internet explorer penceresi açar.
3. Git tooTools Internet Seçenekleri -> -> bağlantıları LAN Ayarları ->.
4. Sistem hesabı için proxy ayarlarını doğrulayın. Proxy IP ve bağlantı noktası ayarlayın.
5. Internet Explorer'ı kapatın.

Bu bir makine genelinde proxy yapılandırmasını ayarlanır ve tüm giden HTTP/HTTPS trafiği için kullanılır.

Geçerli kullanıcı hesabında (yerel sistem hesabı değildir) bir proxy sunucu kurulum varsa, komut dosyası tooapply bunları tooSYSTEMACCOUNT hello:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Proxy sunucu oturum açma "(407) Proxy kimlik doğrulaması gerekli" gözlemlerseniz, kimlik doğrulama Kurulumu doğru ayarlandığından emin olun.
>
>

###### <a name="for-linux-machines"></a>Linux makineler için
Satır toohello aşağıdaki hello eklemek ```/etc/environment``` dosyası:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Aşağıdaki satırları toohello hello eklemek ```/etc/waagent.conf``` dosyası:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>2. Adım Gelen bağlantıları hello proxy sunucusuna izin ver:
1. Merhaba proxy sunucusunda, Windows Güvenlik Duvarı'nı açın. Merhaba en kolay yolu tooaccess hello Güvenlik Duvarı'nı Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı toosearch ' dir.

    ![Merhaba Güvenlik Duvarı'nı açın](./media/backup-azure-vms-prepare/firewall-01.png)
2. Merhaba Windows Güvenlik Duvarı iletişim kutusunda sağ **gelen kuralları** tıklatıp **yeni kural...** .

    ![Yeni bir kural oluşturun](./media/backup-azure-vms-prepare/firewall-02.png)
3. Merhaba, **yeni gelen kuralı Sihirbazı**, hello seçin **özel** hello seçeneği **kural türü** tıklatıp **sonraki**.
4. Başlangıç sayfası tooselect hello üzerinde **Program**, seçin **tüm programlar** tıklatıp **sonraki**.
5. Merhaba üzerinde **protokol ve bağlantı noktaları** sayfasında, aşağıdaki bilgilerle hello girin ve tıklatın **sonraki**:

    ![Yeni bir kural oluşturun](./media/backup-azure-vms-prepare/firewall-03.png)

   * için *protokol türü* seçin *TCP*
   * için *yerel bağlantı noktası* seçin *belirli bağlantı noktaları*, aşağıdaki hello alana hello belirtin ```<Proxy Port>``` yapılandırılmış.
   * için *uzak bağlantı noktası* seçin *tüm bağlantı noktaları*

     Merhaba rest hello Sihirbazı'nın tüm hello yolu toohello Sonlandır'ı tıklatın ve bu kural bir ad verin.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>3. Adım Bir özel durum kuralı toohello NSG ekleyin:
Bir Azure PowerShell komut isteminde, komutu aşağıdaki hello girin:

komutu aşağıdaki hello bir özel durum toohello NSG ekler. Bu özel durumun 10.0.0.5 üzerinde herhangi bir bağlantı gelen TCP trafiğine izin verir tooany bağlantı noktası 80 (HTTP) veya 443 (HTTPS) Internet adresi. Belirli bir bağlantı noktası gerekiyorsa ortak Internet olması toohello bağlantı noktası emin tooadd hello ```-DestinationPortRange``` de.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Merhaba ayrıntıları uygun tooyour dağıtımı ile Merhaba örneği hello adları yerine emin olun.*

## <a name="vm-agent"></a>VM Aracısı
Azure sanal makinesi hello yedekleyebilirsiniz önce o hello Azure VM Aracısı hello sanal makineye doğru şekilde yüklendiğinden emin olmalısınız. Merhaba VM Aracısı sanal makine hello hello zaman isteğe bağlı bir bileşen oluşturulan olduğundan hello sanal makine sağlanmadan önce hello VM Aracısı seçili hello onay kutusu emin olun.

### <a name="manual-installation-and-update"></a>El ile yükleme ve güncelleştirme
Merhaba VM Aracısı zaten hello Azure galerisinde ' oluşturulan VM'ler bulunur. Ancak, şirket içi veri merkezlerinden Geçişi sanal makineleri hello VM aracısının yüklü sahip olmaz. Bu tür VM'ler için açıkça yüklü toobe hello VM Aracısı gerekiyor. Daha fazla bilgi edinin [yükleme hello VM Aracısı'nı mevcut bir VM'yi](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **İşlem** | **Windows** | **Linux** |
| --- | --- | --- |
| Merhaba VM Aracısı yükleniyor |<li>Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. <li>[Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. |<li> Merhaba son yükleme [Linux Aracısı](https://github.com/Azure/WALinuxAgent) github'dan. Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. <li> [Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. |
| Merhaba VM Aracısı'nı güncelleştirme |Güncelleştirme hello VM aracısı yeniden yüklemeyi hello kadar basit [VM Aracısı ikili dosyalarının](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Merhaba VM Aracısı güncelleştirilirken herhangi bir yedekleme işleminin çalıştığından emin olun. |Merhaba yönergelerini izleyin [hello Linux VM Aracısı güncelleştirme ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Merhaba VM Aracısı güncelleştirilirken herhangi bir yedekleme işleminin çalıştığından emin olun. |
| Merhaba VM Aracısı yüklemesini doğrulama |<li>Toohello gidin *C:\WindowsAzure\Packages* hello Azure VM klasöründe. <li>Mevcut hello WaAppAgent.exe dosyasını bulmanız gerekir.<li> Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello ürün sürümü alanı 2.6.1198.718 olmalıdır ya da daha yüksek. |Yok |

Merhaba hakkında bilgi edinin [VM Aracısı](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) ve [nasıl tooinstall onu](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Backup uzantısı
tooback hello sanal makineyi hello Azure Backup hizmeti uzantı toohello VM aracısı yükler. Hello Azure Backup hizmeti sorunsuz bir şekilde yükseltilir ve ek kullanıcı müdahalesi olmadan hello yedekleme uzantısını düzeltme ekleri.

Merhaba VM çalışıyorsa hello yedekleme uzantısı yüklenir. Çalışan bir VM ayrıca bir uygulamayla tutarlı bir kurtarma noktası hello büyük olasılığı sağlar. Ancak, hello Azure Backup hizmeti hello VM--yukarı tooback kapalı ve hello uzantısı yüklenemedi olsa bile devam (diğer adıyla çevrimdışı VM) yüklü. Bu durumda, hello kurtarma noktası olur *kilitlenmeyle tutarlı* yukarıda açıklandığı gibi.

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
VM yedeklemesi için ortamınızı hazırlandığınıza göre sonraki mantıksal toocreate bir yedekleme adımdır. makale planlama hello Vm'leri yedekleme konusunda daha ayrıntılı bilgi sağlar.

* [Sanal makineleri yedekleme](backup-azure-vms.md)
* [VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md)
* [Sanal makine yedeklerini yönetme](backup-azure-manage-vms.md)
