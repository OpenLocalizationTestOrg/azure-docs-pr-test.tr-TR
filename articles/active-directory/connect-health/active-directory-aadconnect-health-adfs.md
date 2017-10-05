---
title: Azure AD Connect Health'i AD FS ile Kullanma| Microsoft Belgeleri
description: "Bu Azure AD Connect Health sayfasında, şirket içi AD FS altyapınızı nasıl izleyeceğiniz açıklanmıştır."
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
ms.openlocfilehash: 7946f11d209e6341caa3a11e946fb1596e758277
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>AD FS'yi Azure AD Connect Health'i kullanarak izleme
Aşağıdaki belgeler, AD FS altyapınızın Azure AD Connect Health ile izlenmesine ilişkin belgelerdir. Azure AD Connect’i (Eşitleme) Azure AD Connect Health ile izleme hakkında bilgi için bkz. [Eşitleme için Azure AD Connect Health Kullanma](active-directory-aadconnect-health-sync.md). Ek olarak, Active Directory Etki Alanı Hizmetleri’ni Azure AD Connect Health ile izleme hakkında bilgi için bkz. [AD DS ile Azure AD Connect Health Kullanma](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>AD FS uyarıları
Azure AD Connect Health Uyarıları bölümünde etkin uyarıların listesi mevcuttur. Her uyarı için ilgili bilgiler, çözüm adımları ve ilgili belgelere yönelik bağlantılar verilmiştir.

Ek bilgiler, uyarıyı çözme adımları ve ilgili belgelerin bağlantılarını içeren yeni bir dikey pencere açmak için etkin veya çözümlenmiş bir uyarıya çift tıklayabilirsiniz. Ayrıca, geçmişte çözümlenen uyarılara ilişkin geçmiş verileri de görüntüleyebilirsiniz.

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>AD FS için Kullanım Analizi
Azure AD Connect Health Kullanım Analizi, federasyon sunucularınızın kimlik doğrulama trafiğini analiz eder. Birkaç ölçüm ve gruplandırmayı gösteren kullanım analizi dikey penceresini açmak için kullanım analizi kutusuna çift tıklayabilirsiniz.

> [!NOTE]
> Kullanım Analizini AD FS ile kullanabilmek için AD FS denetiminin etkin olduğundan emin olmanız gerekir. Daha fazla bilgi için bkz. [AD FS için Denetimi Etkinleştirme](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/report1.png)

Ek ölçümler seçmek, zaman aralığı belirtmek veya gruplandırmayı değiştirmek için kullanım analizi grafiğine sağ tıklayıp Grafiği Düzenle seçeneğini belirleyin. Ardından zaman aralığı belirtebilir, farklı bir ölçüm seçebilir ve gruplandırmayı değiştirebilirsiniz. Kimlik doğrulama trafiğinin dağılımını farklı "ölçümlere" göre görüntüleyebilir ve aşağıdaki bölümde açıklanan ilgili "gruplandırma ölçütü" parametrelerini kullanarak her ölçümü gruplandırabilirsiniz:

**Ölçüm: Toplam İstek Sayısı** - AD FS sunucuları tarafından işlenen toplam istek sayısı.

|Gruplandırma Ölçütü | Gruplandırma nedir ve ne işe yarar? |
| --- | --- |
| Tümü | Tüm AD FS sunucuları tarafından işlenen isteklerin toplam sayısını gösterir.|
| Uygulama | Tüm istekleri hedeflenen bağlı olan tarafa göre gruplandırır. Bu gruplandırma, hangi uygulamanın toplam trafiğin yüzde kaçını aldığını anlamak için kullanışlıdır. |
|  Sunucu |Tüm istekleri isteği işleyen sunucuya göre gruplandırır. Bu gruplandırma, toplam trafiğin yük dağıtımını anlamak için kullanışlıdır.
| Çalışma Alanına Katılım |Tüm istekleri çalışma alanına katılmış (bilinen) cihazlardan gelip gelmediğine göre gruplandırır. Bu gruplandırma, kaynaklarınıza kimlik altyapısı tarafından bilinmeyen cihazlar kullanılarak erişilip erişilmediğini anlamak için kullanışlıdır. |
|  Kimlik Doğrulama Yöntemi | Toplam istekleri kimlik doğrulamak için kullanılan kimlik doğrulama yöntemine göre gruplandırır. Bu gruplandırma, kimlik doğrulaması için kullanılan yaygın kimlik doğrulama yöntemini anlamak için kullanışlıdır. Olası kimlik doğrulama yöntemleri aşağıda verilmiştir <ol> <li>Windows Tümleşik Kimlik Doğrulaması (Windows)</li> <li>Forms Tabanlı Kimlik Doğrulaması (Forms)</li> <li>SSO (Çoklu Oturum Açma)</li> <li>X509 Sertifika Doğrulaması (Sertifika)</li> <br>Federasyon sunucuları SSO Tanımlama Bilgisi ile istek alırsa bu istek SSO (Çoklu Oturum Açma) olarak sayılır. Bu gibi durumlarda, tanımlama bilgisi geçerliyse kullanıcıdan kimlik bilgilerini sağlaması istenmez ve kullanıcı uygulamaya sorunsuz bir şekilde erişir. Federasyon sunucuları tarafından korunan birden fazla bağlı olan tarafınız varsa bu davranış yaygındır. |
| Ağ Konumu | Tüm istekleri kullanıcının ağ konumuna göre gruplandırır. İntranet veya extranet olabilir. Bu gruplandırma, trafiğin yüzde kaçının intranetten veya extranetten geldiğini anlamak için kullanışlıdır. |


**Ölçüm: Toplam Başarısız İstek Sayısı** - Federasyon hizmeti tarafından işlenen başarısız isteklerin toplam sayısı. (Bu ölçüm yalnızca Windows Server 2012 R2 için AD FS'de kullanılabilir)

|Gruplandırma Ölçütü | Gruplandırma nedir ve ne işe yarar? |
| --- | --- |
| Hata Türü | Önceden tanımlanmış hata türlerine göre hata sayısını gösterir. Bu gruplandırma, genel hata türlerini anlamak için kullanışlıdır. <ul><li>Hatalı Kullanıcı Adı veya Parola: Hatalı kullanıcı adı veya paroladan kaynaklanan hatalar.</li> <li>"Extranet Kilitleme": Extranet dışında bırakılan bir kullanıcıdan alınan isteklerden kaynaklanan hatalar </li><li> "Süresi Dolan Parola": Süresi dolmuş bir parolayla oturum açmaya çalışan kullanıcılardan kaynaklanan hatalar.</li><li>"Devre Dışı Hesap": Devre dışı bırakılmış bir hesap ile oturum açmaya çalışan kullanıcılardan kaynaklanan hatalar.</li><li>"Cihaz Kimlik Doğrulaması": Cihaz Kimlik Doğrulamasını kullanarak kimlik doğrulaması gerçekleştiremeyen kullanıcılardan kaynaklanan hatalar.</li><li>"Kullanıcı Sertifikası Kimlik Doğrulaması": Geçersiz bir sertifika nedeniyle kimlik doğrulaması gerçekleştiremeyen kullanıcılardan kaynaklanan hatalar.</li><li>"MFA": Multi-Factor Authentication kullanarak kimlik doğrulaması yapmakta başarısız olan kullanıcılardan kaynaklanan hatalar.</li><li>"Diğer Kimlik Bilgisi": "Sertifika Verme Yetkilendirmesi": Başarısız yetkilendirmelerden kaynaklanan hatalar.</li><li>"Sertifika Verme Temsilcisi": Sertifika verme temsilcisi hatalarından kaynaklanan hatalar.</li><li>"Belirteç Onayı": ADFS'nin üçüncü taraf Kimlik Sağlayıcısından gelen bir belirteci reddetmesinden kaynaklanan hatalar.</li><li>"Protokol": Protokol hatalarından kaynaklanan hatalar.</li><li>"Bilinmeyen": Farklı nedenlerden kaynaklananlar. Tanımlanan kategorilere uymayan diğer tüm hatalar.</li> |
| Sunucu | Hataları sunucuya göre gruplandırır. Bu gruplandırma sunucular genelindeki hata dağıtımını anlamak için kullanışlıdır. Düzensiz dağıtım, hatalı durumdaki bir sunucunun göstergesi olabilir. |
| Ağ Konumu | Hataları isteklerin ağ konumuna (intranet veya extranet) göre gruplandırır. Bu gruplandırma başarısız olan istek türlerini anlamak için kullanışlıdır. |
|  Uygulama | Hataları hedeflenen uygulamaya (bağlı olan taraf) göre gruplandırır. Bu gruplandırma hedeflenen hangi uygulamanın en çok hata sayısını gördüğünü anlamak için kullanışlıdır. |

**Ölçüm: Kullanıcı sayısı** - Kimlik doğrulamak için etkin olarak AD FS’yi kullanan ortalama benzersiz kullanıcı sayısı

|Gruplandırma Ölçütü | Gruplandırma nedir ve ne işe yarar? |
| --- | --- |
|Tümü |Bu ölçüm seçilen bir zaman dilimi içinde federasyon hizmeti kullanan kullanıcıların ortalama sayısını sağlar. Kullanıcılar gruplandırılmaz. <br>Ortalama, seçilen zaman dilimine bağlı olarak değişir. |
| Uygulama |Ortalama kullanıcı sayısını hedeflenen uygulamaya (bağlı olan taraf) göre gruplandırır. Bu gruplandırma kaç kullanıcının hangi uygulamayı kullanmakta olduğunu anlamak için kullanışlıdır. |

## <a name="performance-monitoring-for-ad-fs"></a>AD FS için Performans İzleme
Azure AD Connect Health Performans İzleme, ölçümlere ilişkin izleme bilgileri sağlar. İzleme kutusunu seçtiğinizde, ölçümlere ilişkin ayrıntılı bilgiler içeren yeni bir dikey pencere açılır.

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/perf1.png)

Dikey pencerenin üst kısmındaki Filtre seçeneğini işaretlediğinizde her bir sunucunun ölçümlerini görmek için sunucuya göre filtreleme yapabilirsiniz. Ölçümü değiştirmek için, izleme dikey penceresinin altındaki izleme grafiğine sağ tıklayıp Grafiği Düzenle’yi seçin (veya Grafiği Düzenle düğmesini seçin). Açılan yeni dikey pencerede, açılan menüden başka ölçümler seçebilir veya performans verilerini görüntülemek istediğiniz zaman aralığını belirleyebilirsiniz.

## <a name="reports-for-ad-fs"></a>AD FS raporları
Azure AD Connect Health, AD FS'nin etkinlik ve performansı hakkında raporlar sağlar. Bu raporlar, yöneticilerin AD FS sunucularındaki etkinlikler hakkında öngörü edinmelerine yardımcı olur.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Hatalı Kullanıcı Adı/Parola kullanarak oturum açamayan İlk 50 Kullanıcı
Bir AD FS sunucusunda gerçekleşen başarısız kimlik doğrulama isteğinin en yaygın nedenlerinden biri geçersiz kimlik bilgileri ile ilgili isteklerdir, yani yanlış kullanıcı adı veya şifre istekleridir. Genellikle karmaşık parolalar, unutulan parolalar veya yazım hatalar nedeniyle oluşur.

Ancak, AD FS sunucularınızın beklenmeyen sayıda isteği işlemesiyle sonuçlanabilen diğer nedenlerle de mevcuttur, örneğin: Kullanıcı kimlik bilgilerini önbelleğe alan bir uygulama ve kimlik bilgilerinin süresinin dolması ya da kötü amaçlı bir kullanıcının bir dizi iyi bilinen parola ile hesapta oturum açmaya çalışması. Bu iki örnek, isteklerde ani bir artışa neden olabilecek geçerli nedenlerdir.

ADFS için Azure AD Connect Health, geçersiz kullanıcı adı veya paroladan dolayı oturum açma denemeleri başarısız olan İlk 50 Kullanıcıya ilişkin bir rapor sağlar. Bu rapor, gruplardaki tüm AD FS sunucuları tarafından oluşturulan denetim olaylarının işlenmesiyle sağlanır

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health-adfs/report1a.png)

