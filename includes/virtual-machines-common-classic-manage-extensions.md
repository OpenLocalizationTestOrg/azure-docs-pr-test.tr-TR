


## <a name="using-vm-extensions"></a>VM uzantıları kullanma
Azure VM uzantıları uygulamak davranışları veya ya da Azure Vm'lerde iş diğer programları yardımcı olan özellikleri (örneğin, hello **WebDeployForVSDevTest** uzantısı, Azure VM dağıtma çözümleri Visual Studio tooWeb sağlar) veya sağlayın başka bir davranışı, toointeract hello VM toosupport ile yeteneği hello (örneğin, PowerShell, hello Azure CLI ve REST istemcileri tooreset hello VM erişimi uzantılarını kullanıyorsanız veya uzaktan erişim değerleri, Azure VM'deki değiştirmek için).

> [!IMPORTANT]
> Uzantılar destekledikleri hello özellikleri için tam bir listesi için bkz: [Azure VM uzantıları ve özellikleri](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Her VM uzantısı belirli bir özelliği desteklediğinden, tam olarak ne yapıp uzantılı olamaz hello uzantısı bağlıdır. Bu nedenle, VM değiştirmeden önce hello toouse istediğiniz VM uzantısı için hello belgelerini okuma emin olun. Bazı VM uzantıları kaldırma desteklenmiyor; diğer VM davranışı tüketicisinin değiştirmek ayarlanabilir özelliklere sahiptir.
> 
> 

Merhaba en yaygın görevleri şunlardır:

1. Kullanılabilir uzantılar bulma
2. Yüklenen uzantıları güncelleştiriliyor
3. Uzantılar ekleme
4. Uzantılarını kaldırma

## <a name="find-available-extensions"></a>Kullanılabilir uzantılar bulun
Uzantı ve genişletilmiş bilgileri kullanarak bulabilirsiniz:

* PowerShell
* Azure platformlar arası komut satırı arabirimi (Azure CLI)
* Hizmet Yönetimi REST API'si

### <a name="azure-powershell"></a>Azure PowerShell
Bazı uzantılar yapılandırmalarını Powershell'den daha kolay hale getirebilir belirli toothem olan PowerShell cmdlet'leri; yine de sahip istiyor musunuz? ancak hello aşağıdaki cmdlet'leri çalışması için tüm VM uzantıları.

Kullanılabilir uzantılar hakkında cmdlet'leri tooobtain bilgi aşağıdaki hello kullanabilirsiniz:

* İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet'i.
* İçin örnekleri sanal makinelerin hello kullanabilirsiniz [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet'i.
  
   Örneğin, kod örnekteki nasıl aşağıdaki hello toolist hello bilgilerini **IaaSDiagnostics** PowerShell kullanarak uzantısı.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Azure komut satırı arabirimi (Azure CLI)
Belirli toothem olan Azure CLI komutlarının bazı uzantılı (Merhaba Docker VM uzantısı olan bir örnek) yapılandırmalarını daha kolay hale getirebilir; ancak tüm VM uzantıları için iş hello aşağıdaki komutları.

Merhaba kullanabilirsiniz **azure vm uzantısı listesinde** komutu kullanılabilir uzantıları tooobtain bilgilerini ve hello kullan **–-json** bir veya daha fazla uzantıları hakkında tüm kullanılabilir bilgi toodisplay seçeneği. Bir uzantı adı kullanmıyorsanız hello komut tüm kullanılabilir uzantıları JSON açıklamasını döndürür.

Örneğin, aşağıdaki kod örneğine hello nasıl toolist hello bilgi hello için gösterir **IaaSDiagnostics** uzantısını kullanarak hello Azure CLI **azure vm uzantısı listesinde** komut ve kullandığı hello **–-json** seçeneği tooreturn tam bilgi.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>Hizmet Yönetimi REST API'leri
Kullanılabilir uzantılar hakkında REST API'leri tooobtain bilgi aşağıdaki hello kullanabilirsiniz:

* İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz [listesi kullanılabilir uzantıları](https://msdn.microsoft.com/library/dn169559.aspx) işlemi. kullanabileceğiniz hello sürümlerinde kullanılabilir uzantıları toolist, [listesi uzantısı sürümleri](https://msdn.microsoft.com/library/dn495437.aspx).
* İçin örnekleri sanal makinelerin hello kullanabilirsiniz [listesi kaynak uzantıları](https://msdn.microsoft.com/library/dn495441.aspx) işlemi. kullanabileceğiniz hello sürümlerinde kullanılabilir uzantıları toolist, [listesi kaynak uzantısı sürümleri](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Ekleme, güncelleştirme ya da uzantılarını devre dışı bırakma
Uzantıları örneği oluşturulduğunda veya örneğini çalıştıran tooa eklenebilir eklenebilir. Uzantıları güncelleştirildi, devre dışı veya kaldırılabilir. Azure PowerShell cmdlet'lerini kullanarak veya hello Hizmet Yönetimi REST API işlemleri kullanarak bu eylemleri gerçekleştirebilir. Parametreler gerekli tooinstall ve bazı uzantıların ayarlayın. Ortak ve özel parametreleri uzantılar için desteklenir.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell cmdlet'lerini kullanarak hello en kolay yolu tooadd ve güncelleştirme uzantıları değildir. Merhaba uzantısı cmdlet'leri kullandığınızda, hello uzantısının hello yapılandırmasının çoğu yapılır sizin için. Bazen gerekebilir tooprogrammatically uzantı ekleyin. Bu toodo gerektiğinde Merhaba uzantısı hello yapılandırmasını sağlamanız gerekir.

Uzantı genel ve özel parametrelerinin yapılandırması sağlanıp sağlanmadığını cmdlet'leri tooknow aşağıdaki hello kullanabilirsiniz:

* İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz **Get-AzureServiceAvailableExtension** cmdlet'i.
* İçin örnekleri sanal makinelerin hello kullanabilirsiniz **Get-AzureVMAvailableExtension** cmdlet'i.

### <a name="service-management-rest-apis"></a>Hizmet Yönetimi REST API'leri
Merhaba REST API'lerini kullanarak kullanılabilir uzantıları listesini almak için yapılandırılmış toobe hello uzantısı nasıl olduğu hakkında bilgi alıyorsunuz. döndürülen hello bilgi ortak şema ve özel şema tarafından temsil edilen parametre bilgilerini gösterebilir. Ortak parametre değerlerini hello örnekleri hakkında sorgularda döndürülür. Özel parametre değerlerini döndürülmez.

Uzantı genel ve özel parametrelerinin yapılandırması sağlanıp sağlanmadığını REST API'leri tooknow aşağıdaki hello kullanabilirsiniz:

* İçin web rolleri veya çalışan rolleri örneklerini hello **PublicConfigurationSchema** ve **PrivateConfigurationSchema** öğeleri içeren hello hello yanıttan hello bilgileri [listesi Kullanılabilir uzantılar](https://msdn.microsoft.com/library/dn169559.aspx) işlemi.
* İçin sanal makine örneklerini hello **PublicConfigurationSchema** ve **PrivateConfigurationSchema** öğeleri içeren hello hello yanıttan hello bilgileri [listesi Kaynak uzantıları](https://msdn.microsoft.com/library/dn495441.aspx) işlemi.

> [!NOTE]
> Uzantılar, JSON ile tanımlanan yapılandırmaları da kullanabilirsiniz. Bu uzantı türlerini kullanıldığında, yalnızca hello **SampleConfig** öğe kullanılır.
> 
> 

