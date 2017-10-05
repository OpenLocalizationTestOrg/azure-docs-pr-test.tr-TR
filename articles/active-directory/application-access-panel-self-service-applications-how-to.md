---
title: "Self Servis uygulamaya erişim kullanma | Microsoft Docs"
description: "Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir"
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
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="523df-103">Self Servis uygulamaya erişim kullanma</span><span class="sxs-lookup"><span data-stu-id="523df-103">How to use self-service application access</span></span>

<span data-ttu-id="523df-104">Kullanıcılarınıza kendi erişim paneli uygulamaları kendi kendine bulabilmesi için öncelikle etkinleştirmeniz gerekiyor **Self Servis uygulamaya erişim** otomatik olarak bulmak ve istemek kullanıcılara izin vermek istediğiniz herhangi bir uygulama erişimi.</span><span class="sxs-lookup"><span data-stu-id="523df-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="523df-105">Bu özellik, zaman ve para bir BT grubu olarak kaydetmek mükemmel bir yoldur ve Azure Active Directory ile modern uygulamalar dağıtımının bir parçası olarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="523df-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="523df-106">Bu özelliği kullanarak, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="523df-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="523df-107">Kullanıcıların uygulamalardan Self Bul izin [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) BT grubu rahatsız etme olmadan.</span><span class="sxs-lookup"><span data-stu-id="523df-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="523df-108">Erişim isteğinde bulundu bkz, erişimi kaldırmak ve atanmış rollerini yönetmek için bu kullanıcıların önceden yapılandırılmış bir gruba ekleyin.</span><span class="sxs-lookup"><span data-stu-id="523df-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="523df-109">İsteğe bağlı olarak BT grubu sahip değil için uygulama erişim isteklerini onaylamak bir iş onaylayan izin verir.</span><span class="sxs-lookup"><span data-stu-id="523df-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="523df-110">İsteğe bağlı olarak bu uygulamaya erişim onaylaması en fazla 10 kişiler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="523df-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="523df-111">İsteğe bağlı olarak bir iş izin kullanıcılarla parolalar ayarlamak için onaylayan uygulamaya sağ iş onaylayanın oturum açmak için kullanabileceğiniz [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="523df-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="523df-112">İsteğe bağlı olarak otomatik olarak Self Servis kullanıcıları için uygulama rolü doğrudan atanmış atayın.</span><span class="sxs-lookup"><span data-stu-id="523df-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="523df-113">Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="523df-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="523df-114">Self Servis uygulamaya erişim uygulamaları, kendi kendine Bul yapmalarına izin vermek için mükemmel bir yoldur bu uygulamalara erişimi onaylamak için iş grubuna isteğe bağlı olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="523df-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="523df-115">Bu kullanıcılar için parola çoklu oturum uygulamalar üzerinde sağ bunların erişim paneller atanan kimlik bilgilerini yönetmek iş grubuna izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523df-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="523df-116">Bir uygulama Self Servis uygulama erişimi etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="523df-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="523df-117">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="523df-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="523df-118">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="523df-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="523df-119">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="523df-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="523df-120">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="523df-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="523df-121">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="523df-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="523df-122">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="523df-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="523df-123">Self Servis etkinleştirmek istediğiniz uygulamayı seçin listeden erişmek için.</span><span class="sxs-lookup"><span data-stu-id="523df-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="523df-124">Uygulamanın yüklediği sonra tıklayın **Self Servis** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="523df-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="523df-125">Bu uygulama için Self Servis uygulama erişimini etkinleştirmek için Aç **bu uygulamaya erişmek kullanıcıların?** geç **Evet.**</span><span class="sxs-lookup"><span data-stu-id="523df-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="523df-126">Ardından, isteyen hangi kullanıcıların bu uygulamaya erişim eklenecek grubu seçmek için etiketi yanındaki seçiciyi **hangi grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="523df-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="523df-127">**İsteğe bağlı:** önce iş onayı iste isterseniz, kullanıcılara erişim verilir, Ayarla **bu uygulamaya erişim vermeden önce onay gerektirir?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="523df-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="523df-128">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** onaylanan kullanıcılar için bu uygulamaya gönderilen parolalar belirtmek bu iş onaylayanlar izin vermek istiyorsanız, Ayarla **bu uygulama için kullanıcının parola ayarlamak onaylayanlar izin?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="523df-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="523df-129">**İsteğe bağlı:** bu uygulamaya erişimi onaylamak için izin verilen iş onaylayanlar belirtmek için etiketi yanındaki seçiciyi **kimin bu uygulamaya erişimi onaylamak için verilir?** en fazla 10 ayrı ayrı iş onaylayanlar seçin.</span><span class="sxs-lookup"><span data-stu-id="523df-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="523df-130">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="523df-130">Groups are not supported.</span></span>

13. <span data-ttu-id="523df-131">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, Self Servis onaylanan kullanıcılar role atamak istiyorsanız Seçici tıklayın **hangi rolü için kullanıcıları bu uygulamada atanmalıdır?** , bu kullanıcılar atanabilir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="523df-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="523df-132">Tıklatın **kaydetmek** tamamlamak için dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="523df-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="523df-133">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar için gezinebilir kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tıklatıp **+ Ekle** Self Servis erişim etkin uygulamalar Bul düğmesi.</span><span class="sxs-lookup"><span data-stu-id="523df-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="523df-134">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="523df-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="523df-135">Bir kullanıcı kendi onay gerektiren bir uygulamaya erişim istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523df-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="523df-136">Bu onaylar birden çok onaylayanlar belirtirseniz, tek bir onaylayan uygulaması'na erişimi onaylamak yani tek onay iş akışları yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="523df-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="523df-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="523df-137">Next steps</span></span>
[<span data-ttu-id="523df-138">Self Servis Grup Yönetimi için Azure Active Directory ayarlayan</span><span class="sxs-lookup"><span data-stu-id="523df-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
