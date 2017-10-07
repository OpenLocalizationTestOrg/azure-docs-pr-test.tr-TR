---
title: "aaaHow uygulamaları hello erişim panelinde görüntülenir | Microsoft Docs"
description: "Bir uygulama hello erişim paneli görünen neden sorun giderme"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Uygulamaları hello erişim panelinde görüntülenme

Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni. Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır. Hello Yöneticisi hello uygulama toohello kullanıcı doğrudan veya bir kullanıcı hello kullanıcının erişim Panoda görünmesini hello uygulamada kaynaklanan bir parçası olan tooa Grup sağlayabilirsiniz.

## <a name="general-issues-toocheck-first"></a>Genel toocheck ilk sorunları

-   Merhaba uygulaması kaldırılırsa bir uygulamayı yalnızca bir kullanıcıdan kaldırıldı veya grup hello kullanıcının üyesi olduğu, toosign giriş ve çıkış yeniden hello kullanıcının erişim paneline sonra birkaç dakika toosee deneyin.

-   Bir lisans yalnızca bir kullanıcı veya grup hello kullanıcı kaldırıldıysa bu üyesi hello boyutu ve karmaşıklığı yapılan değişiklikleri toobe hello grubunun bağlı olarak uzun bir süre devam edebilir ' dir. Erişim paneli hello oturum açmadan önce ek süresi için izin verin.

## <a name="problems-related-tooassigning-applications-toousers"></a>Sorunları ilgili tooassigning uygulamaları toousers

Bunlar daha önce tooit atanmış çünkü bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz. Bazı yolları toocheck aşağıda verilmiştir:

-   [Bir kullanıcı toohello uygulama atandığından emin olun](#check-if-a-user-is-assigned-to-the-application)

-   [Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Bir kullanıcı toohello uygulama atandığından emin olun

toocheck toohello uygulama atanmış bir kullanıcı yoksa, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

6.  **Arama** için söz konusu hello uygulamasının hello adı.

7.  tıklatın **kullanıcılar ve gruplar**.

8.  Kullanıcı toohello uygulama atanmışsa toosee denetleyin.

  * Merhaba uygulamasından tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello kullanıcı seçin ve **silmek**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama

toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.

   * Merhaba kullanıcı atanan tooan Office lisansı ise bu etkinleştirin birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Sorunları ilgili tooassigning uygulamaları toogroups

Merhaba uygulaması atanmış bir grubun parçası olmadığından bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz. Bazı yolları toocheck aşağıda verilmiştir:

-   [Bir kullanıcı grup üyeliklerini denetleyin](#check-a-users-group-memberships)

-   [Bir kullanıcı tooa lisans atanmış bir grup üyesi olup olmadığını denetleyin](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Bir kullanıcı grup üyeliklerini denetleyin

toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **gruplar.**

8.  Kullanıcı grubunun bir parçası ise onay toosee toohello uygulama atanır.

   * Merhaba grubundan tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello grubu ve select silin.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Bir kullanıcı tooa lisans atanmış bir grup üyesi olup olmadığını denetleyin

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.

5.  tıklatın **tüm kullanıcılar**.

6.  **Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.

7.  tıklatın **gruplar.**

8.  belirli bir grup Hello satırının'ı tıklatın.

9.  tıklatın **lisansları** toosee hangi lisansları hello Grup tooit atanan.

  * Merhaba grubu atanan tooan Office lisansı ise bu belirli birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde sağlayabilir.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Sorun giderme adımları değil hello varsa hello sorunu çözün

bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:

-   Bağıntı hata kimliği

-   UPN (kullanıcı e-posta adresi)

-   Kiracı Kimliği

-   Tarayıcı türü

-   Saat dilimi ve saat/zaman çerçevesine hata oluşuyor

-   Fiddler izlemeleri

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
