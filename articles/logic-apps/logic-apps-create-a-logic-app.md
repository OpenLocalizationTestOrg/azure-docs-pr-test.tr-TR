---
title: "Bulut uygulamaları ile bulut hizmetleri arasında ilk iş akışınızı oluşturma - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="374be-104">Bulut uygulamaları ile bulut hizmetleri arasında süreçleri otomatik hale getirmek için ilk mantıksal uygulama iş akışınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="374be-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="374be-105">[Azure Logic Apps](logic-apps-what-are-logic-apps.md) ile iş akışları oluşturup çalıştırdığınızda, herhangi bir kod yazmadan iş süreçlerini daha kolay ve hızlı bir şekilde otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="374be-106">Bu ilk örnekte, bir web sitesindeki yeni içerikleri belirlemek için RSS akışını denetleyen temel bir mantıksal uygulama iş akışı oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="374be-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="374be-107">Web sitesinin akışında yeni öğeler göründüğünde, mantıksal uygulama bir Outlook veya Gmail hesabından e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="374be-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="374be-108">Bir mantıksal uygulama oluşturup çalıştırmak için şu öğeler gerekir:</span><span class="sxs-lookup"><span data-stu-id="374be-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="374be-109">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="374be-109">An Azure subscription.</span></span> <span data-ttu-id="374be-110">Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="374be-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="374be-111">Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="374be-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="374be-112">Azure aboneliğiniz, mantıksal uygulama kullanımını faturalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="374be-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="374be-113">[Kullanım ölçümü](../logic-apps/logic-apps-pricing.md) ve [fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps) işlemlerinin Azure Logic Apps’te nasıl işlediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="374be-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="374be-114">Ayrıca, bu örnek şu öğeleri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="374be-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="374be-115">Bir Outlook.com, Office 365 Outlook veya Gmail hesabı</span><span class="sxs-lookup"><span data-stu-id="374be-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="374be-116">Kişisel bir [Microsoft hesabınız](https://account.microsoft.com/account) varsa Outlook.com hesabınız vardır.</span><span class="sxs-lookup"><span data-stu-id="374be-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="374be-117">Aksi takdirde, bir Azure iş veya okul hesabınız varsa **Office 365 Outlook** hesabınız vardır.</span><span class="sxs-lookup"><span data-stu-id="374be-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="374be-118">Web sitesinin RSS akışının bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="374be-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="374be-119">Bu örnekte [CNN.com web sitesindeki en önemli haberler için RSS akışı](http://rss.cnn.com/rss/cnn_topstories.rss) kullanılmıştır: `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="374be-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="374be-120">İş akışınızı başlatan bir tetikleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="374be-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="374be-121">[*Tetikleyici*](./logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınızı başlatan bir olaydır ve mantıksal uygulamanız için gereken ilk öğedir.</span><span class="sxs-lookup"><span data-stu-id="374be-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="374be-122">[Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="374be-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="374be-123">Resimde gösterildiği gibi, sol menüden **Yeni** > **Kurumsal Tümleştirme** > **Mantıksal Uygulama**’yı seçin:</span><span class="sxs-lookup"><span data-stu-id="374be-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure portalı, Yeni, Kurumsal Tümleştirme, Mantıksal Uygulama](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="374be-125">Ayrıca **Yeni**’yi seçebilir, ardından arama kutusuna `logic app` yazıp Enter tuşuna basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="374be-126">Ardından **Mantıksal Uygulama** > **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="374be-127">Mantıksal uygulamanızı adlandırın ve Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="374be-128">Şimdi, ilgili Azure kaynaklarını düzenleyip yönetmenize yardımcı olan bir Azure kaynak grubu oluşturun veya seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="374be-129">Son olarak, mantıksal uygulamanızı barındıracak veri merkezi konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="374be-130">Hazır olduğunuzda **Panoya sabitle** ve ardından **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Mantıksal uygulama ayrıntıları](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="374be-132">**Panoya sabitle**’yi seçtiğinizde, mantıksal uygulamanız dağıtıldıktan sonra Azure panosunda gösterilir ve otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="374be-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="374be-133">Mantıksal uygulamanız panoda görünmüyorsa, **Tüm kaynaklar** kutucuğunda **Daha Fazla Göster**’ü ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="374be-134">Veya sol menüden **Diğer hizmetler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="374be-135">**Kurumsal Tümleştirme** altında **Logic Apps**’ı belirleyip mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="374be-136">Mantıksal uygulamanızı ilk kez açtığınızda, Mantıksal Uygulama Tasarımcısı başlamak için kullanabileceğiniz şablonları gösterir.</span><span class="sxs-lookup"><span data-stu-id="374be-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="374be-137">Mantıksal uygulamanızı sıfırdan oluşturabilmek için şimdilik **Boş Mantıksal Uygulama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="374be-138">Mantıksal Uygulama Tasarımcısı'nı açar ve kullanılabilir hizmetler gösterir ve *Tetikleyicileri* , mantıksal uygulamanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="374be-139">Arama kutusuna `RSS` yazıp şu tetikleyiciyi seçin: **RSS - Akış öğesi yayımlandığında**</span><span class="sxs-lookup"><span data-stu-id="374be-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS tetikleyicisi](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="374be-141">İzlemek istediğiniz web sitesinin RSS akışına ait bağlantıyı girin.</span><span class="sxs-lookup"><span data-stu-id="374be-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="374be-142">Ayrıca **Sıklık** ve **Aralık** değerlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="374be-143">Bu ayarlar mantıksal uygulamanızın yeni öğeleri ne sıklıkla denetleyeceğini belirler ve bu süre boyunca bulunan tüm öğeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="374be-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="374be-144">Bu örnekte her gün CNN web sitesinde yayımlanan en önemli haberlere bakalım.</span><span class="sxs-lookup"><span data-stu-id="374be-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Tetikleyicinin RSS akışı, sıklık ve aralık ayarını yapma](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="374be-146">Çalışmanızı şimdilik kaydedin.</span><span class="sxs-lookup"><span data-stu-id="374be-146">Save your work for now.</span></span> <span data-ttu-id="374be-147">(Tasarımcı komut çubuğunda **Kaydet**’i seçin.)</span><span class="sxs-lookup"><span data-stu-id="374be-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Mantıksal uygulamanızı kaydetme](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="374be-149">Mantıksal uygulamanızı kaydettiğinizde etkin hale gelir, ancak şu anda mantıksal uygulamanız yalnızca belirtilen RSS akışındaki yeni öğeleri denetler.</span><span class="sxs-lookup"><span data-stu-id="374be-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="374be-150">Bu örneği daha kullanışlı hale getirmek için tetikleyici başlatıldıktan sonra mantıksal uygulamanızın gerçekleştireceği bir eylem ekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="374be-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="374be-151">Tetikleyicinize yanıt veren bir eylem ekleme</span><span class="sxs-lookup"><span data-stu-id="374be-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="374be-152">[*Eylem*](./logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="374be-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="374be-153">Mantıksal uygulamanıza bir tetikleyici ekledikten sonra, bu tetikleyici tarafından oluşturulan işlemleri gerçekleştirmek için bir eylem ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="374be-154">Bu örnekte, web sitesinin RSS akışında yeni öğeler göründüğünde e-posta gönderen bir eylem ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="374be-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="374be-155">Tasarımcıda, resimde gösterildiği gibi tetikleyicinizin altındaki **Yeni adım** > **Eylem ekle** öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="374be-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Eylem ekleme](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="374be-157">Tasarımcı, tetikleyiciniz başlatıldığında gerçekleştirilecek bir eylem seçebilmeniz için [kullanılabilir bağlayıcıları](../connectors/apis-list.md) gösterir.</span><span class="sxs-lookup"><span data-stu-id="374be-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="374be-158">E-posta hesabınıza bağlı olarak, Outlook veya Gmail’e yönelik adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="374be-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="374be-159">Outlook hesabınızdan e-posta göndermek için arama kutusuna `outlook` girin.</span><span class="sxs-lookup"><span data-stu-id="374be-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="374be-160">**Hizmetler** altında kişisel Microsoft hesaplarınız için **Outlook.com** veya Azure iş ya da okul hesapları için **Office 365 Outlook**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="374be-161">**Eylemler** altında **E-posta gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-161">Under **Actions**, select **Send an email**.</span></span>

       ![Outlook "E-posta gönder" eylemini seçin](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="374be-163">Gmail hesabınızdan e-posta göndermek için arama kutusuna `gmail` girin.</span><span class="sxs-lookup"><span data-stu-id="374be-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="374be-164">**Eylemler** altında **E-posta gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-164">Under **Actions**, select **Send email**.</span></span>

       !["Gmail - E-posta gönder" öğesini seçin](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="374be-166">Kimlik bilgileriniz istendiğinde, e-posta hesabınıza ait kullanıcı adı ve parolayla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="374be-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="374be-167">Bu eylemin hedef e-posta adresi gibi ayrıntılarını belirtin ve e-postaya eklenecek verilerin parametrelerini seçin, örneğin:</span><span class="sxs-lookup"><span data-stu-id="374be-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![E-postaya eklenecek verileri seçme](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="374be-169">Outlook’u seçerseniz mantıksal uygulamanız bu örnektekine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="374be-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Tamamlanan mantıksal uygulama](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="374be-171">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="374be-171">Save your changes.</span></span> <span data-ttu-id="374be-172">(Tasarımcı komut çubuğunda **Kaydet**’i seçin.)</span><span class="sxs-lookup"><span data-stu-id="374be-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="374be-173">Mantıksal uygulamanızı test için el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="374be-174">Tasarımcı komut çubuğunda **Çalıştır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="374be-175">Ya da mantıksal uygulamanızın ayarladığınız zamanlamaya göre RSS akışını denetlemesine izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="374be-176">Mantıksal uygulamanız yeni öğeler bulursa, mantıksal uygulama seçtiğiniz verileri içeren e-postayı gönderir.</span><span class="sxs-lookup"><span data-stu-id="374be-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="374be-177">Yeni öğe bulunmazsa, mantıksal uygulamanız e-posta gönderen eylemi atlar.</span><span class="sxs-lookup"><span data-stu-id="374be-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="374be-178">Mantıksal uygulamanızın çalışma ve tetikleyici geçmişini izlemek ve denetlemek için, mantıksal uygulama menüsünde **Genel Bakış**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Mantıksal uygulamanın çalışma ve tetikleyici geçmişini izleme ve görüntüleme](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="374be-180">Beklediğiniz verileri bulamazsanız, komut çubuğunda **Yenile**’yi seçmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="374be-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="374be-181">Mantıksal uygulamanızın durumu veya çalışma ve tetikleyici geçmişi hakkında daha fazla bilgi almak için bkz. [Mantıksal uygulamanızla ilgili sorun giderme](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="374be-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="374be-182">Mantıksal uygulamanız siz kapatana kadar çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="374be-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="374be-183">Uygulamanızı şimdilik kapatmak için, mantıksal uygulama menüsünde **Genel Bakış**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="374be-184">Komut çubuğunda **Devre Dışı Bırak**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="374be-185">Tebrikler, ilk temel mantıksal uygulamanızı oluşturup çalıştırdınız.</span><span class="sxs-lookup"><span data-stu-id="374be-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="374be-186">Ayrıca, herhangi bir kod kullanmadan, süreçleri otomatik hale getiren iş akışlarını ne kadar kolay oluşturabileceğinizi ve bulut uygulamaları ile bulut hizmetlerini tümleştirmeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="374be-187">Mantıksal uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="374be-187">Manage your logic app</span></span>

<span data-ttu-id="374be-188">Uygulamanızı yönetmek için durumu denetleme, düzenleme, geçmişi görüntüleme, kapatma ya da mantıksal uygulamanızı silme gibi görevler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374be-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="374be-189">[Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="374be-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="374be-190">Sol menüden **Diğer hizmetler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="374be-191">**Kurumsal Tümleştirme** altında **Logic Apps**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="374be-192">Mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-192">Select your logic app.</span></span> 

   <span data-ttu-id="374be-193">Mantıksal uygulama menüsünde şu mantıksal uygulama yönetim görevlerini bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="374be-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="374be-194">Görev</span><span class="sxs-lookup"><span data-stu-id="374be-194">Task</span></span>|<span data-ttu-id="374be-195">Adımlar</span><span class="sxs-lookup"><span data-stu-id="374be-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="374be-196">Uygulamanızın durumunu, yürütme geçmişini ve genel bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="374be-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="374be-197">**Genel Bakış**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="374be-198">Uygulamanızı düzenleme</span><span class="sxs-lookup"><span data-stu-id="374be-198">Edit your app</span></span> | <span data-ttu-id="374be-199">**Mantıksal Uygulama Tasarımcısı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="374be-200">Uygulamanızın iş akışı JSON tanımını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="374be-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="374be-201">**Mantıksal Uygulama Kod Görünümü**’nü seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="374be-202">Mantıksal uygulamanız üzerinde gerçekleştirilen işlemleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="374be-202">View operations performed on your logic app</span></span> | <span data-ttu-id="374be-203">**Ekinlik günlüğü**’nü seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="374be-204">Mantıksal uygulamanızın geçmiş sürümlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="374be-204">View past versions for your logic app</span></span> | <span data-ttu-id="374be-205">**Sürümler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="374be-206">Uygulamanızı geçici olarak kapatma</span><span class="sxs-lookup"><span data-stu-id="374be-206">Turn off your app temporarily</span></span> | <span data-ttu-id="374be-207">**Genel Bakış**’ı seçin, ardından komut çubuğunda **Devre Dışı Bırak**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="374be-208">Uygulamanızı silme</span><span class="sxs-lookup"><span data-stu-id="374be-208">Delete your app</span></span> | <span data-ttu-id="374be-209">**Genel Bakış**’ı seçin, ardından komut çubuğunda **Sil**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="374be-210">Mantıksal uygulamanızın adını girip **Sil**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="374be-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="374be-211">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="374be-211">Get help</span></span>

<span data-ttu-id="374be-212">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını öğrenmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="374be-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="374be-213">Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="374be-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="374be-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="374be-214">Next steps</span></span>

*  [<span data-ttu-id="374be-215">Koşul ekleme ve iş akışları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="374be-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="374be-216">Mantıksal uygulama şablonları</span><span class="sxs-lookup"><span data-stu-id="374be-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="374be-217">Azure Resource Manager şablonlarından mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="374be-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
