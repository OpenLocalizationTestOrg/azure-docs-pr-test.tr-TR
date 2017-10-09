---
title: "aaaDeploy Azure Service Fabric uygulamayla sürekli tümleştirme (Team Services) | Microsoft Docs"
description: "Bilgi nasıl tooset sürekli tümleştirme ve Visual Studio Team Services kullanarak bir Service Fabric uygulaması için dağıtım.  Bir uygulama tooa Service Fabric kümesi Azure dağıtın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Bir uygulama CI/CD tooa Service Fabric kümesi oluşturup dağıtın
Bu öğretici üç bir serinin bir parçasıdır ve açıklar nasıl tooset sürekli tümleştirme ve Visual Studio Team Services kullanarak bir Azure Service Fabric uygulaması için dağıtım.  Var olan bir Service Fabric uygulaması gereklidir, hello uygulama oluşturulan [bir .NET uygulaması oluşturma](service-fabric-tutorial-create-dotnet-app.md) bir örnek olarak kullanılır.

Bölümünde hello serisinin üç bilgi nasıl yapılır:

> [!div class="checklist"]
> * Kaynak denetimi tooyour projesi ekleme
> * Yapı tanımı Team Services içinde oluşturma
> * Team Services içinde bir yayın tanımı oluşturun
> * Otomatik olarak dağıtma ve uygulama yükseltme

