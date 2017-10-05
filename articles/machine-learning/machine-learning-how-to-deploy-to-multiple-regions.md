---
title: "Bir Web hizmeti için birden çok bölgeye dağıtma | Microsoft Docs"
description: "(Kopya) yeni bir Web hizmeti diğer bölgeler dağıtmak için adımları."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="25ac8-103">Web Hizmetini birden fazla bölgeye dağıtma</span><span class="sxs-lookup"><span data-stu-id="25ac8-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="25ac8-104">Yeni Azure Web Hizmetleri kolayca birden fazla abonelikleri veya çalışma alanları gerek kalmadan bir web hizmeti için birden çok bölgeye dağıtmanıza izin verin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="25ac8-105">Fiyatlandırma belirli, bu nedenle, web hizmeti dağıtacağınız her bölge için bir faturalandırma planı tanımlamalısınız bölgedir.</span><span class="sxs-lookup"><span data-stu-id="25ac8-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="25ac8-106">Başka bir bölgede bir plan oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="25ac8-106">To create a plan in another region</span></span>
1. <span data-ttu-id="25ac8-107">Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="25ac8-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="25ac8-108">Tıklatın **planları** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="25ac8-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="25ac8-109">Görünüm sayfası üzerinden planlarında tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="25ac8-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="25ac8-110">Gelen **abonelik** açılan listesinde, yeni plan bulunacağı aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="25ac8-111">Gelen **bölge** açılan listesinde, yeni plan için bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="25ac8-112">Seçilen bölge için planlama seçenekleri görüntüleyecek **planlama seçenekleri** sayfasının bölümünde.</span><span class="sxs-lookup"><span data-stu-id="25ac8-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="25ac8-113">Gelen **kaynak grubu** bir kaynak grubu plan için açılan listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="25ac8-114">Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ac8-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="25ac8-115">İçinde **Plan adı** planın adını yazın.</span><span class="sxs-lookup"><span data-stu-id="25ac8-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="25ac8-116">Altında **planı seçenekleri**, yeni plan için fatura düzeyi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="25ac8-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="25ac8-117">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="25ac8-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="25ac8-118">Web hizmeti başka bir bölgeye dağıtmayı</span><span class="sxs-lookup"><span data-stu-id="25ac8-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="25ac8-119">Tıklatın **Web Hizmetleri** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="25ac8-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="25ac8-120">Yeni bir bölgeye dağıtmayı Web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="25ac8-121">Tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="25ac8-121">Click **Copy**.</span></span>
4. <span data-ttu-id="25ac8-122">İçinde **Web hizmeti adı**, web hizmeti için yeni bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="25ac8-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="25ac8-123">İçinde **Web hizmeti açıklaması**, web hizmeti için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="25ac8-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="25ac8-124">Gelen **abonelik** açılan listesinde, yeni web hizmeti bulunacağı aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="25ac8-125">Gelen **kaynak grubu** bir kaynak grubu için web hizmeti açılan listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="25ac8-126">Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ac8-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="25ac8-127">Gelen **bölge** açılan listesinde, web hizmeti dağıtmak üzere bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="25ac8-128">Gelen **depolama hesabı** açılan listesinde, bir depolama birimi seçin, web hizmeti depolamak hesap.</span><span class="sxs-lookup"><span data-stu-id="25ac8-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="25ac8-129">Gelen **fiyat planı** açılan listesinde, 8. adımda seçtiğiniz bölgede planı seçin.</span><span class="sxs-lookup"><span data-stu-id="25ac8-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="25ac8-130">Tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="25ac8-130">Click **Copy**.</span></span>

