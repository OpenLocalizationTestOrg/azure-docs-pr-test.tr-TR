---
title: "bir Azure Cosmos DB hesaba aaaMongoDB bağlantı dizesini | Microsoft Docs"
description: "Tooconnect MongoDB uygulama tooan Azure Cosmos DB nasıl hesap MongoDB bağlantı dizesi kullanarak öğrenin."
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="c611e-104">MongoDB uygulama tooAzure Cosmos DB Bağlan</span><span class="sxs-lookup"><span data-stu-id="c611e-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="c611e-105">Tooconnect MongoDB uygulama tooan Azure Cosmos DB nasıl hesap MongoDB bağlantı dizesi kullanarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c611e-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="c611e-106">Sonra Azure Cosmos DB veritabanı hello verileri olarak kullanabileceğiniz depolama MongoDB uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="c611e-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="c611e-107">Bu öğretici tooretrieve bağlantı dizesi bilgilerini sağlayan iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="c611e-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="c611e-108">[Merhaba Hızlı Başlangıç yöntemi](#QuickstartConnection), .NET, Node.js, MongoDB Kabuk, Java ve Python sürücüleri ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="c611e-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="c611e-109">[Merhaba özel bir bağlantı dizesi yöntemi](#GetCustomConnection), diğer sürücülerin ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="c611e-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c611e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c611e-110">Prerequisites</span></span>

- <span data-ttu-id="c611e-111">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="c611e-111">An Azure account.</span></span> <span data-ttu-id="c611e-112">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure hesabı](https://azure.microsoft.com/free/) şimdi.</span><span class="sxs-lookup"><span data-stu-id="c611e-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="c611e-113">Bir Azure Cosmos DB hesabı.</span><span class="sxs-lookup"><span data-stu-id="c611e-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="c611e-114">Yönergeler için bkz: [.NET ile MongoDB API web uygulaması oluşturma ve Azure portal hello](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c611e-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="c611e-115"><a id="QuickstartConnection"></a>Merhaba Hızlı Başlangıç'ı kullanarak Hello MongoDB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="c611e-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="c611e-116">Bir Internet tarayıcısında toohello içinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c611e-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c611e-117">Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello API MongoDB hesabı.</span><span class="sxs-lookup"><span data-stu-id="c611e-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="c611e-118">Merhaba sol hello hesabı dikey bölmesinde **Hızlı Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="c611e-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="c611e-119">Platformunuzu seçin (**.NET**, **Node.js**, **MongoDB Kabuk**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="c611e-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="c611e-120">Sürücü veya listelenen, aracı endişelenmeyin--görmüyorsanız, biz sürekli olarak daha fazla bağlantı kod parçacıkları belge.</span><span class="sxs-lookup"><span data-stu-id="c611e-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="c611e-121">Lütfen aşağıda ne istiyorsunuz üzerinde açıklama toosee.</span><span class="sxs-lookup"><span data-stu-id="c611e-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="c611e-122">toolearn nasıl toocraft kendi bağlantısını oku [hello hesabın bağlantı dizesi bilgilerini al](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="c611e-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="c611e-123">Kopyalayıp MongoDB uygulamanıza hello kod parçacığını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="c611e-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Hızlı Başlangıç dikey penceresi](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="c611e-125"><a id="GetCustomConnection"></a>Merhaba MongoDB bağlantı dizesi toocustomize Al</span><span class="sxs-lookup"><span data-stu-id="c611e-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="c611e-126">Bir Internet tarayıcısında toohello içinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c611e-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c611e-127">Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello API MongoDB hesabı.</span><span class="sxs-lookup"><span data-stu-id="c611e-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="c611e-128">Merhaba sol hello hesabı dikey bölmesinde **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="c611e-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="c611e-129">Merhaba **bağlantı dizesi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="c611e-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="c611e-130">Bu, tüm hello bilgiler gerekli tooconnect toohello hesabı preconstructed bağlantı dizesi dahil olmak üzere MongoDB için bir sürücü kullanarak sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c611e-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Bağlantı dizesi dikey penceresi](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="c611e-132">Bağlantı dizesi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="c611e-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="c611e-133">Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartları vardır.</span><span class="sxs-lookup"><span data-stu-id="c611e-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="c611e-134">Azure Cosmos DB hesapların gerektirdiği kimlik doğrulaması ve güvenli iletişim aracılığıyla *SSL*.</span><span class="sxs-lookup"><span data-stu-id="c611e-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="c611e-135">Azure Cosmos DB destekleyen hello standart MongoDB bağlantı dizesi URI biçimi, birkaç belirli gereksinimleri: Azure Cosmos DB hesapları, kimlik doğrulama ve SSL üzerinden güvenli iletişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c611e-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="c611e-136">Bu nedenle, hello bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c611e-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="c611e-137">Merhaba Bu dize değerleri hello kullanılabilir **bağlantı dizesi** daha önce gösterilen dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="c611e-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="c611e-138">Kullanıcı adı (gerekli): Azure Cosmos DB hesap adı.</span><span class="sxs-lookup"><span data-stu-id="c611e-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="c611e-139">Parola (gerekli): Azure Cosmos DB hesap parolası.</span><span class="sxs-lookup"><span data-stu-id="c611e-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="c611e-140">Ana bilgisayar (gerekli): hello Azure Cosmos DB hesabı'nın FQDN'si.</span><span class="sxs-lookup"><span data-stu-id="c611e-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="c611e-141">Bağlantı noktası (gerekli): 10255 değerini bulur.</span><span class="sxs-lookup"><span data-stu-id="c611e-141">Port (required): 10255.</span></span>
* <span data-ttu-id="c611e-142">Veritabanı (isteğe bağlı): bağlantı hello hello veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c611e-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="c611e-143">Hiçbir veritabanı sağladıysanız, "test" Merhaba varsayılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c611e-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="c611e-144">SSL = true (gerekli)</span><span class="sxs-lookup"><span data-stu-id="c611e-144">ssl=true (required)</span></span>

<span data-ttu-id="c611e-145">Örneğin, hello gösterilen hello hesap göz önünde bulundurun **bağlantı dizesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="c611e-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="c611e-146">Geçerli bir bağlantı dizesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c611e-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="c611e-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c611e-147">Next steps</span></span>
* <span data-ttu-id="c611e-148">Nasıl çok öğrenin[MongoChef kullanmak](mongodb-mongochef.md) Azure Cosmos DB API MongoDB hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="c611e-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="c611e-149">Hello Azure Cosmos DB API MongoDB için görüntüleyerek keşfedin [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c611e-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
