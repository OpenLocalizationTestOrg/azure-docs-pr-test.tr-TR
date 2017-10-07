---
title: "aaaUsing Windows PowerShell betikleri tooPublish tooDev ve Test ortamları | Microsoft Docs"
description: "Nasıl Visual Studio toopublish toodevelopment ve test ortamları toouse Windows PowerShell komut dosyaları hakkında bilgi edinin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Windows PowerShell kullanarak toopublish toodev ve test ortamları komut dosyaları
Visual Studio'da bir web uygulaması oluşturduğunuzda, bir Web uygulamasını Azure App Service veya bir sanal makine olarak Web sitesi tooAzure sonraki tooautomate hello yayımlanmasıyla kullanabileceğiniz bir Windows PowerShell Betiği oluşturabilir. Düzenle ve gereksinimlerinizi hello Visual Studio Düzenleyicisi toosuit hello Windows PowerShell betik genişletin veya hello betik varolan derleme, test ve yayımlama betikleri ile tümleştirin.

Bu komut dosyalarını kullanarak, siteniz geçici kullanım için özelleştirilmiş sürümleri (geliştirme ve test ortamları olarak da bilinir) sağlayabilirsiniz. Örneğin, olabilir Web sitenizi belirli bir sürümü hazırlık yuvasındaki Web sitesi toorun üzerinde hello veya bir Azure sanal makinesi üzerinde bir test paketine ayarlayın, bir hatayı yeniden, önerilen bir değişikliğin hata düzeltmesi, deneme test veya bir tanıtım veya sunumu için özel bir ortamı ayarlama. Projenizi yayımlayan bir komut dosyası oluşturduktan sonra aynı ortamları hello betik gerektiği gibi yeniden çalıştırarak yeniden veya hello betiği, kendi web uygulama toocreate yapı ile test etmek için özel bir ortam çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor
* Azure SDK 2.3 veya üzeri. Bkz: [Visual Studio indirmeleri](http://go.microsoft.com/fwlink/?LinkID=624384) daha fazla bilgi için.

Web projeleri için hello Azure SDK'sı toogenerate hello betikleri gerekmez. Bu özellik web projeleri, olmayan bulut Hizmetleri web rolleri için kullanılabilir.

* Azure PowerShell 0.7.4 veya sonraki bir sürümü. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) veya sonraki bir sürümü.

