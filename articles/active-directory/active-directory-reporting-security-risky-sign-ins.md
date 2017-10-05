---
title: "Azure Active Directory portalındaki riskli oturum açma işlemleri raporu | Microsoft Docs"
description: "Azure Active Directory portalındaki riskli oturum açma işlemleri raporu hakkında bilgi edinin"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 45a6f63bd920c9a70c25b8dfae084ea030256cf4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="02f94-103">Azure Active Directory portalındaki riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="02f94-103">Risky sign-ins report in the Azure Active Directory portal</span></span>

<span data-ttu-id="02f94-104">Azure Active Directory’de (Azure AD) güvenlik raporları ile ortamınızda güvenliği tehlikeye girmiş kullanıcı hesaplarının olasılığı hakkında bilgi sahibi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-104">With the security reports in Azure Active Directory (Azure AD) you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="02f94-105">Azure AD, kullanıcı hesaplarınızla ilgili kuşkulu eylemleri algılar.</span><span class="sxs-lookup"><span data-stu-id="02f94-105">Azure AD detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="02f94-106">Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="02f94-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="02f94-107">Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="02f94-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="02f94-108">Algılanan risk olayları aşağıdakileri hesaplamak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="02f94-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="02f94-109">**Riskli oturum açma işlemleri** - Riskli oturum açma işlemi bir kullanıcı hesabının meşru sahibi olmayan bir kişi tarafından gerçekleştirilmiş olabilecek oturum açma girişiminin göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="02f94-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="02f94-110">Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="02f94-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="02f94-111">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="02f94-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="02f94-112">Daha fazla bilgi için bkz. [Riskli oldukları belirlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="02f94-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="02f94-113">Güvenlik raporlarını, [Azure portalının](https://portal.azure.com) **Azure Active Directory** dikey penceresindeki **Güvenlik** bölümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-113">In [the Azure portal](https://portal.azure.com), you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span> 

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="02f94-115">Güvenlik raporuna erişebilmek için hangi Azure AD lisansınızın olması gerekir?</span><span class="sxs-lookup"><span data-stu-id="02f94-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="02f94-116">Azure Active Directory'nin tüm sürümlerinde size riskli oturum açma işlemleri raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="02f94-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="02f94-117">Bununla birlikte, rapordaki ayrıntı düzeyi sürümler arasında değişiklik gösterir:</span><span class="sxs-lookup"><span data-stu-id="02f94-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="02f94-118">**Azure Active Directory Ücretsiz ve Temel sürümlerinde**, riskli oturum açmaların bir listesini zaten alırsınız.</span><span class="sxs-lookup"><span data-stu-id="02f94-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="02f94-119">**Azure Active Directory Premium 1** sürümü bu modeli genişleterek her raporda algılanmış olan temel risk olaylarından bazılarını incelemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="02f94-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="02f94-120">**Azure Active Directory Premium 2** sürümü, tüm temel risk olayları hakkında en ayrıntılı bilgileri sağlar ve ayrıca, yapılandırılmış risk düzeylerine otomatik olarak yanıt veren güvenlik ilkeleri yapılandırmanıza da olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="02f94-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="02f94-121">Azure Active Directory ücretsiz ve temel sürümleri</span><span class="sxs-lookup"><span data-stu-id="02f94-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="02f94-122">Azure Active Directory ücretsiz ve temel sürümleri, kullanıcılarınızla ilgili algılanan riskli oturum açma işlemlerinin listesini sunar.</span><span class="sxs-lookup"><span data-stu-id="02f94-122">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="02f94-123">Bu raporda şunlar listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="02f94-123">This report lists:</span></span>

- <span data-ttu-id="02f94-124">**Kullanıcı** - Oturum açma işlemi sırasında kullanılan kullanıcının adı</span><span class="sxs-lookup"><span data-stu-id="02f94-124">**User** - The name of the user that was used during the sign-in operation</span></span>
- <span data-ttu-id="02f94-125">**IP** - Azure Active Directory'ye bağlanmak için kullanılan cihazın IP adresi</span><span class="sxs-lookup"><span data-stu-id="02f94-125">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="02f94-126">**Konum** - Azure Active Directory'ye bağlanmak için kullanılan konum</span><span class="sxs-lookup"><span data-stu-id="02f94-126">**Location** - The location used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="02f94-127">**Oturum açma saati** - Oturum açma işleminin gerçekleştirildiği saat</span><span class="sxs-lookup"><span data-stu-id="02f94-127">**Sign-in time** - The time when the sign-in was performed</span></span>
- <span data-ttu-id="02f94-128">**Durum** - Oturum açma durumu</span><span class="sxs-lookup"><span data-stu-id="02f94-128">**Status** - The status of the sign-in</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="02f94-130">Riskli oturum açma işlemi araştırmanıza göre, Azure Active Directory'ye aşağıdaki eylemlerle geri bildirim sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="02f94-130">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span></span>

- <span data-ttu-id="02f94-131">Çözümleme</span><span class="sxs-lookup"><span data-stu-id="02f94-131">Resolve</span></span>
- <span data-ttu-id="02f94-132">Yanlış pozitif olarak işaretleme</span><span class="sxs-lookup"><span data-stu-id="02f94-132">Mark as false positive</span></span>
- <span data-ttu-id="02f94-133">Yoksayma</span><span class="sxs-lookup"><span data-stu-id="02f94-133">Ignore</span></span>
- <span data-ttu-id="02f94-134">Yeniden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="02f94-134">Reactivate</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="02f94-136">Daha fazla ayrıntı için bkz. [Risk olaylarını elle kapatma](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="02f94-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="02f94-137">Bu rapor size şu seçeneği sağlar:</span><span class="sxs-lookup"><span data-stu-id="02f94-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="02f94-138">Kaynaklarda ara</span><span class="sxs-lookup"><span data-stu-id="02f94-138">Searh resources</span></span>
- <span data-ttu-id="02f94-139">Rapor verilerini indir</span><span class="sxs-lookup"><span data-stu-id="02f94-139">Download the report data</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="02f94-141">Azure Active Directory premium sürümleri</span><span class="sxs-lookup"><span data-stu-id="02f94-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="02f94-142">Azure Active Directory premium sürümlerindeki riskli oturum açma işlemleri raporu aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="02f94-142">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="02f94-143">Algılanan [risk olayı türleri](active-directory-identity-protection-risk-events.md) hakkında toplu bilgiler</span><span class="sxs-lookup"><span data-stu-id="02f94-143">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="02f94-144">Raporu indirme seçeneği</span><span class="sxs-lookup"><span data-stu-id="02f94-144">An option to download the report</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="02f94-146">Bir risk olayını seçtiğinizde bu risk olayına ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="02f94-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="02f94-147">Bir [kullanıcı riskini azaltma ilkesi](active-directory-identityprotection.md#user-risk-security-policy) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-147">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="02f94-148">Risk olayının algılanma zaman çizelgesini gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-148">Review the detection timeline for the risk event</span></span>  

- <span data-ttu-id="02f94-149">Bu risk olayının hangi kullanıcılarla ilgili olarak algılandığının listesini gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="02f94-150">[Risk olayını elle kapatabilir](active-directory-identityprotection.md#closing-risk-events-manually) ya da elle kapatılmış bir risk olayını yeniden etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="02f94-152">Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="02f94-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="02f94-153">Tüm oturum açma işlemleri görünümünü açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-153">Open the All sign-ins view</span></span>

- <span data-ttu-id="02f94-154">Kullanıcının parolasını sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-154">Reset the user's password</span></span>

- <span data-ttu-id="02f94-155">Tüm olayları kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-155">Dismiss all events</span></span>

- <span data-ttu-id="02f94-156">Kullanıcıya ilişkin bildirilmiş risk olaylarını araştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02f94-156">Investigate reported risk events for the user.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="02f94-158">Bir risk olayını araştırmak için, söz konusu olayı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="02f94-158">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="02f94-159">Bu risk olayına ilişkin **Ayrıntılar** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="02f94-159">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="02f94-160">**Ayrıntılar** dikey penceresinde, [risk olayını elle kapatma](active-directory-identityprotection.md#closing-risk-events-manually) ve elle kapatılmış risk olayını yeniden etkinleştirme seçenekleri sunulur.</span><span class="sxs-lookup"><span data-stu-id="02f94-160">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="02f94-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02f94-162">Next steps</span></span>

- <span data-ttu-id="02f94-163">Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="02f94-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

