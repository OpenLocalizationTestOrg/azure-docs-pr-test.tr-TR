---
title: "Azure mantıksal uygulamaları (çevrimiçi) Dynamics 365 bağlanma | Microsoft Docs"
description: "Dynamics 365 (çevrimiçi) varlıklar Dynamics 365 Bağlayıcısı tarafından sağlanan API aracılığıyla yönetmek uygulama iş mantığı oluşturun"
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
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="f6e29-103">Mantıksal uygulama akışlarından Dynamics 365'e bağlanın</span><span class="sxs-lookup"><span data-stu-id="f6e29-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="f6e29-104">Logic Apps ile (çevrimiçi) Dynamics 365 bağlama ve kayıtları oluşturma, öğeleri güncelleştirmek veya kayıtlar listesi döndüren kullanışlı iş akışları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="f6e29-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="f6e29-105">Dynamics 365 Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f6e29-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="f6e29-106">İş akışınız Dynamics 365'ten (çevrimiçi) alma verileri temel alan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f6e29-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="f6e29-107">Bir yanıt ve daha sonra çıktı diğer eylemler için kullanılabilir hale eylemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="f6e29-108">Örneğin, bir öğe Dynamics 365'te (çevrimiçi) güncelleştirildiğinde, Office 365 kullanılarak bir e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6e29-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="f6e29-109">Bu konuda yeni bir sağlama Dynamics 365'te oluşturulduğunda Dynamics 365'te bir görev oluşturan bir mantıksal uygulama oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6e29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f6e29-110">Prerequisites</span></span>
* <span data-ttu-id="f6e29-111">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f6e29-111">An Azure account.</span></span>
* <span data-ttu-id="f6e29-112">Dynamics 365 (çevrimiçi) hesabı.</span><span class="sxs-lookup"><span data-stu-id="f6e29-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="f6e29-113">Yeni bir sağlama Dynamics 365'te oluşturduğunuzda bir görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e29-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="f6e29-114">[Azure'da oturum aç](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6e29-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="f6e29-115">Azure arama kutusuna `Logic apps`, ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Logic Apps Bul](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="f6e29-117">Altında **Logic apps**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp Ekle](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="f6e29-119">Mantıksal uygulama oluşturmak için tamamlamak **adı**, **abonelik**, **kaynak grubu**, ve **konumu** alanları ve ardından**Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="f6e29-120">Yeni mantıksal uygulamaya seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-120">Select the new logic app.</span></span> <span data-ttu-id="f6e29-121">Aldığınızda **dağıtımı başarılı oldu** bildirimi tıklatın **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="f6e29-122">Altında **geliştirme araçları**, tıklatın **mantığı Uygulama Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="f6e29-123">Şablon listesinde tıklayın **boş mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="f6e29-124">Arama kutusuna `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="f6e29-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="f6e29-125">Dynamics 365 Tetikleyiciler listesinden **Dynamics bir kayıt oluşturulduğunda 365 –**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="f6e29-126">Dynamics 365'e oturum açmak için istenirse, bunu şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="f6e29-127">Tetikleyici Ayrıntılar aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="f6e29-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="f6e29-128">**Kuruluş adı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-128">**Organization Name**.</span></span> <span data-ttu-id="f6e29-129">Dinlemek için mantıksal uygulama istediğiniz Dynamics 365 örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="f6e29-130">**Varlık adı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-130">**Entity Name**.</span></span> <span data-ttu-id="f6e29-131">Dinlemek istediğiniz varlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="f6e29-132">Bu olay mantıksal uygulamayı başlatmak için bir tetikleyici olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="f6e29-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="f6e29-133">Bu kılavuzda **müşteri adayları** seçilir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="f6e29-134">**Ne sıklıkta öğeleri denetlemek istiyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="f6e29-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="f6e29-135">Mantıksal uygulama tetikleyici ile ilgili güncelleştirmeler için ne sıklıkta denetleyeceğini bu değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="f6e29-136">Her üç dakikada güncelleştirmeleri denetlemek için varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="f6e29-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="f6e29-137">**Sıklık**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-137">**Frequency**.</span></span> <span data-ttu-id="f6e29-138">Saniye, dakika, saat veya gün seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="f6e29-139">**Aralığı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-139">**Interval**.</span></span> <span data-ttu-id="f6e29-140">Saniye, dakika, saat veya önce sonraki onay geçirmek istediğiniz gün sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Mantıksal uygulama tetikleyici ayrıntıları](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="f6e29-142">Tıklatın **yeni adım**ve ardından **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="f6e29-143">Arama kutusuna `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="f6e29-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="f6e29-144">Eylemler listesinden **Dynamics 365 – yeni bir kayıt oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="f6e29-145">Aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="f6e29-145">Enter the following information:</span></span>

    * <span data-ttu-id="f6e29-146">**Kuruluş adı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-146">**Organization Name**.</span></span> <span data-ttu-id="f6e29-147">Akış kaydı oluşturmak için istediğiniz Dynamics 365 örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="f6e29-148">Bu örneği burada gelen olay tetiklenir örnekle aynı olmak zorunda değildir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="f6e29-149">**Varlık adı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-149">**Entity Name**.</span></span> <span data-ttu-id="f6e29-150">Olay tetiklendiğinde bir kayıt oluşturmak istediğiniz varlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="f6e29-151">Bu kılavuzda **görevleri** seçilir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="f6e29-152">' I tıklatın **konu** görüntülenen kutusunda.</span><span class="sxs-lookup"><span data-stu-id="f6e29-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="f6e29-153">Görüntülenen dinamik içerik listeden, bu alanlardan birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f6e29-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="f6e29-154">**Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-154">**Last Name**.</span></span> <span data-ttu-id="f6e29-155">Görev kaydı oluşturulduğunda, bu alanın seçilmesi Soyadı sağlama için konu alanı görev ekler.</span><span class="sxs-lookup"><span data-stu-id="f6e29-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="f6e29-156">**Konu**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-156">**Topic**.</span></span> <span data-ttu-id="f6e29-157">Görev kaydı oluşturulduğunda, bu alanın seçilmesi görev için konu alanına sağlama konu alanı ekler.</span><span class="sxs-lookup"><span data-stu-id="f6e29-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="f6e29-158">Tıklatın **konu** olarak eklemek için **konu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="f6e29-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Mantıksal uygulama oluşturma yeni kayıt ayrıntıları](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="f6e29-160">Mantıksal Uygulama Tasarımcısı araç çubuğunda tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="f6e29-162">Mantıksal uygulama başlatmak için tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-162">To start the Logic App, click **Run**.</span></span>

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="f6e29-164">Artık Dynamics 365 satış sağlama kaydı oluşturun ve akışınız eylem bakın!</span><span class="sxs-lookup"><span data-stu-id="f6e29-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="f6e29-165">Bir mantıksal uygulama adımı için Gelişmiş seçenekleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="f6e29-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="f6e29-166">Bir mantıksal uygulama adımda veri filtreleme belirtmek için tıklatın **Gelişmiş Seçenekleri Göster** sorgu tarafından filtre veya düzeni sonra bu adımda, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="f6e29-167">Örneğin, yalnızca active hesapları ve sırası tarafından hesap adını almak için bir filtre sorgusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6e29-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="f6e29-168">Bu görevi gerçekleştirmek için OData filtre sorgusu girin `statuscode eq 1`seçip **hesap adı** dinamik içerik listesinden.</span><span class="sxs-lookup"><span data-stu-id="f6e29-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="f6e29-169">Daha fazla bilgi: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) ve [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="f6e29-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Gelişmiş Seçenekleri mantıksal uygulama](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="f6e29-171">Gelişmiş seçenekleri kullanırken en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="f6e29-171">Best practices when using advanced options</span></span>

<span data-ttu-id="f6e29-172">Bir değeri bir alan eklediğinizde, bir değer yazın ya da dinamik içerik listeden bir değer seçin alan türü eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="f6e29-173">Alan türü</span><span class="sxs-lookup"><span data-stu-id="f6e29-173">Field type</span></span>  |<span data-ttu-id="f6e29-174">Nasıl kullanılır</span><span class="sxs-lookup"><span data-stu-id="f6e29-174">How to use</span></span>  |<span data-ttu-id="f6e29-175">Nerede bulunacağını</span><span class="sxs-lookup"><span data-stu-id="f6e29-175">Where to find</span></span>  |<span data-ttu-id="f6e29-176">Ad</span><span class="sxs-lookup"><span data-stu-id="f6e29-176">Name</span></span>  |<span data-ttu-id="f6e29-177">Veri türü</span><span class="sxs-lookup"><span data-stu-id="f6e29-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="f6e29-178">Metin alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-178">Text fields</span></span>|<span data-ttu-id="f6e29-179">Metin alanları tek satırlık bir metin veya metin türü alan dinamik içerik gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="f6e29-180">Örnekler kategori ve alt kategori alanlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="f6e29-181">Ayarlar > özelleştirmeleri > Sistem Özelleştirme > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6e29-182">category</span><span class="sxs-lookup"><span data-stu-id="f6e29-182">category</span></span> |<span data-ttu-id="f6e29-183">Tek satırlık metin</span><span class="sxs-lookup"><span data-stu-id="f6e29-183">Single Line of Text</span></span>        
<span data-ttu-id="f6e29-184">Tamsayı alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-184">Integer fields</span></span> | <span data-ttu-id="f6e29-185">Bazı alanlar, tamsayı veya tamsayı türünde bir alan dinamik içerik gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="f6e29-186">Örnek tamamlanma yüzdesi ve süre verilebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="f6e29-187">Ayarlar > özelleştirmeleri > Sistem Özelleştirme > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6e29-188">TamamlanmaYüzdesi</span><span class="sxs-lookup"><span data-stu-id="f6e29-188">percentcomplete</span></span> |<span data-ttu-id="f6e29-189">Tam sayı</span><span class="sxs-lookup"><span data-stu-id="f6e29-189">Whole Number</span></span>         
<span data-ttu-id="f6e29-190">Tarih alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-190">Date fields</span></span> | <span data-ttu-id="f6e29-191">Bazı alanlar, tarih gg/aa/yyyy biçiminde veya bir tarih alanı dinamik içerik girilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="f6e29-192">Oluşturma tarihi, başlangıç tarihi, gerçek başlatma, son zaman tutun, gerçek bitiş ve son tarih örnekler.</span><span class="sxs-lookup"><span data-stu-id="f6e29-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="f6e29-193">Ayarlar > özelleştirmeleri > Sistem Özelleştirme > varlıklar > Görev > alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6e29-194">createdon</span><span class="sxs-lookup"><span data-stu-id="f6e29-194">createdon</span></span> |<span data-ttu-id="f6e29-195">Tarih ve saat</span><span class="sxs-lookup"><span data-stu-id="f6e29-195">Date and Time</span></span>
<span data-ttu-id="f6e29-196">Bir kayıt kimliği hem arama gerektiren alanlar yazın</span><span class="sxs-lookup"><span data-stu-id="f6e29-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="f6e29-197">Başka bir varlık kaydı başvuru bazı alanları kayıt kimliği ve arama türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="f6e29-198">Ayarlar > özelleştirmeleri > Sistem Özelleştirme > varlıklar > hesabı > alanları</span><span class="sxs-lookup"><span data-stu-id="f6e29-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="f6e29-199">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="f6e29-199">accountid</span></span>  | <span data-ttu-id="f6e29-200">Birincil anahtar</span><span class="sxs-lookup"><span data-stu-id="f6e29-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="f6e29-201">Daha fazla örnekleri bir kayıt kimliği ve arama gerektiren alanlar yazın</span><span class="sxs-lookup"><span data-stu-id="f6e29-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="f6e29-202">Önceki tabloda genişleterek, daha fazla dinamik içerik listeden seçilen değerlerle çalışmıyor alanları örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="f6e29-203">Bunun yerine, bu alanların PowerApps alanlara girilen her iki kayıt kimliği ve arama türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="f6e29-204">Sahibi ve sahip türü.</span><span class="sxs-lookup"><span data-stu-id="f6e29-204">Owner and Owner Type.</span></span> <span data-ttu-id="f6e29-205">Sahip alanı geçerli bir kullanıcı veya takım kayıt kimliği olmalıdır</span><span class="sxs-lookup"><span data-stu-id="f6e29-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="f6e29-206">Sahibi türü ya da olmalıdır **systemusers** veya **takımlar**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="f6e29-207">Müşteri ve müşteri türü.</span><span class="sxs-lookup"><span data-stu-id="f6e29-207">Customer and Customer Type.</span></span> <span data-ttu-id="f6e29-208">Müşteri alanın geçerli bir hesap olması veya kayıt kimliği başvurun</span><span class="sxs-lookup"><span data-stu-id="f6e29-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="f6e29-209">Sahibi türü ya da olmalıdır **hesapları** veya **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="f6e29-210">İlgili ve ilgili türü.</span><span class="sxs-lookup"><span data-stu-id="f6e29-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="f6e29-211">İlgili alanı bir hesap gibi bir geçerli kayıt kimliği olması veya kayıt kimliği başvurun</span><span class="sxs-lookup"><span data-stu-id="f6e29-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="f6e29-212">İlgili kaydı için arama türü gibi türünden olmalıdır **hesapları** veya **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="f6e29-213">Aşağıdaki görev oluşturma eylem örneği görev ilgi alanına ekleme kayıt kimliği karşılık gelen bir hesap kaydı ekler.</span><span class="sxs-lookup"><span data-stu-id="f6e29-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="f6e29-215">Bu örnek ayrıca kullanıcının kaydı kimliğine göre belirli bir kullanıcı bir görev atar.</span><span class="sxs-lookup"><span data-stu-id="f6e29-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="f6e29-217">Bir kaydın Kimliğini bulmak için aşağıdaki bölüme bakın: *kayıt kimliği bulunamıyor*</span><span class="sxs-lookup"><span data-stu-id="f6e29-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="f6e29-218">Kayıt Kimliği bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="f6e29-218">Find the record ID</span></span>

1. <span data-ttu-id="f6e29-219">Hesap kaydı gibi bir kaydı açın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="f6e29-220">Eylemler araç çubuğunda tıklatın **öne çıkar** ![açılan kayıt](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="f6e29-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="f6e29-221">Alternatif olarak, varsayılan e-posta programınıza tam URL'yi kopyalamak için Eylemler araç çubuğunda tıklatın **e-posta A bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="f6e29-222">Kayıt Kimliği URL'nin karakter kodlama % 7b ve %7 d Between görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f6e29-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="f6e29-224">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f6e29-224">Troubleshooting</span></span>
<span data-ttu-id="f6e29-225">Bir mantıksal uygulama başarısız bir adımda gidermek için olay durum ayrıntılarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e29-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="f6e29-226">Altında **Logic Apps**, mantıksal uygulamanızı seçin ve ardından **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="f6e29-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="f6e29-227">Özet alanı gösterilir ve mantıksal uygulama için çalışma durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6e29-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Mantıksal uygulama çalışma durumu](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="f6e29-229">Tüm başarısız çalışmaları hakkında daha fazla bilgi görüntülemek için başarısız olay'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="f6e29-230">Başarısız olan bir adım genişletmek için bu adımı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f6e29-230">To expand a failed step, click that step.</span></span>

   ![Başarısız olan adımda genişletin](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="f6e29-232">Adım ayrıntıları görünür ve hatanın nedenini gidermenize yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="f6e29-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Adım ayrıntıları başarısız oldu](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="f6e29-234">Logic apps sorunlarını giderme hakkında daha fazla bilgi için bkz: [mantığı uygulama hatalarını tanılama](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="f6e29-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f6e29-235">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f6e29-235">Connector-specific details</span></span>

<span data-ttu-id="f6e29-236">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="f6e29-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6e29-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6e29-237">Next steps</span></span>
<span data-ttu-id="f6e29-238">Logic Apps diğer kullanılabilir bağlayıcılar keşfedin bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f6e29-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