Bu öğretici serisinde öğrenin nasıl yapılır:
> [!div class="checklist"]
> * [Bir .NET Service Fabric uygulaması oluşturma](service-fabric-tutorial-create-dotnet-app.md)
> * [Merhaba uygulama tooa uzak kümesi dağıtma](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * CI/CD Visual Studio Team Services kullanarak yapılandırma

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.
- [Merhaba Service Fabric SDK yükleme](service-fabric-get-started.md)
- Service Fabric uygulaması, örneğin oluşturun [Bu öğreticiyi izleyerek](service-fabric-tutorial-create-dotnet-app.md). 
- Azure üzerinde bir Windows Service Fabric kümesi tarafından örneğin oluşturma [Bu öğreticiyi izleyerek](service-fabric-tutorial-create-cluster-azure-ps.md)
- Oluşturma bir [Team Services hesabı](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Merhaba oylama örnek uygulamayı indirin
Merhaba oylama örnek uygulaması oluşturacağınız değil, [Bu öğretici seri birini Kısım](service-fabric-tutorial-create-dotnet-app.md), yükleyebilirsiniz. Bir komut penceresinde komut tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Bir yayımlama profili hazırlama
Artık [bir uygulama oluşturulan](service-fabric-tutorial-create-dotnet-app.md) ve [hello uygulama tooAzure dağıtılan](service-fabric-tutorial-deploy-app-to-party-cluster.md), sürekli tümleştirme hazır tooset demektir.  İlk olarak, bir yayımlama profili kullanmak için uygulama içinde Team Services içinde yürütür hello dağıtım işlemi tarafından hazırlayın.  Yayımlama Hello profil daha önceden oluşturduğunuz yapılandırılmış tootarget hello kümesine olması gerekir.  Visual Studio'yu başlatın ve var olan bir Service Fabric uygulaması projesini açın.  İçinde **Çözüm Gezgini**, hello uygulamayı sağ tıklatın ve seçin **Yayımla...** .

Uygulama projesi toouse sürekli tümleştirme iş akışınız için hedef profilinde seçin, örneğin bulut.  Merhaba küme bağlantı uç noktası belirtin.  Merhaba denetleyin **yükseltme hello uygulama** onay kutusunu böylece her dağıtımda Team Services için uygulamanızı yükseltir.  Merhaba tıklatın **kaydetmek** köprü toosave hello ayarları toohello yayımlama profili ve ardından **iptal** tooclose hello iletişim kutusu.  

![Anında iletme profili][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Visual Studio çözümü tooa Yeni Team Services Git deposuna paylaşma
Takım oluşturabileceğiniz şekilde Hizmetleri tooa takım projesinde derlemeler uygulama Kaynak dosyalarınız paylaşır.  

Projeniz için yeni bir yerel Git deposu seçerek oluşturun **tooSource denetim eklemek** -> **Git** hello durum çubuğunda hello alt sağ köşesinde Visual Studio. 

Merhaba, **anında** görünümünde **Takım Gezgini**seçin hello **yayımlama Git deposuna** altında düğmesini **anında tooVisual Studio Team Services**.

![Git deposuna Gönder][push-git-repo]

Hello hesabınızı seçin ve e-postanızı doğrulayın **Team Services etki alanı** açılır. Depo adınızı girin ve **Yayımla depo**.

![Git deposuna Gönder][publish-code]

Yayımlama Hello depodaki aynı hello yerel deposu ad hello hesabınızla yeni takım projesi oluşturur. Varolan bir takım projesinde toocreate hello depodaki tıklatın **Gelişmiş** sonraki çok**depo** ad ve bir takım projesini seçin. Seçerek kodunuzu hello Web'de de görüntüleyebilirsiniz **hello Web'de bakın**.

## <a name="configure-continuous-delivery-with-vsts"></a>Kesintisiz teslim VSTS ile yapılandırma
Bir Team Services yapı tanımı sırayla yürütülen derleme adımları kümesinden oluşan bir iş akışını açıklar. Yapı tanımı üreten bir Service Fabric uygulama paketi ve diğer yapıları, toodeploy tooa Service Fabric kümesi oluşturabilirsiniz. Daha fazla bilgi edinmek [Team Services yapı tanımları](https://www.visualstudio.com/docs/build/define/create). 

Bir Team Services sürüm tanımı bir uygulama paketi tooa küme dağıtan bir iş akışını açıklar. Birlikte kullanıldığında, hello yapı tanımı ve kaynak dosyaları tooending kümenizde çalışan bir uygulama ile başlayarak hello tüm iş akışı yayın tanımı yürütün. Team Services hakkında daha fazla bilgi [yayın tanımları](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-build-definition"></a>Yapı tanımı oluşturma
Bir web tarayıcısı açın ve tooyour yeni takım projesi konumunda gidin: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Select hello **yapı & yayın** sekmesinde, ardından **derlemeler**, ardından **+ yeni tanımı**.  İçinde **bir şablon seçin**seçin hello **Azure Service Fabric uygulaması** şablonu ve tıklatın **Uygula**. 

![Yapı şablonunu seçin][select-build-template] 

.NET Core projesi uygulama oylama hello içerir, böylece hello bağımlılıkları geri yükleyen bir görev ekleyin. Merhaba, **görevleri** görünümü, select **+ görev eklemek** hello sayfanın sol. Arama "Komut satırı" toofind hello komut satırı görevi ve ardından **Ekle**. 

![Görev ekleme][add-task] 

Merhaba yeni görevi, "dotnet.exe Çalıştır" girin **görünen adı**, "dotnet.exe" **aracı**ve "geri" **bağımsız değişkenleri**. 

![Yeni görev][new-task] 

Merhaba, **Tetikleyicileri** görüntülemek için hello tıklatın **Bu tetikleyici etkinleştirmek** altında geçiş **sürekli tümleştirme**. 

Seçin **sıraya & Kaydet** ve "Barındırılan VS2017" Merhaba girin **Aracısı sırası**. Seçin **sıra** toomanually bir yapı başlatın.  Ayrıca Tetikleyiciler İtme veya iade oluşturur.

toocheck derleme ilerleme durumunuzu, anahtar toohello **derlemeler** sekmesi.  Merhaba yapı başarılı bir şekilde çalıştığından emin olun, sonra uygulama tooa kümenizi dağıtan bir yayın tanımı tanımlayın. 

### <a name="create-a-release-definition"></a>Bir yayın tanımı oluşturun  

Select hello **yapı & yayın** sekmesinde, ardından **sürümleri**, ardından **+ yeni tanımı**.  İçinde **oluşturma yayın tanımı**seçin hello **Azure Service Fabric dağıtımı** şablonu hello listesi ve tıklatın **sonraki**.  Select hello **yapı** kaynak, hello denetleyin **sürekli dağıtım** ve'ı tıklatın **oluşturma**. 

Merhaba, **ortamları** görüntülemek için tıklatın **Ekle** sağında toohello **küme bağlantısı**.  "Mysftestcluster", küme uç noktası hello Azure Active Directory veya sertifika kimlik bilgileri ve "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" Merhaba küme için bir bağlantı adı belirtin. Azure Active Directory kimlik bilgileri için toouse tooconnect toohello hello kümesinde istediğiniz hello bilgilerini tanımlayın **kullanıcıadı** ve **parola** alanları. Sertifika tabanlı kimlik doğrulaması için dosyasının hello istemci sertifikası hello hello Base64 kodlaması tanımlamak **istemci sertifikası** alan.  Merhaba Yardım açılır nasıl ilişkin bilgi için bu alan bakın değer tooget.  Sertifikanız parola korumalıysa hello parolası hello tanımlamak **parola** alan.  Tıklatın **kaydetmek** toosave hello yayın tanımı.

![Küme Bağlantısı Ekle][add-cluster-connection] 

Tıklatın **aracı üzerinde çalıştığı**seçeneğini belirleyip **barındırılan VS2017** için **dağıtım sırası**. Tıklatın **kaydetmek** toosave hello yayın tanımı.

![Aracısı'nı çalıştırın][run-on-agent]

Seçin **+ yayın** -> **oluşturma yayın** -> **oluşturma** toomanually bir yayın oluşturun.  Merhaba dağıtımı başarılı oldu ve Merhaba uygulaması hello kümede çalışan doğrulayın.  Bir web tarayıcısı açın ve çok gidin[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Bu örnekte "1.0.0.20170616.3" olan Hello uygulama sürümü unutmayın. 

## <a name="commit-and-push-changes-trigger-a-release"></a>Yürütme ve değişiklikleri gönderin, sürüm tetikleme
Sürekli Tümleştirme ardışık düzen hello tooverify tooTeam Hizmetleri bazı kod değişikliklerini denetleyerek çalışır.    

Kodunuzu yazarken değişikliklerinizi Visual Studio tarafından otomatik olarak izlenir. Bekleyen değişiklikleri simgesi (Merhaba seçerek değişiklikleri tooyour yerel Git deposu Yürüt![Beklemede][pending]) hello durum çubuğunda hello sayfanın sağ.

Merhaba üzerinde **değişiklikleri** Takım Gezgini'nde görüntüleme, güncelleştirmeyi açıklayan bir ileti ekleyin ve değişikliklerinizi uygulamak.

![Tümünü Yürüt][changes]

Select hello yayımdan değişiklikleri durum çubuğu simgesi (![yayımlanmamış değişiklikleri][unpublished-changes]) veya eşitleme Takım Gezgini görünümünde hello. Seçin **anında** tooupdate kodunuzu Team Services/TFS.

![Değişiklikleri gönderme][push]

Merhaba değişiklikleri tooTeam Ftp'den Tetikleyicileri otomatik olarak bir yapı hizmetleri.  Merhaba derleme tanımı başarıyla tamamlandığında, bir yayın otomatik olarak oluşturulur ve Merhaba uygulaması hello kümede yükseltmeyi başlatır.

toocheck derleme ilerleme durumunuzu, anahtar toohello **derlemeler** sekmesinde **Takım Gezgini** Visual Studio.  Merhaba yapı başarılı bir şekilde çalıştığından emin olun, sonra uygulama tooa kümenizi dağıtan bir yayın tanımı tanımlayın.

Merhaba dağıtımı başarılı oldu ve Merhaba uygulaması hello kümede çalışan doğrulayın.  Bir web tarayıcısı açın ve çok gidin[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Bu örnekte "1.0.0.20170815.3" olan Hello uygulama sürümü unutmayın.

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Merhaba uygulamayı güncelleştirme
Kod değişikliklerini hello uygulamada yapın.  Kaydet ve hello önceki adımları izleyerek hello değişiklikleri uygulayın.

Merhaba yükseltin sonra hello uygulama başlar, Service Fabric Explorer'da hello yükseltme ilerleme durumunu izleyebilirsiniz:

![Service Fabric Explorer][sfx2]

Merhaba uygulama yükseltme birkaç dakika sürebilir. Merhaba yükseltme tamamlandıktan sonra Merhaba uygulaması hello sonraki sürümünü çalıştıran.  Bu örnekte "1.0.0.20170815.4".

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Kaynak denetimi tooyour projesi ekleme
> * Yapı tanımı oluşturma
> * Bir yayın tanımı oluşturun
> * Otomatik olarak dağıtma ve uygulama yükseltme

Dağıtılan bir uygulama ve sürekli tümleştirme yapılandırılmış göre hello aşağıdakileri deneyin:
- [Uygulama yükseltme](service-fabric-application-upgrade.md)
- [Bir uygulamayı test etme](service-fabric-testability-overview.md) 
- [İzleme ve tanılama](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png