---
title: "Logic apps içinde SFTP Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. Dosya gönderme ve alma için SFTP API'sine bağlayın. Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="c8b87-105">SFTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c8b87-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="c8b87-106">Dosya gönderme ve alma için bir SFTP hesaba erişmek için SFTP Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b87-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="c8b87-107">Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b87-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="c8b87-108">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8b87-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="c8b87-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8b87-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="c8b87-110">SFTP için Bağlan</span><span class="sxs-lookup"><span data-stu-id="c8b87-110">Connect to SFTP</span></span>
<span data-ttu-id="c8b87-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="c8b87-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="c8b87-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8b87-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="c8b87-113">SFTP bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8b87-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="c8b87-114">SFTP tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="c8b87-114">Use an SFTP trigger</span></span>
<span data-ttu-id="c8b87-115">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="c8b87-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c8b87-116">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c8b87-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="c8b87-117">Bu örnekte, **bir dosya eklendiğinde veya SFTP -** tetikleyici için bir dosya eklendiğinde mantığı uygulama iş akışını başlatmak için kullanılan veya bir SFTP sunucusunda, değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="c8b87-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="c8b87-118">Ayrıca, yeni veya değiştirilmiş dosyasının içeriğini denetler ve içeriğini, içeriği kullanmadan önce ayıklanması gereken olduğunu gösteriyorsa dosyasını ayıklamak için bir karar verir bir koşul de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8b87-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="c8b87-119">Son olarak, bir dosyanın içeriğini ayıklamak için bir eylem ekleyin ve ayıklanan içeriğin SFTP sunucu üzerindeki bir klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8b87-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="c8b87-120">Bir kurumsal örnekte, bu tetikleyici müşteri siparişleri temsil eden yeni dosyalar için bir SFTP klasörü izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b87-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="c8b87-121">Ardından bir SFTP bağlayıcı eylem gibi kullanabilir **alma dosya içeriğini**, siparişler veritabanında daha fazla işleme ve depolama sipariş içeriğini almak için.</span><span class="sxs-lookup"><span data-stu-id="c8b87-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="c8b87-122">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="c8b87-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="c8b87-123">SFTP eylemini kullanın</span><span class="sxs-lookup"><span data-stu-id="c8b87-123">Use an SFTP action</span></span>
<span data-ttu-id="c8b87-124">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c8b87-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c8b87-125">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c8b87-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="c8b87-126">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c8b87-126">Connector-specific details</span></span>

<span data-ttu-id="c8b87-127">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="c8b87-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c8b87-128">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="c8b87-128">More connectors</span></span>
<span data-ttu-id="c8b87-129">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c8b87-129">Go back to the [APIs list](apis-list.md).</span></span>