---
title: "aaaConnect Windows bilgisayarları tooAzure günlük analizi | Microsoft Docs"
description: "Bu makalede, hello Microsoft İzleme Aracısı'nı (MMA) özelleştirilmiş bir sürümünü kullanarak, şirket içi altyapı toohello günlük analizi hizmeti hello adımları tooconnect hello Windows bilgisayarları gösterir."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Windows bilgisayarları toohello günlük analizi hizmeti Azure connect

Bu makalede hello adımları tooconnect Windows bilgisayarları şirket içi altyapı tooOMS alanlarınızı hello Microsoft İzleme Aracısı'nı (MMA) özelleştirilmiş bir sürümünü kullanarak gösterir. Tüm bunları sırayla tooonboard toosend veri toohello günlük analizi hizmeti ve tooview ve bu verileri act istediğiniz hello bilgisayarları için aracıları bağlanmak ve tooinstall gerekir. Her bir aracının toomultiple çalışma alanları bildirebilirsiniz.

Kurulum, komut satırı kullanılarak aracıları yükleyebilirsiniz veya ile istenen durum yapılandırması (DSC) Azure Automation.  

>[!NOTE]
Azure'da çalışan sanal makineler için yükleme hello kullanarak basitleştirebilirsiniz [sanal makine uzantısı](log-analytics-azure-vm-extension.md).

Internet bağlantısı olan bilgisayarlarda hello Aracısı hello bağlantı toohello Internet toosend veri tooOMS kullanır. Internet bağlantısına sahip olmayan bilgisayarlar için bir proxy veya hello kullanabilirsiniz [OMS ağ geçidi](log-analytics-oms-gateway.md).

Windows bilgisayarları tooOMS bağlanma üç basit adımları kullanarak basittir:

1. Merhaba OMS Portalı'ndan Hello Aracısı kurulum dosyasını indirin
2. Seçtiğiniz hello yöntemi kullanarak hello aracı yükleme
3. Gerekirse ek çalışma alanları ekleyin veya Hello Aracısı Yapılandırma

yüklü ve aracıları yapılandırdıktan sonra hello Aşağıdaki diyagramda hello arasındaki ilişkiyi Windows bilgisayarları ve OMS gösterir.

