---
title: "aaaHow tooassign kullanıcılar ve gruplar tooan uygulama | Microsoft Docs"
description: "Kullanıcıların toohello uygulama toogrant erişimi atayın"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a>Nasıl tooassign kullanıcılar ve gruplar tooan uygulama

Kullanıcılarınızın herhangi belirli bir uygulama için hello yapabilmeniz için önce toofirst gerek **toohello uygulama atama** erişmesine toogrant:

-   Bir uygulama tarafından erişim **toohello uygulamanın URL doğrudan gezinme** (olarak da bilinen SP tarafından başlatılan oturum açma).

-   Hello kullanarak bir uygulamaya erişim **kullanıcı erişim URL'si** bir uygulamanın üzerinde **özellikleri** sayfa (olarak da bilinen IDP başlatılan oturum açma).

-   Görünür bir uygulama bkz kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) ya da mobil uygulama.

-   Görünür bir uygulama bkz kendi [Office 365 uygulama Başlatıcı](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).

## <a name="methods-tooassign-applications-with-azure-active-directory"></a>Azure Active Directory ile yöntemleri tooassign uygulamalar 

Azure Active Directory ile uygulamaları atayabilirsiniz 3 yolu vardır:

-   [Bir kullanıcı atamak doğrudan tooan uygulama yönetici olarak](#assign-a-user-directly-as-an-administrator)

-   [Bir gruba atamak doğrudan tooan uygulama yönetici olarak](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>Yönetici doğrudan kullanıcı atama

tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.

9.  Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.

10. Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.

13. Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.

Bir kısa süre sonra seçtiğiniz hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Bir gruba atamak doğrudan tooan uygulama yönetici olarak

bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.

9.  Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.

10. Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.

11. Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**. Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.

12. **İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.

13. Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.

14. **İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.

15. Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.

Bir kısa süre sonra seçtiğiniz hello grupları içindeki hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması. Bu dinamik grupların varsa, bazı ek işleme gecikme olabilir bu grupları atanan içindeki kullanıcılar için görünen bu atamaları içinde.

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
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
