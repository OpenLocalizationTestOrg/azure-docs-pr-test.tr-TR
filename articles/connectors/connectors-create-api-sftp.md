---
title: "aaaLearn nasıl toouse hello mantıksal uygulamalarınızı SFTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooSFTP API toosend bağlanmak ve dosyaları alabilirsiniz. Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="d3ea2-105">Merhaba SFTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d3ea2-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="d3ea2-106">Merhaba SFTP bağlayıcı tooaccess SFTP hesap toosend kullanın ve dosyaları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="d3ea2-107">Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="d3ea2-108">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d3ea2-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea2-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="d3ea2-110">TooSFTP Bağlan</span><span class="sxs-lookup"><span data-stu-id="d3ea2-110">Connect tooSFTP</span></span>
<span data-ttu-id="d3ea2-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d3ea2-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="d3ea2-113">Bir bağlantı tooSFTP oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3ea2-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="d3ea2-114">SFTP tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="d3ea2-114">Use an SFTP trigger</span></span>
<span data-ttu-id="d3ea2-115">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d3ea2-116">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d3ea2-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="d3ea2-117">Bu örnekte, hello **bir dosya eklendiğinde veya SFTP -** tetikleyici olduğunda kullanılan tooinitiate mantığı uygulama iş akışı bir dosya için eklenemez veya bir SFTP sunucusunda, değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="d3ea2-118">Ayrıca, hello yeni veya değiştirilmiş dosyasının Merhaba içeriğine denetler ve içeriğini, hello içeriği kullanmadan önce ayıklanması gereken olduğunu gösteriyorsa karar tooextract hello dosya yapar bir koşul de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="d3ea2-119">Son olarak, bir dosyanın bir eylem tooextract hello içeriğini ekleyin ve ayıklanan hello içeriği hello SFTP sunucusundaki bir klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="d3ea2-120">Kurumsal örnek, bu tetikleyici toomonitor SFTP klasörü müşteri siparişleri temsil eden yeni dosyaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="d3ea2-121">Ardından bir SFTP bağlayıcı eylem gibi kullanabilir **dosya içeriğini almak**, tooget hello içeriği başka bir işleme ve siparişleri veritabanında depolama için hello sırası.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="d3ea2-122">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="d3ea2-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="d3ea2-123">SFTP eylemini kullanın</span><span class="sxs-lookup"><span data-stu-id="d3ea2-123">Use an SFTP action</span></span>
<span data-ttu-id="d3ea2-124">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d3ea2-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d3ea2-125">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d3ea2-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="d3ea2-126">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d3ea2-126">Connector-specific details</span></span>

<span data-ttu-id="d3ea2-127">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="d3ea2-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d3ea2-128">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="d3ea2-128">More connectors</span></span>
<span data-ttu-id="d3ea2-129">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d3ea2-129">Go back toohello [APIs list](apis-list.md).</span></span>
