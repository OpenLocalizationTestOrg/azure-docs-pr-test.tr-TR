---
title: Azure Active Directory raporlama | Microsoft Docs
description: "Azure Active Directory raporlamasına genel bir bakış sağlar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="03145-103">Azure Active Directory raporlama</span><span class="sxs-lookup"><span data-stu-id="03145-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="03145-104">Azure Active Directory raporlamasıyla, ortamınızın nasıl çalıştığıyla ilgili fikir edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="03145-105">Sağlanan verilerle:</span><span class="sxs-lookup"><span data-stu-id="03145-105">The provided data enables you to:</span></span>

- <span data-ttu-id="03145-106">Uygulama ve hizmetlerinizin kullanıcılarınız tarafından nasıl kullanıldığını saptayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="03145-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="03145-107">Ortamınızın durumunu etkileyebilecek olası riskleri algılayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="03145-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="03145-108">Kullanıcılarınızın işlerini yapmalarını engelleyen sorunları giderebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="03145-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="03145-109">Raporlama mimarisinin iki ana dayanağı vardır:</span><span class="sxs-lookup"><span data-stu-id="03145-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="03145-110">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="03145-110">Security reports</span></span>
- <span data-ttu-id="03145-111">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="03145-111">Activity reports</span></span>

![Raporlama](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="03145-113">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="03145-113">Security reports</span></span>

<span data-ttu-id="03145-114">Azure Active Directory'deki güvenlik raporları kuruluşunuzun kimliklerini korumanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="03145-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="03145-115">Azure Active Directory'de iki tür güvenlik raporu vardır:</span><span class="sxs-lookup"><span data-stu-id="03145-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="03145-116">**Riskli oldukları belirlenen kullanıcılar** - [Riskli oldukları belirlenen kullanıcılar güvenlik raporundan](active-directory-reporting-security-user-at-risk.md), gizliliği bozulmuş olabilecek kullanıcı hesaplarına genel bir bakış elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="03145-117">**Riskli oturum açma işlemleri** - [Riskli oturum açma işlemleri güvenlik raporuyla](active-directory-reporting-security-risky-sign-ins.md), kullanıcı hesabının meşru sahibi olmayan biri tarafından gerçekleştirilmiş olabilecek oturum açma işlemleriyle ilgili göstergeler elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="03145-118">**Güvenlik raporuna erişebilmek için hangi Azure AD lisansınızın olması gerekir?**</span><span class="sxs-lookup"><span data-stu-id="03145-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="03145-119">Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve riskli oturum açma işlemleri raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03145-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="03145-120">Bununla birlikte, rapordaki ayrıntı düzeyi sürümler arasında değişiklik gösterir:</span><span class="sxs-lookup"><span data-stu-id="03145-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="03145-121">**Azure Active Directory Ücretsiz ve Temel sürümlerinde**, riskli olduğu belirlenen kullanıcıların ve riskli oturum açma işlemlerinin listesini zaten alırsınız.</span><span class="sxs-lookup"><span data-stu-id="03145-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="03145-122">**Azure Active Directory Premium 1** sürümü bu modeli genişleterek her raporda algılanmış olan temel risk olaylarından bazılarını incelemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="03145-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="03145-123">**Azure Active Directory Premium 2** sürümü temel risk olayları hakkında en ayrıntılı bilgileri sağlar ve ayrıca, yapılandırılmış risk düzeylerine otomatik olarak yanıt veren güvenlik ilkeleri yapılandırmanıza da olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="03145-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="03145-124">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="03145-124">Activity reports</span></span>

<span data-ttu-id="03145-125">Azure Active Directory'de iki tür etkinlik raporu vardır:</span><span class="sxs-lookup"><span data-stu-id="03145-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="03145-126">**Denetim günlükleri** - [Denetim günlükleri etkinlik raporu](active-directory-reporting-activity-audit-logs.md), kiracınızda gerçekleştirilen her görevin geçmişine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="03145-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="03145-127">**Oturum açma işlemleri** - [Oturum açma işlemleri etkinlik raporuyla](active-directory-reporting-activity-sign-ins.md), denetim günlükleri raporunda bildirilen görevleri kimlerin gerçekleştirdiğini saptayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="03145-128">**Denetim günlükleri raporu** uyumluluk amacıyla sistem etkinliklerinin kayıtlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="03145-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="03145-129">Sağlanan verilerin yararları arasında şu yaygın senaryolara çözüm getirmenize olanak tanımaları da sayılabilir:</span><span class="sxs-lookup"><span data-stu-id="03145-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="03145-130">Kiracımda birisi yönetici grubuna erişim aldı.</span><span class="sxs-lookup"><span data-stu-id="03145-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="03145-131">Ona kim erişim verdi?</span><span class="sxs-lookup"><span data-stu-id="03145-131">Who gave them access?</span></span> 

- <span data-ttu-id="03145-132">Belirli bir uygulamayı yeni ekledim ve iyi çalışıp çalışmadığını bilmek istiyorum; bu nedenle uygulamada oturum açan kullanıcıların listesini öğrenmek istiyorum</span><span class="sxs-lookup"><span data-stu-id="03145-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="03145-133">Kiracımda kaç parola sıfırlama işlemi yapıldığını bilmek istiyorum</span><span class="sxs-lookup"><span data-stu-id="03145-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="03145-134">**Denetim günlükleri raporuna erişebilmek için hangi Azure AD lisansınızın olması gerekir?**</span><span class="sxs-lookup"><span data-stu-id="03145-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="03145-135">Denetim günlükleri raporu, lisansınız olan özellikler için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03145-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="03145-136">Belirli bir özelliğin lisansına sahipseniz, o özelliğin denetim günlüğü bilgilerine de erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="03145-137">Diğer ayrıntılar için, [Azure Active Directory özellikleri ve becerileri](https://www.microsoft.com/cloud-platform/azure-active-directory-features) altında **Ücretsiz, Temel ve Premium sürümlerinin genel olarak sağlanan özelliklerini karşılaştırma** konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="03145-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="03145-138">**Oturum açma işlemleri etkinlik raporu**, şöyle soruların yanıtlarını bulmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="03145-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="03145-139">Belirli bir kullanıcının oturum açma düzeni nedir?</span><span class="sxs-lookup"><span data-stu-id="03145-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="03145-140">Bir hafta içerisinde kaç adet kullanıcı oturum açtı?</span><span class="sxs-lookup"><span data-stu-id="03145-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="03145-141">Bu açılan oturumların durumu nedir?</span><span class="sxs-lookup"><span data-stu-id="03145-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="03145-142">**Oturum açma işlemleri etkinlik raporuna erişebilmek için hangi Azure AD lisansınızın olması gerekir?**</span><span class="sxs-lookup"><span data-stu-id="03145-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="03145-143">Oturum açma işlemleri etkinlik raporuna erişebilmek için, kiracınızın ilişkili bir Azure AD Premium lisansı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03145-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="03145-144">Programlı erişim</span><span class="sxs-lookup"><span data-stu-id="03145-144">Programmatic access</span></span>

<span data-ttu-id="03145-145">Kullanıcı arabirimine ek olarak, Azure Active Directory raporlaması [programlı erişim](active-directory-reporting-api-getting-started-azure-portal.md) yoluyla da raporlama verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="03145-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="03145-146">Bu raporların verileri SIEM sistemleri, denetim ve iş zekası araçları gibi uygulamalarınız için çok yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="03145-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="03145-147">Azure AD raporlama API'leri, bir dizi REST tabanlı API aracılığıyla verilere programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="03145-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="03145-148">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03145-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="03145-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03145-149">Next steps</span></span>

<span data-ttu-id="03145-150">Azure Active Directory'deki çeşitli rapor türleri hakkında daha fazla bilgi edinmek istiyorsanız, bkz.:</span><span class="sxs-lookup"><span data-stu-id="03145-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="03145-151">Riskli olarak işaretlenen kullanıcılar raporu</span><span class="sxs-lookup"><span data-stu-id="03145-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="03145-152">Riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="03145-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="03145-153">Denetim günlükleri raporu</span><span class="sxs-lookup"><span data-stu-id="03145-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="03145-154">Oturum açma günlükleri raporu</span><span class="sxs-lookup"><span data-stu-id="03145-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="03145-155">Raporlama API'sini kullanarak raporlama verilerine erişim hakkında daha fazla bilgi edinmek istiyorsanız, bkz:</span><span class="sxs-lookup"><span data-stu-id="03145-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="03145-156">Azure Active Directory raporlama API’siyle çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="03145-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png