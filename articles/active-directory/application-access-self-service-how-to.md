---
title: aaaHow tooconfigure Self Servis uygulama atama | Microsoft Docs
description: "Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme"
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
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a>Nasıl tooconfigure Self Servis uygulama atama

Kullanıcılarınıza kendi erişim paneli uygulamaları kendi kendine bulabilmesi için öncelikle tooenable gerek **Self Servis uygulamaya erişim** tooallow kullanıcılar tooself istediğiniz tooany uygulamaları-bulmak ve erişim isteği.

Bu özellik toosave zaman ve para BT grubu olarak harika bir yol olduğu ve Azure Active Directory ile modern uygulamalar dağıtımının bir parçası olarak önerilir.

Bu özelliği kullanarak, şunları yapabilirsiniz:

-   Merhaba uygulamalardan otomatik olarak bulmak, kullanıcıların izin [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello BT rahatsız etme olmadan grup.

-   Erişim isteğinde bulundu bkz, erişimi kaldırmak ve toothem atanan hello rollerini yönetmek için bu kullanıcıların tooa önceden yapılandırılmış grubunu ekleyin.

-   İsteğe bağlı olarak Hello BT grubu sahip değil şekilde bir iş onaylayan tooapprove uygulama erişim isteklerini izin verir.

-   İsteğe bağlı olarak erişim toothis uygulama onaylaması too10 kişiler yapılandırın.

-   İsteğe bağlı olarak bir iş onaylayan tooset hello parolalara izin ver kullanıcılarla toosign toohello uygulamasından, sağa hello iş onaylayanın kullanabilirsiniz [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).

-   İsteğe bağlı olarak otomatik olarak doğrudan kendine atanan kullanıcılar tooan uygulama rolü atayın.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme

Self Servis uygulama erişimi olan mükemmel şekilde tooallow kullanıcılar tooself-uygulamaları bulmak, isteğe bağlı olarak hello iş grubu tooapprove erişimi toothose uygulamaları izin verin. Merhaba iş grubu toomanage hello kimlik toothose kullanıcılar kendi access panel üzerinde parola çoklu oturum uygulamaları sağdan için atanan izin verebilirsiniz.

tooenable Self Servis uygulama erişim tooan uygulaması, aşağıdaki hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooenable Self Servis erişim toofrom hello listesi hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **Self Servis** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  tooenable bu uygulama için Self Servis uygulama erişimi etkinleştirmek hello **toorequest erişim toothis uygulama kullanıcıların?** çok geçiş**Evet.**

9.  Ardından, access toothis uygulaması eklenmesi, isteyen tooselect hello Grup toowhich kullanıcılar'ı tıklatın hello Seçici sonraki toohello etiket **toowhich grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.

10. **İsteğe bağlı:** kullanıcıların erişim izin verilmeden önce bir iş onay toorequire isterseniz, hello ayarlamak **erişim toothis uygulama vermeden önce onay gerektirir?** çok geçiş**Evet**.

11. **İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** toothis uygulama onaylanan kullanıcılar için gönderilen bu iş onaylayanlar toospecify hello parolaları tooallow isterseniz hello ayarlamak **izin onaylayanlar tooset Bu uygulama için kullanıcının parola?**  çok geçiş**Evet**.

12. **İsteğe bağlı:** tooapprove erişim toothis uygulama, izin verilen toospecify hello iş onaylayanlar tıklatın hello Seçici sonraki toohello etiket **kimin tooapprove erişim toothis uygulama verilir?** tooselect ayarlama too10 ayrı ayrı iş onaylayanlar.

   >[!NOTE]
   >Grupları desteklenmez.
   >
   >

13. **İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, tooassign Self Servis onaylanan kullanıcılar tooa rol istiyorsanız hello Seçici sonraki toohello tıklatın **toowhich rol kullanıcılar bu atanmalıdır Uygulama?**  tooselect hello rol toowhich bu kullanıcılar atanabilir.

14. Merhaba tıklatın **kaydetmek** hello dikey toofinish hello üstündeki düğmesi.

Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar tootheir gezinebilir [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello tıklatıp **+ Ekle** düğmesini toofind hello uygulamaları toowhich etkinleştirdiğiniz Self Servis erişim. İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/). Bir kullanıcı kendi onay gerektiren erişim tooan uygulama istendiğinde bildiren bir e-posta etkinleştirebilirsiniz. 

Bu onaylar, birden çok onaylayanlar belirtirseniz, tek bir onaylayan onaylayan access toohello uygulaması olabilir yani yalnızca tek onay iş akışları destekler.

## <a name="next-steps"></a>Sonraki adımlar
[Self Servis Grup Yönetimi için Azure Active Directory ayarlayan](active-directory-accessmanagement-self-service-group-management.md)
