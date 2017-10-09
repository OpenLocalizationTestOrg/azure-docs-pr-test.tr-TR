---
title: "aaaView erişim ve kullanım raporlarınızı | Microsoft Docs"
description: "Nasıl tooview erişim ve kullanım raporları toogain fikirler hello bütünlüğü ve güvenlik kuruluşunuzun dizininin açıklanmaktadır."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Erişim ve kullanım raporlarınızı görüntüleme
*Bu belge hello parçası olan [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*

Azure Active Directory'nin erişim ve kullanım raporları toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanabilirsiniz. Bu bilgileri kullanarak bir dizin yönetici böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri burada bulunan daha iyi belirleyebilirsiniz.

Hello Azure Yönetim Portalı'da, raporları hello yolları aşağıdaki kategorilere ayrılır:

* Kural dışı durum raporları – toobe anormal bulduk olduğunu içeren oturum açma olayları. Amacımız toomake olduğundan, bu tür etkinliğini kullanan ve toobe mümkün toomake bir olay şüpheli olup olmadığı hakkında bir belirleme etkinleştirin.
* Tümleşik uygulama raporları – Öngörüler bulut uygulamalarını, kuruluşunuzda nasıl kullanıldığını içine sağlar. Azure Active Directory bulut uygulamalarını binlerce ile tümleştirme sağlar.
* Hata raporlarını – hesapları tooexternal uygulamalar sağlama sırasında meydana gelebilecek gösterin hataları.
* Kullanıcıya özgü raporları – aygıt/oturum etkinlik verileri belirli bir kullanıcı için görüntüler.
* Etkinlik günlükleri – içeren bir kayıt hello içindeki tüm Denetlenen olayları en son 24 saat, son 7 gün veya son 30 Günün yanı sıra grup etkinlik değişikliklerini ve parola sıfırlama ve kayıt etkinliği.

> [!NOTE]
> * Bazı gelişmiş anomali ve kaynak kullanım raporları yalnızca, etkinleştirdiğinizde kullanılabilir [Azure Active Directory Premium](active-directory-get-started-premium.md). Gelişmiş raporlar yanıt toopotential tehditleri erişim güvenliğini artırmak ve aygıt erişim ve uygulama kullanımı erişim tooanalytics alma yardımcı olur.
> * Azure Active Directory Premium ve Basic sürümleri Azure Active Directory Merhaba Dünya çapındaki örneğini kullanan Çin müşteriler için kullanılabilir. Azure Active Directory Premium ve Basic sürümleri şu anda Çin'de 21Vianet tarafından işletilen hello Microsoft Azure hizmetindeki desteklenmez. Daha fazla bilgi için bize hello başvurun [Azure Active Directory Forumu](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Reports
| Rapor | Açıklama |
| --- | --- |
| **Anormal etkinlik raporları** | |
| [Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri](active-directory-reporting-sign-ins-from-unknown-sources.md) |Bir deneme toosign izlenen olmadan gösteriyor olabilir. |
| [Birden çok hatadan sonra oturum açmalar](active-directory-reporting-sign-ins-after-multiple-failures.md) |Başarılı yanılma saldırısı gösteriyor olabilir. |
| [Birden çok coğrafyadan oturum](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Birden çok kullanıcı oturum hello aynı oturum açıyorsanız olduğunu gösterebilir hesabı. |
| [Şüpheli etkinliğe sahip IP adreslerinden oturum açmalar](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Başarılı oturum açma sürekli yetkisiz erişim girişiminden sonra gösteriyor olabilir. |
| [Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Muhtemelen virüs bulaşmış cihazlardan içinde girişimi toosign gösteriyor olabilir. |
| [Düzensiz oturum açma etkinliği](active-directory-reporting-irregular-sign-in-activity.md) |Olayları anormal toousers oturum açma desenleri gösteriyor olabilir. |
| [Anormal oturum açma etkinliği olan kullanıcılar](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Kullanıcıları, hesapları tehlikede olduğunu gösterir. |
| Sızan kimlik bilgilerine sahip kullanıcılar |Sızan kimlik bilgilerine sahip kullanıcılar |
| **Etkinlik günlükleri** | |
| Denetim raporu |Dizininizde Denetlenen olayları |
| Parola sıfırlama etkinliği |Kuruluşunuzda ortaya parola sıfırlama ayrıntılı bir görünümünü sağlar. |
| Parola sıfırlama kaydı etkinliği |Kuruluşunuzda ortaya kayıtlar ayrıntılı görünümünü parola sıfırlama sağlar. |
| Self Servis Grup etkinliği |Bir etkinlik günlüğü tooall sağlar Grup dizininizde self servis etkinliği |
| **Tümleşik uygulamalar** | |
| Uygulama kullanımı |Directory ile tümleşik tüm SaaS uygulamaları için bir kullanım özeti sağlar. |
| Hesap etkinlik sağlama |Deneme geçmişini tooprovision hesapları tooexternal uygulamaları sağlar. |
| Parola rollover durumu |SaaS uygulamaları otomatik parola rollover durumu ayrıntılı bir genel bakış sağlar. |
| Hesap hazırlama hataları |Bir etkisi toousers erişim tooexternal uygulamaları gösterir. |
| **Hak Yönetimi** | |
| RMS kullanımı |Rights Management kullanım için bir Özet sağlar |
| En etkin RMS kullanıcıları |RMS korumalı dosyalara kimin ilk 1000 etkin kullanıcılar listeler |
| RMS Aygıt kullanımı |Eriştiği RMS korumalı dosyaları için kullanılan aygıtları listeler |
| RMS özellikli uygulama kullanımı |Etkin olan uygulamalar, RMS kullanım sağlar |

## <a name="report-editions"></a>Rapor sürümleri
| Rapor | Ücretsiz | Temel | Premium |
| --- | --- | --- | --- |
| **Anormal etkinlik raporları** | | | |
| Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri |✓ |✓ |✓ |
| Birden çok hatadan sonra oturum açmalar |✓ |✓ |✓ |
| Birden çok coğrafyadan oturum |✓ |✓ |✓ |
| Şüpheli etkinliğe sahip IP adreslerinden oturum açmalar | | |✓ |
| Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri | | |✓ |
| Düzensiz oturum açma etkinliği | | |✓ |
| Anormal oturum açma etkinliği olan kullanıcılar | | |✓ |
| Sızan kimlik bilgilerine sahip kullanıcılar | | |✓ |
| **Etkinlik günlükleri** | | | |
| Denetim raporu |✓ |✓ |✓ |
| Parola sıfırlama etkinliği | | |✓ |
| Parola sıfırlama kaydı etkinliği | | |✓ |
| Self Servis Grup etkinliği | | |✓ |
| **Tümleşik uygulamalar** | | | |
| Uygulama kullanımı | | |✓ |
| Hesap etkinlik sağlama |✓ |✓ |✓ |
| Parola rollover durumu | | |✓ |
| Hesap hazırlama hataları |✓ |✓ |✓ |
| **Hak Yönetimi** | | | |
| RMS kullanımı | | |Yalnızca RMS |
| En etkin RMS kullanıcıları | | |Yalnızca RMS |
| RMS Aygıt kullanımı | | |Yalnızca RMS |
| RMS özellikli uygulama kullanımı | | |Yalnızca RMS |

## <a name="anomalous-activity-reports"></a>Anormal etkinlik raporları
<p>Merhaba anormal etkinlik raporları bayrağı şüpheli oturum açma etkinliği tooOffice365, Azure Yönetim Portalı, Azure AD erişim paneli, Sharepoint Online, Dynamics CRM Online ve diğer Microsoft online services oturum açın.</p>

<p>Tüm rapor, "birden çok hatadan sonra oturum açmalar" Merhaba dışında bu raporları ayrıca şüpheli bayrak <i>federe</i> bileşenler toohello daha önce bahsedilen Hizmetleri hello Federasyon sağlayıcısı bağımsız olarak oturum açın. </p>

<p>Raporlar aşağıdaki hello kullanılabilir: </p><ul>

<li>[Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Birden çok hatadan sonra oturum açmalar](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Birden çok coğrafyadan oturum](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Şüpheli etkinliğe sahip IP adreslerinden oturum açmalar](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Düzensiz oturum açma etkinliği](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Anormal sahip kullanıcılar oturum etkinliğinde](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Sızan kimlik bilgilerine sahip kullanıcılar</li></ul>

## <a name="activity-logs"></a>Etkinlik günlükleri
### <a name="audit-report"></a>Denetim raporu
| Açıklama | Rapor konumu |
|:--- |:--- |
| Merhaba son 24 saat, son 7 gün veya son 30 gün içinde tüm Denetlenen olayları kaydını gösterir. <br /> Daha fazla bilgi için bkz: [Azure Active Directory Denetim Raporu olayları](active-directory-reporting-audit-events.md) |Dizin > Raporlar sekmesi |

![Denetim raporu](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Parola sıfırlama etkinliği
| Açıklama | Rapor konumu |
|:--- |:--- |
| Tüm parola sıfırlama, kuruluşunuzda oluşmuş denemeleri gösterir. |Dizin > Raporlar sekmesi |

![Parola sıfırlama etkinliği](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Parola sıfırlama kaydı etkinliği
| Açıklama | Rapor konumu |
|:--- |:--- |
| Kuruluşunuzda oluşmuş kayıtlar tüm parola sıfırlama gösterir |Dizin > Raporlar sekmesi |

![Parola sıfırlama kaydı etkinliği](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Self Servis Grup etkinliği
| Açıklama | Rapor konumu |
|:--- |:--- |
| Merhaba kendi kendine yönetilen grupları için tüm etkinlik dizininizde gösterir. |Dizin > Kullanıcılar > <i>kullanıcı</i> > aygıtlar sekmesi |

![Self Servis Grup etkinliği](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Tümleşik uygulamalar raporları
### <a name="application-usage-summary"></a>Uygulama kullanımı: özet
| Açıklama | Rapor konumu |
|:--- |:--- |
| Dizininizdeki tüm hello SaaS uygulamaları için toosee kullanım istediğinizde bu raporu kullanın. Bu rapor hello kaç kez kullanıcılar hello erişim paneli hello uygulamada üzerinde tıkladıysanız temel alır. |Dizin > Raporlar sekmesi |

Bu raporda oturum açmalar çok*tüm* dizininize olan uygulamalara erişmek için önceden tümleştirilmiş Microsoft uygulamaları dahil olmak üzere.

Office 365, Sharepoint, hello Azure Yönetim Portalı ve diğerleri önceden tümleştirilmiş Microsoft uygulamalarını içerir.

![Uygulama Kullanım Özeti](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Uygulama kullanımı: ayrıntılı
| Açıklama | Rapor konumu |
|:--- |:--- |
| Ne kadar belirli bir SaaS uygulaması kullanılan toosee istediğinizde bu raporu kullanın. Bu rapor hello kaç kez kullanıcılar hello erişim paneli hello uygulamada üzerinde tıkladıysanız temel alır. |Dizin > Raporlar sekmesi |

### <a name="application-dashboard"></a>Uygulama panosu
| Açıklama | Rapor konumu |
|:--- |:--- |
| Bu rapor seçili zaman aralığı içinde kuruluşunuzdaki kullanıcılar tarafından toplu oturum bileşenler toohello uygulama gösterir. Merhaba panosu sayfasında Hello grafik, bu uygulamanın tüm kullanım eğilimleri belirlemenize yardımcı olur. |Dizin > Uygulama > Pano sekmesi |

## <a name="error-reports"></a>Hata raporları
### <a name="account-provisioning-errors"></a>Hesap hazırlama hataları
| Açıklama | Rapor konumu |
|:--- |:--- |
| SaaS uygulamaları tooAzure Active Directory hesapları hello eşitleme sırasında oluşan bu toomonitor hataları kullanın. |Dizin > Raporlar sekmesi |

![Hesap hazırlama hataları](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Kullanıcıya özgü raporları
### <a name="devices"></a>Cihazlar
| Açıklama | Rapor konumu |
|:--- |:--- |
| Toosee başlangıç IP adresi ve belirli bir kullanıcı tooaccess Azure Active Directory kullandı aygıtları coğrafi konumunu istediğinizde bu raporu kullanın. |Dizin > Kullanıcılar > <i>kullanıcı</i> > aygıtlar sekmesi |

### <a name="activity"></a>Etkinlik
| Açıklama | Rapor konumu |
|:--- |:--- |
| Bir kullanıcı için etkinliğinde Hello oturum gösterir. Merhaba rapor oturum Merhaba uygulaması, kullanılan aygıt, IP adresi ve konum gibi bilgileri içerir. Bir Microsoft hesabı ile oturum kullanıcılar için hello geçmişini toplamaz. |Dizin > Kullanıcılar > <i>kullanıcı</i> > etkinlik sekmesi |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Oturum açma olayları hello kullanıcı etkinliği raporu dahil
Oturum açma olayları yalnızca belirli türdeki hello kullanıcı etkinliği raporu görünür.

| Olay türü | Dahil? |
| --- | --- |
| Oturum açmalar toohello [erişim paneli](http://myapps.microsoft.com/) |Evet |
| Oturum açmalar toohello [Azure Yönetim Portalı](https://manage.windowsazure.com/) |Evet |
| Oturum açmalar toohello [Microsoft Azure portalı](https://portal.azure.com/) |Evet |
| Oturum açmalar toohello [Office 365 portalı](http://portal.office.com/) |Evet |
| Oturum açmalar tooa yerel uygulama, Outlook gibi (aşağıdaki özel durum bakın) |Evet |
| Merhaba Salesforce gibi erişim paneli üzerinden oturum bileşenler tooa federe ve sağlanan uygulama |Evet |
| Parola tabanlı bileşenler tooa uygulama hello Twitter gibi erişim paneli aracılığıyla oturum açın |Evet |
| Toohello dizin eklenen bileşenleri tooa özel iş uygulamasını imzalama |Yok (yakında) |
| Toohello dizin eklenen bileşenleri tooan Azure AD uygulama proxy'si uygulamasını imzalama |Yok (yakında) |

> Not: Bu raporda, parazit tooreduce hello miktarını oturum bileşenler tarafından hello [Microsoft Online Services oturum açma Yardımcısı](http://community.office365.com/en-us/w/sso/534.aspx) gösterilmez.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Güvenlik ihlali şüpheleniyorsanız şeyler tooconsider
Şüpheleniyorsanız bir kullanıcı hesabı tehlikeye girebilir veya herhangi bir tür, dizin verilerini tooa güvenlik açığını hello bulutta açabilir şüpheli kullanıcı etkinliği tooconsider biri veya birkaçı eylemleri aşağıdaki hello isteyebilirsiniz:

* Merhaba kullanıcı tooverify hello etkinliği başvurun
* Merhaba kullanıcı parolasını sıfırlama
* [Çok faktörlü kimlik doğrulamasını etkinleştir](../multi-factor-authentication/multi-factor-authentication-get-started.md) ek güvenlik için

## <a name="view-or-download-a-report"></a>Görüntülemek veya bir raporu yükleyin
1. Hello Klasik Azure portalı, tıklatın **Active Directory**, kuruluşunuzun dizininde hello adına tıklayın ve ardından **raporları**.
2. Merhaba raporu tooview Hello raporları sayfasında, tıklatın ve/veya indirin.
   
   > [!NOTE]
   > Bu özellik Azure Active Directory raporlama hello kullanılan ilk kez hello ise, bir ileti tooOpt görürsünüz. Kabul ediyorsanız, hello onay işareti simgesi toocontinue'ı tıklatın.
   > 
   > 
3. Merhaba açılır menü sonraki tooInterval tıklayın ve sonra bu rapor oluşturulurken kullanılacak zaman aralıklarına aşağıdaki hello birini seçin:
   
   * Son 24 saat
   * Son 7 gün
   * Son 30 gün
4. Merhaba onay işareti simgesi toorun hello raporu tıklatın.
   * Too1000 olayları hello Klasik Azure portalı gösterilir.
5. Varsa, tıklatın **karşıdan** çevrimdışı görüntülemek veya arşivleme amacıyla toodownload hello rapor tooa sıkıştırılmış dosya virgülle ayrılmış değerler (CSV) biçiminde.
   * Too75 000 olayları indirilen hello dosyasına dahil edilir.
   * Daha fazla veri için hello denetleyin [Azure AD raporlama API'si](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Bir olay yoksay
Herhangi bir anomali rapor görüntülüyorsanız ilgili raporlarda görünmesini çeşitli olayları yoksayabilirsiniz fark edebilirsiniz. bir olay, tooignore yalnızca hello rapordaki hello olayı vurgulayın ve ardından **Yoksay**. Merhaba **Yoksay** düğmesi hello vurgulanan olay hello rapordan kalıcı olarak kaldırır ve yalnızca lisanslı genel yöneticiler tarafından kullanılabilir.

## <a name="automatic-email-notifications"></a>Otomatik e-posta bildirimleri
Bildirimleri rapor Azure AD hakkında daha fazla bilgi için kullanıma [Azure Active Directory raporlama bildirimleri](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Sırada ne var?
* [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md)
* [Tooyour oturum aç ve erişim paneli sayfalarınıza şirket markası ekleme](active-directory-add-company-branding.md)

