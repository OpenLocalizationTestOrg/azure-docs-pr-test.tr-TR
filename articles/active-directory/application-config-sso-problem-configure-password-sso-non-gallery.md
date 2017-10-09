---
title: "Parola tek oturum açma için Galeri olmayan uygulama yapılandırma aaaProblem | Microsoft Docs"
description: "Parola tek oturum açma için listelenmeyen Özel Galeri olmayan uygulamaları hello Azure AD uygulama galerisinde yapılandırırken Hello ortak sorunları kişiler yüz anlama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e8892-103">Parola tek oturum açma için Galeri olmayan uygulama yapılandırma sorunu</span><span class="sxs-lookup"><span data-stu-id="e8892-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e8892-104">Bu makalede yardımcı toounderstand hello ortak sorunları kişiler yüz yapılandırırken **parola çoklu oturum açma** bir galeri olmayan uygulama ile.</span><span class="sxs-lookup"><span data-stu-id="e8892-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="e8892-105">Nasıl toocapture oturum açma için uygulama alanları</span><span class="sxs-lookup"><span data-stu-id="e8892-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="e8892-106">Oturum açma alan yakalama HTML etkin oturum açma sayfaları için yalnızca desteklenir ve olduğu **için standart olmayan oturum açma sayfaları desteklenmeyen**, Flash, veya diğer HTML etkin olmayan teknolojileri kullananlar ister.</span><span class="sxs-lookup"><span data-stu-id="e8892-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="e8892-107">Özel uygulamalarınız için oturum açma alanları yakalamak için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="e8892-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="e8892-108">Otomatik oturum açma alan yakalama</span><span class="sxs-lookup"><span data-stu-id="e8892-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="e8892-109">Oturum açma el ile alan yakalama</span><span class="sxs-lookup"><span data-stu-id="e8892-109">Manual sign-in field capture</span></span>

