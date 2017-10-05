---
title: "GitHub bağlayıcı Azure Logic Apps içinde | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. GitHub hizmetini barındıran bir web tabanlı Git deposu ' dir. Dağıtılmış değişiklik denetimi ve kaynak kodu Yönetimi (SCM) işlevselliğini Git yanı sıra kendi özellik ekleme tümünün sunar."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="ff20d-105">GitHub Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff20d-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="ff20d-106">GitHub hizmetini barındıran bir web tabanlı Git deposu ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff20d-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="ff20d-107">Dağıtılmış değişiklik denetimi ve kaynak kodu Yönetimi (SCM) işlevselliğini Git yanı sıra kendi özellik ekleme tümünün sunar.</span><span class="sxs-lookup"><span data-stu-id="ff20d-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="ff20d-108">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ff20d-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="ff20d-109">GitHub bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff20d-109">Create a connection to GitHub</span></span>
<span data-ttu-id="ff20d-110">Logic apps ile GitHub oluşturmak için önce oluşturmanız gerekir bir **bağlantı** ardından ayrıntılar için aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="ff20d-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="ff20d-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="ff20d-111">Property</span></span> | <span data-ttu-id="ff20d-112">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff20d-112">Required</span></span> | <span data-ttu-id="ff20d-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff20d-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff20d-114">Belirteç</span><span class="sxs-lookup"><span data-stu-id="ff20d-114">Token</span></span> |<span data-ttu-id="ff20d-115">Evet</span><span class="sxs-lookup"><span data-stu-id="ff20d-115">Yes</span></span> |<span data-ttu-id="ff20d-116">GitHub kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="ff20d-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="ff20d-117">Bağlantı oluşturduktan sonra Eylemler yürütür ve bu makalede açıklanan Tetikleyicileri dinlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff20d-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="ff20d-118">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="ff20d-118">Connector-specific details</span></span>

<span data-ttu-id="ff20d-119">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="ff20d-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ff20d-120">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="ff20d-120">More connectors</span></span>
<span data-ttu-id="ff20d-121">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ff20d-121">Go back to the [APIs list](apis-list.md).</span></span>