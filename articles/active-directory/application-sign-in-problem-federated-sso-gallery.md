---
title: "Federasyon için yapılandırılan tooa galeri uygulamada imzalama aaaProblems çoklu oturum açma | Microsoft Docs"
description: "Yönergeler için yapılandırdığınız bir uygulamaya SAML tabanlı Federasyon tek oturum açma için Azure AD ile imzalarken hello belirli hataları"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>Federasyon çoklu oturum açma için yapılandırılmış tooa galeri uygulamada oturum sorunları

tootroubleshoot, sorun izleme olarak Azure AD'de tooverify hello uygulama yapılandırması gerekir:

-   Hello Azure AD galeri uygulama için tüm hello yapılandırma adımları izlediğinizi.

-   Merhaba tanımlayıcısı ve yanıt AAD'de yapılandırılmış URL'si eşleşen bunlar hello uygulamada beklenen değerler

-   Toohello uygulama veya atanan kullanıcılar

## <a name="application-not-found-in-directory"></a>Uygulama dizinde bulunamadı

*Hata AADSTS70001: Uygulama, tanımlayıcısı 'https://contoso.com' hello dizininde bulunamadı*.

**Olası neden**

Merhaba veren özniteliği hello SAML isteğinde AD hello uygulama Azure AD yapılandırılmış hello tanımlayıcı değeri eşleşmiyor hello uygulama tooAzure gönderir.

**Çözümleme**

Bu hello veren öznitelik hello Azure AD içinde yapılandırılmış tanımlayıcı değeri eşleşen hello SAML isteğinde emin olun:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**etki alanı ve URL'leri** bölümü. Merhaba textbox hello değeri hello hata görüntülenen hello tanımlayıcı değeri için eşleştirme tanımlayıcı hello değeri doğrulayın.

Azure AD'de veya güncelleştirilen hello tanımlayıcı değerine ve hello SAML isteğinde hello uygulama tarafından eşleşen hello değeri gönderir sonra toohello uygulamada mümkün toosign olmalıdır.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>Merhaba yanıt adresi hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor.

*Hata AADSTS50011: hello yanıt adresini 'https://contoso.com' hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor.*

**Olası neden**

Merhaba hello SAML istekteki AssertionConsumerServiceURL değeri hello yanıt URL'si değer veya desen Azure AD içinde yapılandırılmış eşleşmiyor. Merhaba hello SAML istekteki AssertionConsumerServiceURL değeri hello hata gördüğünüz hello URL'dir.

**Çözümleme**

Azure AD'de cihazın eşleşen hello yanıt URL'si değeri yapılandırılmış hello SAML isteğinde hello AssertionConsumerServiceURL değeri emin olun.

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**etki alanı ve URL'leri** bölümü. Doğrulamak veya hello yanıt URL'si metin kutusuna toomatch hello hello SAML istekteki AssertionConsumerServiceURL değeri hello değeri güncelleştirin.  
    * Merhaba yanıt URL'si textbox görmüyorsanız, hello seçin **Göster Gelişmiş URL ayarları** onay kutusu.

Azure AD'de veya güncelleştirilen hello yanıt URL'si değerine ve onu sonra hello değerle eşleşen hello uygulama tarafından hello SAML isteği gönderir, toohello uygulamada mümkün toosign olması gerekir.

## <a name="user-not-assigned-a-role"></a>Kullanıcı bir role atanmış olmamalıdır

*Hata AADSTS50105: hello imzalı kullanıcı 'brian@contoso.com' hello uygulama için tooa rolü atanmamış*.

**Olası neden**

Azure AD erişim toohello uygulamada Hello kullanıcı verilmedi.

**Çözümleme**

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

## <a name="not-a-valid-saml-request"></a>Bir geçerli SAML istekte

*Hata AADSTS75005: hello isteği, geçerli bir Saml2 protokol iletisi değil.*

**Olası neden**

Azure AD hello SAML çoklu oturum açma için Merhaba uygulaması tarafından gönderilen isteği desteklemiyor. Bazı yaygın sorunlar şunlardır:

-   Merhaba SAML isteğinde gerekli alanlar eksik

-   SAML kodlanmış isteği yöntemi

**Çözümleme**

1.  SAML isteğinde yakalayın. Merhaba öğreticisini izleyin [nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure AD'de](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn nasıl toocapture hello SAML isteyin.

2.  Merhaba uygulamanın satıcısına ve Paylaşım başvurun:

   -   SAML isteği

   -   [Azure AD çoklu oturum açma SAML protokolü gereksinimleri](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Bunlar doğrulamalıdır hello Azure AD SAML uygulama için çoklu oturum açmayı destekledikleri.

## <a name="no-resource-in-requiredresourceaccess-list"></a>RequiredResourceAccess listesinde kaynak yok

*Hata AADSTS65005:hello istemci uygulaması erişim tooresource istedi ' 00000002-0000-0000-c000-000000000000'. Merhaba istemci kendi requiredResourceAccess listesinde bu kaynak belirtilmedi bu isteği başarısız oldu*.

**Olası neden**

Merhaba uygulama nesnesi bozuk.

**Çözüm: seçeneği 1**

toosolve hello sorun hello Azure AD yapılandırmasında hello benzersiz tanımlayıcısı değeri ekleyin. tooadd tanımlayıcı değeri hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello üzerinde tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde

8.  Merhaba altında **etki alanı ve URL** bölümünde, denetleme üzerinde hello **Göster Gelişmiş URL ayarları**.

9.  Merhaba, **tanımlayıcısı** metin hello uygulama için benzersiz bir tanımlayıcı yazın.

10. **Kaydet** hello yapılandırma.


**Çözüm seçeneği 2**

Seçenek 1 yukarıda sizin için olmadıysa Merhaba uygulaması hello dizininden kaldırmayı deneyin. Ardından, ekleyin ve hello uygulamayı yeniden yapılandırmak, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Tıklatın **silmek** hello sol üst hello uygulamasının adresindeki **genel bakış** dikey.

8.  Azure AD yenileyin ve hello Azure AD Galerisi'nden hello uygulama ekleyin. Ardından, Merhaba uygulaması yapılandırın

<span id="_Hlk477190176" class="anchor"></span>Merhaba uygulaması yeniden yapılandırmadan sonra toohello uygulamada mümkün toosign olmalıdır.

## <a name="certificate-or-key-not-configured"></a>Sertifika veya anahtar yapılandırılmadı

*Hata AADSTS50003: yapılandırılmış hiçbir imzalama anahtarı.*

**Olası neden**

Merhaba uygulama nesnesi bozuk ve Azure AD hello uygulama için yapılandırılan hello sertifika tanımıyor.

**Çözümleme**

toodelete ve yeni bir sertifika oluşturmak, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

 * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  tıklatın **yeni sertifika oluştur** hello altında **imzalama sertifikası SAML** bölümü.

9.  Sona erme tarihini seçin. Ardından **kaydedin.**

10. Denetleme **yeni sertifika etkin hale getirin** toooverride hello active sertifika. Ardından **kaydetmek** hello dikey penceresinde hello üstündeki ve tooactivate hello geçiş sertifikası kabul edin.

11. Merhaba altında **SAML imzalama sertifikası** 'yi tıklatın **kaldırmak** tooremove hello **kullanılmayan** sertifika.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Merhaba SAML talep özelleştirirken sorun tooan uygulama gönderilen

toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl toodebug SAML tabanlı tek oturum açma tooapplications Azure AD'de](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
