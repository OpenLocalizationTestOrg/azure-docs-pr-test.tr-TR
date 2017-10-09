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
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="c6711-103">Azure Cosmos DB: .NET, Xamarin ve Facebook kimlik doğrulaması ile web uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="c6711-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="c6711-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="c6711-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c6711-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6711-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c6711-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6711-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="c6711-107">Daha sonra yapı ve hello üzerinde oluşturulmuş bir Yapılacaklar listesi web uygulaması dağıtma [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)ve hello Azure Cosmos DB yetkilendirme altyapısı.</span><span class="sxs-lookup"><span data-stu-id="c6711-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="c6711-108">Merhaba Yapılacaklar listesi web uygulamasının Facebook kimlik doğrulama kullanarak kullanıcıların toologin sağlayan bir kullanıcı başına veri deseni uygular ve kendi toodo öğelerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="c6711-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6711-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c6711-109">Prerequisites</span></span>

<span data-ttu-id="c6711-110">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c6711-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="c6711-111">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="c6711-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c6711-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6711-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c6711-113">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="c6711-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="c6711-114">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="c6711-114">Clone hello sample application</span></span>

<span data-ttu-id="c6711-115">Artık şimdi github, kopya bir DocumentDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c6711-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="c6711-116">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c6711-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="c6711-117">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="c6711-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="c6711-118">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="c6711-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="c6711-119">Ardından Visual Studio'da hello samples/xamarin/UserItems/xamarin.forms klasöründen hello DocumentDBTodo.sln dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c6711-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="c6711-120">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="c6711-120">Review hello code</span></span>

<span data-ttu-id="c6711-121">Merhaba Xamarin klasöründeki Hello kod içerir:</span><span class="sxs-lookup"><span data-stu-id="c6711-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="c6711-122">Xamarin uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c6711-122">Xamarin app.</span></span> <span data-ttu-id="c6711-123">Merhaba uygulama hello kullanıcının yapılacaklar öğelerini UserItems adlı bölümlendirilmiş bir koleksiyon içinde depolar.</span><span class="sxs-lookup"><span data-stu-id="c6711-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="c6711-124">Kaynak belirteci aracı API’si.</span><span class="sxs-lookup"><span data-stu-id="c6711-124">Resource token broker API.</span></span> <span data-ttu-id="c6711-125">Basit bir ASP.NET Web API toobroker Azure Cosmos DB kaynak oturum açmış olan kullanıcılar hello uygulamasının toohello belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="c6711-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="c6711-126">Kaynak, kullanıcının verileri günlüğe hello erişim toohello hello uygulama sağlamak kısa süreli erişim belirteçleri belirteçleridir.</span><span class="sxs-lookup"><span data-stu-id="c6711-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="c6711-127">Merhaba kimlik doğrulaması ve veri akış hello çizimde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6711-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="c6711-128">Merhaba UserItems koleksiyonu hello bölüm anahtarı ile oluşturulan ' / UserID'.</span><span class="sxs-lookup"><span data-stu-id="c6711-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="c6711-129">Bir koleksiyon için bir bölüm anahtarı Azure Cosmos DB tooscale sonsuz hello kullanıcı sayısı ve öğeleri tanır belirtme artar.</span><span class="sxs-lookup"><span data-stu-id="c6711-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="c6711-130">Merhaba Xamarin uygulaması Facebook kimlik bilgilerine sahip kullanıcılar toologin sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6711-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="c6711-131">Merhaba Xamarin uygulaması Facebook erişim belirteci tooauthenticate ResourceTokenBroker API'si ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6711-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="c6711-132">Merhaba kaynak belirteci Aracısı API uygulama hizmet kimlik doğrulama özelliğini kullanarak hello isteğin kimliğini doğrular ve bir Azure Cosmos DB kaynak belirteci hello kimliği doğrulanmış kullanıcının bölüm anahtarı paylaşımı okuma/yazma erişimi tooall belgelerle ister.</span><span class="sxs-lookup"><span data-stu-id="c6711-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="c6711-133">Kaynak belirteci Aracısı hello kaynak belirteci toohello istemci uygulamasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="c6711-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="c6711-134">Merhaba uygulama hello kullanıcının yapılacaklar öğelerini hello kaynak belirteci kullanarak erişir.</span><span class="sxs-lookup"><span data-stu-id="c6711-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="c6711-136">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c6711-136">Update your connection string</span></span>

<span data-ttu-id="c6711-137">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c6711-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="c6711-138">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="c6711-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c6711-139">Merhaba sonraki adımda hello Web.config dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello URI ve birincil anahtar kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c6711-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="c6711-141">Visual Studio 2017 içinde hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker klasöründeki hello Web.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c6711-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="c6711-142">URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello accountUrl Web.config dosyasındaki değeri.</span><span class="sxs-lookup"><span data-stu-id="c6711-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="c6711-143">Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello accountKey Web.congif içinde değeri.</span><span class="sxs-lookup"><span data-stu-id="c6711-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="c6711-144">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="c6711-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="c6711-145">Derleme ve hello web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="c6711-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="c6711-146">Hello Azure portal'da, bir uygulama hizmeti Web sitesi toohost hello kaynak belirteci Aracısı API oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6711-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="c6711-147">Hello Azure portal, hello hello kaynak belirteci Aracısı API Web uygulaması ayarları dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="c6711-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="c6711-148">Uygulama ayarları aşağıdaki hello doldurun:</span><span class="sxs-lookup"><span data-stu-id="c6711-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="c6711-149">accountUrl - Azure Cosmos DB hesabınızın hello anahtarları sekmesinden hello Azure Cosmos DB hesap URL'si.</span><span class="sxs-lookup"><span data-stu-id="c6711-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="c6711-150">accountKey - hello Azure Cosmos DB hesabı ana anahtarını Azure Cosmos DB hesabınızın hello anahtarları sekmesinden.</span><span class="sxs-lookup"><span data-stu-id="c6711-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="c6711-151">Oluşturduğunuz veritabanı ve koleksiyonun databaseId ile collectionId değerleri</span><span class="sxs-lookup"><span data-stu-id="c6711-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="c6711-152">Yayımlama Hello ResourceTokenBroker çözüm tooyour Web sitesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c6711-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="c6711-153">Merhaba Xamarin projesini açın ve tooTodoItemManager.cs gidin.</span><span class="sxs-lookup"><span data-stu-id="c6711-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="c6711-154">Merhaba kaynak belirteci Aracısı Web sitesi için hello temel https URL'si olarak accountURL, CollectionId, Databaseıd yanı sıra resourceTokenBrokerURL hello değerlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="c6711-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="c6711-155">Tam hello [nasıl tooconfigure App Service uygulama toouse Facebook oturum açma](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) öğretici toosetup Facebook kimlik doğrulaması ve hello ResourceTokenBroker Web sitesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c6711-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="c6711-156">Merhaba Xamarin uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c6711-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="c6711-157">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="c6711-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c6711-158">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="c6711-158">Clean up resources</span></span>

<span data-ttu-id="c6711-159">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="c6711-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="c6711-160">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından yeni oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c6711-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="c6711-161">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c6711-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6711-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6711-162">Next steps</span></span>

<span data-ttu-id="c6711-163">Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve derleme ve Xamarin uygulaması dağıtma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c6711-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="c6711-164">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6711-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6711-165">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="c6711-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
