---
title: aaaAzure Active Directory Raporlama ile ilgili SSS | Microsoft Docs
description: Azure Active Directory Raporlama ile ilgili SSS.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="e8fed-103">SSS raporlama Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8fed-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="e8fed-104">Bu makale, Azure Active Directory raporlama hakkında sorulan sorular (SSS) yanıtlar toofrequently içerir.</span><span class="sxs-lookup"><span data-stu-id="e8fed-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="e8fed-105">Daha fazla ayrıntı için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8fed-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="e8fed-106">**S: hello veri bekletme etkinlik günlükleri (Denetim ve oturum açma işlemleri) için hello Azure portalı nedir?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="e8fed-107">**Y:** ücretsiz müşterilerimiz için ve tooan Azure AD Premium 1 veya Premium 2 lisans geçiş tarafından 7 günlük verileri sağlamak için verileri too30 günlerini erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8fed-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="e8fed-108">Bekletme hakkında daha fazla bilgi için bkz: [Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="e8fed-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="e8fed-109">**S: my görev tamamladığınızda hello etkinlik verileri görene kadar ne kadar sürer?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="e8fed-110">**Y:** denetim etkinlik günlükleri 15 dakika tooan saat arasında bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="e8fed-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="e8fed-111">Oturum açma etkinliği günlükleri çoğu kaydeder ve birkaç kayıtları too2 saat 15 dakika arasında değişen bir gecikme süresine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e8fed-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="e8fed-112">**S: bir genel yönetici toosee hello etkinliği hello Azure Portal ya da hello API üzerinden tooget veri günlüklerini toobe gerekiyor?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="e8fed-113">**C:** Hayır.</span><span class="sxs-lookup"><span data-stu-id="e8fed-113">**A:** No.</span></span> <span data-ttu-id="e8fed-114">Ya da olabilir bir **güvenlik okuyucu**, **güvenlik yönetici** veya **genel yönetici** raporlama verilerini Azure portalında veya hello API erişerek toosee.</span><span class="sxs-lookup"><span data-stu-id="e8fed-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="e8fed-115">**S: Office 365 etkinlik günlüğü bilgilerini hello Azure portal aracılığıyla alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="e8fed-116">**Y:** olsa bile Office 365 etkinliği ve Azure AD etkinlik günlükleri paylaşım çok fazla tam görünümünü istiyorsanız hello dizin kaynak, Office 365 etkinlik günlükleri Merhaba, toohello Office 365 Yönetim Merkezi tooget Office 365 etkinlik günlüğü bilgilerini tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8fed-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="e8fed-117">**S: hangi API'leri yapmak Office 365 etkinlik günlükleri tooget bilgilerini kullanmak?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="e8fed-118">**Y:** kullanım hello Office 365 Yönetim API'leri tooaccess hello [Office 365 etkinlik günlükleri bir API aracılığıyla](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="e8fed-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="e8fed-119">**S: kaç kayıt Azure portalından karşıdan yükleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="e8fed-120">**Y:** hello Azure portal too120K kayıtları yukarı indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8fed-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="e8fed-121">Merhaba kayıtları tarafından sıralanır *en son* ve varsayılan olarak, en son 120 K hello kayıtları alın.</span><span class="sxs-lookup"><span data-stu-id="e8fed-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="e8fed-122">**S: kaç kayıt ı hello etkinlikleri API sorgulama yapabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="e8fed-123">**Y:** too1 milyon kayıtlarını sorgulama yapabilirsiniz (çoğu tarafından hello kayıt sıralar hello top işleci kullanmazsanız son).</span><span class="sxs-lookup"><span data-stu-id="e8fed-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="e8fed-124">Merhaba "top" işleci kullanırsanız too500K kayıtları sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8fed-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="e8fed-125">Örnek sorgular nasıl toouse hello API burada üzerinde bulabilirsiniz [burada](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8fed-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="e8fed-126">**S: premium lisansı nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="e8fed-127">**Y:** bkz [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md) bir yanıt toothis soru için.</span><span class="sxs-lookup"><span data-stu-id="e8fed-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="e8fed-128">**S: kadar kısa sürede ı etkinlikleri veri premium lisansı aldıktan sonra görmeniz gerekir?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="e8fed-129">**Y:** ücretsiz bir lisans gibi etkinlikler veriler zaten varsa, görebilirsiniz hello aynı veri.</span><span class="sxs-lookup"><span data-stu-id="e8fed-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="e8fed-130">Herhangi bir veri yoksa, bir veya iki gün sürer.</span><span class="sxs-lookup"><span data-stu-id="e8fed-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="e8fed-131">**S: Son ayın verilerini bir Azure AD premium lisansı aldıktan sonra görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="e8fed-132">**Y:** (bir deneme sürümü dahil) tooa Premium sürüm son geçtiyseniz, veri too7 günlerini başlangıçta görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8fed-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="e8fed-133">Veri öğelerden too30 günleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e8fed-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="e8fed-134">**S: bir risk olayı kimlik koruması olmakla birlikte hello karşılık gelen oturum içindeki tüm oturum açma işlemleri görüyorum değil. Bu beklenen bir durumdur?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="e8fed-135">**Y:** Evet, kimlik koruması tüm kimlik doğrulama akışlar için risk olup olmadığını değerlendirir etkileşimli veya etkileşimli olmayan olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8fed-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="e8fed-136">Ancak, tüm oturum açma işlemleri yalnızca rapor yalnızca hello etkileşimli oturum açma işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8fed-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="e8fed-137">**S: nasıl hello "İçin risk bayrak eklenen kullanıcılar" rapor Azure portalında karşıdan yükleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="e8fed-138">**Y:** hello seçeneği toodownload *bayrak eklenen kullanıcılar için risk* rapor yakında eklenecek.</span><span class="sxs-lookup"><span data-stu-id="e8fed-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="e8fed-139">**S: neden bir oturum açma veya bir kullanıcı hello Azure portal'ın riskli bayrakla edildi nasıl biliyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="e8fed-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="e8fed-140">**Y:** Premium edition müşteriler risk olaylarını "İçin risk bayrak eklenen kullanıcılar" Merhaba kullanıcı tıklayarak veya "Riskli gerçekleştirilen oturum açma" Merhaba üzerinde tıklatarak temel hello hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e8fed-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="e8fed-141">Ücretsiz ve temel sürümü müşteriler risk olay bilgilerini temel hello toosee hello at-risk kullanıcılar ve oturum açma işlemleri alın.</span><span class="sxs-lookup"><span data-stu-id="e8fed-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="e8fed-142">**S: nasıl IP adreslerini hello oturum açma işlemleri ve riskli oturum açma işlemleri raporu hesaplandığını??**</span><span class="sxs-lookup"><span data-stu-id="e8fed-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="e8fed-143">**Y:** IP adresleri, bir IP adresi ve hello bilgisayarın adresine sahip fiziksel olarak bulunduğu arasında kesin bağlantı yoktur şekilde yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="e8fed-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="e8fed-144">Bu etkenler mobil sağlayıcıları ve hello istemci aygıt gerçekte kullanıldığı gölgeden uzak IP adresleri merkezi havuzlarından genellikle çok veren VPN gibi karmaşık.</span><span class="sxs-lookup"><span data-stu-id="e8fed-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="e8fed-145">IP adresi tooa fiziksel konum dönüştürme Hello yukarıdaki verildiğinde, izlemeleri, kayıt defteri verilerini, geriye doğru arama ve diğer bilgilere göre en iyi çaba olur.</span><span class="sxs-lookup"><span data-stu-id="e8fed-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
