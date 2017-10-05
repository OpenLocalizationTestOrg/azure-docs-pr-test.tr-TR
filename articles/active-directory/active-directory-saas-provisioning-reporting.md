---
title: "Azure Active Directory'ye otomatik olarak bir kullanıcı hesabı SaaS uygulamaları için sağlama üzerinde raporlama | Microsoft Docs"
description: "İşlerini sağlama otomatik olarak bir kullanıcı hesabı durumunu denetlemek nasıl, bireysel kullanıcılar sağlama ile ilgili sorunları giderme öğrenin."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 86b9a3d93745045904c6038583b9bc6ebac5667e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a><span data-ttu-id="191e1-103">Öğretici: otomatik olarak bir kullanıcı hesabı sağlama raporlama</span><span class="sxs-lookup"><span data-stu-id="191e1-103">Tutorial: Reporting on automatic user account provisioning</span></span>


<span data-ttu-id="191e1-104">Azure Active Directory içeren bir [hizmet sağlama kullanıcı hesabı](active-directory-saas-app-provisioning.md) yardımcı sağlama SaaS uygulamaları ve diğer sistemler uçtan uca kimlik yaşam döngüsü amacıyla kullanıcı hesaplarının sağlamayı kaldırma özelliklerini otomatikleştirme yönetimi.</span><span class="sxs-lookup"><span data-stu-id="191e1-104">Azure Active Directory includes a [user account provisioning service](active-directory-saas-app-provisioning.md) that helps automate the provisioning de-provisioning of user accounts in SaaS apps and other systems, for the purpose of end-to-end identity lifecycle management.</span></span> <span data-ttu-id="191e1-105">Azure AD destekleyen tüm uygulamalar ve sistemler "Öne çıkan" bölümündeki bağlayıcılarının sağlama önceden tümleştirilmiş kullanıcı [Azure AD uygulama galerisinde](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span><span class="sxs-lookup"><span data-stu-id="191e1-105">Azure AD supports pre-integrated user provisioning connectors for all of the applications and systems in the "Featured" section of the [Azure AD application gallery](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span></span>

<span data-ttu-id="191e1-106">Bu makalede, bunlar ayarlanan sonra işleri sağlama durumunu kontrol etme ve tek tek kullanıcılar ve gruplar sağlama ile ilgili sorunları giderme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="191e1-106">This article describes how to check the status of provisioning jobs after they have been set up, and how to troubleshoot the provisioning of individual users and groups.</span></span>

## <a name="overview"></a><span data-ttu-id="191e1-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="191e1-107">Overview</span></span>

<span data-ttu-id="191e1-108">Sağlama bağlayıcılar öncelikle ayarlanır ve kullanılarak yapılandırılan [Azure Yönetim Portalı](https://portal.azure.com), izleyerek [belgelerine sağlanan](active-directory-saas-tutorial-list.md) burada kullanıcı hesabı sağlama, uygulama için İstenen.</span><span class="sxs-lookup"><span data-stu-id="191e1-108">Provisioning connectors are primarily set up and configured using the [Azure management portal](https://portal.azure.com), by following the [provided documentation](active-directory-saas-tutorial-list.md) for the application where user account provisioning is desired.</span></span> <span data-ttu-id="191e1-109">Yapılandırılmış ve çalışan sonra bir uygulama için işleri sağlama iki yöntemden birini kullanarak bildirilebilir:</span><span class="sxs-lookup"><span data-stu-id="191e1-109">Once configured and running, provisioning jobs for an application can be reported on using one of two methods:</span></span>

* <span data-ttu-id="191e1-110">**Azure Yönetim Portalı** -bu makalede, öncelikle rapor bilgilerini alma açıklanır [Azure Yönetim Portalı](https://portal.azure.com), hem bir sağlama özet raporu yanı sıra sağlama ayrıntılı denetim sağlar belirli bir uygulamada günlükleri.</span><span class="sxs-lookup"><span data-stu-id="191e1-110">**Azure management portal** - This article primarily describes retrieving report information from the [Azure management portal](https://portal.azure.com), which provides both a provisioning summary report as well as detailed provisioning audit logs for a given application.</span></span>

* <span data-ttu-id="191e1-111">**API denetim** -Azure Active Directory ayrıca bir denetim ayrıntılı sağlama denetim günlüklerini programlı alınmasını sağlayan API sağlar.</span><span class="sxs-lookup"><span data-stu-id="191e1-111">**Audit API** - Azure Active Directory also provides an Audit API that enables programmatic retrieval of the detailed provisioning audit logs.</span></span> <span data-ttu-id="191e1-112">Bkz: [Azure Active Directory denetim API Başvurusu](active-directory-reporting-api-audit-reference.md) bu API'yi kullanarak belirli belgeleri için.</span><span class="sxs-lookup"><span data-stu-id="191e1-112">See [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md) for documentation specific to using this API.</span></span> <span data-ttu-id="191e1-113">Bu makalede API kullanma özellikle kapsamaz olsa da, Denetim günlüğüne kaydedilen olayları sağlama türleri detaylandırır.</span><span class="sxs-lookup"><span data-stu-id="191e1-113">While this article does not specifically cover how to use the API, it does detail the types of provisioning events that are recorded in the audit log.</span></span>

### <a name="definitions"></a><span data-ttu-id="191e1-114">Tanımlar</span><span class="sxs-lookup"><span data-stu-id="191e1-114">Definitions</span></span>

<span data-ttu-id="191e1-115">Bu makalede aşağıda tanımlanan aşağıdaki terimler kullanır:</span><span class="sxs-lookup"><span data-stu-id="191e1-115">This article uses the following terms, defined below:</span></span>

* <span data-ttu-id="191e1-116">**Kaynak sistem** -hizmet sağlama Azure AD alanından eşitler kullanıcı deposu.</span><span class="sxs-lookup"><span data-stu-id="191e1-116">**Source System** - The repository of users that the Azure AD provisioning service synchronizes from.</span></span> <span data-ttu-id="191e1-117">Azure Active Directory kaynak sistem çoğunluğu için bağlayıcıları sağlama önceden tümleştirilmiştir, ancak kopyalanamayan bazı özel durumlar (örnek: Workday gelen eşitleme).</span><span class="sxs-lookup"><span data-stu-id="191e1-117">Azure Active Directory is the source system for the majority of pre-integrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).</span></span>

* <span data-ttu-id="191e1-118">**Hedef sistem** -için hizmet sağlama Azure AD eşitler kullanıcı deposu.</span><span class="sxs-lookup"><span data-stu-id="191e1-118">**Target System** - The repository of users that the Azure AD provisioning service synchronizes to.</span></span> <span data-ttu-id="191e1-119">Bu genellikle bir SaaS uygulaması olur (örnek: Salesforce, ServiceNow, Google Apps, iş için Dropbox), ancak bazı durumlarda Active Directory gibi şirket içi sistem olabilir (örnek: Active Directory'ye Workday gelen eşitleme).</span><span class="sxs-lookup"><span data-stu-id="191e1-119">This is typically a SaaS application (examples: Salesforce, ServiceNow, Google Apps, Dropbox for Business), but in some cases can be an on-premises system such as Active Directory (example: Workday Inbound Synchronization to Active Directory).</span></span>


## <a name="getting-provisioning-reports-from-the-azure-management-portal"></a><span data-ttu-id="191e1-120">Azure Yönetim Portalı'ndan raporları sağlama alma</span><span class="sxs-lookup"><span data-stu-id="191e1-120">Getting provisioning reports from the Azure management portal</span></span>

<span data-ttu-id="191e1-121">Başlatarak sağlama belirli bir uygulamada rapor bilgilerini almak için başlangıç [Azure Yönetim Portalı](https://portal.azure.com) ve kuruluş için sağlama yapılandırılmış bir uygulama için gözatma.</span><span class="sxs-lookup"><span data-stu-id="191e1-121">To get provisioning report information for a given application, start by launching the [Azure management portal](https://portal.azure.com) and browsing to the Enterprise Application for which provisioning is configured.</span></span> <span data-ttu-id="191e1-122">Örneğin, LinkedIn yükseltmesine kullanıcılara sağlama, uygulama ayrıntıları Gezinti yolu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="191e1-122">For example, if you are provisioning users to LinkedIn Elevate, the navigation path to the application details is:</span></span>

<span data-ttu-id="191e1-123">**Azure Active Directory > Kurumsal uygulamalar > tüm uygulamaları > LinkedIn Yükselt**</span><span class="sxs-lookup"><span data-stu-id="191e1-123">**Azure Active Directory > Enterprise Applications > All applications > LinkedIn Elevate**</span></span>

<span data-ttu-id="191e1-124">Buradan, hazırlama özet raporu hem sağlama denetim günlüklerini erişebilir, her ikisi de aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="191e1-124">From here, you can access both the Provisioning summary report, and the provisioning audit logs, both described below.</span></span>


### <a name="provisioning-summary-report"></a><span data-ttu-id="191e1-125">Sağlama özet raporu</span><span class="sxs-lookup"><span data-stu-id="191e1-125">Provisioning summary report</span></span>

<span data-ttu-id="191e1-126">Sağlama özet raporu görünür **sağlama** uygulama sekmesinde için.</span><span class="sxs-lookup"><span data-stu-id="191e1-126">The provisioning summary report is visible in the **Provisioning** tab for given application.</span></span> <span data-ttu-id="191e1-127">Eşitleme ayrıntıları bölümü altında bulunan **ayarları**ve aşağıdaki bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="191e1-127">It is located in the Synchronization Details section underneath **Settings**, and provides the following information:</span></span>

* <span data-ttu-id="191e1-128">Toplam sayısı, kullanıcı ve / grupları, eşitlenmemiş ve şu anda kapsamında kaynak ve hedef sistemleri arasında sağlama.</span><span class="sxs-lookup"><span data-stu-id="191e1-128">The total number of users and/groups that have been synchronized and are currently in scope for provisioning between the source system and the target system.</span></span>

* <span data-ttu-id="191e1-129">En son ne zaman eşitleme çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="191e1-129">The last time the synchronization was run.</span></span> <span data-ttu-id="191e1-130">Eşitlemeler genellikle 20-40 tam eşitleme tamamlandıktan sonra dakikada oluşur.</span><span class="sxs-lookup"><span data-stu-id="191e1-130">Synchronizations typically occur every 20-40 minutes, after a full synchronization has completed.</span></span>

* <span data-ttu-id="191e1-131">Desteklemediğini ilk tam Eşitleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="191e1-131">Whether or not an initial full synchronization has been completed.</span></span>

* <span data-ttu-id="191e1-132">Sağlama işlemini Karantinadaki yerleştirilmiş olup olmadığına ve karantina durum nedeni örn (geçersiz yönetici kimlik bilgileri nedeniyle hedef sistemiyle iletişim kurulamıyor) nedir</span><span class="sxs-lookup"><span data-stu-id="191e1-132">Whether or not the provisioning process has been placed in quarantine, and what the reason for the quarantine status is (e.g. failure to communicate with target system due to invalid admin credentials)</span></span>

<span data-ttu-id="191e1-133">Sağlama özet raporu sağlama işi işletimsel durumunu denetlemek için ilk yer admins görünüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="191e1-133">The provisioning summary report should be the first place admins look to check on the operational health of the provisioning job.</span></span>

 ![Özet raporu](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a><span data-ttu-id="191e1-135">Sağlama denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="191e1-135">Provisioning audit logs</span></span>
<span data-ttu-id="191e1-136">Sağlama hizmeti tarafından gerçekleştirilen tüm etkinlikler görüntülenebilir Azure AD denetim günlüklerine kaydedilir **denetim günlüklerini** altında sekmesinde **hesap sağlama** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="191e1-136">All activities performed by the provisioning service are recorded in the Azure AD audit logs, which can be viewed in the **Audit logs** tab under the **Account Provisioning** category.</span></span> <span data-ttu-id="191e1-137">Günlüğe kaydedilen etkinlik olay türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="191e1-137">Logged activity event types include:</span></span>

* <span data-ttu-id="191e1-138">**Olayları alma** -hizmet sağlama Azure AD, bir kaynak sistemi veya hedef sistem tek bir kullanıcı veya grup hakkında bilgi alır her zaman bir "alma" olayı kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="191e1-138">**Import events** - An "import" event is recorded each time the Azure AD provisioning service retrieves information about an individual user or group from a source system or target system.</span></span> <span data-ttu-id="191e1-139">Eşitleme sırasında kullanıcılar kaynak sistemden ilk olarak, "olayları Al"olarak kaydedilen sonuçlarıyla alınır.</span><span class="sxs-lookup"><span data-stu-id="191e1-139">During synchronization, users are retrieved from the source system first, with the results recorded as "import" events.</span></span> <span data-ttu-id="191e1-140">Alınan kullanıcı eşleşen kimlikleri, de "Al" olayları olarak kaydedilen sonuçlarla varsa denetlemek için hedef sistemine karşı seçmeleri istenir.</span><span class="sxs-lookup"><span data-stu-id="191e1-140">The matching IDs of the retrieved users are then queried against the target system to check if they exist, with the results also recorded as "import" events.</span></span> <span data-ttu-id="191e1-141">Bu olaylar, tüm eşlenen kullanıcı öznitelikleri ve olay aynı anda hizmet sağlama Azure AD tarafından görülen değerlerine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="191e1-141">These events record all mapped user attributes and their values that were seen by the Azure AD provisioning service at the time of the event.</span></span> 

* <span data-ttu-id="191e1-142">**Eşitleme kuralı olayları** - bu olayları özniteliği eşleme kurallarını sonuçlarını rapor ve kullanıcı verilerini içe ve kaynak ve hedef sistemlerden hesaplanan sonra herhangi bir kapsam filtreleri, yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="191e1-142">**Synchronization rule events** - These events report on the results of the attribute mapping rules and any configured scoping filters, after user data has been imported and evaluated from the source and target systems.</span></span> <span data-ttu-id="191e1-143">Örneğin, bir kullanıcı bir kaynak sistemde sağlama için kapsam olarak kabul ve hedef sistemde mevcut değil, bu olay kayıtlarını sonra kabul kullanıcı hedef sistemde sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="191e1-143">For example, if a user in a source system is deemed to be in scope for provisioning, and deemed to not exist in the target system, then this event records that the user will be provisioned in the target system.</span></span> 

* <span data-ttu-id="191e1-144">**Olay Ver** -hizmet sağlama Azure AD hedef sistem için bir kullanıcı hesabı veya grup nesnesi Yazar her zaman "export" olay kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="191e1-144">**Export events** - An "export" event is recorded each time the Azure AD provisioning service writes a user account or group object to a target system.</span></span> <span data-ttu-id="191e1-145">Bu olaylar, tüm kullanıcı özniteliklerini ve Azure AD tarafından hizmet olayı aynı anda sağlama yazılmış değerleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="191e1-145">These events record all user attributes and their values that were written by the Azure AD provisioning service at the time of the event.</span></span> <span data-ttu-id="191e1-146">Oluştu hata oluşursa hedef sisteme kullanıcı hesabı veya grup nesnesi yazılırken, burada görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="191e1-146">If there was an error while writing the user account or group object to the target system, it will be displayed here.</span></span>

* <span data-ttu-id="191e1-147">**İşlem emanet olayları** -işlem escrows ortaya sağlama hizmeti bir işlem çalışırken bir hatayla karşılaşırsa ve bir geri alma aralığı süre işlemi yeniden deneyin başlar.</span><span class="sxs-lookup"><span data-stu-id="191e1-147">**Process escrow events** - Process escrows occur when the provisioning service encounters a failure while attempting an operation, and begins to retry the operation on a back-off interval of time.</span></span> <span data-ttu-id="191e1-148">Bir "emanet" olay sağlama işlemi devre dışı bırakılan her zaman kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="191e1-148">An "escrow" event is recorded each time a provisioning operation was retired.</span></span>

<span data-ttu-id="191e1-149">Olayları tek bir kullanıcı için sağlama sırasında bakarken olaylar normalde bu sırada oluşur:</span><span class="sxs-lookup"><span data-stu-id="191e1-149">When looking at provisioning events for an individual user, the events normally occur in this order:</span></span>

1. <span data-ttu-id="191e1-150">Alma olayı: kullanıcı, kaynak sistemden alınır.</span><span class="sxs-lookup"><span data-stu-id="191e1-150">Import event: User is retrieved from the source system.</span></span>

2. <span data-ttu-id="191e1-151">Alma olayı: hedef sistem sorgulanan alınan kullanıcı varlığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="191e1-151">Import event: Target system is queried to check for the existence of the retrieved user.</span></span>

3. <span data-ttu-id="191e1-152">Eşitleme kuralı olayı: kullanıcı verilerini hedef ve kaynak sistemlerden eşleme kurallarını ve kapsam belirleme filtreleri varsa, hangi eylemin gerçekleştirileceğini belirlemek için yapılandırılmış öznitelik karşı değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="191e1-152">Synchronization rule event: User data from source and target systems are evaluated against the configured attribute mapping rules and scoping filters to determine what action, if any, should be performed.</span></span>

4. <span data-ttu-id="191e1-153">Olayı ver: eşitleme kuralını olay eylem olması gerektiğini dikte varsa (örneğin ekleme, güncelleştirme, silme), eylem sonuçlarını dışarı aktarma olayda kaydedilir sonra gerçekleştirilen.</span><span class="sxs-lookup"><span data-stu-id="191e1-153">Export event: If the synchronization rule event dictated that an action should be performed (e.g. Add, Update, Delete), then the results of the action are recorded in an Export event.</span></span>

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a><span data-ttu-id="191e1-155">Belirli bir kullanıcı için olayları sağlama yukarı aranıyor</span><span class="sxs-lookup"><span data-stu-id="191e1-155">Looking up provisioning events for a specific user</span></span>

<span data-ttu-id="191e1-156">En yaygın kullanım için sağlama denetim günlüklerini bireysel bir kullanıcı hesabı sağlama durumunu denetlemek için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="191e1-156">The most common use case for the provisioning audit logs is to check the provisioning status of an individual user account.</span></span> <span data-ttu-id="191e1-157">Belirli bir kullanıcı için son sağlama olayları aramak için:</span><span class="sxs-lookup"><span data-stu-id="191e1-157">To look up the last provisioning events for a specific user:</span></span>

1. <span data-ttu-id="191e1-158">Git **denetim günlüklerini** bölümü.</span><span class="sxs-lookup"><span data-stu-id="191e1-158">Go to the **Audit logs** section.</span></span>

2. <span data-ttu-id="191e1-159">Gelen **kategori** menüsünde, select **hesap sağlama**.</span><span class="sxs-lookup"><span data-stu-id="191e1-159">From the **Category** menu, select **Account Provisioning**.</span></span>

3. <span data-ttu-id="191e1-160">İçinde **tarih aralığı** menüsünde, aramak istediğiniz tarih aralığını seçin</span><span class="sxs-lookup"><span data-stu-id="191e1-160">In the **Date Range** menu, select the date range you want to search,</span></span>

4. <span data-ttu-id="191e1-161">İçinde **arama** çubuğu, aramak istediğiniz kullanıcının kullanıcı Kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="191e1-161">In the **Search** bar, enter the user ID of the user you wish to search for.</span></span> <span data-ttu-id="191e1-162">Kimliği değerinin biçimi ne olursa olsun özniteliği eşleme yapılandırması (örn. userPrincipalName veya çalışan kimlik numarası) birincil eşleşen kimliği olarak seçtiğiniz eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="191e1-162">The format of ID value should match whatever you selected as the primary matching ID in the attribute mapping configuration (e.g. userPrincipalName or employee ID number).</span></span> <span data-ttu-id="191e1-163">Gerekli kimlik değeri hedeflere sütununda görünür.</span><span class="sxs-lookup"><span data-stu-id="191e1-163">The ID value required will be visible in the Target(s) column.</span></span>

5. <span data-ttu-id="191e1-164">Arama için Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="191e1-164">Press Enter to search.</span></span> <span data-ttu-id="191e1-165">En son sağlama olayların ilk döndürülür.</span><span class="sxs-lookup"><span data-stu-id="191e1-165">The most recent provisioning events will be returned first.</span></span>

6. <span data-ttu-id="191e1-166">Olayları döndürülürse, etkinlik türleri ve olup bunlar başarılı veya başarısız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="191e1-166">If events are returned, note the activity types and whether they succeeded or failed.</span></span> <span data-ttu-id="191e1-167">Ardından hiç sonuç döndürmedi, kullanıcı yok ya da bir tam eşitleme henüz tamamlanmadı, henüz Hazırlama işlemi tarafından algılanmadı demektir.</span><span class="sxs-lookup"><span data-stu-id="191e1-167">If no results are returned, then it means the user either does not exist, or has not yet been detected by the provisioning process if a full sync has not yet completed.</span></span>

7. <span data-ttu-id="191e1-168">Alınan, değerlendirilen ya da olay bir parçası olarak yazılan tüm kullanıcı özellikler de dahil olmak üzere ilave ayrıntıları görüntülemek için olayları tek tek tıklatın.</span><span class="sxs-lookup"><span data-stu-id="191e1-168">Click on individual events to view extended details, including all user properties that were retrieved, evaluated, or written as part of the event.</span></span>


### <a name="tips-for-viewing-the-provisioning-audit-logs"></a><span data-ttu-id="191e1-169">Sağlama denetim günlüklerini görüntülemek için ipuçları</span><span class="sxs-lookup"><span data-stu-id="191e1-169">Tips for viewing the provisioning audit logs</span></span>

<span data-ttu-id="191e1-170">Azure Portalı'ndaki en iyi okunabilirlik için seçin **sütunları** düğmesini tıklatın ve bu sütunları seçin:</span><span class="sxs-lookup"><span data-stu-id="191e1-170">For best readability in the Azure portal, select the **Columns** button and choose these columns:</span></span>

* <span data-ttu-id="191e1-171">**Tarih** -olayın tarihi gösterir.</span><span class="sxs-lookup"><span data-stu-id="191e1-171">**Date** - Shows the date the event occurred.</span></span>
* <span data-ttu-id="191e1-172">**Hedeflere** -olay konular uygulama adı ve kullanıcı Kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="191e1-172">**Target(s)** - Shows the app name and user ID that are the subjects of the event.</span></span>
* <span data-ttu-id="191e1-173">**Etkinlik** -daha önce açıklandığı gibi etkinlik türü.</span><span class="sxs-lookup"><span data-stu-id="191e1-173">**Activity** - The activity type, as described previously.</span></span>
* <span data-ttu-id="191e1-174">**Durum** - olay veya başarılı olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="191e1-174">**Status** - Whether the event succeeded or not.</span></span>
* <span data-ttu-id="191e1-175">**Durum Açıklaması** -sağlama durumunda ne Özet.</span><span class="sxs-lookup"><span data-stu-id="191e1-175">**Status Reason** - A summary of what happened in the provisioning event.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="191e1-176">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="191e1-176">Troubleshooting</span></span>

<span data-ttu-id="191e1-177">Sağlama özet raporu ve Denetim günlükleri sorunları sağlama çeşitli kullanıcı hesabı sorun giderme admins yardımcı olacak önemli bir rol oynar.</span><span class="sxs-lookup"><span data-stu-id="191e1-177">The provisioning summary report and audit logs play a key role helping admins troubleshoot various user account provisioning issues.</span></span>

<span data-ttu-id="191e1-178">Senaryo tabanlı otomatik kullanıcı sağlamayı ile ilgili sorunları giderme hakkında yönergeler için bkz [yapılandırma ve uygulama kullanıcılara sağlama sorunları](active-directory-application-provisioning-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="191e1-178">For scenario-based guidance on how to troubleshoot automatic user provisioning, see [Problems configuring and provisioning users to an application](active-directory-application-provisioning-content-map.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="191e1-179">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="191e1-179">Additional Resources</span></span>

* [<span data-ttu-id="191e1-180">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="191e1-180">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="191e1-181">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="191e1-181">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
