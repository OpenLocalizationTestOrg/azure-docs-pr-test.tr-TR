---
title: "Bir Azure Cosmos DB hesaba MongoDB bağlantı dizesini | Microsoft Docs"
description: "MongoDB bağlantı dizesi kullanarak bir Azure Cosmos DB hesabına MongoDB uygulamanızı bağlayacağınızı öğrenin."
keywords: "mongodb bağlantı dizesi"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="a4a29-104">Azure Cosmos DB MongoDB uygulamaya bağlama</span><span class="sxs-lookup"><span data-stu-id="a4a29-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="a4a29-105">MongoDB bağlantı dizesi kullanarak bir Azure Cosmos DB hesabına MongoDB uygulamanızı bağlayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a4a29-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="a4a29-106">Daha sonra verileri olarak Azure Cosmos DB veritabanı kullanabilirsiniz MongoDB uygulamanız için deposu.</span><span class="sxs-lookup"><span data-stu-id="a4a29-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="a4a29-107">Bu öğretici, bağlantı dizesi bilgilerini almak için iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="a4a29-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="a4a29-108">[Hızlı Başlangıç yöntemi](#QuickstartConnection), .NET, Node.js, MongoDB Kabuk, Java ve Python sürücüleri ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="a4a29-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="a4a29-109">[Özel bağlantı dizesi yöntemi](#GetCustomConnection), diğer sürücülerin ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="a4a29-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4a29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4a29-110">Prerequisites</span></span>

- <span data-ttu-id="a4a29-111">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a4a29-111">An Azure account.</span></span> <span data-ttu-id="a4a29-112">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure hesabı](https://azure.microsoft.com/free/) şimdi.</span><span class="sxs-lookup"><span data-stu-id="a4a29-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="a4a29-113">Bir Azure Cosmos DB hesabı.</span><span class="sxs-lookup"><span data-stu-id="a4a29-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="a4a29-114">Yönergeler için bkz: [.NET ve Azure portal ile bir MongoDB API web uygulaması oluşturma](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a4a29-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="a4a29-115"><a id="QuickstartConnection"></a>Hızlı Başlangıç'ı kullanarak MongoDB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="a4a29-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="a4a29-116">Bir Internet tarayıcısında oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4a29-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4a29-117">İçinde **Azure Cosmos DB** dikey penceresinde API MongoDB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="a4a29-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="a4a29-118">Hesap dikey pencerenin sol bölmede tıklatın **Hızlı Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="a4a29-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="a4a29-119">Platformunuzu seçin (**.NET**, **Node.js**, **MongoDB Kabuk**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="a4a29-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="a4a29-120">Sürücü veya listelenen, aracı endişelenmeyin--görmüyorsanız, biz sürekli olarak daha fazla bağlantı kod parçacıkları belge.</span><span class="sxs-lookup"><span data-stu-id="a4a29-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="a4a29-121">Lütfen aşağıda ne görmek istediğiniz üzerinde açıklama.</span><span class="sxs-lookup"><span data-stu-id="a4a29-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="a4a29-122">Kendi bağlantısı oluşturabilir öğrenmek için okuma [hesabın bağlantı dizesi bilgilerini al](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="a4a29-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="a4a29-123">Kopyalayıp MongoDB uygulamanıza kod parçacığını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4a29-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Hızlı Başlangıç dikey penceresi](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="a4a29-125"><a id="GetCustomConnection"></a>Özelleştirme için MongoDB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="a4a29-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="a4a29-126">Bir Internet tarayıcısında oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4a29-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4a29-127">İçinde **Azure Cosmos DB** dikey penceresinde API MongoDB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="a4a29-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="a4a29-128">Hesap dikey pencerenin sol bölmede tıklatın **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="a4a29-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="a4a29-129">**Bağlantı dizesi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a4a29-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="a4a29-130">Hesabınıza preconstructed bağlantı dizesi dahil olmak üzere MongoDB için bir sürücü kullanarak bağlanmak için gereken tüm bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a4a29-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Bağlantı dizesi dikey penceresi](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="a4a29-132">Bağlantı dizesi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="a4a29-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="a4a29-133">Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartları vardır.</span><span class="sxs-lookup"><span data-stu-id="a4a29-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="a4a29-134">Azure Cosmos DB hesapların gerektirdiği kimlik doğrulaması ve güvenli iletişim aracılığıyla *SSL*.</span><span class="sxs-lookup"><span data-stu-id="a4a29-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="a4a29-135">Azure Cosmos DB destekleyen standart MongoDB bağlantı dizesi URI biçimi, birkaç belirli gereksinimleri: Azure Cosmos DB hesapları, kimlik doğrulama ve SSL üzerinden güvenli iletişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a4a29-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="a4a29-136">Bu nedenle, bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a4a29-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="a4a29-137">Bu dize değerlerini mevcuttur **bağlantı dizesi** daha önce gösterilen dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="a4a29-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="a4a29-138">Kullanıcı adı (gerekli): Azure Cosmos DB hesap adı.</span><span class="sxs-lookup"><span data-stu-id="a4a29-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="a4a29-139">Parola (gerekli): Azure Cosmos DB hesap parolası.</span><span class="sxs-lookup"><span data-stu-id="a4a29-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="a4a29-140">Ana bilgisayar (gerekli): Azure Cosmos DB hesabı'nın FQDN'si.</span><span class="sxs-lookup"><span data-stu-id="a4a29-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="a4a29-141">Bağlantı noktası (gerekli): 10255 değerini bulur.</span><span class="sxs-lookup"><span data-stu-id="a4a29-141">Port (required): 10255.</span></span>
* <span data-ttu-id="a4a29-142">Veritabanı (isteğe bağlı): bağlantı kullanan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a4a29-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="a4a29-143">Hiçbir veritabanı sağladıysanız varsayılan veritabanı "test".</span><span class="sxs-lookup"><span data-stu-id="a4a29-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="a4a29-144">SSL = true (gerekli)</span><span class="sxs-lookup"><span data-stu-id="a4a29-144">ssl=true (required)</span></span>

<span data-ttu-id="a4a29-145">Örneğin, gösterilen hesap göz önünde bulundurun **bağlantı dizesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="a4a29-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="a4a29-146">Geçerli bir bağlantı dizesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a4a29-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="a4a29-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4a29-147">Next steps</span></span>
* <span data-ttu-id="a4a29-148">Bilgi nasıl [MongoChef kullanmak](mongodb-mongochef.md) Azure Cosmos DB API MongoDB hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="a4a29-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="a4a29-149">Azure Cosmos DB API MongoDB için görüntüleyerek keşfedin [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4a29-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
