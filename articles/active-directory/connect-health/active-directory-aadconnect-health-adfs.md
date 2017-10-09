---
title: AD FS ile Azure AD Connect Health aaaUsing | Microsoft Docs
description: "Hello Azure AD Connect Health sayfasında nasıl budur toomonitor şirket içi AD FS altyapısı."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>AD FS'yi Azure AD Connect Health'i kullanarak izleme
Merhaba belgeleri belirli toomonitoring, Azure AD Connect Health ile AD FS altyapısıdır. Azure AD Connect’i (Eşitleme) Azure AD Connect Health ile izleme hakkında bilgi için bkz. [Eşitleme için Azure AD Connect Health Kullanma](active-directory-aadconnect-health-sync.md). Ek olarak, Active Directory Etki Alanı Hizmetleri’ni Azure AD Connect Health ile izleme hakkında bilgi için bkz. [AD DS ile Azure AD Connect Health Kullanma](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>AD FS uyarıları
Hello Azure AD Connect Health uyarıları bölümünde etkin uyarıların listesi hello sağlar. Her uyarı ilgili bilgileri, çözüm adımları ve bağlantıları toorelated belgeleri içerir.

Bir etkin veya çözümlenmiş uyarı, tooopen ek bilgileri içeren yeni bir dikey pencere çift tıklayarak, uyarı ve bağlantıları toorelevant belgelerine tooresolve atabileceğiniz adımlar hello. Ayrıca, geçmiş verileri hello geçmişte çözümlenen uyarıları görüntüleyebilirsiniz.

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>AD FS için Kullanım Analizi
Azure AD Connect Health kullanım analizi, Federasyon sunucularınızın hello kimlik doğrulama trafiğini analiz eder. Merhaba kullanım analizi kutusunu, çeşitli ölçümleri ve gruplandırmaları gösteren tooopen hello kullanım analizi dikey penceresi, çift tıklayabilirsiniz.

> [!NOTE]
> AD FS ile kullanım analizi toouse, AD FS denetiminin etkin olduğundan emin olmalısınız. Daha fazla bilgi için bkz. [AD FS için Denetimi Etkinleştirme](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/report1.png)

tooselect ek ölçümler, bir zaman aralığı ya da toochange hello gruplandırma belirtin, hello kullanım analizi grafiğine sağ tıklayın ve grafiği Düzenle seçin. Ardından hello zaman aralığı belirtin, farklı bir ölçümü seçin ve hello gruplandırmayı değiştirebilirsiniz. Merhaba dağıtım hello kimlik doğrulama trafiğinin farklı "ölçümlere" göre görüntüleyebilir ve bölümden hello açıklanan ilgili "gruplandırma ölçütü" parametrelerini kullanarak her ölçümü gruplandırabilirsiniz:

**Ölçüm: Toplam İstek Sayısı** - AD FS sunucuları tarafından işlenen toplam istek sayısı.

|Gruplandırma Ölçütü | Hangi hello gruplandırma anlamına gelir ve neden yararlıdır? |
| --- | --- |
| Tümü | Tüm AD FS sunucuları tarafından işlenen isteklerin toplam sayısı Hello sayısını gösterir.|
| Uygulama | Grupları hello hedeflenen bağlı olan tarafa göre toplam istek sayısı hello. Hangi uygulamanın ne kadar hello toplam trafik yüzdesi alıyor yararlı toounderstand grubudur. |
|  Sunucu |Grupları hello istek işlenmeden hello sunucuya göre toplam istek sayısı hello. Bu yararlı toounderstand hello yük dağıtımı hello toplam trafik grubudur.
| Çalışma Alanına Katılım |Grupları olup bunların çalışma alanına katılmış olan cihazlardan gelip temel toplam istek (bilinen) hello. Bu gruplandırma, kaynaklarınızı bilinmeyen toohello kimlik altyapısı cihazları kullanarak erişilen yararlı toounderstand olur. |
|  Kimlik Doğrulama Yöntemi | Grupları toplam istekleri kimlik doğrulaması için kullanılan hello kimlik doğrulama yöntemine dayalı hello. Bu gruplandırma, kimlik doğrulaması için kullanılan yararlı toounderstand hello ortak kimlik doğrulama yöntemidir. Merhaba olası kimlik doğrulama yöntemleri aşağıda verilmiştir <ol> <li>Windows Tümleşik Kimlik Doğrulaması (Windows)</li> <li>Forms Tabanlı Kimlik Doğrulaması (Forms)</li> <li>SSO (Çoklu Oturum Açma)</li> <li>X509 Sertifika Doğrulaması (Sertifika)</li> <br>Merhaba federasyon sunucuları hello isteği SSO tanımlama bilgisi alırsanız, bu isteğin SSO (çoklu oturum tam açma) sayılır. Böyle durumlarda, hello tanımlama bilgisi geçerliyse, hello kullanıcı tooprovide kimlik bilgileri istenmez ve kesintisiz erişim toohello uygulama alır. Bu davranış, hello federasyon sunucuları tarafından korunan birden çok bağlı olan tarafınız varsa yaygındır. |
| Ağ Konumu | Grupları hello kullanıcının ağ konumuna hello dayalı toplam istek sayısı hello. İntranet veya extranet olabilir. Bu yararlı tooknow hello intranet ve extranet hello trafiğin yüzde kaçının geldiği grubudur. |


**Ölçüm: Toplam isteği başarısız oldu** -başarısız hello Federasyon Hizmeti tarafından işlenen isteklerin hello toplam sayısı. (Bu ölçüm yalnızca Windows Server 2012 R2 için AD FS'de kullanılabilir)

|Gruplandırma Ölçütü | Hangi hello gruplandırma anlamına gelir ve neden yararlıdır? |
| --- | --- |
| Hata Türü | Merhaba önceden tanımlanmış hata türlerine göre hata sayısını gösterir. Bu yararlı toounderstand hello genel hata türlerini grubudur. <ul><li>Yanlış kullanıcı adı veya parola: tooincorrect kullanıcı adı veya parola nedeniyle hatalar.</li> <li>"Extranet kilitleme": extranet dışında bırakılan bir kullanıcıdan alınan toohello isteği nedeniyle hataları </li><li> "Süresi dolan parola": süresi dolmuş bir parolayla oturum açma toousers nedeniyle hataları.</li><li>"Devre dışı hesap": toousers günlüğü devre dışı bırakılmış bir hesap ile son hataları.</li><li>"Cihaz kimlik doğrulaması": cihaz kimlik doğrulamasını kullanarak toousers başarısız tooauthenticate nedeniyle hataları.</li><li>"Kullanıcı sertifikası kimlik doğrulaması": geçersiz bir sertifika nedeniyle toousers başarısız tooauthenticate nedeniyle hataları.</li><li>"MFA": çok faktörlü kimlik doğrulaması kullanarak toouser başarısız tooauthenticate nedeniyle hataları.</li><li>"Diğer kimlik bilgisi": "Sertifika verme yetkilendirmesi": tooauthorization hataları nedeniyle hataları.</li><li>"Sertifika verme Temsilcisi": tooissuance temsilci hatalar nedeniyle hataları.</li><li>"Belirteç onayı": tooADFS reddetme nedeniyle hataları hello bir üçüncü taraf kimlik sağlayıcısından belirteç.</li><li>"Protokolü": tooprotocol hataları nedeniyle başarısız.</li><li>"Bilinmeyen": Farklı nedenlerden kaynaklananlar. Merhaba uymayan diğer hataları kategorileri tanımlanır.</li> |
| Sunucu | Grupları hello sunucuya göre hatalar hello. Bu yararlı toounderstand hello hata dağıtım sunucular arasında grubudur. Düzensiz dağıtım, hatalı durumdaki bir sunucunun göstergesi olabilir. |
| Ağ Konumu | Grupları hello isteklerinin (intranet veya extranet) hello ağ konumuna bağlı hataları hello. Bu gruplandırma, başarısız olan istek yararlı toounderstand hello türü değil. |
|  Uygulama | Grupları hello hedeflenen uygulamaya (bağlı olan taraf) göre hataları hello. Hedeflenen hangi uygulamanın en çok hata sayısını gördüğünü yararlı toounderstand grubudur. |

**Ölçüm: Kullanıcı sayısı** - Kimlik doğrulamak için etkin olarak AD FS’yi kullanan ortalama benzersiz kullanıcı sayısı

|Gruplandırma Ölçütü | Hangi hello gruplandırma anlamına gelir ve neden yararlıdır? |
| --- | --- |
|Tümü |Bu ölçüm hello seçilen bir zaman dilimi içinde hello Federasyon Hizmeti kullanan kullanıcıların ortalama sayısını sayısını sağlar. Merhaba kullanıcılar gruplandırılmaz. <br>Merhaba ortalama seçili hello saat dilimine bağlıdır. |
| Uygulama |Grupları hello kullanıcıların ortalama sayısı üzerinde hello tabanlı uygulama (bağlı olan taraf) hedeflenen. Bu yararlı toounderstand grubudur kaç kullanıcının hangi uygulamayı kullanmakta olduğunu. |

## <a name="performance-monitoring-for-ad-fs"></a>AD FS için Performans İzleme
Azure AD Connect Health Performans İzleme, ölçümlere ilişkin izleme bilgileri sağlar. Hello izleme kutusunu seçtiğinizde, hello ölçümleri hakkında ayrıntılı bilgi içeren yeni bir dikey pencere açar.

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/perf1.png)

Merhaba dikey penceresinde hello üstündeki Hello filtre seçeneğini seçerek, her bir sunucunun ölçümlerini sunucu toosee göre filtreleyebilirsiniz. toochange ölçüm dikey izleme hello altında grafik izleme hello sağ tıklayın ve grafiği Düzenle (veya select hello grafiği Düzenle düğmesi) seçin. Açılan hello yeni dikey penceresinden, ek ölçümler hello açılan listeden seçin ve hello performans verilerini görüntülemek için bir zaman aralığı belirtin.

## <a name="reports-for-ad-fs"></a>AD FS raporları
Azure AD Connect Health, AD FS'nin etkinlik ve performansı hakkında raporlar sağlar. Bu raporlar, yöneticilerin AD FS sunucularındaki etkinlikler hakkında öngörü edinmelerine yardımcı olur.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Hatalı Kullanıcı Adı/Parola kullanarak oturum açamayan İlk 50 Kullanıcı
Merhaba ortak bir AD FS sunucusunda başarısız kimlik doğrulama isteği nedenlerinden biri geçersiz kimlik bilgileri, diğer bir deyişle, yanlış kullanıcı adı veya parola ile isteğidir. Genellikle son toocomplex parolalar, unutulan parolaları veya yazım hatalarını toousers olur.

Ancak, AD FS sunucularınız tarafından gibi işlenen istekleri beklenmeyen sayıda içinde neden olabilecek diğer nedeni vardır: önbellekleri kullanıcı kimlik bilgilerini ve hello kimlik bilgilerinin süresi dolacak bir uygulama veya bir dizi olan bir hesaba toosign çalışırken kötü niyetli bir kullanıcı iyi bilinen parolalar. Bu iki örnek tooa dalgalanma isteklerine neden olabilecek geçerli nedenleridir.

Azure AD Connect Health ADFS tooinvalid kullanıcı adı veya parola nedeniyle başarısız oturum açma denemesi ile ilk 50 kullanıcı hakkında bir rapor sağlar. Bu rapor hello grupları hello AD FS sunucuları tarafından oluşturulan hello denetim olayları işlenmesiyle sağlanır.

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health-adfs/report1a.png)

