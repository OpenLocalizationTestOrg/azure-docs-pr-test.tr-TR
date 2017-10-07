---
title: "aaaHow toouse hello Azure Active Directory Power BI İçerik Paketi | Microsoft Docs"
description: "Nasıl toouse hello Azure Active Directory Power BI içerik paketi öğrenin"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="8b982-103">Nasıl toouse hello Azure Active Directory Power BI İçerik Paketi</span><span class="sxs-lookup"><span data-stu-id="8b982-103">How toouse hello Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="8b982-104">Kullanıcılarınızın Azure Active Directory özelliklerini benimseme ve kullanma şekli BT yöneticileri için çok önemlidir. BT altyapısı ve iletişim tooincrease kullanım ve tooget AAD özellikleri dışında en hello tooplan sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b982-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin. It allows you tooplan your IT infrastructure and communication tooincrease usage and tooget hello most out of AAD features.</span></span> <span data-ttu-id="8b982-105">Power BI içerik paketi Azure Active Directory özelliği toofurther hello verir nasıl kullanabileceğiniz hello kendi Azure Active Directory ile neler olup bittiğini içine bu verileri toogather daha zengin Öngörüler, veri toounderstand çözümlemek için çeşitli özellikleri, yoğun olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b982-105">Power BI Content Pack for Azure Active Directory gives you hello ability toofurther analyze your data toounderstand how you can use this data toogather richer insights into what’s going on with their Azure Active Directory for hello various capabilities you heavily rely on.</span></span>  <span data-ttu-id="8b982-106">Hello Azure Active Directory API'leri ile tümleştirme Power bı'da, kolayca hello önceden oluşturulmuş içerik paketleri indirin ve Azure Active Power BI sunar zengin görselleştirme deneyimi kullanarak dizininizde tooall hello etkinlikleri serisidir.</span><span class="sxs-lookup"><span data-stu-id="8b982-106">With hello integration of Azure Active Directory APIs into Power BI, you can easily download hello pre-built content packs and gain insights tooall hello activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="8b982-107">Kendi panonuzu oluşturabilir ve kuruluşunuzdaki herkesle kolayca paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-107">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="8b982-108">Bu konu size adım adım yönergeler nasıl içerik tooinstall ve kullanım hello ortamınızda paketi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b982-108">This topic provides you with step-by-step instructions on how tooinstall and use hello content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="8b982-109">Yükleme</span><span class="sxs-lookup"><span data-stu-id="8b982-109">Installation</span></span>  

<span data-ttu-id="8b982-110">**tooinstall hello Power BI içerik paketi:**</span><span class="sxs-lookup"><span data-stu-id="8b982-110">**tooinstall hello Power BI Content Pack:**</span></span>

