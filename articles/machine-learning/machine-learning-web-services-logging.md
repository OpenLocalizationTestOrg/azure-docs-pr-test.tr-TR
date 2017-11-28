---
title: "Machine Learning web hizmetleri için aaaLogging | Microsoft Docs"
description: "Bilgi nasıl tooenable günlüğü için Machine Learning web hizmetleri. Günlük toohelp hello API'leri sorun giderme ek bilgi sağlar."
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
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="5c252-104">Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5c252-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="5c252-105">Bu belge Machine Learning web hizmetlerini yeteneğini günlüğü hello hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c252-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="5c252-106">Günlük yalnızca bir hata numarası ve, Machine Learning API çağrıları toohello gidermenize yardımcı olabilecek bir ileti ötesinde ek bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c252-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="5c252-107">Nasıl bir Web hizmeti için tooenable günlüğü</span><span class="sxs-lookup"><span data-stu-id="5c252-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="5c252-108">Merhaba günlüğe etkinleştirmek [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="5c252-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="5c252-109">Toohello Azure Machine Learning Web Hizmetleri portalında oturum [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="5c252-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="5c252-110">Klasik web hizmeti, ayrıca toohello portal tıklayarak alabilirsiniz **yeni Web Hizmetleri deneyiminizin** Machine Learning Studio'da hello Machine Learning Web Hizmetleri sayfasında.</span><span class="sxs-lookup"><span data-stu-id="5c252-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Yeni Web Hizmetleri deneyiminizin bağlantısı](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="5c252-112">Merhaba üst menü çubuğunda **Web Hizmetleri** için yeni web hizmeti veya tıklatın **Klasik Web Hizmetleri** için Klasik web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="5c252-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Yeni veya Klasik web hizmetleri seçin](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="5c252-114">Yeni bir web hizmeti için hello web hizmeti adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c252-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="5c252-115">Klasik web hizmeti hello web hizmeti adına tıklayın ve hello uygun endpoint hello sonraki sayfada'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5c252-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="5c252-116">Merhaba üst menü çubuğunda **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="5c252-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="5c252-117">Set hello **Enable Logging** çok seçenek*hata* (toolog yalnızca hatalar) veya *tüm* (için tam günlük kaydı).</span><span class="sxs-lookup"><span data-stu-id="5c252-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="5c252-119">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c252-119">Click **Save**.</span></span>

7. <span data-ttu-id="5c252-120">Klasik web hizmetleri için hello oluşturmanız **ml tanılama** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5c252-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="5c252-121">Tüm web hizmeti günlükleri adlı blob kapsayıcısında tutulur **ml tanılama** hello depolama hesabındaki hello web hizmeti ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="5c252-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="5c252-122">Yeni web hizmetleri için bu kapsayıcı hello web hizmetine erişim ilk kez hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5c252-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="5c252-123">Klasik web hizmetleri için zaten yoksa toocreate hello kapsayıcı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c252-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="5c252-124">Merhaba, [Azure portal](https://portal.azure.com)gidin hello web hizmeti ile ilişkili toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="5c252-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="5c252-125">Altında **Blob hizmeti**, tıklatın **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="5c252-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="5c252-126">Varsa hello kapsayıcı **ml tanılama** mevcut değil,'ı tıklatın **+ kapsayıcı**hello kapsayıcı hello adı "ml-Tanılama" verin ve seçin hello **erişim türüne** "Blob" olarak.</span><span class="sxs-lookup"><span data-stu-id="5c252-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="5c252-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c252-127">Click **OK**.</span></span>

      ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="5c252-129">Klasik web hizmeti, hello Web Hizmetleri Pano Machine Learning Studio'da bir geçiş tooenable günlük de vardır.</span><span class="sxs-lookup"><span data-stu-id="5c252-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="5c252-130">Ancak, günlük şimdi hello Web Hizmetleri Portalı aracılığıyla yönetildiğinden dolayı bu makalesinde açıklandığı gibi hello portal üzerinden oturum tooenable gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c252-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="5c252-131">Studio'da oturum zaten etkinleştirilmişse hello Web Hizmetleri portalı, günlüğü devre dışı bırakın ve yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5c252-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="5c252-132">Merhaba etkilerini günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5c252-132">hello effects of enabling logging</span></span>
<span data-ttu-id="5c252-133">Günlük kaydı etkinleştirildiğinde, hello tanılama ve hello web hizmeti uç noktası hatalarından hello kaydedilir **ml tanılama** hello Azure depolama hesabı blob kapsayıcısında hello kullanıcının çalışma ile bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="5c252-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="5c252-134">Bu kapsayıcıdaki tüm hello web hizmeti uç noktaları için bu depolama hesabıyla ilişkili tüm hello çalışma alanları için tüm hello tanılama bilgileri tutar.</span><span class="sxs-lookup"><span data-stu-id="5c252-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="5c252-135">Merhaba günlükleri hello birini çeşitli araçlar kullanılabilir tooexplore Azure Storage hesabını kullanarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="5c252-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="5c252-136">Hello kolay toonavigate toohello depolama hesabında hello Azure portal olması, tıklatın **kapsayıcıları**ve ardından hello kapsayıcı **ml tanılama**.</span><span class="sxs-lookup"><span data-stu-id="5c252-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="5c252-137">Günlük blob ayrıntı bilgileri</span><span class="sxs-lookup"><span data-stu-id="5c252-137">Log blob detail information</span></span>
<span data-ttu-id="5c252-138">Merhaba kapsayıcıdaki her blob tam olarak bir eylemler aşağıdaki hello hello tanılama bilgilerini içerir:</span><span class="sxs-lookup"><span data-stu-id="5c252-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="5c252-139">Merhaba toplu iş yürütme yönteminin yürütülmesi</span><span class="sxs-lookup"><span data-stu-id="5c252-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="5c252-140">Bir yürütme hello istek-yanıt yöntemi</span><span class="sxs-lookup"><span data-stu-id="5c252-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="5c252-141">İstek-yanıt kapsayıcı başlatma</span><span class="sxs-lookup"><span data-stu-id="5c252-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="5c252-142">Her bir blob Hello adını form aşağıdaki hello öneki vardır:</span><span class="sxs-lookup"><span data-stu-id="5c252-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="5c252-143">Burada _oturum türü_ değerleri aşağıdaki hello biridir:</span><span class="sxs-lookup"><span data-stu-id="5c252-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="5c252-144">Toplu işlem</span><span class="sxs-lookup"><span data-stu-id="5c252-144">batch</span></span>  
* <span data-ttu-id="5c252-145">puan/istekleri</span><span class="sxs-lookup"><span data-stu-id="5c252-145">score/requests</span></span>  
* <span data-ttu-id="5c252-146">puan/başlatma</span><span class="sxs-lookup"><span data-stu-id="5c252-146">score/init</span></span>  

