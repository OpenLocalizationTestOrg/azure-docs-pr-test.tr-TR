---
title: "aaaAzure işlevleri çalışma zamanına genel bakış | Microsoft Docs"
description: "Hello Azure işlevleri çalışma zamanı önizlemesi genel bakış"
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
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="6ae81-103">Azure işlevleri çalışma zamanına genel bakış</span><span class="sxs-lookup"><span data-stu-id="6ae81-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="6ae81-104">Hello Azure işlevleri çalışma zamanı programlama modeli şirket içi, tootake avantajlarından hello kolaylık ve esneklik hello Azure işlevlerinin için yeni bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="6ae81-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="6ae81-105">Azure işlevleri, Azure işlevleri çalışma zamanı olduğu gibi neredeyse aynı geliştirme deneyimi hello bulut hizmeti olarak şirket içinde dağıtılabilir tooprovide hello üzerinde oluşturulmuş aynı kaynak kökleri açın.</span><span class="sxs-lookup"><span data-stu-id="6ae81-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Azure işlevleri çalışma zamanı Önizleme portalı][1]

<span data-ttu-id="6ae81-107">Hello Azure işlevleri çalışma zamanı toohello bulut kaydetmeden önce bir yol, tooexperience Azure işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ae81-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="6ae81-108">Geçirdiğinizde bu şekilde, oluşturacağınız hello kod varlıklarına sonra toohello bulutla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="6ae81-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="6ae81-109">Örneğin, şirket içi bilgisayarları toorun toplu işlemler hello yedek işlem gücünü günde kullanarak yeni seçeneklerini, Hello çalışma zamanı da açılır.</span><span class="sxs-lookup"><span data-stu-id="6ae81-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="6ae81-110">Cihazlar, kuruluş tooconditionally gönderme veri tooother sistemlerinizi, hem şirket içinde ve hello bulutta de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ae81-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="6ae81-111">Hello Azure işlevleri çalışma zamanı iki parça oluşur:</span><span class="sxs-lookup"><span data-stu-id="6ae81-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="6ae81-112">Azure işlevleri çalışma zamanı Yönetimi rolü</span><span class="sxs-lookup"><span data-stu-id="6ae81-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="6ae81-113">Azure işlevleri çalışma zamanı çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="6ae81-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="6ae81-114">Azure işlevleri Yönetimi rolü</span><span class="sxs-lookup"><span data-stu-id="6ae81-114">Azure Functions Management Role</span></span>

<span data-ttu-id="6ae81-115">Hello Azure işlevleri yönetim rolü işlevleri şirket içi hello yönetimi için bir konak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ae81-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="6ae81-116">Bu rolü hello aşağıdaki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="6ae81-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="6ae81-117">Merhaba hello olan Azure işlevleri Yönetim Portalı barındırma, hello hello gördüğünüz aynı [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6ae81-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6ae81-118">Şekilde hello Azure portalı gibi bu sağlar, işlevlerde geliştirmek aynı hello.</span><span class="sxs-lookup"><span data-stu-id="6ae81-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="6ae81-119">İşlevler arasında birden çok işlevleri Worker dağıtma.</span><span class="sxs-lookup"><span data-stu-id="6ae81-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="6ae81-120">Microsoft Visual Studio, işlevleri doğrudan yayımlaması yayımlama bir uç noktası sağlama.</span><span class="sxs-lookup"><span data-stu-id="6ae81-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="6ae81-121">Azure işlevleri çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="6ae81-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="6ae81-122">Hello Azure işlevleri çalışan rolleri Windows kapsayıcılarında dağıtılır ve bu işlev kodunuzu nereye yürütür.</span><span class="sxs-lookup"><span data-stu-id="6ae81-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="6ae81-123">Birden çok çalışan rolleri kuruluşunuz genelinde dağıtabilirsiniz ve müşteriler hale getirebilir anahtar şekilde yedek işlem gücünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ae81-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="6ae81-124">En düşük gereksinimler</span><span class="sxs-lookup"><span data-stu-id="6ae81-124">Minimum Requirements</span></span>

<span data-ttu-id="6ae81-125">hello Azure işlevleri sahip bir makine olmalıdır çalışma zamanı ile çalışmaya tooget **Windows Server 2016 veya Windows 10 oluşturucuları Update** erişim tooa ile **SQL Server** örneği.</span><span class="sxs-lookup"><span data-stu-id="6ae81-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ae81-126">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6ae81-126">Next Steps</span></span>

<span data-ttu-id="6ae81-127">Merhaba yüklemek [Azure işlevleri çalışma zamanı Önizleme](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="6ae81-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
