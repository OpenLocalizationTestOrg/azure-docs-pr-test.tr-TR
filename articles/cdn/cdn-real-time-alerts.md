---
title: "aaaAzure CDN gerçek zamanlı uyarılar | Microsoft Docs"
description: "Microsoft Azure CDN gerçek zamanlı uyarılar. Gerçek zamanlı uyarılar CDN profilinizi hello uç noktalarını hello performansını hakkında bildirimler sağlayın."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="309a9-104">Microsoft Azure cdn'de gerçek zamanlı uyarılar</span><span class="sxs-lookup"><span data-stu-id="309a9-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="309a9-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="309a9-105">Overview</span></span>
<span data-ttu-id="309a9-106">Bu belgede, Microsoft Azure cdn'de gerçek zamanlı uyarılar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="309a9-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="309a9-107">Bu işlevsellik, CDN profilinize hello uç noktaları hello performansı hakkında gerçek zamanlı bildirimler sağlar.</span><span class="sxs-lookup"><span data-stu-id="309a9-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="309a9-108">E-posta veya temel HTTP uyarılar ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="309a9-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="309a9-109">Bant Genişliği</span><span class="sxs-lookup"><span data-stu-id="309a9-109">Bandwidth</span></span>
* <span data-ttu-id="309a9-110">Durum kodları</span><span class="sxs-lookup"><span data-stu-id="309a9-110">Status Codes</span></span>
* <span data-ttu-id="309a9-111">Önbellek durumları</span><span class="sxs-lookup"><span data-stu-id="309a9-111">Cache Statuses</span></span>
* <span data-ttu-id="309a9-112">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="309a9-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="309a9-113">Gerçek zamanlı uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="309a9-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="309a9-114">Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="309a9-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN profili dikey penceresi](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="309a9-116">Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309a9-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="309a9-118">Merhaba CDN Yönetim Portalı açar.</span><span class="sxs-lookup"><span data-stu-id="309a9-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="309a9-119">Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **gerçek zamanlı İstatistikler** çıkma.</span><span class="sxs-lookup"><span data-stu-id="309a9-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="309a9-120">Tıklayın **gerçek zamanlı uyarılar**.</span><span class="sxs-lookup"><span data-stu-id="309a9-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN Yönetim Portalı](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="309a9-122">var olan uyarı yapılandırmaları (varsa) Hello listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="309a9-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="309a9-123">Merhaba tıklatın **eklemek uyarı** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309a9-123">Click hello **Add Alert** button.</span></span>
   
    ![Uyarı düğme ekleme](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="309a9-125">Yeni bir uyarı oluşturmak için bir form görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="309a9-125">A form for creating a new alert is displayed.</span></span>
   
    ![Yeni uyarı formu](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="309a9-127">Bu uyarı toobe etkin istiyorsanız tıkladığınızda **kaydetmek**, hello denetleyin **uyarı etkin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="309a9-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="309a9-128">Hello Uyarınız için açıklayıcı bir ad girin **adı** alan.</span><span class="sxs-lookup"><span data-stu-id="309a9-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="309a9-129">Merhaba, **medya türü** açılan listesinde, select **HTTP büyük nesne**.</span><span class="sxs-lookup"><span data-stu-id="309a9-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![HTTP büyük seçili nesne medya türüyle](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="309a9-131">Seçmelisiniz **HTTP büyük nesne** hello olarak **medya türü**.</span><span class="sxs-lookup"><span data-stu-id="309a9-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="309a9-132">Merhaba diğer seçenekleri tarafından kullanılmaz **verizon'dan Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="309a9-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="309a9-133">Hata tooselect **HTTP büyük nesne** uyarıyı neden olacak toonever tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="309a9-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="309a9-134">Oluşturma bir **ifade** seçerek toomonitor bir **ölçüm**, **işleci**, ve **tetikleyen değer**.</span><span class="sxs-lookup"><span data-stu-id="309a9-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="309a9-135">İçin **ölçüm**, izlenen istediğiniz koşul hello türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="309a9-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="309a9-136">**Bant genişliği Mbps** hello saniye başına megabit olarak bant genişliği kullanım miktarı.</span><span class="sxs-lookup"><span data-stu-id="309a9-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="309a9-137">**Toplam Bağlantı** hello eşzamanlı HTTP bağlantıları tooour uç sunucuların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="309a9-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="309a9-138">Çeşitli önbellek durumları ve durum kodları hello tanımları için bkz: [Azure CDN önbellek durum kodları](https://msdn.microsoft.com/library/mt759237.aspx) ve [Azure CDN HTTP durum kodları](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="309a9-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="309a9-139">**İşleç** hello ölçüm ve hello tetikleyici değeri arasında hello ilişki kurar hello matematik işleci.</span><span class="sxs-lookup"><span data-stu-id="309a9-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="309a9-140">**Tetikleyen değer** bir bildirim gönderilir önce karşılanması gereken hello eşik değeri.</span><span class="sxs-lookup"><span data-stu-id="309a9-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="309a9-141">Örnek aşağıda Hello 404 durum kodları hello sayısı 25'den büyük olduğunda bildirim toobe istiyorum oluşturmuş olduğunuz hello ifadeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="309a9-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Gerçek zamanlı uyarı örnek bir ifade](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="309a9-143">İçin **aralığı**, ne sıklıkta hello ifade Hesaplandı istediğinizi girin.</span><span class="sxs-lookup"><span data-stu-id="309a9-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="309a9-144">Merhaba, **bildirim** açılan listesinde, zaman toobe hello ifade doğruysa bildirim istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="309a9-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="309a9-145">**Koşul başlangıç** hello koşul algılanan belirtildiğinde bir bildirim gönderileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="309a9-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="309a9-146">**Koşul son** hello koşul artık algıladı belirtildiğinde bir bildirim gönderileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="309a9-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="309a9-147">Belirtilen bu hello bizim ağ sistem izleme saptadıktan sonra yalnızca bu bildirim tetiklenebilir koşulu oluştu.</span><span class="sxs-lookup"><span data-stu-id="309a9-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="309a9-148">**Sürekli** belirten bir bildirim ağ izleme sistemi hello her zaman algılar belirtilen hello gönderilir koşulu.</span><span class="sxs-lookup"><span data-stu-id="309a9-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="309a9-149">Bu hello ağ onay kez hello için aralık başına koşul belirtilen yalnızca sistem olacak izleme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="309a9-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="309a9-150">**Koşul başlangıç ve bitiş** hello belirtilen koşulu hello ilk kez algılandı ve bir kez daha zaman hello koşul artık algılandığında bir bildirim gönderileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="309a9-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="309a9-151">E-posta ile tooreceive bildirimleri istiyorsanız hello denetleyin **e-posta ile bildir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="309a9-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![E-posta formu tarafından bildir](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="309a9-153">Merhaba, **için** alanında, istediğiniz yere bildirimleri gönderdiğiniz hello e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="309a9-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="309a9-154">İçin **konu** ve **gövde**hello varsayılan bırakabilir veya hello kullanarak selamlama iletisine özelleştirebilir **kullanılabilir anahtar sözcükleri** listesi toodynamically Ekle uyarı verileri zaman Merhaba ileti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="309a9-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="309a9-155">Merhaba tıklatarak hello e-posta bildirimi sınayabilirsiniz **Test bildirimi** hello uyarı yapılandırma kaydedildikten sonra ancak yalnızca düğme.</span><span class="sxs-lookup"><span data-stu-id="309a9-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="309a9-156">Tooa web sunucusuna gönderilen bildirimler toobe istiyorsanız, hello denetleyin **HTTP Post tarafından bildirim** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="309a9-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![HTTP Post formuyla bildir](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="309a9-158">Merhaba, **Url** alanında, istediğiniz yere hello HTTP iletisi deftere hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="309a9-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="309a9-159">Merhaba, **üstbilgileri** metin kutusuna, hello istekte gönderilen hello HTTP üstbilgileri toobe girin.</span><span class="sxs-lookup"><span data-stu-id="309a9-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="309a9-160">İçin **gövde** hello kullanarak selamlama iletisine özelleştirebilir **kullanılabilir anahtar sözcükleri** listesi toodynamically hello ileti gönderildiğinde uyarı verileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="309a9-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="309a9-161">**Üstbilgileri** ve **gövde** tooan XML yükü benzer toohello örnek aşağıda varsayılan.</span><span class="sxs-lookup"><span data-stu-id="309a9-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="309a9-162">Merhaba tıklatarak hello HTTP Post bildirim sınayabilirsiniz **Test bildirimi** hello uyarı yapılandırma kaydedildikten sonra ancak yalnızca düğme.</span><span class="sxs-lookup"><span data-stu-id="309a9-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="309a9-163">Merhaba tıklatın **kaydetmek** toosave uyarı yapılandırmanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="309a9-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="309a9-164">İşaretlendiğinde, **uyarı etkin** 5. adımda Uyarınız şimdi etkindir.</span><span class="sxs-lookup"><span data-stu-id="309a9-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="309a9-165">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="309a9-165">Next Steps</span></span>
* <span data-ttu-id="309a9-166">Analiz [Azure CDN içindeki gerçek zamanlı İstatistikler](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="309a9-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="309a9-167">Dıg ile daha derin [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="309a9-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="309a9-168">Analiz [kullanım desenleri](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="309a9-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

