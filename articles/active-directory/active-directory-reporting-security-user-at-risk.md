---
title: "aaaUsers bayrağı risk güvenlik raporu hello Azure Active Directory portalında için | Microsoft Docs"
description: "Risk güvenlik raporu hello Azure Active Directory portalında için işaretlenen hello kullanıcılar hakkında bilgi edinin"
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
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="6bd41-103">Risk güvenlik raporu hello Azure Active Directory portalında için bayrak eklenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="6bd41-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="6bd41-104">Hello Azure Active Directory (Azure AD) içinde Hello güvenlik raporları ile ortamınızda ele geçirilen kullanıcı hesapları hello olasılığını Öngörüler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd41-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="6bd41-105">Azure Active Directory, ilgili tooyour kullanıcı hesapları olan şüpheli eylemleri algılar.</span><span class="sxs-lookup"><span data-stu-id="6bd41-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="6bd41-106">Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6bd41-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="6bd41-107">Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="6bd41-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="6bd41-108">Merhaba risk olaylarını kullanılan toocalculate algıladı:</span><span class="sxs-lookup"><span data-stu-id="6bd41-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="6bd41-109">**Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="6bd41-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="6bd41-110">Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="6bd41-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="6bd41-111">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="6bd41-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="6bd41-112">Daha fazla bilgi için bkz. [Risk için işaretlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="6bd41-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="6bd41-113">Hello Azure portal, hello güvenlik raporları hello üzerinde bulabilirsiniz **Azure Active Directory** dikey penceresinde hello **güvenlik** bölümü.</span><span class="sxs-lookup"><span data-stu-id="6bd41-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="6bd41-115">Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="6bd41-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="6bd41-116">Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve risk raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6bd41-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="6bd41-117">Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="6bd41-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="6bd41-118">Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten risk bayrak eklenen kullanıcılar listesini alın.</span><span class="sxs-lookup"><span data-stu-id="6bd41-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="6bd41-119">Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="6bd41-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="6bd41-120">Merhaba **Azure Active Directory Premium 2** edition ile sağlar hello tüm temel alınan risk olaylar hakkında en ayrıntılı bilgi ve otomatik olarak tooconfigured risk yanıt tooconfigure güvenlik ilkeleri sağlar düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="6bd41-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="6bd41-121">Azure Active Directory ücretsiz ve temel sürümleri</span><span class="sxs-lookup"><span data-stu-id="6bd41-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="6bd41-122">risk raporda hello Azure Active Directory ücretsiz ve temel sürümleri için işaretlenen hello kullanıcılar tehlikede olduğunu kullanıcı hesaplarının bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bd41-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="6bd41-124">Bir kullanıcı seçilmesi hello ilgili kullanıcı veri dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="6bd41-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="6bd41-125">Risk altında olan kullanıcı için hello kullanıcının oturum açma geçmişini gözden geçirin ve gerekirse hello parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="6bd41-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="6bd41-127">Bu iletişim kutusu size şu seçeneği sunar:</span><span class="sxs-lookup"><span data-stu-id="6bd41-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="6bd41-128">Merhaba raporu yükleyin</span><span class="sxs-lookup"><span data-stu-id="6bd41-128">Download hello report</span></span>

- <span data-ttu-id="6bd41-129">Kullanıcılarda arama</span><span class="sxs-lookup"><span data-stu-id="6bd41-129">Search users</span></span>

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="6bd41-131">Azure Active Directory premium sürümleri</span><span class="sxs-lookup"><span data-stu-id="6bd41-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="6bd41-132">risk rapor hello Azure Active Directory premium sürümlerinde için işaretlenen hello kullanıcılar ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="6bd41-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="6bd41-133">Tehlikeye girmiş olabilecek [kullanıcı hesaplarının listesi](active-directory-identityprotection.md#users-flagged-for-risk)</span><span class="sxs-lookup"><span data-stu-id="6bd41-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="6bd41-134">Merhaba hakkında bilgiler birleştirilir [risk olayı türleri](active-directory-identity-protection-risk-events.md) , algılandı</span><span class="sxs-lookup"><span data-stu-id="6bd41-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="6bd41-135">Bir seçenek toodownload hello raporu</span><span class="sxs-lookup"><span data-stu-id="6bd41-135">An option toodownload hello report</span></span>

- <span data-ttu-id="6bd41-136">Bir seçenek tooconfigure bir [kullanıcı risk düzeltme İlkesi](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="6bd41-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="6bd41-138">Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="6bd41-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="6bd41-139">Tüm oturum açma işlemleri görüntülemek hello açın</span><span class="sxs-lookup"><span data-stu-id="6bd41-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="6bd41-140">Merhaba kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="6bd41-140">Reset hello user's password</span></span>

- <span data-ttu-id="6bd41-141">Tüm olayları kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd41-141">Dismiss all events</span></span>

- <span data-ttu-id="6bd41-142">Merhaba kullanıcı için bildirilen risk olaylarını araştırın.</span><span class="sxs-lookup"><span data-stu-id="6bd41-142">Investigate reported risk events for hello user.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="6bd41-144">tooinvestigate bir risk olayı seçin hello listesi tooopen hello birinden **ayrıntıları** dikey penceresinde bu risk olay.</span><span class="sxs-lookup"><span data-stu-id="6bd41-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="6bd41-145">Merhaba üzerinde **ayrıntıları** dikey penceresinde hello seçeneği tooeither sahip [el ile bir risk olayı kapatmak](active-directory-identityprotection.md#closing-risk-events-manually) veya el ile kapatılmış risk olayı yeniden etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="6bd41-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="6bd41-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bd41-147">Next steps</span></span>

- <span data-ttu-id="6bd41-148">Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="6bd41-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

