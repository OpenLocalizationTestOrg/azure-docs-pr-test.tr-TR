---
title: "bir Web hizmeti aaaHow toodeploy toomultiple bölgeler | Microsoft Docs"
description: "Adımları toodeploy (kopya) yeni Web hizmeti tooother bölgeleri."
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
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="1723e-103">Nasıl toodeploy bir Web hizmeti toomultiple bölgeleri</span><span class="sxs-lookup"><span data-stu-id="1723e-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="1723e-104">Merhaba yeni Azure Web Hizmetleri izin tooeasily birden çok abonelikleri veya çalışma alanları gerek kalmadan bir web hizmeti toomultiple bölgeler dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1723e-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="1723e-105">Fiyatlandırma belirli, bu nedenle hello web hizmeti dağıtacağınız her bölge için bir faturalandırma planı tanımlamanız gerekir bölgedir.</span><span class="sxs-lookup"><span data-stu-id="1723e-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="1723e-106">toocreate başka bir bölgede bir planı</span><span class="sxs-lookup"><span data-stu-id="1723e-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="1723e-107">Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="1723e-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="1723e-108">Merhaba tıklatın **planları** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1723e-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="1723e-109">Görünüm sayfası üzerinden Hello planlarını temel tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="1723e-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="1723e-110">Merhaba gelen **abonelik** açılan listesinde, hangi hello yeni plan bulunacağı select hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="1723e-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="1723e-111">Merhaba gelen **bölge** açılan listesinde, hello yeni plan için bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="1723e-112">Merhaba planlama seçenekleri hello seçili bölgeye hello görüntüler **planlama seçenekleri** hello sayfasının bölümünde.</span><span class="sxs-lookup"><span data-stu-id="1723e-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="1723e-113">Merhaba gelen **kaynak grubu** bir kaynak grubu hello planlama açılan listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="1723e-114">Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1723e-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="1723e-115">İçinde **Plan adı** hello planının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="1723e-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="1723e-116">Altında **planı seçenekleri**, fatura düzeyi hello yeni plan hello'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1723e-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="1723e-117">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1723e-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="1723e-118">Merhaba web hizmeti tooanother bölge dağıtma</span><span class="sxs-lookup"><span data-stu-id="1723e-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="1723e-119">Merhaba tıklatın **Web Hizmetleri** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1723e-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="1723e-120">Merhaba, tooa yeni bölge dağıttığınız Web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="1723e-121">Tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="1723e-121">Click **Copy**.</span></span>
4. <span data-ttu-id="1723e-122">İçinde **Web hizmeti adı**, hello web hizmeti için yeni bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="1723e-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="1723e-123">İçinde **Web hizmeti açıklaması**, hello web hizmeti için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="1723e-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="1723e-124">Merhaba gelen **abonelik** açılan listesinde, hangi hello yeni web hizmeti bulunacağı select hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="1723e-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="1723e-125">Merhaba gelen **kaynak grubu** bir kaynak grubu hello web hizmeti için açılan listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="1723e-126">Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1723e-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="1723e-127">Merhaba gelen **bölge** açılan listesinde, hangi toodeploy hello web hizmeti seçin hello bölgede.</span><span class="sxs-lookup"><span data-stu-id="1723e-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="1723e-128">Merhaba gelen **depolama hesabı** hangi toostore hello depolama hesabında web hizmeti açılan listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="1723e-129">Merhaba gelen **fiyat planı** açılan listesinde, 8. adımda seçtiğiniz hello bölgede planı seçin.</span><span class="sxs-lookup"><span data-stu-id="1723e-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="1723e-130">Tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="1723e-130">Click **Copy**.</span></span>