![OMS doğrudan Aracısı diyagramı](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

BT güvenlik ilkeleri, ağ tooconnect toohello Internet bilgisayarları izin vermiyorsa, bilgisayarları tooconnect toohello OMS ağ geçidi yapılandırabilirsiniz. Daha fazla bilgi ve tooconfigure, sunucuları toocommunicate bir OMS ağ geçidi toohello OMS hizmeti aracılığıyla nasıl görürüm adımlar [hello OMS ağ geçidi kullanarak bilgisayarları tooOMS bağlanmak](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Sistem gereksinimleri ve gerekli yapılandırma
Yükleyip aracıları dağıtmak için önce hello gereksinimleri karşılaması ayrıntıları tooensure aşağıdaki hello gözden geçirin.

- Yalnızca Windows Server 2008 SP 1 veya sonrasını çalıştıran bilgisayarlar veya Windows 7 SP1 hello OMS MMA yükleyebilirsiniz ya da daha sonra.
- Bir Azure aboneliği gerekir.  Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md).
- Her Windows bilgisayarı mümkün tooconnect toohello Internet olmalıdır HTTPS veya toohello OMS ağ geçidi kullanarak. Bu bağlantıyı doğrudan hello OMS ağ geçidi veya proxy aracılığıyla olabilir.
- Tek başına bilgisayarların, sunucuların ve sanal makinelerin hello OMS MMA yükleyebilirsiniz. Tooconnect Azure barındırılan sanal makineleri tooOMS istiyorsanız, bkz: [bağlanmak Azure sanal makineleri tooLog Analytics](log-analytics-azure-vm-extension.md).
- Merhaba aracının toouse TCP bağlantı noktası 443 çeşitli kaynaklar için gerekir.

### <a name="network"></a>Ağ

Hello bağlantı noktası numaraları ve etki alanı URL'leri dahil erişim toonetwork kaynakları hello OMS hizmetiyle Windows aracıları tooconnect tooand kayıt için olmaları gerekir.

- Proxy sunucuları için uygun proxy sunucu kaynakları Aracısı ayarlarında yapılandırılan hello tooensure gerekir.
- Erişim toohello Internet kısıtlamak, güvenlik duvarları için siz veya ağ mühendisleri, güvenlik duvarı toopermit erişim tooOMS tooconfigure gerekir. Aracı ayarlarında bir işlem yapılması gerekmez.

Aşağıdaki tablonun hello iletişimi için gerekli kaynakları gösterir.

>[!NOTE]
>Bazı kaynaklar aşağıdaki Merhaba, operasyonel Öngörüler, günlük analizi için önceki bir ad olduğu gerekeceğinden buraya.

| Aracı Kaynağı | Bağlantı Noktaları | HTTPS denetlemesini atlama |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Evet |
| *.oms.opinsights.azure.com | 443 | Evet |
| *.blob.core.windows.net | 443 | Evet |
| *.azure-automation.net | 443 | Evet |



## <a name="download-hello-agent-setup-file-from-oms"></a>OMS Hello Aracısı kurulum dosyasını indirin
1. Merhaba OMS portalında, hello **genel bakış** hello sayfasında, **ayarları** döşeme.  Merhaba tıklatın **bağlı kaynakları** sekmesini hello üstünde.  
    ![Bağlı kaynaklar sekmesi](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Tıklatın **Windows sunucuları** ve ardından **Windows Aracısı indirme** geçerli tooyour bilgisayar işlemci türü toodownload hello kurulum dosyası.
3. Merhaba sağında üzerinde **çalışma alanı kimliği**hello Kopyala simgesine tıklayın ve hello kimliği Not Defteri'ne yapıştırın.
4. Merhaba sağında üzerinde **birincil anahtar**hello Kopyala simgesine tıklayın ve başlangıç anahtarı Not Defteri'ne yapıştırın.     

## <a name="install-hello-agent-using-setup"></a>Kurulumu kullanarak hello aracı yükleme
1. Kurulum tooinstall hello Aracısı toomanage istediğiniz bir bilgisayarda çalıştırın.
2. Merhaba Hoş Geldiniz sayfasında, tıklatın **sonraki**.
3. Merhaba lisans koşulları sayfasında, hello lisans okuyun ve ardından **ediyorum**.
4. Merhaba hedef klasörü sayfasında, değiştirmek veya hello varsayılan yükleme klasörünü ve ardından **sonraki**.
5. Hello aracı Kur seçenekleri sayfasında, tooconnect hello Aracısı tooAzure günlük analizi (OMS), Operations Manager'ı seçin veya tooconfigure hello aracının daha sonra isterseniz hello seçimler boş bırakabilirsiniz. **İleri**’ye tıklayın.   
    - Tooconnect tooAzure günlük analizi (OMS) seçerseniz, hello Yapıştır **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** hello önceki yordamda Not Defteri'ne kopyalanan ve ardından  **Sonraki**.  
        ![Çalışma alanı kimliği ve birincil anahtar yapıştırın](./media/log-analytics-windows-agents/connect-workspace.png)
    - Tooconnect tooOperations Yöneticisi'ni seçerseniz, hello yazın **yönetim grubu adı**, **Management Server** adı ve **yönetim sunucusu bağlantı noktası**ve ardından **Sonraki**. Merhaba aracı eylem hesabı sayfada hello yerel sistem hesabı veya yerel etki alanı hesabı seçin ve ardından **sonraki**.  
        ![Yönetim grubu Yapılandırması](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![aracı eylem hesabı](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Merhaba hazır tooInstall sayfasında, seçimlerinizi gözden geçirin ve ardından **yükleme**.
7. Yapılandırma başarıyla tamamlandı hello üzerinde sayfasında, **son**.
8. Tamamlandığında, hello **Microsoft İzleme Aracısı** görünür **Denetim Masası**. Vardır, yapılandırmanızı gözden geçirin ve bu hello aracı bağlı tooOperational Öngörüler (OMS) olduğunu doğrulayın. Aracı bağlı tooOMS hello belirten bir ileti görüntülenir: **hello Microsoft İzleme Aracısı toohello Microsoft Operations Management Suite hizmeti başarıyla bağlandı.**

## <a name="configure-proxy-settings"></a>Proxy ayarlarını yapılandır

Yordam tooconfigure proxy ayarlarını hello Microsoft Monitoring Agent Denetim Masası'nı kullanarak aşağıdaki hello kullanabilirsiniz. Her sunucu için bu yordamı toouse gerekir. Çok sayıda sunucuya tooconfigure gereksiniminiz varsa, daha kolay toouse bir komut dosyası tooautomate bulabileceğiniz bu işlem. Bu durumda, hello sonraki yordama bakın [tooconfigure hello betik kullanarak Microsoft İzleme Aracısı için proxy ayarlarını](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>Microsoft Monitoring Agent Denetim Masası'nı kullanarak hello için tooconfigure proxy ayarları
1. **Denetim Masası**'nı açın.
2. **Microsoft İzleme Aracısı**'nı açın.
3. Merhaba tıklatın **Proxy ayarlarını** sekmesi.  
    ![ara sunucu ayarları sekmesi](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Seçin **bir proxy sunucu kullanacak** hello URL'sini yazın ve bağlantı noktası numarası, gerekli, benzer toohello örnekte gösterilen ise. Proxy sunucusu kimlik doğrulaması gerektiriyorsa, hello kullanıcı adı ve parola tooaccess hello proxy sunucusu yazın.


### <a name="verify-agent-connectivity-toooms"></a>Aracı bağlantısı tooOMS doğrulayın

Kolayca aracılarınızı hello aşağıdaki yordamı kullanarak OMS ile iletişim kuran olup olmadığını doğrulayın:

1.  Merhaba Windows Aracısı ile Merhaba bilgisayarda Denetim Masası açın.
2.  Microsoft Monitoring Agent'ı açın.
3.  Hello Azure günlük analizi (OMS) sekmesine tıklayın.
4.  Merhaba Durum sütununda bu hello aracı toohello Operations Management Suite hizmeti başarıyla bağlandı görmeniz gerekir.

![bağlı aracı](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>Merhaba betik kullanarak Microsoft Monitoring Agent için tooconfigure proxy ayarları
Aşağıdaki örnek, bilgi belirli tooyour ortamıyla güncelleştirme, bir PS1 dosya adı uzantısıyla kaydedin ve ardından hello betik toohello OMS hizmetine doğrudan bağlanan her bilgisayarda çalıştırın hello kopyalayın.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Merhaba komut satırını kullanarak hello aracı yükleme
- Değiştirebilirsiniz ve hello komut satırını kullanarak örnek tooinstall hello aracı aşağıdaki hello kullanabilirsiniz. Merhaba örnek tam olarak sessiz yükleme gerçekleştirir.

    >[!NOTE]
    Bir aracı tooupgrade istiyorsanız, toouse hello günlük analizi gerekir betik API'si. Merhaba sonraki bölümde tooupgrade bir aracı bakın.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

Merhaba Aracısı'nın kullandığı IExpress kendi ayıklayıcısı hello kullanarak `/c` komutu. Merhaba komut satırı anahtarları adresindeki görebilirsiniz [IExpress komut satırı anahtarları](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) ve ardından güncelleştirme hello örnek toosuit gereksinimlerinizi.

|MMA özgü seçenekleri                   |Notlar         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = Yapılandır hello Aracısı tooreport tooa çalışma alanı                |
|OPINSIGHTS_WORKSPACE_ID                | Merhaba çalışma tooadd için çalışma alanı kimliği (GUID)                    |
|OPINSIGHTS_WORKSPACE_KEY               | Çalışma alanı anahtarı kullanılan tooinitially hello çalışma ile kimlik doğrulaması |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Merhaba çalışma bulunduğu hello bulut ortamını belirtin <br> 0 = azure ticari bulut (varsayılan) <br> 1 azure kamu = |
|OPINSIGHTS_PROXY_URL               | Merhaba proxy toouse için URI |
|OPINSIGHTS_PROXY_USERNAME               | Kullanıcı adı tooaccess doğrulanmış bir proxy |
|OPINSIGHTS_PROXY_PASSWORD               | Parola tooaccess doğrulanmış bir proxy |

>[!NOTE]
tooavoid basarsa hello komut satırı uzunluğunu IExpress, yapılandırılmış hiçbir çalışma alanıyla hello aracısı yükleyin ve ardından bir betik tooset yapılandırmasını hello çalışma alanı için kullanın.

>[!NOTE]
Alırsanız bir `Command line option syntax error.` hello kullanırken `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametresi, geçici çözüm aşağıdaki hello kullanabilirsiniz:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Bir komut dosyası kullanarak bir çalışma alanı Ekle
Aşağıdaki örneğine hello ile Merhaba günlük analizi aracı komut dosyası API kullanarak bir çalışma alanı ekleyin:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd Azure ABD devlet kurumları, komut dosyası örneği aşağıdaki kullanım hello için çalışma:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Sütun hello komut satırı kullandıysanız, daha önce tooinstall komut dosyası veya hello Aracısı'nı yapılandırma `EnableAzureOperationalInsights` tarafından değiştirildi `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Azure Otomasyonu'nda DSC kullanarak hello aracı yükleme

Azure Otomasyonu'nda DSC kullanarak betik örnek tooinstall hello aracısını aşağıdaki hello kullanabilirsiniz. Merhaba örneği yükler hello hello tarafından tanımlanan 64-bit Aracısı `URI` değeri. Merhaba URI değerini değiştirerek hello 32-bit sürümünü de kullanabilirsiniz. Merhaba URI'ler iki sürümü vardır:

- Windows 64-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828603
- Windows 32-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
Bu yordam ve komut dosyası örneği var olan bir aracıyı yükseltmez.

1. Merhaba xPSDesiredStateConfiguration DSC modülü içe gelen [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) Azure Otomasyonu içine.  
2.  İçin Azure Otomasyonu değişken varlıkları oluşturma *OPSINSIGHTS_WS_ID* ve *OPSINSIGHTS_WS_KEY*. Ayarlama *OPSINSIGHTS_WS_ID* tooyour OMS günlük analizi çalışma alanı kimliği ve *OPSINSIGHTS_WS_KEY* çalışma alanınızın toohello birincil anahtar.
3.  Aşağıdaki komut dosyası ve MMAgent.ps1 Kaydet hello kullanın
4.  Değiştirebilirsiniz ve Azure Otomasyonu'nda DSC kullanarak örnek tooinstall hello aracısını aşağıdaki hello kullanabilirsiniz. MMAgent.ps1 hello Azure Otomasyon arabirimi veya cmdlet'ini kullanarak Azure Automation'a aktarabilir.
5.  Bir düğüm toohello yapılandırması atayın. 15 dakika içinde hello düğüm yapılandırmasını denetler ve hello MMA toohello düğümü gönderilir.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Merhaba son ProductID değerini alın

Merhaba `ProductId value` hello MMAgent.ps1 betik benzersiz tooeach Aracısı sürümüdür. Her bir aracının güncelleştirilmiş bir sürümü yayımlandığında, hello ProductID değerini değiştirir. Bu nedenle, Hello ProductID hello gelecekteki değiştiğinde, basit bir komut dosyası kullanarak hello aracı sürümü bulabilirsiniz. Bir test sunucusunda yüklü hello en son aracı sürümü aldıktan sonra aşağıdaki komut dosyası tooget yüklü hello ProductID değeri hello kullanabilirsiniz. Merhaba son ProductID değerini kullanarak hello MMAgent.ps1 betik hello değerinde güncelleştirebilirsiniz.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Bir aracı el ile yapılandırma veya ek çalışma alanları ekleme
Aracıları yüklediyseniz bunları yapılandırmadı ancak veya hello Aracısı tooreport toomultiple çalışma alanları istiyorsanız, bilgi tooenable bir aracı aşağıdaki hello kullanın ya da yeniden yapılandırın. Merhaba Aracısı yapılandırdıktan sonra hello Aracısı hizmeti ile kaydeder ve gerekli yapılandırma bilgilerini ve çözüm bilgileri içeren yönetim paketleri alır.

1. Merhaba Microsoft İzleme Aracısı yükledikten sonra açmak **Denetim Masası**.
2. Açık **Microsoft İzleme Aracısı** ve hello ardından **Azure günlük analizi (OMS)** sekmesi.   
3. Tıklatın **Ekle** tooopen hello **günlük analizi çalışma alanı Ekle** kutusu.
4. Yapıştır hello **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** tooadd istediğiniz ve ardından hello çalışma alanı için bir önceki yordamda Not Defteri'ne kopyalanan **Tamam**.  
    ![Operasyonel Öngörüler yapılandırın](./media/log-analytics-windows-agents/add-workspace.png)

Merhaba aracısı tarafından izlenen bilgisayarlardan toplanan veriler sonra OMS tarafından izlenen bilgisayarlar hello sayısı hello hello OMS portalında görünür **bağlı kaynakları** sekmesinde **ayarları** olarak  **Bağlı olan sunucuları**.


## <a name="toodisable-an-agent"></a>toodisable bir aracı
1. Merhaba aracıyı yükledikten sonra açmak **Denetim Masası**.
2. Microsoft Monitoring Agent'ı açın ve hello ardından **Azure günlük analizi (OMS)** sekmesi.
3. Bir çalışma alanını seçin ve ardından **kaldırmak**. Bu adım için diğer çalışma alanları yineleyin.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>İsteğe bağlı olarak, aracıları tooreport tooan Operations Manager yönetim grubunu yapılandırın

BT altyapınızın Operations Manager'ı kullanırsanız, hello MMA aracı Operations Manager aracısı olarak kullanabilirsiniz.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>tooconfigure MMA aracıları tooreport tooan Operations Manager yönetim grubu
1.  Merhaba Aracısı yüklendiği hello bilgisayarda açın **Denetim Masası**.  
2.  Açık **Microsoft İzleme Aracısı** ve hello ardından **Operations Manager** sekmesi.  
    ![Microsoft İzleme Aracısı Operations Manager sekmesi](./media/log-analytics-windows-agents/om-mg01.png)
3.  Operations Manager sunucularınızın Active Directory ile tümleştirme varsa, tıklatın **yönetim grubu atamalarını AD DS'den otomatik olarak güncelleştir**.
4.  Tıklatın **Ekle** tooopen hello **bir yönetim grubu Ekle** iletişim kutusu.  
    ![Microsoft İzleme Aracısı Yönetim Grubu Ekle](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  İçinde **yönetim grubu adı** kutusu, yönetim grubunuzun türü hello adı.
6.  Merhaba, **birincil yönetim sunucusu** kutusu, türü hello hello birincil yönetim sunucusunun bilgisayar adı.
7.  Merhaba, **yönetim sunucusu bağlantı noktası** kutusunda türü hello TCP bağlantı noktası numarası.
8.  Altında **aracı eylem hesabı**, hello yerel sistem hesabı veya yerel etki alanı hesabı seçin.
9.  Tıklatın **Tamam** tooclose hello **bir yönetim grubu Ekle** iletişim kutusunu ve ardından **Tamam** tooclose hello **Microsoft Monitoring Agent özellikleri**iletişim kutusu.


## <a name="next-steps"></a>Sonraki adımlar

- [Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.
