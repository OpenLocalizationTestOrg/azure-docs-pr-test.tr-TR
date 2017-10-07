---
title: "aaaMulti coğrafi Yardım belgelerine | Microsoft Docs"
description: "Bilgi nasıl toocreate bir çalışma alanı ve bir web hizmeti hello Güney Orta Amerika Birleşik Devletleri (SCUS) farklı bir Azure bölgesi yayımlamak Azure bölgesi."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="5f9e5-103">Çoklu Coğrafi Bölge Yardım belgeleri</span><span class="sxs-lookup"><span data-stu-id="5f9e5-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="5f9e5-104">Bu makalede, nasıl bir çalışma alanı oluşturmak ve bir web hizmeti farklı Azure bölgelerinde yayımlama açıklanır.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="5f9e5-105">Merhaba [Azure ürünleri bölge sayfası tarafından](https://azure.microsoft.com/en-us/regions/services/) Azure Machine Learning olduğu kullanılabilir bölgeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="5f9e5-106">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f9e5-106">Create a workspace</span></span>
1. <span data-ttu-id="5f9e5-107">Toohello Klasik Azure Portalı ' oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="5f9e5-108">Tıklatın **+ yeni** > **Veri Hizmetleri** > **MACHINE LEARNING** > **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="5f9e5-109">Altında **konumu** gibi başka bir bölge seçin **Güneydoğu Asya**.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="5f9e5-110">![Birden çok coğrafi yardımcı görüntü 1][1]</span><span class="sxs-lookup"><span data-stu-id="5f9e5-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="5f9e5-111">Merhaba çalışma alanını seçin ve ardından **oturum açma Studio tooML**.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="5f9e5-112">![Birden çok coğrafi yardımcı görüntü 2][2]</span><span class="sxs-lookup"><span data-stu-id="5f9e5-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="5f9e5-113">Diğer çalışma gibi kullanabilir, başka bir bölgede bir çalışma alanı artık sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="5f9e5-114">Görünüm toohello üst ekranınızın sağ tooswitch, çalışma alanları arasında.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="5f9e5-115">Merhaba açılır, select hello bölge ve ardından hello çalışma tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="5f9e5-116">Her şeyin yerel toohello çalışma bölgedir.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="5f9e5-117">Örneğin, bir çalışma alanından oluşturulan web hizmetlerinizi tümünün aynı bölge hello çalışma alanında bulunan hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="5f9e5-118">![Birden çok coğrafi yardımcı görüntü 3][3]</span><span class="sxs-lookup"><span data-stu-id="5f9e5-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="5f9e5-119">Galeriden bir denemeyi açın</span><span class="sxs-lookup"><span data-stu-id="5f9e5-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="5f9e5-120">Galeriden bir denemeyi açarsanız, hangi bölgede toocopy hello deneme istediğiniz de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Birden çok coğrafi yardımcı görüntü 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="5f9e5-122">Web Hizmeti Yönetimi</span><span class="sxs-lookup"><span data-stu-id="5f9e5-122">Web service management</span></span>
<span data-ttu-id="5f9e5-123">tooprogrammatically yönetme web Hizmetleri gibi yeniden eğitme için bölgeye özgü adresini hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5f9e5-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="5f9e5-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="5f9e5-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="5f9e5-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="5f9e5-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="5f9e5-126">Şeyler toonote</span><span class="sxs-lookup"><span data-stu-id="5f9e5-126">Things toonote</span></span>
1. <span data-ttu-id="5f9e5-127">Yalnızca denemeler toohello ait çalışma alanları arasında kopyalayabilirsiniz aynı bölgede bu şekilde.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="5f9e5-128">Toocopy deneme gerekiyorsa hello kullanabileceğiniz farklı bölgelerdeki çalışma alanları arasında [PowerShell](http://aka.ms/amlps) komutunu [ *kopya AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="5f9e5-129">Başka bir çözüm toopublish hello deneme Galerisi içine listelenmemiş modundayken sonra diğer bölge hello hello çalışma alanını açın.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="5f9e5-130">Hello bölge Seçici aynı anda yalnızca tek bir bölge için çalışma alanları gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="5f9e5-131">Ücretsiz çalışma alanında ya da konuk erişimi (anonim) çalışma oluşturulacak ve ABD merkezi Güney içinde barındırılan</span><span class="sxs-lookup"><span data-stu-id="5f9e5-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="5f9e5-132">Güneydoğu Asya Güneydoğu Asya, bir çalışma alanından dağıtılan web hizmetleri de barındırılacak.</span><span class="sxs-lookup"><span data-stu-id="5f9e5-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="5f9e5-133">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="5f9e5-133">More information</span></span>
<span data-ttu-id="5f9e5-134">Bir soru sorun üzerinde hello [Azure Machine Learning Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="5f9e5-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
