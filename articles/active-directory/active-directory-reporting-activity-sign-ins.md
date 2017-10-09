---
title: "hello Azure Active Directory portalında aaaSign bileşenini etkinlik raporları | Microsoft Docs"
description: "Hello Azure Active Directory portalında giriş toosign bileşenini etkinlik raporları"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="a8132-103">Hello Azure Active Directory portalında oturum açma etkinliği raporları</span><span class="sxs-lookup"><span data-stu-id="a8132-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="a8132-104">Azure Active Directory (Azure AD) hello Raporlama ile [Azure portal](https://portal.azure.com), toodetermine ortamınızı nasıl yapılması gereken hello bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8132-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="a8132-105">Raporlama mimarisi Azure Active Directory'de hello bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="a8132-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="a8132-106">**Etkinlik**</span><span class="sxs-lookup"><span data-stu-id="a8132-106">**Activity**</span></span> 
    - <span data-ttu-id="a8132-107">**Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi</span><span class="sxs-lookup"><span data-stu-id="a8132-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="a8132-108">**Denetim günlükleri**: Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a8132-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="a8132-109">**Güvenlik**</span><span class="sxs-lookup"><span data-stu-id="a8132-109">**Security**</span></span> 
    - <span data-ttu-id="a8132-110">**Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="a8132-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="a8132-111">Daha fazla bilgi için bkz. Riskli oturum açma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="a8132-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="a8132-112">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="a8132-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="a8132-113">Daha fazla bilgi için bkz. Riskli oldukları belirlenen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="a8132-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="a8132-114">Bu konuda, oturum açma hello etkinlikleri genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8132-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="a8132-115">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="a8132-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="a8132-116">Merhaba veri erişebilecek mi?</span><span class="sxs-lookup"><span data-stu-id="a8132-116">Who can access hello data?</span></span>
* <span data-ttu-id="a8132-117">Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="a8132-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="a8132-118">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="a8132-118">Global Admins</span></span>
* <span data-ttu-id="a8132-119">Tüm kullanıcılar (yönetici olmayan) kendi oturum açma etkinliklerine erişebilirler</span><span class="sxs-lookup"><span data-stu-id="a8132-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="a8132-120">Hangi Azure AD lisans tooaccess oturum açma etkinliği gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="a8132-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="a8132-121">Kiracı kendisiyle ilişkili bir Azure AD Premium lisansına sahip olması gerekir toosee hello tüm kadar oturum açma etkinliği raporu</span><span class="sxs-lookup"><span data-stu-id="a8132-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="a8132-122">Oturum açma etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="a8132-122">Signs-in activities</span></span>

<span data-ttu-id="a8132-123">Oturum açma Hello kullanıcı raporu tarafından sağlanan hello bilgilerle yanıtlar tooquestions gibi bulun:</span><span class="sxs-lookup"><span data-stu-id="a8132-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="a8132-124">Bir kullanıcı oturum açma hello desenini nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="a8132-125">Bir hafta içerisinde kaç adet kullanıcı oturum açtı?</span><span class="sxs-lookup"><span data-stu-id="a8132-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="a8132-126">Bu oturum açma işlemleri hello durumu nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="a8132-127">Verilerin ilk giriş noktası tooall oturum açma etkinliklerinizi **oturum açma işlemleri** hello etkinlik bölümünde **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="a8132-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="a8132-128">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/61.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="a8132-129">Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:</span><span class="sxs-lookup"><span data-stu-id="a8132-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="a8132-130">Merhaba ilgili kullanıcı</span><span class="sxs-lookup"><span data-stu-id="a8132-130">hello related user</span></span>
- <span data-ttu-id="a8132-131">Merhaba uygulama hello kullanıcısı için açan</span><span class="sxs-lookup"><span data-stu-id="a8132-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="a8132-132">Merhaba oturum açma durumu</span><span class="sxs-lookup"><span data-stu-id="a8132-132">hello sign-in status</span></span>
- <span data-ttu-id="a8132-133">Merhaba oturum açma zamanı</span><span class="sxs-lookup"><span data-stu-id="a8132-133">hello sign-in time</span></span>

<span data-ttu-id="a8132-134">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/41.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-135">Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.</span><span class="sxs-lookup"><span data-stu-id="a8132-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="a8132-136">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/19.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-137">Bu toodisplay ek alanlar etkinleştirir veya zaten görüntülenen alanları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a8132-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="a8132-138">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/42.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-139">Merhaba liste görünümünde bir öğeyi tıklatarak bunu hakkında tüm kullanılabilir ayrıntıları alın.</span><span class="sxs-lookup"><span data-stu-id="a8132-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="a8132-140">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/43.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="a8132-141">Oturum açma etkinliklerini filtreleme</span><span class="sxs-lookup"><span data-stu-id="a8132-141">Filtering sign-in activities</span></span>

