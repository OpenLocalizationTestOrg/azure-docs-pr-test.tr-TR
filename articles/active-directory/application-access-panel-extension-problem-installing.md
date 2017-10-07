---
title: "Merhaba uygulama erişim paneli tarayıcı uzantısı yükleme aaaProblem | Microsoft Docs"
description: "Hello erişim paneli tarayıcı uzantısı yüklerken toofix sık karşılaşılan hataların nasıl karşılaştı"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Merhaba uygulama erişim paneli tarayıcı uzantısı yükleme sorunu

Merhaba erişim paneli, hangi etkinleştirir bir iş veya Okul sahip bir kullanıcı hesabı Azure Active Directory (Azure AD) tooview ve başlatma bulut tabanlı uygulamalarda o hello Azure AD yönetici web tabanlı bir portal erişim verildi ' dir. Azure AD sürümleri olan bir kullanıcı, Self Servis grup ve hello erişim paneli üzerinden uygulama yönetim özellikleri de kullanabilirsiniz. Merhaba erişim paneli hello Azure portal ' ayrıdır ve kullanıcıların toohave bir Azure aboneliği gerektirmez.

toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Merhaba erişim paneli toplantı tarayıcı gereksinimleri

JavaScript destekleyen bir tarayıcı Hello erişim paneli gerektirir ve CSS etkinleştirdi. toouse parola tabanlı çoklu oturum açma (SSO) hello erişim paneli, hello erişim paneli uzantısı içinde hello kullanıcının tarayıcısında yüklenmesi gerekir. Bir kullanıcı, parola tabanlı SSO için yapılandırılmış bir uygulama seçtiğinde bu uzantıyı otomatik olarak yüklenir.

Parola tabanlı, SSO için hello son kullanıcının tarayıcılar olabilir:

-   Internet Explorer 8, 9, 10, 11--Windows 7 veya üzeri

-   Edge Windows 10 Anniversary Edition veya daha yenisi 

-   Chrome--Windows 7 veya daha sonra ve MacOS x veya sonraki sürümlerde

-   Firefox 26,0 veya daha sonra--Windows XP SP2 veya sonraki ve Mac OS X 10,6 veya üzeri

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Nasıl tooinstall hello erişim paneli tarayıcı uzantısı

tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:

1.  Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.

2.  Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.

3.  Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.

4.  Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir. **Ekleme** hello uzantısı tooyour tarayıcı.

5.  Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.

6.  Bir kez yüklenir, **yeniden** tarayıcı oturumunda.

7.  Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamaları

Ayrıca hello uzantısı Chrome ve kenar hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:

-   [Chrome erişim paneli uzantısı](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Edge erişim paneli uzantısı](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Internet Explorer için Grup İlkesi ayarı

Kullanıcılarınızın makinelerde Internet Explorer için tooremotely yükleme hello erişim paneli uzantısına izin ver Grup İlkesi ayarlayabilirsiniz.

Merhaba Önkoşullar şunlardır:

-   Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.

-   Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir. Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Merhaba öğreticisini izleyin [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md) ilişkin adım adım yönergeler nasıl tooconfigure hello Grup İlkesi ve toousers dağıtın.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Merhaba erişim paneli Internet Explorer'da sorun giderme

Merhaba izleyin [sorun giderme hello Internet Explorer için erişim paneli uzantısı](active-directory-saas-ie-troubleshooting.md) hello uzantısı için IE yapılandırma erişim için bir tanılama aracı ve adım adım yönergeler Kılavuzu.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Bu sorun giderme adımları hello sorunu çözmezse

bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Tenantıd

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
