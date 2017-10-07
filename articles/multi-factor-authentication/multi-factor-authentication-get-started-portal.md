---
title: "Azure MFA sunucusu için aaaUser portalı | Microsoft Docs"
description: "Bu tooget hello Kullanıcı Portalı ile Azure MFA ile çalışmaya nasıl açıklayan hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Hello Azure multi-Factor Authentication sunucusu kullanıcı portalı

Merhaba Kullanıcı Portalı, kullanıcıların tooenroll Azure çok faktörlü kimlik doğrulama (MFA) verir ve hesaplarını korumalarını bir IIS web sitesi ' dir. Bir kullanıcı, telefon numarasını, PIN'ini değiştirebilir veya iki aşamalı doğrulama, bir sonraki oturum açma sırasında toobypass seçin.

Kullanıcılar kendi normal kullanıcı adı ve parola ile toohello kullanıcı portalında oturum açın, sonra iki aşamalı doğrulama aramayı tamamlamak ya da güvenlik soruları toocomplete kendi kimlik doğrulaması yanıt. Kullanıcı kaydına izin veriliyorsa, kullanıcılar ilk kez oturum telefon numaraları ve PIN hello toohello Kullanıcı Portalı'nda yapılandırın.

Kullanıcı Portalı Yöneticileri ayarlanabilir ve izin tooadd yeni kullanıcılar ve varolan kullanıcıları güncelleştir verildi.

Ortamınıza bağlı olarak toodeploy hello Kullanıcı Portalı'nı hello isteyebilirsiniz Azure multi-Factor Authentication sunucusu veya başka bir internet'e yönelik sunucuda aynı sunucu.

