---
title: "Machine Learning web hizmetleri için günlüğe kaydetme | Microsoft Docs"
description: "Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirmek öğrenin. Günlük API'leri gidermenize yardımcı olacak ek bilgiler sağlar."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="b0bab-104">Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b0bab-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="b0bab-105">Bu belgede, Machine Learning web hizmetleri günlüğe kaydetme özelliği bilgiler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0bab-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="b0bab-106">Günlük yalnızca bir hata numarası ve Machine Learning API'ları aramalarınız gidermenize yardımcı olabilecek bir ileti ötesinde ek bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0bab-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="b0bab-107">Bir Web hizmeti için günlük kaydını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b0bab-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="b0bab-108">Gelen günlük kaydını etkinleştir [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="b0bab-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="b0bab-109">Oturum açtığınızda Azure Machine Learning Web Hizmetleri portalında [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="b0bab-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="b0bab-110">Klasik web hizmeti, ayrıca Portalı'na tıklayarak alabilirsiniz **yeni Web Hizmetleri deneyiminizin** Machine Learning Studio'da Machine Learning Web Hizmetleri sayfasında.</span><span class="sxs-lookup"><span data-stu-id="b0bab-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Yeni Web Hizmetleri deneyiminizin bağlantısı](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="b0bab-112">Üst menü çubuğunda **Web Hizmetleri** için yeni web hizmeti veya tıklatın **Klasik Web Hizmetleri** için Klasik web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b0bab-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Yeni veya Klasik web hizmetleri seçin](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="b0bab-114">İçin yeni bir web hizmeti, web hizmeti adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0bab-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="b0bab-115">Klasik web hizmeti, web hizmeti adına tıklayın ve uygun endpoint sonraki sayfada'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b0bab-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="b0bab-116">Üst menü çubuğunda **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b0bab-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="b0bab-117">Ayarlama **Enable Logging** için seçenek *hata* (yalnızca hataları günlüğe kaydetmek için) veya *tüm* (için tam günlük kaydı).</span><span class="sxs-lookup"><span data-stu-id="b0bab-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="b0bab-119">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0bab-119">Click **Save**.</span></span>

7. <span data-ttu-id="b0bab-120">Klasik web hizmetleri için oluşturmanız **ml tanılama** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b0bab-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="b0bab-121">Tüm web hizmeti günlükleri adlı blob kapsayıcısında tutulur **ml tanılama** web hizmeti ile ilişkili depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="b0bab-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="b0bab-122">Yeni web hizmetleri için bu kapsayıcı web hizmetine erişim ilk kez oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b0bab-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="b0bab-123">Klasik web hizmetleri için zaten yoksa kapsayıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0bab-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="b0bab-124">İçinde [Azure portal](https://portal.azure.com), web hizmeti ile ilişkilendirilmiş depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="b0bab-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="b0bab-125">Altında **Blob hizmeti**, tıklatın **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="b0bab-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="b0bab-126">Varsa kapsayıcı **ml tanılama** mevcut değil, tıklatın **+ kapsayıcı**, kapsayıcı "ml-Tanılama" ad verin ve seçin **erişim türüne** "Blob" olarak.</span><span class="sxs-lookup"><span data-stu-id="b0bab-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="b0bab-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0bab-127">Click **OK**.</span></span>

      ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="b0bab-129">Klasik web hizmeti, Machine Learning Studio Web Hizmetleri panosunda da günlüğe kaydetmeyi etkinleştirmek için bir anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="b0bab-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="b0bab-130">Ancak, günlük kaydı Web Hizmetleri Portalı aracılığıyla şimdi yönetildiğinden, bu makalede anlatıldığı gibi günlüğe kaydetme portalı üzerinden etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0bab-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="b0bab-131">Studio'da oturum zaten etkinleştirilmişse Web Hizmetleri Portalı'nda günlüğü devre dışı bırakın ve yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b0bab-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="b0bab-132">Günlüğü etkinleştirme etkileri</span><span class="sxs-lookup"><span data-stu-id="b0bab-132">The effects of enabling logging</span></span>
<span data-ttu-id="b0bab-133">Günlük kaydı etkinleştirildiğinde tanılama ve web hizmeti uç noktası hatalarından oturum **ml tanılama** Azure depolama hesabı blob kapsayıcısında kullanıcının çalışma alanıyla bağlı.</span><span class="sxs-lookup"><span data-stu-id="b0bab-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="b0bab-134">Bu kapsayıcıdaki tüm web hizmeti uç noktaları için bu depolama hesabıyla ilişkili tüm çalışma alanları için tüm tanılama bilgileri tutar.</span><span class="sxs-lookup"><span data-stu-id="b0bab-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="b0bab-135">Günlükleri, herhangi bir Azure depolama hesabı keşfetmek kullanılabilen çeşitli araçlar kullanılarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="b0bab-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="b0bab-136">Daha kolay olabilir Azure Portal'da depolama hesabı gitmek için **kapsayıcıları**ve kapsayıcı ardından **ml tanılama**.</span><span class="sxs-lookup"><span data-stu-id="b0bab-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="b0bab-137">Günlük blob ayrıntı bilgileri</span><span class="sxs-lookup"><span data-stu-id="b0bab-137">Log blob detail information</span></span>
<span data-ttu-id="b0bab-138">Her bir blob kapsayıcısında tanılama bilgileri için aşağıdaki eylemleri tam olarak birine tutar:</span><span class="sxs-lookup"><span data-stu-id="b0bab-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="b0bab-139">Bir toplu iş yürütme yönteminin yürütülmesi</span><span class="sxs-lookup"><span data-stu-id="b0bab-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="b0bab-140">İstek-yanıt yönteminin bir yürütme</span><span class="sxs-lookup"><span data-stu-id="b0bab-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="b0bab-141">İstek-yanıt kapsayıcı başlatma</span><span class="sxs-lookup"><span data-stu-id="b0bab-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="b0bab-142">Her bir blob adı ön eki aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b0bab-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="b0bab-143">Burada _oturum türü_ aşağıdaki değerlerden biri:</span><span class="sxs-lookup"><span data-stu-id="b0bab-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="b0bab-144">Toplu işlem</span><span class="sxs-lookup"><span data-stu-id="b0bab-144">batch</span></span>  
* <span data-ttu-id="b0bab-145">puan/istekleri</span><span class="sxs-lookup"><span data-stu-id="b0bab-145">score/requests</span></span>  
* <span data-ttu-id="b0bab-146">puan/başlatma</span><span class="sxs-lookup"><span data-stu-id="b0bab-146">score/init</span></span>  

