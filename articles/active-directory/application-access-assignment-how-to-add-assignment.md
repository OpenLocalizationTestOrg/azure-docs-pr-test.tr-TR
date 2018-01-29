---
title: "Kullanıcılar ve gruplar için bir uygulama atama | Microsoft Docs"
description: "Kullanıcılara erişim vermek için uygulamaya atayın"
services: active-directory
documentationcenter: 
author: ajamess
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4198b5fd971291e78a45af764eaaa1b9dc155893
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a>Kullanıcılar ve gruplar için bir uygulama atama

Kullanıcılarınızın herhangi birini yapmak için önce aşağıdaki belirli bir uygulama için ilk için gereksinim duyduğunuz **uygulamaya atamak** erişim vermek için:

-   Bir uygulama tarafından erişim **doğrudan uygulamanın URL'ye geçerken** (olarak da bilinen SP tarafından başlatılan oturum açma).

-   Kullanarak bir uygulamaya erişim **kullanıcı erişim URL'si** bir uygulamanın üzerinde **özellikleri** sayfa (olarak da bilinen IDP başlatılan oturum açma).

-   Görünür bir uygulama bkz kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) ya da mobil uygulama.

-   Görünür bir uygulama bkz kendi [Office 365 uygulama Başlatıcı](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).

## <a name="methods-to-assign-applications-with-azure-active-directory"></a>Azure Active Directory ile uygulamaları atamak için yöntemleri 

Azure Active Directory ile uygulamaları atayabilirsiniz 3 yolu vardır:

-   [Yönetici olarak bir uygulamaya doğrudan kullanıcı atama](#assign-a-user-directly-as-an-administrator)

-   [Yönetici olarak bir uygulamaya doğrudan bir gruba atamak](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>Yönetici doğrudan kullanıcı atama

Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.

5.  tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.

  * Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**

6.  Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.

7.  Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.

8.  Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.

9.  tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.

10. Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.

11. Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**. Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.

12. **İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.

13. Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.

14. **İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.

15. Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.

Bir kısa süre sonra seçtiğiniz kullanıcıların çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir.

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a>Yönetici olarak bir uygulamaya doğrudan bir gruba atamak

Bir veya daha fazla grupları doğrudan bir uygulamaya atamak için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.

5.  tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.

  * Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**

6.  Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.

7.  Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.

8.  Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.

9.  tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.

10. Yazın **tam grup adı** içine atama ilgilenen grubunun **ad veya e-posta adresine göre arama** arama kutusu.

11. Üzerine gelerek **grup** ortaya çıkarmak için listedeki bir **onay kutusunu**. Grubun profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.

12. **İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla grubu Ekle**, başka bir tür **tam grup adı** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu gruba eklemek için onay kutusunu işaretleyin **seçili** listesi.

13. Grupları seçmek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.

14. **İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz gruplarına atamak için bir rol seçin dikey.

15. Tıklatın **atamak** seçilen grupları uygulamaya atamak için düğmesi.

Bir kısa süre sonra kullanıcılar seçtiğiniz grupları içindeki çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir. Bu dinamik grupların varsa, bazı ek işleme gecikme olabilir bu grupları atanan içindeki kullanıcılar için görünen bu atamaları içinde.

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a>Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir

Self Servis uygulamaya erişim uygulamaları, kendi kendine Bul yapmalarına izin vermek için mükemmel bir yoldur bu uygulamalara erişimi onaylamak için iş grubuna isteğe bağlı olarak sağlar. Bu kullanıcılar için parola çoklu oturum uygulamalar üzerinde sağ bunların erişim paneller atanan kimlik bilgilerini yönetmek iş grubuna izin verebilirsiniz.

Bir uygulama Self Servis uygulama erişimi etkinleştirmek için aşağıdaki adımları izleyin:

1.  Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**

2.  Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.

3.  Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.

4.  tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.

5.  tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.

   * Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**

6.  Self Servis etkinleştirmek istediğiniz uygulamayı seçin listeden erişmek için.

7.  Uygulamanın yüklediği sonra tıklayın **Self Servis** uygulamanın sol taraftaki gezinti menüsünde.

8.  Bu uygulama için Self Servis uygulama erişimini etkinleştirmek için Aç **bu uygulamaya erişmek kullanıcıların?** geç **Evet.**

9.  Ardından, isteyen hangi kullanıcıların bu uygulamaya erişim eklenecek grubu seçmek için etiketi yanındaki seçiciyi **hangi grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.

10. **İsteğe bağlı:** önce iş onayı iste isterseniz, kullanıcılara erişim verilir, Ayarla **bu uygulamaya erişim vermeden önce onay gerektirir?** geç **Evet**.

11. **İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** onaylanan kullanıcılar için bu uygulamaya gönderilen parolalar belirtmek bu iş onaylayanlar izin vermek istiyorsanız, Ayarla **bu uygulama için kullanıcının parola ayarlamak onaylayanlar izin?** geç **Evet**.

12. **İsteğe bağlı:** bu uygulamaya erişimi onaylamak için izin verilen iş onaylayanlar belirtmek için etiketi yanındaki seçiciyi **kimin bu uygulamaya erişimi onaylamak için verilir?** en fazla 10 ayrı ayrı iş onaylayanlar seçin.

  >[!NOTE]
  >Grupları desteklenmez.
  >
  >

13. **İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, Self Servis onaylanan kullanıcılar role atamak istiyorsanız Seçici tıklayın **hangi rolü için kullanıcıları bu uygulamada atanmalıdır?** , bu kullanıcılar atanabilir rol seçin.

14. Tıklatın **kaydetmek** tamamlamak için dikey pencerenin üstündeki düğmesi.

Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar için gezinebilir kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tıklatıp **+ Ekle** Self Servis erişim etkin uygulamalar Bul düğmesi. İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/). Bir kullanıcı kendi onay gerektiren bir uygulamaya erişim istendiğinde bildiren bir e-posta etkinleştirebilirsiniz. 

Bu onaylar, birden çok onaylayanlar belirtirseniz, tek bir onaylayan uygulamaya onaylayan erişim olabilir yani yalnızca tek onay iş akışları destekler.

## <a name="next-steps"></a>Sonraki adımlar
[Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.](active-directory-application-proxy-sso-using-kcd.md)
