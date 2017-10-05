---
title: "1. adım: Machine Learning çalışma alanı oluşturma | Microsoft Docs"
description: "Adım 1 / geliştirme Tahmine dayalı bir çözüm izlenecek yol: yeni bir Azure Machine Learning Studio çalışma alanı ayarlayıp öğrenin."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="52180-103">Kılavuz Adımı 1: Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="52180-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="52180-104">Bu izlenecek yol ilk adımdır [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="52180-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="52180-105">**Bir Machine Learning çalışma alanı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="52180-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="52180-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="52180-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="52180-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="52180-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="52180-108">Modelleri eğitme ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="52180-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="52180-109">Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="52180-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="52180-110">Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="52180-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="52180-111">Machine Learning Studio kullanmak için bir Microsoft Azure Machine Learning çalışma alanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="52180-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="52180-112">Bu çalışma alanı oluşturmak, yönetmek ve denemeler yayımlamak için ihtiyacınız olan araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="52180-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="52180-113">Azure aboneliğiniz için Yönetici çalışma alanı oluşturmak ve ardından sahibi veya katkıda eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="52180-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="52180-114">Ayrıntılar için bkz [oluşturma ve Paylaşım bir Azure Machine Learning çalışma alanı](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="52180-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="52180-115">Çalışma alanınızı oluşturulduktan sonra Machine Learning Studio açın ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="52180-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="52180-116">Birden fazla çalışma alanı varsa, pencerenin sağ üst köşesindeki araç çubuğundaki çalışma seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52180-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Studio çalışma alanı seçin][2]

> [!TIP]
> <span data-ttu-id="52180-118">Çalışma alanının sahibi yapılmışsa başkaları için çalışma alanına davet üzerinde çalıştığınız denemeler paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52180-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="52180-119">Machine Learning Studio'da üzerinde bunu yapabilirsiniz **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="52180-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="52180-120">Microsoft hesabı veya Kurumsal hesap her kullanıcı için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="52180-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="52180-121">Üzerinde **ayarları** sayfasında, **kullanıcılar**, ardından **daha fazla kullanıcı davet** pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="52180-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="52180-122">**Sonraki: [var olan verileri yükleme](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="52180-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
