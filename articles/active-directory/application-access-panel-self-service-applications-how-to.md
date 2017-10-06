---
title: "aaaHow toouse Self Servis uygulamaya erişim | Microsoft Docs"
description: "Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="d91ee-103">Nasıl toouse Self Servis uygulamaya erişim</span><span class="sxs-lookup"><span data-stu-id="d91ee-103">How toouse self-service application access</span></span>

<span data-ttu-id="d91ee-104">Kullanıcılarınıza kendi erişim paneli uygulamaları kendi kendine bulabilmesi için öncelikle tooenable gerek **Self Servis uygulamaya erişim** tooallow kullanıcılar tooself istediğiniz tooany uygulamaları-bulmak ve erişim isteği.</span><span class="sxs-lookup"><span data-stu-id="d91ee-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="d91ee-105">Bu özellik toosave zaman ve para BT grubu olarak harika bir yol olduğu ve Azure Active Directory ile modern uygulamalar dağıtımının bir parçası olarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="d91ee-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="d91ee-106">Bu özelliği kullanarak, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91ee-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="d91ee-107">Merhaba uygulamalardan otomatik olarak bulmak, kullanıcıların izin [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello BT rahatsız etme olmadan grup.</span><span class="sxs-lookup"><span data-stu-id="d91ee-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="d91ee-108">Erişim isteğinde bulundu bkz, erişimi kaldırmak ve toothem atanan hello rollerini yönetmek için bu kullanıcıların tooa önceden yapılandırılmış grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d91ee-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="d91ee-109">İsteğe bağlı olarak Hello BT grubu sahip değil şekilde bir iş onaylayan tooapprove uygulama erişim isteklerini izin verir.</span><span class="sxs-lookup"><span data-stu-id="d91ee-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="d91ee-110">İsteğe bağlı olarak erişim toothis uygulama onaylaması too10 kişiler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d91ee-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="d91ee-111">İsteğe bağlı olarak bir iş onaylayan tooset hello parolalara izin ver kullanıcılarla toosign toohello uygulamasından, sağa hello iş onaylayanın kullanabilirsiniz [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d91ee-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="d91ee-112">İsteğe bağlı olarak otomatik olarak doğrudan kendine atanan kullanıcılar tooan uygulama rolü atayın.</span><span class="sxs-lookup"><span data-stu-id="d91ee-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="d91ee-113">Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d91ee-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="d91ee-114">Self Servis uygulama erişimi olan mükemmel şekilde tooallow kullanıcılar tooself-uygulamaları bulmak, isteğe bağlı olarak hello iş grubu tooapprove erişimi toothose uygulamaları izin verin.</span><span class="sxs-lookup"><span data-stu-id="d91ee-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="d91ee-115">Merhaba iş grubu toomanage hello kimlik toothose kullanıcılar kendi access panel üzerinde parola çoklu oturum uygulamaları sağdan için atanan izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ee-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="d91ee-116">tooenable Self Servis uygulama erişim tooan uygulaması, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d91ee-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d91ee-117">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="d91ee-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d91ee-118">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d91ee-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d91ee-119">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d91ee-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d91ee-120">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d91ee-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d91ee-121">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d91ee-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d91ee-122">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d91ee-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d91ee-123">Tooenable Self Servis erişim toofrom hello listesi hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d91ee-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="d91ee-124">Merhaba uygulamanın yüklediği sonra tıklayın **Self Servis** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d91ee-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d91ee-125">tooenable bu uygulama için Self Servis uygulama erişimi etkinleştirmek hello **toorequest erişim toothis uygulama kullanıcıların?** çok geçiş**Evet.**</span><span class="sxs-lookup"><span data-stu-id="d91ee-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="d91ee-126">Ardından, access toothis uygulaması eklenmesi, isteyen tooselect hello Grup toowhich kullanıcılar'ı tıklatın hello Seçici sonraki toohello etiket **toowhich grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="d91ee-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="d91ee-127">**İsteğe bağlı:** kullanıcıların erişim izin verilmeden önce bir iş onay toorequire isterseniz, hello ayarlamak **erişim toothis uygulama vermeden önce onay gerektirir?** çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="d91ee-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="d91ee-128">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** toothis uygulama onaylanan kullanıcılar için gönderilen bu iş onaylayanlar toospecify hello parolaları tooallow isterseniz hello ayarlamak **izin onaylayanlar tooset Bu uygulama için kullanıcının parola?**  çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="d91ee-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="d91ee-129">**İsteğe bağlı:** tooapprove erişim toothis uygulama, izin verilen toospecify hello iş onaylayanlar tıklatın hello Seçici sonraki toohello etiket **kimin tooapprove erişim toothis uygulama verilir?** tooselect ayarlama too10 ayrı ayrı iş onaylayanlar.</span><span class="sxs-lookup"><span data-stu-id="d91ee-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="d91ee-130">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d91ee-130">Groups are not supported.</span></span>

13. <span data-ttu-id="d91ee-131">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, tooassign Self Servis onaylanan kullanıcılar tooa rol istiyorsanız hello Seçici sonraki toohello tıklatın **toowhich rol kullanıcılar bu atanmalıdır Uygulama?**  tooselect hello rol toowhich bu kullanıcılar atanabilir.</span><span class="sxs-lookup"><span data-stu-id="d91ee-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="d91ee-132">Merhaba tıklatın **kaydetmek** hello dikey toofinish hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d91ee-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="d91ee-133">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar tootheir gezinebilir [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello tıklatıp **+ Ekle** düğmesini toofind hello uygulamaları toowhich etkinleştirdiğiniz Self Servis erişim.</span><span class="sxs-lookup"><span data-stu-id="d91ee-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="d91ee-134">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d91ee-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="d91ee-135">Bir kullanıcı kendi onay gerektiren erişim tooan uygulama istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91ee-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="d91ee-136">Bu onaylar birden çok onaylayanlar belirtirseniz, tek bir onaylayan erişim toohello uygulamayı Onayla yani tek onay iş akışları yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="d91ee-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91ee-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d91ee-137">Next steps</span></span>
[<span data-ttu-id="d91ee-138">Self Servis Grup Yönetimi için Azure Active Directory ayarlayan</span><span class="sxs-lookup"><span data-stu-id="d91ee-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
