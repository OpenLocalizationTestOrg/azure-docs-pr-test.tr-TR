---
title: "Azure portalında etkinlik raporları bulmak | Microsoft Docs"
description: "Azure portalında Azure Active Directory etkinlik raporları bulmayı öğrenin."
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
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="21e12-103">Azure portalında etkinlik raporları Bul</span><span class="sxs-lookup"><span data-stu-id="21e12-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="21e12-104">Azure portalında Klasik Azure portalından taşıyorsanız, Azure Active Directory (Azure AD) etkinlik günlükleri yeni göz alın.</span><span class="sxs-lookup"><span data-stu-id="21e12-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="21e12-105">En son içinde [blog gönderisi](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), etkinlik günlükleri üzerinde çalıştığınız Azure portalında kaynak bağlamında nasıl görebilirim açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="21e12-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="21e12-106">Bu makalede, Azure portalında Klasik Azure Portalı'nda kullandığınız raporları bulmak nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="21e12-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="21e12-107">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="21e12-107">What's new</span></span>

<span data-ttu-id="21e12-108">Azure Klasik portalında raporları kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="21e12-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="21e12-109">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-109">Security reports</span></span>
2.  <span data-ttu-id="21e12-110">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-110">Activity reports</span></span>
3.  <span data-ttu-id="21e12-111">Tümleşik uygulama raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="21e12-112">Etkinlik ve tümleşik uygulama raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-112">Activity and integrated app reports</span></span>

<span data-ttu-id="21e12-113">Azure portalında raporlama Bağlam tabanlı için varolan raporları tek bir görünümde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="21e12-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="21e12-114">Tek bir API temel alınan veri görünümüne sağlar.</span><span class="sxs-lookup"><span data-stu-id="21e12-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="21e12-115">Bu görünüm görmek için **Azure Active Directory** dikey altında **etkinlik**seçin **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="21e12-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="21e12-116">![Denetim günlükleri](./media/active-directory-reporting-migration/482.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="21e12-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="21e12-117">Aşağıdaki raporlar bu görünümde birleştirilir:</span><span class="sxs-lookup"><span data-stu-id="21e12-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="21e12-118">Denetim raporu</span><span class="sxs-lookup"><span data-stu-id="21e12-118">Audit report</span></span>
-   <span data-ttu-id="21e12-119">Parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-119">Password reset activity</span></span>
-   <span data-ttu-id="21e12-120">Parola sıfırlama kaydı etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-120">Password reset registration activity</span></span>
-   <span data-ttu-id="21e12-121">Self Servis Grup etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-121">Self-service groups activity</span></span>
-   <span data-ttu-id="21e12-122">Office365 grup adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="21e12-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="21e12-123">Hesap etkinlik sağlama</span><span class="sxs-lookup"><span data-stu-id="21e12-123">Account provisioning activity</span></span>
-   <span data-ttu-id="21e12-124">Parola rollover durumu</span><span class="sxs-lookup"><span data-stu-id="21e12-124">Password rollover status</span></span>
-   <span data-ttu-id="21e12-125">Hesap hazırlama hataları</span><span class="sxs-lookup"><span data-stu-id="21e12-125">Account provisioning errors</span></span>


<span data-ttu-id="21e12-126">Uygulama kullanım raporu geliştirilmiştir ve dahil **oturum açma işlemleri** görünümü.</span><span class="sxs-lookup"><span data-stu-id="21e12-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="21e12-127">Bu görünüm görmek için **Azure Active Directory** dikey altında **etkinlik**seçin **oturum açma işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="21e12-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="21e12-128">![Oturum açma işlemleri Görünüm](./media/active-directory-reporting-migration/483.png "oturum açma işlemleri görüntüleyin")</span><span class="sxs-lookup"><span data-stu-id="21e12-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="21e12-129">**Oturum açma işlemleri** görünümü, tüm kullanıcı oturum açma işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="21e12-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="21e12-130">Uygulama kullanım bilgilerini almak için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e12-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="21e12-131">Uygulama kullanım bilgilerini görüntülemek **kurumsal uygulamalar** genel bakış, **Yönet** bölümü.</span><span class="sxs-lookup"><span data-stu-id="21e12-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="21e12-132">![Kuruluş uygulamaları](./media/active-directory-reporting-migration/484.png "kurumsal uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="21e12-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="21e12-133">Belirli bir rapor erişim</span><span class="sxs-lookup"><span data-stu-id="21e12-133">Access a specific report</span></span>

<span data-ttu-id="21e12-134">Azure portalı tek bir görünüm sunmasına karşın özel raporları de bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21e12-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="21e12-135">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="21e12-135">Audit logs</span></span>

