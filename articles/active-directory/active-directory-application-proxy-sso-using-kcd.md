---
title: "aaaSingle oturum açma uygulama proxy'si ile | Microsoft Docs"
description: "Nasıl tooprovide çoklu oturum Azure AD uygulama proxy'si kullanarak açma kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Kerberos Kısıtlı temsilci tek oturum açma tooyour uygulamalar için uygulama proxy'si ile uygulama

Şirket içi için çoklu oturum açma sağlayabilir yayımlanan uygulamaları aracılığıyla uygulama proxy'si tümleşik Windows kimlik doğrulaması ile güvenli hale getirilir. Bu uygulama için erişim bir Kerberos anahtarı gerektirir. Uygulama proxy'si Kerberos Kısıtlı temsilci (KCD) toosupport bu uygulamaları kullanır. 

Active Directory tooimpersonate kullanıcıları uygulama proxy'si bağlayıcılar izin vererek tümleşik Windows kimlik doğrulaması (IWA) kullanarak oturum açma tek tooyour uygulamaları etkinleştirebilirsiniz. Merhaba bağlayıcılar şirket adına belirteçleri almak ve bu izni toosend kullanın.

## <a name="how-single-sign-on-with-kcd-works"></a>KCD works ile nasıl çoklu oturum açma
Bir kullanıcı tooaccess IWA kullanan bir şirket içi uygulama çalıştığında bu diyagramda hello akışı açıklanır.

