---
title: "Azure Active Directory'de önceden tümleştirilen uygulamalar için hello SAML belirtecinde verilen aaaCustomizing talepler | Microsoft Docs"
description: "Nasıl toocustomize hello talep hello Azure Active Directory'de önceden tümleştirilen uygulamalar için SAML belirtecinde verilen bilgi edinin"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Hello Azure Active Directory'de önceden tümleştirilen uygulamalar için SAML belirtecinde verilen talepler özelleştiriliyor
Azure Active Directory önceden tümleştirilmiş binlerce uygulamasına hello Azure AD uygulama galerisinde üzerinde çoklu oturum açma desteği 360 dahil olmak üzere, bugün destekler hello SAML 2.0 protokolü kullanarak. Kullanıcının SAML kullanarak Azure AD üzerinden tooan uygulama doğruladığında, Azure AD belirteci toohello uygulamayı (aracılığıyla bir HTTP POST) gönderir. Ve daha sonra Merhaba uygulaması doğrular ve bir kullanıcı adı ve parola istemek yerine hello belirteci toolog hello kullanıcı kullanır. Bu SAML belirteçleri "talep" olarak bilinen hello kullanıcı hakkında bilgi içerir.

İçinde kimlik-seslendir, "talep" bir kimlik sağlayıcısı bildiren bir kullanıcı bu kullanıcı için sorun hello belirteci içinde hakkında bilgi. İçinde [SAML belirteci](http://en.wikipedia.org/wiki/SAML_2.0), bu veri genellikle hello SAML özniteliği deyimi içeriyor. Merhaba kullanıcının benzersiz Kimliğini genellikle SAML konu adı tanımlayıcı olarak da bilinen hello gösterilir.

Varsayılan olarak, Azure Active Directory NameIdentifier talep, Azure AD'de hello kullanıcının kullanıcı adı (AKA kullanıcı asıl adı) değerini içeren bir SAML belirteci tooyour uygulaması verir. Bu değer hello kullanıcı benzersiz şekilde tanımlayabilir. Merhaba SAML belirteci hello kullanıcının e-posta adresi, ilk ad ve Soyadı içeren ek talepleri de içerir.

tooview veya düzenleme hello talep hello SAML belirteci toohello uygulama açık hello Azure portalında verdi. Merhaba seçin **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** hello onay kutusu **kullanıcı öznitelikleri** hello uygulama bölümü.

![Kullanıcı öznitelikleri bölümü][1]

Merhaba SAML belirtecinde verilen tooedit hello talepler neden gerekebilecek iki olası nedeni vardır:
* Merhaba uygulaması farklı bir talep URI'ler ayarlayın veya talep değerleri toorequire yazıldı.
* Merhaba uygulaması, Azure Active Directory'de depolanan bir şey hello kullanıcı adı (AKA kullanıcı asıl adı) dışında hello NameIdentifier talep toobe gerektiren bir şekilde dağıtıldı.

Merhaba varsayılan talep değerleri düzenleyebilirsiniz. Merhaba talep satır hello SAML belirteci öznitelikleri tablosunda seçin. Merhaba açılır **öznitelik Düzenle** bölüm ve daha sonra talep adını, değeri ve hello taleple ilişkili ad alanı düzenleyebilirsiniz.

![Kullanıcı özniteliği Düzenle][2]

Merhaba üzerinde tıklayarak açar hello bağlam menüsünü kullanarak talep (dışında NameIdentifier) da kaldırabilirsiniz **...**  simgesi.  Yeni talepleri hello kullanarak da ekleyebilirsiniz **Ekle özniteliği** düğmesi.

![Kullanıcı özniteliği Düzenle][3]

## <a name="editing-hello-nameidentifier-claim"></a>Merhaba NameIdentifier talep düzenleme
Burada Merhaba uygulaması dağıtılan toosolve hello sorunu farklı bir kullanıcı adı kullanarak hello üzerinde tıklatın **kullanıcı tanımlayıcısı** hello açılan **kullanıcı öznitelikleri** bölümü. Bu eylem bir iletişim kutusu birkaç farklı seçeneklerle sağlar:

![Kullanıcı özniteliği Düzenle][4]

Hello açılır, seçin **user.mail** tooset hello NameIdentifier talep hello dizinindeki toobe hello kullanıcının e-posta adresi. Ya da seçin **user.onpremisessamaccountname** tooset toohello kullanıcının SAM hesap adı'ndan eşitlenen şirket içi Azure AD.

Merhaba özel de kullanabilirsiniz **ExtractMailPrefix()** işlevi tooremove hello etki alanı soneki hello e-posta adresi, SAM hesap adı ya da hello kullanıcı asıl adı. Merhaba ilk bölümü hello kullanıcı adı yalnızca aracılığıyla geçirilen bu ayıklar (örneğin, "joe_smith" yerine joe_smith@contoso.com).

![Kullanıcı özniteliği Düzenle][5]

Şimdi de hello ekledik **join()** işlevi toojoin hello hello kullanıcı tanımlayıcısı değeri ile etki alanı doğrulandı. hello hello join() işlevi seçtiğinizde, **kullanıcı tanımlayıcısı** ilk select e-posta adresi veya kullanıcı asıl adı olarak gibi kullanıcı tanımlayıcısı hello ve doğrulanmış etki alanınız hello ikinci açılan listesinde seçin. Hello doğrulanmış etki alanıyla hello e-posta adresi seçin ve ardından Azure AD hello ilk değer joe_smith gelen hello kullanıcıadı ayıklar varsa joe_smith@contoso.com ve contoso.onmicrosoft.com ile ekler. Aşağıdaki örnek hello bakın:

![Kullanıcı özniteliği Düzenle][6]

## <a name="adding-claims"></a>Talep ekleme
Bir talep eklerken (hangi kesinlikle toofollow URI düzeni hello SAML spec göredir gerek yoktur) hello öznitelik adı belirtebilirsiniz. Merhaba dizininde depolanan hello değeri tooany kullanıcı özniteliğini ayarlayın.

![Kullanıcı öznitelik Ekle][7]

Örneğin, toosend gereken kullanıcı hello hello departmanı, kuruluşları bir talep (örneğin, satış) olarak tooin ait. Merhaba uygulama tarafından beklendiği gibi Hello talep adını girin ve ardından **user.department** hello değeri olarak.

> [!NOTE]
> Belirli bir kullanıcının seçili öznitelik için depolanan hiçbir değer varsa, daha sonra bu talep hello belirteçte çıkarılan değil.

> [!TIP]
> Merhaba **user.onpremisesecurityidentifier** ve **user.onpremisesamaccountname** kullanıcı verilerini hello kullanarak Active Directory içi eşitleme, yalnızca desteklenen [Azure AD Connect aracını](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Kısıtlı talepleri

SAML bazı kısıtlı talep vardır. Bu talep eklerseniz, Azure AD bu talepler göndermez. Aşağıda verilmiştir hello SAML kısıtlanmış talep kümesi:

    | Talep türü (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expired |
    | http://schemas.microsoft.com/identity/Claims/accesstoken |
    | http://schemas.microsoft.com/identity/Claims/openid2_id |
    | http://schemas.microsoft.com/identity/Claims/identityprovider |
    | http://schemas.microsoft.com/identity/Claims/objectidentifier |
    | http://schemas.microsoft.com/identity/Claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/nameidentifier [MR1] |
    | http://schemas.microsoft.com/identity/Claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/AuthenticationMethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/Claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/groups |
    | http://schemas.microsoft.com/Claims/Groups.Link |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/Claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/Claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/Claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/Claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/Claims/Actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/Authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/Sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/UPN |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/SPN |
    | http://schemas.microsoft.com/ws/2008/06/identity/Claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/Claims/Scope |

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](../active-directory-apps-index.md)
* [Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma](../active-directory-saas-custom-apps.md)
* [Sorun giderme SAML tabanlı çoklu oturum açma](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png