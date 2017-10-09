---
title: "aaaContinuous dağıtım tooAzure App Service | Microsoft Docs"
description: "Bilgi nasıl tooenable sürekli dağıtım tooAzure uygulama hizmeti."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>Sürekli dağıtım tooAzure uygulama hizmeti
Bu öğretici şunların nasıl yapıldığını gösterir tooconfigure sürekli dağıtımı iş akışı için [Azure App Service] uygulama. BitBucket, GitHub, uygulama hizmeti tümleşme ve [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) bir sürekli etkinleştirir hello en son güncelleştirmeleri projenizden Azure burada çekmesi dağıtımı iş akışı yayımlanan bu hizmetlerin tooone. Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir.

nasıl tooconfigure sürekli dağıtım depodan tarafından listelenmeyen el ile bir bulut hello Azure Portal çıkışı toofind (gibi [GitLab](https://gitlab.com/)), bkz: [el ile adımları kullanarak sürekli dağıtım ayarı](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Sürekli dağıtımı etkinleştirme
tooenable sürekli dağıtım

1. Sürekli dağıtım için kullanılacak olan uygulama içerik toohello deponuza yayımlayın.  
    Proje toothese hizmetlerinizi yayımlama ile ilgili daha fazla bilgi için bkz: [deposu (GitHub) oluşturma], [deposu (BitBucket) oluşturma], ve [VSTS ile çalışmaya başlama].
2. Uygulamanızın menü dikey penceresinde hello içinde [Azure portal], tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri**. Tıklatın **Kaynağı Seç**seçeneğini belirleyip hello dağıtım kaynağı.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure VSTS hesap uygulama hizmeti dağıtımı için lütfen bkz. Bu [Öğreticisi](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Merhaba yetkilendirme iş akışı tamamlayın.
4. Merhaba, **dağıtım kaynağı** dikey penceresinde hello projesini seçin ve dal gelen toodeploy. İşiniz bittiğinde, **Tamam**’a tıklayın.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > GitHub veya BitBucket ile sürekli dağıtımı etkinleştirirken hem genel hem de özel projeler gösterilir.
   > 
   > 
   
    Uygulama hizmeti hello seçili deposu ile ilişkilendirir, hello belirtilen şube hello dosyalarından çeker ve deponuz App Service uygulamanız için bir kopyasını tutar. VSTS hello Azure portalı sürekli dağıtımı yapılandırdığınızda hello tümleştirme hello uygulama hizmeti kullanan [Kudu dağıtım altyapısı](https://github.com/projectkudu/kudu/wiki), hangi zaten ile derleme ve dağıtım görevleri otomatikleştiren her `git push`. Tooseparately gerekmez VSTS sürekli dağıtım ayarlayın. Bu işlem, hello tamamlandıktan sonra **dağıtım seçenekleri** uygulaması dikey dağıtım belirten etkin dağıtımı başarılı gösterir.
5. tooverify hello uygulama başarıyla dağıtıldığından, hello tıklatın **URL** hello uygulamanızın dikey penceresinde hello Azure portal hello üstünde.
6. sürekli dağıtım tercih ettiğiniz hello depodan oluştuğunu tooverify bir değişiklik toohello deposu iletin. Kısa süre içinde hello itme toohello depo tamamlandıktan sonra uygulamanızı tooreflect hello değişiklikleri güncelleştirmeniz gerekir. Merhaba hello güncelleştirmedeki çekilen doğrulayabilirsiniz **dağıtım seçenekleri** dikey penceresinde uygulamanızı.

## <a name="VSsolution"></a>Visual Studio çözümünün sürekli dağıtımı
Visual Studio çözümü tooAzure uygulama hizmeti Ftp'den basit index.html dosya itme olarak oldukça kolaydır. Merhaba uygulama hizmeti dağıtım işlemi NuGet bağımlılıkları geri yükleme ve hello uygulama ikili dosyaları oluşturma dahil olmak üzere tüm hello ayrıntıları kolaylaştırır. Git deponuz yalnızca kodda sürdürme hello kaynak denetimi en iyi uygulamaları izleyin ve uygulama hizmeti dağıtım ilgilenebilmek hello geri kalanı sağlayabilirsiniz.

Merhaba, Visual Studio çözümü tooApp hizmet gönderilmesi için adımları aynı olduğu gibi hello hello [önceki bölümde](#overview), çözümünüz ve depo gibi yapılandırmanız koşuluyla:

* Merhaba Visual Studio kaynak denetim seçeneği toogenerate kullanmak bir `.gitignore` dosya aşağıdaki hello görüntü gibi veya el ile eklemeniz bir `.gitignore` içerik benzer toothis ile depo kök dosyasında [.gitignore örnek](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Merhaba tüm çözümün dizin ağacında tooyour depo hello depo kök hello .sln dosyasını ekleyin.

Deponuz açıklandığı ayarlayın ve uygulamanızı sürekli yayımlama hello çevrimiçi Git depoları birinden Azure içinde yapılandırılmış sonra ASP.NET uygulamanızı yerel olarak Visual Studio'da geliştirme ve sürekli olarak kodunuzu yalnızca göre dağıtma değişiklikleri tooyour çevrimiçi Git deponuzu Ftp'den.

## <a name="disableCD"></a>Sürekli dağıtımı devre dışı bırakma
toodisable sürekli dağıtım

1. Uygulamanızın menü dikey penceresinde hello içinde [Azure portal], tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri**. Ardından **Bağlantıyı Kes** hello içinde **dağıtım seçenekleri** dikey.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Yanıtlama sonra **Evet** toohello onay iletisi tooyour uygulamanızın dikey dönün ve tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri** tooset başka bir kaynaktan yayımlamayı istiyorsanız.

## <a name="additional-resources"></a>Ek Kaynaklar
* [İle sürekli dağıtımın nasıl tooinvestigate ortak sorunları](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Nasıl toouse Azure PowerShell]
* [Nasıl toouse hello Azure komut satırı araçları Mac ve Linux için]
* [Git belgeleri]
* [Kudu Projesi](https://github.com/projectkudu/kudu/wiki)
* [Azure kullanmak tooautomatically bir CI/CD ardışık düzen toodeploy ASP.NET 4 uygulaması oluştur](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Nasıl toouse Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Nasıl toouse hello Azure komut satırı araçları Mac ve Linux için]:../cli-install-nodejs.md
[Git Belgeleri]: http://git-scm.com/documentation

[deposu (GitHub) oluşturma]: https://help.github.com/articles/create-a-repo
[deposu (BitBucket) oluşturma]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[VSTS ile çalışmaya başlama]: https://www.visualstudio.com/docs/vsts-tfs-overview
