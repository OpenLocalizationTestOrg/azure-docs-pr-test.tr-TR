---
title: My bulut hizmeti projesini ne oldu? | Microsoft Belgeleri
description: "Visual Studio kullanarak bir Azure depolama hesabına bağlanma Hizmetleri bağlandıktan sonra bulut Hizmetleri projede ne olacağını açıklar"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 4c9de56f6daf07097c0f593db37d14dce3bce05f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="14e9c-104">Bulut Hizmetleri proje için ne (Visual Studio Azure depolama bağlı hizmeti)?</span><span class="sxs-lookup"><span data-stu-id="14e9c-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="14e9c-105">Eklenen başvuruları</span><span class="sxs-lookup"><span data-stu-id="14e9c-105">References added</span></span>
<span data-ttu-id="14e9c-106">Azure depolama NuGet paketini Visual Studio projenizi eklendi.</span><span class="sxs-lookup"><span data-stu-id="14e9c-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="14e9c-107">Bu paket aşağıdaki .NET başvuru ekler:</span><span class="sxs-lookup"><span data-stu-id="14e9c-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="14e9c-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="14e9c-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="14e9c-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="14e9c-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="14e9c-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="14e9c-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="14e9c-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="14e9c-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="14e9c-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="14e9c-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="14e9c-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="14e9c-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="14e9c-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="14e9c-114">**System.Data**</span></span>
* <span data-ttu-id="14e9c-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="14e9c-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="14e9c-116">Azure eklenen depolama alanı için bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="14e9c-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="14e9c-117">Öğeleri seçilen depolama hesabı bağlantı dizesi ve anahtar ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="14e9c-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="14e9c-118">Aşağıdaki dosyalar için yapılan değişiklikler:</span><span class="sxs-lookup"><span data-stu-id="14e9c-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="14e9c-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="14e9c-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="14e9c-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="14e9c-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="14e9c-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="14e9c-121">**ServiceConfiguration.Local.cscfg**</span></span>

