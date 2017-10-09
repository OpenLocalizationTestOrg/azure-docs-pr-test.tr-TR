---
title: "Azure Active Directory Raporlama: Başlarken | Microsoft Belgeleri"
description: "Azure Active Directory raporlamada kullanılabilen çeşitli raporları listeler hello"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Azure Active Directory Raporlama ile çalışmaya başlama
## <a name="what-it-is"></a>Nedir?
Azure Active Directory (Azure AD), dizininize yönelik güvenlik, etkinlik ve denetim raporlarını içerir. Dahil hello raporları listesi aşağıdadır:

### <a name="security-reports"></a>Güvenlik raporları
* Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri
* Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri
* Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri
* Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri
* Düzensiz oturum açma etkinliği
* Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri
* Anormal oturum açma etkinliği gösteren kullanıcılar

### <a name="activity-reports"></a>Etkinlik raporları
* Uygulama kullanımı: özet
* Uygulama kullanımı: ayrıntılı
* Uygulama panosu
* Hesap hazırlama hataları
* Bireysel kullanıcı cihazları
* Bireysel kullanıcı Etkinliği
* Grup etkinlik raporu
* Parola Sıfırlama Kayıt Etkinlik Raporu
* Parola sıfırlama etkinliği

### <a name="audit-reports"></a>Denetim raporları
* Dizin denetimi raporu

> [!TIP]
> Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.
> 
> 

## <a name="how-it-works"></a>Nasıl çalışır?
### <a name="reporting-pipeline"></a>Raporlama işlem hattı
Merhaba raporlama işlem hattı üç ana adımdan oluşur. Bir kullanıcı oturum açtığında veya bir kimlik doğrulaması yapılan her zaman, hello aşağıdakiler gerçekleşir:

* İlk olarak, (başarıyla veya başarısız) hello kullanıcı kimlik doğrulaması ve hello sonuç hello Azure Active Directory Hizmeti veritabanlarında depolanır.
* Düzenli aralıklarla, en yeni oturum açma işlemlerinin tümü işlenir. Bu noktada, güvenlik ve anormal etkinlik algoritmalarımız en yeni oturum açma işlemlerinin tümünde şüpheli etkinlik araması gerçekleştirmektedir.
* İşlemeden sonra hello raporları yazılmış, önbelleğe alınan ve hello Klasik Azure portalına hizmet.

### <a name="report-generation-times"></a>Rapor oluşturma süreleri
Toohello büyük hacimli kimlik doğrulamaları ve bileşenler Azure AD platformu hello tarafından işlenen oturum, hello en son işlenen oturum açma işlemlerini, ortalama olarak bir saat öncesine aittir. Nadir durumlarda too8 saatleri tooprocess hello en son oturum açma işlemleri sürebilir.

Merhaba en son işlenen oturum açma, her rapor hello üstündeki hello Yardım metnini inceleyerek bulabilirsiniz.

![Her rapor hello üst kısmındaki Yardım metnini](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.
> 
> 

## <a name="getting-started"></a>Başlarken
### <a name="sign-into-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalında oturum açın
Önce hello toosign gerekir. [Klasik Azure portalı](https://manage.windowsazure.com) genel veya uyumluluk Yöneticisi olarak. Ayrıca, bir Azure aboneliği Hizmet Yöneticisi veya ortak yöneticisi olmanız gerekir veya hello "erişim tooAzure AD" kullanarak Azure aboneliği.

### <a name="navigate-tooreports"></a>TooReports gidin
tooview raporları toohello hello dizininizin üst kısmındaki Raporlar sekmesine gidin.

Merhaba raporları görüntüleme, ilk kez kullanıyorsanız hello raporlarını görüntüleyebilmek için tooagree tooa iletişim kutusu gerekir. Bu tooensure kuruluş tooview admins için kabul edilebilir olduğundan emin olup bu veriler, bazı ülkelerde özel bilgi olarak kabul.

![İletişim kutusu](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Raporların her birini araştırma
Toplanmakta olan her rapor toosee hello veri gidin ve hello oturum açma işlemleri işlenebilir. Bulabileceğiniz bir [burada tüm hello raporların listesini](active-directory-reporting-guide.md).

![Tüm raporlar](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Merhaba raporları CSV olarak indirme
Raporların her biri CSV (virgülle ayrılmış değer) dosyası olarak indirilebilir. Bu dosyaları Excel, Powerbı veya üçüncü taraf analiz programları toofurther analiz verilerinizi kullanabilirsiniz.

herhangi bir CSV olarak rapor toodownload toohello rapora gidin ve "Merhaba altındaki Yükle"'yi tıklatın.

![İndir düğmesi](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Anormal oturum açma etkinliği için uyarıları özelleştirme
Dizininizin toohello "Yapılandırma" sekmesine gidin.

Toohello "Bildirimler" bölümüne gidin.

Etkinleştirmek veya devre dışı hello "Anormal oturum açma işlemlerine e-posta bildirimleri" bölümü.

![Merhaba bildirimler bölümü](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Azure AD raporlama API'si ile Merhaba tümleştirme
Bkz: [hello raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Multi-Factor Authentication'ı kullanıcılar üzerinde uygulama
Rapordaki bir kullanıcıyı seçin.

Merhaba ekranın hello Hello "MFA'yı etkinleştir" düğmesini tıklatın.

![Merhaba ekranında hello sonundaki Hello çok faktörlü kimlik doğrulaması düğmesi](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.
> 
> 

## <a name="learn-more"></a>Daha fazla bilgi edinin
### <a name="audit-events"></a>Denetim olayları
Hangi olayları hakkında hello dizininde denetleneceğini öğrenin [Azure Active Directory raporlama denetim olayları](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>API Tümleştirme
Bkz: [hello raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) ve hello [API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>İletişim
Geri bildirim, yardım veya her türlü sorularınız için [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) adresine e-posta gönderin.

> [!TIP]
> Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.
> 
> 