<span data-ttu-id="e8892-110">**Otomatik oturum açma alan yakalama** kullanıyorlarsa iyi çoğu HTML etkin oturum açma sayfaları ile çalışır **hello kullanıcı adı ve parola girişi için iyi bilinen DIV kimlikleri** alan.</span><span class="sxs-lookup"><span data-stu-id="e8892-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="e8892-111">Bu çalışır hello değiştirilene hello HTML hello sayfa toofind belirli ölçütlere uyan DIV kimlikleri üzerinde ve parolaları tooit daha sonra yeniden şekilde bu uygulama için bu meta veri kaydetme tarafından yoludur.</span><span class="sxs-lookup"><span data-stu-id="e8892-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="e8892-112">**Oturum açma el ile alan yakalama** uygulama hello hello durumda kullanılabilir **satıcı etiket değil** hello giriş oturum açmak için kullanılan alanları.</span><span class="sxs-lookup"><span data-stu-id="e8892-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="e8892-113">Oturum açma el ile alan yakalama hello durumda hello olduğunda da kullanılabilir **satıcı işler birden çok alan** , otomatik olarak algılanır olamaz.</span><span class="sxs-lookup"><span data-stu-id="e8892-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="e8892-114">Merhaba üzerinde olduğu gibi birçok alan oturum açma sayfası, gibi bu alanların hello sayfasında olduğu bize sürece azure AD için veri depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8892-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="e8892-115">Genel olarak, **otomatik oturum açma alan yakalama çalışmazsa, her zaman çalışırken hello el ile seçeneği öneririz.**</span><span class="sxs-lookup"><span data-stu-id="e8892-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e8892-116">Nasıl tooautomatically yakalama alanları bir uygulama için oturum açma</span><span class="sxs-lookup"><span data-stu-id="e8892-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="e8892-117">tooconfigure **parola tabanlı çoklu oturum açma** kullanarak bir uygulama için **otomatik oturum açma alan yakalama**, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e8892-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="e8892-118">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="e8892-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8892-119">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e8892-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8892-120">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8892-121">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e8892-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8892-122">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e8892-123">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="e8892-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e8892-124">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e8892-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e8892-125">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e8892-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8892-126">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="e8892-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e8892-127">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e8892-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e8892-128">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="e8892-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e8892-129">**Merhaba oturum alanları sağladığınız hello URL'de görünür olduğundan emin olun**.</span><span class="sxs-lookup"><span data-stu-id="e8892-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="e8892-130">Merhaba tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="e8892-131">Bunu, biz otomatik olarak bir kullanıcı adı için bu URL'yi scrape ve parola giriş kutusu ve izin sonra toouse Azure AD toosecurely hello erişim paneli tarayıcı uzantısı kullanarak parolaları toothat uygulaması iletme.</span><span class="sxs-lookup"><span data-stu-id="e8892-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e8892-132">Nasıl toomanually yakalama alanları bir uygulama için oturum açma</span><span class="sxs-lookup"><span data-stu-id="e8892-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="e8892-133">toomanually yakalama oturum alanları hello erişim paneli tarayıcı uzantısı yüklü ilk olmalıdır ve **InPrivate, incognito ya da özel modunda çalışmıyor.**</span><span class="sxs-lookup"><span data-stu-id="e8892-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="e8892-134">tooinstall hello tarayıcı uzantısı, hello adımları hello içinde [nasıl tooinstall hello erişim paneli tarayıcı uzantısı](#i-cannot-manually-detect-sign-in-fields-for-my-application) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e8892-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="e8892-135">tooconfigure **parola tabanlı çoklu oturum açma** kullanarak bir uygulama için **oturum açma el ile alan yakalama**, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e8892-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="e8892-136">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="e8892-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e8892-137">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e8892-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e8892-138">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e8892-139">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e8892-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e8892-140">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e8892-141">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="e8892-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e8892-142">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e8892-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e8892-143">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e8892-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e8892-144">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="e8892-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e8892-145">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e8892-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e8892-146">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="e8892-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e8892-147">**Merhaba oturum alanları sağladığınız hello URL'de görünür olduğundan emin olun**.</span><span class="sxs-lookup"><span data-stu-id="e8892-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="e8892-148">Merhaba tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="e8892-149">Bunu, biz otomatik olarak bir kullanıcı adı için bu URL'yi scrape ve parola giriş kutusu ve izin sonra toouse Azure AD toosecurely hello erişim paneli tarayıcı uzantısı kullanarak parolaları toothat uygulaması iletme.</span><span class="sxs-lookup"><span data-stu-id="e8892-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="e8892-150">Bu başarısız hello durumda cihazı **hello oturum açma modu toouse oturum açma el ile alan yakalama değiştirme** toostep 12 etmeden tarafından.</span><span class="sxs-lookup"><span data-stu-id="e8892-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="e8892-151">tıklatın **yapılandırma &lt;appname&gt; parola çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e8892-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="e8892-152">Select hello **el ile oturum açma alanları algılama** yapılandırma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e8892-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="e8892-153">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8892-153">Click **Ok**.</span></span>

15. <span data-ttu-id="e8892-154">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8892-154">Click **Save**.</span></span>

16. <span data-ttu-id="e8892-155">Merhaba ekranında yönergeleri toouse hello erişim paneli izleyin.</span><span class="sxs-lookup"><span data-stu-id="e8892-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="e8892-156">"Bu URL'de oturum açma alanları bulamadık" hata bakın</span><span class="sxs-lookup"><span data-stu-id="e8892-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="e8892-157">Oturum açma alanlarının otomatik algılama başarısız olduğunda, bu hatayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e8892-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="e8892-158">Bu sorun, deneyin oturum açma el ile alan algılama aşağıdaki hello tarafından adımları hello tooresolve [nasıl toomanually yakalama alanları bir uygulama için oturum açma](#how-to-manually-capture-sign-in-fields-for-an-application) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e8892-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="e8892-159">Bir "çoklu oturum açma oluşturulamıyor toosave yapılandırma" hatası bakın</span><span class="sxs-lookup"><span data-stu-id="e8892-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="e8892-160">Belirli nadir durumlarda, oturum açma hello tek yapılandırmasını güncelleştirme başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8892-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="e8892-161">tooresolve bu deneyin hello tek oturum açma yapılandırması yeniden kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="e8892-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="e8892-162">Bu toofail tutarlı bir şekilde devam ederse, destek olayı açın ve hello toplanan hello bilgilerini [nasıl toosee hello portal bildirim ayrıntılarını](#i-cannot-manually-detect-sign-in-fields-for-my-application) ve [tooget nasıl yardımcı bildirim ayrıntıları tooa göndererek Destek Mühendisi](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) bölümler.</span><span class="sxs-lookup"><span data-stu-id="e8892-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="e8892-163">I el ile oturum alanlarında Uygulamam için algılayamıyor</span><span class="sxs-lookup"><span data-stu-id="e8892-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="e8892-164">El ile algılama çalışmıyor açtığınızda görebilirsiniz hello davranışları bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e8892-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="e8892-165">Merhaba el ile yakalama işlemi toowork görünen ancak yakalanan hello alanları doğru değildi</span><span class="sxs-lookup"><span data-stu-id="e8892-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="e8892-166">Merhaba sağ alanları hello yakalama işlemi gerçekleştirirken vurgulanmış yok</span><span class="sxs-lookup"><span data-stu-id="e8892-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="e8892-167">Merhaba yakalama işlemi bana toohello uygulamanın oturum açma sayfasına beklendiği gibi alır, ancak hiçbir şey olmaz</span><span class="sxs-lookup"><span data-stu-id="e8892-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="e8892-168">El ile yakalama toowork görünür, ancak Kullanıcılarım hello erişim paneli toohello uygulamadan gittiğinizde SSO gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="e8892-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="e8892-169">Bu sorunların karşılaşırsanız hello aşağıdakileri denetleyin:</span><span class="sxs-lookup"><span data-stu-id="e8892-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="e8892-170">Merhaba erişim paneli tarayıcı uzantısı hello en son sürümüne sahip olduğunuzdan emin olun **yüklü** ve **etkin** hello hello adımları izleyerek [nasıl tooinstall hello paneli tarayıcı erişimi Uzantı](#how-to-install-the-access-panel-browser-extension) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e8892-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="e8892-171">Merhaba yakalama işlemi sırasında tarayıcınızda denediğiniz değil emin olun **incognito, InPrivate ya da özel mod**.</span><span class="sxs-lookup"><span data-stu-id="e8892-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e8892-172">Merhaba erişim paneli uzantısı bu modda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e8892-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e8892-173">Kullanıcılarınızın panelinden hello erişim sırasında toohello uygulamada toosign ayarlamadığınızdan emin olun **incognito, InPrivate ya da özel mod**.</span><span class="sxs-lookup"><span data-stu-id="e8892-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e8892-174">Merhaba erişim paneli uzantısı bu modda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e8892-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e8892-175">Merhaba el ile yakalama işlemi yeniden deneyin, hello kırmızı işaretçileri alanlardır hello doğru sağlama.</span><span class="sxs-lookup"><span data-stu-id="e8892-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="e8892-176">Merhaba el ile yakalama işlemi toohang gibi görünüyor veya hello oturum açma sayfası yapmaz (durum 3 yukarıda), her şeyi hello el ile yakalama işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8892-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="e8892-177">Ancak, bu kez basın hello hello işlemi tamamladıktan sonra **F12** tooopen tarayıcınızın Geliştirici konsol düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="e8892-178">Bir kez Merhaba, açık **konsol** ve türü **window.location= "&lt;hello oturum hello uygulama yapılandırırken belirttiğiniz URL'yi girin&gt;"** ve tuşuna basın  **Girin**.</span><span class="sxs-lookup"><span data-stu-id="e8892-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="e8892-179">Bu sayfa zorla hello yakalama işlemi sona erdirmek ve yakalanan hello alanları depolamak yeniden yönlendir.</span><span class="sxs-lookup"><span data-stu-id="e8892-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="e8892-180">Bu yaklaşım hiçbiri sizin için çalışıyorsanız, size yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8892-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="e8892-181">Merhaba ayrıntılarını ne çalıştığınız yanı sıra hello toplanan hello bilgi ile bir destek servis talebi açma [nasıl toosee hello portal bildirim ayrıntılarını](#i-cannot-manually-detect-sign-in-fields-for-my-application) ve [tooget nasıl yardımcı tooa destek bildirim ayrıntıları göndererek mühendislik](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (varsa) bölümler.</span><span class="sxs-lookup"><span data-stu-id="e8892-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="e8892-182">Nasıl tooinstall hello erişim paneli tarayıcı uzantısı</span><span class="sxs-lookup"><span data-stu-id="e8892-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="e8892-183">tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e8892-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="e8892-184">Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.</span><span class="sxs-lookup"><span data-stu-id="e8892-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="e8892-185">Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.</span><span class="sxs-lookup"><span data-stu-id="e8892-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="e8892-186">Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.</span><span class="sxs-lookup"><span data-stu-id="e8892-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="e8892-187">Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8892-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="e8892-188">**Ekleme** hello uzantısı tooyour tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="e8892-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="e8892-189">Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="e8892-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="e8892-190">Bir kez yüklenir, **yeniden** tarayıcı oturumunda.</span><span class="sxs-lookup"><span data-stu-id="e8892-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="e8892-191">Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamalarınızı.</span><span class="sxs-lookup"><span data-stu-id="e8892-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="e8892-192">Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8892-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="e8892-193">Chrome erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="e8892-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="e8892-194">Firefox erişim paneli uzantısı</span><span class="sxs-lookup"><span data-stu-id="e8892-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="e8892-195">Nasıl bir portal bildirim toosee hello ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e8892-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="e8892-196">Merhaba adımları izleyerek herhangi bir portal bildirim hello ayrıntılarını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8892-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="e8892-197">Merhaba tıklatın **bildirimleri** hello sağ üst köşesinde, hello Azure Portal (Merhaba zil) simgesi</span><span class="sxs-lookup"><span data-stu-id="e8892-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="e8892-198">Herhangi bir bildirim seçin bir **hata** durumu (kırmızı (!) sonraki toothem sahip olanlar).</span><span class="sxs-lookup"><span data-stu-id="e8892-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="e8892-199">! DİKKAT] bildirimleri tıklatın olamaz bir **başarılı** veya **sürüyor** durumu.</span><span class="sxs-lookup"><span data-stu-id="e8892-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="e8892-200">Bu açık hello **bildirim ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8892-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="e8892-201">Bu bilgileri kendiniz hello sorun hakkında daha fazla ayrıntı toounderstand kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8892-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="e8892-202">Hala yardıma ihtiyacınız varsa, sorununuzu ile bir destek mühendisi veya hello ürün grubu tooget Yardım ile bu bilgileri de paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="e8892-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="e8892-203">Merhaba tıklatın **kopyalama** **simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="e8892-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="e8892-204">Tooget nasıl yardımcı bildirim ayrıntıları tooa destek mühendisine göndererek</span><span class="sxs-lookup"><span data-stu-id="e8892-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="e8892-205">Paylaştığınız çok önemlidir **tüm ayrıntılar aşağıda listelenen hello** size hızla yardımcı böylece yardıma gereksiniminiz varsa bir destek mühendisine ile.</span><span class="sxs-lookup"><span data-stu-id="e8892-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="e8892-206">Bu yana kolayca yapabilirsiniz **bir ekran görüntüsü alma** veya hello tıklatarak **kopyalama hata simgesi**, hello toohello sağındaki bulundu **kopyalama hatası** textbox.</span><span class="sxs-lookup"><span data-stu-id="e8892-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="e8892-207">Açıklanan bildirim ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e8892-207">Notification Details Explained</span></span>