![Microsoft AAD kimlik doğrulaması akışı diyagramı](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. Merhaba kullanıcı uygulama proxy'si aracılığıyla hello URL tooaccess hello şirket içi uygulama girer.
2. Uygulama proxy'si hello isteği tooAzure AD kimlik doğrulama hizmetleri toopreauthenticate yönlendirir. Bu noktada, tüm geçerli kimlik doğrulama ve yetkilendirme ilkeleri, çok faktörlü kimlik doğrulaması gibi Azure AD geçerlidir. Merhaba kullanıcı doğrulanırsa, Azure AD bir belirteç oluşturur ve toohello kullanıcı gönderir.
3. Merhaba kullanıcı hello belirteci tooApplication Proxy geçirir.
4. Uygulama proxy'si hello belirteci doğrular ve kullanıcı asıl adı (UPN) ondan alır hello ve sonra gönderir isteği Merhaba, UPN hello ve dually kimliği doğrulanmış olarak güvenli bir kanal üzerinden hizmet asıl adı (SPN) toohello bağlayıcı hello.
5. Merhaba bağlayıcı hello şirket içi Kerberos Kısıtlı temsilci (KCD) anlaşmasını gerçekleştirir hello kullanıcı tooget Kerberos belirteci toohello uygulama kimliğine bürünmek AD.
6. Active Directory hello uygulama toohello bağlayıcı için hello Kerberos belirteci gönderir.
7. Merhaba bağlayıcı AD'den alınan hello Kerberos belirteci kullanarak hello özgün istek toohello uygulama sunucusu, gönderir.
8. Merhaba uygulaması hello yanıt toohello toohello uygulama proxy'si hizmeti ve son olarak toohello kullanıcı daha sonra döndürülen bağlayıcı gönderir.

## <a name="prerequisites"></a>Ön koşullar
IWA uygulamalar için çoklu oturum açmayı ile çalışmaya başlamadan önce ortamınız ile Merhaba hazır olduğundan emin olun ayarları ve yapılandırmaları aşağıdaki:

* SharePoint Web uygulamaları gibi uygulamalarınızın toouse ayarlanan tümleşik Windows kimlik doğrulaması. Daha fazla bilgi için bkz: [Kerberos kimlik doğrulaması için desteği etkinleştirme](https://technet.microsoft.com/library/dd759186.aspx), veya SharePoint bakın [Plan SharePoint 2013'te Kerberos kimlik doğrulaması için](https://technet.microsoft.com/library/ee806870.aspx).
* Tüm uygulamaların [hizmet asıl adları](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* Merhaba server çalışan hello bağlayıcı ve hello uygulama çalıştıran hello sunucusu olduğundan etki alanına katılmış ve hello parçası aynı etki alanında veya güvenilen etki alanları. Etki alanına katılma ile ilgili daha fazla bilgi için bkz: [bilgisayar tooa etki alanına katılma](https://technet.microsoft.com/library/dd807102.aspx).
* hello sunucu Hello Bağlayıcısı çalıştıran kullanıcılar için erişim tooread hello TokenGroupsGlobalAndUniversal özniteliğine sahiptir. Bu varsayılan ayarı tarafından güvenlik hello ortamı artırma etkilenmiş.

### <a name="configure-active-directory"></a>Active Directory'yi yapılandırma
Hello Active Directory yapılandırması değişir, mı hello uygulama sunucusu ve uygulama ara sunucusu Bağlayıcısı olarak mı bağlı olarak hello aynı etki alanında veya değil.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Bağlayıcı ve uygulama sunucusu Merhaba, aynı etki alanında
1. Active Directory'de çok Git**Araçları** > **kullanıcıları ve Bilgisayarları**.
2. Merhaba bağlayıcısını çalıştıran hello sunucuyu seçin.
3. Sağ tıklatıp **özellikleri** > **temsilci**.
4. Seçin **bu bilgisayara yalnızca temsilci toospecified Hizmetleri için güven**. 
5. Altında **Hizmetleri toowhich bu hesap atanmış kimlik bilgileri sunabileceği** hello SPN hello uygulama sunucusunun kimliğini hello değerini ekleyin. Bu hello uygulama Proxy Bağlayıcısı tooimpersonate kullanıcıların AD içinde hello listesinde tanımlı hello uygulamaları karşı sağlar.

   ![Bağlayıcı SVR özellikleri penceresinin ekran görüntüsü](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Bağlayıcı ve uygulama sunucusu farklı etki alanlarında
1. KDC ile çalışma alanlarında önkoşullarının listesi için bkz: [alanlarında Kerberos Kısıtlı temsilci](https://technet.microsoft.com/library/hh831477.aspx).
2. Kullanım hello `principalsallowedtodelegateto` hello bağlayıcı sunucusu tooenable hello uygulama proxy'si toodelegate hello bağlayıcı sunucusu özelliği. Merhaba uygulama sunucusu `sharepointserviceaccount` ve sunucu için temsilci seçme hello `connectormachineaccount`. Windows 2012 R2 için bir örnek olarak bu kodu kullanabilirsiniz:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount hello SP'ler makine hesabı veya uygulama havuzu Hangi hello SP'ler altında çalışan bir hizmet hesabı olabilir.

## <a name="configure-single-sign-on"></a>Çoklu oturum açmayı yapılandırın 
1. Açıklanan toohello yönergeleri göre uygulamanızı yayımlamak [uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md). Emin tooselect olun **Azure Active Directory** hello olarak **ön kimlik doğrulama yöntemi**.
2. Uygulamanızı hello kurumsal uygulamalar listesinde göründükten sonra onu seçin ve tıklatın **çoklu oturum açma**.
3. Oturum açma Hello tek mod çok ayarlamak**tümleşik Windows kimlik doğrulaması**.  
4. Merhaba girin **iç uygulama SPN** hello uygulama sunucusu. Bu örnekte, yayımlanan uygulamamız için SPN hello http/www.contoso.com ' dir. Bu SPN gereksinimlerini toobe Hizmetleri toowhich hello bağlayıcı hello listesinde atanmış kimlik bilgileri sunabilir. 
5. Merhaba seçin **oturum açma kimlik temsilcisi** hello bağlayıcı toouse, kullanıcılar adına için. Daha fazla bilgi için bkz: [farklı şirket içi ve bulut kimlikleri ile çalışma](#Working-with-different-on-premises-and-cloud-identities)

   ![Gelişmiş uygulama yapılandırması](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Windows olmayan uygulamalar için SSO
Azure AD hello bulutta hello kullanıcı kimliği doğruladığında hello Azure AD uygulama proxy'si Kerberos temsilci akışı başlatır. Şirket içi Hello isteği geldikten sonra hello Azure AD uygulama proxy'si ile etkileşim kurarak hello kullanıcı adına bir Kerberos anahtarı bağlayıcı sorunları yerel Active Directory hello. Başvurulan tooas Kerberos Kısıtlı temsilci (KCD) işlemidir. Hello sonraki aşamasında, bir istek toohello arka uç uygulaması bu Kerberos anahtarı ile gönderilir. Nasıl toosend gibi istekleri tanımlayan çeşitli protokoller vardır. Çoğu Windows olmayan sunucuları üzerinde Azure AD uygulama proxy'si artık desteklenmektedir Negotiate/SPNego bekler.

Kerberos hakkında daha fazla bilgi için bkz: [tüm tooknow Kerberos Kısıtlı temsilci (KCD) hakkında istediğiniz](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Windows olmayan uygulamalar genellikle kullanıcı kullanıcı adlarını veya etki alanı yerine SAM hesap adlarını e-posta adresleri. Bu durum tooyour uygulamaları geçerliyse, bulut kimlikleri tooyour uygulama kimlikleri tooconfigure temsilci hello oturum açma kimlik alanı tooconnect gerekir. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Şirket içi ve bulut kimlikleri ile çalışma
Uygulama proxy'si varsayar kullanıcıların tam olarak sahip hello hello Bulut ve şirket içi aynı kimlik. Merhaba durum bu değilse, hala KCD çoklu oturum açma için kullanabileceğiniz. Yapılandırma bir **oturum açma kimlik temsilcisi** hangi kimlik kullanılmalıdır, çoklu oturum açma gerçekleştirirken her uygulama toospecify için.  

Bu özellik şirket içi ve hello kullanıcılar tooenter farklı kullanıcı adları ve parolalar gerek kalmadan hello bulut tooon içi uygulamalardan kimlikleri toohave SSO bulut birçok kuruluş sağlar. Bu kuruluşların içerir:

* Dahili olarak birden çok etki alanınız (joe@us.contoso.com, joe@eu.contoso.com) ve tek bir etki alanı hello bulutta (joe@contoso.com).
* Dahili yönlendirilebilir olmayan etki alanı adına sahip (joe@contoso.usa) ve yasal bir hello bulutta.
* Etki alanı adları dahili olarak kullanmamanız (CAN)
* İçi farklı diğer adlar kullanın ve hello bulutta. Örneğin, joe-johns@contoso.com vs.joej@contoso.com  

Uygulama proxy'si ile hangi kimlik toouse tooobtain hello Kerberos bileti seçebilirsiniz. Bu ayarı bir uygulamadır. Bu seçeneklerden bazısı e-posta adresi biçimi kabul ediyor musunuz sistemler için uygun olan, başkalarının alternatif oturum açma için tasarlanmıştır.

![Temsilci oturum açma kimlik parametresi ekran görüntüsü](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Temsilci oturum açma kimliği kullanılırsa, hello değer tüm hello etki alanları veya ormanlar, kuruluşunuzda arasında benzersiz olmayabilir. Bu sorunu önlemek için iki kez iki farklı bağlayıcı gruplarını kullanarak bu uygulamaları yayımlayarak. Her uygulama farklı kullanıcı İzleyici olduğundan, bağlayıcılar tooa farklı etki alanına katılabilirsiniz.

### <a name="configure-sso-for-different-identities"></a>SSO için farklı kimlik Yapılandır
1. Azure AD Connect ayarları Hello asıl kimlik hello e-posta adresi (posta) olacak şekilde yapılandırın. Merhaba parçası özelleştirme gibi işlem hello değiştirerek bu yapılır **kullanıcı asıl adı** hello eşitleme ayarları alanındaki. Bu ayarlar, ayrıca nasıl tooOffice365, Windows10 aygıtlar ve bunların kimlik deposu olarak Azure AD kullanan diğer uygulamalar kullanıcılar oturum belirler.  
   ![Kullanıcıların ekran görüntüsü - kullanıcı asıl adı açılan tanımlama](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Merhaba uygulaması için hello uygulama yapılandırma ayarlarında toomodify, select hello istediğiniz **oturum açma kimlik temsilcisi** kullanılan toobe:

   * Kullanıcı asıl adı (örneğin, joe@contoso.com)
   * Diğer kullanıcı asıl adı (örneğin, joed@contoso.local)
   * Kullanıcı asıl adı (örneğin, Can) kullanıcıadı parçası
   * Kullanıcı adı bölümü diğer kullanıcı asıl adı (örneğin, joed)
   * Şirket içi SAM hesap adı (Merhaba etki alanı denetleyicisi yapılandırmasına bağlıdır)

### <a name="troubleshooting-sso-for-different-identities"></a>SSO için farklı kimlik sorunlarını giderme
Merhaba SSO işlemi bir hata varsa, hello bağlayıcı makine olay günlüğü'nde açıklandığı gibi göründüğü [sorun giderme](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Ancak, bu uygulama diğer HTTP yanıtlarını çeşitli yanıtlar karşın bazı durumlarda, hello isteği başarıyla toohello arka uç uygulaması gönderilir. Bu gibi durumlarda sorun giderme hello bağlayıcı makinede hello uygulama proxy'si oturum olay günlüğünde olay numarası 24029 inceleyerek başlamalısınız. temsilci seçme için kullanılan hello kullanıcı kimliği hello Olay Ayrıntıları içinde hello "kullanıcı" alanında görüntülenir. Oturum günlüğü üzerinde tooturn seçin **Göster Analitik ve hata ayıklama günlüklerini** hello Olay Görüntüleyicisi'ni Görünüm menüsünde.

## <a name="next-steps"></a>Sonraki adımlar

* [Nasıl tooconfigure uygulama proxy'si uygulama toouse Kerberos Kısıtlı temsilci](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Uygulama Ara sunucusu ile ilgili sorunları giderme](active-directory-application-proxy-troubleshoot.md)


Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)