<span data-ttu-id="21e12-136">Azure portalında müşteri geri bildirimine yanıt Gelişmiş filtreleme istediğiniz verilere erişmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21e12-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="21e12-137">Kullanabileceğiniz bir filtredir bir *etkinlik kategorisi*, Azure AD'de oturum hangi etkinlik farklı türlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="21e12-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="21e12-138">Aradığınız ne için sonuçları daraltmak için bir kategori seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21e12-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="21e12-139">Örneğin, yalnızca Self Servis parola sıfırlama için ilgili etkinlikleri de ilgileniyorsanız, seçebileceğiniz **Self Servis parola yönetimi** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="21e12-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="21e12-140">Gördüğünüz kategorileri çalıştığınız kaynak dayanır.</span><span class="sxs-lookup"><span data-stu-id="21e12-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="21e12-141">![Filtre denetim günlüklerini sayfasındaki Kategori seçenekleri](./media/active-directory-reporting-migration/06.png "filtre denetim günlüklerini sayfasındaki Kategori seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="21e12-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="21e12-142">Etkinlik kategorileri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="21e12-142">Activity categories include:</span></span>

- <span data-ttu-id="21e12-143">Çekirdek Dizin</span><span class="sxs-lookup"><span data-stu-id="21e12-143">Core Directory</span></span>
- <span data-ttu-id="21e12-144">Self Servis Parola Yönetimi</span><span class="sxs-lookup"><span data-stu-id="21e12-144">Self-service Password Management</span></span>
- <span data-ttu-id="21e12-145">Self Servis Grup Yönetimi</span><span class="sxs-lookup"><span data-stu-id="21e12-145">Self-service Group Management</span></span>
- <span data-ttu-id="21e12-146">Hesap Sağlama</span><span class="sxs-lookup"><span data-stu-id="21e12-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="21e12-147">Uygulama kullanımı</span><span class="sxs-lookup"><span data-stu-id="21e12-147">Application usage</span></span>

<span data-ttu-id="21e12-148">Altında tek bir uygulamayı veya tüm uygulamalar için uygulama kullanımı hakkındaki ayrıntıları görüntülemek için **etkinlik**seçin **oturum açma işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="21e12-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="21e12-149">Sonuçları daraltmak için kullanıcı adı veya uygulama adı filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21e12-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="21e12-150">![Filtre oturum açma olayları sayfası](./media/active-directory-reporting-migration/07.png "filtre oturum açma olayları sayfası")</span><span class="sxs-lookup"><span data-stu-id="21e12-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="21e12-151">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="21e12-152">Azure AD anormal etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="21e12-153">Azure AD anormal bir etkinliğin güvenlik raporları Azure Klasik portalından birleştirilmiş bir merkezi görünümünü sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="21e12-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="21e12-154">Bu görünüm, Azure AD algılamak ve raporlama tüm risk güvenlikle ilgili olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="21e12-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="21e12-155">Aşağıdaki tablo listeleri Azure AD anormal bir etkinliğin güvenlik raporları ve Azure portalında karşılık gelen risk olayı türleri.</span><span class="sxs-lookup"><span data-stu-id="21e12-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="21e12-156">Azure AD anormal Etkinlik Raporu</span><span class="sxs-lookup"><span data-stu-id="21e12-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="21e12-157">Kimlik koruması risk olay türü</span><span class="sxs-lookup"><span data-stu-id="21e12-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="21e12-158">Sızan kimlik bilgilerine sahip kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="21e12-158">Users with leaked credentials</span></span> | <span data-ttu-id="21e12-159">Sızan kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="21e12-159">Leaked credentials</span></span> |
| <span data-ttu-id="21e12-160">Düzensiz oturum açma etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-160">Irregular sign-in activity</span></span> | <span data-ttu-id="21e12-161">Alışılmadık konumlara imkansız seyahat</span><span class="sxs-lookup"><span data-stu-id="21e12-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="21e12-162">Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="21e12-163">Virüs bulaşmış cihazlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="21e12-164">Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="21e12-165">Anonim IP adreslerinden oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="21e12-166">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="21e12-167">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="21e12-168">Alışılmadık konumlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="21e12-169">Aşağıdaki Azure AD anormal bir etkinliğin güvenlik raporları olmayan risk olaylarını Azure portalında eklendi:</span><span class="sxs-lookup"><span data-stu-id="21e12-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="21e12-170">Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="21e12-171">Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="21e12-172">Bu raporlara Klasik Azure portalında hala kullanılabilir, ancak bunlar gelecekte bir zamanda kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="21e12-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="21e12-173">Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="21e12-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="21e12-174">Algılanan risk olayı</span><span class="sxs-lookup"><span data-stu-id="21e12-174">Detected risk events</span></span>