![MFA Kullanıcı Portalı](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> Merhaba Kullanıcı Portalı yalnızca multi-Factor Authentication sunucusu ile kullanılabilir. Merhaba bulutta çok faktörlü kimlik doğrulaması kullanıyorsanız, kullanıcıların toohello başvurun [Kurulum hesabınız iki aşamalı doğrulama için](./end-user/multi-factor-authentication-end-user-first-time.md) veya [iki aşamalı doğrulama için ayarlarınızı yönetme](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Merhaba web hizmeti SDK'sını yükleyin

Her iki durumda da hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı ise **değil** hello Azure çok faktörlü kimlik doğrulama (MFA) sunucu üzerinde yüklü, tam hello adımlar anlatılmaktadır.

1. Merhaba çok faktörlü kimlik doğrulama sunucusu konsolunu açın.
2. Toohello Git **Web hizmeti SDK'sı** seçip **Web hizmeti SDK'sını yüklemek**.
3. Tam hello yükleme toochange gerekmedikçe hello varsayılanları kullanarak herhangi bir nedenle bunları.
4. IIS'de bir SSL sertifikası toohello sitesi bağlayın.

Bir IIS sunucusunda bir SSL sertifikası yapılandırma hakkında sorularınız varsa, hello makalesine bakın [nasıl tooSet SSL IIS'de](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Merhaba Web hizmeti SDK'sı bir SSL sertifikası ile güvenli gerekir. Bu amaç için otomatik olarak imzalanan bir sertifika kullanılabilir. Böylece hello SSL bağlantısı başlatılırken bu sertifikayı güvenleri hello sertifika hello hello Kullanıcı Portalı web sunucusundaki yerel bilgisayar hesabının hello "Güvenilen kök sertifika yetkilileri" deposuna aktarın.

![MFA Sunucusu yapılandırma kurulum Web hizmeti SDK'sı](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Merhaba Kullanıcı Portalı'nı hello dağıtmak hello Azure multi-Factor Authentication sunucusu ile aynı sunucu

Merhaba aşağıdaki önkoşulların olan gerekli tooinstall hello Kullanıcı Portalı'nı hello **aynı sunucu** Azure çok faktörlü kimlik doğrulama sunucusu hello olarak:

* ASP.NET ve IIS 6 meta tabanı uyumluluğu (IIS 7 ya da üst sürümü için) dahil IIS
* Merhaba bilgisayar ve etki alanı varsa için yönetici haklarına sahip bir hesap. Merhaba hesabının izinleri toocreate Active Directory güvenlik gruplarını gerekir.
* Merhaba Kullanıcı Portalı bir SSL sertifikası ile güvenli hale getirin.
* Hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı bir SSL sertifikası ile güvenli hale getirin.

Bu adımları toodeploy hello Kullanıcı Portalı, izleyin:

1. Merhaba hello Azure çok faktörlü kimlik doğrulama sunucusu konsolunu açın, **kullanıcı portalı** hello simgesine sol menüsü, ardından **kullanıcı portalını Yükle**.
2. Tam hello yükleme toochange gerekmedikçe hello varsayılanları kullanarak herhangi bir nedenle bunları.
3. IIS'de bir SSL sertifikası toohello sitesi bağlama

   > [!NOTE]
   > Bu SSL Sertifikası çoğunlukla genel olarak imzalanmış bir SSL sertifikasıdır.

4. Herhangi bir bilgisayarda web tarayıcısını açın ve hello Kullanıcı Portalı yüklendiği toohello URL'ye gidin (örnek: https://mfa.contoso.com/MultiFactorAuth). Sertifika uyarısı ya da hatası görüntülenmediğinden emin olun.

![MFA Sunucusu Kullanıcı Portalını yükleme](./media/multi-factor-authentication-get-started-portal/install.png)

Bir IIS sunucusunda bir SSL sertifikası yapılandırma hakkında sorularınız varsa, hello makalesine bakın [nasıl tooSet SSL IIS'de](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Merhaba Kullanıcı Portalı ayrı bir sunucuya dağıtma

Azure multi-Factor Authentication Sunucusu'nun çalıştığı hello sunucusu internet'e yönelik değilse, üzerinde hello Kullanıcı Portalı yüklemelisiniz bir **ayrı, internet'e yönelik sunucu**.

Kuruluşunuz Microsoft Authenticator uygulaması hello doğrulama yöntemlerini biri olarak hello ve toodeploy hello Kullanıcı Portalı'nı kendi sunucusuna istiyorsanız hello gereksinimleri aşağıdaki tamamlayın:

* V6.0 kullanın ya da üst sürümünü hello Azure çok faktörlü kimlik doğrulama sunucusu.
* Microsoft Internet çalıştıran bir internet'e yönelik web sunucusunda Hello Kullanıcı Portalı'nı yükleme Information Services (IIS) 6.x ya da daha yüksek.
* IIS 6.x, ASP.NET v2.0.50727 yüklü, kayıtlı ve çok ayarlamak olun**izin verilen**.
* IIS 7.x veya sonrasını kullanırken, Temel Kimlik Doğrulaması, ASP.NET ve IIS 6 Metatabanı Uyumluluğu dahil IIS.
* Merhaba Kullanıcı Portalı bir SSL sertifikası ile güvenli hale getirin.
* Hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı bir SSL sertifikası ile güvenli hale getirin.
* Bu hello Kullanıcı Portalı SSL üzerinden Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı toohello bağlanabilir emin olun.
* Bu hello Kullanıcı Portalı toohello Azure multi-Factor Authentication Web hizmeti SDK kimlik doğrulaması sağlamak hello "PhoneFactor yöneticileri" güvenlik grubuna bir hizmet hesabı hello kimlik bilgilerini kullanarak. Hello Azure multi-Factor Authentication sunucusu etki alanına katılmış bir sunucuda çalışıyorsa, bu hizmet hesabı ve grubu Active Directory'de var olmalıdır. Birleştirilmiş tooa etki alanında değilse bu hizmet hesabı ve grubu hello Azure çok faktörlü kimlik doğrulama sunucusu üzerinde yerel olarak mevcut.

Yükleme hello Kullanıcı Portalı'hello Azure çok faktörlü kimlik doğrulama sunucusu başka bir sunucuda aşağıdaki adımları hello gerektirir:

1. **Merhaba MFA sunucusu üzerinde**, toohello yükleme yolu gidin (örnek: C:\Program Files\Multi-Factor Authentication sunucusu) ve hello dosya Kopyala **MultiFactorAuthenticationUserPortalSetup64** tooa konumu erişilebilir toohello Internet'e sunucu burada yükler.
2. **Merhaba internet'e yönelik web sunucusunda**, hello MultiFactorAuthenticationUserPortalSetup64 yükleme dosyasını bir yönetici olarak çalıştırın, isterseniz hello Site değiştirme ve isterseniz hello sanal dizin tooa kısa adı değiştirin.
3. IIS'de bir SSL sertifikası toohello sitesi bağlayın.

   > [!NOTE]
   > Bu SSL Sertifikası çoğunlukla genel olarak imzalanmış bir SSL sertifikasıdır.

4. Çok Gözat**C:\inetpub\wwwroot\MultiFactorAuth**
5. Not Defteri'nde Hello Web.Config dosyasını düzenleme

    * Merhaba anahtarını bulun **"Use_web_servıce_sdk"** değiştirip **değer = "false"** çok**değer = "true"**
    * Merhaba anahtarını bulun **"Web_servıce_sdk_authentıcatıon_username"** değiştirip **değer = ""** çok**değer "Etki alanı\kullanıcı" =** burada bir parçası olan bir hizmet hesabı, etki alanı\kullanıcı "PhoneFactor Admins" grubu.
    * Hello anahtarını bulun **"Web_servıce_sdk_authentıcatıon_password değerlerini"** değiştirip **değeri = ""** çok**değeri "Password" =** parola hello hizmet hello parolasını olduğu Merhaba önceki satırda girilen hesabı.
    * Merhaba değerini bulmak **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** ve bu yer tutucu URL toohello Web hizmeti SDK 2. adımda biz yüklü URL'si değiştirin.
    * Merhaba Web.Config dosyasını kaydedin ve Not Defteri'ni kapatın.

6. Herhangi bir bilgisayarda web tarayıcısını açın ve hello Kullanıcı Portalı yüklendiği toohello URL'ye gidin (örnek: https://mfa.contoso.com/MultiFactorAuth). Sertifika uyarısı ya da hatası görüntülenmediğinden emin olun.

Bir IIS sunucusunda bir SSL sertifikası yapılandırma hakkında sorularınız varsa, hello makalesine bakın [nasıl tooSet SSL IIS'de](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Hello Azure multi-Factor Authentication sunucusu kullanıcı portalı ayarlarını yapılandırma

Bu hello Kullanıcı Portalı yüklü artık tooconfigure hello Azure çok faktörlü kimlik doğrulama sunucusu toowork hello portalıyla gerekir.

1. Merhaba Hello Azure çok faktörlü kimlik doğrulama sunucusu konsolunda tıklatın **kullanıcı portalı** simgesi. Hello ayarları sekmesinde hello URL toohello Kullanıcı Portalı hello girin **Kullanıcı Portalı URL'si** metin kutusu. E-posta işlevselliği etkinleştirildiğinde bu URL hello Azure çok faktörlü kimlik doğrulama sunucusu aktarıldıkları zaman toousers gönderilen hello e-postalar dahil edilir.
2. Hello ayarlarını seçin hello Kullanıcı Portalı toouse istiyor. Örneğin, kendi kimlik doğrulama yöntemlerini kullanıcıların toochoose izin verilen emin olun, **tooselect yöntemi kullanıcıların** bunlar seçim yapabileceğiniz hello yöntemleri birlikte denetlenir.
3. Kimin Yöneticiler hello üzerinde çalıştırılması tanımlamak **Yöneticiler** sekmesi. Ayrıntılı yönetim izinleri hello onay kutularını ve bırakmalar hello Ekle/Düzenle kutularında kullanarak oluşturabilirsiniz.

İsteğe bağlı yapılandırma:
- **Güvenlik soruları** -tanımlamak gösterilir, ortam ve hello dil için güvenlik soruları onaylandı.
- **Geçmiş Oturumlar** -MFA kullanarak bir form tabanlı web sitesi ile kullanıcı portalı tümleştirmesini yapılandırın.
- **Güvenilen IP'leri** -güvenilen IP'leri veya aralıkları listesinden kimlik doğrulaması sırasında kullanıcıların tooskip MFA izin verin.

![MFA Sunucusu Kullanıcı Portalı yapılandırması](./media/multi-factor-authentication-get-started-portal/config.png)

Azure multi-Factor Authentication sunucusu hello kullanıcı portalı için çeşitli seçenekler sağlar. Merhaba aşağıdaki tabloda bu seçeneklerin ve ne için kullanıldıkları bir açıklama listesini sağlar.

| Kullanıcı Portalı Ayarları | Açıklama |
|:--- |:--- |
| Kullanıcı Portalı URL’si | Merhaba portal barındırıldığı hello URL'sini girin. |
| Birincil kimlik doğrulama | Kimlik doğrulama toouse Hello türü toohello Portalı'nda oturum açarken belirtin. Windows, Radius veya LDAP kimlik doğrulaması. |
| Kullanıcıların toolog izin ver | Kullanıcıların tooenter hello oturum açma sayfasında hello kullanıcı portalı için bir kullanıcı adı ve parola verin. Bu seçenek seçilmezse hello kutuları gri görünür. |
| Kullanıcı kaydına izin ver | Bir kullanıcı tooenroll, onları telefon numarası gibi ek bilgi ister tooa Kurulumu ekranına gerçekleştirerek çok faktörlü kimlik doğrulamasına izin verin. Yedek telefon kullanıcıları toospecify ikincil bir telefon numarası sağlar ister. OATH belirteci üçüncü taraf istemi kullanıcıların toospecify bir üçüncü taraf OATH belirtecini sağlar. |
| Kullanıcıların tooinitiate bir kerelik geçiş izin ver | Kullanıcıların tooinitiate bir kerelik geçiş izin verin. Bu seçenek bir kullanıcı kurar, bu efekti hello hello kullanıcı oturum açtığında sonraki zaman alır. Atlama saniye hello varsayılan değeri 300 saniye değiştirebilmeniz için bu hello kullanıcı içeren bir kutu sağlar. Aksi takdirde hello bir kerelik atlama yalnızca 300 saniye iyi olur. |
| Kullanıcıların tooselect yöntemi | Kullanıcıların toospecify kendi birincil iletişim yöntemine izin verir. Bu yöntem telefon araması, SMS, mobil uygulama veya OATH belirteci olabilir. |
| Kullanıcıların tooselect dil izin ver | Kullanıcıların hello telefon araması, SMS mesajı, mobil uygulama veya OATH belirteci için kullanılan toochange hello dil izin verin. |
| Kullanıcıların tooactivate mobil uygulamanın izin ver | Kullanıcıların toogenerate hello sunucusu ile kullanılan bir etkinleştirme kodu toocomplete hello mobil uygulama etkinleştirme işlemini izin verir.  Bunlar etkinleştirebilir aygıtları hello sayısını da ayarlayabilirsiniz hello uygulaması, 1 ile 10 arasında. |
| Geri dönüş için güvenlik sorularını kullan | İki aşamalı doğrulamanın başarısız olması halinde güvenlik sorularının kullanılmasını sağlar. Başarılı bir şekilde yanıtlanması gereken güvenlik sorusu hello sayısını belirtebilirsiniz. |
| Kullanıcıların tooassociate üçüncü taraf OATH belirteci izin ver | Kullanıcıların toospecify bir üçüncü taraf OATH belirteci izin verir. |
| Geri dönüş için OATH belirtecini kullan | İki aşamalı doğrulama başarılı olmayan olasılığına hello bir OATH belirteci kullanımına izin verin. Dakika cinsinden hello oturum zaman aşımı süresini de belirtebilirsiniz. |
| Günlü kaydını etkinleştir | Merhaba kullanıcı portalında günlük kaydını etkinleştirin. Merhaba günlük dosyaları şu adreste bulunabilir: C:\Program Files\Multi-Factor Authentication Server\Logs. |

Bu ayarları hello portalında görünür toohello kullanıcı etkinleştirildikten sonra toohello Kullanıcı Portalı'nda imzalanmış haline gelir.

![Kullanıcı portalı ayarları](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Self servis kullanıcı kaydı

Kullanıcıların toosign istediğiniz ve kaydetme, hello seçmelisiniz **kullanıcılar toolog izin** ve **kullanıcı kaydına izin ver** seçenekleri hello ayarları sekmesi altında. Seçtiğiniz hello ayarları hello kullanıcı oturum açma deneyimini etkileyen unutmayın.

Bir kullanıcı hello için toohello kullanıcı portalında ilk kez oturum açtığında, örneğin, bunlar ardından toohello Azure multi-Factor Authentication Kullanıcı Kurulumu sayfasına yönlendirilirsiniz. Merhaba kullanıcı olabilir nasıl Azure multi-Factor Authentication yapılandırdığınıza bağlı olarak, kendi kimlik doğrulama yöntemini mümkün tooselect olabilir.

Merhaba sesli arama doğrulama yöntemi seçin veya önceden yapılandırılmış toouse bu yöntem silinmiş hello sayfasında birincil telefon numarasını ve varsa dahili hello kullanıcı tooenter istenir. Ayrıca olabilir tooenter yedek bir telefon numarası izin verilir.

![Birincil ve yedek telefon numaralarını kaydetme](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Merhaba kullanıcı kimlik doğrulaması sırasında bir PIN gerekli toouse ise, başlangıç sayfasında bunları toocreate bir PIN istenir. Kendi telefon numaraları ve PIN (eğer varsa) girdikten sonra hello hello kullanıcı **Şimdi beni tooAuthenticate** düğmesi. Azure multi-Factor Authentication telefon araması doğrulama toohello kullanıcının birincil telefon numarası gerçekleştirir. Merhaba kullanıcı hello aramayı yanıtlamalı ve PIN'ini (varsa) girin ve # toomove toohello üzerinde hello Self Servis kayıt işleminin sonraki adımı tuşuna basın.

Hello kullanıcı hello metin iletisi doğrulama yöntemini seçerse ya da bu yöntemi önceden yapılandırılmış toouse bırakıldı, hello sayfa kullanıcıdan birincil telefonu numarasını hello kullanıcıya sorar. Kimlik doğrulaması sırasında hello kullanıcı bir PIN gerekli toouse ise, hello sayfasında bunları da tooenter bir PIN istenir.  Kendi telefon numarasını ve PIN'ini (varsa) girdikten sonra hello hello kullanıcı **bana şimdi mesaj tooAuthenticate** düğmesi. Bir SMS doğrulama toohello kullanıcının cep telefonu Azure çok faktörlü kimlik doğrulaması gerçekleştirir. Merhaba kullanıcı, bir-zamanlı-geçiş kodu (OTP) içeren hello kısa mesaj sonra bu OTP'nin yanı sıra kendi PIN'ini (varsa) ile yanıtlar toohello iletisi alır.

![Kullanıcı portalı SMS](./media/multi-factor-authentication-get-started-portal/text.png)

Merhaba kullanıcı hello mobil uygulama doğrulama yöntemini seçerse, hello sayfa cihazlarında hello kullanıcı tooinstall hello Microsoft Authenticator uygulamasını ister ve bir etkinleştirme kodu oluşturmak. Merhaba uygulamasını yükledikten sonra hello kullanıcı hello etkinleştirme kodu Oluştur düğmesine tıklar.

> [!NOTE]
> toouse hello Microsoft Authenticator uygulaması hello kullanıcı kendi cihazı için anında iletme bildirimleri etkinleştirmelisiniz.

Başlangıç sayfası, daha sonra bir etkinleştirme kodu ve URL bir barkod resmi ile birlikte görüntüler. Kimlik doğrulaması sırasında hello kullanıcı bir PIN gerekli toouse ise, hello sayfa bunları ayrıca tooenter bir PIN ister. Merhaba kullanıcı hello Microsoft Authenticator uygulamaya hello etkinleştirme kodu ve URL'yi girer ya da hello barkod tarayıcısı tooscan hello barkod resmini kullanır ve hello etkinleştir düğmesine tıklar.

Merhaba Etkinleştirme tamamlandıktan sonra hello hello kullanıcı **şimdi Kimliğimi doğrula** düğmesi. Doğrulama toohello kullanıcının mobil uygulamasına Azure çok faktörlü kimlik doğrulaması gerçekleştirir. Merhaba kullanıcı PIN'ini (varsa) girin ve toohello üzerinde hello Self Servis kayıt işleminin sonraki adımı kendi mobil uygulama toomove hello kimlik doğrulaması yap düğmesine basın.

Merhaba Yöneticiler hello Azure çok faktörlü kimlik doğrulama sunucusu toocollect güvenlik sorularını ve yanıtlarını yapılandırdıysanız, hello kullanıcı ardından toohello güvenlik soruları sayfasına alınır. Hello kullanıcı dört güvenlik sorusu seçin ve seçili tootheir soruları yanıtlar sağlamanız gerekir.

![Kullanıcı portalı güvenlik soruları](./media/multi-factor-authentication-get-started-portal/secq.png)

Merhaba kullanıcı kendi kendine kayıt tamamlanmıştır ve hello kullanıcı toohello Kullanıcı Portalı'nda imzalanır. Kendi yöntemlerini değiştirme, yöneticileri izin verilip verilmediğini kullanıcılar geri toohello Kullanıcı Portalı'nda hello gelecekteki toochange herhangi bir zamanda kendi telefon numaralarını, PIN, kimlik doğrulama yöntemleri ve güvenlik sorularını oturum açabilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Hello Azure çok faktörlü kimlik doğrulama sunucusu mobil uygulama Web Hizmeti'ni dağıtma](multi-factor-authentication-get-started-server-webservice.md)
