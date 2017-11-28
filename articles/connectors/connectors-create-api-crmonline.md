---
title: "Azure mantığı uygulamalardan aaaConnect tooDynamics 365 (çevrimiçi) | Microsoft Docs"
description: "Dynamics 365 (çevrimiçi) varlıklar hello hello Dynamics 365 Bağlayıcısı tarafından sağlanan API aracılığıyla yönetmek uygulama iş akışları mantığı oluşturun"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="381f2-103">Mantıksal uygulama akışlarından tooDynamics 365 Bağlan</span><span class="sxs-lookup"><span data-stu-id="381f2-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="381f2-104">Logic Apps ile tooDynamics (çevrimiçi) 365 bağlama ve kayıtları oluşturma, öğeleri güncelleştirmek veya kayıtlar listesi döndüren kullanışlı iş akışları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="381f2-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="381f2-105">Merhaba Dynamics 365 Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="381f2-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="381f2-106">İş akışınız hello verileri (çevrimiçi) Dynamics 365 Al esas oluşturun.</span><span class="sxs-lookup"><span data-stu-id="381f2-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="381f2-107">Bir yanıt ve daha sonra hello çıkış diğer eylemler için kullanılabilir hale eylemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="381f2-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="381f2-108">Örneğin, bir öğe Dynamics 365'te (çevrimiçi) güncelleştirildiğinde, Office 365 kullanılarak bir e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="381f2-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="381f2-109">Bu konu, nasıl toocreate bir mantıksal uygulama, bir görev Dynamics 365 oluşturduğunu gösterir. yeni bir sağlama Dynamics 365 oluşturulduğu zaman.</span><span class="sxs-lookup"><span data-stu-id="381f2-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="381f2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="381f2-110">Prerequisites</span></span>
* <span data-ttu-id="381f2-111">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="381f2-111">An Azure account.</span></span>
* <span data-ttu-id="381f2-112">Dynamics 365 (çevrimiçi) hesabı.</span><span class="sxs-lookup"><span data-stu-id="381f2-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="381f2-113">Yeni bir sağlama Dynamics 365'te oluşturduğunuzda bir görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="381f2-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="381f2-114">[İçinde tooAzure oturum](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="381f2-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="381f2-115">Hello Azure arama kutusuna yazın `Logic apps`, ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="381f2-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Logic Apps Bul](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="381f2-117">Altında **Logic apps**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="381f2-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp Ekle](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="381f2-119">toocreate hello mantıksal uygulama, tam hello **adı**, **abonelik**, **kaynak grubu**, ve **konumu** alanları ve 'ıtıklatın **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="381f2-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="381f2-120">Merhaba yeni mantıksal uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-120">Select hello new logic app.</span></span> <span data-ttu-id="381f2-121">Merhaba aldığınızda **dağıtımı başarılı oldu** bildirimi tıklatın **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="381f2-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="381f2-122">Altında **geliştirme araçları**, tıklatın **mantığı Uygulama Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="381f2-123">Merhaba şablon listesinde tıklayın **boş mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="381f2-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="381f2-124">Merhaba arama kutusuna yazın `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="381f2-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="381f2-125">Hello Dynamics 365 listesi tetikler, seçin **Dynamics 365 bir kayıt oluşturulduğunda –**.</span><span class="sxs-lookup"><span data-stu-id="381f2-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="381f2-126">İstendiğinde toosign tooDynamics 365 de varsa, bunu şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="381f2-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="381f2-127">Aşağıdaki bilgilerle hello Hello tetikleyici ayrıntıları girin:</span><span class="sxs-lookup"><span data-stu-id="381f2-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="381f2-128">**Kuruluş adı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-128">**Organization Name**.</span></span> <span data-ttu-id="381f2-129">Merhaba mantığı uygulama toolisten istediğiniz hello Dynamics 365 örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="381f2-130">**Varlık adı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-130">**Entity Name**.</span></span> <span data-ttu-id="381f2-131">Toolisten için istediğiniz hello varlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="381f2-132">Bu olay bir tetikleyici toostart hello mantıksal uygulama davranır.</span><span class="sxs-lookup"><span data-stu-id="381f2-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="381f2-133">Bu kılavuzda **müşteri adayları** seçilir.</span><span class="sxs-lookup"><span data-stu-id="381f2-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="381f2-134">**Ne sıklıkta toocheck öğeleri istiyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="381f2-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="381f2-135">Bu değerleri ne sıklıkta ayarlayın hello mantıksal uygulama güncelleştirmeleri ilgili toohello tetikleyici için denetler.</span><span class="sxs-lookup"><span data-stu-id="381f2-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="381f2-136">güncelleştirmeleri üç dakikada toocheck Hello varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="381f2-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="381f2-137">**Sıklık**.</span><span class="sxs-lookup"><span data-stu-id="381f2-137">**Frequency**.</span></span> <span data-ttu-id="381f2-138">Saniye, dakika, saat veya gün seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="381f2-139">**Aralığı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-139">**Interval**.</span></span> <span data-ttu-id="381f2-140">Merhaba saniye, dakika, saat veya toopass hello sonraki onay önce istediğiniz gün sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="381f2-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Mantıksal uygulama tetikleyici ayrıntıları](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="381f2-142">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="381f2-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="381f2-143">Merhaba arama kutusuna yazın `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="381f2-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="381f2-144">Merhaba eylemler listesinden **Dynamics 365 – yeni bir kayıt oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="381f2-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="381f2-145">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="381f2-145">Enter hello following information:</span></span>

    * <span data-ttu-id="381f2-146">**Kuruluş adı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-146">**Organization Name**.</span></span> <span data-ttu-id="381f2-147">Merhaba Dynamics 365 örneği hello akış toocreate hello kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="381f2-148">Bu örnek aynı hello toobe yok bildirim burada hello olay tetiklenir gelen örneği.</span><span class="sxs-lookup"><span data-stu-id="381f2-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="381f2-149">**Varlık adı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-149">**Entity Name**.</span></span> <span data-ttu-id="381f2-150">Merhaba olay tetiklendiğinde toocreate bir kaydı istediğiniz hello varlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="381f2-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="381f2-151">Bu kılavuzda **görevleri** seçilir.</span><span class="sxs-lookup"><span data-stu-id="381f2-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="381f2-152">Tıklatın hello **konu** görüntülenen kutusunda.</span><span class="sxs-lookup"><span data-stu-id="381f2-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="381f2-153">Görüntülenen hello dinamik içerik listesinden, bu alanlardan birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="381f2-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="381f2-154">**Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-154">**Last Name**.</span></span> <span data-ttu-id="381f2-155">Merhaba görev kayıt oluşturulduğunda bu alanın seçilmesi hello görevin hello Konu alanına hello Soyadı hello sağlama için ekler.</span><span class="sxs-lookup"><span data-stu-id="381f2-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="381f2-156">**Konu**.</span><span class="sxs-lookup"><span data-stu-id="381f2-156">**Topic**.</span></span> <span data-ttu-id="381f2-157">Bu alan ekler hello konu alan hello görevin hello Konu alanına hello sağlama için seçerek, ne zaman hello görev kaydı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="381f2-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="381f2-158">Tıklatın **konu** tooadd bu toohello **konu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="381f2-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Mantıksal uygulama oluşturma yeni kayıt ayrıntıları](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="381f2-160">Merhaba mantığı uygulama Designer araç çubuğundan, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="381f2-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="381f2-162">toostart hello mantıksal uygulama'ı tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="381f2-162">toostart hello Logic App, click **Run**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="381f2-164">Artık Dynamics 365 satış sağlama kaydı oluşturun ve akışınız eylem bakın!</span><span class="sxs-lookup"><span data-stu-id="381f2-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="381f2-165">Bir mantıksal uygulama adımı için Gelişmiş seçenekleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="381f2-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="381f2-166">bir mantıksal uygulama adımı toofilter verileri nasıl tıklatın toospecify **Gelişmiş Seçenekleri Göster** sorgu tarafından filtre veya düzeni sonra bu adımda, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="381f2-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="381f2-167">Örneğin, bir filtre sorgu tooget yalnızca etkin hesapları kullanın ve hello hesap adıyla sipariş.</span><span class="sxs-lookup"><span data-stu-id="381f2-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="381f2-168">tooperform bu görev, hello OData filtre sorgusu girin `statuscode eq 1`seçip **hesap adı** hello dinamik içerik listesinden.</span><span class="sxs-lookup"><span data-stu-id="381f2-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="381f2-169">Daha fazla bilgi: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) ve [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="381f2-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Gelişmiş Seçenekleri mantıksal uygulama](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="381f2-171">Gelişmiş seçenekleri kullanırken en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="381f2-171">Best practices when using advanced options</span></span>

<span data-ttu-id="381f2-172">Değer tooa alanı eklediğinizde, bir değer yazın ya da hello dinamik içerik listeden bir değer seçin hello alan türüyle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="381f2-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="381f2-173">Alan türü</span><span class="sxs-lookup"><span data-stu-id="381f2-173">Field type</span></span>  |<span data-ttu-id="381f2-174">Nasıl toouse</span><span class="sxs-lookup"><span data-stu-id="381f2-174">How toouse</span></span>  |<span data-ttu-id="381f2-175">Burada toofind</span><span class="sxs-lookup"><span data-stu-id="381f2-175">Where toofind</span></span>  |<span data-ttu-id="381f2-176">Ad</span><span class="sxs-lookup"><span data-stu-id="381f2-176">Name</span></span>  |<span data-ttu-id="381f2-177">Veri türü</span><span class="sxs-lookup"><span data-stu-id="381f2-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="381f2-178">Metin alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-178">Text fields</span></span>|<span data-ttu-id="381f2-179">Metin alanları tek satırlık bir metin veya metin türü alan dinamik içerik gerektirir.</span><span class="sxs-lookup"><span data-stu-id="381f2-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="381f2-180">Örnekler hello kategori ve alt kategori alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="381f2-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="381f2-181">Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="381f2-182">category</span><span class="sxs-lookup"><span data-stu-id="381f2-182">category</span></span> |<span data-ttu-id="381f2-183">Tek satırlık metin</span><span class="sxs-lookup"><span data-stu-id="381f2-183">Single Line of Text</span></span>        
<span data-ttu-id="381f2-184">Tamsayı alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-184">Integer fields</span></span> | <span data-ttu-id="381f2-185">Bazı alanlar, tamsayı veya tamsayı türünde bir alan dinamik içerik gerektirir.</span><span class="sxs-lookup"><span data-stu-id="381f2-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="381f2-186">Örnek tamamlanma yüzdesi ve süre verilebilir.</span><span class="sxs-lookup"><span data-stu-id="381f2-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="381f2-187">Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="381f2-188">TamamlanmaYüzdesi</span><span class="sxs-lookup"><span data-stu-id="381f2-188">percentcomplete</span></span> |<span data-ttu-id="381f2-189">Tam sayı</span><span class="sxs-lookup"><span data-stu-id="381f2-189">Whole Number</span></span>         
<span data-ttu-id="381f2-190">Tarih alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-190">Date fields</span></span> | <span data-ttu-id="381f2-191">Bazı alanlar, tarih gg/aa/yyyy biçiminde veya bir tarih alanı dinamik içerik girilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="381f2-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="381f2-192">Oluşturma tarihi, başlangıç tarihi, gerçek başlatma, son zaman tutun, gerçek bitiş ve son tarih örnekler.</span><span class="sxs-lookup"><span data-stu-id="381f2-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="381f2-193">Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="381f2-194">createdon</span><span class="sxs-lookup"><span data-stu-id="381f2-194">createdon</span></span> |<span data-ttu-id="381f2-195">Tarih ve saat</span><span class="sxs-lookup"><span data-stu-id="381f2-195">Date and Time</span></span>
<span data-ttu-id="381f2-196">Bir kayıt kimliği hem arama gerektiren alanlar yazın</span><span class="sxs-lookup"><span data-stu-id="381f2-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="381f2-197">Başka bir varlık kaydı başvuru bazı alanları hello kayıt kimliği ve hello arama türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="381f2-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="381f2-198">Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > hesabı > alanları</span><span class="sxs-lookup"><span data-stu-id="381f2-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="381f2-199">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="381f2-199">accountid</span></span>  | <span data-ttu-id="381f2-200">Birincil anahtar</span><span class="sxs-lookup"><span data-stu-id="381f2-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="381f2-201">Daha fazla örnekleri bir kayıt kimliği ve arama gerektiren alanlar yazın</span><span class="sxs-lookup"><span data-stu-id="381f2-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="381f2-202">Önceki tabloda Hello genişleterek, daha fazla hello dinamik içerik listeden seçilen değerlerle çalışmıyor alanları örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="381f2-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="381f2-203">Bunun yerine, bu alanların PowerApps hello alanlarına girilen hem bir kayıt kimliği ve arama türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="381f2-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="381f2-204">Sahibi ve sahip türü.</span><span class="sxs-lookup"><span data-stu-id="381f2-204">Owner and Owner Type.</span></span> <span data-ttu-id="381f2-205">Merhaba sahibi alan geçerli bir kullanıcı veya takım kayıt kimliği olmalıdır</span><span class="sxs-lookup"><span data-stu-id="381f2-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="381f2-206">Merhaba sahip türü ya da olmalıdır **systemusers** veya **takımlar**.</span><span class="sxs-lookup"><span data-stu-id="381f2-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="381f2-207">Müşteri ve müşteri türü.</span><span class="sxs-lookup"><span data-stu-id="381f2-207">Customer and Customer Type.</span></span> <span data-ttu-id="381f2-208">Merhaba müşteri alan geçerli bir hesap olması veya kayıt kimliği başvurun</span><span class="sxs-lookup"><span data-stu-id="381f2-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="381f2-209">Merhaba sahip türü ya da olmalıdır **hesapları** veya **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="381f2-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="381f2-210">İlgili ve ilgili türü.</span><span class="sxs-lookup"><span data-stu-id="381f2-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="381f2-211">Merhaba alan ilgili bir hesap gibi bir geçerli kayıt kimliği olması veya kayıt kimliği başvurun</span><span class="sxs-lookup"><span data-stu-id="381f2-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="381f2-212">Merhaba ilgili türü hello kaydına hello arama türü gibi olmalıdır **hesapları** veya **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="381f2-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="381f2-213">Merhaba aşağıdaki görev oluşturma eylem örneği hello görev alanının ilgili toohello ekleme toohello kayıt Kimliğine karşılık gelen bir hesap kaydı ekler.</span><span class="sxs-lookup"><span data-stu-id="381f2-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="381f2-215">Bu örnek ayrıca hello kullanıcının kaydı kimliğine göre hello görev tooa belirli bir kullanıcı atar</span><span class="sxs-lookup"><span data-stu-id="381f2-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="381f2-217">toofind bir kayıt kimliği, kullanıcının bölümden hello bkz: *Bul hello kayıt kimliği*</span><span class="sxs-lookup"><span data-stu-id="381f2-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="381f2-218">Merhaba kayıt kimliği bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="381f2-218">Find hello record ID</span></span>

1. <span data-ttu-id="381f2-219">Hesap kaydı gibi bir kaydı açın.</span><span class="sxs-lookup"><span data-stu-id="381f2-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="381f2-220">Merhaba Eylemler araç çubuğunda tıklatın **öne çıkar** ![açılan kayıt](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="381f2-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="381f2-221">Alternatif olarak, hello Eylemler araç çubuğunda, varsayılan e-posta programınız içine toocopy hello tam URL'yi tıklatın **e-posta A bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="381f2-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="381f2-222">Merhaba kayıt kimliği hello URL'nin karakter kodlama hello 7b ve %7 %d Between görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="381f2-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="381f2-224">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="381f2-224">Troubleshooting</span></span>
<span data-ttu-id="381f2-225">bir mantıksal uygulama, görünüm hello durum hello olay ayrıntılarını başarısız bir adımda tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="381f2-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="381f2-226">Altında **Logic Apps**, mantıksal uygulamanızı seçin ve ardından **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="381f2-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="381f2-227">Merhaba Özet alanı gösterilir ve hello mantıksal uygulama için Çalıştır hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="381f2-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Mantıksal uygulama çalışma durumu](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="381f2-229">tooview herhangi başarısız çalışmaları hakkında daha fazla bilgi tıklatın başarısız hello olay.</span><span class="sxs-lookup"><span data-stu-id="381f2-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="381f2-230">tooexpand başarısız adımı bu adımı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="381f2-230">tooexpand a failed step, click that step.</span></span>

   ![Başarısız olan adımda genişletin](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="381f2-232">Merhaba adım ayrıntıları görünür ve hello hatanın nedenini hello gidermenize yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="381f2-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Adım ayrıntıları başarısız oldu](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="381f2-234">Logic apps sorunlarını giderme hakkında daha fazla bilgi için bkz: [mantığı uygulama hatalarını tanılama](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="381f2-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="381f2-235">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="381f2-235">Connector-specific details</span></span>

<span data-ttu-id="381f2-236">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="381f2-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="381f2-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="381f2-237">Next steps</span></span>
<span data-ttu-id="381f2-238">Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="381f2-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
