---
title: "aaaCreate azure'da bir zamanlamaya göre çalışan bir işlev | Microsoft Docs"
description: "Nasıl toocreate çalıştıran Azure işlevinde tanımladığınız bir zamanlamaya göre öğrenin."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="b2aaf-103">Azure’da bir zamanlayıcı tarafından tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2aaf-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="b2aaf-104">Nasıl toouse Azure işlevleri toocreate çalıştırılan bir işlevi tanımladığınız bir zamanlamaya bağlı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Hello Azure portal işlev uygulaması oluşturma](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="b2aaf-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b2aaf-106">Prerequisites</span></span>

<span data-ttu-id="b2aaf-107">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="b2aaf-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="b2aaf-108">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="b2aaf-109">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2aaf-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="b2aaf-111">Ardından, hello yeni işlev uygulamada bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="b2aaf-112">Zamanlayıcı ile tetiklenen işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2aaf-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="b2aaf-113">Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="b2aaf-114">Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="b2aaf-115">Merhaba eksiksiz işlev şablonları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-115">This displays hello complete set of function templates.</span></span>

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="b2aaf-117">Select hello **TimerTrigger** istediğiniz dili için şablon.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="b2aaf-118">Ardından hello tabloda belirtildiği gibi hello ayarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b2aaf-118">Then use hello settings as specified in hello table:</span></span>

    ![Zamanlayıcı tetiklenen bir işlev hello Azure portal oluşturun.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="b2aaf-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="b2aaf-120">Setting</span></span> | <span data-ttu-id="b2aaf-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="b2aaf-121">Suggested value</span></span> | <span data-ttu-id="b2aaf-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2aaf-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="b2aaf-123">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="b2aaf-123">**Name your function**</span></span> | <span data-ttu-id="b2aaf-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="b2aaf-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="b2aaf-125">Tetiklenen Zamanlayıcı işlevinizin Hello adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="b2aaf-126">**[Zamanlama](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="b2aaf-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="b2aaf-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="b2aaf-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="b2aaf-128">Altı alan [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression) , işlevi toorun dakikada zamanlar.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="b2aaf-129">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-129">Click **Create**.</span></span> <span data-ttu-id="b2aaf-130">Seçtiğiniz dilde her dakika çalışan bir işlev oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="b2aaf-131">Yürütme toohello günlüklerine yazılmış izleme bilgilerini görüntüleyerek doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![İşlevler Görüntüleyicisi hello Azure portalında oturum açın.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="b2aaf-133">Şimdi, böylece daha az sıklıkta saatte gibi çalışır hello işlevin zamanlamasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="b2aaf-134">Güncelleştirme hello Zamanlayıcı zamanlaması</span><span class="sxs-lookup"><span data-stu-id="b2aaf-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="b2aaf-135">İşlevinizi genişletin ve **Tümleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="b2aaf-136">Bu, giriş tanımlayın ve bağlamaları işlevi için çıktı ve hello ayarlamaktır yerdir.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="b2aaf-137">`0 0 */1 * * *` şeklinde yeni bir **Zamanlama** değeri girin ve **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![İşlevler hello Azure portal Zamanlayıcı zamanlamada güncelleştirin.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="b2aaf-139">Saatte bir çalışan bir işleviniz oldu.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="b2aaf-140">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="b2aaf-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="b2aaf-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2aaf-141">Next steps</span></span>

<span data-ttu-id="b2aaf-142">Bir zamanlamaya göre çalışan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b2aaf-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="b2aaf-143">Zamanlayıcı tetikleyicileri hakkında daha fazla bilgi edinmek için bkz. [Azure İşlevleri ile kod yürütme zamanlama](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="b2aaf-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>