## <a name="additional-tools"></a>Ek araçlar
Ek araçlar ve kaynaklar Azure geliştirme için Visual Studio de PowerShell ile çalışmak için kullanılabilir. Bkz: [Visual Studio için PowerShell Araçları](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Komut dosyaları yayımlama Hello oluşturma
Merhaba oluşturabileceğiniz izleyerek yeni bir proje oluşturduğunuzda, Web sitenizi barındıran bir sanal makine için komut dosyaları yayımlama [bu yönergeleri](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Ayrıca [oluşturmak betikler web uygulamaları için Azure App Service'te yayımlama](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Visual Studio'nun oluşturduğu komut dosyaları
Visual Studio'nun oluşturduğu adlı bir çözüm düzeyi klasör **PublishScripts** sanal makineniz veya Web sitesi ve hello kullanabileceğiniz işlevleri içeren bir modül için bir yayımlama komut dosyası iki Windows PowerShell dosyaları içerir komut dosyaları. Visual Studio, ayrıca, dağıttığınız hello proje hello ayrıntılarını belirtir hello JSON biçiminde bir dosya oluşturur.

### <a name="windows-powershell-publish-script"></a>Windows PowerShell komut dosyası yayımlama
komut dosyası yayımlama Hello belirli içeren tooa Web sitesi ya da sanal makineyi dağıtma adımları yayımlayın. Visual Studio için Windows PowerShell geliştirme renklendirme sözdizimi sağlar. Merhaba işlevler kullanılabilir ve değişen gereksinimlerinizi hello betik toosuit hello işlevlerde serbestçe düzenleyebilirsiniz için Yardım.

### <a name="windows-powershell-module"></a>Windows PowerShell Modülü
Merhaba Visual Studio'nun oluşturduğu modülü hello işlevleri içeren Windows PowerShell komut dosyası kullanan yayımlayın. Bunlar Azure PowerShell işlevleri ve değiştiren hedeflenen toobe değildir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.

### <a name="json-configuration-file"></a>JSON yapılandırma dosyası
Merhaba JSON dosyası hello oluşturulan **yapılandırmaları** klasörü ve tam olarak hangi kaynaklara toodeploy tooAzure belirtir yapılandırma verilerini içerir. Merhaba Visual Studio'nun oluşturduğu hello dosya proje-adı-WAWS-bir sanal makine oluşturduysanız, bir Web sitesi ya da proje adı-VM-dev.json oluşturduysanız dev.json adıdır. Bir Web sitesi oluşturduğunuzda oluşturan bir JSON yapılandırma dosyası bir örneği burada verilmiştir. Merhaba değerleri çoğu kendinden açıklamalıdır. projenizin adına eşleşmeyebilir şekilde hello Web sitesi adı Azure tarafından oluşturulur.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Bir sanal makine oluşturduğunuzda, hello JSON yapılandırma dosyası benzer toohello aşağıdaki görünür. Bir bulut hizmeti hello sanal makine için bir kapsayıcı olarak oluşturulduğunu unutmayın. Hello sanal makine için yerel makine, Uzak Masaüstü ve Windows PowerShell toohello Web sitesi yayımlama imkan tanıyan Web dağıtımı, uç nokta yanı sıra hello normal uç noktaları için HTTP ve HTTPS üzerinden web access içerir.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Merhaba çalıştırdığınızda neler hello JSON yapılandırma toochange düzenleyebilirsiniz betikleri yayımlayın. Merhaba `cloudService` ve `virtualMachine` bölümleri gereklidir, ancak hello silebilirsiniz `databases` ihtiyaç duymuyorsanız bölüm. Visual Studio oluşturan hello varsayılan yapılandırma dosyasında boş hello özellikleri isteğe bağlıdır; Merhaba varsayılan yapılandırma dosyasında değerleri olan gereklidir.

Azure'da tek üretim site yerine birden çok dağıtım ortamı (yuvaları da bilinir) sahip bir Web sitesi varsa, hello Web hello JSON yapılandırma dosyasında hello adı hello yuva adı dahil edebilirsiniz. Adlı bir Web sitesi varsa, örneğin, **Sitem** ve onu adlı yuvasını **test** hello URI Sitem test.cloudapp.net, ancak hello doğru adı toouse hello yapılandırma dosyasında mysite(test) sonra . Merhaba Web sitesi ve yuvaları aboneliğinizde zaten varsa yalnızca bunu yapabilirsiniz. Yoksa, hello yuvası belirtmeden hello komut dosyası çalıştırarak hello Web sitesi oluşturun, sonra oluşturmak hello hello yuvasına [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ve bundan sonra hello betik hello değiştirilmiş Web sitesi adı ile çalıştırın. Web uygulamaları için dağıtım yuvası hakkında daha fazla bilgi için bkz: [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Nasıl toorun hello yayımlama betikleri
Önce bir Windows PowerShell Betiği çalıştırılmadı, hello yürütme İlkesi tooenable betikleri toorun ayarlamanız gerekir. Güvenlik Açığı toomalware veya komut dosyaları yürütme içeren virüslere iseniz Windows PowerShell komut dosyası çalıştırarak bir güvenlik özelliği tooprevent kullanıcıların budur.

### <a name="run-hello-script"></a>Merhaba komut dosyasını çalıştır
1. Projeniz için Hello Web dağıtım paketi oluşturun. Bir Web dağıtımı toocopy tooyour Web sitesi ya da sanal makineyi istediğiniz dosyaları içeren sıkıştırılmış bir arşiv (.zip dosyası) paketidir. Visual Studio'da Web dağıtımı paketleri için herhangi bir web uygulaması oluşturabilirsiniz.

![Web oluşturma paketini dağıtma](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Daha fazla bilgi için bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx). Merhaba, Web dağıtımı paketi oluşturulmasını hello bölümde açıklandığı gibi otomatikleştirebilirsiniz **özelleştirme ve hello genişletme yayımlama betikleri** bu konuda daha sonra.

1. İçinde **Çözüm Gezgini**hello betik hello bağlam menüsünü açın ve ardından **PowerShell ISE ile açmak**.
2. Bu hello bu bilgisayarda Windows PowerShell komut dosyalarını çalıştırmak ilk kez kullanıyorsanız, komutu aşağıdaki türü hello ve yönetici ayrıcalıkları ile bir komut istemi penceresi açın:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. İçinde tooAzure komutu aşağıdaki hello kullanarak oturum açın.

    ```powershell
    Add-AzureAccount
    ```

    İstendiğinde, kullanıcı adı ve parola sağlayın.

    Merhaba betik Otomasyon gerçekleştirirken Azure kimlik bilgileri sağlama bu yöntem çalışmaz unutmayın. Bunun yerine, hello .publishsettings dosyasını tooprovide kimlik bilgileri kullanmanız gerekir. Merhaba komutu, yalnızca bir kez kullanın **Get-AzurePublishSettingsFile** toodownload hello dosya Azure'dan ve bundan sonra kullanın **Import-AzurePublishSettingsFile** tooimport hello dosya. Ayrıntılı yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

4. (İsteğe bağlı) Toocreate Azure istiyorsanız hello sanal makine, veritabanı ve web uygulamanızı yayımlamayı olmadan Web sitesi gibi kaynakları hello kullan **Yayımla WebApplication.ps1** hello komutunu **-yapılandırma** değişkenini toohello JSON yapılandırma dosyası. Bu komut satırı hello JSON yapılandırma dosyası toodetermine hangi kaynaklara toocreate kullanır. Diğer komut satırı bağımsız değişkenleri hello varsayılan ayarları kullandığından, hello kaynakları oluşturur, ancak web uygulamanızı yayımlamak değil. Merhaba – ayrıntılı seçeneği, neler hakkında daha fazla bilgi sağlar.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Kullanım hello **Yayımla WebApplication.ps1** komut örnekleri tooinvoke hello betik aşağıdaki hello birinde gösterildiği gibi ve web uygulamanızı yayımlayın. Toooverride hello varsayılan ayarları herhangi bir hello için hello abonelik adı gibi diğer bağımsız değişkenler gerekiyorsa paket adı, sanal makine kimlik bilgileri veya veritabanı sunucusu kimlik bilgileri yayımlama, bu parametreleri belirtebilirsiniz. Kullanım hello **– ayrıntılı** hello ilerleme durumu hakkında daha fazla bilgi işlem yayımlama hello toosee seçeneği.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Bir sanal makine oluşturuyorsanız, hello komutu hello aşağıdaki gibi görünür. Bu örnek ayrıca nasıl toospecify hello birden çok veritabanı için kimlik bilgilerini gösterir. Merhaba bu komut dosyaları oluşturmak için sanal makinelerde, hello SSL sertifikası bir güvenilen kök yetkilisi değil. Bu nedenle, toouse hello gerekir **– AllowUntrusted** seçeneği.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    Merhaba betik veritabanları oluşturabilirsiniz, ancak veritabanı sunucuları oluşturmaz. Bir veritabanı sunucusu toocreate istiyorsanız hello kullanabilirsiniz **yeni AzureSqlDatabaseServer** hello Azure modülü işlevinde.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Özelleştirme ve hello genişletme betikleri yayımlama
Merhaba özelleştirebilirsiniz komut dosyası ve JSON yapılandırma dosyası yayımlayın. Merhaba hello Windows PowerShell modülü işlevlerde **AzureWebAppPublishModule.psm1** değiştiren hedeflenen toobe değildir. Yalnızca toospecify farklı bir veritabanı veya bazı hello hello sanal makinenin özelliklerini değiştirmek istiyorsanız, hello JSON yapılandırma dosyasını düzenleyin. Derleme ve dağıtım projenizi sınamayı hello betik tooautomate tooextend hello işlevselliğini istiyorsanız işlevi saplamalar uygulayabilirsiniz **Yayımla WebApplication.ps1**.

tooautomate, projenizi derleme ekleyin MSBuild çok çağıran kodu`New-WebDeployPackage` Bu kod örneğinde gösterildiği gibi. Hello yolu toohello MSBuild komut yüklediğiniz Visual Studio hello sürümüne bağlı olarak farklılık gösterir. tooget hello doğru yolu, hello işlevi kullanabilirsiniz **Get-MSBuildCmd**, bu örnekte gösterildiği gibi.

### <a name="tooautomate-building-your-project"></a>projenizi derleme tooautomate
1. Merhaba eklemek `$ProjectFile` hello genel param bölümünde parametresi.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copy Hello işlevi `Get-MSBuildCmd` komut dosyanızı içine.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Değiştir `New-WebDeployPackage` aşağıdaki kod ve satır hello oluştururken hello yer tutucuları değiştirmek hello ile `$msbuildCmd`. Visual Studio 2015 için kodudur. Visual Studio 2013 kullanıyorsanız, hello değiştirme **VisualStudioVersion** özelliği aşağıdaki çok`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild, web uygulaması, MsBuild.exe kullanın. MSBuild komut satırı başvurusu, Yardım için bkz: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Merhaba yapı komutu yürütme Başlat

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Merhaba çağrısı `New-WebDeployPackage` bu satırı önce işlevin: `$Config = Read-ConfigFile $Configuration` web uygulamaları için veya `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` sanal makineler için.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Özelleştirilmiş hello betik geçirme hello kullanarak komut satırından çağırma `$Project` olduğu gibi hello aşağıdaki örnek komut satırı bağımsız değişkeni.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate uygulamanızın veya test ekleme kodu çok`Test-WebApplication`. Merhaba satırlarında emin toouncomment olması **Yayımla WebApplication.ps1** burada bu işlevler adı verilir. Uygulaması sağlamazsanız, projenizi Visual Studio ile el ile oluşturabilir ve sonra çalışma hello yayımlama betik toopublish tooAzure.

## <a name="publishing-function-summary"></a>Özet yayımlama işlevi
Merhaba Windows PowerShell komut isteminde kullanabileceğiniz işlevleri tooget yardımını hello komutunu kullanın `Get-Help function-name`. Merhaba Yardımı parametre Yardım ve örnekler içerir. aynı Yardım metni, ayrıca hello betik kaynak dosyalarında hello **AzureWebAppPublishModule.psm1** ve **Yayımla WebApplication.ps1**. Visual Studio dilinizde Hello komut dosyası ve Yardım yerelleştirilmiştir.

**AzureWebAppPublishModule**

| İşlev adı | Açıklama |
| --- | --- |
| Ekleme AzureSQLDatabase |Yeni bir Azure SQL veritabanı oluşturur. |
| Ekleme AzureSQLDatabases |Visual Studio'nun oluşturduğu hello JSON yapılandırma dosyası hello değerlerinden Azure SQL veritabanı oluşturur. |
| Add-AzureVM |Bir Azure sanal makine oluşturur ve VM hello hello URL'sini dağıtılan döndürür. Merhaba işlevi hello önkoşulları ve ardından çağrıları hello ayarlar **New-AzureVM** (Azure Modülü) toocreate yeni bir sanal makine işlev. |
| Ekleme AzureVMEndpoints |Yeni bir giriş uç noktaları tooa sanal makine ekler ve hello yeni uç nokta ile Merhaba sanal makine döndürür. |
| Ekleme AzureVMStorage |Yeni bir Azure depolama hesabı hello geçerli abonelikte oluşturur. Merhaba hello hesap adını "benzersiz bir alfasayısal dize tarafından izlenen devtest" ile başlar. Merhaba işlevi hello hello yeni depolama hesabı adını döndürür. Bir konumu veya hello yeni depolama hesabı için bir benzeşim grubu belirtmeniz gerekir. |
| Ekleme AzureWebsite |Merhaba belirtilen adı ve konumu ile bir Web sitesi oluşturur. Bu işlev hello çağırır **yeni AzureWebsite** hello Azure modülü işlevinde. Merhaba abonelik hello belirtilen ada sahip bir Web sitesi içermiyorsa, bu işlev hello Web sitesi oluşturur ve bir Web sitesi nesnesi döndürür. Aksi takdirde, döndürür `$null`. |
| Yedekleme abonelik |Kaydeder hello hello Azure geçerli abonelikte `$Script:originalSubscription` betik kapsamında değişken. Bu işlev hello geçerli Azure aboneliği kaydeder (ile alınan `Get-AzureSubscription -Current`) ve depolama hesabı ve bu komut dosyası tarafından değiştirilen hello abonelik (Merhaba değişkeninde depolanan `$UserSpecifiedSubscription`) ve betik kapsamında, depolama hesabı. Merhaba değerleri kaydederek bir işlev gibi kullanabileceğiniz `Restore-Subscription`, hello geçerli durumu değişirse toorestore hello özgün geçerli abonelik ve depolama hesabı toocurrent durumu. |
| Bul-AzureVM |Alır hello Azure sanal makine belirtildi. |
| Biçim DevTestMessageWithTime |Başlangıç tarihi ve saati tooa ileti başına. Bu işlev toohello hata ve ayrıntı akışları yazılan iletilerin için tasarlanmıştır. |
| Get-AzureSQLDatabaseConnectionString |Bir bağlantı dizesi tooconnect tooan Azure SQL veritabanı derler. |
| Get-AzureVMStorage |Döndürür hello hello ilk depolama hesabıyla hello adı deseni adını "devtest*" (büyük küçük harfe duyarlı) hello belirtilen konumda veya benzeşim grubunda. Merhaba, "devtest*" Merhaba konumu ya da benzeşim grubu depolama hesabı eşleşmiyor, hello işlevi yoksayar. Bir konumu veya bir benzeşim grubu belirtmeniz gerekir. |
| Get-MSDeployCmd |Bir komut toorun hello MsDeploy.exe aracını döndürür. |
| AzureVMEnvironment yeni |Bulur veya hello JSON yapılandırma dosyası hello değerlerle eşleştiğini hello Abonelikteki bir sanal makine oluşturur. |
| Yayımlama WebPackage |MsDeploy.exe kullanır ve bir web paketi yayımlayın. Zip dosyası toodeploy kaynakları tooa Web sitesi. Bu işlev, herhangi bir çıktı üretmez. Merhaba çağrısı tooMSDeploy.exe başarısız olursa, hello işlevi bir özel durum oluşturur. daha ayrıntılı çıktı, kullanım hello tooget **-Verbose** seçeneği. |
| Yayımlama WebPackageToVM |Merhaba parametre değerlerini doğrular ve hello çağırır **Yayımla WebPackage** işlevi. |
| Okuma ConfigFile |Merhaba JSON yapılandırma dosyası doğrular ve seçili değerlerinin bir karma tablosu döndürür. |
| Geri yükleme-abonelik |Merhaba geçerli abonelik toohello özgün abonelik sıfırlar. |
| Test-AzureModule |Döndürür `$true` yüklü hello Azure Modül sürümü 0.7.4 ise veya sonraki bir sürümü. Döndürür `$false` hello Modülü yüklü değil veya önceki bir sürümü. Bu işlev hiç parametre yok. |
| Test-AzureModuleVersion |Döndürür `$true` hello Azure modülü hello sürümü 0.7.4 ise veya sonraki bir sürümü. Döndürür `$false` hello Modülü yüklü değil veya önceki bir sürümü. Bu işlev hiç parametre yok. |
| Test-HttpsUrl |Merhaba giriş URL tooa System.Uri nesnesi dönüştürür. Döndürür `$True` hello URL mutlak ve kendi şeması https ise. Döndürür `$false` hello URL göreli kendi şeması HTTPS değil veya hello giriş dizesi dönüştürülmüş tooa URL olamaz. |
| Test-üyesi |Döndürür `$true` bir özellik veya yöntem hello nesnesinin bir üyesi ise. Aksi takdirde, döndürür `$false`. |
| Yazma ErrorWithTime |Geçerli saat ile Merhaba önekli bir hata iletisi yazar. Bu işlev hello çağırır **biçimi DevTestMessageWithTime** hello ileti toohello hata akışı yazmadan önce işlevi tooprepend hello zaman. |
| Yazma HostWithTime |Bir ileti toohello ana bilgisayar programı yazar (**Write-Host**) ile Merhaba geçerli saati öneki. Merhaba etkisini toohello ana bilgisayar programı yazma değişir. Çoğu program barındıran Windows PowerShell Bu iletiler toostandard çıktı yazma. |
| Yazma VerboseWithTime |Geçerli saat ile Merhaba önekli ayrıntılı bir ileti yazar. Çağırır çünkü **Write-Verbose**, selamlama iletisine görüntüler yalnızca hello betik ile Merhaba çalıştığında **ayrıntılı** parametresi veya ne zaman hello **VerbosePreference** tercih olduğu çok ayarlamak**devam**. |

**Yayımlama WebApplication**

| İşlev adı | Açıklama |
| --- | --- |
| AzureWebApplicationEnvironment yeni |Bir Web sitesi veya sanal makine gibi Azure kaynakları oluşturur. |
| WebDeployPackage yeni |Bu işlev uygulanmadı. Projenizi bu işlevi toobuild komutları ekleyebilirsiniz. |
| Yayımlama AzureWebApplication |Bir web uygulaması tooAzure yayımlar. |
| Yayımlama WebApplication |Oluşturur ve Web uygulamaları, sanal makineler, SQL veritabanları ve depolama hesapları için bir Visual Studio web projesini dağıtır. |
| Test-WebApplication |Bu işlev uygulanmadı. Uygulamanız bu işlevi tootest komutları ekleyebilirsiniz. |

## <a name="next-steps"></a>Sonraki adımlar
PowerShell okuyarak komut dosyası hakkında daha fazla bilgi [ile Windows PowerShell komut dosyası](https://technet.microsoft.com/library/bb978526.aspx) ve diğer Azure PowerShell betikleri hello adresindeki [Komut Merkezi](https://azure.microsoft.com/documentation/scripts/).
