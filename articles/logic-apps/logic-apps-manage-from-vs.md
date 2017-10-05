---
title: "Visual Studio - Azure Logic Apps mantığı uygulamaları yönetme | Microsoft Docs"
description: "Mantıksal uygulamalar ve diğer Azure varlıkları Visual Studio bulut Gezgini ile yönetme"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="41ddc-103">Mantıksal uygulamalarınızı Visual Studio bulut Gezgini ile yönetme</span><span class="sxs-lookup"><span data-stu-id="41ddc-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="41ddc-104">Ancak [Azure portal](https://portal.azure.com/) tasarlama ve Azure mantıksal uygulamaları yönetmek harika bir yol sunar, Visual Studio Cloud Explorer mantıksal uygulamalar dahil olmak üzere birçok Azure varlıklar yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41ddc-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="41ddc-105">Visual Studio bulut Gezgini, Gözat, yönetme, düzenleme sağlar ve logic apps indirme yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="41ddc-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="41ddc-106">Yönetim görevleri etkinleştir, devre dışı bırakma ve geçmişini görüntüleme çalıştırmak içerir.</span><span class="sxs-lookup"><span data-stu-id="41ddc-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="41ddc-107">Erişebilir ve logic apps Visual Studio içinde yönetebilirsiniz önce yükleyin ve bu Visual Studio Araçları Azure Logic Apps için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41ddc-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41ddc-108">Prerequisites</span></span>

* [<span data-ttu-id="41ddc-109">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="41ddc-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="41ddc-110">[En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="41ddc-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="41ddc-111">Visual Studio bulut Gezgini</span><span class="sxs-lookup"><span data-stu-id="41ddc-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="41ddc-112">Katıştırılmış Tasarımcısı'nı kullanırken web erişimi</span><span class="sxs-lookup"><span data-stu-id="41ddc-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="41ddc-113">Mantıksal uygulamalar için Visual Studio araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="41ddc-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="41ddc-114">Önkoşulları yüklendikten sonra indirin ve Visual Studio için Azure Logic Apps Araçları'nı yükleme.</span><span class="sxs-lookup"><span data-stu-id="41ddc-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="41ddc-115">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-115">Open Visual Studio.</span></span> <span data-ttu-id="41ddc-116">Üzerinde **Araçları** menüsünde, select **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="41ddc-117">Genişletme **çevrimiçi** Visual Studio Galerisi çevrimiçi arama yapabilmeniz için kategori.</span><span class="sxs-lookup"><span data-stu-id="41ddc-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="41ddc-118">Göz atın veya arayın **Logic Apps** bulana kadar **Visual Studio için Azure Logic Apps Araçları**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="41ddc-119">Karşıdan yükle ve uzantıyı yüklemek için tıklatın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="41ddc-120">Yüklendikten sonra Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="41ddc-121">Azure Logic Apps araçları Visual Studio için doğrudan indirmek için Git [Visual Studio Market'te](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="41ddc-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="41ddc-122">Logic apps Cloud Explorer'da gözatın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="41ddc-123">Cloud Explorer açmak için **Görünüm** menüsünde seçin **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="41ddc-124">Mantıksal uygulamanız için kaynak grubu veya kaynak türüne göre göz atın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="41ddc-125">Kaynak türüne göre göz atarsanız, Azure aboneliğinizi seçin, genişletin **Logic Apps** bölümünde ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="41ddc-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="41ddc-126">Kaynak grubu tarafından göz atarsanız, mantıksal uygulamanızı sahip olan kaynak grubunu genişletin ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="41ddc-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="41ddc-127">Mantıksal uygulamanız için komutları görüntülemek için mantıksal uygulamanızı sağ tıklayın ya da bulut Explorer alt kısmındaki arasından **Eylemler** menüsü.</span><span class="sxs-lookup"><span data-stu-id="41ddc-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Mantıksal uygulamanızı gözatın.](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="41ddc-129">Mantıksal uygulamanızı Logic Apps Tasarımcısı ile Düzenle</span><span class="sxs-lookup"><span data-stu-id="41ddc-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="41ddc-130">Bulut Gezgini'nden Azure portalında kullandığınız aynı Tasarımcısı'nda şu anda dağıtılmış mantıksal uygulama açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41ddc-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="41ddc-131">Cloud Explorer'da mantıksal uygulamanızı düzenlemek için mantıksal uygulamanızı sağ tıklatın ve seçin **mantığı uygulama Düzenleyicisi ile açık**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="41ddc-132">Güncelleştirmelerinizi buluta yayımlamak için tercih **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="41ddc-133">Yeni bir çalışma başlatmayı seçin **tetikleyici çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-133">To start a new run, choose **Run Trigger**.</span></span>

![Logic Apps Tasarımcısı](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="41ddc-135">Tasarımcısı'ndan şunları da yapabilirsiniz **karşıdan** bir mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="41ddc-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="41ddc-136">Bu eylem otomatik olarak mantıksal uygulama tanımını parameterizes ve tanım bir Azure Resource Manager dağıtım şablonu olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="41ddc-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="41ddc-137">Bu dağıtım şablonu Azure kaynak grubu projenizi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41ddc-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="41ddc-138">Mantıksal uygulamanızı çalıştırma geçmişi göz atın</span><span class="sxs-lookup"><span data-stu-id="41ddc-138">Browse your logic app run history</span></span>

<span data-ttu-id="41ddc-139">Mantıksal uygulamanızı çalıştırma geçmişini görüntülemek için mantıksal uygulamanızı sağ tıklatın ve seçin **açık çalıştırma geçmişi**.</span><span class="sxs-lookup"><span data-stu-id="41ddc-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="41ddc-140">Gösterilen özellikleri hiçbirinde göre çalışma geçmişinizi yeniden sıralamak için sütun başlığını seçin.</span><span class="sxs-lookup"><span data-stu-id="41ddc-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![çalıştırma geçmişi](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="41ddc-142">Girişleri ve çıkışları her adımdan dahil olmak üzere çalışma sonuçlarını inceleyebilirsiniz bir örneği için çalıştırma geçmişi görüntüleyecek şekilde çalışma örneklerden birini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="41ddc-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Geçmiş sonuçlarını, giriş ve çıkış adımları çalıştırın](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="41ddc-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41ddc-144">Next steps</span></span>

* [<span data-ttu-id="41ddc-145">İlk mantıksal uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41ddc-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="41ddc-146">Tasarım, derleme ve logic apps Visual Studio içinde dağıtma</span><span class="sxs-lookup"><span data-stu-id="41ddc-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="41ddc-147">Sık rastlanan örnekleri ve senaryoları inceleyin</span><span class="sxs-lookup"><span data-stu-id="41ddc-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="41ddc-148">Video: Azure Logic Apps ile iş süreçlerini otomatikleştirmek</span><span class="sxs-lookup"><span data-stu-id="41ddc-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="41ddc-149">Video: sistemlerinizi Azure Logic Apps ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="41ddc-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
