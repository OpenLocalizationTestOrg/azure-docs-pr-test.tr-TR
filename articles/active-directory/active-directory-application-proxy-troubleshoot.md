---
title: Uygulama proxy'si aaaTroubleshoot | Microsoft Docs
description: "Kapak nasıl Azure AD uygulama proxy'si tootroubleshoot hatalar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Uygulama proxy'si sorunları ve hata iletileri sorunlarını giderme
Yayımlanmış bir uygulamanın erişme veya yayımlama uygulamalarda hatalar meydana gelirse, Microsoft Azure AD uygulama proxy'si düzgün çalışıp çalışmadığını seçenekleri toosee aşağıdaki hello denetleyin:

* Açık hello Windows Hizmetleri konsol ve o hello doğrulayın **Microsoft AAD Application Proxy Connector** hizmetidir etkin ve çalışıyor. Ayrıca hello görüntü aşağıdaki gösterildiği gibi hello uygulama proxy'si hizmeti özellikleri sayfasında, toolook isteyebilirsiniz:  
  ![Microsoft AAD uygulama Proxy Bağlayıcısı özellikleri penceresinin ekran görüntüsü](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Olay Görüntüleyicisi'ni açın ve uygulama Proxy Bağlayıcısı olayları arayın **uygulama ve hizmet günlükleri** > **Microsoft** > **AadApplicationProxy** > **bağlayıcı** > **yönetici**.
* Gerekli olursa, daha ayrıntılı günlükler tarafından [açma hello uygulama Proxy Bağlayıcısı oturum günlükleri](application-proxy-understand-connectors.md#under-the-hood).

Hello Azure AD sorun giderme aracı hakkında daha fazla bilgi için bkz: [aracı toovalidate bağlayıcı ağ Önkoşullar sorun giderme](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>Merhaba sayfa doğru işlenmez
İşleme veya yanlış özel hata iletileri almadan çalışmıyor uygulamanız ile ilgili sorunlar olabilir. Hello makale yolu yayımlanan ancak Merhaba uygulaması dışında yol mevcut içeriği gerektiren bu durum ortaya çıkabilir.

Örneğin, hello yolu https://yourapp/app yayımlama ancak hello uygulama görüntüleri içinde https://yourapp/media çağırır, bunlar işlenip olmaz. Tüm ilgili içeriği tooinclude ihtiyacınız hello yüksek düzey yolu kullanarak hello uygulama yayımlama emin olun. Bu örnekte, http://yourapp/ olacaktır.

Yol tooinclude başvurulan içeriği değiştirmek, ancak yine de kullanıcıların tooland hello yolundaki daha derin bir bağlantıyı gerekir, bkz: hello blog yayını [ayarı hello sağ bağlantısını uygulama proxy'si uygulamalarda hello Azure AD erişim paneli ve Office 365 uygulama Başlatıcı](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Bağlayıcı hataları

Kullanım hello [Azure AD uygulama Proxy Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify Bağlayıcınızı hello uygulama proxy'si hizmeti ulaşabilirsiniz. En azından hello Orta ABD bölgesi ve hello bölgeye en yakın tooyou tüm yeşil onay işaretli olduğundan emin olun. Bunun ötesinde, daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir. 

Kayıt sırasında hello Bağlayıcı Sihirbazı'nı yükleme başarısız olursa, tooview hello hello başarısızlık nedeni iki yolu vardır. Ya da Ara hello olay günlüğünde altında **uygulamaları ve Hizmetleri Logs\Microsoft\AadApplicationProxy\Connector\Admin**, veya aşağıdaki Windows PowerShell komutunu çalıştırma hello:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Merhaba bağlayıcı hata hello olay günlüğünden bulduktan sonra ortak hataları tooresolve hello sorununun bu tabloyu kullanın:

| Hata | Önerilen adımlar |
| ----- | ----------------- |
| Bağlayıcı kaydı başarısız oldu: etkin hello Azure Yönetim Portalı'nda uygulama proxy'si ve Active Directory kullanıcı adınızı ve parolanızı doğru girdiğinizden emin olun. Hata: 'bir veya daha fazla hata oluştu.' | Merhaba kaydı penceresi tooAzure AD imzalamadan kapattıysanız, hello Bağlayıcı Sihirbazı'nı yeniden çalıştırın ve hello bağlayıcı kaydedin. <br><br> Merhaba kaydı penceresi açılır ve toolog içinde vermeden hemen kapatılır, büyük olasılıkla bu hatayı alırsınız. Sisteminizde bir ağ hatası olduğunda bu hata oluşur. Bir tarayıcı tooa ortak Web sitesinden olası tooconnect olduğunu ve hello bağlantı noktalarını belirtildiği şekilde açık olduğundan emin olun [uygulama ara sunucusu önkoşulları](active-directory-application-proxy-enable.md). |
| NET hata hello kayıt pencerede sunulur. Devam edilemiyor. | Bu hatayı görürseniz ve hello penceresi kapanır hello yanlış kullanıcı adı ya da parola girdi. Yeniden Deneyin. |
| Bağlayıcı kaydı başarısız oldu: etkin hello Azure Yönetim Portalı'nda uygulama proxy'si ve Active Directory kullanıcı adınızı ve parolanızı doğru girdiğinizden emin olun. Hata: ' AADSTS50059: hiçbir Kiracı tanımlama bilgileri ya da hello istekte bulunan veya asıl URI başarısız oldu, kimlik bilgileri ve arama hizmeti tarafından sağlanan herhangi tarafından kapsanan. | Toosign çalıştığınız Microsoft Account ve hello kuruluş kimliği hello dizininin parçası olan bir etki alanı değil kullanarak tooaccess çalışıyorsunuz. Bu hello Yöneticisi hello parçası olduğundan emin olun hello Kiracı etki alanı, örneğin, etki alanı adıyla aynı hello Azure AD etki alanı contoso.com ise hello Yöneticisi olmalıdır admin@contoso.com. |
| PowerShell komut dosyaları çalıştırmak için tooretrieve hello geçerli yürütme İlkesi başarısız oldu. | Merhaba Bağlayıcısı yükleme başarısız olursa, PowerShell yürütme ilkesini devre dışı olduğundan emin toomake denetleyin. <br><br>1. Merhaba Grup İlkesi Düzenleyicisi'ni açın.<br>2. Çok Git**Bilgisayar Yapılandırması** > **Yönetim Şablonları** > **Windows bileşenleri**  >   **Windows PowerShell** çift tıklayın ve **komut dosyası yürütme kapatma**.<br>3. hello yürütme İlkesi tooeither ayarlanabilir **yapılandırılmamış** veya **etkin**. Varsa çok ayarlamak**etkin**seçenekleri altında olduğundan emin olun, hello yürütme İlkesi tooeither ayarlanmış **yerel ve uzak imzalanmış komut dosyalarını izin** veya çok**tüm komut dosyalarına izin**. |
| Bağlayıcı toodownload hello yapılandırması başarısız oldu. | kimlik doğrulaması için kullanılır, hello bağlayıcı'nın istemci sertifikasının süresi doldu. Bağlayıcısı bir proxy'nin arkasında yüklü hello varsa, bu da oluşabilir. Bu durumda, hello bağlayıcı hello Internet erişemez ve mümkün tooprovide uygulamaları tooremote kullanıcılar olmayacaktır. Güven hello kullanarak el ile yenileme `Register-AppProxyConnector` Windows PowerShell cmdlet'i. Bağlayıcınızı bir proxy'nin arkasında, gerekli toogrant Internet erişimi toohello bağlayıcı hesapları "Ağ Hizmetleri" ve "yerel sistem." ise, Bu gerçekleştirilebilir vererek toohello Proxy erişmesine veya ayarlayarak bunları toobypass proxy hello. |
| Bağlayıcı kaydı başarısız oldu: Active Directory tooregister hello bağlayıcı genel Yöneticisi olduğundan emin olun. Hata: 'hello kayıt isteği reddedildi.' | Bu etki alanı yönetici ile toolog çalıştığınız hello diğer ad değil. Bağlayıcınızı hello kullanıcının etki alanı sahibi hello dizin için her zaman yüklenir. Merhaba yönetici hesabı ile toosign çalıştığınız genel izinleri toohello Azure AD Kiracı sahip olduğundan emin olun. |

## <a name="kerberos-errors"></a>Kerberos hataları

Bu tabloda daha yaygın hello yer almaktadır Kerberos kurulumu ve yapılandırması dönün ve çözümü için öneriler içermektedir hatalar.

| Hata | Önerilen adımlar |
| ----- | ----------------- |
| PowerShell komut dosyaları çalıştırmak için tooretrieve hello geçerli yürütme İlkesi başarısız oldu. | Merhaba Bağlayıcısı yükleme başarısız olursa, PowerShell yürütme ilkesini devre dışı olduğundan emin toomake denetleyin.<br><br>1. Merhaba Grup İlkesi Düzenleyicisi'ni açın.<br>2. Çok Git**Bilgisayar Yapılandırması** > **Yönetim Şablonları** > **Windows bileşenleri**  >   **Windows PowerShell** çift tıklayın ve **komut dosyası yürütme kapatma**.<br>3. hello yürütme İlkesi tooeither ayarlanabilir **yapılandırılmamış** veya **etkin**. Varsa çok ayarlamak**etkin**seçenekleri altında olduğundan emin olun, hello yürütme İlkesi tooeither ayarlanmış **yerel ve uzak imzalanmış komut dosyalarını izin** veya çok**tüm komut dosyalarına izin**. |
| 12008 - azure AD aşıldı hello sayısı izin verilen Kerberos kimlik doğrulaması toohello arka uç sunucusu çalışır. | Bu hata yanlış yapılandırma Azure AD arasında belirtmek ve arka uç hello uygulama sunucusu ya da her iki makinede saat ve tarih yapılandırmasında bir sorun. Merhaba arka uç sunucusuna Azure AD tarafından oluşturulan hello Kerberos biletini reddetti. Doğrulayın, Azure AD ve hello arka uç uygulama sunucusu doğru şekilde yapılandırılır. Başlangıç saati ve tarihi yapılandırmasına hello Azure AD ve hello arka uç uygulama sunucusu eşitlendiğinden emin olun. |
| 13016 - hiçbir UPN hello edge'de belirteç veya olmadığından hello erişim tanımlama bilgisinde azure AD hello kullanıcı adına bir Kerberos anahtarı alınamıyor. | Merhaba STS yapılandırmasında bir sorun yoktur. UPN Talebi hello yapılandırma hello STS düzeltin. |
| 13019 - azure AD Genel API hatası aşağıdaki hello nedeniyle hello kullanıcı adına bir Kerberos anahtarı alınamıyor. | Bu olay Azure AD arasında yanlış yapılandırma gösterebilir ve hello etki alanı denetleyici sunucusu veya her iki makinede saat ve tarih yapılandırmasında bir sorun. Merhaba etki alanı denetleyicisi Azure AD tarafından oluşturulan hello Kerberos biletini reddetti. Doğrulayın, Azure AD ve hello arka uç uygulama sunucusu doğru bir şekilde yapılandırıldığını, özellikle SPN hello yapılandırma. Hello Azure AD etki alanına katılmış toohello olduğundan emin olun aynı etki alanında etki alanı denetleyicisi hello etki alanı denetleyicisi tooensure hello olarak Azure AD ile güven oluşturur. Başlangıç saati ve tarihi yapılandırmasına hello Azure AD ve hello etki alanı denetleyicisi eşitlendiğinden emin olun. |
| 13020 - Merhaba arka uç sunucu SPN'si tanımlanmadığından azure AD hello kullanıcı adına bir Kerberos anahtarı alınamıyor. | Bu olay Azure AD arasında yanlış yapılandırma gösterebilir ve hello etki alanı denetleyici sunucusu veya her iki makinede saat ve tarih yapılandırmasında bir sorun. Merhaba etki alanı denetleyicisi Azure AD tarafından oluşturulan hello Kerberos biletini reddetti. Doğrulayın, Azure AD ve hello arka uç uygulama sunucusu doğru bir şekilde yapılandırıldığını, özellikle SPN hello yapılandırma. Hello Azure AD etki alanına katılmış toohello olduğundan emin olun aynı etki alanında etki alanı denetleyicisi hello etki alanı denetleyicisi tooensure hello olarak Azure AD ile güven oluşturur. Başlangıç saati ve tarihi yapılandırmasına hello Azure AD ve hello etki alanı denetleyicisi eşitlendiğinden emin olun. |
| 13022 - çünkü bir HTTP 401 hata ile tooKerberos kimlik doğrulama girişimlerini Hello arka uç sunucusuna yanıtlar azure AD hello kullanıcının kimliğini doğrulayamıyor. | Bu olay Azure AD arasında yanlış yapılandırma belirtmek ve arka uç hello uygulama sunucusu ya da her iki makinede saat ve tarih yapılandırmasında bir sorun. Merhaba arka uç sunucusuna Azure AD tarafından oluşturulan hello Kerberos biletini reddetti. Doğrulayın, Azure AD ve hello arka uç uygulama sunucusu doğru şekilde yapılandırılır. Başlangıç saati ve tarihi yapılandırmasına hello Azure AD ve hello arka uç uygulama sunucusu eşitlendiğinden emin olun. |

## <a name="end-user-errors"></a>Son kullanıcı hataları

Bu liste tooaccess hello uygulamayı deneyin ve başarısız olduğunda, son kullanıcılarınızın karşılaşabileceğiniz hataları kapsar. 

| Hata | Önerilen adımlar |
| ----- | ----------------- |
| Merhaba Web sitesi hello sayfa görüntülenemiyor. | Kullanıcı hello uygulama IWA uygulama ise, yayımlanan tooaccess hello uygulama çalışırken bu hatayı alabilirsiniz. Bu uygulama yanlış için hello SPN tanımlanmış. IWA uygulamaları için o hello bu uygulama için yapılandırılan SPN doğru olduğundan emin olun. |
| Merhaba Web sitesi hello sayfa görüntülenemiyor. | Kullanıcı hello uygulama OWA uygulama ise, yayımlanan tooaccess hello uygulama çalışırken bu hatayı alabilirsiniz. Bunun nedeni hello aşağıdakilerden biri:<br><li>Bu uygulama yanlış için hello SPN tanımlanır. Bu hello bu uygulama için yapılandırılan SPN doğru olduğundan emin olun.</li><li>tooaccess Merhaba uygulaması çalıştı hello kullanıcının bir Microsoft hesabı kullanarak yerine hello uygun şirket hesabı toosign veya hello kullanıcı bir konuk kullanıcıdır. Eşleşme hello etki alanını hello şirket hesabındaki kullanarak yapma emin hello kullanıcı işaretlerini uygulama yayımlanır. Microsoft Account kullanıcıları ve Konuk IWA uygulamaları erişemez.</li><li>tooaccess Merhaba uygulaması çalıştı hello kullanıcının hello şirket içi tarafında bu uygulama için düzgün tanımlanmadı. Bu kullanıcı hello şirket içi makinede bu arka uç uygulaması için tanımlanan hello uygun izinlere sahip olduğundan emin olun. |
| Bu şirket uygulama erişilemiyor. Bu uygulama yetkili değil tooaccess olan. Yetkilendirme başarısız oldu. Erişim toothis uygulama emin tooassign hello kullanıcıyla olun. | Kullanıcılarınızın, kullanıcılar kendi Kurumsal hesap toosign yerine Microsoft hesapları kullanıyorsanız, yayımlanan tooaccess hello uygulama çalışırken bu hatayı alabilirsiniz. Konuk kullanıcılar da bu hatayı alabilirsiniz. Microsoft Account kullanıcılar ve konuklar IWA uygulamaları erişemez. Eşleşme hello etki alanını hello şirket hesabındaki kullanarak yapma emin hello kullanıcı işaretlerini uygulama yayımlanır.<br><br>Bu uygulama için hello kullanıcı atanmamış. Toohello Git **uygulama** sekmesinde ve altında **kullanıcılar ve gruplar**, bu kullanıcı veya kullanıcı grubu toothis uygulama atayın. |
| Bu şirket uygulama şu anda erişilemiyor. Lütfen daha sonra yeniden... zaman aşımına uğradı hello bağlayıcı deneyin. | Kullanıcılarınızın, bunların düzgün şekilde hello şirket içi tarafında bu uygulama için tanımlanmazsa, yayımlanan tooaccess hello uygulama çalışırken bu hatayı alabilirsiniz. Kullanıcılarınızın hello şirket içi makinede bu arka uç uygulaması için tanımlanan hello uygun izinlere sahip olduğunuzdan emin olun. |
| Bu şirket uygulama erişilemiyor. Bu uygulama yetkili değil tooaccess olan. Yetkilendirme başarısız oldu. Azure Active Directory Premium veya Basic hello kullanıcı bir lisans olduğundan emin olun. | Kullanıcılarınızın, bunlar açıkça Premium/temel lisansıyla hello abonenin yönetici tarafından doğru atanmışsa, yayımlanan tooaccess hello uygulama çalışırken bu hatayı alabilirsiniz. Active Directory toohello abonenin Git **lisansları** sekmesinde ve bu kullanıcı veya kullanıcı grubunun bir Premium veya Basic lisansı atanmış olduğundan emin olun. |

## <a name="my-error-wasnt-listed-here"></a>My hata burada listelenen değildi

Bir hata veya sorun bu sorun giderme Kılavuzu'nda listelenmiyor Azure AD uygulama proxy'si ile karşılaşırsanız, ilgili toohear isteriz. Bir e-posta tooour Gönder [geri bildirim takım](mailto:aadapfeedback@microsoft.com) hello ayrıntılarıyla, hello karşılaşıldı.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory Uygulama Ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md)
* [Uygulama proxy'si ile uygulama yayımlama](active-directory-application-proxy-publish.md)
* [Çoklu oturum açmayı etkinleştir](active-directory-application-proxy-sso-using-kcd.md)
* [Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
