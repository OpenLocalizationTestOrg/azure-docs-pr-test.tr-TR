---
title: bir galeri olmayan uygulama ekleme aaaProblem | Microsoft Docs
description: "Özel Galeri olmayan uygulamaları eklerken Hello ortak sorunları kişiler yüz anlama"
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
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="ef947-103">Bir galeri olmayan uygulama eklenirken hata</span><span class="sxs-lookup"><span data-stu-id="ef947-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="ef947-104">Bu makalede yardımcı toounderstand hello ortak sorunları kişiler yüz eklerken **Özel Galeri olmayan uygulamalar** ve neler yapabileceğinizi tooresolve bunları.</span><span class="sxs-lookup"><span data-stu-id="ef947-104">This article help you toounderstand hello common problems people face when adding **custom non-gallery applications** and what you can do tooresolve them.</span></span> 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a><span data-ttu-id="ef947-105">"Düğmesi ve uygulamamın uzun süre tooappear sürdü Ekle" Merhaba tıklattınız</span><span class="sxs-lookup"><span data-stu-id="ef947-105">I clicked hello “add” button and my application took a long time tooappear</span></span>

<span data-ttu-id="ef947-106">Bazı durumlarda, 1-2 dakika alabilir (ve bazı durumlarda daha uzun) tooyour dizin ekledikten sonra bir uygulama tooappear için.</span><span class="sxs-lookup"><span data-stu-id="ef947-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application tooappear after adding it tooyour directory.</span></span> <span data-ttu-id="ef947-107">Bu hello normal beklenen performans olmamasına karşın, hello uygulama toplama devam ediyor üzerinde hello tıklayarak görebilirsiniz **bildirimleri** hello sağ üst tarafındaki hello (Merhaba zil) simgesinde [Azure Portal](https://portal.azure.com/)ve aramakta bir **sürüyor** veya **tamamlandı** etiketli bildirim **uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ef947-107">While this is not hello normal expected performance, you can see hello application addition is in progress by clicking on hello **Notifications** icon (hello bell) in hello upper right of hello [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="ef947-108">Uygulamanızı hiçbir zaman eklediyseniz veya hello tıklatıldığında hatayla karşılaşırsanız **Ekle** düğmesi, göreceğiniz bir **bildirim** içinde bir **hata** durumu.</span><span class="sxs-lookup"><span data-stu-id="ef947-108">If your application is never added, or you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="ef947-109">Daha fazla tooor destek engingeer ile paylaşmak hello hata toolearn hakkında daha fazla ayrıntı isterseniz hello hello adımları izleyerek hello hata hakkında daha fazla bilgi görebilirsiniz [nasıl toosee hello portal bildirim ayrıntılarını](#how-to-see-the-details-of-a-portal-notification) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ef947-109">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="ef947-110">Merhaba "Ekle" düğmesine tıklandığında ve uygulamamın görünmedi</span><span class="sxs-lookup"><span data-stu-id="ef947-110">I clicked hello “add” button and my application didn’t appear</span></span>

<span data-ttu-id="ef947-111">Bazı durumlarda, tootransient sorunları ağ sorunları veya bir hata, bir uygulama başarısız ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="ef947-111">Sometimes, due tootransient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="ef947-112">Hello tıklattığınızda böyle anlayabilirsiniz **bildirimleri** hello sağ üst köşesinde, hello Azure Portal ve (Merhaba zil) simgesinde kırmızı (!) bkz simgesi sonraki tooyour **uygulaması oluşturma** bildirim.</span><span class="sxs-lookup"><span data-stu-id="ef947-112">You can tell this happens when you click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal and you see a red (!) icon next tooyour **Create application** notification.</span></span> <span data-ttu-id="ef947-113">Başka bir gösterir Merhaba uygulaması oluşturulurken bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ef947-113">This indicates there was an error when creating hello application.</span></span>

<span data-ttu-id="ef947-114">Merhaba tıklatıldığında hatayla karşılaşırsanız **Ekle** düğmesi, göreceğiniz bir **bildirim** içinde bir **hata** durumu.</span><span class="sxs-lookup"><span data-stu-id="ef947-114">If you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="ef947-115">Daha fazla tooor destek engingeer ile paylaşmak hello hata toolearn hakkında daha fazla ayrıntı isterseniz hello hello adımları izleyerek hello hata hakkında daha fazla bilgi görebilirsiniz [nasıl toosee hello portal bildirim ayrıntılarını](#how-to-see-the-details-of-a-portal-notification) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ef947-115">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a><span data-ttu-id="ef947-116">Nasıl tooset Uygulamam kez yedeklemek, ekledim bilmiyorsanız</span><span class="sxs-lookup"><span data-stu-id="ef947-116">I don’t know how tooset up my application once I’ve added it</span></span>

<span data-ttu-id="ef947-117">Özel uygulamalar hakkında öğrenme yardıma gereksinim duyarsanız, hello [Azure AD uygulamaları belge kitaplığı](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) toolearn hakkında daha fazla Azure AD ile çoklu oturum açma ve nasıl çalıştığı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ef947-117">If you need help learning about custom applications, hello [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you toolearn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="ef947-118">Nasıl bir portal bildirim toosee hello ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="ef947-118">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="ef947-119">Merhaba adımları izleyerek herhangi bir portal bildirim hello ayrıntılarını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef947-119">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="ef947-120">Merhaba tıklatın **bildirimleri** hello sağ üst köşesinde, hello Azure Portal (Merhaba zil) simgesi</span><span class="sxs-lookup"><span data-stu-id="ef947-120">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="ef947-121">Herhangi bir bildirim seçin bir **hata** durumu (kırmızı (!) sonraki toothem sahip olanlar).</span><span class="sxs-lookup"><span data-stu-id="ef947-121">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

   >[!NOTE]
   ><span data-ttu-id="ef947-122">Bildirimlerde'ı bir **başarılı** veya **sürüyor** durumu.</span><span class="sxs-lookup"><span data-stu-id="ef947-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="ef947-123">Bu açık hello **bildirim ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="ef947-123">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="ef947-124">Bu bilgileri kendiniz hello sorun hakkında daha fazla ayrıntı toounderstand kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef947-124">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="ef947-125">Hala yardıma ihtiyacınız varsa, sorununuzu ile bir destek mühendisi veya hello ürün grubu tooget Yardım ile bu bilgileri de paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="ef947-125">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="ef947-126">Merhaba tıklatın **Kopyala simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="ef947-126">Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="ef947-127">Tooget nasıl yardımcı bildirim ayrıntıları tooa destek mühendisine göndererek</span><span class="sxs-lookup"><span data-stu-id="ef947-127">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="ef947-128">Paylaştığınız çok önemlidir **tüm ayrıntılar aşağıda listelenen hello** size hızla yardımcı böylece yardıma gereksiniminiz varsa bir destek mühendisine ile.</span><span class="sxs-lookup"><span data-stu-id="ef947-128">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="ef947-129">Bu yana kolayca yapabilirsiniz **bir ekran görüntüsü alma** veya hello tıklatarak **kopyalama hata simgesi**, hello toohello sağındaki bulundu **kopyalama hatası** textbox.</span><span class="sxs-lookup"><span data-stu-id="ef947-129">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="ef947-130">Açıklanan bildirim ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="ef947-130">Notification Details Explained</span></span>

<span data-ttu-id="ef947-131">Merhaba aşağıdaki daha hangi öğelerin her birini hello bildirim anlamına gelir ve bunların her birini verir örnekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef947-131">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="ef947-132">Temel bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="ef947-132">Essential Notification Items</span></span>

-   <span data-ttu-id="ef947-133">**Başlık** – hello hello bildirim açıklayıcı bir başlık</span><span class="sxs-lookup"><span data-stu-id="ef947-133">**Title** – hello descriptive title of hello notification</span></span>
   *  <span data-ttu-id="ef947-134">Örnek – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="ef947-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ef947-135">**Açıklama** – hello ne hello işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="ef947-135">**Description** – hello description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="ef947-136">Örnek – **girilen iç url başka bir uygulama tarafından zaten kullanılıyor**</span><span class="sxs-lookup"><span data-stu-id="ef947-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="ef947-137">**Bildirim kimliği** – hello bildirim hello benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="ef947-137">**Notification Id** – hello unique id of hello notification</span></span>

   *  <span data-ttu-id="ef947-138">Örnek – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="ef947-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="ef947-139">**İstemci istek kimliği** – tarayıcınız tarafından yapılan hello belirli bir istek kimliği</span><span class="sxs-lookup"><span data-stu-id="ef947-139">**Client Request Id** – hello specific request id made by your browser</span></span>

   *  <span data-ttu-id="ef947-140">Örnek – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="ef947-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="ef947-141">**Zaman damgası UTC** – sırasında hello bildirim meydana geldiği UTC zaman damgası hello</span><span class="sxs-lookup"><span data-stu-id="ef947-141">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

   *  <span data-ttu-id="ef947-142">Örnek – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="ef947-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="ef947-143">**İç işlem kimliği** – kullanabileceğiniz toolook hello hata bizim sistemlerinde iç kimliği hello</span><span class="sxs-lookup"><span data-stu-id="ef947-143">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

   *  <span data-ttu-id="ef947-144">Örnek – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="ef947-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="ef947-145">**UPN** – hello işlemi gerçekleştiren hello kullanıcı</span><span class="sxs-lookup"><span data-stu-id="ef947-145">**UPN** – hello user who performed hello operation</span></span>

   *  <span data-ttu-id="ef947-146">Örnek –**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="ef947-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="ef947-147">**Kiracı kimliği** – hello benzersiz kimliği kullanıcı hello hello Kiracı hello işlemi gerçekleştiren bir üyesi.</span><span class="sxs-lookup"><span data-stu-id="ef947-147">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

   *  <span data-ttu-id="ef947-148">Örnek – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="ef947-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="ef947-149">**Kullanıcı nesnesi kimliği** – hello işlemi gerçekleştiren hello kullanıcının benzersiz Kimliğini hello</span><span class="sxs-lookup"><span data-stu-id="ef947-149">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

 *  <span data-ttu-id="ef947-150">Örnek – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="ef947-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="ef947-151">Ayrıntılı bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="ef947-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="ef947-152">**Görünen ad** – **(boş olabilir)** hello hatası için ayrıntılı bir görünen ad</span><span class="sxs-lookup"><span data-stu-id="ef947-152">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

  *  <span data-ttu-id="ef947-153">Örnek – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="ef947-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ef947-154">**Durum** – hello hello bildirim özel durumu</span><span class="sxs-lookup"><span data-stu-id="ef947-154">**Status** – hello specific status of hello notification</span></span>

   *  <span data-ttu-id="ef947-155">Örnek – **başarısız oldu**</span><span class="sxs-lookup"><span data-stu-id="ef947-155">Example – **Failed**</span></span>

-   <span data-ttu-id="ef947-156">**Nesne Kimliği** – **(boş olabilir)** karşı hangi hello işlemi gerçekleştirildiği nesne kimliği hello</span><span class="sxs-lookup"><span data-stu-id="ef947-156">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

   *  <span data-ttu-id="ef947-157">Örnek – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="ef947-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="ef947-158">**Ayrıntılar** – hello ayrıntılı ne hello işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="ef947-158">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="ef947-159">Örnek – **iç url 'http://bing.com/', zaten kullanımda olduğundan geçersiz**</span><span class="sxs-lookup"><span data-stu-id="ef947-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="ef947-160">**Kopyalama hatası** – tıklatın hello **Kopyala simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba</span><span class="sxs-lookup"><span data-stu-id="ef947-160">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

   *  <span data-ttu-id="ef947-161">Örnek```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="ef947-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef947-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef947-162">Next steps</span></span>
[<span data-ttu-id="ef947-163">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="ef947-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



