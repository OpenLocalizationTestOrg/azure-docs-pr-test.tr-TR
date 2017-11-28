---
title: "aaaFind etkinlik raporları hello Azure portalı | Microsoft Docs"
description: "Nasıl toofind Azure Active Directory etkinliği hello Azure portalında raporları öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="eea3a-103">Etkinlik raporları hello Azure portal Bul</span><span class="sxs-lookup"><span data-stu-id="eea3a-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="eea3a-104">Azure portalında Azure Klasik portalı toohello hello taşıyorsanız, Azure Active Directory (Azure AD) etkinlik günlükleri yeni göz alın.</span><span class="sxs-lookup"><span data-stu-id="eea3a-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="eea3a-105">En son içinde [blog gönderisi](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), etkinlik günlükleri hello kaynak üzerinde çalıştığınız hello Azure portal hello bağlamında nasıl görebilirim açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eea3a-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="eea3a-106">Bu makalede, nasıl toofind hello hello Azure portalında Klasik Azure portalında kullanılan raporları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eea3a-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="eea3a-107">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="eea3a-107">What's new</span></span>

<span data-ttu-id="eea3a-108">Merhaba Klasik Azure portalı raporlarında kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="eea3a-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="eea3a-109">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-109">Security reports</span></span>
2.  <span data-ttu-id="eea3a-110">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-110">Activity reports</span></span>
3.  <span data-ttu-id="eea3a-111">Tümleşik uygulama raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="eea3a-112">Etkinlik ve tümleşik uygulama raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-112">Activity and integrated app reports</span></span>

