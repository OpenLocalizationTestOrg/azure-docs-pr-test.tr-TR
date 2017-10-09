---
title: "Azure AD Connect: Bir Active Directory Federasyon Hizmetleri (AD FS) grubu güncelleştirme hello SSL sertifikası | Microsoft Docs"
description: "Bu belge ayrıntıları hello adımları tooupdate hello SSL sertifikasını Azure AD Connect kullanarak AD FS grubunda."
services: active-directory
keywords: "Azure ad connect, adfs ssl güncelleştirme, adfs sertifika güncelleştirme, değişiklik adfs sertifika, yeni adfs sertifika, adfs sertifika ssl sertifikası, güncelleştirme ssl sertifikası adfs, adfs ssl sertifikası, adfs, ssl, sertifika, adfs hizmet iletişimi sertifikasına, güncelleştirme Federasyon yapılandırma, güncelleştirme adfs Federasyon yapılandırma, aad bağlanma"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="b14b2-104">Bir Active Directory Federasyon Hizmetleri (AD FS) grubu için Hello SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b14b2-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="b14b2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b14b2-105">Overview</span></span>
<span data-ttu-id="b14b2-106">Bu makalede, Azure AD Connect tooupdate hello SSL sertifikası bir Active Directory Federasyon Hizmetleri (AD FS) grubu için nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="b14b2-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="b14b2-107">AD FS oturum açma hello kullanıcı yöntemi seçili olmasa bile, başlangıç AD FS grubu için hello Azure AD Connect aracı tooeasily güncelleştirme hello SSL sertifikası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b14b2-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="b14b2-108">Tüm Federasyon ve üç basit adımda Web uygulaması Ara sunucusu (WAP) sunucuları arasında hello AD FS grubu için SSL sertifikası güncelleştirme hello tüm işlem gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b14b2-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Üç adımı](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="b14b2-110">Daha fazla AD FS tarafından kullanılan sertifikalar hakkında toolearn bkz [AD FS tarafından kullanılan sertifikaları anlama](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="b14b2-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b14b2-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b14b2-111">Prerequisites</span></span>

