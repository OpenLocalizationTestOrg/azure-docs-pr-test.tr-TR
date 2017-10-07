---
title: "aaaRisky oturum açma işlemleri raporu hello Azure Active Directory portalında | Microsoft Docs"
description: "Merhaba riskli oturum açma işlemleri raporu hello Azure Active Directory portalında hakkında bilgi edinin"
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
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="9a13d-103">Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="9a13d-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="9a13d-104">Merhaba güvenlik raporları Azure Active Directory'de (Azure AD) ile ortamınızda ele geçirilen kullanıcı hesapları hello olasılığını Öngörüler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a13d-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="9a13d-105">Azure AD, ilgili tooyour kullanıcı hesapları olan şüpheli eylemleri algılar.</span><span class="sxs-lookup"><span data-stu-id="9a13d-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="9a13d-106">Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a13d-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="9a13d-107">Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="9a13d-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="9a13d-108">Merhaba risk olaylarını kullanılan toocalculate algıladı:</span><span class="sxs-lookup"><span data-stu-id="9a13d-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="9a13d-109">**Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="9a13d-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="9a13d-110">Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="9a13d-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="9a13d-111">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="9a13d-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="9a13d-112">Daha fazla bilgi için bkz. [Riskli oldukları belirlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="9a13d-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="9a13d-113">İçinde [Azure portal hello](https://portal.azure.com), hello güvenlik raporları hello üzerinde bulabilirsiniz **Azure Active Directory** dikey penceresinde hello **güvenlik** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9a13d-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="9a13d-115">Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="9a13d-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="9a13d-116">Azure Active Directory'nin tüm sürümlerinde size riskli oturum açma işlemleri raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="9a13d-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="9a13d-117">Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="9a13d-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="9a13d-118">Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten riskli oturum açma işlemleri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="9a13d-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="9a13d-119">Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="9a13d-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="9a13d-120">Merhaba **Azure Active Directory Premium 2** edition, ayrıca, otomatik olarak tooconfigured yanıt tooconfigure güvenlik ilkeleri sağlar ve tüm temel alınan risk olaylar hakkında bilgi en ayrıntılı hello ile sağlar risk düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="9a13d-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="9a13d-121">Azure Active Directory ücretsiz ve temel sürümleri</span><span class="sxs-lookup"><span data-stu-id="9a13d-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="9a13d-122">Hello Azure Active Directory ücretsiz ve basic sürümleri, kullanıcılarınız için riskli oturum açma, algılanmış olan işlemleri, bir listesi sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a13d-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="9a13d-123">Bu raporda şunlar listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="9a13d-123">This report lists:</span></span>

- <span data-ttu-id="9a13d-124">**Kullanıcı** - hello hello oturum açma işlemi sırasında kullanılan hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9a13d-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="9a13d-125">**IP** -hello kullanılan tooconnect tooAzure Active Directory olduğu hello aygıtın IP adresi</span><span class="sxs-lookup"><span data-stu-id="9a13d-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="9a13d-126">**Konum** -başlangıç konumu kullanılan tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a13d-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="9a13d-127">**Oturum açma saatini** -hello zaman zaman hello oturum açma gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="9a13d-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="9a13d-128">**Durum** -hello hello oturum açma durumu</span><span class="sxs-lookup"><span data-stu-id="9a13d-128">**Status** - hello status of hello sign-in</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="9a13d-130">Araştırmanızı hello riskli oturum açma, bağlı olarak, geri bildirim tooAzure biçiminde hello eylemleri aşağıdaki Active Directory sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a13d-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="9a13d-131">Çözümleme</span><span class="sxs-lookup"><span data-stu-id="9a13d-131">Resolve</span></span>
- <span data-ttu-id="9a13d-132">Yanlış pozitif olarak işaretleme</span><span class="sxs-lookup"><span data-stu-id="9a13d-132">Mark as false positive</span></span>
- <span data-ttu-id="9a13d-133">Yoksayma</span><span class="sxs-lookup"><span data-stu-id="9a13d-133">Ignore</span></span>
- <span data-ttu-id="9a13d-134">Yeniden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9a13d-134">Reactivate</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="9a13d-136">Daha fazla ayrıntı için bkz. [Risk olaylarını elle kapatma](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="9a13d-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="9a13d-137">Bu rapor size şu seçeneği sağlar:</span><span class="sxs-lookup"><span data-stu-id="9a13d-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="9a13d-138">Kaynaklarda ara</span><span class="sxs-lookup"><span data-stu-id="9a13d-138">Searh resources</span></span>
- <span data-ttu-id="9a13d-139">Merhaba rapor verilerini indirme</span><span class="sxs-lookup"><span data-stu-id="9a13d-139">Download hello report data</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="9a13d-141">Azure Active Directory premium sürümleri</span><span class="sxs-lookup"><span data-stu-id="9a13d-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="9a13d-142">Merhaba riskli oturum açma işlemleri raporu hello Azure Active Directory premium sürümlerinde ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="9a13d-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="9a13d-143">Merhaba hakkında bilgiler birleştirilir [risk olayı türleri](active-directory-identity-protection-risk-events.md) , algılandı</span><span class="sxs-lookup"><span data-stu-id="9a13d-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="9a13d-144">Bir seçenek toodownload hello raporu</span><span class="sxs-lookup"><span data-stu-id="9a13d-144">An option toodownload hello report</span></span>


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="9a13d-146">Bir risk olayını seçtiğinizde bu risk olayına ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="9a13d-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="9a13d-147">Bir seçenek tooconfigure bir [kullanıcı risk düzeltme İlkesi](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="9a13d-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="9a13d-148">Gözden geçirme hello algılama hello risk olayı için zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="9a13d-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="9a13d-149">Bu risk olayının hangi kullanıcılarla ilgili olarak algılandığının listesini gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a13d-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="9a13d-150">[Risk olayını elle kapatabilir](active-directory-identityprotection.md#closing-risk-events-manually) ya da elle kapatılmış bir risk olayını yeniden etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a13d-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="9a13d-152">Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="9a13d-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="9a13d-153">Tüm oturum açma işlemleri görüntülemek hello açın</span><span class="sxs-lookup"><span data-stu-id="9a13d-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="9a13d-154">Merhaba kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="9a13d-154">Reset hello user's password</span></span>

- <span data-ttu-id="9a13d-155">Tüm olayları kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a13d-155">Dismiss all events</span></span>

- <span data-ttu-id="9a13d-156">Merhaba kullanıcı için bildirilen risk olaylarını araştırın.</span><span class="sxs-lookup"><span data-stu-id="9a13d-156">Investigate reported risk events for hello user.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="9a13d-158">tooinvestigate bir risk olayı hello listeden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="9a13d-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="9a13d-159">Merhaba açılır **ayrıntıları** dikey penceresinde bu risk olay.</span><span class="sxs-lookup"><span data-stu-id="9a13d-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="9a13d-160">Merhaba üzerinde **ayrıntıları** dikey penceresinde hello seçeneği tooeither sahip [el ile bir risk olayı kapatmak](active-directory-identityprotection.md#closing-risk-events-manually) veya el ile kapatılmış risk olayı yeniden etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="9a13d-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="9a13d-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a13d-162">Next steps</span></span>

- <span data-ttu-id="9a13d-163">Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="9a13d-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

