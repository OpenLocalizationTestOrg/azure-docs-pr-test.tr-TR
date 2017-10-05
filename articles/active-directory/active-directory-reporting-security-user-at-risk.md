---
title: "Azure Active Directory portalında risk güvenliği raporu için işaretlenmiş kullanıcılar | Microsoft Docs"
description: "Azure Active Directory portalında risk güvenliği için işaretlenmiş kullanıcılar hakkında bilgi edinin"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="7e217-103">Azure Active Directory portalında risk güvenliği için işaretlenmiş kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="7e217-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="7e217-104">Azure Active Directory’de (Azure AD) güvenlik raporları ile ortamınızda güvenliği tehlikeye girmiş kullanıcı hesaplarının olasılığı hakkında bilgi sahibi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="7e217-105">Azure Active Directory, kullanıcı hesaplarınızla ilgili kuşkulu eylemleri algılar.</span><span class="sxs-lookup"><span data-stu-id="7e217-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="7e217-106">Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7e217-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="7e217-107">Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="7e217-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="7e217-108">Algılanan risk olayları aşağıdakileri hesaplamak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7e217-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="7e217-109">**Riskli oturum açma işlemleri** - Riskli oturum açma işlemi bir kullanıcı hesabının meşru sahibi olmayan bir kişi tarafından gerçekleştirilmiş olabilecek oturum açma girişiminin göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="7e217-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="7e217-110">Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="7e217-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="7e217-111">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="7e217-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="7e217-112">Daha fazla bilgi için bkz. [Risk için işaretlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="7e217-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="7e217-113">Güvenlik raporlarını, Azure portalında **Azure Active Directory** dikey penceresindeki **Güvenlik** bölümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="7e217-115">Güvenlik raporuna erişebilmek için hangi Azure AD lisansınızın olması gerekir?</span><span class="sxs-lookup"><span data-stu-id="7e217-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="7e217-116">Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve risk raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7e217-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="7e217-117">Bununla birlikte, rapordaki ayrıntı düzeyi sürümler arasında değişiklik gösterir:</span><span class="sxs-lookup"><span data-stu-id="7e217-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="7e217-118">**Azure Active Directory Ücretsiz ve Temel sürümlerinde**, riskli olduğu belirlenen kullanıcıların listesini zaten alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7e217-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="7e217-119">**Azure Active Directory Premium 1** sürümü bu modeli genişleterek her raporda algılanmış olan temel risk olaylarından bazılarını incelemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7e217-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="7e217-120">**Azure Active Directory Premium 2** sürümü, tüm temel risk olayları hakkında en ayrıntılı bilgileri sağlar ve yapılandırılmış risk düzeylerine otomatik olarak yanıt veren güvenlik ilkeleri yapılandırmanıza da olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7e217-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="7e217-121">Azure Active Directory ücretsiz ve temel sürümleri</span><span class="sxs-lookup"><span data-stu-id="7e217-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="7e217-122">Azure Active Directory ücretsiz ve temel sürümlerinde risk için işaretlenmiş kullanıcılar raporu, tehlikeye girmiş olabilecek kullanıcı hesaplarının bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e217-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="7e217-124">Bir kullanıcının seçilmesi, ilgili kullanıcı verileri dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="7e217-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="7e217-125">Risk altındaki kullanıcılarla ilgili olarak kullanıcının oturum açma geçmişini gözden geçirebilir ve gerekirse parolasını sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="7e217-127">Bu iletişim kutusu size şu seçeneği sunar:</span><span class="sxs-lookup"><span data-stu-id="7e217-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="7e217-128">Raporu indirme</span><span class="sxs-lookup"><span data-stu-id="7e217-128">Download the report</span></span>

- <span data-ttu-id="7e217-129">Kullanıcılarda arama</span><span class="sxs-lookup"><span data-stu-id="7e217-129">Search users</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="7e217-131">Azure Active Directory premium sürümleri</span><span class="sxs-lookup"><span data-stu-id="7e217-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="7e217-132">Azure Active Directory premium sürümlerinde risk için işaretlenmiş kullanıcılar raporu aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="7e217-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="7e217-133">Tehlikeye girmiş olabilecek [kullanıcı hesaplarının listesi](active-directory-identityprotection.md#users-flagged-for-risk)</span><span class="sxs-lookup"><span data-stu-id="7e217-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="7e217-134">Algılanan [risk olayı türleri](active-directory-identity-protection-risk-events.md) hakkında toplu bilgiler</span><span class="sxs-lookup"><span data-stu-id="7e217-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="7e217-135">Raporu indirme seçeneği</span><span class="sxs-lookup"><span data-stu-id="7e217-135">An option to download the report</span></span>

- <span data-ttu-id="7e217-136">[Kullanıcı riskini azaltma ilkesi](active-directory-identityprotection.md#user-risk-security-policy) yapılandırma seçeneği</span><span class="sxs-lookup"><span data-stu-id="7e217-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="7e217-138">Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="7e217-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="7e217-139">Tüm oturum açma işlemleri görünümünü açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="7e217-140">Kullanıcının parolasını sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-140">Reset the user's password</span></span>

- <span data-ttu-id="7e217-141">Tüm olayları kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-141">Dismiss all events</span></span>

- <span data-ttu-id="7e217-142">Kullanıcıya ilişkin bildirilmiş risk olaylarını araştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e217-142">Investigate reported risk events for the user.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="7e217-144">Bir risk olayını araştırmak için listeden bir olay seçerek bu olayın **Ayrıntılar** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="7e217-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="7e217-145">**Ayrıntılar** dikey penceresinde, [risk olayını elle kapatma](active-directory-identityprotection.md#closing-risk-events-manually) ve elle kapatılmış risk olayını yeniden etkinleştirme seçenekleri sunulur.</span><span class="sxs-lookup"><span data-stu-id="7e217-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="7e217-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e217-147">Next steps</span></span>

- <span data-ttu-id="7e217-148">Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="7e217-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