Bu rapor içinde bilgi aşağıdaki kolay erişim toohello vardır:

* Merhaba son 30 gün içinde yanlış kullanıcı adı/parola ile başarısız olmuş isteklerin toplam sayısı
* Her gün hatalı kullanıcı adı/parola ile oturum açarak başarısız olan kullanıcıların ortalama sayısı.

Bu bölümü tıklamak ek ayrıntılar sağlanmaktadır toohello ana rapor dikey penceresine götürür. Bu dikey toohelp kurmak istekleriyle yanlış kullanıcı adı veya parola ile ilgili temel bilgileri eğilim ile bir grafik içerir. Ayrıca, başarısız girişim sayısı hello ile ilk 50 kullanıcı hello listesini sağlar.

Merhaba grafiği aşağıdaki bilgilerle hello sağlar:

* Merhaba tooa hatalı kullanıcı adı/parola gün başına temelinde nedeniyle başarısız oturum açmalar toplam sayısı.
* Merhaba gün başına temelinde oturumları başarısız olan benzersiz kullanıcıların toplam sayısı.
* Son istek için istemci IP adresi

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health-adfs/report3a.png)

Merhaba rapor aşağıdaki bilgilerle hello sağlar:

| Rapor Öğesi | Açıklama |
| --- | --- |
| Kullanıcı Kimliği |Kullanılan hello kullanıcı Kimliğini gösterir. Bu değer hangi hello: Bazı durumlarda yanlış kullanıcı kimliği kullanılan hello yazılı kullanıcı. |
| Başarısız Denemeler |Gösterir toplam başarısız girişim sayısı için belirli bir kullanıcı kimliğine hello Merhaba tablo hello azalan düzende başarısız girişim sayısı en ile sıralanır. |
| Son Hata |Merhaba son hatanın oluştuğu sırada hello zaman damgasını gösterir. |
| Son Hata IP’si |Merhaba son hatalı istek Hello istemci IP adresini gösterir. |

> [!NOTE]
> Bu rapor, bu süre içinde her iki saatte hello ile toplanan yeni bilgiler sonra otomatik olarak güncelleştirilir. Sonuç olarak, oturum açma denemesi hello son iki saat içinde hello rapora dahil edilmeyebilir.
>
>

## <a name="related-links"></a>İlgili bağlantılar
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Aracısı Yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health İşlemleri](active-directory-aadconnect-health-operations.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health Sürüm Geçmişi](active-directory-aadconnect-health-version-history.md)