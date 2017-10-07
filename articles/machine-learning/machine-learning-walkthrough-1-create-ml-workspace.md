---
title: "1. adım: Machine Learning çalışma alanı oluşturma | Microsoft Docs"
description: "1. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: öğrenin nasıl tooset yeni bir Azure Machine Learning Studio çalışma alanı ayarlama."
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
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="23014-103">Kılavuz Adımı 1: Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="23014-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="23014-104">Merhaba kılavuzun hello ilk adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="23014-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="23014-105">**Bir Machine Learning çalışma alanı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="23014-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="23014-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="23014-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="23014-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="23014-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="23014-108">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="23014-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="23014-109">Merhaba Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="23014-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="23014-110">Merhaba Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="23014-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="23014-111">toouse Machine Learning Studio, toohave bir Microsoft Azure Machine Learning çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="23014-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="23014-112">Bu çalışma alanı toocreate ihtiyacınız hello araçları içerir, yönetmek ve denemeler yayımlama.</span><span class="sxs-lookup"><span data-stu-id="23014-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="23014-113">Hello Yöneticisi Azure aboneliğinizi toocreate hello çalışma gerekir ve ardından sahibi veya katkıda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="23014-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="23014-114">Ayrıntılar için bkz [oluşturma ve Paylaşım bir Azure Machine Learning çalışma alanı](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="23014-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="23014-115">Çalışma alanınızı oluşturulduktan sonra Machine Learning Studio açın ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="23014-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="23014-116">Birden fazla çalışma alanı varsa, hello araç hello hello penceresinin sağ üst köşesindeki hello çalışma seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23014-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Studio çalışma alanı seçin][2]

> [!TIP]
> <span data-ttu-id="23014-118">Merhaba çalışma alanı sahibi yapılmışsa, üzerinde çalıştığınız diğer davet etme hello denemeler paylaşabilirsiniz toohello çalışma.</span><span class="sxs-lookup"><span data-stu-id="23014-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="23014-119">Machine Learning Studio'da hello üzerinde bunu yapabilirsiniz **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="23014-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="23014-120">Merhaba Microsoft hesabı veya Kurumsal hesap her kullanıcı için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="23014-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="23014-121">Hello üzerinde **ayarları** sayfasında, **kullanıcılar**, ardından **daha fazla kullanıcı davet** hello pencerenin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="23014-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="23014-122">**Sonraki: [var olan verileri yükleme](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="23014-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
