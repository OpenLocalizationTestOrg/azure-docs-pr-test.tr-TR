---
title: aaaUse PowerShell tooCreate bir VM ile bir yerel moddaki bir rapor sunucusunda | Microsoft Docs
description: "Bu konuda açıklar ve hello dağıtımını ve SQL Server Reporting Services yerel mod rapor sunucusu bir Azure sanal makine yapılandırmasını size yol göstermektedir. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Bir Azure VM ile bir yerel moddaki bir rapor sunucusunda PowerShell tooCreate kullanın
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bu konuda açıklar ve hello dağıtımını ve SQL Server Reporting Services yerel mod rapor sunucusu bir Azure sanal makine yapılandırmasını size yol göstermektedir. Merhaba bu belgeyi kullanımda el ile yapılacak adımlar toocreate hello sanal makine ve bir Windows PowerShell Betiği bileşimini hello VM üzerinde tooconfigure Reporting Services adımları. HTTP veya HTTPs için bir güvenlik duvarı bağlantı noktası açma Hello yapılandırma komut dosyası içerir.

> [!NOTE]
> Gerekli olmadığı, **HTTPS** hello rapor sunucusunda **2. adıma geçin**.
> 
> 1. adımda Hello VM oluşturduktan sonra toohello bölüm kullan betik tooconfigure hello report server ve HTTP gidin. Merhaba betiği çalıştırdıktan sonra hello rapor hazır toouse sunucusudur.