<span data-ttu-id="e8892-208">Merhaba aşağıdaki daha hangi öğelerin her birini hello bildirim anlamına gelir ve bunların her birini verir örnekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8892-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="e8892-209">Temel bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="e8892-209">Essential Notification Items</span></span>

-   <span data-ttu-id="e8892-210">**Başlık** – hello hello bildirim açıklayıcı bir başlık</span><span class="sxs-lookup"><span data-stu-id="e8892-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="e8892-211">Örnek – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="e8892-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="e8892-212">**Açıklama** – hello ne hello işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8892-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="e8892-213">Örnek – **girilen iç url başka bir uygulama tarafından zaten kullanılıyor**</span><span class="sxs-lookup"><span data-stu-id="e8892-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="e8892-214">**Bildirim kimliği** – hello bildirim hello benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="e8892-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="e8892-215">Örnek – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="e8892-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="e8892-216">**İstemci istek kimliği** – tarayıcınız tarafından yapılan hello belirli bir istek kimliği</span><span class="sxs-lookup"><span data-stu-id="e8892-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="e8892-217">Örnek – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="e8892-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="e8892-218">**Zaman damgası UTC** – sırasında hello bildirim meydana geldiği UTC zaman damgası hello</span><span class="sxs-lookup"><span data-stu-id="e8892-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="e8892-219">Örnek – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="e8892-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="e8892-220">**İç işlem kimliği** – kullanabileceğiniz toolook hello hata bizim sistemlerinde iç kimliği hello</span><span class="sxs-lookup"><span data-stu-id="e8892-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="e8892-221">Örnek – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="e8892-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="e8892-222">**UPN** – hello işlemi gerçekleştiren hello kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e8892-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="e8892-223">Örnek –**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="e8892-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="e8892-224">**Kiracı kimliği** – hello benzersiz kimliği kullanıcı hello hello Kiracı hello işlemi gerçekleştiren bir üyesi.</span><span class="sxs-lookup"><span data-stu-id="e8892-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="e8892-225">Örnek – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="e8892-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="e8892-226">**Kullanıcı nesnesi kimliği** – hello işlemi gerçekleştiren hello kullanıcının benzersiz Kimliğini hello</span><span class="sxs-lookup"><span data-stu-id="e8892-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="e8892-227">Örnek – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="e8892-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="e8892-228">Ayrıntılı bildirim öğeleri</span><span class="sxs-lookup"><span data-stu-id="e8892-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="e8892-229">**Görünen ad** – **(boş olabilir)** hello hatası için ayrıntılı bir görünen ad</span><span class="sxs-lookup"><span data-stu-id="e8892-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="e8892-230">Örnek * – **uygulama proxy ayarları**</span><span class="sxs-lookup"><span data-stu-id="e8892-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="e8892-231">**Durum** – hello hello bildirim özel durumu</span><span class="sxs-lookup"><span data-stu-id="e8892-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="e8892-232">Örnek * – **başarısız oldu**</span><span class="sxs-lookup"><span data-stu-id="e8892-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="e8892-233">**Nesne Kimliği** – **(boş olabilir)** karşı hangi hello işlemi gerçekleştirildiği nesne kimliği hello</span><span class="sxs-lookup"><span data-stu-id="e8892-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="e8892-234">Örnek – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="e8892-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="e8892-235">**Ayrıntılar** – hello ayrıntılı ne hello işlem sonucunda oluşan açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8892-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="e8892-236">Örnek – **iç url 'http://bing.com/', zaten kullanımda olduğundan geçersiz**</span><span class="sxs-lookup"><span data-stu-id="e8892-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="e8892-237">**Kopyalama hatası** – tıklatın hello **Kopyala simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba</span><span class="sxs-lookup"><span data-stu-id="e8892-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="e8892-238">Örnek –```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="e8892-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8892-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8892-239">Next steps</span></span>
[<span data-ttu-id="e8892-240">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="e8892-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