<span data-ttu-id="a8132-142">Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello gerçekleştirilen oturum açma verileri filtreleyebilirsiniz bildirdi:</span><span class="sxs-lookup"><span data-stu-id="a8132-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="a8132-143">Zaman aralığı</span><span class="sxs-lookup"><span data-stu-id="a8132-143">Time interval</span></span>
- <span data-ttu-id="a8132-144">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="a8132-144">User</span></span>
- <span data-ttu-id="a8132-145">Uygulama</span><span class="sxs-lookup"><span data-stu-id="a8132-145">Application</span></span>
- <span data-ttu-id="a8132-146">İstemci</span><span class="sxs-lookup"><span data-stu-id="a8132-146">Client</span></span>
- <span data-ttu-id="a8132-147">Oturum açma durumu</span><span class="sxs-lookup"><span data-stu-id="a8132-147">Sign-in status</span></span>

<span data-ttu-id="a8132-148">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/44.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="a8132-149">Merhaba **zaman aralığı** filtre etkinleştirir tooyou toodefine hello için bir zaman çerçevesi veri döndürdü.</span><span class="sxs-lookup"><span data-stu-id="a8132-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="a8132-150">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a8132-150">Possible values are:</span></span>

- <span data-ttu-id="a8132-151">1 ay</span><span class="sxs-lookup"><span data-stu-id="a8132-151">1 month</span></span>
- <span data-ttu-id="a8132-152">7 gün</span><span class="sxs-lookup"><span data-stu-id="a8132-152">7 days</span></span>
- <span data-ttu-id="a8132-153">24 saat</span><span class="sxs-lookup"><span data-stu-id="a8132-153">24 hours</span></span>
- <span data-ttu-id="a8132-154">Özel</span><span class="sxs-lookup"><span data-stu-id="a8132-154">Custom</span></span>

<span data-ttu-id="a8132-155">Özel bir zaman çerçevesi seçerken başlangıç ve bitiş zamanını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8132-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="a8132-156">Merhaba **kullanıcı** filtresini etkinleştirir, size, toospecify hello adı veya hello kullanıcı asıl adı (UPN) önem verdiğiniz hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="a8132-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="a8132-157">Merhaba **uygulama** filtre önem verdiğiniz hello uygulamasının toospecify hello adı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8132-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="a8132-158">Merhaba **istemci** filtre toospecify önem verdiğiniz hello cihaz hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8132-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="a8132-159">Merhaba **oturum açma durumu** filtre filtre aşağıdaki Merhaba, tooselect sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8132-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="a8132-160">Tümü</span><span class="sxs-lookup"><span data-stu-id="a8132-160">All</span></span>
- <span data-ttu-id="a8132-161">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a8132-161">Success</span></span>
- <span data-ttu-id="a8132-162">Hata</span><span class="sxs-lookup"><span data-stu-id="a8132-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="a8132-163">Oturum açma etkinlikleri kısayolları</span><span class="sxs-lookup"><span data-stu-id="a8132-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="a8132-164">Ayrıca Active Directory tooAzure, hello Azure portal, iki ek giriş noktaları toosign bileşenini etkinlikleri verilerle sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8132-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="a8132-165">Kullanıcılar ve gruplar</span><span class="sxs-lookup"><span data-stu-id="a8132-165">Users and groups</span></span>
- <span data-ttu-id="a8132-166">Kurumsal uygulamalar</span><span class="sxs-lookup"><span data-stu-id="a8132-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="a8132-167">Kullanıcı ve grupların oturum açma etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="a8132-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="a8132-168">Oturum açma Hello kullanıcı raporu tarafından sağlanan hello bilgilerle yanıtlar tooquestions gibi bulun:</span><span class="sxs-lookup"><span data-stu-id="a8132-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="a8132-169">Bir kullanıcı oturum açma hello desenini nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="a8132-170">Bir hafta içerisinde kaç adet kullanıcı oturum açtı?</span><span class="sxs-lookup"><span data-stu-id="a8132-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="a8132-171">Bu oturum açma işlemleri hello durumu nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="a8132-172">Giriş noktası toothis verilerinizi hello kullanıcı oturum açma grafiğinde hello olan **genel bakış** altında bölümünde **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a8132-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="a8132-173">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/45.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-174">oturum açma Hello kullanıcı grafik gösterir oturum haftalık toplamalarının belirli bir süre içinde tüm kullanıcılar için bileşenler.</span><span class="sxs-lookup"><span data-stu-id="a8132-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="a8132-175">hello için Hello varsayılan süre 30 gündür.</span><span class="sxs-lookup"><span data-stu-id="a8132-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="a8132-176">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/46.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-177">Oturum açma hello grafikteki bir günde tıkladığınızda, bu günlük hello oturum açma etkinliklerini ayrıntılı bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a8132-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="a8132-178">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/41.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-179">Her satırda bir seçili hello oturum açma gibi hakkında ayrıntılı bilgi hello hello oturum açma etkinlikleri listesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8132-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="a8132-180">Kim oturum açtı?</span><span class="sxs-lookup"><span data-stu-id="a8132-180">Who has signed in?</span></span>
* <span data-ttu-id="a8132-181">Merhaba neydi UPN ilgili?</span><span class="sxs-lookup"><span data-stu-id="a8132-181">What was hello related UPN?</span></span>
* <span data-ttu-id="a8132-182">Hangi uygulama hello oturum açma hello hedefi neydi?</span><span class="sxs-lookup"><span data-stu-id="a8132-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="a8132-183">Başlangıç IP adresi hello oturum açma nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="a8132-184">Merhaba oturum açma hello durumu neydi?</span><span class="sxs-lookup"><span data-stu-id="a8132-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="a8132-185">Merhaba **oturum açma işlemleri** seçeneği tüm kullanıcı oturum açma işlemlerine eksiksiz bir genel bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="a8132-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="a8132-186">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/51.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="a8132-187">Yönetilen uygulamaların kullanımı</span><span class="sxs-lookup"><span data-stu-id="a8132-187">Usage of managed applications</span></span>

