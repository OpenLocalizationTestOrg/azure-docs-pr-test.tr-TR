---
title: "Machine Learning çalışma alanı aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Machine Learning Studio'da bir çalışma alanı"
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
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="f291f-103">Bir Azure Machine Learning çalışma alanı oluşturma ve paylaşma</span><span class="sxs-lookup"><span data-stu-id="f291f-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="f291f-104">Bu menü hello yukarı tooset çeşitli veri bilimi ortamları hello Cortana analitik işlem (CAP) tarafından nasıl kullanılacağını açıklamaktadır tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="f291f-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="f291f-105">Azure Machine Learning Studio toouse toohave Machine Learning çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f291f-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="f291f-106">Bu çalışma alanı toocreate ihtiyacınız hello araçları içerir, yönetmek ve denemeler yayımlama.</span><span class="sxs-lookup"><span data-stu-id="f291f-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="f291f-107">toocreate bir çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="f291f-107">toocreate a workspace</span></span>
1. <span data-ttu-id="f291f-108">İçinde toohello oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f291f-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="f291f-109">içinde toosign ve çalışma alanı oluşturma, toobe Azure Abonelik Yöneticisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f291f-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="f291f-110">Tıklatın **+ yeni**</span><span class="sxs-lookup"><span data-stu-id="f291f-110">Click **+New**</span></span>

3. <span data-ttu-id="f291f-111">Seçin **Intelligence + analiz**, tıklatın **Machine Learning çalışma alanı**, ardından **oluştur**</span><span class="sxs-lookup"><span data-stu-id="f291f-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="f291f-112">Çalışma alanı bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="f291f-112">Enter your workspace information</span></span>

    - <span data-ttu-id="f291f-113">Merhaba *çalışma alanı adı* too260 karakter, bir boşluk bitiş değil yukarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f291f-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="f291f-114">Merhaba adı şu karakterleri içeremez:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="f291f-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="f291f-115">Merhaba *web hizmeti planı* , seçin (veya oluşturun), ilişkili hello birlikte *fiyatlandırma katmanı* seçin, web hizmetleri bu çalışma alanından dağıtırsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f291f-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Yeni bir çalışma alanı oluşturma](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="f291f-117">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="f291f-117">Click **Create**</span></span>

<span data-ttu-id="f291f-118">Merhaba çalışma dağıtıldığında, Machine Learning Studio'da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f291f-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="f291f-119">TooMachine Learning Studio Gözat adresindeki [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f291f-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="f291f-120">Çalışma alanınızı hello üst sağ taraftaki köşedeki seçin.</span><span class="sxs-lookup"><span data-stu-id="f291f-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Çalışma alanı seçin](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="f291f-122">Tıklatın **denemelerim**.</span><span class="sxs-lookup"><span data-stu-id="f291f-122">Click **my experiments**.</span></span>

    ![Açık denemeleri](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="f291f-124">Çalışma alanınızı yönetme hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f291f-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="f291f-125">Çalışma alanınızı oluşturulurken bir sorunla karşılaşırsanız, bkz: [sorun giderme kılavuzu: oluşturmak ve tooa Machine Learning çalışma alanı bağlanmak](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f291f-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="f291f-126">Bir Azure Machine Learning çalışma alanı paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f291f-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="f291f-127">Machine Learning çalışma alanı oluşturulduktan sonra kullanıcılar tooyour çalışma tooshare erişim tooyour çalışma ve tüm alt denemeler, veri kümeleri, dizüstü bilgisayarlar, vb. davet edebilirsiniz. Kullanıcılar iki rolleri ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f291f-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="f291f-128">**Kullanıcı** -çalışma kullanıcı oluşturmak, açın, değiştirmek ve silmek denemeler, veri kümeleri, vb. hello çalışma alanında.</span><span class="sxs-lookup"><span data-stu-id="f291f-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="f291f-129">**Sahibi** - sahibi davet edebilir ve Kaldır kullanıcıların eklenmesi toowhat bir kullanıcı olarak hello çalışma alanında yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f291f-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="f291f-130">Merhaba çalışma alanı oluşturur hello yönetici hesabı, çalışma alanı sahibi olarak toohello çalışma alanı otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="f291f-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="f291f-131">Ancak, abonelik olmayan, otomatik olarak diğer Yöneticiler veya kullanıcılar toohello çalışma erişim verilen - tooinvite ihtiyacınız bunları açıkça.</span><span class="sxs-lookup"><span data-stu-id="f291f-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="f291f-132">tooshare bir çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="f291f-132">tooshare a workspace</span></span>

1. <span data-ttu-id="f291f-133">Learning Studio'ya tooMachine içinde oturum [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="f291f-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="f291f-134">Merhaba sol panelinde tıklatın **ayarları**</span><span class="sxs-lookup"><span data-stu-id="f291f-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="f291f-135">Merhaba tıklatın **kullanıcılar** sekmesi</span><span class="sxs-lookup"><span data-stu-id="f291f-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="f291f-136">Tıklatın **daha fazla kullanıcı davet** hello sayfa hello altındaki</span><span class="sxs-lookup"><span data-stu-id="f291f-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Studio ayarları](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="f291f-138">Bir veya daha fazla e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="f291f-138">Enter one or more email addresses.</span></span> <span data-ttu-id="f291f-139">Merhaba kullanıcıların geçerli bir Microsoft hesabı veya kurumsal bir hesap (Azure Active Directory'den) gerekir.</span><span class="sxs-lookup"><span data-stu-id="f291f-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="f291f-140">Sahibi veya kullanıcı olarak tooadd hello kullanıcılar istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f291f-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="f291f-141">Merhaba tıklatın **Tamam** onay işareti düğmesine.</span><span class="sxs-lookup"><span data-stu-id="f291f-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="f291f-142">Eklediğiniz her bir kullanıcı çalışma toohello toosign nasıl paylaşılacağını hakkında yönergeler içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f291f-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="f291f-143">Kullanıcıların toobe mümkün toodeploy için veya bu çalışma alanında web hizmetleri yönetmek için katkıda bulunan veya hello Azure abonelik yöneticisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f291f-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



