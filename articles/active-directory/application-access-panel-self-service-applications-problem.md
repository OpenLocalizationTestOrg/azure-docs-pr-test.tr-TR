---
title: "Self Servis uygulamaya erişim kullanarak aaaProblem | Microsoft Docs"
description: "Sorunları ilgili tooself hizmet uygulaması erişim sorunlarını giderme"
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
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="3e63e-103">Self Servis uygulamaya erişim ile sorunu</span><span class="sxs-lookup"><span data-stu-id="3e63e-103">Problem using self-service application access</span></span>

<span data-ttu-id="3e63e-104">Self Servis uygulama erişimi olan mükemmel şekilde tooallow kullanıcılar tooself-uygulamaları bulmak, isteğe bağlı olarak hello iş grubu tooapprove erişimi toothose uygulamaları izin verin.</span><span class="sxs-lookup"><span data-stu-id="3e63e-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="3e63e-105">Merhaba iş grubu toomanage hello kimlik toothose kullanıcılar kendi access panel üzerinde parola çoklu oturum uygulamaları sağdan için atanan izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e63e-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="3e63e-106">Kullanıcılarınıza kendi erişim paneli uygulamaları kendi kendine bulabilmesi için öncelikle tooenable gerek **Self Servis uygulamaya erişim** tooallow kullanıcılar tooself istediğiniz tooany uygulamaları-bulmak ve erişim isteği.</span><span class="sxs-lookup"><span data-stu-id="3e63e-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="3e63e-107">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="3e63e-107">General issues toocheck first</span></span>

-   <span data-ttu-id="3e63e-108">Self Servis uygulama erişiminin doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e63e-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="3e63e-109">"Nasıl tooconfigure Self Servis uygulamaya erişim" bakın.</span><span class="sxs-lookup"><span data-stu-id="3e63e-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="3e63e-110">Merhaba kullanıcı veya grup süredir emin olun toorequest Self Servis uygulamaya erişim etkin.</span><span class="sxs-lookup"><span data-stu-id="3e63e-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="3e63e-111">Merhaba kullanıcı Self Servis uygulamaya erişim için doğru yerde hello ziyaret emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e63e-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="3e63e-112">Kullanıcıların tootheir gidin [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello tıklatıp **+ Ekle** düğmesini toofind hello uygulamaları toowhich Self Servis erişim etkinleştirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="3e63e-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="3e63e-113">Self Servis uygulamaya erişim yalnızca son yapılandırıldıysa, hello Self Servis erişim değişikliklerini görünen toosign içeri ve dışarı yeniden hello kullanıcının erişim paneline sonra birkaç dakika toosee deneyin.</span><span class="sxs-lookup"><span data-stu-id="3e63e-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="3e63e-114">Nasıl tooconfigure Self Servis uygulamaya erişim</span><span class="sxs-lookup"><span data-stu-id="3e63e-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="3e63e-115">tooenable Self Servis uygulama erişim tooan uygulaması, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3e63e-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3e63e-116">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="3e63e-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3e63e-117">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="3e63e-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3e63e-118">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="3e63e-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e63e-119">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3e63e-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3e63e-120">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="3e63e-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3e63e-121">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="3e63e-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3e63e-122">Tooenable Self Servis erişim toofrom hello listesi hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3e63e-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="3e63e-123">Merhaba uygulamanın yüklediği sonra tıklayın **Self Servis** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3e63e-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3e63e-124">tooenable bu uygulama için Self Servis uygulama erişimi etkinleştirmek hello **toorequest erişim toothis uygulama kullanıcıların?** çok geçiş**Evet.**</span><span class="sxs-lookup"><span data-stu-id="3e63e-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="3e63e-125">Ardından, access toothis uygulaması eklenmesi, isteyen tooselect hello Grup toowhich kullanıcılar'ı tıklatın hello Seçici sonraki toohello etiket **toowhich grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="3e63e-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="3e63e-126">**İsteğe bağlı:** kullanıcıların erişim izin verilmeden önce bir iş onay toorequire isterseniz, hello ayarlamak **erişim toothis uygulama vermeden önce onay gerektirir?** çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="3e63e-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="3e63e-127">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** toothis uygulama onaylanan kullanıcılar için gönderilen bu iş onaylayanlar toospecify hello parolaları tooallow isterseniz hello ayarlamak **izin onaylayanlar tooset Bu uygulama için kullanıcının parola?**  çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="3e63e-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="3e63e-128">**İsteğe bağlı:** tooapprove erişim toothis uygulama, izin verilen toospecify hello iş onaylayanlar tıklatın hello Seçici sonraki toohello etiket **kimin tooapprove erişim toothis uygulama verilir?** tooselect ayarlama too10 ayrı ayrı iş onaylayanlar.</span><span class="sxs-lookup"><span data-stu-id="3e63e-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="3e63e-129">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="3e63e-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="3e63e-130">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, tooassign Self Servis onaylanan kullanıcılar tooa rol istiyorsanız hello Seçici sonraki toohello tıklatın **toowhich rol kullanıcılar bu atanmalıdır Uygulama?**  tooselect hello rol toowhich bu kullanıcılar atanabilir.</span><span class="sxs-lookup"><span data-stu-id="3e63e-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="3e63e-131">Merhaba tıklatın **kaydetmek** hello dikey toofinish hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3e63e-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="3e63e-132">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar tootheir gezinebilir [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello tıklatıp **+ Ekle** düğmesini toofind hello uygulamaları toowhich etkinleştirdiğiniz Self Servis erişim.</span><span class="sxs-lookup"><span data-stu-id="3e63e-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="3e63e-133">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3e63e-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="3e63e-134">Bir kullanıcı kendi onay gerektiren erişim tooan uygulama istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e63e-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="3e63e-135">Bu onaylar birden çok onaylayanlar belirtirseniz, tek bir onaylayan erişim toohello uygulamayı Onayla yani tek onay iş akışları yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="3e63e-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="3e63e-136">Bu sorun giderme adımları hello sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="3e63e-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="3e63e-137">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="3e63e-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="3e63e-138">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="3e63e-138">Correlation error ID</span></span>

-   <span data-ttu-id="3e63e-139">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="3e63e-139">UPN (user email address)</span></span>

-   <span data-ttu-id="3e63e-140">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="3e63e-140">TenantID</span></span>

-   <span data-ttu-id="3e63e-141">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="3e63e-141">Browser type</span></span>

-   <span data-ttu-id="3e63e-142">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="3e63e-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3e63e-143">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="3e63e-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e63e-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e63e-144">Next steps</span></span>
[<span data-ttu-id="3e63e-145">Self Servis Grup Yönetimi için Azure Active Directory ayarlayan</span><span class="sxs-lookup"><span data-stu-id="3e63e-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
