---
title: "Machine Learning çalışma alanı oluşturma | Microsoft Docs"
description: "Azure Machine Learning Studio'da bir çalışma alanı oluşturma"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="7532d-103">Bir Azure Machine Learning çalışma alanı oluşturma ve paylaşma</span><span class="sxs-lookup"><span data-stu-id="7532d-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="7532d-104">Cortana analitik işlem (CAP) tarafından kullanılan çeşitli veri bilimi ortamları ayarlama nasıl açıklayan konulara bu menü bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="7532d-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="7532d-105">Azure Machine Learning Studio kullanmak için bir Machine Learning çalışma alanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7532d-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="7532d-106">Bu çalışma alanı oluşturmak, yönetmek ve denemeler yayımlamak için ihtiyacınız olan araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="7532d-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="7532d-107">Bir çalışma alanı oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="7532d-107">To create a workspace</span></span>
1. <span data-ttu-id="7532d-108">Oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="7532d-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="7532d-109">Oturum açın ve bir çalışma alanı oluşturmak için Azure abonelik yöneticisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7532d-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="7532d-110">Tıklatın **+ yeni**</span><span class="sxs-lookup"><span data-stu-id="7532d-110">Click **+New**</span></span>

3. <span data-ttu-id="7532d-111">Seçin **Intelligence + analiz**, tıklatın **Machine Learning çalışma alanı**, ardından **oluştur**</span><span class="sxs-lookup"><span data-stu-id="7532d-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="7532d-112">Çalışma alanı bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="7532d-112">Enter your workspace information</span></span>

    - <span data-ttu-id="7532d-113">*Çalışma alanı adı* boşluk bitiş değil, en fazla 260 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="7532d-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="7532d-114">Adı şu karakterleri içeremez:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="7532d-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="7532d-115">*Web hizmeti planı* , seçin (veya oluşturun), ilişkili birlikte *fiyatlandırma katmanı* seçin, web hizmetleri bu çalışma alanından dağıtırsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7532d-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Yeni bir çalışma alanı oluşturma](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="7532d-117">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="7532d-117">Click **Create**</span></span>

<span data-ttu-id="7532d-118">Çalışma alanı dağıtıldığında, Machine Learning Studio'da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7532d-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="7532d-119">Machine Learning Studio'ya için Gözat [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="7532d-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="7532d-120">Çalışma alanınızı üst sağ taraftaki köşedeki seçin.</span><span class="sxs-lookup"><span data-stu-id="7532d-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Çalışma alanı seçin](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="7532d-122">Tıklatın **denemelerim**.</span><span class="sxs-lookup"><span data-stu-id="7532d-122">Click **my experiments**.</span></span>

    ![Açık denemeleri](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="7532d-124">Çalışma alanınızı yönetme hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="7532d-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="7532d-125">Çalışma alanınızı oluşturulurken bir sorunla karşılaşırsanız, bkz: [sorun giderme kılavuzu: oluşturun ve Machine Learning çalışma alanına bağlayın](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="7532d-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="7532d-126">Bir Azure Machine Learning çalışma alanı paylaşımı</span><span class="sxs-lookup"><span data-stu-id="7532d-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="7532d-127">Bir kez çalışma alanı oluşturulduğunda Machine Learning, kullanıcıları çalışma alanınızı ve tüm alt denemeler, veri kümeleri, dizüstü bilgisayarlar, vb. erişimi paylaşmak için çalışma alanına davet edebilirsiniz. Kullanıcılar iki rolleri ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7532d-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="7532d-128">**Kullanıcı** -çalışma kullanıcı oluşturmak, açın, değiştirmek ve silmek denemeler, veri kümeleri, vb. çalışma alanında.</span><span class="sxs-lookup"><span data-stu-id="7532d-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="7532d-129">**Sahibi** - sahibi davet edebilir ve çalışma alanında, hangi kullanıcı yanı sıra Kaldır kullanıcılar yapabilir.</span><span class="sxs-lookup"><span data-stu-id="7532d-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="7532d-130">Çalışma alanı oluşturur yönetici hesabı, çalışma alanı sahibi olarak çalışma alanına otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="7532d-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="7532d-131">Ancak, diğer Yöneticiler veya kullanıcılar bu abonelikte çalışma alanına erişim otomatik olarak verilmez - açıkça davet gerekir.</span><span class="sxs-lookup"><span data-stu-id="7532d-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="7532d-132">Bir çalışma alanı paylaşmak için</span><span class="sxs-lookup"><span data-stu-id="7532d-132">To share a workspace</span></span>

1. <span data-ttu-id="7532d-133">Machine Learning Studio'ya oturum [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="7532d-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="7532d-134">Sol panelinde tıklatın **ayarları**</span><span class="sxs-lookup"><span data-stu-id="7532d-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="7532d-135">Tıklatın **kullanıcılar** sekmesi</span><span class="sxs-lookup"><span data-stu-id="7532d-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="7532d-136">Tıklatın **daha fazla kullanıcı davet** sayfanın sonundaki</span><span class="sxs-lookup"><span data-stu-id="7532d-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Studio ayarları](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="7532d-138">Bir veya daha fazla e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="7532d-138">Enter one or more email addresses.</span></span> <span data-ttu-id="7532d-139">Kullanıcıların geçerli bir Microsoft hesabı veya kurumsal bir hesap (Azure Active Directory'den) gerekir.</span><span class="sxs-lookup"><span data-stu-id="7532d-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="7532d-140">Sahibi veya kullanıcı kullanıcılar eklemek istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="7532d-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="7532d-141">Tıklatın **Tamam** onay işareti düğmesine.</span><span class="sxs-lookup"><span data-stu-id="7532d-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="7532d-142">Eklediğiniz her kullanıcı için paylaşılan çalışma alanına oturum açmak yönergeler içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="7532d-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="7532d-143">Kullanıcıların dağıtmak veya bu çalışma alanında web hizmetleri yönetmek için bunların katkıda bulunan veya Azure Abonelik Yöneticisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7532d-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