<span data-ttu-id="eea3a-113">Bağlam tabanlı hello Azure portalı raporlama için varolan raporları tek bir görünümde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="eea3a-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="eea3a-114">Bir tek, temel alınan API hello veri toohello görünümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="eea3a-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="eea3a-115">Bu görünümü, üzerinde hello toosee **Azure Active Directory** dikey altında **etkinlik**seçin **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="eea3a-116">![Denetim günlükleri](./media/active-directory-reporting-migration/482.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="eea3a-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="eea3a-117">Raporlar aşağıdaki hello bu görünümde birleştirilir:</span><span class="sxs-lookup"><span data-stu-id="eea3a-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="eea3a-118">Denetim raporu</span><span class="sxs-lookup"><span data-stu-id="eea3a-118">Audit report</span></span>
-   <span data-ttu-id="eea3a-119">Parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-119">Password reset activity</span></span>
-   <span data-ttu-id="eea3a-120">Parola sıfırlama kaydı etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-120">Password reset registration activity</span></span>
-   <span data-ttu-id="eea3a-121">Self Servis Grup etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-121">Self-service groups activity</span></span>
-   <span data-ttu-id="eea3a-122">Office365 grup adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="eea3a-123">Hesap etkinlik sağlama</span><span class="sxs-lookup"><span data-stu-id="eea3a-123">Account provisioning activity</span></span>
-   <span data-ttu-id="eea3a-124">Parola rollover durumu</span><span class="sxs-lookup"><span data-stu-id="eea3a-124">Password rollover status</span></span>
-   <span data-ttu-id="eea3a-125">Hesap hazırlama hataları</span><span class="sxs-lookup"><span data-stu-id="eea3a-125">Account provisioning errors</span></span>


<span data-ttu-id="eea3a-126">Merhaba uygulama kullanım raporu geliştirilmiştir ve hello dahil **oturum açma işlemleri** görünümü.</span><span class="sxs-lookup"><span data-stu-id="eea3a-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="eea3a-127">Bu görünümü, üzerinde hello toosee **Azure Active Directory** dikey altında **etkinlik**seçin **oturum açma işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="eea3a-128">![Oturum açma işlemleri Görünüm](./media/active-directory-reporting-migration/483.png "oturum açma işlemleri görüntüleyin")</span><span class="sxs-lookup"><span data-stu-id="eea3a-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="eea3a-129">Merhaba **oturum açma işlemleri** görünümü, tüm kullanıcı oturum açma işlemleri içerir. Bu bilgileri tooget uygulama kullanım bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eea3a-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="eea3a-130">Hello uygulama kullanım bilgilerini de görüntüleyebilirsiniz **kurumsal uygulamalar** genel bakış, hello **Yönet** bölümü.</span><span class="sxs-lookup"><span data-stu-id="eea3a-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="eea3a-131">![Kuruluş uygulamaları](./media/active-directory-reporting-migration/484.png "kurumsal uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="eea3a-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="eea3a-132">Belirli bir rapor erişim</span><span class="sxs-lookup"><span data-stu-id="eea3a-132">Access a specific report</span></span>

<span data-ttu-id="eea3a-133">Tek bir görünüm Hello Azure portal sunmasına karşın özel raporları da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eea3a-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="eea3a-134">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-134">Audit logs</span></span>

<span data-ttu-id="eea3a-135">Yanıt toocustomer Geribildiriminizi hello Azure portal, Gelişmiş filtreleme tooaccess istediğiniz hello veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eea3a-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="eea3a-136">Kullanabileceğiniz bir filtredir bir *etkinlik kategorisi*, Azure AD'de oturum hangi hello farklı etkinlik türlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="eea3a-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="eea3a-137">Aradığınız toowhat toonarrow sonuçları, bir kategori seçin.</span><span class="sxs-lookup"><span data-stu-id="eea3a-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="eea3a-138">Örneğin, yalnızca etkinlikleri ilgili tooself hizmeti parolasını sıfırlar ilgileniyorsanız hello seçebilirsiniz **Self Servis parola yönetimi** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="eea3a-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="eea3a-139">gördüğünüz hello kategorileri çalıştığınız hello kaynak dayanır.</span><span class="sxs-lookup"><span data-stu-id="eea3a-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="eea3a-140">![Merhaba filtre denetim günlüklerini sayfasındaki Kategori seçenekleri](./media/active-directory-reporting-migration/06.png "hello filtre denetim günlüklerini sayfasındaki Kategori seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="eea3a-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="eea3a-141">Etkinlik kategorileri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eea3a-141">Activity categories include:</span></span>

- <span data-ttu-id="eea3a-142">Çekirdek Dizin</span><span class="sxs-lookup"><span data-stu-id="eea3a-142">Core Directory</span></span>
- <span data-ttu-id="eea3a-143">Self Servis Parola Yönetimi</span><span class="sxs-lookup"><span data-stu-id="eea3a-143">Self-service Password Management</span></span>
- <span data-ttu-id="eea3a-144">Self Servis Grup Yönetimi</span><span class="sxs-lookup"><span data-stu-id="eea3a-144">Self-service Group Management</span></span>
- <span data-ttu-id="eea3a-145">Hesap Sağlama</span><span class="sxs-lookup"><span data-stu-id="eea3a-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="eea3a-146">Uygulama kullanımı</span><span class="sxs-lookup"><span data-stu-id="eea3a-146">Application usage</span></span>

<span data-ttu-id="eea3a-147">tooview hakkında ayrıntılı uygulama kullanım veya tek bir uygulamayı tüm uygulamalar için altında **etkinlik**seçin **oturum açma işlemleri**. toonarrow hello sonuçları, kullanıcı adı veya uygulama adı filtreleyebilir.</span><span class="sxs-lookup"><span data-stu-id="eea3a-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="eea3a-148">![Filtre oturum açma olayları sayfası](./media/active-directory-reporting-migration/07.png "filtre oturum açma olayları sayfası")</span><span class="sxs-lookup"><span data-stu-id="eea3a-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="eea3a-149">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="eea3a-150">Azure AD anormal etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="eea3a-151">Azure AD anormal bir etkinliğin güvenlik hello Klasik Azure portalı raporlardan birleştirilmiş tooprovide olmuştur, bir merkezi görünümü.</span><span class="sxs-lookup"><span data-stu-id="eea3a-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="eea3a-152">Bu görünüm, Azure AD algılamak ve raporlama tüm risk güvenlikle ilgili olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="eea3a-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="eea3a-153">Aşağıdaki tablonun hello hello Azure AD anormal bir etkinliğin güvenlik raporları ve hello Azure portalında karşılık gelen risk olay türlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="eea3a-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="eea3a-154">Azure AD anormal Etkinlik Raporu</span><span class="sxs-lookup"><span data-stu-id="eea3a-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="eea3a-155">Kimlik koruması risk olay türü</span><span class="sxs-lookup"><span data-stu-id="eea3a-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="eea3a-156">Sızan kimlik bilgilerine sahip kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="eea3a-156">Users with leaked credentials</span></span> | <span data-ttu-id="eea3a-157">Sızan kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="eea3a-157">Leaked credentials</span></span> |
| <span data-ttu-id="eea3a-158">Düzensiz oturum açma etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-158">Irregular sign-in activity</span></span> | <span data-ttu-id="eea3a-159">Mümkün olmayan seyahat tooatypical konumları</span><span class="sxs-lookup"><span data-stu-id="eea3a-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="eea3a-160">Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="eea3a-161">Virüs bulaşmış cihazlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="eea3a-162">Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="eea3a-163">Anonim IP adreslerinden oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="eea3a-164">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="eea3a-165">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="eea3a-166">Alışılmadık konumlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="eea3a-167">Azure AD anormal bir etkinliğin güvenlik aşağıdaki hello raporları olmayan hello Azure portal risk olayları eklendi:</span><span class="sxs-lookup"><span data-stu-id="eea3a-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="eea3a-168">Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="eea3a-169">Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="eea3a-170">Bu raporlar hello Klasik Azure portalı hala kullanılabildiği ancak bunların bazı zaman hello gelecekteki kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="eea3a-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="eea3a-171">Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="eea3a-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="eea3a-172">Algılanan risk olayı</span><span class="sxs-lookup"><span data-stu-id="eea3a-172">Detected risk events</span></span>

<span data-ttu-id="eea3a-173">Hello Azure portal, hello algılanan risk olayı hakkında raporlarına erişebilir **Azure Active Directory** dikey altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="eea3a-174">Algılanan risk olayı raporları aşağıdaki hello izlenir:</span><span class="sxs-lookup"><span data-stu-id="eea3a-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="eea3a-175">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="eea3a-175">Users at Risk</span></span>
- <span data-ttu-id="eea3a-176">Riskli Oturum Açma İşlemleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-176">Risky Sign-ins</span></span>

<span data-ttu-id="eea3a-177">![Güvenlik raporları](./media/active-directory-reporting-migration/04.png "güvenlik raporları")</span><span class="sxs-lookup"><span data-stu-id="eea3a-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="eea3a-178">Güvenlik raporları hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="eea3a-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="eea3a-179">Risk güvenlik raporu hello Azure Active Directory portalında kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="eea3a-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="eea3a-180">Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="eea3a-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="eea3a-181">Merhaba hello Azure portalı ve Azure Klasik portalı etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="eea3a-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="eea3a-182">Bu bölümdeki Hello tablo hello Klasik Azure portalı içinde varolan raporları listeler.</span><span class="sxs-lookup"><span data-stu-id="eea3a-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="eea3a-183">Ayrıca nasıl erişebileceğini açıklanır hello hello Azure portalı, aynı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="eea3a-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="eea3a-184">tooview tüm veri hello denetim **Azure Active Directory** dikey altında **etkinlik**, çok Git**denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="eea3a-185">![Denetim günlükleri](./media/active-directory-reporting-migration/61.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="eea3a-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="eea3a-186">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="eea3a-186">Azure classic portal</span></span>                 | <span data-ttu-id="eea3a-187">hello Azure portal toofind</span><span class="sxs-lookup"><span data-stu-id="eea3a-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="eea3a-188">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="eea3a-188">Audit logs</span></span>                           | <span data-ttu-id="eea3a-189">İçin **etkinlik kategorisi**seçin **çekirdek dizin**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="eea3a-190">Parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-190">Password reset activity</span></span>              | <span data-ttu-id="eea3a-191">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="eea3a-192">Parola sıfırlama kaydı etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-192">Password reset registration activity</span></span> | <span data-ttu-id="eea3a-193">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="eea3a-194">Self Servis Grup etkinliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-194">Self-service groups activity</span></span>         | <span data-ttu-id="eea3a-195">İçin **etkinlik kategorisi**seçin **Self Servis Grup Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="eea3a-196">Hesap etkinlik sağlama</span><span class="sxs-lookup"><span data-stu-id="eea3a-196">Account provisioning activity</span></span>        | <span data-ttu-id="eea3a-197">İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="eea3a-198">Parola rollover durumu</span><span class="sxs-lookup"><span data-stu-id="eea3a-198">Password rollover status</span></span>             | <span data-ttu-id="eea3a-199">İçin **etkinlik kategorisi**seçin **otomatik uygulama parolası Rollover**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="eea3a-200">Hesap hazırlama hataları</span><span class="sxs-lookup"><span data-stu-id="eea3a-200">Account provisioning errors</span></span>          | <span data-ttu-id="eea3a-201">İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="eea3a-202">Office365 grup adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="eea3a-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="eea3a-203">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="eea3a-204">İçin **etkinlik kaynak türü**seçin **grup**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="eea3a-205">İçin **etkinlik kaynağı**seçin **O365 grupları**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="eea3a-206">tooview hello **uygulama kullanımı** raporda hello **Azure Active Directory** dikey altında **Yönet**seçin **kurumsal uygulamalar**ve ardından **oturum açma işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="eea3a-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="eea3a-207">![Kuruluş uygulamaları oturum açma işlemleri raporu](./media/active-directory-reporting-migration/199.png "Kurumsal uygulamaları oturum açma işlemleri raporu")</span><span class="sxs-lookup"><span data-stu-id="eea3a-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="eea3a-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eea3a-208">Next steps</span></span>

<span data-ttu-id="eea3a-209">Merhaba raporlama genel bakış için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eea3a-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
