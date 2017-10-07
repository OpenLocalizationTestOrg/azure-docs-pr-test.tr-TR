---
title: "aaaRetrain makine öğrenimi modeline | Microsoft Docs"
description: "Web hizmeti toouse hello yeni eğitilen modeli Azure Machine learning'de tooretrain bir model ve güncelleştirme nasıl hello öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="9e0a9-103">Machine Learning modelini çağırma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="9e0a9-104">Azure Machine Learning makine öğrenimi modellerinin operationalization hello sürecinin bir parçası olarak, modelinizi eğitilmiş ve kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="9e0a9-105">Ardından toocreate predicative bir Web hizmetini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="9e0a9-106">Merhaba Web hizmeti web siteleri, panolar ve mobil uygulamaları tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="9e0a9-107">Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="9e0a9-108">Yeni veriler kullanılabilir olduğunda ya da hello API hello tüketicisi varsa, kendi veri hello modeli retrained toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="9e0a9-109">Yeniden eğitme sık oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-109">Retraining may occur frequently.</span></span> <span data-ttu-id="9e0a9-110">Merhaba programlı yeniden eğitme API özelliğiyle hello yeniden eğitme API'lerini ve güncelleştirme hello Web hizmeti ile Merhaba yeni eğitilen modeli kullanarak hello modeli program aracılığıyla yeniden eğitme.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="9e0a9-111">Bu belge, işlemi yeniden eğitme hello açıklar ve nasıl toouse hello yeniden eğitme API'lerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="9e0a9-112">Neden yeniden eğitme: hello sorunu tanımlama</span><span class="sxs-lookup"><span data-stu-id="9e0a9-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="9e0a9-113">İşlem eğitim hello machine learning bir parçası olarak, bir model veri kümesini kullanarak eğitildi.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="9e0a9-114">Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="9e0a9-115">Yeni veriler kullanılabilir olduğunda ya da hello API hello tüketicisi varsa, kendi veri hello modeli retrained toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="9e0a9-116">Bu senaryolarda, siz veya hello programlı bir API uygun şekilde tooallow sağlar, API toocreate bir kerelik veya normal temelinde hello modeli kullanarak kendi verileri yeniden eğitme bir istemci tüketici.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="9e0a9-117">Bunlar daha sonra yeniden eğitme hello sonuçlarını değerlendirmek ve hello Web hizmeti API toouse hello yeni eğitilen modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="9e0a9-118">Varolan eğitim denemenizi ve yeni Web hizmeti varsa, varolan bir Tahmine dayalı Web hizmeti bölümden hello belirtildiği aşağıdaki hello yönergeler yerine Retrain çıkışı toocheck isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="9e0a9-119">Uçtan uca iş akışı</span><span class="sxs-lookup"><span data-stu-id="9e0a9-119">End-to-end workflow</span></span>
<span data-ttu-id="9e0a9-120">Merhaba işlemi içerir bileşenleri aşağıdaki hello: A eğitim denemenizi ve Tahmine dayalı denemeye bir Web hizmeti olarak yayımladı.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="9e0a9-121">tooenable eğitilen modeli, hello eğitim denemenizi yeniden eğitme eğitilen bir modelin hello çıktıyla bir Web hizmeti olarak yayımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="9e0a9-122">Bu yeniden eğitme için API erişim toohello modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="9e0a9-123">tooboth yeni ve Klasik Web Hizmetleri hello aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="9e0a9-124">Merhaba ilk Tahmine dayalı Web hizmeti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="9e0a9-125">Eğitim denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-125">Create a training experiment</span></span>
* <span data-ttu-id="9e0a9-126">Tahmine dayalı web deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="9e0a9-127">Tahmine dayalı web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-127">Deploy a predictive web service</span></span>

<span data-ttu-id="9e0a9-128">Merhaba Web hizmeti yeniden eğitme:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="9e0a9-129">Yeniden eğitme için eğitim deneme tooallow güncelleştir</span><span class="sxs-lookup"><span data-stu-id="9e0a9-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="9e0a9-130">Web hizmeti yeniden eğitme hello dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="9e0a9-131">Merhaba toplu yürütme hizmeti kod tooretrain hello modeli kullanın</span><span class="sxs-lookup"><span data-stu-id="9e0a9-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="9e0a9-132">Önceki adımları hello bir anlatım için bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a9-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="9e0a9-133">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="9e0a9-134">Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a9-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="9e0a9-135">Klasik Web hizmeti dağıttıysanız:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="9e0a9-136">Tahmine dayalı Web hizmeti hello üzerinde yeni bir uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="9e0a9-137">Merhaba düzeltme eki URL ve kodu alın</span><span class="sxs-lookup"><span data-stu-id="9e0a9-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="9e0a9-138">Kullanım hello düzeltme eki URL toopoint hello yeni uç noktada hello retrained modeli</span><span class="sxs-lookup"><span data-stu-id="9e0a9-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="9e0a9-139">Önceki adımları hello bir anlatım için bkz: [Klasik Web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a9-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="9e0a9-140">Klasik Web hizmeti yeniden eğitme zorluklar çalıştırırsanız, bkz: [hello bir Azure Machine Learning Klasik Web hizmeti yeniden eğitme sorun giderme](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a9-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="9e0a9-141">Yeni Web hizmeti dağıttıysanız:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="9e0a9-142">Tooyour Azure Resource Manager hesabı oturum</span><span class="sxs-lookup"><span data-stu-id="9e0a9-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="9e0a9-143">Merhaba Web hizmeti tanımının Al</span><span class="sxs-lookup"><span data-stu-id="9e0a9-143">Get hello Web service definition</span></span>
* <span data-ttu-id="9e0a9-144">Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="9e0a9-145">Merhaba başvuru toohello güncelleştirme `ilearner` hello JSON blob</span><span class="sxs-lookup"><span data-stu-id="9e0a9-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="9e0a9-146">İçeri aktarma hello JSON Web hizmeti tanımının içinde</span><span class="sxs-lookup"><span data-stu-id="9e0a9-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="9e0a9-147">Yeni Web hizmeti tanımının ile Merhaba Web hizmetini güncelleştirmek</span><span class="sxs-lookup"><span data-stu-id="9e0a9-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="9e0a9-148">Önceki adımları hello bir anlatım için bkz: [hello makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak yeni Web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a9-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="9e0a9-149">Klasik Web hizmeti yeniden eğitme yukarı ayarlamak için hello işlemi hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Yeniden eğitme işlemine genel bakış][1]

<span data-ttu-id="9e0a9-151">Yeni Web hizmeti yeniden eğitme yukarı ayarlamak için hello işlemi hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="9e0a9-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Yeniden eğitme işlemine genel bakış][7]

## <a name="other-resources"></a><span data-ttu-id="9e0a9-153">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9e0a9-153">Other Resources</span></span>
* [<span data-ttu-id="9e0a9-154">Azure Data Factory ile güncelleştirme Azure Machine Learning yeniden eğitme ve modelleri</span><span class="sxs-lookup"><span data-stu-id="9e0a9-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="9e0a9-155">Birçok Machine Learning modellerini ve web hizmeti uç noktalarını PowerShell kullanarak bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0a9-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="9e0a9-156">Merhaba [AML yeniden eğitme modelleri kullanarak API'lerini](https://www.youtube.com/watch?v=wwjglA8xllg) video gösterir, yeniden eğitme API'lerini ve PowerShell tooretrain Machine Learning modellerini hello kullanarak Azure Machine Learning ile nasıl oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="9e0a9-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

