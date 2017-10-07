---
title: aaaNode.js Getting Started Guide | Microsoft Docs
description: "Nasıl toocreate basit bir Node.js web uygulaması ve tooan Azure bulut hizmeti dağıtmak öğrenin."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma

Bu öğreticide gösterilmiştir nasıl toocreate basit bir Node.js uygulama bir Azure bulut hizmeti çalışıyor. Bulut, azure'daki ölçeklenebilir bulut uygulamalarının yapı taşları hello hizmetleridir. Merhaba ayırma ve bağımsız yönetimi ile uygulamanızın ön uç ve arka uç bileşenlerinin genişleme sağlarlar.  Cloud Services her bir rolü güvenilir bir şekilde barındırmaya yönelik sağlam bir özel sanal makine sağlar.

Bulut Hizmetleri ve bunların nasıl tooAzure Web siteleri ve sanal makineleri karşılaştırın hakkında daha fazla bilgi için bkz: [Azure Websites, Cloud Services ve sanal makineleri karşılaştırma].

> [!TIP]
> Toobuild basit bir Web sitesi mi arıyorsunuz? Senaryonuz yalnızca basit bir web sitesi ön ucu içeriyorsa, [basit bir web uygulaması kullanmayı] düşünün. Web uygulamanız büyüdükçe ve gereksinimleriniz değiştikçe kolayca bulut hizmeti tooa yükseltebilirsiniz.

Bu öğreticiyi izleyerek bir web rolünün içinde barındırılan basit bir web uygulaması oluşturacaksınız. Merhaba işlem öykünücüsü tootest uygulamanızı yerel olarak kullanın ardından PowerShell komut satırı araçlarını kullanarak dağıtın.

Merhaba, basit bir "hello world" uygulaması uygulamadır:

