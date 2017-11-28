---
title: "aaaAutomate Azure günlük analizi Microsoft Flow işler."
description: "Microsoft Flow nasıl kullanabileceğinizi öğrenin tooquickly hello Azure günlük analizi Bağlayıcısı'nı kullanarak yinelenebilir işlemleri otomatikleştirme."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="6473e-103">İçin Microsoft Flow hello bağlayıcı ile günlük analizi işlemlerini otomatikleştirmeyi</span><span class="sxs-lookup"><span data-stu-id="6473e-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="6473e-104">[Microsoft Flow](https://ms.flow.microsoft.com) Eylemler yüzlerce çok çeşitli hizmetlerini kullanarak otomatik toocreate iş akışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6473e-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="6473e-105">Bir eylem çıktısını farklı hizmetler arasında toocreate tümleştirme izin vererek giriş tooanother olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6473e-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="6473e-106">Hello Azure günlük analizi Bağlayıcısı Microsoft Flow için günlük analizi günlük aramalarda tarafından alınan veri dahil toobuild iş akışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6473e-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="6473e-107">Örneğin, Office 365'ten bir e-posta bildiriminin Microsoft Flow toouse günlük analizi veri kullanın, Visual Studio Team Services içinde oluşturma veya Slack iletisi.</span><span class="sxs-lookup"><span data-stu-id="6473e-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="6473e-108">Bir iş akışı, bir basit zamanlama veya bağlantılı hizmetindeki bir posta ya da bir tweet alındığında gibi bazı eylemleri tetikleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6473e-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="6473e-109">Microsoft Flow Hello Azure günlük analizi bağlayıcı çalışma yükseltilmiş toobe toohello yeni günlük analizi sorgu dilini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6473e-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="6473e-110">Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="6473e-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="6473e-111">Bu makalede Hello öğretici nasıl toocreate otomatik olarak gönderir bir akış hello günlük analizi günlük arama sonuçlarını e-posta, günlük analizi Microsoft Flow nasıl kullanabileceğiniz yalnızca bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="6473e-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="6473e-112">1. adım: bir akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6473e-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="6473e-113">Çok oturum[Microsoft Flow](http://flow.microsoft.com)seçip **My akar**.</span><span class="sxs-lookup"><span data-stu-id="6473e-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="6473e-114">Tıklatın **+ Oluştur boş**.</span><span class="sxs-lookup"><span data-stu-id="6473e-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="6473e-115">2. adım: akışınız için bir Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="6473e-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="6473e-116">Tıklatın **arama bağlayıcılar ve Tetikleyicileri yüzlerce**.</span><span class="sxs-lookup"><span data-stu-id="6473e-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="6473e-117">Tür **zamanlama** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="6473e-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="6473e-118">Seçin **zamanlama**ve ardından **çizelgesi - yinelenme**.</span><span class="sxs-lookup"><span data-stu-id="6473e-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="6473e-119">Merhaba, **sıklığı** kutusunda seçin **gün** ve hello **aralığı** kutusuna **1**.</span><span class="sxs-lookup"><span data-stu-id="6473e-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="6473e-120">![Microsoft Flow tetikleyici iletişim kutusu](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="6473e-121">3. adım: bir günlük analizi eylem ekleme</span><span class="sxs-lookup"><span data-stu-id="6473e-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="6473e-122">Tıklatın **+ yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6473e-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="6473e-123">Arama **oturum Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6473e-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="6473e-124">Tıklatın **Azure günlük analizi – sorgu çalıştırmak ve sonuçlarını görselleştirme**.</span><span class="sxs-lookup"><span data-stu-id="6473e-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="6473e-125">![Günlük analizi sorgu penceresi](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="6473e-126">4. adım: hello günlük analizi eylemi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6473e-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="6473e-127">Merhaba abonelik kimliği, kaynak grubu ve çalışma alanı adı dahil olmak üzere çalışma alanınızı Hello ayrıntılarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="6473e-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="6473e-128">Günlük analizi sorgu toohello aşağıdaki hello eklemek **sorgu** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6473e-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="6473e-129">Bu yalnızca bir örnek sorgu ve veri veren diğer tüm değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6473e-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="6473e-130">Seçin **HTML tablosu** hello için **grafik türü**.</span><span class="sxs-lookup"><span data-stu-id="6473e-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="6473e-131">![Günlük analizi eylemi](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="6473e-132">Adım 5: hello akış toosend e-posta yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6473e-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="6473e-133">Tıklatın **yeni adım**ve ardından **+ Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6473e-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="6473e-134">Arama **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="6473e-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="6473e-135">Tıklatın **Office 365 Outlook – bir e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="6473e-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="6473e-136">![Office 365 Outlook seçim penceresi](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="6473e-137">Bir alıcı Hello e-posta adresini hello belirtin **için** penceresi ve hello e-posta için bir konu **konu**.</span><span class="sxs-lookup"><span data-stu-id="6473e-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="6473e-138">Hello herhangi bir yere tıklayın **gövde** kutusu.</span><span class="sxs-lookup"><span data-stu-id="6473e-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="6473e-139">A **dinamik içerik** önceki Eylemler değerlerle penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="6473e-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="6473e-140">Seçin **gövde**.</span><span class="sxs-lookup"><span data-stu-id="6473e-140">Select **Body**.</span></span>  <span data-ttu-id="6473e-141">Merhaba hello günlük analizi eylemin hello sorgu sonuçlarını budur.</span><span class="sxs-lookup"><span data-stu-id="6473e-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="6473e-142">Tıklatın **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="6473e-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="6473e-143">Merhaba, **HTML'dir** kutusunda **Evet**.</span><span class="sxs-lookup"><span data-stu-id="6473e-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="6473e-144">![Office 365 e-posta yapılandırma penceresi](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="6473e-145">6. adım: Kaydetmek ve akışınız test</span><span class="sxs-lookup"><span data-stu-id="6473e-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="6473e-146">Merhaba, **Akış adı** kutusuna akışınız için bir ad ekleyin ve ardından **akışı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="6473e-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="6473e-147">![Akış Kaydet](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="6473e-148">Merhaba akış şimdi oluşturulur ve belirttiğiniz hello zamanlaması olan bir gün sonra çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="6473e-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="6473e-149">tooimmediately test hello akış tıklatın **Şimdi Çalıştır** ve ardından **akışı çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="6473e-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="6473e-150">![Akış çalıştırın](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="6473e-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="6473e-151">Merhaba akışı tamamlandığında, belirttiğiniz hello alıcının hello posta denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6473e-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="6473e-152">Gövde benzer toohello aşağıdakileri içeren bir posta almış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6473e-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Örnek e-posta](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="6473e-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6473e-154">Next steps</span></span>

- <span data-ttu-id="6473e-155">Daha fazla bilgi edinmek [günlük analizi aramaları oturum](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="6473e-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="6473e-156">Daha fazla bilgi edinmek [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6473e-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