<span data-ttu-id="21e12-175">Azure portalında algılanan risk olayı hakkında raporlar üzerinde erişebilirsiniz **Azure Active Directory** dikey altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="21e12-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="21e12-176">Algılanan risk olayı aşağıdaki raporlarda izlenir:</span><span class="sxs-lookup"><span data-stu-id="21e12-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="21e12-177">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="21e12-177">Users at Risk</span></span>
- <span data-ttu-id="21e12-178">Riskli Oturum Açma İşlemleri</span><span class="sxs-lookup"><span data-stu-id="21e12-178">Risky Sign-ins</span></span>

<span data-ttu-id="21e12-179">![Güvenlik raporları](./media/active-directory-reporting-migration/04.png "güvenlik raporları")</span><span class="sxs-lookup"><span data-stu-id="21e12-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="21e12-180">Güvenlik raporları hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="21e12-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="21e12-181">Azure Active Directory portalında Risk güvenlik raporu kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="21e12-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="21e12-182">Azure Active Directory portalında riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="21e12-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="21e12-183">Azure portalı ve Azure Klasik portalında etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="21e12-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="21e12-184">Bu bölümdeki tabloda Klasik Azure portalındaki varolan raporları listeler.</span><span class="sxs-lookup"><span data-stu-id="21e12-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="21e12-185">Ayrıca, Azure portalında aynı bilgilerin nasıl erişebileceğini anlatır.</span><span class="sxs-lookup"><span data-stu-id="21e12-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="21e12-186">Tüm denetim verileri görüntülemek için **Azure Active Directory** dikey altında **etkinlik**gidin **denetim günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="21e12-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="21e12-187">![Denetim günlükleri](./media/active-directory-reporting-migration/61.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="21e12-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="21e12-188">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="21e12-188">Azure classic portal</span></span>                 | <span data-ttu-id="21e12-189">Azure Portalı'nda bulmak için</span><span class="sxs-lookup"><span data-stu-id="21e12-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="21e12-190">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="21e12-190">Audit logs</span></span>                           | <span data-ttu-id="21e12-191">İçin **etkinlik kategorisi**seçin **çekirdek dizin**.</span><span class="sxs-lookup"><span data-stu-id="21e12-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="21e12-192">Parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-192">Password reset activity</span></span>              | <span data-ttu-id="21e12-193">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="21e12-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="21e12-194">Parola sıfırlama kaydı etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-194">Password reset registration activity</span></span> | <span data-ttu-id="21e12-195">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="21e12-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="21e12-196">Self Servis Grup etkinliği</span><span class="sxs-lookup"><span data-stu-id="21e12-196">Self-service groups activity</span></span>         | <span data-ttu-id="21e12-197">İçin **etkinlik kategorisi**seçin **Self Servis Grup Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="21e12-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="21e12-198">Hesap etkinlik sağlama</span><span class="sxs-lookup"><span data-stu-id="21e12-198">Account provisioning activity</span></span>        | <span data-ttu-id="21e12-199">İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.</span><span class="sxs-lookup"><span data-stu-id="21e12-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="21e12-200">Parola rollover durumu</span><span class="sxs-lookup"><span data-stu-id="21e12-200">Password rollover status</span></span>             | <span data-ttu-id="21e12-201">İçin **etkinlik kategorisi**seçin **otomatik uygulama parolası Rollover**.</span><span class="sxs-lookup"><span data-stu-id="21e12-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="21e12-202">Hesap hazırlama hataları</span><span class="sxs-lookup"><span data-stu-id="21e12-202">Account provisioning errors</span></span>          | <span data-ttu-id="21e12-203">İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.</span><span class="sxs-lookup"><span data-stu-id="21e12-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="21e12-204">Office365 grup adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="21e12-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="21e12-205">İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="21e12-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="21e12-206">İçin **etkinlik kaynak türü**seçin **grup**.</span><span class="sxs-lookup"><span data-stu-id="21e12-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="21e12-207">İçin **etkinlik kaynağı**seçin **O365 grupları**.</span><span class="sxs-lookup"><span data-stu-id="21e12-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="21e12-208">Görüntülemek için **uygulama kullanımı** üzerinde rapor **Azure Active Directory** dikey altında **Yönet**seçin **kurumsal uygulamalar**, ve ardından **oturum açma işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="21e12-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="21e12-209">![Kuruluş uygulamaları oturum açma işlemleri raporu](./media/active-directory-reporting-migration/199.png "Kurumsal uygulamaları oturum açma işlemleri raporu")</span><span class="sxs-lookup"><span data-stu-id="21e12-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e12-210">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21e12-210">Next steps</span></span>

<span data-ttu-id="21e12-211">Raporlamaya genel bir bakış için bkz. [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21e12-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