1. <span data-ttu-id="8b982-111">İçine oturum [Power BI](https://app.powerbi.com/groups/me/getdata/services) Power BI hesabınızla (Merhaba budur, O365 veya Azure AD hesabınızla aynı hesabı).</span><span class="sxs-lookup"><span data-stu-id="8b982-111">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is hello same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="8b982-112">Merhaba sol gezinti bölmesinin Hello altında seçin **Veri Al**.</span><span class="sxs-lookup"><span data-stu-id="8b982-112">At hello bottom of hello left navigation pane, select **Get Data**.</span></span>

    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="8b982-114">Merhaba, **Hizmetleri** kutusunda, **almak**.</span><span class="sxs-lookup"><span data-stu-id="8b982-114">In hello **Services** box, click **Get**.</span></span>
   
    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="8b982-116">**Azure Active Directory** aratın.</span><span class="sxs-lookup"><span data-stu-id="8b982-116">Search for **Azure Active Directory**.</span></span>

    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="8b982-118">İstendiğinde Azure AD Kiracı Kimliğinizi girin ve **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-118">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="8b982-119">Office 365 / Azure AD kiracınız için hızlı şekilde tooget hello Kiracı kimliği toologin toohello Azure AD portalı olduğunda, ayrıntıya toohello dizin ve URL aşağıdaki hello hello Kimliğini kopyalayın: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="8b982-119">A quick way tooget hello Tenant Id for your Office 365 / Azure AD tenant is toologin toohello Azure AD Portal, drill down toohello directory and copy hello ID from hello following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="8b982-121">**Oturum aç**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-121">Click **Sign-in**.</span></span> 
 
    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="8b982-123">Kullanıcı adınızı ve parolanızı girip **Oturum aç**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-123">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="8b982-125">Merhaba uygulama onay iletişim kutusunda tıklatın **kabul**.</span><span class="sxs-lookup"><span data-stu-id="8b982-125">On hello app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="8b982-126">Azure Active Directory Etkinlik günlükleri panonuz oluşturulduğunda üzerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-126">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="8b982-128">Bu içerik paketiyle ne yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="8b982-128">What can I do with this content pack?</span></span>

<span data-ttu-id="8b982-129">Bu içerik paketi ile neler yapabileceğinizi içine atlama önce hello hızlı önizlemesini burada'nın çeşitli raporlar hello içerik paketi.</span><span class="sxs-lookup"><span data-stu-id="8b982-129">Before we jump into what you can do with this content pack, here’s quick preview of hello various reports in hello content pack.</span></span> <span data-ttu-id="8b982-130">Rapor verileri gider geri toohello **son 30 gün**.</span><span class="sxs-lookup"><span data-stu-id="8b982-130">Report data goes back toohello **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="8b982-131">Bu Azure Active Directory günlükleri İçerik Paketi sürümünde yer alan raporlar</span><span class="sxs-lookup"><span data-stu-id="8b982-131">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="8b982-132">**Uygulama kullanımı ve eğilimi raporu**: kullanılan hello uygulamaları Öngörüler alın, kuruluşunuz ve hangilerinin kullanıldığını en hello ve ne zaman.</span><span class="sxs-lookup"><span data-stu-id="8b982-132">**App Usage and Trend report**:  Get insights into hello apps used in your organization and which ones are being used hello most and when.</span></span> <span data-ttu-id="8b982-133">Bu rapor toogather Öngörüler kuruluşunuzdaki son toplu bir uygulamanın nasıl kullanıldığını içine veya hangi uygulamaların popüler olduğunu bulmak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-133">You can use this report toogather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="8b982-134">Bunu yaparak, hello uygulama değil kullanılıp kullanılmadığını görürseniz kullanımını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="8b982-134">By doing this, you can improve usage if you see if hello app is not being used.</span></span>

<span data-ttu-id="8b982-135">**Oturum açma işlemleri konumu ve kullanıcılar tarafından**: tüm hello gerçekleştirilen oturum açma Azure kimlik ve hello hello kullanıcıların kimliğini verir Öngörüler kullanılarak gerçekleştirilen Öngörüler alın.</span><span class="sxs-lookup"><span data-stu-id="8b982-135">**Sign-ins by location and users**: Get insights into all hello sign-ins performed using Azure Identity and gives insights into hello identity of hello users.</span></span> <span data-ttu-id="8b982-136">Bu bilgiyle oturum açma işlemleri hakkında ayrıntılı bilgilere ulaşabilir ve şu soruların yanıtlarını bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b982-136">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="8b982-137">Bu kullanıcı en çok nereden oturum açmış?</span><span class="sxs-lookup"><span data-stu-id="8b982-137">From where did this user sign-ins?</span></span>
- <span data-ttu-id="8b982-138">Kullanıcı oturum açmaları hello olan ve burada bunlar oturum gelen açma?</span><span class="sxs-lookup"><span data-stu-id="8b982-138">Which user has hello most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="8b982-139">Merhaba oturum açma başarılı oldu mu?</span><span class="sxs-lookup"><span data-stu-id="8b982-139">Was hello sign-in successful?</span></span>  
 
<span data-ttu-id="8b982-140">Belirli bir tarihe veya konuma tıklayarak ayrıntılara ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-140">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="8b982-141">**Uygulama başına benzersiz kullanıcı sayısı**: Belirli bir uygulamayı kullanan tüm benzersiz kullanıcıları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8b982-141">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="8b982-142">Buna yalnızca uygulamada “*başarıyla*” oturum açmış kullanıcılar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="8b982-142">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="8b982-143">**Cihaz oturum açma işlemleri**: işletim sistemi hello türü bir görünümünü elde ve tarayıcılar dahil olmak üzere hello kullanıcılar hakkında ayrıntılı bilgi, kuruluşunuzdaki kullanıcılar tarafından kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8b982-143">**Device sign-ins**: Get a view of hello type of OS and browsers are being used by users in your organization with detailed information on hello users including:</span></span>

- <span data-ttu-id="8b982-144">User Name</span><span class="sxs-lookup"><span data-stu-id="8b982-144">User Name</span></span>
- <span data-ttu-id="8b982-145">IP Adresi</span><span class="sxs-lookup"><span data-stu-id="8b982-145">IP Address</span></span>
- <span data-ttu-id="8b982-146">Konum</span><span class="sxs-lookup"><span data-stu-id="8b982-146">Location</span></span> 
- <span data-ttu-id="8b982-147">Oturum açma durumu</span><span class="sxs-lookup"><span data-stu-id="8b982-147">Sign-in status</span></span> 

<span data-ttu-id="8b982-148">Bu raporla çeşitli aygıt profilleri kuruluşunuzda kullanılan ve cihaz ilkelerini ne kullanıldığına göre belirlemek hello anlama</span><span class="sxs-lookup"><span data-stu-id="8b982-148">With this report, you can understand hello various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="8b982-149">**SSPR Hunisi**: Kuruluşunuzda parola sıfırlama işlemlerinin nasıl gerçekleştirildiğini kavrayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-149">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="8b982-150">Kaç tane parola sıfırlama hello SSPR aracı kullanılarak denendi göz almak ve kaç tanesinin başarılı.</span><span class="sxs-lookup"><span data-stu-id="8b982-150">Get a peek into how many password resets were attempted through hello SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="8b982-151">Merhaba SSPR Huni kullanarak hello parola sıfırlama hata derinliklerine ve neden belirli hataları oluştu anlayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-151">Dig deeper into hello Password resets failure using hello SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="8b982-152">Bu rapor hello doğru kararlar olabilmeniz hello SSPR aracı kuruluşunuz içinde nasıl kullanıldığını, daha derin bir anlayış verir.</span><span class="sxs-lookup"><span data-stu-id="8b982-152">This report gives a deeper understanding of how hello SSPR tool is used within your organization so you can make hello right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="8b982-153">Azure AD Etkinlik içerik paketini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8b982-153">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="8b982-154">**Görselleştirme değiştirme**: tıklatarak raporu görselleştirme değiştirebilirsiniz **Raporu Düzenle** ve istediğiniz hello görselleştirme seçin.</span><span class="sxs-lookup"><span data-stu-id="8b982-154">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select hello visualization you want.</span></span>
 
![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="8b982-157">**Ek alanlar**: alan toohello rapor eklemek veya hello visual toowhich tooadd/Kaldır hello alan istediğiniz seçerek kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8b982-157">**Include additional fields**:  You can add a field toohello report or remove it by selecting hello visual toowhich you want tooadd/remove hello field.</span></span> <span data-ttu-id="8b982-158">Merhaba aşağıdaki örnekte, I "oturum açma durumu" alan toohello Tablo görünümü ekleme.</span><span class="sxs-lookup"><span data-stu-id="8b982-158">In hello example below, I am adding “sign-in status” field toohello table view.</span></span> 
 
![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="8b982-160">**PIN görselleştirmeleri tooyour Pano**: panonuzu özelleştirebilir ve kendi görselleştirmeleri toohello raporunuzu içerir ve toohello Pano sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="8b982-160">**Pin visualizations tooyour dashboard**:  You can customize your dashboard and include your own visualizations toohello report and pin it toohello dashboard.</span></span> <span data-ttu-id="8b982-161">Örnekte hello aşağıdaki t "oturum açma durumu" adlı yeni bir filtre eklenebilir ve hello rapora dahil.</span><span class="sxs-lookup"><span data-stu-id="8b982-161">In hello example below, I added a new filter called “Sign-in Status” and included it in hello report.</span></span> <span data-ttu-id="8b982-162">I ayrıca hello görselleştirme çubuk grafik tooa satır grafikten değişti ve bu yeni bir görsel toohello Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-162">I also changed hello visualization from bar chart tooa line chart and can pin this new visual toohello dashboard.</span></span>

![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="8b982-165">**Pano paylaşımı**: hello içeriği oluşturduktan sonra kuruluşunuzdaki hello Pano hello kullanıcılarıyla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-165">**Sharing your dashboard**: Once you have created hello content you want, you can share hello dashboard with hello users in your organization.</span></span> <span data-ttu-id="8b982-166">Merhaba raporu paylaşmak sonra bunlar hello raporda seçtiğiniz hello alanlar görebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-166">Please remember that once you share hello report, they can see hello fields you have selected in hello report.</span></span>
 
![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="8b982-168">Power BI raporunuzun her gün yenilenmesini planlama</span><span class="sxs-lookup"><span data-stu-id="8b982-168">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="8b982-169">tooschedule, Power BI raporu günlük yenileme Git çok**veri kümeleri > Ayarlar > Yenileme zamanlaması** ve aşağıda gösterilen şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-169">tooschedule a daily refresh of your Power BI report, go too**Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a><span data-ttu-id="8b982-171">İçerik Paketi toonewer sürümü güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="8b982-171">Updating toonewer version of content pack</span></span>

<span data-ttu-id="8b982-172">Tooupdate istiyorsanız, içerik daha yeni bir sürüm tooget paketi:</span><span class="sxs-lookup"><span data-stu-id="8b982-172">If you want tooupdate your content pack tooget a newer version:</span></span>

- <span data-ttu-id="8b982-173">Merhaba yeni içerik paketini karşıdan yüklemek ve bu makalede listelenen yönergeleri uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8b982-173">Download hello new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="8b982-174">Kurduktan sonra çok Git**veri kaynağı > ayarları > veri kaynağı kimlik bilgileri** ve aşağıda gösterildiği gibi kimlik bilgilerinizi yeniden girin</span><span class="sxs-lookup"><span data-stu-id="8b982-174">Once you have set it up, go too**Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Azure Active Directory Power BI İçerik Paketi](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="8b982-176">Merhaba içerik paketinin yeni sürümü Hello çalışma hemen hello temel alınan raporları ve bu içerik paketiyle ilişkili veri kümeleri silerek gerekirse hello eski sürümünü kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b982-176">As soon as hello new version of hello content pack is working, you can remove hello old version if needed by deleting hello underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="8b982-177">Sorun yaşamaya devam mı ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="8b982-177">Still having issues?</span></span> 

<span data-ttu-id="8b982-178">[Sorun giderme kılavuzumuzu](active-directory-reporting-troubleshoot-content-pack.md) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="8b982-178">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="8b982-179">Power BI hakkında genel yardım için bu [yardım makalelerini inceleyin](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="8b982-179">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="8b982-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b982-180">Next steps</span></span>

<span data-ttu-id="8b982-181">Merhaba raporlama genel bakış için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8b982-181">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
