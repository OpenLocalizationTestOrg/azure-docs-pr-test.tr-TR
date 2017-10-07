---
title: "aaaCreate hello Azure Portal işlevi uygulamadan | Microsoft Docs"
description: "Yeni bir işlev uygulaması Azure App Service'te hello portalından oluşturun."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="7c711-103">Azure portal hello bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c711-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="7c711-104">Azure işlev uygulamalarının hello Azure App Service altyapısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7c711-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="7c711-105">Bu konu, nasıl gösterir toocreate hello Azure portal'ın bir işlev uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7c711-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="7c711-106">Bir işlev uygulaması tekil işlevler hello yürütülmesi barındıran hello kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7c711-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="7c711-107">Bir işlev uygulaması hello App Service barındırma planı oluşturduğunuzda, işlevi uygulamanızı App Service tüm hello özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c711-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="7c711-108">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c711-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="7c711-109">Bir işlev uygulaması oluşturduğunuzda, geçerli bir tedarik **uygulama adı**, hangi içerebilir yalnızca harf, rakam ve kısa çizgi.</span><span class="sxs-lookup"><span data-stu-id="7c711-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="7c711-110">Alt çizgi (**_**) izin verilen bir karakter değildir.</span><span class="sxs-lookup"><span data-stu-id="7c711-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="7c711-111">Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7c711-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="7c711-112">Depolama hesabınızın adının Azure içinde benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c711-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="7c711-113">Merhaba işlevi uygulama oluşturulduktan sonra bir veya daha fazla farklı dillerde tekil işlevler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c711-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="7c711-114">İşlevler Oluştur [hello portalını kullanarak](functions-create-first-azure-function.md#create-function), [sürekli dağıtım](functions-continuous-deployment.md), ya da [FTP ile karşıya](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="7c711-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="7c711-115">Hizmet planları</span><span class="sxs-lookup"><span data-stu-id="7c711-115">Service plans</span></span>

<span data-ttu-id="7c711-116">Azure işlevleri sahip iki farklı hizmet planları: Tüketim planlama ve uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="7c711-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="7c711-117">kod çalışmadığı zaman, kodunuzu, Ölçek genişletme gerekli toohandle yükü olarak ve ardından ölçekler bileşenini çalışırken hello tüketim planı otomatik olarak işlem gücü ayırır.</span><span class="sxs-lookup"><span data-stu-id="7c711-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="7c711-118">Uygulama hizmeti planı Hello işlevinizi uygulama erişim tooall hello tesis App Service'in sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c711-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="7c711-119">İşlev uygulamanızı oluşturulur ve şu anda değiştirilemez, hizmeti planınızı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c711-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="7c711-120">Daha fazla bilgi için bkz: [barındırma planı bir Azure işlevleri arasından seçim](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7c711-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="7c711-121">Bir uygulama hizmeti planı toorun JavaScript işlevleri planlıyorsanız, daha az çekirdek planla seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c711-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="7c711-122">Daha fazla bilgi için bkz: Merhaba [işlevleri için JavaScript başvurusu](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="7c711-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="7c711-123">Depolama hesabı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="7c711-123">Storage account requirements</span></span>

<span data-ttu-id="7c711-124">Bir işlev uygulaması App Service'te oluştururken oluşturmanız veya Blob, kuyruk ve tablo depolama destekleyen tooa genel amaçlı Azure depolama hesabı bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c711-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="7c711-125">Dahili olarak, işlevlerini kullanan depolama Tetikleyicileri yönetme ve işlev yürütmeleri günlüğü gibi işlemler için.</span><span class="sxs-lookup"><span data-stu-id="7c711-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="7c711-126">Bazı depolama hesapları, kuyruklar ve tablolar, yalnızca blob storage hesapları, Azure Premium Storage ve ZRS çoğaltma genel amaçlı depolama hesaplarıyla gibi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="7c711-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="7c711-127">Bu hesapları dışı hello depolama hesabı dikey penceresinden bir işlev uygulaması oluştururken filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="7c711-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="7c711-128">Hello tüketim barındırma planı kullanırken, işlevi kod ve bağlama yapılandırma dosyaları Azure File storage hello ana depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7c711-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="7c711-129">Merhaba ana depolama hesabını sildiğinizde, bu içeriği silinir ve kurtarılamaz.</span><span class="sxs-lookup"><span data-stu-id="7c711-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="7c711-130">Depolama hesabı türleri hakkında daha fazla toolearn bkz [hello Azure Storage hizmetlerine giriş](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="7c711-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c711-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c711-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



