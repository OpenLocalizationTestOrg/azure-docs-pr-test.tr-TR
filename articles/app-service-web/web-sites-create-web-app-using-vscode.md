---
title: "Visual Studio Code ASP.NET Core web uygulamasında aaaCreate"
description: "Bu öğretici nasıl toocreate ASP.NET Core web uygulamasını Visual Studio Code kullanarak gösterilmektedir."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Visual Studio kodda bir ASP.NET Core web uygulaması oluşturma
## <a name="overview"></a>Genel Bakış
Bu öğreticide, bir ASP.NET Core toocreate nasıl web uygulamasını kullanarak gösterilir [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) ve çok dağıtma[Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Bu makalede tooweb uygulamaları başvuruyor ancak tooAPI uygulamaları ve mobil uygulamalara da uygulanır. 
> 
> 

ASP.NET çekirdeği ASP.NET önemli yeniden tasarlanması olur. ASP.NET Core .NET kullanarak modern bulut tabanlı web uygulamaları oluşturmak için yeni bir açık kaynaklı ve çapraz platform framework kümesidir. Daha fazla bilgi için bkz: [giriş tooASP.NET çekirdek](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Azure App Service web apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Ön koşullar
* Yükleme [VS Code](http://code.visualstudio.com/Docs/setup).
* Git - yüklemek bu konumları birinden yükleyebilirsiniz: [Chocolatey](https://chocolatey.org/packages/git) veya [git scm.com](http://git-scm.com/downloads). Yeni tooGit varsa, seçin [git scm.com](http://git-scm.com/downloads) ve hello seçeneğini çok**kullanım Git hello Windows komut istemi gelen**. Git yükledikten sonra (bir yürütme VS koddan gerçekleştirirken) daha sonra hello öğreticide gerektiği şekilde de tooset hello Git kullanıcı adı ve e-posta ihtiyacınız vardır.  

## <a name="install-aspnet-core"></a>ASP.NET Core yükleyin
ASP.NET çekirdeği modern Bulut ve OS X, Linux ve Windows çalıştıran web uygulamaları oluşturmak için yalın bir .NET yığını olur. Bu tooprovide plan hello gelen ya da dağıtılmış toohello Bulut veya şirket içi uygulamalar için en iyi duruma getirilmiş geliştirme framework oluşturulmadı. Çözümlerinizi oluşturulurken esneklik korumak için en az ek yük, modüler bileşenlerden oluşur.

Bu öğretici sürümleriyle hello son geliştirme ASP.NET Core uygulamaları oluşturmaya başladı tasarlanmış tooget ' dir. yönergeleri izleyerek hello belirli tooWindows ' dir. OS X, Linux ve Windows yükleme yönergeleri için bkz: [ASP.NET Core ile çalışmaya başlama](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Daha ayrıntılı OS X, Linux ve Windows için yükleme yönergeleri için bkz: [yükleme ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Merhaba web uygulaması oluşturma
Bu bölümde, nasıl tooscaffold yeni bir uygulama ASP.NET web uygulaması hello .NET CLI aracını kullanarak gösterir. 

1. Merhaba komut istemi toocreate hello proje klasörünü ve iskele hello uygulama Hello aşağıdaki girin.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![DotNet CLI - ASP.NET Core Oluşturucusu](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore gerekli NuGet paketlerini Merhaba, hello aşağıdaki komutu çalıştırın:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Merhaba web uygulamasını yerel olarak çalıştırma
Merhaba web uygulaması oluşturuldu ve hello uygulama için tüm hello NuGet paketlerini alınan göre hello web uygulamasını yerel olarak çalıştırabilirsiniz.

1. Merhaba uygulamayı çalıştırın (Merhaba `dotnet run` komutu, hello uygulama oluşturacaksınız, eski olduğunda):
    ```terminal
    dotnet run
    ```
2. Bir tarayıcı açın ve URL'yi aşağıdaki toohello gidin.
   
    **http://localhost: 5000**
   
    Merhaba web uygulaması Hello varsayılan sayfasını aşağıdaki gibi görünür.
   
    ![Bir tarayıcıda yerel web uygulaması](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Tarayıcınızı kapatın. Merhaba, **komut penceresi**, basın **Ctrl + C** hello uygulama ve Kapat hello aşağı tooshut **komut penceresi**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Hello Azure portalı bir web uygulaması oluşturma
Hello aşağıdaki adımlar, bir web uygulaması hello Azure Portal oluşturmada size yol gösterecektir.

1. İçinde toohello oturum [Azure Portal](https://portal.azure.com).
2. Tıklatın **yeni** hello adresindeki hello Portal ' sol üst.
3. Tıklatın **Web uygulamaları > Web uygulaması**.
   
    ![Azure yeni web uygulaması](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. İçin bir değer girin **adı**, gibi **SampleWebAppDemo**. Toobe bu adı benzersiz olmalıdır ve tooenter hello adı çalıştığınızda hello portal, zorunlu kılacak unutmayın. Enter farklı bir değer seçerseniz, bu nedenle, değer toosubstitute her oluşumu için ihtiyacınız vardır **SampleWebAppDemo** Bu öğreticide gördüğünüz. 
5. Var olan seçin **App Service planı** veya yeni bir tane oluşturun. Yeni bir plan oluşturursanız, fiyatlandırma katmanı, konum ve diğer seçenekleri hello seçin. Merhaba makale App Service planları hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Yeni Azure web uygulaması dikey](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. **Oluştur**'a tıklayın.
   
    ![Web uygulaması dikey](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Merhaba yeni web uygulaması için Git yayımlamayı etkinleştirme
Git Azure App Service web uygulamanızı toodeploy kullanabileceğiniz bir dağıtılmış sürüm denetim sistemidir. Web uygulamanızda yerel bir Git deposu için yazma hello kod depolayacak ve tooa uzak depoya ileterek kod tooAzure dağıtacaksınız.   

1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com).
2. **Gözat**’a tıklayın.
3. Tıklatın **Web Apps** tooview hello web uygulamaları Azure aboneliğinizle ilişkili listesi.
4. Bu öğreticide oluşturduğunuz hello web uygulaması seçin.
5. Merhaba web uygulaması dikey penceresinde tıklatın **ayarları** > **sürekli dağıtım**. 
   
    ![Azure web uygulaması konağı](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Tıklatın **Kaynak Seç > yerel Git deposu**.
7. **Tamam** düğmesine tıklayın.
   
    ![Azure yerel Git depo](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Daha önce bir web uygulaması veya diğer App Service uygulama yayımlamak için dağıtım kimlik bilgileri ayarlamadıysanız, bunları şimdi kurun:
   
   * Tıklatın **ayarları** > **dağıtım kimlik bilgileri**. Merhaba **dağıtım kimlik bilgilerini ayarla** dikey penceresinde görüntülenir.
   * Bir kullanıcı adı ve parola oluşturun.  Git ayarlarken daha sonra bu parola gerekir.
   * **Kaydet** düğmesine tıklayın.
9. Web uygulamanızın dikey penceresinde tıklayın **ayarlar > Özellikler**. Merhaba, altında gösterilen toois dağıtacaksınız hello uzak Git deposu URL'sini **GIT URL'si**.
10. Kopya hello **GIT URL'si** hello öğreticide daha sonra kullanmak için değer.
    
    ![Azure Git URL'si](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Web uygulaması tooAzure uygulama hizmeti yayımlama
Bu bölümde, yerel bir Git deposu oluşturursunuz ve bu depo tooAzure toodeploy web uygulama tooAzure gönderme.

1. VS Code'da hello seçin **Git** hello sol gezinti çubuğunda seçeneği.
   
    ![VS code'da Git simgesi](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Seçin **Initialize git deposu** toomake emin çalışma alanınız olduğundan git kaynak denetimi altında. 
   
    ![Git başlatma](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Merhaba komut penceresi açın ve dizinleri toohello dizini, web uygulamanızın değiştirin. Ardından, komutu aşağıdaki hello girin:
   
        git config core.autocrlf false
   
    Bu komut, burada CRLF sonları ve LF sonları oynayan metin ilgili bir sorunu önler.
4. VS code'da kaydetme iletisi ekleyin ve hello tıklatın **tamamlama tüm** onay simgesi.
   
    ![Git Tümünü Yürüt](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Git işleme tamamlandıktan sonra hello Git penceresinde altında listelenen dosyası yok görürsünüz **değişiklikleri**. 
   
    ![Git hiçbir değişiklik](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Geri toohello komut burada hello komut istemi toohello dizin işaret web uygulamanızı bulunduğu penceresi değiştirin.
7. Merhaba Git daha önce kopyaladığınız URL'yi (".git" alanında biten) kullanarak güncelleştirmeleri tooyour web uygulaması gönderilmesi için uzak bir başvuru oluşturun.
   
        git remote add azure [URL for remote repository]
8. Git toosave kimlik bilgilerinizi VS koddan oluşturulan otomatik olarak eklenen tooyour itme komutları yerel olarak olacak şekilde yapılandırın.
   
        git config credential.helper store
9. Değişiklikleri tooAzure komutu aşağıdaki hello girerek iletin. Bu ilk anında tooAzure sonra tüm hello itme VS koddan komutları mümkün toodo olacaktır. 
   
        git push -u azure master
   
    Azure'da daha önce oluşturduğunuz hello parola istenir. **Not: Parolanızı görünür olmaz.**
   
    Merhaba komutu yukarıda Hello çıktısını dağıtım başarılı olduğunu belirten bir ileti ile sona erer.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Değişiklikleri tooyour uygulama yaparsanız, doğrudan kodda VS hello seçerek hello yerleşik Git işlevini kullanarak yayımlayabilirsiniz **Commit tüm** seçeneğinin ardından hello tarafından **anında** seçeneği. Hello bulacaksınız **anında** seçeneği hello açılır menü sonraki toohello kullanılabilir **yürütme tüm** ve **yenileme** düğmeler.
> 
> 

Bir proje üzerinde toocollaborate gerekiyorsa, tooAzure Ftp'den Between tooGitHub Ftp'den düşünmelisiniz.

## <a name="run-hello-app-in-azure"></a>Azure'da Hello uygulamayı çalıştırma
Şimdi web uygulamanızı dağıttıysanız, Azure'da barındırılan sırada hello uygulamayı çalıştırın. 

Bu iki yolla yapılabilir:

* Bir tarayıcı açın ve aşağıdaki gibi web uygulamanızın hello adını girin.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Buna hello Azure Portal, web uygulamanız için başlangıç web uygulaması dikey bulun ve tıklatın **Gözat** tooview uygulamanızı 
* varsayılan tarayıcınızda.

![Azure web uygulaması](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Özet
Bu öğreticide, nasıl öğrenilen toocreate VS code'da bir web uygulaması ve tooAzure dağıtın. VS Code hakkında daha fazla bilgi için hello makalesine bakın [neden Visual Studio Code?](https://code.visualstudio.com/Docs/) App Service web apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](app-service-web-overview.md). 

