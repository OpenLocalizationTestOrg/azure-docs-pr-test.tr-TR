---
title: "Machine Learning aaaCreating Web Hizmeti uç noktalarını | Microsoft Docs"
description: "Azure Machine Learning Web Hizmeti uç noktaları oluşturma"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="69e65-103">Uç Nokta Oluşturma</span><span class="sxs-lookup"><span data-stu-id="69e65-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="69e65-104">Bu konu, geçerli tooa teknikleri açıklar **Klasik** Machine Learning Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="69e65-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="69e65-105">İleriye doğru tooyour müşteriler satmak Web Hizmetleri oluşturduğunuzda, hangi hello Web hizmeti oluşturuldu hala bağlı toohello deneme olan tooprovide eğitilmiş modeller tooeach müşteri gerekir.</span><span class="sxs-lookup"><span data-stu-id="69e65-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="69e65-106">Ayrıca, toohello deneme olması gereken herhangi bir güncelleştirme seçmeli olarak tooan endpoint hello özelleştirmeleri yazmadan uygulanır.</span><span class="sxs-lookup"><span data-stu-id="69e65-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="69e65-107">tooaccomplish Bu, Azure Machine Learning toocreate verir dağıtılan Web hizmeti için birden çok uç nokta.</span><span class="sxs-lookup"><span data-stu-id="69e65-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="69e65-108">Merhaba Web hizmeti içindeki her bir uç nokta bağımsız olarak ele, kısıtlanan yönetilen ve.</span><span class="sxs-lookup"><span data-stu-id="69e65-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="69e65-109">Her uç tooyour müşteriler dağıtabilirsiniz benzersiz bir URL ve yetkilendirme anahtar noktadır.</span><span class="sxs-lookup"><span data-stu-id="69e65-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="69e65-110">Uç noktaları tooa Web hizmeti ekleme</span><span class="sxs-lookup"><span data-stu-id="69e65-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="69e65-111">Bir Web Hizmeti uç noktası tooa üç yolu tooadd vardır.</span><span class="sxs-lookup"><span data-stu-id="69e65-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="69e65-112">Programlama yoluyla</span><span class="sxs-lookup"><span data-stu-id="69e65-112">Programmatically</span></span>
* <span data-ttu-id="69e65-113">Hello Azure Machine Learning Web Hizmetleri Portalı aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="69e65-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="69e65-114">Yine de klasik Azure portalı hello</span><span class="sxs-lookup"><span data-stu-id="69e65-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="69e65-115">Merhaba uç nokta oluşturulduktan sonra zaman uyumlu API'leri, batch API'leri aracılığıyla kullanabilir ve excel çalışma sayfaları.</span><span class="sxs-lookup"><span data-stu-id="69e65-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="69e65-116">Ayrıca tooadding uç noktaları bu kullanıcı Arabirimi aracılığıyla da kullanabilirsiniz hello uç nokta Yönetimi API'leri tooprogrammatically uç noktaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="69e65-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="69e65-117">Ek uç noktaları toohello Web hizmeti eklediyseniz, hello varsayılan uç silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="69e65-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="69e65-118">Bir uç nokta programlı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="69e65-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="69e65-119">Program aracılığıyla hello kullanarak bir uç nokta tooyour Web hizmeti Ekle [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.</span><span class="sxs-lookup"><span data-stu-id="69e65-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="69e65-120">Hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="69e65-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="69e65-121">Machine Learning Studio'da hello sol gezinti sütuna, Web Hizmetleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="69e65-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="69e65-122">Merhaba Web hizmeti Pano Hello altındaki tıklatın **uç yönetin**.</span><span class="sxs-lookup"><span data-stu-id="69e65-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="69e65-123">Hello Azure Machine Learning Web Hizmetleri portalı toohello hello Web hizmeti için uç noktaları sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="69e65-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="69e65-124">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69e65-124">Click **New**.</span></span>
4. <span data-ttu-id="69e65-125">Bir ad ve hello yeni uç noktası için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="69e65-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="69e65-126">Uç nokta adları 24 karakter veya daha az uzunlukta olmalı ve küçük harfler veya numaraların yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="69e65-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="69e65-127">Merhaba günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin.</span><span class="sxs-lookup"><span data-stu-id="69e65-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="69e65-128">Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning Web Hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="69e65-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="69e65-129">Merhaba Klasik Azure portalı kullanarak bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="69e65-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="69e65-130">İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com), tıklatın **Machine Learning** hello sol sütunda.</span><span class="sxs-lookup"><span data-stu-id="69e65-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="69e65-131">Merhaba Web hizmeti, ilgilendiğiniz içeren hello çalışma alanını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="69e65-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Tooworkspace gidin](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="69e65-133">Tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="69e65-133">Click **Web Services**.</span></span>
   
    ![TooWeb Hizmetleri gidin](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="69e65-135">Merhaba Web hizmeti toosee hello listesinde kullanılabilir uç noktaları ilgilendiğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="69e65-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Tooendpoint gidin](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="69e65-137">Merhaba sayfasının Hello altında tıklatın **uç nokta Ekle**.</span><span class="sxs-lookup"><span data-stu-id="69e65-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="69e65-138">Bir ad ve açıklama yazın, aynı ad bu Web hizmeti hello ile diğer uç nokta olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="69e65-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="69e65-139">Özel gereksinimleriniz olmadıkça hello kısıtlama düzeyini varsayılan değerini bırakın.</span><span class="sxs-lookup"><span data-stu-id="69e65-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="69e65-140">Azaltma, hakkında daha fazla toolearn bkz [ölçeklendirme API uç noktaları](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="69e65-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Uç noktası oluşturma](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="69e65-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="69e65-142">Next Steps</span></span>
<span data-ttu-id="69e65-143">[Nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="69e65-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

