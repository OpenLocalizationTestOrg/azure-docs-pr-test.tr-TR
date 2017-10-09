---
title: "aaaSign açma etkinliği raporu hata kodları hello Azure Active Directory portalında | Microsoft Docs"
description: "Oturum açma etkinlik raporu hata kodları başvurusu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory portalında oturum açma etkinliği raporu hata kodları

Merhaba kullanıcı oturum açma işlemleri raporu tarafından sağlanan hello bilgilerle yanıtlar tooquestions gibi bulun:

- Kimler Azure Active Directory kullanarak oturum açtı?
- Hangi uygulamalarda oturum açıldı?
- Hangi oturum açma girişimleri başarısız oldu ve neden?

Bu konuda listeleri hello hata kodları ve ilgili açıklamalar hello. 

## <a name="how-can-i-display-failed-sign-ins"></a>Başarısız oturum açma girişimlerini nasıl görüntüleyebilirim? 

Verilerin ilk giriş noktası tooall oturum açma etkinliklerinizi  **[oturum açma işlemleri](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  hello içinde **etkinlik** bölümünü **Azure Active**.


![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins-errors/61.png "oturum açma etkinliği")


Oturum açma raporunuzda tüm başarısız oturum açma işlemlerini görüntülemek için, **Oturum açma durumu** olarak **Başarısız**'ı seçebilirsiniz.


![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins-errors/06.png "oturum açma etkinliği")

Görüntülenen hello listeden bir öğe tıklatıldığında, açılır hello **etkinliği ayrıntıları: oturum açma işlemleri** dikey. Bu görünüm, Azure Active Directory oturum hello dahil olmak üzere bileşenler hakkında izleyen tüm hello ayrıntıları sağlar **oturum açma hata kodu** ve **başarısızlık nedeniyle**.

![Oturum açma etkinliği](./media/active-directory-reporting-activity-sign-ins-errors/05.png "oturum açma etkinliği")


Bir alternatif toousing hello Azure portal tooaccess hello gerçekleştirilen oturum açma verileri hello de kullanabilirsiniz [raporlama API'si](active-directory-reporting-api-getting-started-azure-portal.md).


Merhaba aşağıdaki bölümde, tüm olası hataları ve hello tam olarak genel bakış ile sağlar ilgili açıklamalar. 

## <a name="error-codes"></a>Hata kodları

| Hata| Açıklama |
| --- | --- |
| 50001| X adlı hello hizmet sorumlusu Y adlı hello Kiracı içinde bulunamadı. Merhaba uygulaması hello Kiracı hello Yöneticisi tarafından yüklü değilse bu durum oluşabilir. Veya kaynak asıl hello dizininde bulunamadı veya geçersiz|
| 50008| SAML onayı eksik veya yanlış yapılandırılmış hello belirteci.|
| 50011| Merhaba yanıt adresi eksik, yanlış yapılandırılmış veya hello uygulama için yapılandırılan yanıt adresleri eşleşmiyor.|
| 50053| Kullanıcı toosign içinde çok fazla kez ile yanlış kullanıcı kimliği veya parola denediğinden hesap kilitlendi.|
| 50054| Kimlik doğrulaması için eski parola kullanıldı.|
| 50055| Geçersiz parola, süresi dolmuş parola girildi.|
| 50057| Kullanıcı hesabı devre dışı bırakıldı.|
| 50058| Kullanıcının kimliği hakkında hiçbir bilgi arasında kimlik bilgileri veya kullanıcı Kiracı içinde bulunamadı veya sessiz bir oturum açma isteği gönderildi ancak hiçbir kullanıcının oturum açtığı veya hizmeti oluşturamıyor tooauthenticate hello kullanıcı tarafından sağlanan bulunamadı.|
| 50074| Güçlü Kimlik Doğrulaması (ikinci faktör) gereklidir|
| 50079| Kullanıcı tooenroll ikinci faktörlü kimlik doğrulaması için gerekiyor.|
| 50126| Geçersiz kullanıcı adı veya parola ya da Geçersiz şirket içi kullanıcı adı veya parola.|
| 50131| Çeşitli koşullu erişim hatalarında kullanılır. Örneğin hatalı Windows cihaz durumu isteği kararları toosuspicious etkinlik, erişim ilkesini ve güvenlik ilkesi engellendi.|
| 50133| Tooexpiration veya son parola değişikliği geçersiz.|
| 50144| Kullanıcının Active Directory parolasının süresi doldu.|
| 65001| Uygulama X izni tooaccess uygulama Y yok veya hello iznini iptal. Veya hello kullanıcı veya yönetici toouse hello uygulama kimliği x gönderme bu kullanıcı ve kaynak için bir etkileşimli yetkilendirme isteği ile seçtiği değil. Veya hello kullanıcı veya yönetici olmayan rıza toouse hello uygulamayla kimliği x gönderme bir yetkilendirme isteği tooyour Kiracı yönetici tooact hello uygulama adına: kaynak için Y: Z.|
| 65005| Kaynak erişim listesi hello kaynak tarafından uygulamaları bulunabilirlik içermiyor veya Merhaba istemci uygulaması, gerekli kaynağa erişim listesi ya da hatalı döndürülen Grafik Hizmeti belirtilmedi erişim tooresource istedi Merhaba uygulaması gerekiyor istek veya kaynak bulunamadı.|
| 70001| X adlı hello uygulaması Y adlı hello Kiracı içinde bulunamadı. Merhaba uygulaması tarafından yüklenmemiş varsa bu hello Kiracı veya razı tooby Yöneticisi hello Kiracı herhangi bir kullanıcı durum hello. Kimlik doğrulama isteği toohello yanlış Kiracı gönderilen.|
| 80001| Kullanılabilir Kimlik Doğrulama Aracısı yok.|
| 80002| Kimlik Doğrulama Aracısı'nın parola doğrulama isteği zaman aşımına uğradı.|
| 80003| Kimlik Doğrulama Aracısı tarafından geçersiz yanıt alındı.|
| 80004| Oturum açma isteğinde yanlış Kullanıcı Asıl Adı (UPN) kullanıldı.|
| 80005| Kimlik Doğrulama Aracısı: Hata oluştu.|
| 80007| Kimlik Doğrulama Aracısı yüklenemiyor tooconnect tooActive dizini.|
| 80010| Kimlik Doğrulama Aracısı yüklenemiyor toodecrypt parolası.|
| 81001| Kullanıcının Kerberos anahtarı fazla büyük.|
| 81002| %S toovalidate kullanıcının Kerberos bileti.|
| 81003| %S toovalidate kullanıcının Kerberos bileti.|
| 81004| Kerberos kimlik doğrulaması girişimi başarısız oldu.|
| 81008| %S toovalidate kullanıcının Kerberos bileti.|
| 81009| %S toovalidate kullanıcının Kerberos bileti.|
| 81010| Merhaba kullanıcının Kerberos anahtarının süresi doldu veya geçersiz olduğu için sorunsuz SSO başarısız oldu.|
| 81011| Merhaba kullanıcının Kerberos bileti içindeki bilgileri temel oluşturulamıyor toofind kullanıcı nesnesi.|
| 81012| toosign tooAzure AD içinde çalışan hello kullanıcının hello cihazda imzalı hello kullanıcı farklıdır.|
| 81013| Merhaba kullanıcının Kerberos bileti içindeki bilgileri temel oluşturulamıyor toofind kullanıcı nesnesi.|
| 90014| Beklenen bir alan hello kimlik bilgisi mevcut olmadığında çeşitli durumlarda kullanılır.|
| 90093| Grafik hello isteği Yasak hata kodunu döndürdü.|



## <a name="next-steps"></a>Sonraki adımlar

Daha fazla ayrıntı için bkz: Merhaba [oturum açma etkinlik raporları'hello Azure Active Directory portalında](active-directory-reporting-activity-sign-ins.md).

