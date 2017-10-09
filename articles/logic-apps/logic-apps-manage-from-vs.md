---
title: Visual Studio - Azure Logic Apps aaaManage logic apps | Microsoft Docs
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="d4beb-103">Mantıksal uygulamalarınızı Visual Studio bulut Gezgini ile yönetme</span><span class="sxs-lookup"><span data-stu-id="d4beb-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="d4beb-104">Merhaba rağmen [Azure portal](https://portal.azure.com/) toodesign sizin için harika bir yol sunar ve Azure mantıksal uygulamaları yönetmek için Visual Studio Cloud Explorer mantıksal uygulamalar dahil olmak üzere birçok Azure varlıklar yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4beb-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="d4beb-105">Visual Studio bulut Gezgini, Gözat, yönetme, düzenleme sağlar ve logic apps indirme yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="d4beb-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="d4beb-106">Yönetim görevleri etkinleştir, devre dışı bırakma ve geçmişini görüntüleme çalıştırmak içerir.</span><span class="sxs-lookup"><span data-stu-id="d4beb-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="d4beb-107">Erişebilir ve logic apps Visual Studio içinde yönetebilirsiniz önce yükleyin ve bu Visual Studio Araçları Azure Logic Apps için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d4beb-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4beb-108">Prerequisites</span></span>

* [<span data-ttu-id="d4beb-109">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d4beb-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="d4beb-110">[En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="d4beb-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="d4beb-111">Visual Studio bulut Gezgini</span><span class="sxs-lookup"><span data-stu-id="d4beb-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="d4beb-112">Merhaba katıştırılmış Tasarımcısı kullanırken erişim toohello web</span><span class="sxs-lookup"><span data-stu-id="d4beb-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="d4beb-113">Mantıksal uygulamalar için Visual Studio araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="d4beb-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="d4beb-114">Merhaba önkoşulları yüklendikten sonra karşıdan yükleyip hello Azure Logic Apps araçları Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="d4beb-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="d4beb-115">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-115">Open Visual Studio.</span></span> <span data-ttu-id="d4beb-116">Merhaba üzerinde **Araçları** menüsünde, select **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="d4beb-117">Merhaba genişletin **çevrimiçi** hello Visual Studio Galerisi çevrimiçi arama yapabilmeniz için kategori.</span><span class="sxs-lookup"><span data-stu-id="d4beb-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="d4beb-118">Göz atın veya arayın **Logic Apps** bulana kadar **Visual Studio için Azure Logic Apps Araçları**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="d4beb-119">toodownload ve yükleme hello uzantısı,'ı **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="d4beb-120">Yüklendikten sonra Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="d4beb-121">toodownload hello Azure Logic Apps araçları Visual Studio için doğrudan toohello Git [Visual Studio Market'te](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="d4beb-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="d4beb-122">Logic apps Cloud Explorer'da gözatın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="d4beb-123">tooopen Cloud Explorer hello üzerinde **Görünüm** menüsünde seçin **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="d4beb-124">Mantıksal uygulamanız için kaynak grubu veya kaynak türüne göre göz atın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="d4beb-125">Kaynak türüne göre göz atarsanız, Azure aboneliğinizi seçin, hello genişletin **Logic Apps** bölümünde ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4beb-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="d4beb-126">Kaynak grubu tarafından göz atarsanız, mantıksal uygulamanızı sahip hello kaynak grubunu genişletin ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4beb-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="d4beb-127">tooview komutları mantığı uygulamanız için mantıksal uygulamanızı sağ tıklayın ya da bulut Explorer hello altındaki hello seçin **Eylemler** menüsü.</span><span class="sxs-lookup"><span data-stu-id="d4beb-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Mantıksal uygulamanızı gözatın.](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="d4beb-129">Mantıksal uygulamanızı Logic Apps Tasarımcısı ile Düzenle</span><span class="sxs-lookup"><span data-stu-id="d4beb-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="d4beb-130">Bulut Gezgini'nden hello şu anda dağıtılmış mantıksal uygulama açabilirsiniz hello Azure portalında kullandığınız aynı Tasarımcısı.</span><span class="sxs-lookup"><span data-stu-id="d4beb-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="d4beb-131">tooedit bulut Gezgini'nde mantıksal uygulamanızı mantıksal uygulamanızı sağ tıklatın ve seçin **mantığı uygulama Düzenleyicisi ile açık**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="d4beb-132">toopublish, güncelleştirmelerinin toohello bulut, seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="d4beb-133">Yeni bir çalışma toostart seçin **tetikleyici çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-133">toostart a new run, choose **Run Trigger**.</span></span>

![Logic Apps Tasarımcısı](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="d4beb-135">Merhaba Tasarımcısı'ndan şunları da yapabilirsiniz **karşıdan** bir mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="d4beb-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="d4beb-136">Bu eylem otomatik olarak hello mantıksal uygulama tanımını parameterizes ve hello tanımı bir Azure Resource Manager dağıtım şablonu olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d4beb-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="d4beb-137">Bu dağıtım şablonu tooyour Azure kaynak grubu projesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4beb-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="d4beb-138">Mantıksal uygulamanızı çalıştırma geçmişi göz atın</span><span class="sxs-lookup"><span data-stu-id="d4beb-138">Browse your logic app run history</span></span>

<span data-ttu-id="d4beb-139">çalıştırma geçmişi mantığı uygulamanız için tooview hello mantıksal uygulamanızı sağ tıklatın ve seçin **açık çalıştırma geçmişi**.</span><span class="sxs-lookup"><span data-stu-id="d4beb-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="d4beb-140">tooreorder çalıştırma geçmişi hello özellikleri gösterilen, select hello sütun başlığını hiçbirinde temel.</span><span class="sxs-lookup"><span data-stu-id="d4beb-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![çalıştırma geçmişi](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="d4beb-142">hello çalıştırmak hello girişleri ve çıkışları her adımdan dahil olmak üzere sonuçları gözden geçirebilmeniz için çalıştırma geçmişi bir örneğinin tooshow hello örneklerinde Çalıştır hello birini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d4beb-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Geçmiş sonuçlarını, giriş ve çıkış adımları çalıştırın](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="d4beb-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4beb-144">Next steps</span></span>

* [<span data-ttu-id="d4beb-145">İlk mantıksal uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4beb-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="d4beb-146">Tasarım, derleme ve logic apps Visual Studio içinde dağıtma</span><span class="sxs-lookup"><span data-stu-id="d4beb-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="d4beb-147">Sık rastlanan örnekleri ve senaryoları inceleyin</span><span class="sxs-lookup"><span data-stu-id="d4beb-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="d4beb-148">Video: Azure Logic Apps ile iş süreçlerini otomatikleştirmek</span><span class="sxs-lookup"><span data-stu-id="d4beb-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="d4beb-149">Video: sistemlerinizi Azure Logic Apps ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d4beb-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
