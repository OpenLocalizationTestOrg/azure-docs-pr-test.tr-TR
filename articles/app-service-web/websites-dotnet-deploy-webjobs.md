---
title: "aaaDeploy Visual Studio'yu kullanarak Web işleri"
description: "Bilgi nasıl toodeploy Azure Web işleri tooAzure App Service Web Apps Visual Studio kullanarak."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Visual Studio kullanarak WebJobs dağıtma
## <a name="overview"></a>Genel Bakış
Bu konuda, nasıl toouse Visual Studio toodeploy bir konsol uygulaması proje tooa web uygulamasında açıklanmaktadır [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) olarak bir [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226). Nasıl kullanarak Web işleri toodeploy hello hakkında bilgi için [Azure Portal](https://portal.azure.com), bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).

Visual Studio Web işleri etkin konsol uygulama projesi dağıtırken, iki görevleri gerçekleştirir:

* Kopya çalışma zamanı toohello uygun hello web uygulaması klasördeki dosyaları (*App_Data/işleri/sürekli* sürekli Webjob'lar için *App_Data/işleri/tetiklenen* zamanlanmış ve isteğe bağlı Webjob için).
* Ayarlayan [Azure zamanlayıcı işlerinin](#scheduler) belirli zamanlarda zamanlanmış toorun olan Web işleri için. (Bu sürekli Webjob'lar için gerekli değildir.)

WebJobs kullanan bir proje öğeleri eklenen tooit aşağıdaki hello sahiptir:

* Merhaba [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi.
* A [webjob yayımlama settings.json](#publishsettings) dağıtım ve Zamanlayıcı ayarlarını içeren dosya. 

![Bir Web işi ne tooa konsol uygulaması tooenable dağıtım eklenir gösteren diyagram](./media/websites-dotnet-deploy-webjobs/convert.png)

Konsol uygulama projesi varolan bu öğeleri tooan ekleyin veya bir şablon toocreate yeni bir Web işleri etkin konsol uygulama projesi kullanın. 

Bir proje bir Web işi kendisi tarafından dağıtabilir veya hello web projesi dağıtma olduğunda otomatik olarak dağıtan şekilde tooa web projesi bağlayın. toolink projeleri, Visual Studio içerir hello WebJobs etkin projesinde hello adını bir [webjobs list.json](#webjobslist) hello web projesi dosyasında.

![Web işi projesinin tooweb projesi bağlanıyor gösteren diyagram](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Ön koşullar
.NET için Azure SDK'sı hello yüklediğinizde, Web işleri dağıtım özelliklerini Visual Studio'da kullanılabilir:

* [.NET (Visual Studio) için Azure SDK](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Mevcut bir konsol uygulama projesi için Web işleri dağıtımı etkinleştir
İki seçeneğiniz vardır:

* [Bir web projesi ile otomatik dağıtımı etkinleştirmek](#convertlink).
  
    Bir web projesi dağıttığınızda, otomatik olarak bir Web işi olarak dağıtan mevcut bir konsol uygulama projesini yapılandırın. Merhaba, Webjob'da toorun istediğinizde bu seçeneği kullanın hello çalıştırmak aynı web uygulaması ile ilgili web uygulaması.
* [Bir web projesi dağıtımıdır etkinleştirmek](#convertnolink).
  
    Mevcut bir konsol uygulama projesi toodeploy bir Web işi kendisi tarafından hiçbir bağlantı tooa web projesi ile yapılandırın. Bir web uygulamasında bir Webjob'un toorun kendisi tarafından hello web uygulamasında çalışan hiçbir web uygulaması ile istediğinizde bu seçeneği kullanın. Bu toodo isteyebilirsiniz, web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı toobe mümkün tooscale sipariş.

### <a id="convertlink"></a>Bir web projesi ile otomatik WebJobs dağıtımı etkinleştir
1. Sağ hello web projesinde **Çözüm Gezgini**ve ardından **Ekle** > **Azure Web işi olarak mevcut proje**.
   
    ![Azure Web işi olarak mevcut proje](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Merhaba [Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.
2. Merhaba, **proje adı** aşağı açılan listesinden, select hello konsol uygulama projesi tooadd bir Web işi olarak.
   
    ![Azure Web işine Ekle iletişim kutusunda proje seçme](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Tam hello [Azure Web işine Ekle](#configure) iletişim ve ardından **Tamam**. 

### <a id="convertnolink"></a>Bir web projesi olmadan Web işleri dağıtımı etkinleştir
1. Sağ hello konsol uygulama projesi **Çözüm Gezgini**ve ardından **Azure Web işi olarak Yayımla...** . 
   
    ![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Merhaba [Azure Web işine Ekle](#configure) hello seçili hello proje ile iletişim kutusu görünür **proje adı** kutusu.
2. Tam hello [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.
   
   Merhaba **Web'i Yayımla** Sihirbazı görünür.  Toopublish hemen istemiyorsanız hello sihirbazı kapatın. girmiş olduğunuz hello ayarları kaydedilir için çok istediğinizde,[hello projesini dağıtma](#deploy).

## <a id="create"></a>Yeni bir Web işleri etkin projesi oluşturma
Yeni bir Web işleri etkin proje toocreate, hello konsol uygulaması proje şablonu ve etkinleştir WebJobs dağıtım kullanabilirsiniz açıklandığı gibi [hello önceki bölümde](#convert). Alternatif olarak, hello WebJobs yeni proje şablonunu kullanarak şunları yapabilirsiniz:

* [Bağımsız bir Web işi için Hello WebJobs yeni proje şablonu kullanın](#createnolink)
  
    Proje oluşturma ve toodeploy kendi başına hiçbir bağlantı tooa web projesi ile bir Web işi olarak yapılandırın. Bir web uygulamasında bir Webjob'un toorun kendisi tarafından hello web uygulamasında çalışan hiçbir web uygulaması ile istediğinizde bu seçeneği kullanın. Bu toodo isteyebilirsiniz, web uygulaması kaynaklarınıza bağımsız olarak, Web işi kaynaklarınızı toobe mümkün tooscale sipariş.
* [Bir Web işi bağlantılı tooa web projesi için Hello WebJobs yeni proje şablonu kullanın](#createlink)
  
    Bir web projesi yokken aynı çözüm dağıtılan hello bir Web işi olarak otomatik olarak yapılandırılan toodeploy bir proje oluşturun. Merhaba, Webjob'da toorun istediğinizde bu seçeneği kullanın hello çalıştırmak aynı web uygulaması ile ilgili web uygulaması.

> [!NOTE]
> Merhaba WebJobs yeni proje şablonu otomatik olarak NuGet paketlerini yükler ve kod içerir *Program.cs* hello için [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Toouse hello Web işleri SDK'si istemiyorsanız, kaldırmak veya hello değiştirme `host.RunAndBlock` deyiminde *Program.cs*.
> 
> 

### <a id="createnolink"></a>Bağımsız bir Web işi için Hello WebJobs yeni proje şablonu kullanın
1. Tıklatın **dosya** > **yeni proje**ve ardından hello **yeni proje** iletişim kutusunda **bulut**  >   **Azure Web işi (.NET Framework)**.
   
    ![Web işi şablon gösteren yeni proje iletişim kutusu](./media/websites-dotnet-deploy-webjobs/np.png)
2. Daha önce gösterilen hello yönergeleri izleyerek çok[konsol uygulama projesi bağımsız bir Web işleri proje hello olun](#convertnolink).

### <a id="createlink"></a>Bir Web işi bağlantılı tooa web projesi için Hello WebJobs yeni proje şablonu kullanın
1. Sağ hello web projesinde **Çözüm Gezgini**ve ardından **Ekle** > **yeni Azure Web işi projesi**.
   
    ![Yeni Azure Web işi projesinin menü girişi](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Merhaba [Azure Web işine Ekle](#configure) iletişim kutusu görüntülenir.
2. Tam hello [Azure Web işine Ekle](#configure) iletişim kutusunu ve ardından **Tamam**.

## <a id="configure"></a>Hello Azure Web işine Ekle iletişim kutusu
Merhaba **Azure Web işine Ekle** iletişim hello Web işi adı girin ve modu ayarı, Web işi için çalıştırmanıza olanak sağlar. 

![Azure Web işi iletişim ekleyin](./media/websites-dotnet-deploy-webjobs/aaw2.png)

Bu iletişim kutusunu Hello alanları karşılık toofields hello üzerinde **yeni iş** hello Azure Portal ile görüşün. Daha fazla bilgi için bkz: [Web işleri ile Çalıştır arka plan görevleri](web-sites-create-web-jobs.md).

> [!NOTE]
> * Komut satırı dağıtımı hakkında daha fazla bilgi için bkz: [etkinleştirme komut satırı veya Azure Web işleri sürekli teslim](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Bir Web işi dağıtırsanız ve toochange hello türüne WebJob dağıtın ve istediğiniz karar toodelete hello Web işleri yayımlama settings.json dosyası gerekir. Bu, Visual Studio Web işi hello türünü değiştirebilmeniz için seçenekleri yeniden yayımlama hello Göster hale getirir.
> * Bir Web işi dağıtmak ve daha sonra değiştirirseniz çalıştırma modundan sürekli toonon sürekli hello veya, yeniden dağıtırken Visual Studio Azure içinde yeni bir Web işi tersi yönde oluşturur. Diğer zamanlama ayarlarını değiştirmek, ancak bırakın çalıştırma modu aynı hello veya zamanlanmış ve isteğe bağlı arasında geçiş yapma, Visual Studio güncelleştirmeleri mevcut iş hello yerine yeni bir tane oluşturun.
> 
> 

## <a id="publishsettings"></a>Web işi yayımlama settings.json
Bir konsol uygulaması Web işleri dağıtımı için yapılandırdığınızda, Visual Studio hello yükler [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paketi ve planlama bilgilerini de depolar bir *webjob yayımlama settings.json*  hello proje dosyasında *özellikleri* hello WebJobs projesinin klasör. Bu dosyayı bir örneği burada verilmiştir:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz. Merhaba dosya şeması depolandı [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) ve orada görüntülenebilir.  

## <a id="webjobslist"></a>Web işleri list.json
WebJobs kullanan proje tooa web projesi bağladığınızda, Visual Studio hello WebJobs projesinde hello adını depolar bir *webjobs list.json* hello web projesinin dosyasında *özellikleri* klasör. Merhaba listesi hello aşağıdaki örnekte gösterildiği gibi birden çok Web işleri projeleri içerebilir:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

Visual Studio IntelliSense sağlar ve bu dosyayı doğrudan düzenleyebilirsiniz. Merhaba dosya şeması depolandı [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) ve orada görüntülenebilir.

## <a id="deploy"></a>Web işleri projesini dağıtma
Tooa web projesi bağlantılı Web işleri proje hello web projesi ile otomatik olarak dağıtır. Web projesi dağıtımı hakkında daha fazla bilgi için bkz: [nasıl toodeploy tooWeb uygulamaları](web-sites-deploy.md).

toodeploy WebJobs proje kendisi tarafından sağ hello projesinde **Çözüm Gezgini** tıklatıp **Azure Web işi olarak Yayımla...** . 

![Azure Web işi Yayımla](./media/websites-dotnet-deploy-webjobs/paw.png)

Bağımsız bir Web işi için aynı hello **Web'i Yayımla** web projeleri görünür, ancak daha az ayarları kullanılabilir toochange ile kullanılan Sihirbazı.

## <a id="nextsteps"></a>Sonraki Adımlar
Bu makalede açıklanan nasıl Visual Studio'yu kullanarak Web işleri toodeploy. Azure Web işleri toodeploy nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri - önerilen kaynaklar - dağıtım](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

