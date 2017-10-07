---
title: "Machine Learning çalışma alanı aaaManage | Microsoft Docs"
description: "Erişim tooAzure Machine Learning çalışma alanlarını, yönetmek ve dağıtmak ve ML API web hizmetleri yönetme"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="f2fde-103">Bir Azure Machine Learning çalışma alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="f2fde-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="f2fde-104">Web Hizmetleri hello Machine Learning Web Hizmetleri portalında yönetme hakkında daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f2fde-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="f2fde-105">Machine Learning çalışma alanlarında ya da hello Azure portalında yönetmek ya da Klasik Azure portalı hello.</span><span class="sxs-lookup"><span data-stu-id="f2fde-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="f2fde-106">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="f2fde-106">Use hello Azure portal</span></span>

<span data-ttu-id="f2fde-107">toomanage hello Azure portal çalışma:</span><span class="sxs-lookup"><span data-stu-id="f2fde-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="f2fde-108">İçinde toohello oturum [Azure portal](https://portal.azure.com/) Azure aboneliği yönetici hesabı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f2fde-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="f2fde-109">"Machine learning çalışma alanları" Merhaba arama kutusuna hello sayfanın üst kısmındaki hello girin ve ardından **Machine Learning çalışma alanları**.</span><span class="sxs-lookup"><span data-stu-id="f2fde-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="f2fde-110">Merhaba çalışma toomanage istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="f2fde-111">Ayrıca toohello standart kaynak yönetimi bilgilerini ve kullanılabilir seçenekler, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f2fde-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="f2fde-112">Görünüm **özellikleri** - hello çalışma ve kaynak bilgileri bu sayfada görüntülenir ve hello abonelik ve bu çalışma alanı ile bağlı olduğu kaynak grubu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fde-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="f2fde-113">**Depolama anahtarlarını yeniden eşitleme** -hello çalışma anahtarları toohello depolama hesabı korur.</span><span class="sxs-lookup"><span data-stu-id="f2fde-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="f2fde-114">Merhaba depolama hesabı anahtarları değişiklikleri sonra tıklayabilirsiniz **anahtarları yeniden eşitleme** hello çalışma toosynchronize hello anahtarları.</span><span class="sxs-lookup"><span data-stu-id="f2fde-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="f2fde-115">Bu çalışma alanıyla ilişkili toomanage hello web hizmetleri hello Machine Learning Web Hizmetleri portalı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="f2fde-116">Bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md) tam bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f2fde-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fde-117">toodeploy, atanmalıdır katkıda bulunan yeni web hizmetleri yönetmek veya yönetici rolü hello abonelik toowhich hello web hizmeti üzerinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="f2fde-118">Başka bir kullanıcı tooa machine learning çalışma alanı davet etmek, dağıtmak veya web hizmetleri yönetmek için önce bunları hello abonelik tooa katkıda bulunan veya yönetici rolü atamalısınız.</span><span class="sxs-lookup"><span data-stu-id="f2fde-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="f2fde-119">Erişim izinlerini ayarlama hakkında daha fazla bilgi için bkz: [hello Azure portal - genel Önizleme alanındaki kullanıcılar ve gruplar için erişim atamalarını görüntüle](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="f2fde-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="f2fde-120">Merhaba Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="f2fde-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="f2fde-121">Merhaba Klasik Azure Portalı'nı kullanarak, Machine Learning çalışma alanlarına yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f2fde-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="f2fde-122">Merhaba çalışma nasıl kullanıldığını izleyin</span><span class="sxs-lookup"><span data-stu-id="f2fde-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="f2fde-123">Merhaba çalışma tooallow yapılandırmak veya erişim engelle</span><span class="sxs-lookup"><span data-stu-id="f2fde-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="f2fde-124">Merhaba çalışma alanında oluşturulan Web Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f2fde-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="f2fde-125">Merhaba çalışma silin</span><span class="sxs-lookup"><span data-stu-id="f2fde-125">Delete hello workspace</span></span>

<span data-ttu-id="f2fde-126">Ayrıca, hello Pano sekmesi çalışma kullanımınızı genel bir bakış ve çalışma bilgilerinizin hızlı bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2fde-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="f2fde-127">Merhaba üzerinde Azure Machine Learning Studio'da **WEB Hizmetleri** sekmesinde, ekleyebilir, güncelleştirmek veya bir Machine Learning Web hizmetini silin.</span><span class="sxs-lookup"><span data-stu-id="f2fde-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="f2fde-128">toomanage hello Klasik Azure portalı çalışma:</span><span class="sxs-lookup"><span data-stu-id="f2fde-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="f2fde-129">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Microsoft Azure kullanarak hesap - hello Azure aboneliği ile ilişkili hello hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="f2fde-130">Merhaba Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="f2fde-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="f2fde-131">Merhaba çalışma toomanage istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="f2fde-132">Merhaba çalışma sayfası, üç sekme içerir:</span><span class="sxs-lookup"><span data-stu-id="f2fde-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="f2fde-133">**PANO** -tooview çalışma kullanım ve bilgileri sağlar</span><span class="sxs-lookup"><span data-stu-id="f2fde-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="f2fde-134">**Yapılandırma** -toomanage erişim toohello çalışma sağlar</span><span class="sxs-lookup"><span data-stu-id="f2fde-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="f2fde-135">**WEB Hizmetleri** -bu çalışma alanından yayımlanan toomanage Web hizmetleri sağlar</span><span class="sxs-lookup"><span data-stu-id="f2fde-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="f2fde-136">Merhaba çalışma nasıl kullanıldığını toomonitor</span><span class="sxs-lookup"><span data-stu-id="f2fde-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="f2fde-137">Merhaba tıklatın **PANO** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f2fde-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="f2fde-138">Merhaba panodan çalışma alanınızı genel kullanımını görüntüleyin ve hızlı bir bakış çalışma bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="f2fde-139">Merhaba **işlem** grafik hello çalışma alanı tarafından kullanılan hello işlem kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="f2fde-140">Merhaba görünüm toodisplay göreli veya mutlak değerler değiştirebilirsiniz ve hello grafikte görüntülenen hello zaman çerçevesi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fde-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="f2fde-141">**Kullanıma genel bakış** hello çalışma alanı tarafından kullanılan Azure depolama görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f2fde-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="f2fde-142">**Hızlı Bakış** çalışma alanı bilgisi ve yararlı bağlantılar özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2fde-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fde-143">Merhaba **oturum açma Studio tooML** bağlantısı, Machine Learning Studio hello Microsoft, şu anda oturumunuz içine Account kullanarak açar.</span><span class="sxs-lookup"><span data-stu-id="f2fde-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="f2fde-144">Merhaba Microsoft toohello Azure Klasik portalı toocreate bir çalışma alanı toosign kullanılan Account bu çalışma izni tooopen otomatik olarak yok.</span><span class="sxs-lookup"><span data-stu-id="f2fde-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="f2fde-145">bir çalışma alanı tooopen toohello hello çalışma hello sahibi olarak tanımlandı Microsoft Account içinde imzalanmalıdır veya tooreceive hello sahibi toojoin hello çalışma alanından bir davet gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="f2fde-146">toogrant veya kullanıcıların erişimini askıya alma</span><span class="sxs-lookup"><span data-stu-id="f2fde-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="f2fde-147">Merhaba tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f2fde-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="f2fde-148">Merhaba yapılandırma sekmesinde şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f2fde-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="f2fde-149">Erişim toohello Machine Learning çalışma alanı REDDETME tıklayarak askıya alın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="f2fde-150">Kullanıcılar artık mümkün tooopen hello çalışma Machine Learning Studio'da olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="f2fde-151">toorestore erişmek için izin VER'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="f2fde-152">Machine Learning Studio'da erişim toohello çalışma sahip toomanage ek hesapları'nı tıklatın **oturum açma Studio tooML** hello içinde **PANO** sekmesini (Merhaba önceki nota bakın ilgili  **TooML Studio Sign-in**).</span><span class="sxs-lookup"><span data-stu-id="f2fde-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="f2fde-153">Machine Learning Studio'da hello çalışma alanı açılır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="f2fde-154">Buradan hello tıklatın **ayarları** sekmesini ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f2fde-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="f2fde-155">Tıklayabilirsiniz **daha fazla kullanıcı davet** toogive kullanıcılar toohello çalışma alanında, erişim veya bir kullanıcı seçin ve tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="f2fde-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="f2fde-156">Bu çalışma alanında toomanage web Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f2fde-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="f2fde-157">Merhaba tıklatın **WEB Hizmetleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f2fde-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="f2fde-158">Bu çalışma alanından yayımlanan web hizmetleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f2fde-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="f2fde-159">toomanage bir web hizmeti hello listesi tooopen hello Web hizmeti sayfanıza hello adlarında'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="f2fde-160">Bir Web hizmeti, tanımlı bir veya daha fazla uç noktaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="f2fde-161">Daha fazla uç noktaları ekleme toohello "Varsayılan" uç tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fde-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="f2fde-162">tooadd uç nokta Merhaba, tıklatın **yönetin uç noktaları** hello altındaki hello Pano tooopen hello Azure Machine Learning Web Hizmetleri portalı.</span><span class="sxs-lookup"><span data-stu-id="f2fde-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="f2fde-163">toodelete ("Varsayılan" Merhaba endpoint silemiyor) bir uç nokta hello uç nokta satır hello başında hello onay kutusuna tıklayın ve tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f2fde-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="f2fde-164">Bu, Web hizmeti hello hello bitiş noktasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f2fde-165">Merhaba endpoint silindiğinde hello web hizmeti uç noktası bir uygulama kullanıyorsa, Merhaba uygulaması başlatıldığında tooaccess hello hizmeti çalışır bir hata hello alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f2fde-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="f2fde-166">Bir Web Hizmeti uç noktası tooopen Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f2fde-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="f2fde-167">Merhaba panodan bir süre boyunca, Web hizmetinin genel kullanım görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fde-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="f2fde-168">Merhaba dönem açılır menüsünden hello sağ üst köşesinde, hello kullanım grafiklerini hello dönem tooview seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fde-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="f2fde-169">Başlangıç Panosu aşağıdaki bilgilerle hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2fde-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="f2fde-170">**Zaman içinde istekleri** süre seçili hello istekleri hello sayısının adım grafiği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f2fde-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="f2fde-171">Bu, kullanımında ani karşılaşıyorsanız tanımlamaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="f2fde-172">**İstek-yanıt istekleri** hello toplam hello hizmet hello seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek-yanıt çağrısı sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f2fde-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="f2fde-173">**Ortalama istek-yanıt işlem süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.</span><span class="sxs-lookup"><span data-stu-id="f2fde-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="f2fde-174">**Toplu istekleri** hello toplam sayısını görüntüler toplu istekleri hello hizmet süre seçili hello aldı ve kaç tanesinin başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="f2fde-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="f2fde-175">**Ortalama iş gecikme süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.</span><span class="sxs-lookup"><span data-stu-id="f2fde-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="f2fde-176">**Hataları** çağrıları toohello web hizmetinde hello toplama oluşan hata sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="f2fde-177">**Hizmetleri maliyetleri** hello hizmetiyle ilişkili hello fatura planı için hello ücretleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f2fde-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="f2fde-178">Merhaba yapılandırma sayfasında, aşağıdaki özelliklere hello güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f2fde-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="f2fde-179">**Açıklama** tooenter hello Web hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2fde-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="f2fde-180">Açıklama gerekli bir alandır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-180">Description is a required field.</span></span>
* <span data-ttu-id="f2fde-181">**Günlük kaydı** hello noktadaki günlüğü tooenable veya devre dışı bırakma hata verir.</span><span class="sxs-lookup"><span data-stu-id="f2fde-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="f2fde-182">Günlüğe kaydetme hakkında daha fazla bilgi için bkz [Machine Learning web hizmetleri için günlüğe kaydetme](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="f2fde-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="f2fde-183">**Örnek verileri etkinleştirmek** tooprovide örnek verileri tootest hello istek-yanıt hizmeti kullanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2fde-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="f2fde-184">Machine Learning Studio'da hello web hizmeti oluşturduysanız, hello örnek verileri kullanılan tootrain hello verilerden alınır, model.</span><span class="sxs-lookup"><span data-stu-id="f2fde-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="f2fde-185">Merhaba hizmet program aracılığıyla oluşturduysanız, hello veri hello JSON paketinin bir parçası sağlanan hello örnek verileri alınır.</span><span class="sxs-lookup"><span data-stu-id="f2fde-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

