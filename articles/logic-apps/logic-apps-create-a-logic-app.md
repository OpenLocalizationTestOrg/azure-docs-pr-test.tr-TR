---
title: "aaaCreate bulut uygulamalarını & Bulut Hizmetleri - Azure mantıksal uygulamaları arasındaki ilk iş akışınızın | Microsoft Docs"
description: "Azure Logic Apps’te iş akışları oluşturup çalıştırarak, sistem tümleştirmeden kuruluş uygulaması tümleştirmeye (EAI) kadar tüm senaryolar için iş süreçlerini otomatik hale getirin"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "iş akışı, bulut uygulamaları, bulut hizmetleri, iş süreçleri, sistem tümleştirme, kuruluş uygulaması tümleştirme, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="6d0d9-104">İş akışı tooautomate işlemleri bulut uygulamaları ve bulut hizmetleri arasında ilk mantıksal uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d0d9-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="6d0d9-105">[Azure Logic Apps](logic-apps-what-are-logic-apps.md) ile iş akışları oluşturup çalıştırdığınızda, herhangi bir kod yazmadan iş süreçlerini daha kolay ve hızlı bir şekilde otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="6d0d9-106">Bu ilk örnek nasıl toocreate bir Web sitesinde yeni içerik için bir RSS denetler bir temel mantığı uygulama iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="6d0d9-107">Yeni öğeler hello Web sitesinin akışta görüntülendiğinde, hello mantıksal uygulama bir Outlook veya Gmail hesaptan e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="6d0d9-108">toocreate ve Çalıştır bir mantıksal uygulama, bu öğeler gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="6d0d9-109">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-109">An Azure subscription.</span></span> <span data-ttu-id="6d0d9-110">Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6d0d9-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="6d0d9-111">Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="6d0d9-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="6d0d9-112">Azure aboneliğiniz, mantıksal uygulama kullanımını faturalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="6d0d9-113">[Kullanım ölçümü](../logic-apps/logic-apps-pricing.md) ve [fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps) işlemlerinin Azure Logic Apps’te nasıl işlediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="6d0d9-114">Ayrıca, bu örnek şu öğeleri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="6d0d9-115">Bir Outlook.com, Office 365 Outlook veya Gmail hesabı</span><span class="sxs-lookup"><span data-stu-id="6d0d9-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="6d0d9-116">Kişisel bir [Microsoft hesabınız](https://account.microsoft.com/account) varsa Outlook.com hesabınız vardır.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="6d0d9-117">Aksi takdirde, bir Azure iş veya okul hesabınız varsa **Office 365 Outlook** hesabınız vardır.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="6d0d9-118">Bir bağlantı tooa Web sitesinin RSS akışı.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="6d0d9-119">Bu örnek hello kullanır [RSS hello CNN.com Web sitesinden için üst hikayeleri akışı](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="6d0d9-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="6d0d9-120">İş akışınızı başlatan bir tetikleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="6d0d9-121">A [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , logic app iş akışınızı başlatır bir olaydır ve mantıksal uygulamanızı gerektiren hello ilk öğedir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="6d0d9-122">İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="6d0d9-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="6d0d9-123">Merhaba sol menüden seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure portalı, Yeni, Kurumsal Tümleştirme, Mantıksal Uygulama](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="6d0d9-125">Ayrıca seçebilirsiniz **yeni**, hello arama kutusuna yazın `logic app`, ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="6d0d9-126">Ardından **Mantıksal Uygulama** > **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="6d0d9-127">Mantıksal uygulamanızı adlandırın ve Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="6d0d9-128">Şimdi, ilgili Azure kaynaklarını düzenleyip yönetmenize yardımcı olan bir Azure kaynak grubu oluşturun veya seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="6d0d9-129">Son olarak, mantıksal uygulamanızı barındırmak için hello datacenter konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="6d0d9-130">Hazır olduğunuzda, seçin **PIN toodashboard** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Mantıksal uygulama ayrıntıları](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="6d0d9-132">Seçtiğinizde, **PIN toodashboard**, mantıksal uygulamanızı Azure Pano hello üzerinde dağıtımdan sonra görünür ve otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="6d0d9-133">Mantıksal uygulamanızı hello Panoda hello görünmüyor varsa **tüm kaynakları** döşeme, seçin **daha görmek**, mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="6d0d9-134">Veya hello sol menüsünde, **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="6d0d9-135">**Kurumsal Tümleştirme** altında **Logic Apps**’ı belirleyip mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="6d0d9-136">Mantıksal uygulamanızı hello için ilk kez açtığınızda, hello mantığı Uygulama Tasarımcısı şablonları başlatılan tooget kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="6d0d9-137">Mantıksal uygulamanızı sıfırdan oluşturabilmek için şimdilik **Boş Mantıksal Uygulama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="6d0d9-138">Merhaba mantığı Uygulama Tasarımcısı açılır ve kullanılabilir hizmetler gösterir ve *Tetikleyicileri* , mantıksal uygulamanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="6d0d9-139">Merhaba arama kutusuna yazın `RSS`, bu Tetikleyici seçin: **bir akış öğesi yayımlandığında RSS -**</span><span class="sxs-lookup"><span data-stu-id="6d0d9-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS tetikleyicisi](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="6d0d9-141">Merhaba bağlantısı için hello Web sitesinin RSS akışı tootrack istediğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="6d0d9-142">Ayrıca **Sıklık** ve **Aralık** değerlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="6d0d9-143">Bu ayarlar mantıksal uygulamanızın yeni öğeleri ne sıklıkla denetleyeceğini belirler ve bu süre boyunca bulunan tüm öğeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="6d0d9-144">Bu örnekte, şimdi popüler konular için her gün toohello CNN Web sitesine gönderilen denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Tetikleyicinin RSS akışı, sıklık ve aralık ayarını yapma](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="6d0d9-146">Çalışmanızı şimdilik kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-146">Save your work for now.</span></span> <span data-ttu-id="6d0d9-147">(Merhaba Tasarımcı komut çubuğunda seçin **kaydetmek**.)</span><span class="sxs-lookup"><span data-stu-id="6d0d9-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Mantıksal uygulamanızı kaydetme](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="6d0d9-149">Kaydettiğiniz, mantıksal uygulamanızı Canlı gider, ancak şu anda, mantıksal uygulamanızı yalnızca yeni öğe denetler hello RSS akışı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="6d0d9-150">Bu örnek, tetikleyici sonra mantıksal uygulamanızı gerçekleştiren eylem eklediğimiz daha kullanışlı toomake ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="6d0d9-151">Tooyour tetikleyici yanıtlayan Eylem Ekle</span><span class="sxs-lookup"><span data-stu-id="6d0d9-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="6d0d9-152">[*Eylem*](./logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="6d0d9-153">Bir tetikleyici tooyour mantıksal uygulama ekledikten sonra Bu tetikleyici tarafından oluşturulan verilerle bir eylem tooperform işlemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="6d0d9-154">Bizim örneğimizde, biz şimdi yeni öğeler görüntülendiğinde hello Web sitesinin RSS akışı e-posta gönderen bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="6d0d9-155">Tetikleyici altında hello Tasarımcısı'nda seçin **yeni adım** > **Eylem Ekle** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Eylem ekleme](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="6d0d9-157">Merhaba Tasarımcı gösterir [kullanılabilir Bağlayıcılar](../connectors/apis-list.md) , tetikleyici başlatıldığında bir eylem tooperform seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="6d0d9-158">E-posta hesabınıza bağlı olarak, Outlook veya Gmail hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="6d0d9-159">Merhaba arama kutusuna, Outlook hesabınızdan toosend e-posta girin `outlook`.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="6d0d9-160">**Hizmetler** altında kişisel Microsoft hesaplarınız için **Outlook.com** veya Azure iş ya da okul hesapları için **Office 365 Outlook**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="6d0d9-161">**Eylemler** altında **E-posta gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-161">Under **Actions**, select **Send an email**.</span></span>

       ![Outlook "E-posta gönder" eylemini seçin](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="6d0d9-163">Merhaba arama kutusuna, Gmail hesabınızdan toosend e-posta girin `gmail`.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="6d0d9-164">**Eylemler** altında **E-posta gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-164">Under **Actions**, select **Send email**.</span></span>

       !["Gmail - E-posta gönder" öğesini seçin](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="6d0d9-166">Kimlik bilgileri istendiğinde, e-posta hesabınız için hello kullanıcı adı ve parolayla oturum.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="6d0d9-167">Merhaba hedef e-posta adresi gibi bu eylemin Hello ayrıntıları sağlayın ve hello veri tooinclude hello parametrelerini hello e-postada, örneğin seçin:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![E-posta ile veri tooinclude seçin](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="6d0d9-169">Outlook’u seçerseniz mantıksal uygulamanız bu örnektekine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Tamamlanan mantıksal uygulama](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="6d0d9-171">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-171">Save your changes.</span></span> <span data-ttu-id="6d0d9-172">(Merhaba Tasarımcı komut çubuğunda seçin **kaydetmek**.)</span><span class="sxs-lookup"><span data-stu-id="6d0d9-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="6d0d9-173">Mantıksal uygulamanızı test için el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="6d0d9-174">Merhaba Tasarımcı komut çubuğunda seçin **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="6d0d9-175">Aksi takdirde, ayarladığınız hello zamanlamaya göre RSS akışı hello belirtilen denetleyin mantıksal uygulamanızı izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="6d0d9-176">Mantıksal uygulamanızı yeni öğeler bulursa, hello mantıksal uygulama, seçilen verileri içeren e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="6d0d9-177">Yeni öğe bulunursa, mantıksal uygulamanızı e-posta gönderir hello eylem atlar.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="6d0d9-178">toomonitor seçip mantıksal uygulamanızı çalıştıran ve tetikleyecek mantığı uygulama menünüzde geçmişi onay **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Mantıksal uygulamanın çalışma ve tetikleyici geçmişini izleme ve görüntüleme](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="6d0d9-180">Merhaba komut çubuğunda, beklediğiniz hello veri bulamazsanız seçmeyi deneyin **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="6d0d9-181">toolearn mantığı uygulamanızın durumu hakkında daha fazla veya çalıştırın ve geçmiş veya toodiagnose mantıksal uygulamanızı tetiklemek, bkz: [mantıksal uygulamanızı sorun giderme](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="6d0d9-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="6d0d9-182">Mantıksal uygulamanız siz kapatana kadar çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="6d0d9-183">Uygulamanız için mantığı uygulama menünüzde şimdi kapatmak tooturn seçin **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="6d0d9-184">Merhaba komut çubuğunda seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="6d0d9-185">Tebrikler, ilk temel mantıksal uygulamanızı oluşturup çalıştırdınız.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="6d0d9-186">Ayrıca, herhangi bir kod kullanmadan, süreçleri otomatik hale getiren iş akışlarını ne kadar kolay oluşturabileceğinizi ve bulut uygulamaları ile bulut hizmetlerini tümleştirmeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="6d0d9-187">Mantıksal uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-187">Manage your logic app</span></span>

<span data-ttu-id="6d0d9-188">toomanage, uygulamanızın hello durumunu denetlemek, düzenleme, görüntüleme geçmişi, kapatmak veya mantıksal uygulamanızı silme gibi görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="6d0d9-189">İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="6d0d9-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="6d0d9-190">Merhaba sol menüsünde, **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="6d0d9-191">**Kurumsal Tümleştirme** altında **Logic Apps**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="6d0d9-192">Mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-192">Select your logic app.</span></span> 

   <span data-ttu-id="6d0d9-193">Merhaba mantığı uygulama menüsünde, bu mantığı uygulama yönetim görevlerini bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d0d9-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="6d0d9-194">Görev</span><span class="sxs-lookup"><span data-stu-id="6d0d9-194">Task</span></span>|<span data-ttu-id="6d0d9-195">Adımlar</span><span class="sxs-lookup"><span data-stu-id="6d0d9-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="6d0d9-196">Uygulamanızın durumunu, yürütme geçmişini ve genel bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="6d0d9-197">**Genel Bakış**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="6d0d9-198">Uygulamanızı düzenleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-198">Edit your app</span></span> | <span data-ttu-id="6d0d9-199">**Mantıksal Uygulama Tasarımcısı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="6d0d9-200">Uygulamanızın iş akışı JSON tanımını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="6d0d9-201">**Mantıksal Uygulama Kod Görünümü**’nü seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="6d0d9-202">Mantıksal uygulamanız üzerinde gerçekleştirilen işlemleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-202">View operations performed on your logic app</span></span> | <span data-ttu-id="6d0d9-203">**Ekinlik günlüğü**’nü seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="6d0d9-204">Mantıksal uygulamanızın geçmiş sürümlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-204">View past versions for your logic app</span></span> | <span data-ttu-id="6d0d9-205">**Sürümler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="6d0d9-206">Uygulamanızı geçici olarak kapatma</span><span class="sxs-lookup"><span data-stu-id="6d0d9-206">Turn off your app temporarily</span></span> | <span data-ttu-id="6d0d9-207">Seçin **genel bakış**, hello komut çubuğunda seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="6d0d9-208">Uygulamanızı silme</span><span class="sxs-lookup"><span data-stu-id="6d0d9-208">Delete your app</span></span> | <span data-ttu-id="6d0d9-209">Seçin **genel bakış**, hello komut çubuğunda seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="6d0d9-210">Mantıksal uygulamanızın adını girip **Sil**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="6d0d9-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="6d0d9-211">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="6d0d9-211">Get help</span></span>

<span data-ttu-id="6d0d9-212">tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="6d0d9-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="6d0d9-213">toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="6d0d9-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d0d9-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d0d9-214">Next steps</span></span>

*  [<span data-ttu-id="6d0d9-215">Koşul ekleme ve iş akışları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6d0d9-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="6d0d9-216">Mantıksal uygulama şablonları</span><span class="sxs-lookup"><span data-stu-id="6d0d9-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="6d0d9-217">Azure Resource Manager şablonlarından mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d0d9-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