<span data-ttu-id="a8132-188">Oturum açma bilgilerinizin uygulama odaklı bir görünümüyle aşağıdakiler gibi sorular yanıtlanabilir:</span><span class="sxs-lookup"><span data-stu-id="a8132-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="a8132-189">Uygulamalarımı kimler kullanıyor?</span><span class="sxs-lookup"><span data-stu-id="a8132-189">Who is using my applications?</span></span>
* <span data-ttu-id="a8132-190">Kuruluşunuzdaki hello üst 3 uygulamaları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="a8132-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="a8132-191">Kısa bir süre önce bir uygulamayı kullanıma sundum.</span><span class="sxs-lookup"><span data-stu-id="a8132-191">I have recently rolled out an application.</span></span> <span data-ttu-id="a8132-192">Uygulamanın durumu nedir?</span><span class="sxs-lookup"><span data-stu-id="a8132-192">How is it doing?</span></span>

<span data-ttu-id="a8132-193">Giriş noktası toothis verilerinizi hello üst 3 uygulamalarında hello son 30 gün raporda hello kuruluşunuzda olan **genel bakış** altında bölümünde **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a8132-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="a8132-194">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/64.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-195">belirli bir süre içinde ilk 3 uygulamalarınız için oturum açmalar Hello uygulama kullanım grafiği haftalık toplamalarının.</span><span class="sxs-lookup"><span data-stu-id="a8132-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="a8132-196">hello için Hello varsayılan süre 30 gündür.</span><span class="sxs-lookup"><span data-stu-id="a8132-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="a8132-197">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/47.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="a8132-198">İsterseniz, belirli bir uygulama hello odak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8132-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="a8132-199">![Raporlama](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="a8132-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="a8132-200">Merhaba uygulama kullanım grafiği bir günde tıkladığınızda hello oturum açma etkinliklerini ayrıntılı bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a8132-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="a8132-201">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/48.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="a8132-202">Merhaba **oturum açma işlemleri** seçeneği tüm oturum açma olayları tooyour uygulamaları eksiksiz bir genel bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="a8132-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="a8132-203">![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins/49.png "oturum açma etkinliği")</span><span class="sxs-lookup"><span data-stu-id="a8132-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="a8132-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8132-204">Next steps</span></span>

<span data-ttu-id="a8132-205">Merhaba tooknow oturum açma etkinliği hata kodları hakkında daha fazla bilgi istiyorsanız bkz [oturum açma etkinliği raporu hata kodları hello Azure Active Directory portalında](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a8132-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

