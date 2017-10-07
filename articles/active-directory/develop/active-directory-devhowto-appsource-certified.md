---
title: "Azure Active Directory için sertifikalı AppSource aaaHow tooget | Microsoft Docs"
description: "Nasıl tooget AppSource uygulamanızı Azure Active Directory için sertifikalı ayrıntılar."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="c7e47-103">Tooget AppSource Azure Active Directory için sertifikalı nasıl</span><span class="sxs-lookup"><span data-stu-id="c7e47-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="c7e47-104">[Microsoft AppSource](https://appsource.microsoft.com/) bir hedef iş kullanıcıları toodiscover için deneyin ve iş kolu satır SaaS uygulamaları (tek başına SaaS ve eklentinin tooexisting Microsoft SaaS ürünlerinde) yönetin.</span><span class="sxs-lookup"><span data-stu-id="c7e47-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="c7e47-105">tek başına bir SaaS uygulaması AppSource üzerinde toolist, uygulamanızı bir çoklu oturum açma herhangi bir şirket veya Azure Active Directory sahip kuruluş iş hesaplarından kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="c7e47-106">Merhaba oturum açma işlemini hello kullanmalıdır [Openıd Connect](./active-directory-protocols-openid-connect-code.md) veya [OAuth 2.0](./active-directory-protocols-oauth-code.md) protokoller.</span><span class="sxs-lookup"><span data-stu-id="c7e47-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="c7e47-107">SAML tümleştirme AppSource sertifika için kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="c7e47-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="c7e47-108">Kılavuzlar ve kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="c7e47-108">Guides and code samples</span></span>
<span data-ttu-id="c7e47-109">Toointegrate Open ID kullanarak Azure Active Directory ile uygulamanızı nasıl bağlanacağını hakkında toolearn istiyorsanız, kılavuzlarımız izleyin ve kod örnekleri hello [Azure Active Directory Geliştirici Kılavuzu](./active-directory-developers-guide.md#get-started "ile çalışmaya başlama Geliştiriciler için Azure AD").</span><span class="sxs-lookup"><span data-stu-id="c7e47-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="c7e47-110">Çok kiracılı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="c7e47-110">Multi-tenant applications</span></span>

<span data-ttu-id="c7e47-111">Oturum açma işlemleri ayrı örneği, yapılandırma veya dağıtım gerek kalmadan Azure Active Directory sahip kullanıcıların herhangi bir şirket veya kuruluş kabul eden bir uygulama olarak bilinen bir *çok kiracılı uygulama*.</span><span class="sxs-lookup"><span data-stu-id="c7e47-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="c7e47-112">AppSource önerir uygulamalarını çoklu kiracı tooenable hello uygulamak *tek tıklamayla* ücretsiz deneme sürümü deneyimi.</span><span class="sxs-lookup"><span data-stu-id="c7e47-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="c7e47-113">Sipariş tooenable çoklu kiralama ile uygulamanızın üzerinde:</span><span class="sxs-lookup"><span data-stu-id="c7e47-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="c7e47-114">Ayarlama `Multi-Tenanted` özelliği çok`Yes` hello içindeki uygulama kaydı ait bilgileri [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (varsayılan olarak hello Azure Portal'da oluşturulan uygulamaların yapılandırılmış *tek Kiracı*)</span><span class="sxs-lookup"><span data-stu-id="c7e47-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="c7e47-115">Kod toosend istekleri toohello Güncelleştir '`common`' uç noktası (Merhaba uç noktasından güncelleştirme *https://login.microsoftonline.com/ {yourtenant}* çok*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="c7e47-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="c7e47-116">ASP.NET gibi bazı platformlar için tooupdate kodu tooaccept etmeniz birden çok verenler</span><span class="sxs-lookup"><span data-stu-id="c7e47-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="c7e47-117">Çoklu kiracı hakkında daha fazla bilgi için bkz: [nasıl tüm Azure Active Directory (AD) kullanıcı kullanarak toosign hello çok kiracılı uygulama düzeni](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7e47-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="c7e47-118">Tek Kiracı uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c7e47-118">Single-tenant applications</span></span>
<span data-ttu-id="c7e47-119">Yalnızca oturum açma işlemleri tanımlı bir Azure Active Directory örneğinin kullanıcılardan kabul uygulamaları olarak bilinen *tek kiracılı uygulama*.</span><span class="sxs-lookup"><span data-stu-id="c7e47-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="c7e47-120">Dış kullanıcılar (diğer kuruluşlardan iş veya Okul hesapları veya kişisel hesap dahil) her bir kullanıcı olarak ekledikten sonra tooa tek Kiracı uygulamada oturum açabilir *Konuk hesabı* toohello Azure Active Directory örneği Merhaba uygulama kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="c7e47-121">Konuk hesapları tooan Azure Active Directory hello aracılığıyla olarak kullanıcıları ekleyebilirsiniz [ *Azure AD B2B işbirliği* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - ve yapılabilir [programlı şekilde](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c7e47-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="c7e47-122">Konuk hesabı tooan Azure Active Directory kullanıcı eklediğinizde, hello davet e-posta hello bağlantıya tıklayarak tooaccept hello davet sahip toohello kullanıcı, bir davet e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="c7e47-123">Tooan ek kullanıcı aynı zamanda hello ortağı kuruluştaki bir üyesi olan bir davet kuruluş içinde gönderilen davetleri gerekli tooaccept bir davet toosign ' dir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="c7e47-124">Tek kiracılı uygulamalara hello etkinleştirebilir *kişi benim* deneyimi, ancak bu, uygulamanızın üzerinde çoklu kiracı AppSource önerdiği tooenable hello tek tıklamayla / ücretsiz deneme sürümü deneyimi istiyorsanız, bunun yerine etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c7e47-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="c7e47-125">AppSource deneme deneyimleri</span><span class="sxs-lookup"><span data-stu-id="c7e47-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="c7e47-126">Ücretsiz deneme (deneme sürümü deneyimi müşteri öncülük)</span><span class="sxs-lookup"><span data-stu-id="c7e47-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="c7e47-127">Merhaba *müşteri öncülük deneme* tek tıklamayla erişim tooyour uygulama sunar oldukça AppSource önerir hello deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="c7e47-128">Nasıl bir çizimi bu deneyim şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="c7e47-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="c7e47-129">Kullanıcı uygulamanızı AppSource Web sitesini bulur.</span><span class="sxs-lookup"><span data-stu-id="c7e47-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="c7e47-130">'Ücretsiz deneme sürümü' seçeneğini belirler</span><span class="sxs-lookup"><span data-stu-id="c7e47-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="c7e47-131">Kullanıcı tooa URL'si, web sitenizdeki AppSource yönlendirir</span><span class="sxs-lookup"><span data-stu-id="c7e47-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="c7e47-132">Merhaba, web sitesini başlatır <i>çoklu oturum açma</i> işlem otomatik olarak (üzerinde sayfa yükleme)</span><span class="sxs-lookup"><span data-stu-id="c7e47-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="c7e47-133">Kullanıcı oturum açma yeniden yönlendirilen tooMicrosoft sayfasıdır</span><span class="sxs-lookup"><span data-stu-id="c7e47-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="c7e47-134">Kullanıcı kimlik bilgilerini toosign sağlar</span><span class="sxs-lookup"><span data-stu-id="c7e47-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="c7e47-135">Kullanıcı, uygulamanız için izin verir</span><span class="sxs-lookup"><span data-stu-id="c7e47-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="c7e47-136">Oturum açma işlemi tamamlandıktan ve kullanıcı yeniden yönlendirilen geri tooyour web sitesidir</span><span class="sxs-lookup"><span data-stu-id="c7e47-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="c7e47-137">Kullanıcı hello ücretsiz deneme başlatır</span><span class="sxs-lookup"><span data-stu-id="c7e47-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="c7e47-138">Bana (deneme sürümü deneyimi iş ortağı öncülük) başvurun</span><span class="sxs-lookup"><span data-stu-id="c7e47-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="c7e47-139">Merhaba *ortak deneme sürümü deneyimi* el ile veya uzun vadeli bir işlem toohappen tooprovision hello kullanıcı gerektiğinde kullanılabilir / şirket: tooprovision sanal makineler, veritabanı örnekleri, örneğin, uygulamanız gerekir veya çok zaman toocomplete ele işlemleri.</span><span class="sxs-lookup"><span data-stu-id="c7e47-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="c7e47-140">Bu durumda, kullanıcı seçer hello sonra *'İstek deneme'* düğmesine tıklayın ve kullanıcının iletişim bilgilerini hello gönderir form AppSource doldurur.</span><span class="sxs-lookup"><span data-stu-id="c7e47-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="c7e47-141">Bu bilgileri alır almaz, sonra hello ortamı sağlamanıza ve nasıl tooaccess deneme sürümü deneyimi hello üzerinde hello yönergeleri toohello kullanıcıya gönder:</span><span class="sxs-lookup"><span data-stu-id="c7e47-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="c7e47-142">Kullanıcı uygulamanızı AppSource web sitesini bulur.</span><span class="sxs-lookup"><span data-stu-id="c7e47-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="c7e47-143">'Kişi benim' seçeneğini belirler</span><span class="sxs-lookup"><span data-stu-id="c7e47-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="c7e47-144">Form kişi bilgilerle doldurur.</span><span class="sxs-lookup"><span data-stu-id="c7e47-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="c7e47-145">Kullanıcı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="c7e47-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="c7e47-146">Kurulum ortamı</span><span class="sxs-lookup"><span data-stu-id="c7e47-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="c7e47-147">Deneme bilgileri ile ilgili kişi kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c7e47-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="c7e47-148">Kullanıcının bilgileri ve Kurulum deneme örnek alma</span><span class="sxs-lookup"><span data-stu-id="c7e47-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="c7e47-149">Uygulama toohello kullanıcı hello köprü tooaccess Gönder</span><span class="sxs-lookup"><span data-stu-id="c7e47-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="c7e47-150">Uygulama ve tam hello çoklu oturum açma işlemi kullanıcının eriştiği</span><span class="sxs-lookup"><span data-stu-id="c7e47-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="c7e47-151">Kullanıcı, uygulamanız için izin verir</span><span class="sxs-lookup"><span data-stu-id="c7e47-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="c7e47-152">Oturum açma işlemi tamamlandıktan ve kullanıcı yeniden yönlendirilen geri tooyour web sitesidir</span><span class="sxs-lookup"><span data-stu-id="c7e47-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="c7e47-153">Kullanıcı hello ücretsiz deneme başlatır</span><span class="sxs-lookup"><span data-stu-id="c7e47-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="c7e47-154">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="c7e47-154">More information</span></span>
<span data-ttu-id="c7e47-155">Merhaba AppSource deneme sürümü deneyimi hakkında daha fazla bilgi için bkz: [bu videoyu](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="c7e47-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="c7e47-156">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c7e47-156">Next Steps</span></span>

- <span data-ttu-id="c7e47-157">Azure Active Directory oturum açma işlemleri destekleyen uygulamalar oluşturma ile ilgili daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="c7e47-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="c7e47-158">Toolist AppSource, SaaS uygulamanızda nasıl Git bkz hakkında bilgi için [AppSource iş ortağı bilgileri](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="c7e47-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="c7e47-159">Destek alın</span><span class="sxs-lookup"><span data-stu-id="c7e47-159">Get Support</span></span>
<span data-ttu-id="c7e47-160">Azure Active Directory tümleştirme için kullandığımız [yığın taşması](http://stackoverflow.com/questions/tagged/azure-active-directory) hello topluluk tooprovide desteği.</span><span class="sxs-lookup"><span data-stu-id="c7e47-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="c7e47-161">Yığın taşması sorularınızı ilk isteyin ve birisi sorunuzu önce istedi, varolan sorunları toosee Gözat önerilir.</span><span class="sxs-lookup"><span data-stu-id="c7e47-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="c7e47-162">Sorularınızı ve yorumlarınızı ile etiketlenir emin `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="c7e47-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="c7e47-163">Açıklamalar bölümüne tooprovide geribildirim aşağıdaki hello kullanın ve daraltın ve içeriği şekil yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c7e47-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->