* <span data-ttu-id="b14b2-112">**AD FS grubu**: AD FS grubunuzu tabanlı Windows Server 2012 R2 veya sonrası olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b14b2-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="b14b2-113">**Azure AD Connect**: Bu hello emin olun, Azure AD Connect sürümüdür 1.1.443.0 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b14b2-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="b14b2-114">Merhaba görev kullanacağınız **güncelleştirme AD FS SSL sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="b14b2-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Güncelleştirme SSL görevi](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="b14b2-116">1. adım: AD FS grubu bilgileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="b14b2-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="b14b2-117">Azure AD Connect hello AD FS grubunu tooobtain bilgilerini tarafından otomatik olarak çalışır:</span><span class="sxs-lookup"><span data-stu-id="b14b2-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="b14b2-118">AD FS (Windows Server 2016 veya sonraki) Hello grubu bilgileri sorgulama.</span><span class="sxs-lookup"><span data-stu-id="b14b2-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="b14b2-119">Azure AD Connect ile yerel olarak depolanan önceki çalıştığında, başvuru hello bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b14b2-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="b14b2-120">Merhaba ekleyerek veya kaldırarak hello sunucuları tooreflect hello geçerli yapılandırmasını hello AD FS grubunu görüntülenen sunucularının listesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b14b2-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="b14b2-121">Merhaba sunucu bilgilerini sağlanan hemen Azure AD Connect hello bağlantısı ve geçerli SSL sertifikası durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b14b2-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![AD FS sunucu bilgisi](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="b14b2-123">Merhaba listesi artık hello AD FS grubunun parçası olan bir sunucu içeriyorsa, tıklatın **kaldırmak** , AD FS grubunuzdaki sunucuların hello listeden toodelete hello sunucusu.</span><span class="sxs-lookup"><span data-stu-id="b14b2-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Çevrimdışı sunucu listesinde](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="b14b2-125">Merhaba listesinden bir sunucu kaldırma sunucuların bir AD FS için Azure AD Connect grupta yerel bir işlemdir ve bilgi hello Azure AD Connect yerel olarak tutar AD FS grubu için güncelleştirmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="b14b2-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="b14b2-126">Azure AD Connect, AD FS tooreflect hello değişiklik hello yapılandırmayı değiştirmeniz değil.</span><span class="sxs-lookup"><span data-stu-id="b14b2-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="b14b2-127">2. adım: yeni bir SSL sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="b14b2-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="b14b2-128">AD FS grubu sunucuları hakkında bilgi hello onaylanıp sonra Azure AD Connect hello yeni SSL sertifikası için sorar.</span><span class="sxs-lookup"><span data-stu-id="b14b2-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="b14b2-129">Bir parola korumalı PFX sertifika toocontinue hello yükleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="b14b2-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![SSL sertifikası](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="b14b2-131">Merhaba sertifika verdikten sonra Azure AD Connect Önkoşullar bir dizi aracılığıyla gider.</span><span class="sxs-lookup"><span data-stu-id="b14b2-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="b14b2-132">Sertifika hello hello sertifika tooensure hello AD FS grubu için doğru olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="b14b2-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="b14b2-133">Merhaba hello sertifikanın konu adı/alternatif konu adı, aynı hello Federasyon Hizmeti adı Merhaba, veya joker sertifikadır olur.</span><span class="sxs-lookup"><span data-stu-id="b14b2-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="b14b2-134">Merhaba sertifika 30 günden fazla bir süre için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b14b2-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="b14b2-135">Merhaba sertifika güven zinciri geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="b14b2-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="b14b2-136">Merhaba, parola korumalı sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="b14b2-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="b14b2-137">3. adım: hello güncelleştirme sunucuları seçin</span><span class="sxs-lookup"><span data-stu-id="b14b2-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="b14b2-138">Merhaba sonraki adımda, güncelleştirilmiş toohave hello SSL sertifikasına sahip olmanız hello sunucuları seçin.</span><span class="sxs-lookup"><span data-stu-id="b14b2-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="b14b2-139">Çevrimdışı sunucuları hello güncelleştirmesi seçilemez.</span><span class="sxs-lookup"><span data-stu-id="b14b2-139">Servers that are offline can't be selected for hello update.</span></span>

![Sunucuları tooupdate seçin](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="b14b2-141">Merhaba yapılandırmayı tamamladıktan sonra Azure AD Connect hello güncelleştirme hello durumunu gösterir ve bir seçenek tooverify hello AD FS oturum açma sağlayan hello iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b14b2-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Yapılandırma tamamlandı](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="b14b2-143">SSS</span><span class="sxs-lookup"><span data-stu-id="b14b2-143">FAQs</span></span>

* <span data-ttu-id="b14b2-144">**Ne hello sertifikasının konu adını hello hello yeni AD FS SSL sertifikası için olması gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="b14b2-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="b14b2-145">Azure AD Connect hello sertifikanın konu adı/alternatif konu adı hello hello Federasyon Hizmeti adı içerip içermediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="b14b2-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="b14b2-146">Örneğin, Federasyon Hizmeti adınız fs.contoso.com ise fs.contoso.com hello konu adı/alternatif konu adı olmalıdır.  Joker karakterli sertifikalar da kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b14b2-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="b14b2-147">**Neden kimlik bilgilerini hello WAP sunucusu sayfasında yeniden soruluyor?**</span><span class="sxs-lookup"><span data-stu-id="b14b2-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="b14b2-148">TooAD FS sunucularına bağlanmak için sağladığınız hello kimlik bilgilerini de hello ayrıcalık toomanage hello WAP sunucuları yoksa, Azure AD Connect hello WAP sunucularında yönetici ayrıcalıklarına sahip kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="b14b2-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="b14b2-149">**Merhaba sunucu çevrimdışı olarak gösterilir. Ne yapmalıyım?**</span><span class="sxs-lookup"><span data-stu-id="b14b2-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="b14b2-150">Merhaba sunucu çevrimdışıysa azure AD Connect hiçbir işlem gerçekleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b14b2-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="b14b2-151">Merhaba sunucusu hello AD FS grubunu parçası ise, hello bağlantı toohello sunucu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b14b2-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="b14b2-152">Merhaba sorunun giderilmiş sonra hello Yenile simgesine tooupdate hello durum hello Sihirbazı'nda tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b14b2-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="b14b2-153">Merhaba bölümü sunucusuysa Merhaba grubu daha önce ancak şimdi artık var, tıklatın **kaldırmak** toodelete, Azure AD Connect sunucuları hello listesinden korur.</span><span class="sxs-lookup"><span data-stu-id="b14b2-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="b14b2-154">Azure AD Connect hello listesinden kaldırmayı hello sunucu hello AD FS yapılandırmasını kendisini değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="b14b2-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="b14b2-155">AD FS Windows Server 2016 veya sonraki sürümlerde, hello sunucu kalır hello yapılandırma ayarlarında kullanıyorsanız ve gösterilecek yeniden hello sonraki kez hello görev çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="b14b2-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="b14b2-156">**Merhaba yeni SSL sertifikası ile bir alt grup Sunucularım kümesini güncelleştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b14b2-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="b14b2-157">Evet.</span><span class="sxs-lookup"><span data-stu-id="b14b2-157">Yes.</span></span> <span data-ttu-id="b14b2-158">Merhaba görev her zaman çalıştırabilirsiniz **SSL sertifikasını Güncelleştir** yeniden sunucuları kalan tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="b14b2-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="b14b2-159">Merhaba üzerinde **Select sunucuları için SSL sertifika güncelleştirme** sayfasında, üzerinde hello sunucularının listesini sıralayabilirsiniz **SSL sona erme tarihi** henüz güncelleştirilmemiş tooeasily erişim hello sunucuları.</span><span class="sxs-lookup"><span data-stu-id="b14b2-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="b14b2-160">**Merhaba Server'da çalıştırmak hello önceki kaldırıldı, ancak bunu hala çevrimdışı ve listelenen olarak hello AD FS sunucuları sayfasında gösteriliyor. Neden kaldırdım bile sonra hello çevrimdışı sunucu hala var mı?**</span><span class="sxs-lookup"><span data-stu-id="b14b2-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="b14b2-161">Azure AD Connect hello listesinden kaldırmayı hello sunucu hello AD FS yapılandırmasını kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="b14b2-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="b14b2-162">Azure AD Connect hello grubu hakkındaki tüm bilgileri için AD FS (Windows Server 2016 veya daha yüksek) başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="b14b2-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="b14b2-163">Merhaba sunucu hello AD FS yapılandırmasını hala varsa, geri hello listesinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="b14b2-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b14b2-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b14b2-164">Next steps</span></span>

- [<span data-ttu-id="b14b2-165">Azure AD Connect ve federasyon</span><span class="sxs-lookup"><span data-stu-id="b14b2-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="b14b2-166">Active Directory Federasyon Hizmetleri Yönetimi ve Azure AD Connect ile özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b14b2-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