## <a name="prerequisites-and-assumptions"></a>Önkoşullar ve varsayımlar
* **Azure aboneliği**: hello Azure aboneliğinizde kullanılabilir çekirdek sayısı doğrulayın. VM boyutu önerilen hello oluşturursanız **A3**, gereksinim duyduğunuz **4** kullanılabilir çekirdekler. Bir VM boyutu kullanırsanız **A2**, gereksinim duyduğunuz **2** kullanılabilir çekirdekler.
  
  * tooverify hello çekirdek hello Klasik Azure portalı, aboneliğinizde sınırının tıklayın ayarları hello sol bölmesinde ve sonra tıklatın kullanım hello üst menüde.
  * tooincrease hello çekirdek kotası, kişi [Azure Destek](https://azure.microsoft.com/support/options/). VM boyutu bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Windows PowerShell komut dosyası**: hello konu Windows PowerShell temel bilgiye sahip olduğunuzu varsayar. Windows PowerShell'i kullanma hakkında daha fazla bilgi için hello aşağıdakilere bakın:
  
  * [Windows Server'da Windows PowerShell'i başlatma](https://technet.microsoft.com/library/hh847814.aspx)
  * [Windows PowerShell ile çalışmaya başlama](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>1. adım: bir Azure sanal makine sağlama
1. Toohello Klasik Azure portalına göz atın.
2. Tıklatın **sanal makineleri** hello sol bölmede.
   
    ![Microsoft azure sanal makineler](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. **Yeni**’ye tıklayın.
   
    ![Yeni düğmesi](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Tıklatın **galerisinden**.
   
    ![Galeriden yeni vm](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Tıklatın **SQL Server 2014 RTM Standard – Windows Server 2012 R2** ve hello ok toocontinue'ı tıklatın.
   
    ![ileri](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Merhaba Reporting Services veri abonelikleri özelliği tabanlı gerek duyuyorsanız, **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. SQL Server sürümleri ve özellik desteği hakkında daha fazla bilgi için bkz: [hello SQL Server 2012 sürümleri tarafından desteklenen özellikler](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. Merhaba üzerinde **sanal makine yapılandırması** sayfasında, aşağıdaki alanları hello düzenleyin:
   
   * Varsa birden fazla **sürüm yayın tarihi**, hello en son sürümünü seçin.
   * **Sanal makine adı**: hello makine adı hello sonraki yapılandırma sayfasında da hello varsayılan bulut hizmeti DNS adı olarak kullanılır. Merhaba DNS adı hello Azure hizmeti arasında benzersiz olması gerekir. Merhaba VM VM için kullanılan hangi hello açıklayan bir bilgisayar adıyla yapılandırmayı göz önünde bulundurun. Örneğin ssrsnativecloud.
   * **Katman**: standart
   * **Boyutu: A3** hello VM boyutu SQL Server iş yükleri için önerilir. Bir VM yalnızca bir rapor sunucusu olarak kullanılıyorsa, büyük bir iş yükü hello rapor sunucusu karşılaştığında sürece, A2 VM boyutunu yeterli olur. VM fiyatlandırma bilgileri için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Yeni bir kullanıcı adı**: sağladığınız hello adı hello VM üzerinde bir yönetici olarak oluşturulur.
   * **Yeni parola** ve **onaylayın**. Bu parola hello yeni yönetici hesabı için kullanılır ve güçlü bir parola kullanmanız önerilir.
   * **İleri**’ye tıklayın. ![sonraki](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Merhaba sonraki sayfada, alanları izleyen hello düzenleyin:
   
   * **Bulut hizmeti**: seçin **yeni bir bulut hizmeti oluşturma**.
   * **Bulut hizmeti DNS adı**: hello Genel DNS adını hello hello VM ile ilişkili bir bulut hizmeti budur. Merhaba varsayılan adı hello VM adı için yazdığınız hello adıdır. Hello konu daha sonraki adımlarda güvenilir bir SSL sertifikası oluşturun ve sonra hello DNS adı hello hello değerini kullanılıyorsa "**verilen**" Merhaba sertifika.
   * **Bölge/benzeşim grubu/sanal ağ**: hello bölgeye en yakın tooyour son kullanıcılar'ı seçin.
   * **Depolama hesabı**: otomatik olarak oluşturulan depolama hesabı kullanın.
   * **Kullanılabilirlik kümesi**: yok.
   * **Uç noktaları** Koru hello **Uzak Masaüstü** ve **PowerShell** uç noktaları ve HTTP veya HTTPS uç noktası, ortamınıza bağlı olarak ekleyin.
     
     * **HTTP**: Merhaba ortak ve özel bağlantı noktaları varsayılan **80**. Özel bir bağlantı noktası 80 dışında kullanırsanız değiştirme Not **$HTTPport = 80** hello http komut.
     * **HTTPS**: Merhaba ortak ve özel bağlantı noktaları varsayılan **443**. En iyi güvenlik uygulaması toochange hello özel bağlantı noktası ve, güvenlik duvarı ve hello rapor sunucusu toouse hello özel bağlantı noktası yapılandırın. Uç noktalar hakkında daha fazla bilgi için bkz: [nasıl tooSet bir sanal makine ile iletişim kurma](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Bir bağlantı noktası 443 dışındaki kullanıyorsanız, hello parametre değiştirme Not **$HTTPsport = 443** hello HTTPS komut dosyası olarak.
   * İleri'yi tıklatın. ![ileri](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Merhaba son sayfasında hello Sihirbazı'nın hello varsayılan tutmak **hello VM aracı yükleme** seçili. Merhaba bu konudaki adımları hello VM Aracısı kullanan değil, ancak bu VM tookeep planlıyorsanız, hello VM aracısı ve uzantılar tooenhance sağlayacak he CM.  Merhaba VM Aracısı hakkında daha fazla bilgi için bkz: [VM aracısı ve uzantılar – Kısım 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Merhaba varsayılan yüklü uzantıları ad çalıştıran biri hello VM masaüstündeki görüntüleyen hello "BGINFO" uzantısı, sistem bilgi ve ücretsiz iç IP gibi sürücü alanı.
9. Tamamlandı'yi tıklatın. ![Tamam](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Merhaba **durum** VM görüntüler olarak Merhaba, **başlangıç (hazırlama)** hello sağlama işlemi ve ardından görüntüler olarak sırasında **çalıştıran** sağlanmıştır ve kullanıma hazırdır hello VM olduğunda toouse.

## <a name="step-2-create-a-server-certificate"></a>2. adım: bir sunucu sertifikası oluşturma
> [!NOTE]
> Merhaba rapor sunucusunda HTTPS ihtiyacınız yoksa, şunları yapabilirsiniz **2. adıma geçin** ve toohello bölümüne gidin **betik tooconfigure hello rapor sunucusu ve HTTP kullanma**. Kullanım hello HTTP betik tooquickly hello report server ve hello rapor sunucusu hazır toouse olacak yapılandırın.

Sipariş toouse içinde HTTPS hello VM üzerinde güvenilir bir SSL sertifikası gerekir. Senaryonuza bağlı olarak, hello aşağıdaki iki yöntemden birini kullanabilirsiniz:

* Geçerli bir SSL sertifikası bir sertifika yetkilisi (CA) tarafından verilen ve Microsoft tarafından güvenilen. Merhaba CA kök sertifikaları Microsoft kök sertifikası programı hello dağıtılmış gerekli toobe ' dir. Bu program hakkında daha fazla bilgi için bkz: [Windows ve Windows Phone 8 SSL kök sertifika programı (üye CA'lar)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) ve [giriş toohello Microsoft kök sertifikası programı](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Kendinden imzalı bir sertifika. Otomatik olarak imzalanan sertifikalar üretim ortamları için önerilmez.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse bir güvenilen sertifika yetkilisi (CA) tarafından oluşturulan bir sertifika
1. **Bir sertifika yetkilisinden hello Web sitesi için bir sunucu sertifikası isteği**. 
   
    Merhaba Web Sunucusu Sertifika Sihirbazı ya da toogenerate tooa sertifika yetkilisi veya toogenerate bir çevrimiçi sertifika yetkilisi için bir istek göndermek bir sertifika isteği dosyasını (Certreq.txt) kullanabilirsiniz. Örneğin, Microsoft Sertifika Hizmetleri Windows Server 2012'de. Sunucu sertifikanızı tarafından sunulan kimlik güvence düzeyini Merhaba, bağlı olarak birkaç gün tooseveral ay hello sertifika yetkilisi tooapprove için isteğiniz olduğundan ve bir sertifika dosyası Gönder. 
   
    Sunucu sertifikaları isteme hakkında daha fazla bilgi için hello aşağıdakilere bakın: 
   
   * Kullanım [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * Güvenlik araçları tooAdminister Windows Server 2012.
     
     [Güvenlik araçları tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Merhaba **verilen** hello alanının güvenilir SSL sertifikası olması hello aynı hello **bulut hizmeti DNS adı** sizin için kullanılan yeni VM hello.

2. **Merhaba sunucu sertifikası hello Web sunucusuna yükleyin**. Merhaba Web bu durumda hello ana rapor sunucusu hello ve Reporting Services yapılandırdığınızda, sonraki adımlarda hello Web sitesi oluşturulur VM sunucusudur. Merhaba sertifika MMC ek bileşenini kullanarak hello Web sunucusunda hello sunucu sertifikası yükleme hakkında daha fazla bilgi için bkz: [sunucu sertifikasını yüklemeniz](https://technet.microsoft.com/library/cc740068).
   
    Bu konuda tooconfigure hello rapor sunucusu dahil toouse hello betik istiyorsanız hello sertifikaları değerini hello **parmak izi** hello komut parametresi olarak gereklidir. Ayrıntılar için sonraki bölüme Hello nasıl tooobtain hello üzerinde hello sertifikanın parmak izini bakın.
3. Merhaba sertifika toohello rapor sunucusu atayın. Merhaba rapor sunucusunu yapılandırdığınızda hello atama hello sonraki bölümde tamamlandı.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>toouse hello sanal makineleri otomatik olarak imzalanan sertifika
Merhaba VM hazırlandığında kendinden imzalı bir sertifika hello VM üzerinde oluşturuldu. Merhaba sertifikanın aynı hello VM DNS adı ad hello vardır. Sipariş tooavoid sertifika hataları gerekli hello sertifikanın hello VM kendisi ve ayrıca hello sitenin tüm kullanıcılar tarafından güvenilmiyor.

1. tootrust hello kök CA'ın hello yerel VM hello sertifika Ekle hello sertifika toohello **güvenilen kök sertifika yetkilileri**. Merhaba, gerekli hello adımları özeti aşağıdadır. Nasıl tootrust hello CA ile ilgili ayrıntılı adımlar için bkz: [sunucu sertifikasını yüklemeniz](https://technet.microsoft.com/library/cc740068).
   
   1. Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın. Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.
      
       ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın. 
      
       Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.
      
       ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. MMC.exe çalıştırın. Daha fazla bilgi için bkz: [nasıl yapılır: hello MMC ek bileşeni ile sertifikaları görüntüleme](https://msdn.microsoft.com/library/ms788967.aspx).
   3. Merhaba konsol uygulamasındaki **dosya** menüsünde hello eklemek **sertifikaları** ek bileşeninde, select **bilgisayar hesabı** istenir ve ardından **İleri**.
   4. Seçin **yerel bilgisayar** toomanage ve ardından **son**.
   5. Tıklatın **Tamam** genişletin ve ardından hello **sertifikalar - kişisel** düğümleri ve ardından **Sertifikalar**. Merhaba sertifika sonra hello VM hello DNS adı olarak adlandırılır ve ile biten **cloudapp.net**. Merhaba sertifika adını sağ tıklatıp **kopya**.
   6. Merhaba genişletin **güvenilen kök sertifika yetkilileri** düğümünü ve ardından sağ tıklayarak **sertifikaları** ve ardından **Yapıştır**.
   7. Merhaba sertifika adı altında toovalidate, çift tıklayarak **güvenilen kök sertifika yetkilileri** ve hatalar yoktur ve sertifikanızı gördüğünüz doğrulayın. Bu konuda tooconfigure hello rapor sunucusu dahil toouse hello HTTPS betik istiyorsanız hello sertifikaları değerini hello **parmak izi** hello komut parametresi olarak gereklidir. **tooget hello parmak izi değeri**, hello aşağıdaki adımları tamamlayın. Bölümünde de bir PowerShell örnek tooretrieve hello parmak izi yok [betik tooconfigure hello rapor sunucusu ve HTTPS kullanma](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Merhaba sertifika, örneğin ssrsnativecloud.cloudapp.net Hello adına çift tıklayın.
      2. Merhaba tıklatın **ayrıntıları** sekmesi.
      3. Tıklatın **parmak izi**. Merhaba hello parmak izi değerini hello Ayrıntılar alanında, örneğin a6 görüntülenen 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.
      4. Merhaba parmak izini kopyalayın ve hello değeri daha sonra kullanmak üzere kaydetmek veya hello betik şimdi düzenleyin.
      5. (*) Merhaba betiği çalıştırmadan önce hello değer çiftlerini Between hello boşlukları kaldırın. Örneğin önce not ettiğiniz hello parmak izi şimdi a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f olur.
      6. Merhaba sertifika toohello rapor sunucusu atayın. Merhaba rapor sunucusunu yapılandırdığınızda hello atama hello sonraki bölümde tamamlandı.

Otomatik olarak imzalanan bir SSL sertifikası kullanıyorsanız, hello hello sertifikadaki zaten hello VM hello ana bilgisayar adıyla aynıdır. Bu nedenle, hello hello makinenin DNS zaten genel olarak kaydedilir ve herhangi bir istemciden erişilebilir.

## <a name="step-3-configure-hello-report-server"></a>3. adım: hello rapor sunucusu yapılandırma
Bu bölümde bir Reporting Services yerel mod rapor sunucusu olarak hello VM nasıl yapılandıracağınız anlatılmaktadır. Yöntemleri tooconfigure hello rapor sunucusu aşağıdaki hello birini kullanabilirsiniz:

* Merhaba betik tooconfigure hello rapor sunucusu kullanma
* Yapılandırma Yöneticisi'ni kullanın tooConfigure hello rapor sunucusu.

Daha ayrıntılı adımlar için hello bölümüne bakın [Bağlan toohello sanal makine ve başlangıç hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Kimlik doğrulama Not:** Windows kimlik doğrulaması kimlik doğrulama yöntemini önerilen hello ve hello varsayılan Reporting Services kimlik doğrulaması olur. Merhaba VM üzerinde yapılandırılmış olan kullanıcılar Reporting Services erişebilir ve Hizmetleri rolleri tooReporting atanır.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Komut dosyası tooconfigure hello report server ve HTTP kullanın
toouse hello Windows PowerShell komut dosyası tooconfigure hello rapor sunucusu, aşağıdaki adımları tam hello. Merhaba yapılandırma HTTP, HTTPS değil içerir:

1. Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın. Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın. 
   
    Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.
   
    ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Hello VM, açık **Windows PowerShell ISE** yönetici ayrıcalıklarına sahip. Merhaba PowerShell ISE, Windows server 2012'de varsayılan olarak yüklenir. İŞE hello hello betiğini yapıştırın, hello komut dosyasını değiştirin ve hello betiğini çalıştırmak yerine standart bir Windows PowerShell penceresinde hello ISE kullanmanız önerilir.
3. Windows PowerShell ISE'de hello tıklatın **Görünüm** menüsünü seçin ve ardından **betik bölmesini göster**.
4. Komut dosyası izleyen hello kopyalayıp hello betik hello Windows PowerShell ISE betik bölmesine yapıştırın.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Bir HTTP bağlantı noktası 80 dışında hello VM oluşturduysanız hello parametresi $HTTPport değiştirin = 80.
6. Merhaba komut dosyası şu anda Raporlama Hizmetleri için yapılandırılır. Raporlama Hizmetleri için toorun hello betik istiyorsanız, hello yolu toohello ad hello sürüm bölümü çok değiştirin "v11" Merhaba Get-WmiObject deyimi üzerinde.
7. Merhaba komut dosyasını çalıştırın.

**Doğrulama**: hello temel rapor sunucusu işlevselliği çalıştığından, tooverify bkz hello [doğrula hello yapılandırma](#verify-the-configuration) bu konunun ilerleyen bölümlerinde.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Komut dosyası tooconfigure hello rapor sunucusu hem de HTTPS kullanın
toouse Windows PowerShell tooconfigure hello rapor sunucusu, aşağıdaki adımları tam hello. Merhaba yapılandırma, HTTPS değil HTTP içerir.

1. Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın. Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın. 
   
    Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.
   
    ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Hello VM, açık **Windows PowerShell ISE** yönetici ayrıcalıklarına sahip. Merhaba PowerShell ISE, Windows server 2012'de varsayılan olarak yüklenir. İŞE hello hello betiğini yapıştırın, hello komut dosyasını değiştirin ve hello betiğini çalıştırmak yerine standart bir Windows PowerShell penceresinde hello ISE kullanmanız önerilir.
3. Windows PowerShell komutunu aşağıdaki hello Çalıştır komut dosyası çalıştırarak tooenable:
   
        Set-ExecutionPolicy RemoteSigned
   
    Ardından tooverify hello ilkesi aşağıdaki hello çalıştırabilirsiniz:
   
        Get-ExecutionPolicy
4. İçinde **Windows PowerShell ISE**, hello tıklatın **Görünüm** menüsünü seçin ve ardından **betik bölmesini göster**.
5. Aşağıdaki komut dosyası ve hello Windows PowerShell ISE betik bölmesine yapıştırın hello kopyalayın.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Merhaba değiştirme **$certificatehash** hello komut parametresi:
   
   * Bu bir **gerekli** parametresi. Merhaba önceki adımları hello sertifika değeri kaydetmediyseniz hello sertifika parmak izini yöntemleri toocopy hello sertifika karma değer aşağıdaki hello birini kullanın.:
     
       Hello VM, Windows PowerShell ISE açın ve hello aşağıdaki komutu çalıştırın:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       Merhaba çıkış benzer toohello aşağıdaki arar. Merhaba komut dosyası boş bir satır döndürürse, hello VM örneğin yapılandırılmış bir sertifikaya sahip değilse, hello bölümüne bakın [toouse hello sanal makineleri otomatik olarak imzalanan sertifika](#to-use-the-virtual-machines-self-signed-certificate).
     
     OR
   * VM çalıştırmak mmc.exe hello ve hello eklemek **sertifikaları** ek bileşenini.
   * Merhaba altında **güvenilen kök sertifika yetkilileri** düğüme çift tıklayın, sertifika adı. Merhaba otomatik olarak imzalanan sertifikasını hello VM kullanıyorsanız, hello sertifika sonra hello VM hello DNS adı olarak adlandırılır ve ile biten **cloudapp.net**.
   * Merhaba tıklatın **ayrıntıları** sekmesi.
   * Tıklatın **parmak izi**. Merhaba hello parmak izi değerini hello Ayrıntılar alanında, örneğin af 11 60 b6 4b 28 8 d 89 0a görüntülenen 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Merhaba betiği çalıştırmadan önce**, değer çiftlerini hello Between hello boşlukları Kaldır. Örneğin af1160b64b288d890a8212ff6ba9c3664f319048
7. Merhaba değiştirme **$httpsport** parametre: 
   
   * Ardından hello HTTPS uç noktası için 443 numaralı bağlantı noktasını kullandıysanız, tooupdate hello betik bu parametrede gerekmez. Aksi durumda VM hello üzerinde hello HTTPS özel uç noktası yapılandırıldığında, seçtiğiniz hello bağlantı noktası değeri kullanın.
8. Merhaba değiştirme **$DNSName** parametre: 
   
   * Merhaba betik bir joker sertifika $DNSName yapılandırılmış = "+". Joker karakter sertifika bağlama için hiçbir istediğiniz tooconfigure bunu yaparsanız, $DNSName Açıklama = "+"ve aşağıdaki satırı, hello tam $DNSNAme başvurusu, ## $DNSName="$server.cloudapp.net hello etkinleştir".
     
       Raporlama Hizmetleri için toouse hello sanal makinenin DNS adı istemiyorsanız hello $DNSName değerini değiştirin. Merhaba parametreyi kullanırsanız, hello sertifika bu adı kullanmanız gerekir ve bir DNS sunucusundaki genel hello adı kaydedin.
9. Merhaba komut dosyası şu anda Raporlama Hizmetleri için yapılandırılır. Raporlama Hizmetleri için toorun hello betik istiyorsanız, hello yolu toohello ad hello sürüm bölümü çok değiştirin "v11" Merhaba Get-WmiObject deyimi üzerinde.
10. Merhaba komut dosyasını çalıştırın.

**Doğrulama**: hello temel rapor sunucusu işlevselliği çalıştığından, tooverify bkz hello [doğrula hello yapılandırma](#verify-the-connection) bu konunun ilerleyen bölümlerinde. tooverify hello sertifika bağlama yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından hello aşağıdaki komutu çalıştırın:

    netsh http show sslcert

Merhaba sonuç hello aşağıdakileri içerir:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Yapılandırma Yöneticisi'ni kullanın tooConfigure hello rapor sunucusu
Toorun hello PowerShell komut dosyası tooconfigure hello rapor sunucusu istemiyorsanız, bu bölümde toouse hello Reporting Services yerel mod configuration manager tooconfigure hello rapor sunucusu hello adımları izleyin.

1. Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın. Merhaba kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın.
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Windows Update'i çalıştırın ve güncelleştirmeleri toohello VM yükleyin. Merhaba VM yeniden başlatılması gerekiyorsa, hello VM yeniden başlatın ve toohello VM hello Klasik Azure Portalı'ndan yeniden bağlanın.
3. Merhaba Başlat menüsünden hello VM üzerinde yazın **Reporting Services** açarak **Reporting Services Configuration Manager**.
4. Merhaba varsayılan değerleri bırakın **sunucu adı** ve **rapor sunucusu örneği**. **Bağlan**'a tıklayın.
5. Merhaba sol bölmede **Web hizmeti URL'si**.
6. Varsayılan olarak, RS IP "Tüm atanan" HTTP bağlantı noktası 80 için yapılandırılır. tooadd HTTPS:
   
   1. İçinde **SSL sertifikası**: select hello sertifika [VM adı] örneğin toouse, istediğiniz. cloudapp.net. Hiçbir sertifika listelenmiyorsa, hello bölümüne bakın. **2. adım: bir sunucu sertifikası oluşturma** nasıl tooinstall ve güven hello VM sertifikadaki hello hakkında bilgi için.
   2. Altında **SSL bağlantı noktası**: 443'ü seçin. Merhaba VM özel farklı bir bağlantı noktası ile Merhaba HTTPS özel uç noktasını yapılandırdıysanız, bu değer burada kullanın.
   3. Tıklatın **Uygula** ve hello işlemi toocomplete için bekleyin.
7. Merhaba sol bölmede **veritabanı**.
   
   1. Tıklatın **değiştirme Databas**e.
   2. Tıklatın **yeni bir rapor sunucusu veritabanı oluşturun** ve ardından **sonraki**.
   3. Merhaba varsayılan adı bırakın **sunucu adı**: hello VM adlandırın ve hello varsayılan adı bırakın **kimlik doğrulama türü** olarak **geçerli kullanıcı** – **tümleşik güvenlik**. **İleri**’ye tıklayın.
   4. Merhaba varsayılan adı bırakın **veritabanı adı** olarak **ReportServer** tıklatıp **sonraki**.
   5. Merhaba varsayılan adı bırakın **kimlik doğrulama türü** olarak **hizmeti kimlik bilgileri** tıklatıp **sonraki**.
   6. Tıklatın **sonraki** hello üzerinde **Özet** sayfası.
   7. Merhaba Yapılandırma tamamlandığında tıklatın **son**.
8. Merhaba sol bölmede **Rapor Yöneticisi URL'si**. Merhaba varsayılan adı bırakın **sanal dizin** olarak **raporları** tıklatıp **Uygula**.
9. Tıklatın **çıkış** tooclose hello Reporting Services Configuration Manager.

## <a name="step-4-open-windows-firewall-port"></a>4. adım: Windows Güvenlik Duvarı bağlantı noktası Aç
> [!NOTE]
> Merhaba betikleri tooconfigure hello rapor sunucusu birini kullandıysanız, bu bölümü atlayabilirsiniz. Merhaba betik adım tooopen hello güvenlik duvarı bağlantı noktası dahil. Merhaba varsayılan bağlantı noktası HTTP için 80 ve HTTPS için 443 numaralı bağlantı noktasını oluştu.
> 
> 

tooconnect uzaktan tooReport Yöneticisi veya hello rapor hello sanal makine sunucuda, bir TCP uç noktası hello VM üzerinde gereklidir. Gerekli tooopen hello hello VM'in Güvenlik Duvarı'nda aynı bağlantı noktası olur. Merhaba VM hazırlandığında hello uç noktası oluşturuldu.

Bu bölüm, nasıl tooopen hello üzerinde güvenlik duvarı bağlantı noktasını temel bilgileri sağlar. Daha fazla bilgi için bkz: [güvenlik duvarını rapor sunucusu erişimi için yapılandırma](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Merhaba betik tooconfigure hello rapor sunucusu kullandıysanız, bu bölümü atlayabilirsiniz. Merhaba betik adım tooopen hello güvenlik duvarı bağlantı noktası dahil.
> 
> 

Özel bir bağlantı noktası HTTPS için 443 dışındaki yapılandırdıysanız, komut dosyası uygun şekilde aşağıdaki hello değiştirin. tooopen bağlantı noktası **443** hello Windows Güvenlik Duvarı, hello aşağıdaki adımları tamamlayın:

1. Yönetici ayrıcalıklarıyla bir Windows PowerShell penceresi açın.
2. Merhaba VM üzerinde hello HTTPS uç noktası yapılandırıldığında bir bağlantı noktası 443 dışındaki kullandıysanız, komut aşağıdaki hello hello bağlantı noktasını güncelleştirin ve hello komutu çalıştırın:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Merhaba komut tamamlandığında, **Tamam** hello Komut İstemi'nde görüntülenir.

başlangıç bağlantı noktası açıldı tooverify bir Windows PowerShell penceresini açın ve komut aşağıdaki çalışma hello açın:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Merhaba yapılandırmasını doğrulayın.
Merhaba temel rapor sunucusu işlevselliği şimdi çalışıyor, tooverify yönetici ayrıcalıklarıyla tarayıcınızı açın ve ardından sunucu ad Rapor Yöneticisi'ni URL'leri Gözat toohello aşağıdaki rapor:

* Hello VM, toohello rapor sunucusu URL'si göz atın:
  
        http://localhost/reportserver
* Hello VM, toohello Rapor Yöneticisi URL'si göz atın:
  
        http://localhost/Reports
* Yerel bilgisayarınızdan toohello Gözat **uzak** Yöneticisi hello VM üzerinde rapor. Aşağıdaki uygun şekilde örneğine hello Hello DNS adını güncelleştirin. İçin bir parola istendiğinde, hello VM hazırlandığında oluşturduğunuz hello yönetici kimlik bilgileri kullanın. Merhaba kullanıcı adınızdır hello [etki alanı]\[kullanıcı adı] biçiminde hello etki hello VM bilgisayar adını, örneğin ssrsnativecloud\testuser olduğu. HTTP kullanmıyorsanız**S**, hello kaldırmak **s** hello URL. VM ek kullanıcılar oluşturma hakkında bilgi için Hello sonraki bölümüne bakın.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* Yerel bilgisayarınızdan toohello uzaktan rapor sunucusu URL'si göz atın. Aşağıdaki uygun şekilde örneğine hello Hello DNS adını güncelleştirin. HTTPS kullanmıyorsanız hello s hello URL'de kaldırın.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Kullanıcılar oluşturma ve rolleri atama
Rapor sunucusu yapılandırma ve hello doğrulama sonra ortak bir yönetim görevi toocreate bir veya daha fazla kullanıcı sayısıdır ve kullanıcıların tooReporting Hizmetleri rolleri atayın. Daha fazla bilgi için hello aşağıdakilere bakın:

* [Bir yerel kullanıcı hesabı oluşturun](https://technet.microsoft.com/library/cc770642.aspx)
* [Kullanıcı erişim izni ver tooa rapor sunucusu (Rapor Yöneticisi)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Oluşturma ve rol atamalarını yönetme](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate ve raporları yayımlama toohello Azure sanal makine
Merhaba aşağıdaki tabloda hello seçenekleri kullanılabilir toopublish varolan raporları hello Microsoft Azure sanal makinesi üzerinde barındırılan bir şirket içi bilgisayar toohello rapor sunucusu özetlenmektedir:

* **RS.exe betik**: kullanım RS.exe betik toocopy rapor öğeleri ve varolan rapor sunucusu tooyour Microsoft Azure sanal makinesi. Daha fazla bilgi için hello "yerel mod tooNative modu – Microsoft Azure sanal makinesi" bölümüne bakın [örnek Raporlama Hizmetleri rs.exe betik tooMigrate rapor sunucuları arasında içerik](https://msdn.microsoft.com/library/dn531017.aspx).
* **Rapor Oluşturucu**: hello sanal makine içeren hello tıklatın-Microsoft SQL Server Rapor Oluşturucusu sürümünü bir kez. toostart Rapor Oluşturucu hello hello sanal makinede ilk kez:
  
  1. Tarayıcınız yönetici ayrıcalıklarıyla başlatın.
  2. Merhaba sanal makineye tooreport Yöneticisi bulun ve tıklatın **Rapor Oluşturucu** hello Şeritte.
     
     Daha fazla bilgi için bkz: [yükleme, kaldırma ve destekleyici Rapor Oluşturucusu'nu](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server veri araçları: VM**: SQL Server 2012 ile Merhaba VM oluşturduğunuz sonra SQL Server veri araçları hello sanal makinede yüklü ve kullanılan toocreate olabilir **rapor sunucusu projeleri** ve hello sanal raporları Makine. SQL Server veri araçları hello raporları toohello rapor sunucusu hello sanal makineye yayımlayabilirsiniz.
  
    SQL server 2014 ile Merhaba VM oluşturduysanız, SQL Server veri araçları - BI visual Studio için yükleyebilirsiniz. Daha fazla bilgi için hello aşağıdakilere bakın:
  
  * [Microsoft SQL Server veri araçları - Visual Studio 2013 iş zekası](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server veri araçları - Visual Studio 2012 için iş zekası](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server veri araçları ve SQL Server Business Intelligence (BI SSDT)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server veri araçları: Uzaktan**: yerel bilgisayarınızda SQL Server veri araçları Raporlama Hizmetleri raporlarını içeren bir Reporting Services projesi oluşturun. Merhaba proje tooconnect toohello web hizmeti URL'si yapılandırın.
  
    ![SSRS projesi için SSDT proje özellikleri](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Komut dosyası kullanma**: betik toocopy rapor sunucusu içeriği kullanın. Daha fazla bilgi için bkz: [örnek Raporlama Hizmetleri rs.exe betik tooMigrate rapor sunucuları arasında içerik](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Merhaba VM kullanmıyorsanız maliyeti en aza indir
> [!NOTE]
> toominimize ücretleri için Azure sanal makinelerinizi kullanılmadığı zaman hello VM hello Klasik Azure Portalı'ndan kapatıldı. Merhaba Windows güç seçenekleri VM tooshut hello VM aşağı içinde kullanırsanız, hala ücretlendirilen hello hello VM için aynı tutar. tooreduce ücretlendirilen hello Klasik Azure portalı hello VM aşağı tooshut gerekir. Merhaba VM artık ihtiyacınız varsa, ilişkili .vhd dosyaları tooavoid depolama ücretleri hello ve toodelete hello VM unutmayın. Daha fazla bilgi için bkz: hello SSS bölümüne [sanal makineler fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Daha Fazla Bilgi
### <a name="resources"></a>Kaynaklar
* Tooa tek sunucu dağıtımı için benzer içerik ilgili SQL Server Business Intelligence ve SharePoint 2013'ın bkz [Windows PowerShell'i kullanın tooCreate bir Azure VM ile SQL Server BI ve SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* SQL Server Business Intelligence ve SharePoint 2013'ün birden çok sunucu dağıtımı için benzer içerik ilgili tooa bkz [dağıtmak SQL Server Business Intelligence Azure Virtual Machines'de](https://msdn.microsoft.com/library/dn321998.aspx).
* SQL Server Business Intelligence Azure sanal makineleri, ilgili toodeployments genel bilgi için bkz [SQL Server Business Intelligence Azure Virtual Machines'de](virtual-machines-windows-classic-ps-sql-bi.md).
* Azure işlem ücretleri hello maliyeti hakkında daha fazla bilgi için bkz: hello sanal makineleri sekmesinde [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Topluluk içeriği
* Nasıl toocreate bir Raporlama Hizmetleri yerel modu rapor sunucusunda komut dosyasını kullanmadan adım adım yönergeler için bkz: [barındırma SQL Raporlama hizmeti Azure sanal makine üzerinde](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Azure vm'lerinde SQL Server için bağlantılar tooother kaynaklar
[SQL Server üzerinde Azure sanal makinelere genel bakış](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

