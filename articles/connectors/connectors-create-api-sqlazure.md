---
title: "Mantıksal uygulamalarınızı Azure SQL Veritabanı Bağlayıcısı ekleme | Microsoft Docs"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="3295a-103">Azure SQL Veritabanı Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3295a-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="3295a-104">Azure SQL Veritabanı Bağlayıcısı'nı kullanarak, tablolardaki verileri yönetmek, kuruluşunuz için iş akışları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3295a-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="3295a-105">SQL Database:</span><span class="sxs-lookup"><span data-stu-id="3295a-105">With SQL Database, you:</span></span>

* <span data-ttu-id="3295a-106">Müşteriler veritabanına yeni bir müşteri ekleyerek veya bir sırada siparişler veritabanını güncelleştirmek, iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3295a-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="3295a-107">Bir satır veri almak, yeni bir satır ekleyin ve hatta silmek için Eylemler kullanın.</span><span class="sxs-lookup"><span data-stu-id="3295a-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="3295a-108">Örneğin, bir kayıt Dynamics CRM Online içinde (tetikleyici) oluşturulduğunda, bir satır bir Azure SQL veritabanı'nda (bir eylem) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3295a-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="3295a-109">Bu konuda, bir mantıksal uygulama SQL Veritabanı Bağlayıcısı'nı kullanmayı gösterir ve ayrıca eylemleri listeler.</span><span class="sxs-lookup"><span data-stu-id="3295a-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="3295a-110">Logic Apps hakkında daha fazla bilgi için bkz: [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3295a-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="3295a-111">Azure SQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="3295a-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="3295a-112">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="3295a-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="3295a-113">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3295a-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="3295a-114">Örneğin, SQL veritabanına bağlanmak için önce bir SQL veritabanı oluşturma *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="3295a-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="3295a-115">Bir bağlantı oluşturmak için normalde bağlandığınız hizmete erişmek için kullandığınız kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="3295a-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="3295a-116">Bu nedenle, SQL veritabanı'nda bağlantı oluşturmak için SQL veritabanı kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="3295a-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="3295a-117">Bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3295a-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="3295a-118">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="3295a-118">Use a trigger</span></span>
<span data-ttu-id="3295a-119">Bu bağlayıcı hiçbir tetikleyici yok.</span><span class="sxs-lookup"><span data-stu-id="3295a-119">This connector does not have any triggers.</span></span> <span data-ttu-id="3295a-120">Bir yineleme tetikleyici, bir HTTP Web kancası tetikleyici, tetikleyici diğer bağlayıcıları ve daha fazla ile kullanılabilir gibi mantıksal uygulamayı başlatmak için diğer Tetikleyicileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3295a-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="3295a-121">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="3295a-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="3295a-122">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="3295a-122">Use an action</span></span>
<span data-ttu-id="3295a-123">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3295a-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="3295a-124">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3295a-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="3295a-125">Artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="3295a-125">Select the plus sign.</span></span> <span data-ttu-id="3295a-126">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya biri **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="3295a-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="3295a-127">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3295a-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="3295a-128">Metin kutusuna, kullanılabilir tüm eylemlerin bir listesini almak için "sql" yazın.</span><span class="sxs-lookup"><span data-stu-id="3295a-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="3295a-129">Bizim örneğimizde seçin **SQL Server - Get satır**.</span><span class="sxs-lookup"><span data-stu-id="3295a-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="3295a-130">Bir bağlantı zaten varsa, ardından **tablo adı** açılan dan listesinde ve girin **satır kimliği** döndürmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="3295a-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="3295a-131">Bağlantı bilgilerini istenirse, bağlantı oluşturmak için ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="3295a-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="3295a-132">[Bağlantı oluşturmak](connectors-create-api-sqlazure.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="3295a-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="3295a-133">Bu örnekte, biz bir tablodan bir satırı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3295a-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="3295a-134">Bu satır verileri görmek için tablodaki alanların kullanarak bir dosya oluşturur başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3295a-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="3295a-135">Örneğin, bulut depolama hesabında yeni bir dosya oluşturmak için adı ve Soyadı alanlarını kullanan bir OneDrive eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3295a-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="3295a-136">**Kaydet** değişikliklerinizi (sol üst köşesindeki araç).</span><span class="sxs-lookup"><span data-stu-id="3295a-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="3295a-137">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3295a-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3295a-138">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="3295a-138">Connector-specific details</span></span>

<span data-ttu-id="3295a-139">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="3295a-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3295a-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3295a-140">Next steps</span></span>
<span data-ttu-id="3295a-141">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3295a-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3295a-142">Logic Apps diğer kullanılabilir bağlayıcılar keşfedin bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3295a-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