Bu raporda şu bilgilere kolayca erişebilirsiniz:

* Son 30 gün içinde yanlış kullanıcı adı/parola ile başarısız olmuş isteklerin toplam sayısı
* Her gün hatalı kullanıcı adı/parola ile oturum açarak başarısız olan kullanıcıların ortalama sayısı.

Bu bölüme tıkladığınızda, ek ayrıntılı bilgi görüntüleyebileceğiniz ana rapor dikey penceresine yönlendirilirsiniz. Bu dikey pencere, yanlış kullanıcı adı veya parola ile yapılan isteklere ilişkin bir temel oluşturmaya yardımcı olan eğilim bilgileriyle birlikte grafik içerir. Ayrıca, en fazla başarısız girişim sayısına sahip ilk 50 kullanıcının listesini verir.

Grafikte şu bilgiler yer alır:

* Günlük olarak hatalı kullanıcı adı/parola nedeniyle başarısız olan oturum açma işlemlerinin toplam sayısı.
* Günlük olarak oturum açmada başarısız olan benzersiz kullanıcıların toplam sayısı.
* Son istek için istemci IP adresi

![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health-adfs/report3a.png)

Raporda şu bilgiler yer alır:

| Rapor Öğesi | Açıklama |
| --- | --- |
| Kullanıcı Kimliği |Kullanılan kullanıcı kimliğini gösterir. Bu değer, kullanıcının ne yazdığıyla ilgilidir ve bazı durumlarda yanlış kullanıcı kimliği kullanılır. |
| Başarısız Denemeler |Belirli bir kullanıcı kimliğine ait başarısız denemelerin toplam sayısını gösterir. Tablo, en fazla deneme sayısından en aza doğru azalan bir düzende sıralanır. |
| Son Hata |Son hatanın oluştuğu andaki zaman damgasını gösterir. |
| Son Hata IP’si |Son hatalı istekteki İstemci IP adresini gösterir. |

> [!NOTE]
> Bu rapor, her iki saatte bir bu süre içinde toplanan yeni bilgiler ile otomatik olarak güncelleştirilir. Bu nedenle raporda son iki saat içinde gerçekleşen oturum açma denemeleri bulunmayabilir.
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