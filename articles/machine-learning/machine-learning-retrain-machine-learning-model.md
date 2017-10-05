---
title: "Machine Learning modelini çağırma | Microsoft Docs"
description: "Bir model yeniden eğitme ve Azure Machine Learning ile yeni eğitilen modelini kullanmak için Web hizmetini güncelleştirmek hakkında bilgi edinin."
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
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="f9f34-103">Machine Learning modelini çağırma</span><span class="sxs-lookup"><span data-stu-id="f9f34-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="f9f34-104">Azure Machine Learning makine öğrenimi modellerinin operationalization sürecinin bir parçası olarak, modelinizi eğitilmiş ve kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="f9f34-105">Ardından, predicative bir Web hizmeti oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9f34-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="f9f34-106">Web hizmeti web siteleri, panolar ve mobil uygulamaları tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="f9f34-107">Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="f9f34-108">Yeni veriler kullanılabilir olduğunda ya da kendi veri tüketici API varsa, model retrained gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="f9f34-109">Yeniden eğitme sık oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-109">Retraining may occur frequently.</span></span> <span data-ttu-id="f9f34-110">Program yeniden eğitme API özelliğiyle program aracılığıyla yeniden eğitme API'lerini kullanarak modeli yeniden eğitme ve Web hizmeti ile yeni eğitilen model güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9f34-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="f9f34-111">Bu belge yeniden eğitme işlemini açıklar ve yeniden eğitme API'lerini kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="f9f34-112">Neden yeniden eğitme: sorun tanımlama</span><span class="sxs-lookup"><span data-stu-id="f9f34-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="f9f34-113">Makine öğrenimi eğitim işleminin bir parçası olarak, bir model veri kümesini kullanarak eğitildi.</span><span class="sxs-lookup"><span data-stu-id="f9f34-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="f9f34-114">Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="f9f34-115">Yeni veriler kullanılabilir olduğunda ya da kendi veri tüketici API varsa, model retrained gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="f9f34-116">Bu senaryolarda, siz veya Apı'lerinizi tüketici kullanıcıların kendi verilerini kullanarak modeli bir kerelik veya normal temelinde yeniden eğitme bir istemci oluşturmak izin vermek için kolay bir yol programlı bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9f34-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="f9f34-117">Bunlar daha sonra yeniden eğitme sonuçlarını değerlendirmek ve yeni eğitilen modelini kullanmak için Web hizmeti API'sine güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9f34-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="f9f34-118">Varolan eğitim denemenizi ve yeni Web hizmeti varsa, aşağıdaki bölümde belirtildiği izlenecek yol aşağıdaki yerine var olan bir Tahmine dayalı Web hizmetini Retrain denetlemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9f34-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="f9f34-119">Uçtan uca iş akışı</span><span class="sxs-lookup"><span data-stu-id="f9f34-119">End-to-end workflow</span></span>
<span data-ttu-id="f9f34-120">İşlemi aşağıdaki bileşenleri içerir: A eğitim denemenizi ve Tahmine dayalı denemeye bir Web hizmeti olarak yayımladı.</span><span class="sxs-lookup"><span data-stu-id="f9f34-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="f9f34-121">Eğitilen modeli yeniden eğitme etkinleştirmek için eğitim denemenizi çıktısı bir modeli, Web hizmetiyle yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9f34-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="f9f34-122">Bu API yeniden eğitme için modeline erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9f34-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="f9f34-123">Aşağıdaki adımlar, hem yeni hem de klasik Web Hizmetleri için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="f9f34-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="f9f34-124">İlk Tahmine dayalı Web hizmeti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f9f34-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="f9f34-125">Eğitim denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9f34-125">Create a training experiment</span></span>
* <span data-ttu-id="f9f34-126">Tahmine dayalı web deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9f34-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="f9f34-127">Tahmine dayalı web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="f9f34-127">Deploy a predictive web service</span></span>

<span data-ttu-id="f9f34-128">Web hizmeti yeniden eğitme:</span><span class="sxs-lookup"><span data-stu-id="f9f34-128">Retrain the Web service:</span></span>

* <span data-ttu-id="f9f34-129">Yeniden eğitme için izin vermek için eğitim denemenizi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f9f34-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="f9f34-130">Yeniden eğitme web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="f9f34-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="f9f34-131">Modeli yeniden eğitme için toplu yürütme hizmeti kodu kullanın</span><span class="sxs-lookup"><span data-stu-id="f9f34-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="f9f34-132">Önceki bir gözden geçirme adımları için bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="f9f34-133">Yeni bir web hizmeti dağıtmak için yeterli izinleri olan Abonelikteki, web hizmetini dağıtma olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f9f34-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="f9f34-134">Daha fazla bilgi için [Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir Web hizmetini yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="f9f34-135">Klasik Web hizmeti dağıttıysanız:</span><span class="sxs-lookup"><span data-stu-id="f9f34-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="f9f34-136">Tahmine dayalı Web hizmetinde yeni bir uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9f34-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="f9f34-137">URL düzeltme ve kodu alın</span><span class="sxs-lookup"><span data-stu-id="f9f34-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="f9f34-138">Retrained modeli yeni uç noktası için düzeltme eki URL'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="f9f34-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="f9f34-139">Önceki bir gözden geçirme adımları için bkz: [Klasik Web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="f9f34-140">Klasik Web hizmeti yeniden eğitme zorluklar çalıştırırsanız, bkz: [bir Azure Machine Learning Klasik Web hizmeti yeniden eğitme sorun giderme](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="f9f34-141">Yeni Web hizmeti dağıttıysanız:</span><span class="sxs-lookup"><span data-stu-id="f9f34-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="f9f34-142">Azure Resource Manager hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="f9f34-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="f9f34-143">Web hizmeti tanımının Al</span><span class="sxs-lookup"><span data-stu-id="f9f34-143">Get the Web service definition</span></span>
* <span data-ttu-id="f9f34-144">Web hizmeti tanımının JSON olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="f9f34-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="f9f34-145">Başvuru güncelleştirme `ilearner` JSON blob</span><span class="sxs-lookup"><span data-stu-id="f9f34-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="f9f34-146">Bir Web hizmeti tanımının JSON içe</span><span class="sxs-lookup"><span data-stu-id="f9f34-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="f9f34-147">Yeni Web hizmeti tanımının Web hizmetiyle güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f9f34-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="f9f34-148">Önceki bir gözden geçirme adımları için bkz: [makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak yeni Web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="f9f34-149">Klasik Web hizmeti yeniden eğitme yukarı ayarlama işlemi şu adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="f9f34-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Yeniden eğitme işlemine genel bakış][1]

<span data-ttu-id="f9f34-151">Yeni Web hizmeti yeniden eğitme yukarı ayarlama işlemi şu adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="f9f34-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Yeniden eğitme işlemine genel bakış][7]

## <a name="other-resources"></a><span data-ttu-id="f9f34-153">Diğer Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f9f34-153">Other Resources</span></span>
* [<span data-ttu-id="f9f34-154">Azure Data Factory ile güncelleştirme Azure Machine Learning yeniden eğitme ve modelleri</span><span class="sxs-lookup"><span data-stu-id="f9f34-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="f9f34-155">Birçok Machine Learning modellerini ve web hizmeti uç noktalarını PowerShell kullanarak bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9f34-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="f9f34-156">[AML yeniden eğitme modelleri kullanarak API'lerini](https://www.youtube.com/watch?v=wwjglA8xllg) video gösterir, Azure Machine Learning ile oluşturulan Machine Learning modelleri yeniden eğitme nasıl yeniden eğitme API'lerini ve PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f9f34-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

