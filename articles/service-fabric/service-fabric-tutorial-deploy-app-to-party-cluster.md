---
title: "Azure Service Fabric uygulaması tooa taraf küme aaaDeploy | Microsoft Docs"
description: "Bilgi toodeploy bir uygulama tooa taraf küme nasıl."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>Bir uygulama tooa Azure taraf kümeye dağıtma
Bu öğretici iki serinin bir parçasıdır ve nasıl gösterir toodeploy Azure Service Fabric uygulaması tooa Azure taraf kümede.

Bölümünde hello öğretici dizisinin iki bilgi nasıl yapılır:
> [!div class="checklist"]
> * Visual Studio kullanarak bir uygulama tooa uzak bir kümeyi dağıtma
> * Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma

Bu öğretici serisinde öğrenin nasıl yapılır:
> [!div class="checklist"]
> * [Bir .NET Service Fabric uygulaması oluşturma](service-fabric-tutorial-create-dotnet-app.md)
> * Merhaba uygulama tooa uzak kümesi dağıtma
> * [CI/CD Visual Studio Team Services kullanarak yapılandırma](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.
- [Merhaba Service Fabric SDK yükleme](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>Merhaba oylama örnek uygulamayı indirin
Merhaba oylama örnek uygulaması oluşturacağınız değil, [Bu öğretici seri birini Kısım](service-fabric-tutorial-create-dotnet-app.md), yükleyebilirsiniz. Bir komut penceresinde komut tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Taraf küme ayarlama
Parti kümeleri Azure üzerinde barındırılan ve burada herkes uygulamaları dağıtabilir ve hello platform hakkında bilgi edinin hello Service Fabric ekibi tarafından çalıştırılan ücretsiz, sınırlı süre Service Fabric kümeleri ' dir. Ücretsiz!

tooget erişim tooa taraf küme toothis site göz atın: http://aka.ms/tryservicefabric ve izleme hello yönergeleri tooget erişim tooa küme. Bir Facebook veya GitHub hesabı tooget erişim tooa taraf küme gerekir.

> [!NOTE]
> Parti kümeleri sağlanmaz, bu nedenle uygulamalarınız ve bunları put herhangi bir veri görünür tooothers olabilir. Başkalarının istemiyorsanız herhangi bir şey dağıtmazsınız toosee. Tüm hello Ayrıntılar için kullanım koşullarını üzerinden tooread emin olun.

## <a name="configure-hello-listening-port"></a>Merhaba dinleme bağlantı noktasını yapılandırın
Merhaba VotingWeb ön uç hizmeti oluşturulduğunda, Visual Studio hello hizmet toolisten için bir bağlantı noktası üzerinde rastgele seçer.  Merhaba VotingWeb hizmet hello bu uygulama için ön uç görevi görür ve dış trafiği kabul eder, sağlandığından sabit bu hizmet tooa bağlayabilir ve bağlantı noktası iyi biliyor. Çözüm Gezgini'nde açık *VotingWeb/PackageRoot/ServiceManifest.xml*.  Hello bulur **Endpoint** hello kaynağında **kaynakları** bölümünde ve hello değiştirme **bağlantı noktası** değeri too80.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

'F5' kullanarak hata ayıklama işlemi yaparken bir web tarayıcısı toohello doğru bağlantı noktası açar. Ayrıca hello uygulama URL'si özelliği değeri hello oylama projesinde güncelleştirin.  Çözüm Gezgini'nde hello seçin **oylama** proje ve güncelleştirme hello **uygulama URL'si** özelliği.

![Uygulama URL'si](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>Merhaba uygulama toohello Azure dağıtma
Merhaba uygulama hazır, toohello taraf küme Visual Studio'dan doğrudan dağıtabilirsiniz.

1. Sağ **oylama** içinde Çözüm Gezgini hello ve seçin **Yayımla**.

    ![Yayımla İletişim Kutusu](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Merhaba hello taraf küme hello bağlantı uç noktasının türünde **bağlantı uç noktasının** alanına gelin ve **Yayımla**.

    Merhaba yayımladıktan sonra sahip bitirdiğinizde, mümkün toosend bir istek toohello uygulaması bir tarayıcı aracılığıyla olmalıdır.

3. Açık tarayıcı ve hello küme adresini (Merhaba bağlantı uç noktası başlangıç bağlantı noktası bilgilerini - örneğin, win1kw5649s.westus.cloudapp.azure.com olmadan) yazın tercih ettiğiniz.

    Merhaba uygulamayı yerel olarak çalıştırırken gördüğünüz gibi aynı sonucu hello görmelisiniz.

    ![Küme API yanıtından](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>Merhaba uygulaması Service Fabric Explorer kullanarak kümeden kaldırma
Service Fabric Explorer bir grafik kullanıcı arabirimi tooexplore olduğundan ve bir Service Fabric kümesi uygulamalarda yönetin.

Merhaba uygulamadan hello taraf küme tooremove:

1. Toohello hello taraf küme kaydolma sayfası tarafından sağlanan hello bağlantıyı kullanarak Service Fabric Explorer gidin. Örneğin, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. Service Fabric Explorer'da toohello gidin **fabric://Voting** hello sol taraftaki hello treeview düğümüne.

3. Merhaba tıklatın **eylem** hello sağ düğmesini **Essentials** bölmesinde ve seçin **uygulama Sil**. Merhaba kümede çalışan uygulamamız hello örneğini kaldıran silme hello uygulama örneği onaylayın.

![Service Fabric Explorer'da uygulama silme](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>Merhaba uygulama türü Service Fabric Explorer kullanarak kümeden kaldırma
Uygulamalar, toohave birden çok örnekleri ve hello küme içinde çalışan hello uygulama sürümlerini sağlayan bir Service Fabric kümesi uygulama türü olarak dağıtılır. Uygulamamız örneğini çalıştıran hello kaldırdıktan sonra biz hello türü, toocomplete hello temizleme hello dağıtımının da kaldırabilirsiniz.

Service Fabric hello uygulama modelleri hakkında daha fazla bilgi için bkz: [Service Fabric uygulamada Model](service-fabric-application-model.md).

1. Toohello gidin **VotingType** hello treeview düğümüne.

2. Merhaba tıklatın **eylem** hello sağ düğmesini **Essentials** bölmesinde ve seçin **sağlamayı kaldırma türü**. Sağlama geri alınıyor hello uygulama türü onaylayın.

![Service Fabric Explorer'da uygulama türü sağlama](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Merhaba öğreticiyi sonlandırır.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Visual Studio kullanarak bir uygulama tooa uzak bir kümeyi dağıtma
> * Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma

Gelişmiş toohello sonraki öğretici:
> [!div class="nextstepaction"]
> [Visual Studio Team Services kullanarak sürekli tümleştirme kurup](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)