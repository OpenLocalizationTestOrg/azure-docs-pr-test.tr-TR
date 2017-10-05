---
title: "Azure remoteapp'te Azure Active Directory kiracısını değiştirme | Microsoft Docs"
description: "Azure RemoteApp ile ilişkili Azure Active Directory kiracısını değiştirme öğrenin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="1a807-103">Azure remoteapp'te Azure Active Directory kiracısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="1a807-103">Change the Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a807-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1a807-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1a807-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="1a807-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1a807-106">Azure RemoteApp kullanıcı erişimine izin vermek için Azure Active Directory (Azure AD) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1a807-106">Azure RemoteApp uses Azure Active Directory (Azure AD) to allow user access.</span></span> <span data-ttu-id="1a807-107">Azure Remoteapp'te kullanabileceğiniz yalnızca Azure AD kiracısı Azure aboneliği ile ilişkili adrestir.</span><span class="sxs-lookup"><span data-stu-id="1a807-107">The only Azure AD tenant that you can use in Azure RemoteApp is the one associated with the Azure subscription.</span></span> <span data-ttu-id="1a807-108">İlişkili abonelik görüntüleyebilirsiniz **ayarları** portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="1a807-108">You can view the associated subscription on the **Settings** page in the portal.</span></span> <span data-ttu-id="1a807-109">Bakmak **Directory** sütunu **abonelikleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1a807-109">Look at the **Directory** column on the **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="1a807-110">Bu değişiklik başarılı olması, var olan tüm Azure RemoteApp koleksiyonları Azure Active Directory kiracısı önce tüm kullanıcıların kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1a807-110">For this change to succeed, first remove all users from the existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="1a807-111">Bunu yapmak için Azure Portalı'na gidin, Git **Azure RemoteApp** sekmesinde ve her bir Azure RemoteApp koleksiyonu açın.</span><span class="sxs-lookup"><span data-stu-id="1a807-111">To do this, go to the Azure Portal, go to the **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="1a807-112">Git **kullanıcılar** sekmesinde ve geçerli Azure Active Directory kiracınıza ait olan kullanıcıların kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1a807-112">Go to the **Users** tab and remove users that belong to your current Azure Active Directory tenant.</span></span> <span data-ttu-id="1a807-113">Tüm mevcut Azure RemoteApp koleksiyonları için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="1a807-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="1a807-114">Bunu yapmazsanız, oluşturmak veya koleksiyonlar düzeltme eki mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="1a807-114">Without doing this, you will not be able to create or patch collections.</span></span>
> 
> 

<span data-ttu-id="1a807-115">Farklı bir kiracı kullanmak istiyorsanız, aboneliğinizi ilişkilendirmesini değiştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1a807-115">If you want to use a different tenant, use these steps to change the association with your subscription:</span></span>

1. <span data-ttu-id="1a807-116">Portalda, Azure AD kullanıcısı için erişim Azure RemoteApp koleksiyonları için verdiniz kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1a807-116">In the portal, remove any Azure AD users to which you’ve given access to Azure RemoteApp collections.</span></span> <span data-ttu-id="1a807-117">(Yukarıdaki adımları için Not bunu nasıl bakın.)</span><span class="sxs-lookup"><span data-stu-id="1a807-117">(See the note above for steps on how to do this.)</span></span>
2. <span data-ttu-id="1a807-118">Bir Microsoft hesabı (eski adıyla Live ID) Hizmet Yöneticisi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1a807-118">Set a Microsoft account (formerly called a Live ID) as the Service administrator.</span></span> <span data-ttu-id="1a807-119">(Hizmet Yöneticisi zaten olup olmadığını bilmiyorsanız?</span><span class="sxs-lookup"><span data-stu-id="1a807-119">(Don't know if you already are the service admin?</span></span> <span data-ttu-id="1a807-120">Tıklayarak öğrenebilirsiniz **ayarlar -> Yöneticiler**.) Şimdi, işte, nasıl değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1a807-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="1a807-121">Sağ üst köşesinde kullanıcı tıklayın ve ardından **faturamı görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="1a807-121">Click the user in the upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="1a807-122">Abonelik'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1a807-122">Click the subscription.</span></span> <span data-ttu-id="1a807-123">Ardından, yeni sayfasında aşağı kaydırın ve tıklatın **Düzenle abonelik ayrıntıları** sağ.</span><span class="sxs-lookup"><span data-stu-id="1a807-123">Then, on the new page, scroll down and click **Edit subscription details** in the right.</span></span> <span data-ttu-id="1a807-124">(Bu varsa sağ Orta alt tür bulmanıza yardımcı olur.)</span><span class="sxs-lookup"><span data-stu-id="1a807-124">(Sort of the middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="1a807-125">Hizmet Yöneticisi olmalıdır kullanıcının Microsoft hesabını girin</span><span class="sxs-lookup"><span data-stu-id="1a807-125">Type the Microsoft account for the user that should be the service admin.</span></span>
3. <span data-ttu-id="1a807-126">Şimdi portal dışında oturum ve ardından önceki adımda belirtilen Microsoft hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1a807-126">Now, sign out of the portal, and then sign back in with the Microsoft account you specified in the previous step.</span></span>
4. <span data-ttu-id="1a807-127">' I tıklatın **yeni App -> hizmetler -> Active Directory dizin -> özel -> oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="1a807-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="1a807-128">Altında **Directory**, seçin **var olan dizini kullan**.</span><span class="sxs-lookup"><span data-stu-id="1a807-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="1a807-129">Şimdi portal dışında oturum, bu nedenle seçin olmasını yapacağız **şimdi oturumunuz için hazır ben**.</span><span class="sxs-lookup"><span data-stu-id="1a807-129">We're going to have to sign you out of the portal now, so choose **I am ready to be signed out now**.</span></span>
6. <span data-ttu-id="1a807-130">Oturum Portalı'na eklemek istediğiniz dizinin genel Yöneticisi olarak yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="1a807-130">Sign back into the portal as a global admin of the directory you want to add.</span></span> <span data-ttu-id="1a807-131">(Genel yönetici zaten doğru değilse, sonra bir turu olacaktır oturum açın ve sonra oturumu kapatın.)</span><span class="sxs-lookup"><span data-stu-id="1a807-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="1a807-132">Oturum açtığınızda aboneliğinizde var olan AD kiracınıza kullanmak isteyip istemediğinizi istenir.</span><span class="sxs-lookup"><span data-stu-id="1a807-132">You'll be asked when you sign in if you want to use your existing AD tenant with your subscription.</span></span> <span data-ttu-id="1a807-133">Tıklatın **devam**ve ardından **şimdi oturumu**.</span><span class="sxs-lookup"><span data-stu-id="1a807-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="1a807-134">Yeniden yeniden oturum açın ve geri dönüp **ayarlar -> abonelikler**.</span><span class="sxs-lookup"><span data-stu-id="1a807-134">Sign back in again, and go back to **Settings -> Subscriptions**.</span></span> <span data-ttu-id="1a807-135">Aboneliğinizi seçin ve ardından **dizini Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="1a807-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="1a807-136">Kullanmak istediğiniz Azure AD kiracısı seçin.</span><span class="sxs-lookup"><span data-stu-id="1a807-136">Select the Azure AD tenant that you want to use.</span></span>

<span data-ttu-id="1a807-137">Şimdi kullanım yeni Azure AD Kiracı Azure aboneliği erişimi denetlemek ve Azure RemoteApp kullanıcı erişimi yapılandırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a807-137">You can now use the new Azure AD tenant to control access to the Azure subscription and to configure user access in Azure RemoteApp.</span></span>

