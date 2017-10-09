---
title: "aaaConfigure hello Always On kullanılabilirlik grubu PowerShell kullanarak Azure VM'de | Microsoft Docs"
description: "Bu öğretici hello Klasik dağıtım modeliyle oluşturulan kaynakları kullanır. Azure PowerShell toocreate Always On kullanılabilirlik grubu kullanın."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>PowerShell ile Azure VM'de Hello Always On kullanılabilirlik grubu yapılandırma
> [!div class="op_single_selector"]
> * [Klasik: kullanıcı Arabirimi](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klasik: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Başlamadan önce Azure resource manager modelinde bu görevi tamamlamak olduğunu göz önünde bulundurun. Azure resource manager modeli yeni dağıtımlar için öneririz. Bkz: [SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerinde](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz. Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.

Azure sanal makineleri (VM'ler) Veritabanı yöneticileri toolower hello maliyeti yüksek kullanılabilirlik SQL Server sistem yardımcı olabilir. Bu öğretici nasıl tooimplement bir kullanılabilirlik grubu SQL Server Always On uçtan uca bir Azure ortamı içindeki kullanarak gösterir. Başlangıç Öğreticisi Hello sonunda, Azure, SQL Server Always On çözümünüz öğeleri aşağıdaki Merhaba oluşur:

* Bir ön uç dahil olmak üzere birden çok alt ağı ve bir arka uç alt ağ içeren bir sanal ağ.
* Bir Active Directory etki alanı ile etki alanı denetleyicisi.
* Dağıtılan toohello arka uç alt ağı ve Active Directory etki alanına katılmış toohello olan iki SQL Server Vm'lerinin.
* Üç düğümlü Windows Yük devretme kümesi hello düğüm çoğunluğu çekirdek modeli.
* Bir kullanılabilirlik veritabanının bir kullanılabilirlik grubu iki synchronous-commit çoğaltmalarından ile.

Bu senaryo olduğunda, düşük maliyet veya diğer etkenlere bağlı için değil, Azure üzerinde kendi Basitlik için iyi bir seçimdir. Örneğin, VM'ler hello sayısı iki çoğaltma kullanılabilirlik grubu toosave için işlem saatlerinde azure'da hello etki alanı denetleyicisi hello çekirdek dosya paylaşım tanığı bir iki düğümlü yük devretme kümesi olarak kullanarak en aza indirebilirsiniz. Bu yöntem yapılandırma yukarıda hello birinden tarafından hello VM sayısını azaltır.

Bu öğreticide gerekli tooset hello ayarlama adımları hello tooshow her adımı hello ayrıntılarını elaborating olmadan çözüm, yukarıda açıklanan amaçlar. İsteğe bağlı olarak Hello GUI yapılandırma adımları, PowerShell tootake komut dosyası kullanan sağlanması bu nedenle, yerine hızlı bir şekilde ile her adımı. Bu öğretici hello aşağıdakileri varsayar:

* Bir Azure hesabı hello sanal makine abonelik zaten var.
* Merhaba yüklediğiniz [Azure PowerShell cmdlet'lerini](/powershell/azure/overview).
* Always On kullanılabilirlik grupları şirket içi çözümler için sağlam bir anlayış zaten var. Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Tooyour Azure aboneliğini bağlama ve hello sanal ağ oluşturma
1. Bir PowerShell penceresinde, yerel bilgisayarınızda hello Azure modülü içe ayarları dosyası tooyour makine yayımlama hello indirin ve indirilen hello yayımlama ayarlarını içeri aktararak, PowerShell oturumu tooyour Azure aboneliği bağlanın.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Merhaba **Get-AzurePublishSettingsFile** komutu otomatik olarak Azure yönetim sertifikasıyla oluşturur ve tooyour makine indirir. Bir tarayıcı otomatik olarak açılır ve istendiğinde tooenter hello Microsoft hesap kimlik bilgilerini Azure aboneliğiniz için demektir. indirilen hello **.publishsettings** dosyası, Azure aboneliğinizin toomanage gereken tüm hello bilgiler içerir. Bu dosya tooa yerel dizin kaydedildikten sonra bunu hello kullanarak içeri **Import-AzurePublishSettingsFile** komutu.

   > [!NOTE]
   > Merhaba .publishsettings dosyasını Azure Abonelikleriniz ve hizmetleri kullanılan tooadminister (kodlanmamış), kimlik bilgilerini içerir. Bu dosya için güvenlik en iyi uygulama Hello olan toostore (örneğin, klasöründe hello Libraries\Documents), kaynak dizinlerinizi dışında geçici olarak ve hello içeri aktarma tamamlandıktan sonra silin. Erişim toohello .publishsettings dosyasını kazanır kötü niyetli bir kullanıcı düzenleme, oluşturma ve Azure hizmetlerinizi silin.

2. Bir dizi bulut BT altyapısı toocreate kullanacağınız değişkenleri tanımlayın.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Komutlarınızı daha sonra başarılı olur tooensure aşağıdaki dikkat toohello ödeme:

   * Değişkenleri **$storageAccountName** ve **$dcServiceName** oldukları için benzersiz olmalıdır tooidentify bulut depolama hesabı ve bulut sunucusu, sırasıyla hello Internet üzerinde kullanılan.
   * Merhaba değişkenleri belirtir adları **$affinityGroupName** ve **$virtualNetworkName** daha sonra kullanacağınız hello sanal ağ yapılandırması belgede yapılandırılır.
   * **$sqlImageName** , SQL Server 2012 Service Pack 1 Enterprise Edition içeren hello VM görüntüsü güncelleştirilmiş hello adını belirtir.
   * Basitleştirmek için **Contoso! 000** olduğundan, hello aynı hello tüm Öğreticisi kullanılan parola.

3. Bir benzeşim grubu oluşturun.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Bir yapılandırma dosyasını içeri aktararak bir sanal ağ oluşturun.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    XML belgesi aşağıdaki hello Hello yapılandırma dosyası içerir. Kısaca, adlı bir sanal ağ belirtir **ContosoNET** hello benzeşim adlı grubundaki **ContosoAG**. Merhaba adres alanına sahip **10.10.0.0/16** ve iki alt ağa sahip **10.10.1.0/24** ve **10.10.2.0/24**, olan hello ön alt ağı ve geri alt ağ, sırasıyla. Burada, Microsoft SharePoint gibi istemci uygulamalarını yerleştirebilirsiniz Hello ön alt ağıdır. Merhaba SQL Server Vm'lerinin nereye Hello geri alt ağıdır. Merhaba değiştirirseniz **$affinityGroupName** ve **$virtualNetworkName** değişkenleri daha önce de değiştirmelisiniz adları karşılık gelen hello.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Merhaba benzeşim oluşturulur ve aboneliğinizde hello geçerli depolama hesabı olarak ayarlanmış grubu ile ilişkili bir depolama hesabı oluşturun.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Merhaba etki alanı denetleyicisi sunucusuna hello yeni bulut hizmeti ve kullanılabilirlik kümesinde oluşturun.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Bu piped komutları şeyleri hello:

   * **AzureVMConfig yeni** bir VM yapılandırması oluşturur.
   * **Ekleme AzureProvisioningConfig** verir hello bir tek başına Windows server'ın yapılandırma parametreleri.
   * **Ekleme AzureDataDisk** seçenek kümesi tooNone önbelleğe alma hello ile Active Directory verilerini depolamak için kullanacağınız hello veri diski ekler.
   * **Yeni-AzureVM** yeni bir bulut hizmeti ve oluşturur Yeni Azure VM hello yeni bulut hizmeti ile Merhaba.

7. Tam olarak sağlanan hello yeni VM toobe için bekleyin ve hello Uzak Masaüstü dosyası tooyour çalışma dizini indirin. Merhaba yeni Azure VM uzun süre tooprovision aldığından hello `while` döngünün devam toopoll kullanıma hazır olana kadar yeni VM hello.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

Merhaba etki alanı denetleyici sunucusu artık başarıyla kaynak sağlandı. Ardından, bu etki alanı denetleyicisi sunucusuna hello Active Directory etki alanı yapılandıracaksınız. Yerel bilgisayarınızda Hello PowerShell penceresini açık bırakın. Kullanacağınız yeniden sonraki toocreate hello iki SQL Server VM.

## <a name="configure-hello-domain-controller"></a>Merhaba etki alanı denetleyicisini Yapılandır
1. Merhaba Uzak Masaüstü dosyası başlatarak toohello etki alanı denetleyicisi sunucusuna bağlanın. Merhaba makine yöneticisinin AzureAdmin kullanıcı adı ve parolası kullanmak **Contoso! 000**, oluşturduğunuzda belirttiğiniz yeni VM hello.
2. Yönetici modunda bir PowerShell penceresi açın.
3. Merhaba aşağıdaki komutu çalıştırarak **DCPROMO. EXE** hello yukarı komutu tooset **corp.contoso.com** M sürücüsü hello veri dizinleri ile etki alanı.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Merhaba VM Hello komut bittikten sonra otomatik olarak yeniden başlatılır.

4. Merhaba Uzak Masaüstü dosyası başlatarak toohello etki alanı denetleyicisi sunucusuna yeniden bağlanın. Bu süre olarak oturum açın **CORP\Administrator**.
5. Yönetici modunda bir PowerShell penceresi açın ve komut aşağıdaki hello kullanarak hello Active Directory PowerShell modülünü içeri aktarın:

        Import-Module ActiveDirectory

6. Aşağıdaki komutları tooadd üç kullanıcılar toohello etki alanı hello çalıştırın.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** kullanılan tooconfigure her şeyi olan ilgili toohello SQL Sunucu hizmeti örneği, hello yük devretme kümesi ve hello kullanılabilirlik grubu. **CORP\SQLSvc1** ve **CORP\SQLSvc2** hello SQL Server hizmet hesabı olarak hello iki SQL Server VM'ler için kullanılır.
7. Ardından, çalışma hello aşağıdaki komutları toogive **CORP\Install** hello hello etki alanındaki izinleri toocreate bilgisayar nesneleri.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Merhaba yukarıda belirtilen GUID hello GUID hello bilgisayar nesnesi türü için ' dir. Merhaba **CORP\Install** hesabının gerekir hello **tüm özellikleri oku** ve **bilgisayar nesneleri oluşturma** izin toocreate hello etkin doğrudan hello yük devretme için nesneleri Küme. Merhaba **tüm özellikleri oku** izni zaten verilen tooCORP\Install varsayılan olarak, yani toogrant gerekiyor mu, açıkça. İzinler hakkında daha fazla bilgi toocreate hello yük devretme küme gerektiği için bkz: [yük devretme kümesi adım adım Kılavuzu: Active Directory hesaplarını yapılandırma](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Active Directory ve hello kullanıcı nesneleri yapılandırma bitirdikten sonra iki SQL Server VM oluşturun ve bunları toothis etki alanına katılma.

## <a name="create-hello-sql-server-vms"></a>Merhaba SQL Server Vm'lerinin oluşturma
1. Yerel bilgisayarınızda açık toouse hello PowerShell penceresi devam edin. Ek değişkenler aşağıdaki hello tanımlayın:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    Merhaba IP adresi **10.10.0.4** toohello genellikle atanan hello oluşturduğunuz ilk VM **10.10.0.0/16** Azure sanal ağınızın alt ağ. Bu etki alanı denetleyicisi sunucunuzun hello adresini çalıştırarak olduğunu doğrulamalısınız **IPCONFIG**.
2. Yöneltilen komutları toocreate hello önce aşağıdaki çalışma hello hello yük devretme kümesinde, VM adlı **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Yukarıdaki hello komutu ilgili Hello aşağıdakileri göz önünde bulundurun:

   * **AzureVMConfig yeni** hello istenen kullanılabilirlik kümesi adı ile bir VM yapılandırması oluşturur. Merhaba sonraki VM'ler ile Merhaba aynı oluşturulacak kullanılabilirlik kümesi adı birleştirilmiş böylece toohello aynı kullanılabilirlik kümesi.
   * **Ekleme AzureProvisioningConfig** birleştirmeler hello oluşturduğunuz VM toohello Active Directory etki alanı.
   * **Set-AzureSubnet** hello geri alt ağda yer hello VM.
   * **Yeni-AzureVM** yeni bir bulut hizmeti ve oluşturur Yeni Azure VM hello yeni bulut hizmeti ile Merhaba. Merhaba **DnsSettings** parametresi belirtir hello DNS sunucu hello hello yeni bulut hizmetindeki sunucular için başlangıç IP adresi **10.10.0.4**. Başlangıç IP adresi hello etki alanı denetleyici sunucusu budur. Bu parametre gerekli tooenable hello hello bulut hizmeti toojoin toohello Active Directory etki alanındaki yeni VM'ler başarıyla. Merhaba VM sağlanır ve hello VM toohello Active Directory etki alanına katılma sonra bu parametre olmadan, el ile Merhaba IPv4 ayarları VM toouse hello etki alanı denetleyicisi sunucunuzda hello birincil DNS sunucusu olarak ayarlamanız gerekir.
3. Çalışma hello yöneltilen aşağıdaki komutları adlı toocreate hello SQL Server Vm'lerinin **ContosoSQL1** ve **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Yukarıdaki hello komutları ilgili Hello aşağıdakileri göz önünde bulundurun:

   * **AzureVMConfig yeni** kullandığı hello hello etki alanı denetleyici sunucusu olarak aynı kullanılabilirlik kümesi adı ve kullandığı hello hello sanal makine Galerisi SQL Server 2012 Service Pack 1 Enterprise Edition görüntüde. Ayrıca, işletim sistemi disk tooread (hiçbir yazma önbelleğini) önbelleğe alma yalnızca hello ayarlar. Toohello VM eklemek ve okuma ile yapılandırmak veya önbelleğe alma yazma olduğunu hello veritabanı dosyaları tooa ayrı veri diski yükseltmenizi öneririz. Ancak, hello sonraki en iyi, kaldırılamıyor çünkü tooremove hello işletim sistemi diskte yazma önbelleğini hello işletim sistemi disk üzerinde okuma şeydir.
   * **Ekleme AzureProvisioningConfig** birleştirmeler hello oluşturduğunuz VM toohello Active Directory etki alanı.
   * **Set-AzureSubnet** hello geri alt ağda yer hello VM.
   * **Ekleme AzureEndpoint** istemci uygulamalarının bu SQL Server Hizmetleri örnekleri hello Internet üzerinde erişebilmesi için erişim uç noktaları ekler. Farklı bağlantı noktaları tooContosoSQL1 ve ContosoSQL2 verilir.
   * **Yeni-AzureVM** oluşturur Yeni SQL Server VM hello hello aynı ContosoQuorum bulut hizmeti. Aynı bulut hizmetine olmalarını istiyorsanız içinde toobe hello hello VM'ler koymanız gerekir hello aynı kullanılabilirlik kümesi.
4. Her VM toodownload ve tam olarak sağlanan her VM toobe için Uzak Masaüstü dosyası tooyour çalışma dizini bekleyin. Merhaba `for` döngü döngüleri hello üç yeni VM'ler ve bunların her biri için hello komutları hello en üst düzey süslü ayraç içinde yürütür.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    Merhaba SQL Server Vm'lerinin şimdi sağlanır ve çalışıyor, ancak bunlar varsayılan seçeneklerle SQL Server ile birlikte yüklenen.

## <a name="initialize-hello-failover-cluster-vms"></a>Merhaba yük devretme kümesi sanal makineleri Başlat
Bu bölümde, hello yük devretme kümesi ve hello SQL Server yüklemesi kullanacağınız toomodify hello üç sunucu gerekir. Bu avantajlar şunlardır:

* Tüm sunucuları: tooinstall hello gereksinim **Yük Devretme Kümelemesi** özelliği.
* Tüm sunucuları: tooadd gerek **CORP\Install** hello makine olarak **yönetici**.
* ContosoSQL1 ve yalnızca ContosoSQL2: tooadd gerek **CORP\Install** olarak bir **sysadmin** hello varsayılan veritabanı rolü.
* ContosoSQL1 ve yalnızca ContosoSQL2: tooadd gerek **NT AUTHORITY\SYSTEM** bir ile oturum açma aşağıdaki izinleri hello olarak:

  * Herhangi bir kullanılabilirlik grubu Değiştir
  * SQL bağlantı
  * VIEW server state
* ContosoSQL1 ve yalnızca ContosoSQL2: Merhaba **TCP** Protokolü hello SQL Server VM üzerinde zaten etkin. Ancak, yine tooopen hello Güvenlik Duvarı için SQL Server'ın uzaktan erişim gerekir.

Şimdi, hazır toostart demektir. İle başlayarak **ContosoQuorum**, hello adımları izleyin:

1. Çok bağlanmak**ContosoQuorum** hello Uzak Masaüstü dosyaları başlatmasını tarafından. Merhaba makine yöneticisinin kullanıcı adı kullanma **AzureAdmin** ve parola **Contoso! 000**, hello VM'ler oluşturduğunuzda belirttiğiniz.
2. Merhaba bilgisayarlar başarıyla çok birleştirilmiş olan doğrulayın**corp.contoso.com**.
3. Devam etmeden önce hello otomatik başlatma görevlerini çalıştıran hello SQL Server yükleme toofinish bekleyin.
4. Yönetici modunda bir PowerShell penceresi açın.
5. Merhaba Windows Yük Devretme Kümelemesi özelliğini yükleyin.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Ekleme **CORP\Install** yerel yönetici olarak.

        net localgroup administrators "CORP\Install" /Add
7. ContosoQuorum dışında oturum açın. Bu sunucu ile artık bitirdiniz.

        logoff.exe

Ardından, başlatma **ContosoSQL1** ve **ContosoSQL2**. Her iki SQL Server VM'ler için aynı olan hello aşağıdaki adımları izleyin.

1. Toohello iki SQL Server Vm'lerinin hello Uzak Masaüstü dosyaları başlatarak bağlayın. Merhaba makine yöneticisinin kullanıcı adı kullanma **AzureAdmin** ve parola **Contoso! 000**, hello VM'ler oluşturduğunuzda belirttiğiniz.
2. Merhaba bilgisayarlar başarıyla çok birleştirilmiş olan doğrulayın**corp.contoso.com**.
3. Devam etmeden önce hello otomatik başlatma görevlerini çalıştıran hello SQL Server yükleme toofinish bekleyin.
4. Yönetici modunda bir PowerShell penceresi açın.
5. Merhaba Windows Yük Devretme Kümelemesi özelliğini yükleyin.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Ekleme **CORP\Install** yerel yönetici olarak.

        net localgroup administrators "CORP\Install" /Add
7. SQL Server PowerShell sağlayıcısı Hello içeri aktarın.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Ekleme **CORP\Install** hello varsayılan SQL Server örneği için hello sysadmin rolü olarak.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Ekleme **NT AUTHORITY\SYSTEM** bir oturum açma yukarıda açıklanan hello üç izinlerle olarak.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. SQL Server'ın uzaktan erişim için Hello Güvenlik Duvarı'nı açın.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Her iki VM dışında oturum açın.

         logoff.exe

Son olarak, hazır tooconfigure hello kullanılabilirlik grubu demektir. Tüm hello çalışacak hello SQL Server PowerShell sağlayıcısı tooperform kullanacağınız **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Merhaba kullanılabilirlik grubunu yapılandırma
1. Çok bağlanmak**ContosoSQL1** hello Uzak Masaüstü dosyaları başlatmasını tarafından yeniden. Yerine Hello makine hesabı kullanarak oturum açma kullanarak oturum açın **CORP\Install**.
2. Yönetici modunda bir PowerShell penceresi açın.
3. Değişkenleri aşağıdaki hello tanımlayın:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. SQL Server PowerShell sağlayıcısı Hello içeri aktarın.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Merhaba SQL Server hizmet hesabını ContosoSQL1 tooCORP\SQLSvc1 değiştirebilirsiniz.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Merhaba SQL Server hizmet hesabını ContosoSQL2 tooCORP\SQLSvc2 değiştirebilirsiniz.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Karşıdan **CreateAzureFailoverCluster.ps1** gelen [Always On kullanılabilirlik grupları Azure VM'de yük devretme kümesi oluşturma](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello yerel çalışma dizini. Bir işlev yük devretme kümesi oluşturma bu komut dosyası toohelp kullanacaksınız. Windows Yük Devretme Kümelemesi hello Azure ile nasıl etkileşim hakkında önemli bilgiler için ağ için bkz: [Azure Virtual Machines'de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Tooyour çalışma dizini değiştirin ve indirilen hello komut dosyasıyla hello yük devretme kümesi oluşturun.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Always On kullanılabilirlik grupları'hello varsayılan SQL Server örnekleri için etkinleştirmek **ContosoSQL1** ve **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Bir yedekleme dizini oluşturmak ve hello SQL Server hizmeti hesapları için izinler verebilirsiniz. Bu dizin tooprepare hello kullanılabilirlik veritabanı hello ikincil kopyada kullanacaksınız.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Bir veritabanı oluşturma **ContosoSQL1** adlı **MyDB1**, hem tam yedekleme hem de bir günlük yedeklemesi alın ve bunları geri **ContosoSQL2** hello ile **ile NORECOVERY** seçeneği.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. SQL Server Vm'lerinin hello üzerinde Hello kullanılabilirlik grubunun uç noktaları oluşturun ve hello uygun izinlere hello uç noktalarda ayarlayın.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Merhaba kullanılabilirlik çoğaltmalarının oluşturun.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Son olarak, hello kullanılabilirlik grubu ve birleştirme hello ikincil çoğaltma toohello kullanılabilirlik grubu oluşturun.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Sonraki adımlar
Artık başarıyla SQL Server Always On Azure'da bir kullanılabilirlik grubu oluşturarak uyguladık. Bu kullanılabilirlik grubu için bir dinleyici tooconfigure bkz [Azure'da Always On kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).

Azure'da SQL Server kullanma hakkında diğer bilgi için bkz: [Azure virtual machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
