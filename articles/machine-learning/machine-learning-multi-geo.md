---
title: "Birden çok coğrafi Yardım belgeleri | Microsoft Docs"
description: "Çalışma alanı oluşturma ve bir web hizmeti Güney Orta Amerika Birleşik Devletleri (SCUS) öğesinden farklı bir Azure bölgesi yayımlamak öğrenin Azure bölgesi."
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
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="5cc23-103">Çoklu Coğrafi Bölge Yardım belgeleri</span><span class="sxs-lookup"><span data-stu-id="5cc23-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="5cc23-104">Bu makalede, nasıl bir çalışma alanı oluşturmak ve bir web hizmeti farklı Azure bölgelerinde yayımlama açıklanır.</span><span class="sxs-lookup"><span data-stu-id="5cc23-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="5cc23-105">[Azure ürünleri bölge sayfası tarafından](https://azure.microsoft.com/en-us/regions/services/) Azure Machine Learning olduğu kullanılabilir bölgeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="5cc23-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="5cc23-106">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cc23-106">Create a workspace</span></span>
1. <span data-ttu-id="5cc23-107">Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5cc23-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="5cc23-108">Tıklatın **+ yeni** > **Veri Hizmetleri** > **MACHINE LEARNING** > **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5cc23-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="5cc23-109">Altında **konumu** gibi başka bir bölge seçin **Güneydoğu Asya**.</span><span class="sxs-lookup"><span data-stu-id="5cc23-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="5cc23-110">![Birden çok coğrafi yardımcı görüntü 1][1]</span><span class="sxs-lookup"><span data-stu-id="5cc23-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="5cc23-111">Çalışma alanını seçin ve ardından **oturum açma ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="5cc23-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="5cc23-112">![Birden çok coğrafi yardımcı görüntü 2][2]</span><span class="sxs-lookup"><span data-stu-id="5cc23-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="5cc23-113">Diğer çalışma gibi kullanabilir, başka bir bölgede bir çalışma alanı artık sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc23-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="5cc23-114">Alanlarınız arasında geçiş yapmak için ekranınızın sağ üst için bakın.</span><span class="sxs-lookup"><span data-stu-id="5cc23-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="5cc23-115">Açılan listeyi tıklatın, bölgeyi seçin ve çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="5cc23-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="5cc23-116">Her şeyi çalışma bölgesine yereldir.</span><span class="sxs-lookup"><span data-stu-id="5cc23-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="5cc23-117">Örneğin, bir çalışma alanından oluşturulan web hizmetlerinizi tümünün çalışma alanında bulunan aynı bölgede olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5cc23-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="5cc23-118">![Birden çok coğrafi yardımcı görüntü 3][3]</span><span class="sxs-lookup"><span data-stu-id="5cc23-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="5cc23-119">Galeriden bir denemeyi açın</span><span class="sxs-lookup"><span data-stu-id="5cc23-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="5cc23-120">Galeriden bir denemeyi açarsanız, denemede kopyalamak istediğiniz hangi bölgede öğesini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc23-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Birden çok coğrafi yardımcı görüntü 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="5cc23-122">Web Hizmeti Yönetimi</span><span class="sxs-lookup"><span data-stu-id="5cc23-122">Web service management</span></span>
<span data-ttu-id="5cc23-123">Program aracılığıyla web Hizmetleri gibi yeniden eğitme için yönetmek için bölgeye özgü adresi kullanın:</span><span class="sxs-lookup"><span data-stu-id="5cc23-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="5cc23-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="5cc23-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="5cc23-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="5cc23-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="5cc23-126">Dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="5cc23-126">Things to note</span></span>
1. <span data-ttu-id="5cc23-127">Yalnızca bu şekilde aynı bölgeye ait çalışma alanları arasında denemeler kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc23-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="5cc23-128">Deneme kopyalamanız gerekiyorsa kullanabileceğiniz farklı bölgelerdeki çalışma alanları arasında [PowerShell](http://aka.ms/amlps) komutunu [ *kopya AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) bunu yapmaya yönelik.</span><span class="sxs-lookup"><span data-stu-id="5cc23-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="5cc23-129">Başka bir çözüm listelenmemiş modunda Galerisi içine deneme yayımlamaktır diğer bölgesinden çalışma alanını açın.</span><span class="sxs-lookup"><span data-stu-id="5cc23-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="5cc23-130">Bölge Seçici aynı anda yalnızca bir bölge için çalışma alanlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cc23-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="5cc23-131">Ücretsiz çalışma alanında ya da konuk erişimi (anonim) çalışma oluşturulacak ve ABD merkezi Güney içinde barındırılan</span><span class="sxs-lookup"><span data-stu-id="5cc23-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="5cc23-132">Güneydoğu Asya Güneydoğu Asya, bir çalışma alanından dağıtılan web hizmetleri de barındırılacak.</span><span class="sxs-lookup"><span data-stu-id="5cc23-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="5cc23-133">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="5cc23-133">More information</span></span>
<span data-ttu-id="5cc23-134">Üzerinde bir soru sorun [Azure Machine Learning Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="5cc23-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
