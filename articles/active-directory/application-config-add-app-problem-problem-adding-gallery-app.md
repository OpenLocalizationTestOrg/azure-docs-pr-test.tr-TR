---
title: Bir Azure AD galeri uygulama eklenirken hata | Microsoft Docs
description: "Azure AD galeri uygulamaları ve bunları gidermek için neler yapabileceğinizi eklerken, ortak sorunları kişiler yüz anlama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: b3ae472d52208d3c76424d29192c1eb982639572
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="cd51a-103">Bir Azure AD galeri uygulama eklenirken hata</span><span class="sxs-lookup"><span data-stu-id="cd51a-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="cd51a-104">Bu makalede Azure AD galeri uygulamaları ve bunları gidermek için neler yapabileceğinizi eklerken, ortak sorunları kişiler yüzünü anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cd51a-104">This article help you to understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="cd51a-105">"Ekle" düğmesine tıklandığında ve uygulamamın görünür uzun sürdü</span><span class="sxs-lookup"><span data-stu-id="cd51a-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="cd51a-106">Bazı durumlarda, 1-2 dakika alabilir (ve bazı durumlarda daha uzun) uygulamanın dizininize eklendikten sonra görünür.</span><span class="sxs-lookup"><span data-stu-id="cd51a-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="cd51a-107">Bu normal beklenen performans olmamasına karşın, uygulama eklenmesi ediyor tıklayarak görebilirsiniz **bildirimleri** (zil) simgesine sağ üst tarafındaki [Azure Portal](https://portal.azure.com/) ve aranıyor için bir **sürüyor** veya **tamamlandı** etiketli bildirim **uygulaması oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="cd51a-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="cd51a-108">Uygulamanızı hiçbir zaman eklenir veya tıklatıldığında hatayla karşılaşırsanız **Ekle** düğmesi, göreceğiniz bir **bildirim** içinde bir **hata** durumu.</span><span class="sxs-lookup"><span data-stu-id="cd51a-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="cd51a-109">Daha fazla bilgi edinmek veya destek engingeer ile paylaşmak için hata hakkında daha fazla ayrıntı isterseniz içindeki adımları izleyerek hata hakkında daha fazla bilgi görebilirsiniz [portal bildirim ayrıntılarını görmek nasıl](#how-to-see-the-details-of-a-portal-notification) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cd51a-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="cd51a-110">"Ekle" düğmesine tıklandığında ve uygulamamın görünmedi</span><span class="sxs-lookup"><span data-stu-id="cd51a-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="cd51a-111">Bazı durumlarda, geçici sorunlar nedeniyle ağ sorunları veya bir hata, bir uygulama başarısız ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="cd51a-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="cd51a-112">Tıkladığınızda böyle anlayabilirsiniz **bildirimleri** (zil) simgesine sağ üst tarafındaki Azure Portalı'nı ve bir kırmızı (!) simgesi yanına bakın, **uygulaması oluşturma** bildirim.</span><span class="sxs-lookup"><span data-stu-id="cd51a-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="cd51a-113">Bu, uygulama oluştururken bir hata oluştu gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd51a-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="cd51a-114">Tıklatıldığında bir hatayla karşılaşırsanız **Ekle** düğmesi, göreceğiniz bir **bildirim** içinde bir **hata** durumu.</span><span class="sxs-lookup"><span data-stu-id="cd51a-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="cd51a-115">Daha fazla bilgi edinmek veya destek engingeer ile paylaşmak için hata hakkında daha fazla ayrıntı isterseniz içindeki adımları izleyerek hata hakkında daha fazla bilgi görebilirsiniz [portal bildirim ayrıntılarını görmek nasıl](#how-to-see-the-details-of-a-portal-notification) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cd51a-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="cd51a-116">Bunu ekledikten sonra my uygulamayı kurmak nasıl çıkılacağını bilmiyoruz</span><span class="sxs-lookup"><span data-stu-id="cd51a-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="cd51a-117">Uygulamaları hakkında öğrenme yardıma gereksinim duyarsanız [SaaS uygulamaları Azure Active Directory ile tümleştirme için nasıl öğreticiler listesi](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) makale başlatmak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="cd51a-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span></span>

<span data-ttu-id="cd51a-118">Bu, ek olarak [Azure AD uygulamaları belge kitaplığı](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) Azure AD ile çoklu oturum açma ve nasıl çalıştığı hakkında daha fazla bilgi için Yardım.</span><span class="sxs-lookup"><span data-stu-id="cd51a-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="cd51a-119">Bir portal bildirim ayrıntılarını görmek nasıl</span><span class="sxs-lookup"><span data-stu-id="cd51a-119">How to see the details of a portal notification</span></span>

<span data-ttu-id="cd51a-120">Aşağıdaki adımları izleyerek herhangi bir portal bildirim ayrıntılarını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cd51a-120">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="cd51a-121">tıklatın **bildirimleri** simgesi (zil) Azure portalının sağ üst</span><span class="sxs-lookup"><span data-stu-id="cd51a-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="cd51a-122">Herhangi bir bildirim seçin bir **hata** durumu (bunları yanında kırmızı (!) sahip olanlar).</span><span class="sxs-lookup"><span data-stu-id="cd51a-122">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

    >[!NOTE]
    ><span data-ttu-id="cd51a-123">Bildirimlerde'ı bir **başarılı** veya **sürüyor** durumu.</span><span class="sxs-lookup"><span data-stu-id="cd51a-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

3.  <span data-ttu-id="cd51a-124">Bu açık **bildirim ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="cd51a-124">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="cd51a-125">Bu bilgileri kullanın kendinize sorun hakkında daha fazla ayrıntı anlayın.</span><span class="sxs-lookup"><span data-stu-id="cd51a-125">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="cd51a-126">Hala yardıma ihtiyacınız varsa, bu bilgiler sorununuzu Yardım almak için bir destek mühendisine veya ürün grubu ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd51a-126">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="cd51a-127">Tıklatın **kopya** **simgesi** sağındaki **kopyalama hatası** desteği veya ürün grubu mühendislik ile paylaşmak için tüm bildirim ayrıntıları kopyalamak için metin kutusu</span><span class="sxs-lookup"><span data-stu-id="cd51a-127">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="cd51a-128">Bir destek mühendisine bildirim ayrıntıları göndererek Yardım alma</span><span class="sxs-lookup"><span data-stu-id="cd51a-128">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="cd51a-129">Paylaştığınız çok önemlidir **aşağıda listelenen tüm ayrıntıları** size hızla yardımcı böylece yardıma gereksiniminiz varsa bir destek mühendisine ile.</span><span class="sxs-lookup"><span data-stu-id="cd51a-129">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="cd51a-130">Bu yana kolayca yapabilirsiniz **bir ekran görüntüsü alma** veya tıklatarak **kopyalama hata simgesi**, sağ tarafında bulunan **kopyalama hatası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cd51a-130">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="cd51a-131">Açıklanan bildirim ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="cd51a-131">Notification Details Explained</span></span>

<span data-ttu-id="cd51a-132">Daha fazla her bildirimin öğelerini anlamına gelir ve bunların her birini örnekleri verir aşağıda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cd51a-132">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="cd51a-133">Temel bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="cd51a-133">Essential Notification Items</span></span>

-   <span data-ttu-id="cd51a-134">**Başlık** – bildirimin açıklayıcı bir başlık</span><span class="sxs-lookup"><span data-stu-id="cd51a-134">**Title** – the descriptive title of the notification</span></span>

  * <span data-ttu-id="cd51a-135">Örnek – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="cd51a-135">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="cd51a-136">**Açıklama** – ne işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="cd51a-136">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="cd51a-137">Örnek – **girilen iç url başka bir uygulama tarafından zaten kullanılıyor**</span><span class="sxs-lookup"><span data-stu-id="cd51a-137">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="cd51a-138">**Bildirim kimliği** – bildirim benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="cd51a-138">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="cd51a-139">Örnek – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="cd51a-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="cd51a-140">**İstemci istek kimliği** – tarayıcınız tarafından yapılan belirli bir istek kimliği</span><span class="sxs-lookup"><span data-stu-id="cd51a-140">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="cd51a-141">Örnek – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="cd51a-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="cd51a-142">**Zaman damgası UTC** – sırasında bildirim meydana geldiği UTC zaman damgası</span><span class="sxs-lookup"><span data-stu-id="cd51a-142">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="cd51a-143">Örnek – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="cd51a-143">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="cd51a-144">**İç işlem kimliği** – iç kimlik kullanabileceğiniz bizim sistemlerinde hata aramak için</span><span class="sxs-lookup"><span data-stu-id="cd51a-144">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="cd51a-145">Örnek – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="cd51a-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="cd51a-146">**UPN** – işlemi gerçekleştiren kullanıcı</span><span class="sxs-lookup"><span data-stu-id="cd51a-146">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="cd51a-147">Örnek –**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="cd51a-147">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="cd51a-148">**Kiracı kimliği** – işlemi gerçekleştiren kullanıcının üyesi olduğu Kiracı benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="cd51a-148">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="cd51a-149">Örnek – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="cd51a-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="cd51a-150">**Kullanıcı nesnesi kimliği** – işlemi gerçekleştiren kullanıcının benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="cd51a-150">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="cd51a-151">Örnek – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="cd51a-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="cd51a-152">Ayrıntılı bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="cd51a-152">Detailed Notification Items</span></span>

-   <span data-ttu-id="cd51a-153">**Görünen ad** – **(boş olabilir)** hatası için ayrıntılı bir görünen ad</span><span class="sxs-lookup"><span data-stu-id="cd51a-153">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="cd51a-154">Örnek – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="cd51a-154">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="cd51a-155">**Durum** – bildirim özel durumu</span><span class="sxs-lookup"><span data-stu-id="cd51a-155">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="cd51a-156">Örnek – **başarısız oldu**</span><span class="sxs-lookup"><span data-stu-id="cd51a-156">Example – **Failed**</span></span>

-   <span data-ttu-id="cd51a-157">**Nesne Kimliği** – **(boş olabilir)** göre işlemi gerçekleştirildiği nesne kimliği</span><span class="sxs-lookup"><span data-stu-id="cd51a-157">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="cd51a-158">Örnek – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="cd51a-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="cd51a-159">**Ayrıntılar** – ayrıntılı ne işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="cd51a-159">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="cd51a-160">Örnek – **iç url 'http://bing.com/', zaten kullanımda olduğundan geçersiz**</span><span class="sxs-lookup"><span data-stu-id="cd51a-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="cd51a-161">**Kopyalama hatası** – tıklatın **Kopyala simgesi** sağındaki **kopyalama hatası** desteği veya ürün grubu mühendislik ile paylaşmak için tüm bildirim ayrıntıları kopyalamak için metin kutusu</span><span class="sxs-lookup"><span data-stu-id="cd51a-161">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="cd51a-162">Örnek```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="cd51a-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd51a-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd51a-163">Next steps</span></span>
[<span data-ttu-id="cd51a-164">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="cd51a-164">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
