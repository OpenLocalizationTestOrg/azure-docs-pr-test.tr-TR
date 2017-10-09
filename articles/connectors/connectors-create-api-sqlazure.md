---
title: "aaaAdd hello Azure SQL Database mantıksal uygulamalarınızı Connector'daki | Microsoft Docs"
description: "Azure SQL veritabanı bağlayıcı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="faf89-103">Hello Azure SQL Veritabanı Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="faf89-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="faf89-104">Hello Azure SQL Veritabanı Bağlayıcısı'nı kullanarak, tablolardaki verileri yönetmek, kuruluşunuz için iş akışları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="faf89-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="faf89-105">SQL Database:</span><span class="sxs-lookup"><span data-stu-id="faf89-105">With SQL Database, you:</span></span>

* <span data-ttu-id="faf89-106">Yeni bir müşteri tooa müşteriler veritabanı ekleyerek veya bir sırada siparişler veritabanını güncelleştirmek, iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="faf89-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="faf89-107">Eylemler tooget bir veri satırı kullanın, yeni bir satır ekleyin ve hatta silin.</span><span class="sxs-lookup"><span data-stu-id="faf89-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="faf89-108">Örneğin, bir kayıt Dynamics CRM Online içinde (tetikleyici) oluşturulduğunda, bir satır bir Azure SQL veritabanı'nda (bir eylem) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="faf89-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="faf89-109">Bu konuda nasıl toouse hello bir mantıksal uygulama içinde SQL Veritabanı Bağlayıcısı gösterir ve ayrıca listeleri Eylemler hello.</span><span class="sxs-lookup"><span data-stu-id="faf89-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="faf89-110">Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="faf89-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="faf89-111">TooAzure SQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="faf89-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="faf89-112">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="faf89-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="faf89-113">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="faf89-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="faf89-114">Örneğin, tooconnect tooSQL veritabanı, önce bir SQL veritabanı oluşturmanız *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="faf89-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="faf89-115">toocreate bir bağlantı, bağlandığınız tooaccess hello hizmet normalde kullandığınız hello kimlik girin.</span><span class="sxs-lookup"><span data-stu-id="faf89-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="faf89-116">Bu nedenle, SQL veritabanı'nda SQL veritabanı kimlik bilgileri toocreate hello bağlantınızı girin.</span><span class="sxs-lookup"><span data-stu-id="faf89-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="faf89-117">Merhaba bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="faf89-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="faf89-118">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="faf89-118">Use a trigger</span></span>
<span data-ttu-id="faf89-119">Bu bağlayıcı hiçbir tetikleyici yok.</span><span class="sxs-lookup"><span data-stu-id="faf89-119">This connector does not have any triggers.</span></span> <span data-ttu-id="faf89-120">Diğer Tetikleyicileri toostart hello mantıksal uygulama, bir yineleme tetikleyici, bir HTTP Web kancası tetikleyici, tetikleyici diğer bağlayıcıları ve daha fazla ile kullanılabilir gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="faf89-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="faf89-121">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="faf89-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="faf89-122">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="faf89-122">Use an action</span></span>
<span data-ttu-id="faf89-123">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="faf89-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="faf89-124">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="faf89-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="faf89-125">Merhaba artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="faf89-125">Select hello plus sign.</span></span> <span data-ttu-id="faf89-126">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="faf89-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="faf89-127">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="faf89-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="faf89-128">Merhaba metin kutusuna "sql" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.</span><span class="sxs-lookup"><span data-stu-id="faf89-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="faf89-129">Bizim örneğimizde seçin **SQL Server - Get satır**.</span><span class="sxs-lookup"><span data-stu-id="faf89-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="faf89-130">Bir bağlantı zaten varsa, hello seçin **tablo adı** hello açılan dan listesinde ve hello girin **satır kimliği** tooreturn istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="faf89-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="faf89-131">Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="faf89-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="faf89-132">[Merhaba bağlantı oluşturmak](connectors-create-api-sqlazure.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="faf89-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="faf89-133">Bu örnekte, biz bir tablodan bir satırı döndürür.</span><span class="sxs-lookup"><span data-stu-id="faf89-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="faf89-134">Bu satırda toosee hello veri Merhaba tablonun hello alanlarını kullanarak bir dosya oluşturur başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="faf89-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="faf89-135">Örneğin, hello FirstName ve LastName alanları toocreate hello bulut depolama hesabı yeni bir dosyada kullanan bir OneDrive eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="faf89-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="faf89-136">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="faf89-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="faf89-137">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="faf89-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="faf89-138">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="faf89-138">Connector-specific details</span></span>

<span data-ttu-id="faf89-139">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="faf89-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="faf89-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="faf89-140">Next steps</span></span>
<span data-ttu-id="faf89-141">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="faf89-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="faf89-142">Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="faf89-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

