---
title: "Azure Service Fabric uygulaması bir taraf kümeye dağıtma | Microsoft Docs"
description: "Bir uygulamayı bir taraf kümesine dağıtmayı öğrenin."
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
ms.openlocfilehash: 6624d683edb548a65d07ab4012c599faaf940ed0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-to-a-party-cluster-in-azure"></a>Azure taraf kümede bir uygulamayı dağıtma
Bu öğretici iki serinin bir parçasıdır ve Azure taraf kümede Azure Service Fabric uygulama dağıtma gösterir.

Bölümünde öğretici dizisinin iki bilgi nasıl yapılır:
> [!div class="checklist"]
> * Visual Studio kullanarak uzak bir küme bir uygulamayı dağıtma
> * Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma

Bu öğretici serisinde öğrenin nasıl yapılır:
> [!div class="checklist"]
> * [Bir .NET Service Fabric uygulaması oluşturma](service-fabric-tutorial-create-dotnet-app.md)
> * Uzak bir küme için uygulama dağıtma
> * [CI/CD Visual Studio Team Services kullanarak yapılandırma](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Visual Studio 2017 yükleme](https://www.visualstudio.com/) yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.
- [Service Fabric SDK yükleme](service-fabric-get-started.md)

## <a name="download-the-voting-sample-application"></a>Oylama örnek uygulamayı indirin
Oylama örnek uygulama yapı içinde değil, [Bu öğretici seri birini Kısım](service-fabric-tutorial-create-dotnet-app.md), yükleyebilirsiniz. Bir komut penceresinde örnek uygulama depoyu yerel makinenize kopyalamak için aşağıdaki komutu çalıştırın.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Taraf küme ayarlama
Grup kümeleri, Azure üzerinde barındırılan ve Service Fabric ekibi tarafından sunulan ücretsiz, sınırlı süreli Service Fabric kümeleridir. Bu kümelerde herkes uygulama dağıtabilir ve platform hakkında bilgi edinebilir. Ücretsiz!

Bir taraf kümesine erişmek için bu siteye göz atın: http://aka.ms/tryservicefabric ve bir küme erişmek için yönergeleri izleyin. Bir taraf kümesine erişmek için bir Facebook veya GitHub hesabı gerekir.

> [!NOTE]
> Parti kümeleri sağlanmaz, bu nedenle uygulamalarınız ve bunları put herhangi bir veri başkalarına görünür olabilir. Başkalarının görmesini istemiyorsanız herhangi bir şey dağıtmazsınız. Tüm Ayrıntılar için kullanım koşullarını üzerinden okuduğunuzdan emin olun.

## <a name="configure-the-listening-port"></a>Dinleme bağlantı noktasını yapılandırın
VotingWeb ön uç hizmeti oluşturulduğunda, Visual Studio bir bağlantı noktası üzerinde dinleme hizmeti için rastgele seçer.  VotingWeb hizmeti bu uygulama için ön uç gibi davranır ve dış trafiği kabul eder, sağlandığından hizmet sabit bir bağlayabilir ve bağlantı noktası iyi biliyor. Çözüm Gezgini'nde açık *VotingWeb/PackageRoot/ServiceManifest.xml*.  Bul **Endpoint** kaynak **kaynakları** bölümünde ve değiştirme **bağlantı noktası** 80 değeri.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Ayrıca 'F5' kullanarak hata ayıklamasını yaparken doğru bağlantı noktasına bir web tarayıcısı açar şekilde oylama Proje uygulama URL'si özelliği değeri güncelleştirin.  Çözüm Gezgini'nde seçin **oylama** proje ve güncelleştirme **uygulama URL'si** özelliği.

![Uygulama URL'si](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-the-app-to-the-azure"></a>Uygulamayı Azure'a dağıtma
Uygulama hazır, Visual Studio'dan doğrudan taraf kümeye dağıtabilirsiniz.

1. Sağ **oylama** Çözüm Gezgini'nde ve **Yayımla**.

    ![Yayımla İletişim Kutusu](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Bağlantı uç noktasının türünde taraf kümede **bağlantı uç noktasının** alanına gelin ve **Yayımla**.

    Yayımla tamamlandıktan sonra uygulamayı bir tarayıcı aracılığıyla bir istek göndermek görebilmeniz gerekir.

3. Küme adresi (bağlantı uç noktasının bağlantı noktası bilgilerini - örneğin, win1kw5649s.westus.cloudapp.azure.com olmadan) açın, tercih edilen tarayıcı ve yazın.

    Uygulamayı yerel olarak çalıştırırken gördüğünüz gibi şimdi aynı sonucu görmeniz gerekir.

    ![Küme API yanıtından](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-the-application-from-a-cluster-using-service-fabric-explorer"></a>Uygulama Service Fabric Explorer kullanarak kümeden kaldırma
Service Fabric Explorer keşfedin ve Service Fabric kümesi uygulamaları yönetmek için bir grafik kullanıcı arabirimidir.

Uygulamayı taraf kümeden kaldırmak için:

1. Taraf küme kaydolma sayfası tarafından sağlanan bağlantıyı kullanarak Service Fabric Explorer gidin. Örneğin, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. Service Fabric Gezgini'ne gidin **fabric://Voting** sol taraftaki treeview düğümüne.

3. ' I tıklatın **eylem** düğmesini sağ **Essentials** bölmesinde ve **uygulama Sil**. Kümede çalışan uygulamamız örneğini kaldırır Uygulama örneğinin silmeden onaylayın.

![Service Fabric Explorer'da uygulama silme](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-the-application-type-from-a-cluster-using-service-fabric-explorer"></a>Uygulama türü Service Fabric Explorer kullanarak kümeden kaldırma
Uygulamaları, birden çok örnekleri ve küme içinde çalışan uygulama sürümlerini olanak tanıyan bir Service Fabric kümesi uygulama türü olarak dağıtılır. Uygulamamız çalışan örneği kaldırdıktan sonra biz temizleme dağıtım işlemini tamamlamak için türü de kaldırabilirsiniz.

Service Fabric uygulaması modelleri hakkında daha fazla bilgi için bkz: [Service Fabric uygulamada Model](service-fabric-application-model.md).

1. Gidin **VotingType** treeview düğümüne.

2. ' I tıklatın **eylem** düğmesini sağ **Essentials** bölmesinde ve **sağlamayı kaldırma türü**. Uygulama türü sağlamanın kaldırılması onaylayın.

![Service Fabric Explorer'da uygulama türü sağlama](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Bu öğreticiyi sonlandırır.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Visual Studio kullanarak uzak bir küme bir uygulamayı dağıtma
> * Bir uygulama Service Fabric Explorer kullanarak kümeden kaldırma

Sonraki öğretici ilerleyin:
> [!div class="nextstepaction"]
> [Visual Studio Team Services kullanarak sürekli tümleştirme kurup](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)