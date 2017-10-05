---
title: "Wunderlist bağlayıcı ı n Azure mantıksal uygulamaları | Microsoft Docs"
description: "Wunderlist bağlantı oluşturun ve mantıksal uygulamalar iş akışınızda oluşturmak için bu bağlantıyı kullanın."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="2ba38-103">Wunderlist Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2ba38-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="2ba38-104">Wunderlist bitti kendi öğe alma kişilerin yardımcı olmak üzere bir Yapılacaklar listesi ve Görev Yöneticisi'ni sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2ba38-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="2ba38-105">Loved bir Market listesini paylaşımı olup bir proje üzerinde çalışırken ya da bir tatil planlaması Wunderlist yakalama, paylaşma ve, to¬dos tamamlamak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2ba38-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="2ba38-106">Tüm Görevler yerden erişebilmeniz için Wunderlist anında telefon, tablet ve bilgisayar arasında eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="2ba38-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="2ba38-107">Bir mantıksal uygulama artık oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2ba38-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="2ba38-108">Wunderlist bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ba38-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="2ba38-109">Logic apps ile Wunderlist oluşturmak için önce oluşturmanız gerekir bir **bağlantı** ardından ayrıntılar için aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="2ba38-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="2ba38-110">Özellik</span><span class="sxs-lookup"><span data-stu-id="2ba38-110">Property</span></span> | <span data-ttu-id="2ba38-111">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ba38-111">Required</span></span> | <span data-ttu-id="2ba38-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ba38-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ba38-113">Belirteç</span><span class="sxs-lookup"><span data-stu-id="2ba38-113">Token</span></span> |<span data-ttu-id="2ba38-114">Evet</span><span class="sxs-lookup"><span data-stu-id="2ba38-114">Yes</span></span> |<span data-ttu-id="2ba38-115">Wunderlist kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="2ba38-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="2ba38-116">Bağlantı oluşturduktan sonra Eylemler yürütür ve Tetikleyicileri dinlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ba38-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="2ba38-117">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2ba38-117">Connector-specific details</span></span>

<span data-ttu-id="2ba38-118">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="2ba38-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2ba38-119">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="2ba38-119">More connectors</span></span>
<span data-ttu-id="2ba38-120">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2ba38-120">Go back to the [APIs list](apis-list.md).</span></span>