---
title: "Self Servis uygulamaya erişim ile sorunu | Microsoft Docs"
description: "Self Servis uygulamaya erişim izni ilgili sorunları giderme"
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
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="5c44f-103">Self Servis uygulamaya erişim ile sorunu</span><span class="sxs-lookup"><span data-stu-id="5c44f-103">Problem using self-service application access</span></span>

<span data-ttu-id="5c44f-104">Self Servis uygulamaya erişim uygulamaları, kendi kendine Bul yapmalarına izin vermek için mükemmel bir yoldur bu uygulamalara erişimi onaylamak için iş grubuna isteğe bağlı olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c44f-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="5c44f-105">Bu kullanıcılar için parola çoklu oturum uygulamalar üzerinde sağ bunların erişim paneller atanan kimlik bilgilerini yönetmek iş grubuna izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c44f-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="5c44f-106">Kullanıcılarınıza kendi erişim paneli uygulamaları kendi kendine bulabilmesi için öncelikle etkinleştirmeniz gerekiyor **Self Servis uygulamaya erişim** otomatik olarak bulmak ve istemek kullanıcılara izin vermek istediğiniz herhangi bir uygulama erişimi.</span><span class="sxs-lookup"><span data-stu-id="5c44f-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="5c44f-107">İlk denetlemek için genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="5c44f-107">General issues to check first</span></span>

-   <span data-ttu-id="5c44f-108">Self Servis uygulama erişiminin doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="5c44f-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="5c44f-109">"Self-Servis uygulama erişim ilkesi nasıl yapılandırılır" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="5c44f-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="5c44f-110">Kullanıcı veya grup Self Servis uygulamaya erişim istemek için etkinleştirilmiş olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5c44f-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="5c44f-111">Kullanıcı Self Servis uygulamaya erişim için doğru yere ziyaret emin olun.</span><span class="sxs-lookup"><span data-stu-id="5c44f-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="5c44f-112">Kullanıcılar gidin kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tıklatıp **+ Ekle** Self Servis erişim etkin uygulamalar Bul düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c44f-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="5c44f-113">Self Servis uygulamaya erişim yalnızca son yapılandırıldıysa, içeri ve dışarı kullanıcının erişim paneline birkaç dakika sonra Self Servis erişim değişikliklerini görüntülenmediğini görmek için oturum yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="5c44f-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="5c44f-114">Self Servis uygulama erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c44f-114">How to configure self-service application access</span></span>

<span data-ttu-id="5c44f-115">Bir uygulama Self Servis uygulama erişimi etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5c44f-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5c44f-116">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="5c44f-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5c44f-117">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="5c44f-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5c44f-118">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="5c44f-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5c44f-119">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5c44f-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5c44f-120">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="5c44f-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5c44f-121">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="5c44f-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5c44f-122">Self Servis etkinleştirmek istediğiniz uygulamayı seçin listeden erişmek için.</span><span class="sxs-lookup"><span data-stu-id="5c44f-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="5c44f-123">Uygulamanın yüklediği sonra tıklayın **Self Servis** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5c44f-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5c44f-124">Bu uygulama için Self Servis uygulama erişimini etkinleştirmek için Aç **bu uygulamaya erişmek kullanıcıların?** geç **Evet.**</span><span class="sxs-lookup"><span data-stu-id="5c44f-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="5c44f-125">Ardından, isteyen hangi kullanıcıların bu uygulamaya erişim eklenecek grubu seçmek için etiketi yanındaki seçiciyi **hangi grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="5c44f-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="5c44f-126">**İsteğe bağlı:** önce iş onayı iste isterseniz, kullanıcılara erişim verilir, Ayarla **bu uygulamaya erişim vermeden önce onay gerektirir?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="5c44f-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="5c44f-127">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** onaylanan kullanıcılar için bu uygulamaya gönderilen parolalar belirtmek bu iş onaylayanlar izin vermek istiyorsanız, Ayarla **bu uygulama için kullanıcının parola ayarlamak onaylayanlar izin?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="5c44f-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="5c44f-128">**İsteğe bağlı:** bu uygulamaya erişimi onaylamak için izin verilen iş onaylayanlar belirtmek için etiketi yanındaki seçiciyi **kimin bu uygulamaya erişimi onaylamak için verilir?** en fazla 10 ayrı ayrı iş onaylayanlar seçin.</span><span class="sxs-lookup"><span data-stu-id="5c44f-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="5c44f-129">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5c44f-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="5c44f-130">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, Self Servis onaylanan kullanıcılar role atamak istiyorsanız Seçici tıklayın **hangi rolü için kullanıcıları bu uygulamada atanmalıdır?** , bu kullanıcılar atanabilir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="5c44f-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="5c44f-131">Tıklatın **kaydetmek** tamamlamak için dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c44f-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="5c44f-132">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar için gezinebilir kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tıklatıp **+ Ekle** Self Servis erişim etkin uygulamalar Bul düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c44f-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="5c44f-133">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5c44f-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="5c44f-134">Bir kullanıcı kendi onay gerektiren bir uygulamaya erişim istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c44f-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="5c44f-135">Bu onaylar birden çok onaylayanlar belirtirseniz, tek bir onaylayan uygulaması'na erişimi onaylamak yani tek onay iş akışları yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="5c44f-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="5c44f-136">Bu sorun giderme adımları sorunu çözmezse</span><span class="sxs-lookup"><span data-stu-id="5c44f-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="5c44f-137">bir destek bileti aşağıdaki bilgilerle varsa açın:</span><span class="sxs-lookup"><span data-stu-id="5c44f-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5c44f-138">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="5c44f-138">Correlation error ID</span></span>

-   <span data-ttu-id="5c44f-139">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="5c44f-139">UPN (user email address)</span></span>

-   <span data-ttu-id="5c44f-140">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="5c44f-140">TenantID</span></span>

-   <span data-ttu-id="5c44f-141">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="5c44f-141">Browser type</span></span>

-   <span data-ttu-id="5c44f-142">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="5c44f-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5c44f-143">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="5c44f-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c44f-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c44f-144">Next steps</span></span>
[<span data-ttu-id="5c44f-145">Self Servis Grup Yönetimi için Azure Active Directory ayarlayan</span><span class="sxs-lookup"><span data-stu-id="5c44f-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
