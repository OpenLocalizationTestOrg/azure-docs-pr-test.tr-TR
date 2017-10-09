---
title: "Automation DSC sürekli dağıtım Chocolatey aaaAzure | Microsoft Docs"
description: "Azure Otomasyonu DSC ve Chocolatey Paket Yöneticisi'ni kullanarak sürekli dağıtım DevOps.  Örnek tam JSON ARM şablonu ve PowerShell kaynağı."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Kullanım örneği: Sürekli dağıtım tooVirtual Automation DSC ve Chocolatey kullanarak makineleri
Bir DevOps world hello sürekli tümleştirme ardışık düzendeki çeşitli noktalarıyla birçok araçları tooassist vardır.  Azure Otomasyonu istenen durum yapılandırması (DSC) DevOps takımlar uygulayabileceğiniz bir Hoş Geldiniz yeni toplama toohello Seçenekleri ' dir.  Bu makalede, bir Windows bilgisayar için yukarı sürekli dağıtımı (CD) ayarı gösterilmektedir.  Merhaba teknik tooinclude hello rol (bir web sitesi, örneğin gibi) ve orada tooadditional gerektiği gibi kadar Windows bilgisayarları kolayca genişletebilirsiniz rolleri de.

![Iaas VM'ler için sürekli dağıtım](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>Yüksek düzeyde
Buraya gelmeden oldukça bit yoktur, ancak iki ana süreçleriyle Neyse ayrılabilir: 

* Kod yazma, test, oluşturma ve yayımlama hello sistem birincil ve ikincil sürümleri için yükleme paketleri. 
* Oluşturma ve yükleyecek ve hello paketlerinde hello kod yürütmek VM'ler yönetme.  

Her iki çekirdek işlem yerinde olduktan sonra yeni sürümler oluşturulan ve dağıtılan herhangi belirli VM üzerinde çalışan bir kısa adım tooautomatically güncelleştirme hello paketi değil.

## <a name="component-overview"></a>Bileşenine genel bakış
Yöneticileri gibi paketini [get apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) Merhaba Linux dünya ancak değil çok hello Windows dünyada oldukça iyi bilinen sorunlardır.  [Chocolatey](https://chocolatey.org/) böyle bir şey ve Scott Hanselman'ın [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) hello üzerinde harika bir giriş konudur.  Buna koysalar Chocolatey paketlerin merkezi bir depodan tooinstall paketler hello komut satırını kullanarak bir Windows sistemine sağlar.  Oluşturma ve kendi depo yönetme ve Chocolatey belirttiğiniz depoları arasında herhangi bir sayı paketleri yükleyebilirsiniz.

İstenen durum Yapılandırması'nı (DSC) ([genel bakış](https://technet.microsoft.com/library/dn249912.aspx)) için bir makine istediğiniz toodeclare hello yapılandırma sağlayan bir PowerShell aracıdır.  Örneğin, sizin deyin, "yüklü Chocolatey istediğiniz IIS'in yüklenmesini istediğiniz, açılan bağlantı noktası 80 istediğiniz, yüklü sürümü 1.0.0 sitemde istiyorum."  Merhaba DSC Local Configuration Manager, bu yapılandırma (LCM'yi) uygular. Bir DSC çekme sunucusuna bir depo makinelerinizi için yapılandırmaların tutar. Merhaba LCM'yi her makinede hello depolanan yapılandırma yapılandırmasıyla eşleşen düzenli aralıklarla toosee içinde denetler. Bu durum raporu ya da hello saklı yapılandırmasıyla hizalama uygulamasına geri toobring hello makine dener. Merhaba depolanan yapılandırma hello çekme sunucu toocause bir makine veya makineler toocome kümesi hizalama içine değiştirilen hello yapılandırmasıyla düzenleyebilirsiniz.

Azure Otomasyonu runbook'ları, düğümler, kimlik bilgilerini, kaynakları ve zamanlamaları ve genel değişkenler gibi varlıklar kullanarak çeşitli görevleri tooautomate sağlayan Microsoft Azure içinde yönetilen bir hizmettir. Azure Otomasyonu DSC bu Otomasyon yetenek tooinclude PowerShell DSC araçları genişletir.  Mükemmel işte [genel bakış](automation-dsc-overview.md).

DSC kaynağı olan ağ, Active Directory ya da SQL Server yönetme gibi belirli özelliklerine kod bir modüldür.  Merhaba Chocolatey DSC kaynağı nasıl tooaccess (Diğerlerinin yanında), NuGet sunucu paketlerini indirmek, paketleri yüklemek ve benzeri bilir.  Hello diğer birçok DSC kaynakları olan [PowerShell Galerisi](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Bu modüller, Azure Automation DSC çekme Sunucusu'na (sizin tarafınızdan) yüklü olan yapılandırmalarınızı tarafından kullanılabilmesi için.

Resource Manager şablonları altyapınızı - ağları, alt ağlar, ağ güvenliği gibi şeyleri oluşturmanın bildirim temelli bir yolunu sağlar ve yönlendirme, yük Dengeleyiciler, NIC'ler, VM'ler ve benzeri.  Burada bir [makale](../azure-resource-manager/resource-manager-deployment-model.md) karşılaştırır hello Azure Hizmet Yönetimi (ASM veya Klasik) ile Resource Manager dağıtım modeli (tanımlayıcı) hello dağıtım modeli (kesinliği) ve hello çekirdek kaynak anlatılmaktadır sağlayıcıları, işlem, depolama ve ağ.

Bir Resource Manager şablonu bir anahtar özellik sağlandığından kendi yeteneği tooinstall VM uzantısı hello VM içine aynıdır.  VM uzantısı özel bir komut dosyası, virüsten koruma yazılımı yükleme veya bir DSC yapılandırma betiği çalıştırmasını gibi belirli özellikleri vardır.  Diğer türlerde VM uzantıları vardır.

## <a name="quick-trip-around-hello-diagram"></a>Hızlı seyahat geçici hello diyagramı
Merhaba üstten başlayarak, kodunuz yazma derleme, test ve sonra bir yükleme paketi oluşturun.  Chocolatey yükleme paketleri, MSI, MSU, posta gibi çeşitli türlerde işleyebilir.  Ve Chocolatey'nın yerel yetenekleri oldukça tooit yoksa PowerShell toodo hello gerçek yükleme hello gücünü vardır.  Merhaba paket nedenini bildirmeden bir yerde ulaşılabilir – bir paket deposu yerleştirin.  Bu kullanım örnek bir Azure blob storage hesabı ortak bir klasörde kullanır, ancak herhangi bir yere olabilir.  Chocolatey yerel NuGet sunucularını ve birkaç diğerleri paket meta verileri yönetimi için birlikte çalışır.  [Bu makalede](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) hello seçenekleri açıklar.  Bu kullanım örneği NuGet kullanır.  Bir Nuspec paketlerinizi hakkındaki meta verileri ' dir.  Merhaba Nuspec'ın "NuPkg ait derlenmiş" ve bir NuGet Server'da depolanır.  Yapılandırmanıza bir paket adıyla ister ve NuGet sunucusuna başvuran hello Chocolatey DSC kaynağı (şimdi üzerinde hello VM) hello paket alan ve sizin yerinize yükler.  Ayrıca, belirli bir paket sürümü isteyebilir.

Merhaba alt sol bölümünde hello resim, bir Azure Resource Manager (ARM) şablonu yoktur.  Bu kullanım örnekte hello VM uzantısı hello VM hello Azure Otomasyonu DSC istek sunucusuyla (diğer bir deyişle, bir çekme sunucu) ile bir düğüm olarak kaydeder.  Merhaba yapılandırma hello çekme sunucusunda depolanır.  Aslında, iki kez depolandıktan: düz metin olarak ve (için olanlar gibi şeyler hakkında bilmeniz.) bir MOF dosyası olarak derlenmiş sonra bir kez  Merhaba Portalı'nda hello MOF bir "düğümü" (karşılıklı toosimply "yapılandırma") yapılandırmadır.  Merhaba düğüm yapılandırmasını bilir, böylece bir düğümle ilişkili onun hello yapı.  Ayrıntılar aşağıdaki nasıl tooassign hello düğüm yapılandırması toohello düğümünü gösterir.

Büyük olasılıkla zaten hello bit hello üstünde veya çoğuna yaptığınız.  Merhaba nuspec oluşturma, derleme ve bir NuGet Server'da depolama küçük bir şeydir.  Ve sanal makineleri zaten yönetme.  Hello sonraki adım toocontinuous dağıtım alma (bir kez) hello çekme sunucusu kurma, düğümleriniz Bununla (bir kez), kaydetme ve oluşturma ve başlangıç yapılandırması (başlangıçta) depolama gerektirir.  Daha sonra paketleri yükseltilir ve toohello depo dağıtılan hello yapılandırma ve düğüm yapılandırması hello çekme sunucusunda (gerektiği şekilde yineleyin) yenileyin.

ARM şablonu ile başlatıyorsanız değil, bu da normaldir.  PowerShell cmdlet'leri tasarlanmış toohelp hello çekme server ve tüm hello rest, Vm'leri kaydetme vardır. Bu makalede daha fazla ayrıntı için bkz: [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>1. adım: Hello çekme sunucusuna ve Otomasyon hesabı ayarlama
Bir kimliği doğrulanmış (Add-AzureRmAccount) PowerShell komut satırında: (Merhaba çekme sunucu ayarlanması birkaç dakika sürebilir)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Otomasyon hesabınızı bölgeler (diğer adıyla konum) aşağıdaki hello hiçbirine koyabilirsiniz: Doğu ABD 2, Orta Güney ABD, BİZE kamu Virginia, Batı Avrupa, Güneydoğu Asya, Japonya Doğu, Orta Hindistan ve Avustralya Güneydoğu, Orta Kanada Kuzey Avrupa.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>2. adım: VM uzantısı tweaks toohello ARM şablonu
Bu konuda sağlanan (Merhaba PowerShell DSC VM uzantısı kullanılarak) VM kaydı ayrıntılarını [Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Bu adım, yeni VM DSC düğümleri hello listesinde hello çekme sunucusuyla kaydeder.  Bu kayıt parçası hello düğümü yapılandırma uygulanan toobe toohello düğümü belirtme.  Bu düğüm yapılandırması tooexist bu ilk kez Merhaba burada yapılır adım 4. Tamam olacak şekilde hello çekme sunucusunda, henüz yok.  Ancak burada 2. adımda toohave kampanyanızın hello hello düğümün adını ve hello yapılandırmasının hello adı gerekir.  Bu kullanım örnekte hello düğümdür 'isvbox' ve 'ISVBoxConfig' hello yapılandırmadır.  Bu nedenle hello düğüm yapılandırması (toobe DeploymentTemplate.json içinde belirtilen) 'ISVBoxConfig.isvbox' adıdır.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>3. adım: gerekli DSC kaynakları toohello çekme sunucu ekleme
Merhaba PowerShell Galerisi Araçlı tooinstall DSC kaynakları Azure Otomasyon hesabınızda ' dir.  İstediğiniz ve hello "Dağıtma tooAzure Otomasyon" düğmesini tıklatın toohello kaynak gidin.

![PowerShell Galerisi örneği](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Başka bir teknik toohello Azure portalı, yeni modüller veya güncelleştirme mevcut modüllerde toopull sağlar eklenen son. Hello Otomasyon hesabı kaynak, hello varlıklar döşeme ve hello modülleri döşeme son tıklatın.  Hello Gözat galeri simgesi toosee hello hello galerisinde modüllerin listesini sağlar, ayrıntılı bilgiler detaya ve sonuçta Otomasyon hesabınızda içeri aktarın. Bu harika yolu tookeep modüllerinizi toodate zaman tootime gelen yukarı olduğu. Ve hiçbir şey eşitlenmemiş alır diğer modüller tooensure bağımlılıklarla hello içeri aktarma özelliğini denetler.

Ya da hello el ile yaklaşım vardır.  bir Windows bilgisayar için bir PowerShell tümleştirme modülü Hello klasör yapısını hello Azure Automation tarafından beklenen hello klasör yapısı biraz farklıdır.  Bu, küçük bir bölümü'uyguladıkça gerektirir.  Ancak sabit değildir ve kaynak başına yalnızca bir kez gerçekleştirilir (tooupgrade istemediğiniz sürece, gelecekte.)  Bu makalede PowerShell tümleştirme modülleri yazma hakkında daha fazla bilgi için bkz: [için Azure Automation tümleştirme modülleri yazma](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* İş istasyonunuza, aşağıdaki gibi gereken hello modülünü yükleyin:
  * Yükleme [Windows Management Framework v5](http://aka.ms/wmf5latest) (Windows 10 için gerekli değildir)
  * `Install-Module –Name MODULE-NAME`< — alan hello hello PowerShell Galerisi Modülü 
* Kopya hello modülü klasöründen `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa geçici klasörü 
* Örnekler ve belgeler hello ana klasöründen silin 
* Zip hello ana klasörü, tam olarak hello ZIP dosyası adlandırma hello aynı hello klasörü olarak 
* Merhaba ZIP dosyası Azure depolama hesabında blob depolama gibi erişilebilir bir HTTP konuma yerleştirin.
* Bu PowerShell çalıştırın:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

Merhaba dahil örnek cChoco ve xNetworking için aşağıdaki adımları gerçekleştirir. Merhaba bkz [notları](#notes) cChoco için özel işleme.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>4. adım: hello düğümü yapılandırma toohello çekme sunucusu ekleme
Hiçbir şey yoktur hello hakkında özel ilk kez yapılandırmanızı hello çekme sunucusuna ve derleme alma.  Tüm sonraki alma/derlerken Merhaba aynı yapılandırma görünüm tam olarak hello aynı.  Paketinizi güncelleştirin ve tooproduction çıkışı, bu adımı hello yapılandırma dosyası olduktan sonra bunu toopush gereken her zaman doğru – hello dahil olmak üzere paketinin yeni sürümü.  Merhaba yapılandırma dosyası ve PowerShell şöyledir:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

Yeni-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Yeni bir düğüm yapılandırması bu adımları neden "Merhaba çekme sunucusuna yerleştirilen ISVBoxConfig.isvbox" adlı.  Merhaba düğüm yapılandırması adı "configurationName.nodeName" oluşturulmuştur.

## <a name="step-5-creating-and-maintaining-package-metadata"></a>5. adım: Oluşturma ve paket meta verileri koruma
Merhaba paket depoya yerleştirdiğiniz her paket için açıklayan bir nuspec gerekir.  Bu nuspec derlenmiş ve NuGet sunucunuz depolanır. Bu işlem açıklanan [burada](http://docs.nuget.org/create/creating-and-publishing-a-package).  Bir NuGet sunucusu olarak MyGet.org kullanabilirsiniz.  Bu hizmet satmak, ancak Başlatıcı ücretsizdir SKU'su vardır.  NuGet.org özel paketlerinizi için kendi NuGet sunucusu yükleme hakkında yönergeler bulabilirsiniz.

## <a name="step-6-tying-it-all-together"></a>6. adım: hepsini bir araya getirmeye kadar
Sürüm QA geçirir ve onaylandıktan dağıtımı için hello paket oluşturuldu, her nuspec ve nupkg güncelleştirildi ve toohello NuGet sunucu dağıtılır.  Ayrıca, başlangıç yapılandırması (yukarıdaki adım 4) güncelleştirilmiş tooagree hello yeni sürüm numarasına sahip olmalıdır.  Toohello çekme sunucusuna gönderilen ve derlenmiş gerekir.  Bu noktadan itibaren bu yapılandırma toopull hello güncelleştirmesi bağlıdır ve yüklemeniz toohello VM'ler olduğu.  Bu güncelleştirmelerden her birini basit - yalnızca bir çizgi veya iki PowerShell.  Visual Studio Team Services Hello durumda bazıları bir yapı içinde birbirine zincirlenebilir derleme görevleri içinde kapsüllenir.  Bu [makale](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) daha fazla ayrıntı sağlar.  Bu [GitHub deposuna](https://github.com/Microsoft/vso-agent-tasks) ayrıntıları hello çeşitli kullanılabilir yapı görevleri.

## <a name="notes"></a>Notlar
Bu kullanım örnek hello Azure galerisinde genel bir Windows Server 2012 R2 görüntüsünden bir VM'den başlar.  Depolanmış bir görüntüden başlatın ve hello DSC yapılandırması ile buradan ince ayar.  Ancak, bir görüntüye baked yapılandırmasını değiştirme DSC kullanarak hello yapılandırmasını dinamik olarak güncelleştirilmesi daha çok daha zordur.

Bu teknik ile Vm'leriniz toouse ARM şablonunu ve hello VM uzantısı toouse yok.  Ve Vm'lerinizi Azure toobe CD Yönetimi altında üzerinde toobe yok.  Tüm bu Chocolatey olması yüklü olduğundan ve hello çekme sunucunun olduğu bilmesi için hello LCM'yi hello VM üzerinde yapılandırılmış gerekli olmasıdır.  

Bir paketi üretim bir VM'de güncelleştirdiğinizde hello güncelleştirme yüklenirken doğal olarak, tootake döndürme dışında bu VM ihtiyacınız var.  Bunu nasıl yapacağınız yaygın olarak değişir.  Örneğin, bir Azure yük dengeleyici arkasında bir VM ile özel araştırma ekleyebilirsiniz.  Merhaba VM güncelleştirilirken bir 400 dönüş hello araştırma uç noktası vardır.  Hello ince ayar gerekli toocause bu değişikliği geri tooreturning bir 200 hello Güncelleştirme tamamlandıktan sonra ince ayar tooswitch hello olarak yapılandırmanızı içinde olabilir.

Bu kullanım örneğin tam kaynak konusu [bu Visual Studio projesi](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) github'da.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Otomasyonu DSC genel bakış](automation-dsc-overview.md)
* [Azure Otomasyonu DSC cmdlet'leri](https://msdn.microsoft.com/library/mt244122.aspx)
* [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)

