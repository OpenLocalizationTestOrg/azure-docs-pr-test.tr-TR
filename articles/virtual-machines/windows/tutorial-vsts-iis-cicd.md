---
title: "aaaCreate CI/CD ardışık düzen Team Services ile azure'da | Microsoft Docs"
description: "Nasıl toocreate bir Visual Studio Team Services kanal sürekli tümleştirme ve bir web uygulaması tooIIS Windows VM üzerinde dağıtır teslimi için bilgi edinin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Visual Studio Team Services ve IIS ile sürekli tümleştirme işlem hattı oluşturma
tooautomate hello derleme, test ve dağıtım aşamaları uygulama geliştirme, sürekli tümleştirme ve dağıtım (CI/CD) ardışık düzen kullanabilirsiniz. Bu öğreticide, Visual Studio Team Services ve Windows sanal makine (VM), IIS çalıştıran Azure kullanarak bir CI/CD işlem hattı oluşturun. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bir ASP.NET web uygulaması tooa Team Services projesini Yayımla
> * Kod tamamlama tarafından tetiklenen bir yapı tanımı oluşturun
> * IIS yükle ve azure'da bir sanal makinede Yapılandır
> * Team Services içinde Hello IIS örnek tooa dağıtım grubu Ekle
> * Bir yayın tanımı toopublish yeni web Oluştur paketleri tooIIS dağıtma
> * Test hello CI/CD ardışık düzen

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma `Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Team Services içinde projesi oluşturma
Şirket içi kodu yönetim çözümünü korumadan kolay işbirliği ve geliştirme için Visual Studio Team Services sağlar. Team Services kodu bulut test, yapı ve application ınsights sağlar. Sürüm denetim deposunu ve kod geliştirme en uygun IDE seçebilirsiniz. Bu öğretici için ücretsiz hesap toocreate temel bir ASP.NET web uygulama ve CI/CD ardışık düzen kullanabilirsiniz. Bir Team Services hesabı zaten yoksa [oluşturmak](http://go.microsoft.com/fwlink/?LinkId=307137).

toomanage hello kod kaydetme işlemi, tanımları, derleme ve tanımları sürüm, Team Services içinde aşağıdaki gibi bir proje oluşturun:

1. Team Services panonuz bir web tarayıcısında açın ve seçin **yeni proje**.
2. Girin *mywebapp şeklindedir* hello için **proje adı**. Tüm diğer varsayılan değerleri toouse bırakın *Git* sürüm denetimi ve *Çevik* iş öğesi işlemi.
3. Çok olarak Hello seçeneği**paylaşmak** *ekip üyelerinin*seçeneğini belirleyip **oluşturma**.
5. Projeniz oluşturulduktan sonra hello çok seçeneği**bir benioku veya gitignore başlatma**, ardından **başlatma**.
6. Yeni projeniz içinde seçin **panolar** hello üstte seçip **Visual Studio'da Aç**.


## <a name="create-aspnet-web-application"></a>ASP.NET web uygulaması oluşturma
Hello önceki adımda, bir proje Team Services ile oluşturulmuş. Merhaba son adım, yeni projeniz Visual Studio'da açılır. Merhaba içinde kod tamamlama yönetmek **Takım Gezgini** penceresi. Yeni projeniz yerel bir kopyasını oluşturun, sonra bir ASP.NET web uygulaması gibi bir şablondan oluşturun:

1. Seçin **kopya** toocreate Team Services projenizin yerel git deposu.
    
    ![Team Services projeden depoyu kopyalama](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. Altında **çözümleri**seçin **yeni**.

    ![Web uygulaması çözümü oluşturun](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Seçin **Web** şablonları ve ardından hello **ASP.NET Web uygulaması** şablonu.
    1. Gibi uygulamanız için bir ad girin *mywebapp şeklindedir*ve hello kutusunun işaretini kaldırın **çözüm için dizin oluştur**.
    2. Merhaba seçeneği kullanılabilir durumdaysa, çok hello kutunun işaretini**Application Insights Ekle tooproject**. Application Insights web uygulamanızı Azure Application Insights ile tooauthorize gerektirir. tookeep bu işlem Bu öğreticide, basit atlayın.
    3. **Tamam**’ı seçin.
4. Seçin **MVC** hello şablonu listesinden.
    1. Seçin **kimlik doğrulamayı Değiştir**, seçin **doğrulaması yok**seçeneğini belirleyip **Tamam**.
    2. Seçin **Tamam** toocreate çözümünüzü.
5. Merhaba, **Takım Gezgini** penceresinde, seçin **değişiklikleri**.

    ![Yerel değişiklikler tooTeam Hizmetleri git deposuna uygulayın](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Bir ileti gibi Hello yürütme metin kutusuna girin *ilk yürütme*. Seçin **Commit tüm ve eşitleme** hello açılan menüsünden.


## <a name="create-build-definition"></a>Yapı tanımı oluşturun
Team Services içinde uygulamanızı nasıl yerleşik bir yapı tanımı toooutline kullanın. Bu öğreticide, bizim kaynak kodu hello çözüm oluşturur, ardından web oluşturur alır toorun hello web uygulaması bir IIS sunucusunda kullanabilirsiniz paketini dağıtmak bir temel tanımı oluşturun.

1. Team Services projenizde seçin **yapı & yayın** hello üstte seçip **derlemeler**.
3. Seçin **+ yeni tanımı**.
4. Merhaba seçin **ASP.NET (Önizleme)** şablonu ve select **Uygula**.
5. Tüm hello varsayılan görev değerleri bırakın. Altında **alma kaynakları**, o hello olun *mywebapp şeklindedir* depo ve *ana* şube seçilir.

    ![Yapı tanımı Team Services projesi oluşturun](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Merhaba üzerinde **Tetikleyicileri** sekmesinde, hello kaydırıcıyı **Bu tetikleyici etkinleştirmek** çok*etkin*.
7. Merhaba derleme tanımı ve sıra seçerek yeni bir yapı Kaydet **sıraya & Kaydet** , ardından **sıraya & Kaydet** yeniden. Merhaba Varsayılanları bırakabilir ve seçin **sıra**.

Merhaba derleme üzerinde barındırılan bir aracısı, zamanlanmış olarak izleme toobuild sonra başlar. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

![Team Services projesinin başarılı derleme](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Sanal makine oluşturma
tooprovide platform toorun ASP.NET web uygulamanızı IIS çalışan bir Windows sanal makine gerekir. Team Services kullanan bir aracı toointeract hello IIS örneğiyle kod tamamlama ve derlemeleri tetiklenen.

Kullanarak bir Windows Server 2016 VM oluşturma [bu komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Merhaba betik toorun birkaç dakika sürer ve hello VM oluşturun. Merhaba VM oluşturulduktan sonra bağlantı noktası 80 web trafiği için açık [Ekle AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) gibi:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM elde hello ortak IP adresiyle [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) gibi:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Uzak Masaüstü oturumu tooyour VM oluşturun:

```cmd
mstsc /v:<publicIpAddress>
```

Hello VM, açık bir **yönetici PowerShell** komut istemi. IIS ve gerekli .NET özellikleri gibi yükleyin:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Dağıtım grubu oluşturma
Merhaba web çıkışı toopush paket toohello IIS sunucusu dağıtabilir, Team Services içinde bir dağıtım grubu tanımlayın. Bu grup, hizmetleri ve derlemeleri tamamlanan kodu tooTeam commit olarak hangi sunucuların yeni yapılar hello hedefinin olduğunu toospecify sağlar.

1. Team Services içinde seçin **yapı & yayın** ve ardından **dağıtım grupları**.
2. Seçin **eklemek dağıtım grubu**.
3. Merhaba grubu için bir ad girin *myIIS*seçeneğini belirleyip **oluşturma**.
4. Merhaba, **kaydetmek makineler** bölümünde, sağlamak *Windows* seçilir ve ardından çok olarak hello kutuyu**kişisel erişim belirteci hello komut dosyasındaki kimlik doğrulaması için kullanmak**.
5. Seçin **kopyalama komut dosyası tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>IIS VM toohello dağıtım grubu Ekle
Oluşturulan hello dağıtım grubuyla her IIS örneği toohello grubuna ekleyin. Team Services yükler ve yeni web aldığı VM dağıtmak hello üzerinde bir aracı yapılandıran bir komut dosyası oluşturduğu paketleri sonra tooIIS uygular.

1. Merhaba edilene **yönetici PowerShell** , VM oturum yapıştırın ve Team Services kopyalanan hello komut dosyasını çalıştırın.
2. Merhaba aracısına yönelik, istendiğinde tooconfigure etiketleri seçtiğinizde *Y* ve girin *web*.
3. Merhaba kullanıcı hesabı için istendiğinde basın *dönmek* tooaccept hello Varsayılanları.
4. Merhaba betik toofinish bir iletiyle bekleyin *hizmet vstsagent.account.computername başarıyla başlatıldı*.
5. Merhaba, **dağıtım grupları** hello sayfasının **yapı & yayın** menüsü, açık hello *myIIS* dağıtım grubu. Merhaba üzerinde **makineler** sekmesinde, VM'yi listelenmiş olduğunu doğrulayın.

    ![VM tooTeam Hizmetleri dağıtım grubuna başarıyla eklendi](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Yayın tanımı oluşturun
toopublish derlemeleriniz, Team Services içinde bir yayın tanımı oluşturun. Bu tanım, uygulamanızın başarılı bir yapı tarafından otomatik olarak başlatılır. Merhaba dağıtım grubu toopush, web dağıtımı için paketi seçin ve hello uygun IIS ayarlarını tanımlayın.

1. Seçin **yapı & yayın**seçeneğini belirleyip **derlemeler**. Bir önceki adımda oluşturduğunuz hello derleme tanımı seçin.
2. Altında **yakın zamanda tamamlandı**hello en son yapı seçin, ardından seçin **sürüm**.
3. Seçin **Evet** toocreate yayın tanımı.
4. Merhaba seçin **boş** şablonu, ardından **sonraki**.
5. Merhaba proje ve kaynak yapı tanımı, projenizi ile doldurulur doğrulayın.
6. Select hello **sürekli dağıtım** onay kutusunu işaretleyin ve ardından **oluşturma**.
7. Merhaba açılan kutudan sonraki çok seçin**+ görev ekleme** ve *bir dağıtım grubu aşaması eklemek*.
    
    ![Team Services içinde görev toorelease tanımı Ekle](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Seçin **Ekle** sonraki çok**IIS Web uygulama Deploy(Preview)**seçeneğini belirleyip **Kapat**.
9. Select hello **dağıtım grubu üzerinde çalışan** üst görev.
    1. İçin **dağıtım grubu**seçin hello dağıtım grubunu daha önce olduğu gibi oluşturulan *myIIS*.
    2. Merhaba, **makine etiketleri** kutusunda **Ekle** ve hello seçin *web* etiketi.
    
    ![IIS için yayın tanımı dağıtım grubu görevi](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Select hello **Dağıt: IIS Web uygulamasını dağıtmak** görev tooconfigure IIS örneği aşağıdaki gibi ayarları:
    1. İçin **Web sitesi adı**, girin *varsayılan Web sitesi*.
    2. Tüm hello diğer varsayılan ayarları bırakın.
12. Seçin **kaydetmek**seçeneğini belirleyip **Tamam** iki kez.


## <a name="create-a-release-and-publish"></a>Sürüm oluşturma ve yayımlama
Şimdi web gönderebilir paket yeni bir sürüm olarak dağıtın. Bu adım hello dağıtım grubunun parçası olduğundan, hello web iter her örneği hello Aracısı ile iletişim kurar paket dağıtın ve ardından IIS toorun güncelleştirilmiş Merhaba web uygulaması yapılandırır.

1. Yayın tanımınızı seçin **+ yayın**, ardından **oluşturma yayın**.
2. İle birlikte Hello son yapı hello aşağı açılan listesinde seçili olduğunu doğrulayın **dağıtım otomatik: sürüm oluşturulduktan sonra**. **Oluştur**’u seçin.
3. Küçük bir başlık yayın tanımınızı hello üstte gibi görünen *yayın 'Sürüm 1' oluşturulan*. Select hello yayın bağlantısı.
4. Açık hello **günlükleri** sekmesinde toowatch hello yayın devam ediyor.
    
    ![Paket gönderme dağıtımı ve başarılı Team Services sürüm](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Merhaba yayın tamamlandıktan sonra bir web tarayıcısı açın ve VM hello ortak işlenen madde adresini girin. ASP.NET web uygulamanız çalışıyor.

    ![IIS VM üzerinde çalışan ASP.NET web uygulaması](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Test hello tüm CI/CD ardışık düzen
IIS üzerinde çalışan web uygulamanız ile Merhaba tüm CI/CD ardışık şimdi deneyin. Visual Studio ve güncelleştirilmiş web sürümü tetikleyen bir yapı kodunuzu tetiklenir yürütme değişikliği yaptıktan sonra paketi tooIIS dağıtın:

1. Visual Studio'da hello açın **Çözüm Gezgini** penceresi.
2. Tooand açık gidin *mywebapp şeklindedir | Görünümleri | Giriş | Index.cshtml*
3. Satır 6 tooread düzenleyin:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Merhaba dosyasını kaydedin.
5. Açık hello **Takım Gezgini** penceresinde, select hello *mywebapp şeklindedir* proje sonra seçin **değişiklikleri**.
6. Bir kaydetme iletisi gibi girin *sınama CI/CD ardışık düzen*, ardından seçin **tamamlama tüm ve eşitleme** hello açılan menüsünden.
7. Team Services çalışma alanında, yeni bir yapı hello kod tamamlama tetiklenir. 
    - Seçin **yapı & yayın**seçeneğini belirleyip **derlemeler**. 
    - Yapı tanımı seçin ve ardından hello **sıraya alınan & çalışan** yapı toowatch hello olarak yapı ilerler.
9. Merhaba derleme başarılı olduktan sonra yeni bir sürüm tetiklenir.
    - Seçin **yapı & yayın**, ardından **sürümleri** toosee hello web dağıtım paketi tooyour IIS VM gönderilir. 
    - Select hello **yenileme** simgesi tooupdate hello durumu. Ne zaman hello *ortamları* sütunda yeşil bir onay işareti görüntülenir, hello yayın tooIIS başarıyla dağıtılan.
11. Değişikliklerinizi toosee uygulanan, IIS Web tarayıcısında yenileyin.

    ![IIS VM'de CI/CD ardışık düzen tarafından çalıştırılan ASP.NET web uygulaması](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir ASP.NET web uygulamasını Team Services içinde oluşturulan ve yapılandırılan derleme ve sürüm tanımlarını toodeploy yeni web paketleri tooIIS her kod tamamlama üzerinde dağıtın. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir ASP.NET web uygulaması tooa Team Services projesini Yayımla
> * Kod tamamlama tarafından tetiklenen bir yapı tanımı oluşturun
> * IIS yükle ve azure'da bir sanal makinede Yapılandır
> * Team Services içinde Hello IIS örnek tooa dağıtım grubu Ekle
> * Bir yayın tanımı toopublish yeni web Oluştur paketleri tooIIS dağıtma
> * Test hello CI/CD ardışık düzen

Toohello sonraki öğretici toolearn nasıl ilerlemek toosecure bir web sunucusu SSL sertifikaları ile.

> [!div class="nextstepaction"]
> [SSL ile güvenli web sunucusu](tutorial-secure-web-server.md)