---
title: "Azure Cosmos DB: Xamarin ve Facebook kimlik doğrulaması ile web uygulaması derleme | Microsoft Docs"
description: "Tooconnect tooand kullanabileceğiniz bir .NET kod örnek sorgu Azure Cosmos DB sunar"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: .NET, Xamarin ve Facebook kimlik doğrulaması ile web uygulaması derleme

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir. Daha sonra yapı ve hello üzerinde oluşturulmuş bir Yapılacaklar listesi web uygulaması dağıtma [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)ve hello Azure Cosmos DB yetkilendirme altyapısı. Merhaba Yapılacaklar listesi web uygulamasının Facebook kimlik doğrulama kullanarak kullanıcıların toologin sağlayan bir kullanıcı başına veri deseni uygular ve kendi toodo öğelerini yönetin.

## <a name="prerequisites"></a>Ön koşullar

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Koleksiyon ekleme

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi github, kopya bir DocumentDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Ardından Visual Studio'da hello samples/xamarin/UserItems/xamarin.forms klasöründen hello DocumentDBTodo.sln dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Merhaba Xamarin klasöründeki Hello kod içerir:

* Xamarin uygulaması. Merhaba uygulama hello kullanıcının yapılacaklar öğelerini UserItems adlı bölümlendirilmiş bir koleksiyon içinde depolar.
* Kaynak belirteci aracı API’si. Basit bir ASP.NET Web API toobroker Azure Cosmos DB kaynak oturum açmış olan kullanıcılar hello uygulamasının toohello belirteçleri. Kaynak, kullanıcının verileri günlüğe hello erişim toohello hello uygulama sağlamak kısa süreli erişim belirteçleri belirteçleridir.

Merhaba kimlik doğrulaması ve veri akış hello çizimde gösterilmiştir.

* Merhaba UserItems koleksiyonu hello bölüm anahtarı ile oluşturulan ' / UserID'. Bir koleksiyon için bir bölüm anahtarı Azure Cosmos DB tooscale sonsuz hello kullanıcı sayısı ve öğeleri tanır belirtme artar.
* Merhaba Xamarin uygulaması Facebook kimlik bilgilerine sahip kullanıcılar toologin sağlar.
* Merhaba Xamarin uygulaması Facebook erişim belirteci tooauthenticate ResourceTokenBroker API'si ile kullanır.
* Merhaba kaynak belirteci Aracısı API uygulama hizmet kimlik doğrulama özelliğini kullanarak hello isteğin kimliğini doğrular ve bir Azure Cosmos DB kaynak belirteci hello kimliği doğrulanmış kullanıcının bölüm anahtarı paylaşımı okuma/yazma erişimi tooall belgelerle ister.
* Kaynak belirteci Aracısı hello kaynak belirteci toohello istemci uygulamasını döndürür.
* Merhaba uygulama hello kullanıcının yapılacaklar öğelerini hello kaynak belirteci kullanarak erişir.

![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. Merhaba sonraki adımda hello Web.config dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello URI ve birincil anahtar kullanacaksınız.

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-xamarin-dotnet/keys.png)

2. Visual Studio 2017 içinde hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker klasöründeki hello Web.config dosyasını açın. 

3. URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello accountUrl Web.config dosyasındaki değeri. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello accountKey Web.congif içinde değeri. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 

## <a name="build-and-deploy-hello-web-app"></a>Derleme ve hello web uygulaması dağıtma

1. Hello Azure portal'da, bir uygulama hizmeti Web sitesi toohost hello kaynak belirteci Aracısı API oluşturun.
2. Hello Azure portal, hello hello kaynak belirteci Aracısı API Web uygulaması ayarları dikey penceresini açın. Uygulama ayarları aşağıdaki hello doldurun:

    * accountUrl - Azure Cosmos DB hesabınızın hello anahtarları sekmesinden hello Azure Cosmos DB hesap URL'si.
    * accountKey - hello Azure Cosmos DB hesabı ana anahtarını Azure Cosmos DB hesabınızın hello anahtarları sekmesinden.
    * Oluşturduğunuz veritabanı ve koleksiyonun databaseId ile collectionId değerleri

3. Yayımlama Hello ResourceTokenBroker çözüm tooyour Web sitesi oluşturuldu.

4. Merhaba Xamarin projesini açın ve tooTodoItemManager.cs gidin. Merhaba kaynak belirteci Aracısı Web sitesi için hello temel https URL'si olarak accountURL, CollectionId, Databaseıd yanı sıra resourceTokenBrokerURL hello değerlerini doldurun.

5. Tam hello [nasıl tooconfigure App Service uygulama toouse Facebook oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) öğretici toosetup Facebook kimlik doğrulaması ve hello ResourceTokenBroker Web sitesini yapılandırın.

    Merhaba Xamarin uygulaması çalıştırın.

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin: 

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından yeni oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve derleme ve Xamarin uygulaması dağıtma öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB hesabınıza veri aktarma](import-data.md)
