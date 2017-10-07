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
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Tooget AppSource Azure Active Directory için sertifikalı nasıl
[Microsoft AppSource](https://appsource.microsoft.com/) bir hedef iş kullanıcıları toodiscover için deneyin ve iş kolu satır SaaS uygulamaları (tek başına SaaS ve eklentinin tooexisting Microsoft SaaS ürünlerinde) yönetin.

tek başına bir SaaS uygulaması AppSource üzerinde toolist, uygulamanızı bir çoklu oturum açma herhangi bir şirket veya Azure Active Directory sahip kuruluş iş hesaplarından kabul etmeniz gerekir. Merhaba oturum açma işlemini hello kullanmalıdır [Openıd Connect](./active-directory-protocols-openid-connect-code.md) veya [OAuth 2.0](./active-directory-protocols-oauth-code.md) protokoller. SAML tümleştirme AppSource sertifika için kabul edilmedi.

## <a name="guides-and-code-samples"></a>Kılavuzlar ve kod örnekleri
Toointegrate Open ID kullanarak Azure Active Directory ile uygulamanızı nasıl bağlanacağını hakkında toolearn istiyorsanız, kılavuzlarımız izleyin ve kod örnekleri hello [Azure Active Directory Geliştirici Kılavuzu](./active-directory-developers-guide.md#get-started "ile çalışmaya başlama Geliştiriciler için Azure AD").

## <a name="multi-tenant-applications"></a>Çok kiracılı uygulamalar

Oturum açma işlemleri ayrı örneği, yapılandırma veya dağıtım gerek kalmadan Azure Active Directory sahip kullanıcıların herhangi bir şirket veya kuruluş kabul eden bir uygulama olarak bilinen bir *çok kiracılı uygulama*. AppSource önerir uygulamalarını çoklu kiracı tooenable hello uygulamak *tek tıklamayla* ücretsiz deneme sürümü deneyimi.

Sipariş tooenable çoklu kiralama ile uygulamanızın üzerinde:
- Ayarlama `Multi-Tenanted` özelliği çok`Yes` hello içindeki uygulama kaydı ait bilgileri [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (varsayılan olarak hello Azure Portal'da oluşturulan uygulamaların yapılandırılmış *tek Kiracı*)
- Kod toosend istekleri toohello Güncelleştir '`common`' uç noktası (Merhaba uç noktasından güncelleştirme *https://login.microsoftonline.com/ {yourtenant}* çok*https://login.microsoftonline.com/common*)
- ASP.NET gibi bazı platformlar için tooupdate kodu tooaccept etmeniz birden çok verenler

Çoklu kiracı hakkında daha fazla bilgi için bkz: [nasıl tüm Azure Active Directory (AD) kullanıcı kullanarak toosign hello çok kiracılı uygulama düzeni](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Tek Kiracı uygulamaları
Yalnızca oturum açma işlemleri tanımlı bir Azure Active Directory örneğinin kullanıcılardan kabul uygulamaları olarak bilinen *tek kiracılı uygulama*. Dış kullanıcılar (diğer kuruluşlardan iş veya Okul hesapları veya kişisel hesap dahil) her bir kullanıcı olarak ekledikten sonra tooa tek Kiracı uygulamada oturum açabilir *Konuk hesabı* toohello Azure Active Directory örneği Merhaba uygulama kaydedilir. Konuk hesapları tooan Azure Active Directory hello aracılığıyla olarak kullanıcıları ekleyebilirsiniz [ *Azure AD B2B işbirliği* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - ve yapılabilir [programlı şekilde](../active-directory-b2b-code-samples.md). Konuk hesabı tooan Azure Active Directory kullanıcı eklediğinizde, hello davet e-posta hello bağlantıya tıklayarak tooaccept hello davet sahip toohello kullanıcı, bir davet e-posta gönderilir. Tooan ek kullanıcı aynı zamanda hello ortağı kuruluştaki bir üyesi olan bir davet kuruluş içinde gönderilen davetleri gerekli tooaccept bir davet toosign ' dir.

Tek kiracılı uygulamalara hello etkinleştirebilir *kişi benim* deneyimi, ancak bu, uygulamanızın üzerinde çoklu kiracı AppSource önerdiği tooenable hello tek tıklamayla / ücretsiz deneme sürümü deneyimi istiyorsanız, bunun yerine etkinleştirin.


## <a name="appsource-trial-experiences"></a>AppSource deneme deneyimleri

### <a name="free-trial-customer-led-trial-experience"></a>Ücretsiz deneme (deneme sürümü deneyimi müşteri öncülük) 
Merhaba *müşteri öncülük deneme* tek tıklamayla erişim tooyour uygulama sunar oldukça AppSource önerir hello deneyimidir. Nasıl bir çizimi bu deneyim şuna benzer:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>Kullanıcı uygulamanızı AppSource Web sitesini bulur.</li><li>'Ücretsiz deneme sürümü' seçeneğini belirler</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>Kullanıcı tooa URL'si, web sitenizdeki AppSource yönlendirir</li><li>Merhaba, web sitesini başlatır <i>çoklu oturum açma</i> işlem otomatik olarak (üzerinde sayfa yükleme)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Kullanıcı oturum açma yeniden yönlendirilen tooMicrosoft sayfasıdır</li><li>Kullanıcı kimlik bilgilerini toosign sağlar</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>Kullanıcı, uygulamanız için izin verir</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Oturum açma işlemi tamamlandıktan ve kullanıcı yeniden yönlendirilen geri tooyour web sitesidir</li><li>Kullanıcı hello ücretsiz deneme başlatır</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Bana (deneme sürümü deneyimi iş ortağı öncülük) başvurun
Merhaba *ortak deneme sürümü deneyimi* el ile veya uzun vadeli bir işlem toohappen tooprovision hello kullanıcı gerektiğinde kullanılabilir / şirket: tooprovision sanal makineler, veritabanı örnekleri, örneğin, uygulamanız gerekir veya çok zaman toocomplete ele işlemleri. Bu durumda, kullanıcı seçer hello sonra *'İstek deneme'* düğmesine tıklayın ve kullanıcının iletişim bilgilerini hello gönderir form AppSource doldurur. Bu bilgileri alır almaz, sonra hello ortamı sağlamanıza ve nasıl tooaccess deneme sürümü deneyimi hello üzerinde hello yönergeleri toohello kullanıcıya gönder:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>Kullanıcı uygulamanızı AppSource web sitesini bulur.</li><li>'Kişi benim' seçeneğini belirler</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Form kişi bilgilerle doldurur.</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Kullanıcı bilgilerini alma</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Kurulum ortamı</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Deneme bilgileri ile ilgili kişi kullanıcı</td>
        </tr>
        </table><br/><br/>
        <ul><li>Kullanıcının bilgileri ve Kurulum deneme örnek alma</li><li>Uygulama toohello kullanıcı hello köprü tooaccess Gönder</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Uygulama ve tam hello çoklu oturum açma işlemi kullanıcının eriştiği</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>Kullanıcı, uygulamanız için izin verir</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Oturum açma işlemi tamamlandıktan ve kullanıcı yeniden yönlendirilen geri tooyour web sitesidir</li><li>Kullanıcı hello ücretsiz deneme başlatır</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Daha fazla bilgi
Merhaba AppSource deneme sürümü deneyimi hakkında daha fazla bilgi için bkz: [bu videoyu](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Sonraki Adımlar

- Azure Active Directory oturum açma işlemleri destekleyen uygulamalar oluşturma ile ilgili daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 

- Toolist AppSource, SaaS uygulamanızda nasıl Git bkz hakkında bilgi için [AppSource iş ortağı bilgileri](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Destek alın
Azure Active Directory tümleştirme için kullandığımız [yığın taşması](http://stackoverflow.com/questions/tagged/azure-active-directory) hello topluluk tooprovide desteği. 

Yığın taşması sorularınızı ilk isteyin ve birisi sorunuzu önce istedi, varolan sorunları toosee Gözat önerilir. Sorularınızı ve yorumlarınızı ile etiketlenir emin `[azure-active-directory]`.

Açıklamalar bölümüne tooprovide geribildirim aşağıdaki hello kullanın ve daraltın ve içeriği şekil yardımcı olur.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->