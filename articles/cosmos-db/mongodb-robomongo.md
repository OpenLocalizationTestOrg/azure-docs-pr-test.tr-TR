---
title: "Azure Cosmos DB Robomongo kullanın | Microsoft Docs"
description: "Bir Azure Cosmos DB ile Robomongo kullanmayı öğrenin: API MongoDB hesabı"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="607b0-104">Bir Azure Cosmos DB ile Robomongo kullanın: API MongoDB hesabı</span><span class="sxs-lookup"><span data-stu-id="607b0-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="607b0-105">Bir Azure Cosmos DB'ye bağlanmasına: API MongoDB hesabının Robomongo kullanarak, şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="607b0-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="607b0-106">İndirme ve yükleme [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="607b0-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="607b0-107">Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri</span><span class="sxs-lookup"><span data-stu-id="607b0-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="607b0-108">Robomongo kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="607b0-108">Connect using Robomongo</span></span>
<span data-ttu-id="607b0-109">Azure Cosmos DB eklemek için: API MongoDB hesap Robomongo MongoDB bağlantılar için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="607b0-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="607b0-110">Azure Cosmos DB almak: API MongoDB hesap bağlantı bilgilerini yönergeleri kullanarak [burada](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="607b0-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="607b0-112">Çalıştırma *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="607b0-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="607b0-113">Altında bağlantı düğmesini **dosya** bağlantılarınızı yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="607b0-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="607b0-114">Ardından **oluşturma** içinde **MongoDB bağlantıları** açılır pencere **bağlantı ayarlarını** penceresi.</span><span class="sxs-lookup"><span data-stu-id="607b0-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="607b0-115">İçinde **bağlantı ayarlarını** penceresinde, bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="607b0-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="607b0-116">Ardından, bulma **konak** ve **bağlantı noktası** adım 1, bağlantı bilgileri ve girmeyi **adresi** ve **bağlantı noktası**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="607b0-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Robomongo bağlantılarını yönet ekran görüntüsü](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="607b0-118">Üzerinde **kimlik doğrulaması** sekmesini tıklatın, **gerçekleştirme kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="607b0-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="607b0-119">Ardından, veritabanınızın girin (varsayılan değer *yönetici*), **kullanıcı adı** ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="607b0-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="607b0-120">Her ikisi de **kullanıcı adı** ve **parola** bağlantı bilgilerinizi adım 1'de bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="607b0-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Robomongo kimlik doğrulaması sekmesinin Ekran görüntüsü](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="607b0-122">Üzerinde **SSL** sekmesi, onay **SSL kullan Protokolü**, sonra değiştirmek **kimlik doğrulama yöntemini** için **otomatik olarak imzalanan sertifika**.</span><span class="sxs-lookup"><span data-stu-id="607b0-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Robomongo SSL sekmesinin Ekran görüntüsü](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="607b0-124">Son olarak, tıklatın **Test** , ardından bağlanabiliyor olduğunu doğrulamak için **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="607b0-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="607b0-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="607b0-125">Next steps</span></span>
* <span data-ttu-id="607b0-126">Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="607b0-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
