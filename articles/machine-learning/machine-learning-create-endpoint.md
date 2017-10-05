---
title: "Machine Learning Web Hizmeti uç noktalarını oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="1ddbc-103">Uç Nokta Oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ddbc-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="1ddbc-104">Bu konu, uygulanabilir teknikleri açıklar bir **Klasik** Machine Learning Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="1ddbc-105">İleri müşterilerinize satış Web Hizmetleri oluşturduğunuzda, Web hizmeti oluşturulduğu deneme hala bağlı her bir müşteri için eğitilmiş modeller sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="1ddbc-106">Ayrıca, herhangi bir güncelleştirme deneme seçerek bir uç nokta özelleştirmeleri yazmadan uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="1ddbc-107">Bunu başarmak için Azure Machine Learning, dağıtılan Web hizmeti için birden fazla uç noktası oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="1ddbc-108">Web hizmeti içindeki her bir uç nokta bağımsız olarak ele, kısıtlanan yönetilen ve.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="1ddbc-109">Bir benzersiz URL ve müşterilerinize dağıtabilirsiniz yetkilendirme anahtar her uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="1ddbc-110">Web hizmeti için uç noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="1ddbc-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="1ddbc-111">Bir Web hizmeti için bir uç nokta eklemenin üç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="1ddbc-112">Programlama yoluyla</span><span class="sxs-lookup"><span data-stu-id="1ddbc-112">Programmatically</span></span>
* <span data-ttu-id="1ddbc-113">Azure Machine Learning Web Hizmetleri Portalı aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="1ddbc-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="1ddbc-114">Ancak klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="1ddbc-114">Though the Azure classic portal</span></span>

<span data-ttu-id="1ddbc-115">Uç nokta oluşturulduktan sonra zaman uyumlu API'leri, batch API'leri aracılığıyla kullanabilir ve excel çalışma sayfaları.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="1ddbc-116">Bu kullanıcı Arabirimi aracılığıyla uç noktaları ekleme ek olarak, uç nokta yönetim API'ları program aracılığıyla uç noktalarını eklemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="1ddbc-117">Web hizmetine ek uç noktaları eklediyseniz, varsayılan uç silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="1ddbc-118">Bir uç nokta programlı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="1ddbc-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="1ddbc-119">Program aracılığıyla kullanarak Web hizmetiniz için bir uç nokta ekleyebilirsiniz [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="1ddbc-120">Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="1ddbc-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="1ddbc-121">Machine Learning Studio'da Web Hizmetleri sol gezinti sütunu,'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="1ddbc-122">Web hizmeti Pano altındaki tıklatın **uç yönetin**.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="1ddbc-123">Web Hizmeti uç noktaları sayfasına Azure Machine Learning Web Hizmetleri Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="1ddbc-124">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-124">Click **New**.</span></span>
4. <span data-ttu-id="1ddbc-125">Bir ad ve yeni uç noktası için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="1ddbc-126">Uç nokta adları 24 karakter veya daha az uzunlukta olmalı ve küçük harfler veya numaraların yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="1ddbc-127">Günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="1ddbc-128">Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning Web Hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="1ddbc-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="1ddbc-129">Klasik Azure portalını kullanarak bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="1ddbc-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="1ddbc-130">Oturum [Klasik Azure portalı](http://manage.windowsazure.com), tıklatın **Machine Learning** sol sütunda.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="1ddbc-131">İçinde ilgilendiğiniz Web hizmeti içeren çalışma alanını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Çalışma alanına gidin](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="1ddbc-133">Tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-133">Click **Web Services**.</span></span>
   
    ![Web Hizmetlerine gidin](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="1ddbc-135">Kullanılabilir uç noktaları listesini görmek ilgilendiğiniz Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Bitiş noktasına gidin](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="1ddbc-137">Sayfanın alt kısmındaki tıklatın **uç nokta Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="1ddbc-138">Bir ad ve açıklama yazın, diğer uç nokta bu Web hizmeti aynı ada sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="1ddbc-139">Özel gereksinimleriniz olmadıkça kısıtlama düzeyini varsayılan değerini bırakın.</span><span class="sxs-lookup"><span data-stu-id="1ddbc-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="1ddbc-140">Azaltma hakkında daha fazla bilgi için bkz: [ölçeklendirme API uç noktaları](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="1ddbc-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Uç noktası oluşturma](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="1ddbc-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1ddbc-142">Next Steps</span></span>
<span data-ttu-id="1ddbc-143">[Bir Azure Machine Learning Web hizmeti kullanmak nasıl](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="1ddbc-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

