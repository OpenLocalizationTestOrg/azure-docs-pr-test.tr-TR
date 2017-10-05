---
title: "My Web işi projesinin ne (Visual Studio Azure depolama bağlı hizmeti)? | Microsoft Belgeleri"
description: "Visual Studio kullanarak bir depolama hesabına bağlanma Hizmetleri bağlandıktan sonra bir Azure Web işi projesi ne açıklar"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="152ad-104">My Web işi projesinin ne (Visual Studio Azure depolama bağlı hizmeti)?</span><span class="sxs-lookup"><span data-stu-id="152ad-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="152ad-105">Eklenen başvuruları</span><span class="sxs-lookup"><span data-stu-id="152ad-105">References Added</span></span>
<span data-ttu-id="152ad-106">Azure depolama NuGet paketini eklenecek veya Visual Studio projenizde güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="152ad-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="152ad-107">Bu paket aşağıdaki .NET başvuru ekler:</span><span class="sxs-lookup"><span data-stu-id="152ad-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="152ad-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="152ad-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="152ad-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="152ad-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="152ad-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="152ad-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="152ad-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="152ad-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="152ad-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="152ad-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="152ad-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="152ad-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="152ad-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="152ad-114">**System.Data**</span></span>
* <span data-ttu-id="152ad-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="152ad-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="152ad-116">Azure eklenen depolama alanı için bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="152ad-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="152ad-117">Projenizin App.config dosyasında **AzureWebJobsStorage** ve **AzureWebJobsDashboard** girişleri, seçilen depolama hesabı bağlantı dizesi ve anahtarı ile güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="152ad-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="152ad-118">Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="152ad-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

