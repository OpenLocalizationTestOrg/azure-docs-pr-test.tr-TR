---
title: aaaUse Azure Cosmos DB Robomongo | Microsoft Docs
description: "Bilgi nasıl toouse bir Azure Cosmos DB ile Robomongo: API MongoDB hesabı"
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="81e55-104">Bir Azure Cosmos DB ile Robomongo kullanın: API MongoDB hesabı</span><span class="sxs-lookup"><span data-stu-id="81e55-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="81e55-105">tooconnect tooan Azure Cosmos DB: API MongoDB hesabının Robomongo kullanarak, şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="81e55-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="81e55-106">İndirme ve yükleme [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="81e55-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="81e55-107">Azure Cosmos DB sahip: API MongoDB hesabı için [bağlantı dizesi](connect-mongodb-account.md) bilgileri</span><span class="sxs-lookup"><span data-stu-id="81e55-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="81e55-108">Robomongo kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="81e55-108">Connect using Robomongo</span></span>
<span data-ttu-id="81e55-109">tooadd Azure Cosmos DB: API MongoDB hesap toohello Robomongo MongoDB bağlantıları için hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="81e55-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="81e55-110">Azure Cosmos DB almak: API MongoDB hesap bağlantı bilgilerini hello yönergeleri kullanarak [burada](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="81e55-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Merhaba bağlantı dizesi dikey penceresi ekran görüntüsü](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="81e55-112">Çalıştırma *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="81e55-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="81e55-113">Merhaba bağlantı düğmesini altında **dosya** toomanage bağlantılarınızı.</span><span class="sxs-lookup"><span data-stu-id="81e55-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="81e55-114">' Ye tıklayın **oluşturma** hello içinde **MongoDB bağlantıları** hello açılır pencere **bağlantı ayarlarını** penceresi.</span><span class="sxs-lookup"><span data-stu-id="81e55-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="81e55-115">Merhaba, **bağlantı ayarlarını** penceresinde, bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="81e55-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="81e55-116">Ardından, hello bulur **konak** ve **bağlantı noktası** adım 1, bağlantı bilgileri ve bunların içine girin **adresi** ve **bağlantı noktası**sırasıyla .</span><span class="sxs-lookup"><span data-stu-id="81e55-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Merhaba Robomongo bağlantılarını yönet ekran görüntüsü](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="81e55-118">Merhaba üzerinde **kimlik doğrulaması** sekmesini tıklatın, **gerçekleştirme kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="81e55-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="81e55-119">Ardından, veritabanınızın girin (varsayılan değer *yönetici*), **kullanıcı adı** ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="81e55-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="81e55-120">Her ikisi de **kullanıcı adı** ve **parola** bağlantı bilgilerinizi adım 1'de bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="81e55-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Merhaba Robomongo kimlik doğrulama sekmesi ekran görüntüsü](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="81e55-122">Merhaba üzerinde **SSL** sekmesi, onay **SSL kullan Protokolü**, hello değiştirme **kimlik doğrulama yöntemini** çok**otomatik olarak imzalanan sertifika**.</span><span class="sxs-lookup"><span data-stu-id="81e55-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Merhaba Robomongo SSL sekmesi ekran görüntüsü](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="81e55-124">Son olarak, tıklatın **Test** mümkün tooconnect sonra olduğunu tooverify **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="81e55-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81e55-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81e55-125">Next steps</span></span>
* <span data-ttu-id="81e55-126">Azure Cosmos DB keşfedin: API MongoDB için [örnekleri](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="81e55-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
