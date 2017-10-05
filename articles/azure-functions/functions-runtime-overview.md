---
title: "Azure işlevleri çalışma zamanına genel bakış | Microsoft Docs"
description: "Azure işlevleri çalışma zamanı önizlemesi genel bakış"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="f7176-103">Azure işlevleri çalışma zamanına genel bakış</span><span class="sxs-lookup"><span data-stu-id="f7176-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="f7176-104">Azure işlevleri çalışma zamanı programlama modeli şirket içi kolaylık ve esneklik Azure işlevlerinin yararlanacak yeni bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7176-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="f7176-105">Azure işlevleri olarak aynı açık kaynak kökleri yerleşik olarak, dağıtılmış bir bulut hizmeti olarak neredeyse aynı geliştirme deneyimi sağlamak için şirket içi Azure işlevleri çalışma zamanı olur.</span><span class="sxs-lookup"><span data-stu-id="f7176-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Azure işlevleri çalışma zamanı Önizleme portalı][1]

<span data-ttu-id="f7176-107">Azure işlevleri çalışma zamanı buluta kaydetmeden önce Azure işlevleri deneyimi bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7176-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="f7176-108">Geçirdiğinizde bu şekilde, oluşturacağınız kod varlıklarına sonra sizinle buluta alınabilir.</span><span class="sxs-lookup"><span data-stu-id="f7176-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="f7176-109">Toplu işlemler günde çalıştırmak için şirket içi bilgisayarları yedek işlem gücünü kullanma gibi yeni seçeneklerini, çalışma zamanı da açılır.</span><span class="sxs-lookup"><span data-stu-id="f7176-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="f7176-110">Koşullu başka sistemlere, hem şirket içi ve buluttaki veri göndermek için kuruluşunuz içinde cihazları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7176-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="f7176-111">Azure işlevleri çalışma zamanı iki parça oluşur:</span><span class="sxs-lookup"><span data-stu-id="f7176-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="f7176-112">Azure işlevleri çalışma zamanı Yönetimi rolü</span><span class="sxs-lookup"><span data-stu-id="f7176-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="f7176-113">Azure işlevleri çalışma zamanı çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="f7176-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="f7176-114">Azure işlevleri Yönetimi rolü</span><span class="sxs-lookup"><span data-stu-id="f7176-114">Azure Functions Management Role</span></span>

<span data-ttu-id="f7176-115">Azure işlevleri yönetim rolü işlevleri şirket içi yönetim için bir konak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7176-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="f7176-116">Bu rol, aşağıdaki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f7176-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="f7176-117">Azure işlevleri yönetim olan Portalı'nın, barındırma aynı gördüğünüz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7176-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f7176-118">Bu, Azure portalında gibi aynı şekilde işlevlerinizi geliştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f7176-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="f7176-119">İşlevler arasında birden çok işlevleri Worker dağıtma.</span><span class="sxs-lookup"><span data-stu-id="f7176-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="f7176-120">Microsoft Visual Studio, işlevleri doğrudan yayımlaması yayımlama bir uç noktası sağlama.</span><span class="sxs-lookup"><span data-stu-id="f7176-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="f7176-121">Azure işlevleri çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="f7176-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="f7176-122">Azure işlevleri çalışan rolleri Windows kapsayıcılarında dağıtılır ve bu işlev kodunuzu nereye yürütür.</span><span class="sxs-lookup"><span data-stu-id="f7176-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="f7176-123">Birden çok çalışan rolleri kuruluşunuz genelinde dağıtabilirsiniz ve müşteriler hale getirebilir anahtar şekilde yedek işlem gücünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="f7176-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="f7176-124">En düşük gereksinimler</span><span class="sxs-lookup"><span data-stu-id="f7176-124">Minimum Requirements</span></span>

<span data-ttu-id="f7176-125">Azure işlevleri çalışma zamanı ile çalışmaya başlamak için bir makine olmalıdır **Windows Server 2016 veya Windows 10 oluşturucuları Update** erişimi olan bir **SQL Server** örneği.</span><span class="sxs-lookup"><span data-stu-id="f7176-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7176-126">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f7176-126">Next Steps</span></span>

<span data-ttu-id="f7176-127">Yükleme [Azure işlevleri çalışma zamanı Önizleme](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="f7176-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