![Merhaba Hello World web sayfasını gösteren bir web tarayıcısı][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Ön koşullar
> [!NOTE]
> Bu öğretici Windows gerektiren Azure PowerShell’i kullanır.

* [Azure PowerShell]'i yükleyip yapılandırın.
* Merhaba yükleyip [.NET 2.7 için Azure SDK]. Kurulum Hello yüklemek, seçin:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Azure Cloud Service projesi oluşturma
Aşağıdaki görevler toocreate temel Node.js iskelesiyle birlikte yeni bir Azure bulut hizmeti projesi hello gerçekleştirin:

1. Çalıştırma **Windows PowerShell** yönetici olarak; hello **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**.
2. [PowerShell'i bağlayın] tooyour abonelik.
3. PowerShell cmdlet toocreate toocreate hello proje aşağıdaki hello girin:

        New-AzureServiceProject helloworld

    ![Merhaba hello New-AzureService helloworld komutunun sonucu][hello result of hello New-AzureService helloworld command]

    Merhaba **New-AzureServiceProject** cmdlet'i bir Node.js uygulaması tooa bulut hizmeti yayımlamak için basit bir yapı oluşturur. Yayımlama tooAzure için gerekli yapılandırma dosyalarını içerir. Merhaba cmdlet'i ayrıca hello hizmeti için çalışma dizini toohello dizini değiştirir.

    Merhaba cmdlet aşağıdaki dosyaları hello oluşturur:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** ve **ServiceDefinition.csdef**: Uygulamanızı yayımlamak için gereken Azure’a özel dosyalar. Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].
   * **deploymentSettings.json**: hello Azure PowerShell dağıtım cmdlet'leri tarafından kullanılan yerel ayarları depolar.
4. Komut tooadd yeni bir web rolü aşağıdaki hello girin:

       Add-AzureNodeWebRole

   ![Merhaba hello Add-AzureNodeWebRole komutunun çıktısı][hello output of hello Add-AzureNodeWebRole command]

   Merhaba **Add-AzureNodeWebRole** cmdlet'i basit bir Node.js uygulaması oluşturur. Ayrıca hello değiştirdiği **.csfg** ve **.csdef** tooadd hello yeni rol için yapılandırma girdileri dosyaları.

   > [!NOTE]
   > Bir rol adı belirtmezseniz varsayılan ad kullanılır. Bir ad hello birinci cmdlet parametresi olarak sağlayabilirsiniz:`Add-AzureNodeWebRole MyRole`

Merhaba Node.js uygulaması hello dosyasında tanımlanan **server.js**hello web rolü için hello dizininde bulunan (**WebRole1** varsayılan olarak). Merhaba kod aşağıdadır:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Bu kod temelde "Hello World" Merhaba aynı örnek üzerinde hello hello olan [nodejs.org] Web sitesi, hello bulut ortamı tarafından atanan hello bağlantı noktası numarasını kullanır.

## <a name="deploy-hello-application-tooazure"></a>Merhaba uygulama tooAzure dağıtma

> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. [MSDN abone avantajınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ya da [ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Hello Azure indirme ayarları yayımlama
toodeploy, uygulama tooAzure önce ayarları Azure aboneliğinizin yayımlama hello indirmeniz gerekir.

1. Merhaba aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:

       Get-AzurePublishSettingsFile

   Bu, tarayıcınızı kullanır toonavigate toohello yayımlama ayarları indirme sayfası. Bir Microsoft Account istendiğinde toolog olabilir. Bu durumda, Azure aboneliğinizle ilişkili hello hesabı kullanın.

   Kolayca erişebilirsiniz indirilen hello profil tooa dosya konumuna kaydedin.
2. Cmdlet'i tooimport hello profil indirdiğiniz yayımlama çalıştırın:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Merhaba aldıktan sonra yayımlama ayarları, birisi verebilecek bilgiler içerdiğinden indirdiğiniz .publishSettings dosyasını hello silme göz önünde bulundurun tooaccess hesabınızı.

### <a name="publish-hello-application"></a>Merhaba uygulama yayımlama
toopublish, hello aşağıdaki komutları çalıştırın:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** hello dağıtım hello adını belirtir. Bu benzersiz bir ad olmalıdır, aksi takdirde hello yayımlama işlemi başarısız olur. Merhaba **Get-Date** komutu tacks hello adın benzersiz olması bir tarih dizesi.
* **-Location** hello uygulama içinde barındırılan hello datacenter belirtir. toosee kullanılabilir veri merkezlerinin, kullanım hello listesini **Get-AzureLocation** cmdlet'i.
* **-Launch** bir tarayıcı penceresi açar ve dağıtım tamamlandıktan sonra barındırılan toohello hizmet gider.

Yayımlama başarılı olduktan sonra yanıt benzer toohello aşağıdaki görürsünüz:

![Merhaba hello Publish-AzureService komutunun çıktısı][hello output of hello Publish-AzureService command]

> [!NOTE]
> Bu hello uygulama toodeploy için birkaç dakika sürer ve ilk kez yayımlandığında kullanılabilir hale gelir.

Merhaba dağıtım tamamlandıktan sonra bir tarayıcı penceresi açın ve toohello bulut hizmetine gidin.

![Merhaba hello world sayfasını gösteren bir tarayıcı penceresi; Merhaba URL hello sayfanın Azure'da barındırıldığını gösterir.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Uygulamanız artık Azure üzerinde çalışıyor.

Merhaba **Publish-AzureServiceProject** cmdlet'i hello aşağıdaki adımları gerçekleştirir:

1. Bir paket toodeploy oluşturur. Hello paket, uygulama klasöründeki tüm hello dosyaları içerir.
2. Mevcut değilse yeni bir **depolama hesabı** oluşturur. Hello Azure depolama hesabı, dağıtım sırasında kullanılan toostore hello uygulama paketi değil. Dağıtımını gerçekleştirdikten sonra hello depolama hesabı güvenle silebilirsiniz.
3. Henüz mevcut değilse yeni bir **bulut hizmeti** oluşturur. A **bulut hizmeti** , uygulamanızın barındırıldığını dağıtılan tooAzure olduğunda hello kapsayıcıdır. Daha fazla bilgi için bkz. [Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış].
4. Merhaba dağıtım paketi tooAzure yayımlar.

## <a name="stopping-and-deleting-your-application"></a>Uygulamanızı durdurma ve silme
Uygulamanızı dağıttıktan sonra toodisable isteyebilirsiniz, ek maliyetlerden kaçınmak için. Azure web rolü örneklerini harcanan sunucu saati başına faturalandırır. Uygulamanızı dağıtıldığında Hello örnekler çalışmadığında ve hello durdurulmuş durumda olsa bile sunucu saati harcanır.

1. Merhaba Windows PowerShell penceresinde hello hizmet dağıtımı cmdlet aşağıdaki hello ile Merhaba önceki bölümde oluşturduğunuz durdurun:

       Stop-AzureService

   Merhaba hizmetin durdurulması birkaç dakika sürebilir. Merhaba hizmet durdurulduğunda bunu belirten bir ileti alırsınız.

   ![Hello hello Stop-AzureService komutunun durumu][hello status of hello Stop-AzureService command]
2. toodelete hello hizmeti, cmdlet aşağıdaki çağrı hello:

       Remove-AzureService

   İstendiğinde, girin **Y** toodelete hello hizmet.

   Merhaba hizmetin silinmesi birkaç dakika sürebilir. Merhaba hizmet silindikten sonra hello hizmeti silinmiş olduğunu belirten bir ileti alırsınız.

   ![Merhaba Remove-AzureService komutunun Hello durumu][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Merhaba hizmetin silinmesi hello hizmet ilk kez yayımlandığında oluşturulan hello depolama hesabı silmez ve kullanılan depolama alanı için fatura toobe devam eder. Hiçbir şey hello depo kullanıyorsa toodelete isteyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi].

<!-- URL List -->

[Azure Websites, Cloud Services ve sanal makineleri karşılaştırma]: ../app-service-web/choose-web-site-cloud-service-vm.md
[basit bir web uygulaması kullanmayı]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[.NET 2.7 için Azure SDK]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[PowerShell'i bağlayın]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Azure için Barındırılan Hizmet Oluşturmaya Genel Bakış]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js Geliştirici Merkezi]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
