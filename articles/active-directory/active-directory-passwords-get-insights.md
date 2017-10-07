---
title: "Get Öngörüler: Azure AD parola yönetimi raporları | Microsoft Docs"
description: "Bu makalede nasıl toouse parola yönetimi işlemleri, kuruluşunuzda tooget fikirler raporları açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Parola yönetimi ile tooget operasyonel Öngörüler nasıl raporları
> [!IMPORTANT]
> **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Bu bölümde Azure Active Directory'nin nasıl kullanabileceğinizi açıklar parola yönetimi nasıl kullanıcılar parola sıfırlama kullanıyorsanız ve kuruluşunuzdaki değiştirmek tooview bildirir.

* [**Parola yönetimi raporları genel bakış**](#overview-of-password-management-reports)
* [**Nasıl hello yeni Azure portalında tooview parola yönetimi raporları**](#how-to-view-password-management-reports)
 * [Tooread raporları izin directory rolleri](#directory-roles-allowed-to-read-reports)
* [**Yeni Azure Portal Self Servis parola yönetimi etkinliği türlerinde hello**](#self-service-password-management-activity-types)
 * [Self Servis parola sıfırlama engellendi](#activity-type-blocked-from-self-service-password-reset)
 * [Parola değiştirme (Self Servis)](#activity-type-change-password-self-service)
 * [(Yönetici tarafından) parola sıfırlama](#activity-type-reset-password-by-admin)
 * [(Self Servis) parola sıfırlama](#activity-type-reset-password-self-service)
 * [Akış etkinliği ilerleme kendi hizmet vermemesini parola sıfırlama](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Kullanıcı hesabının (Self Servis) kilidi](#activity-type-unlock-user-account-self-service)
 * [Self Servis parola sıfırlama için kayıtlı kullanıcı](#activity-type-user-registered-for-self-service-password-reset)
* [**Azure AD raporları ve olayları API tooretrieve parola yönetimi olayları nasıl hello**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Raporlama API veri alma sınırlamaları](#reporting-api-data-retrieval-limitations)
* [**PowerShell ile hızlı bir şekilde kayıt olayları nasıl toodownload parola sıfırlama**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Merhaba Klasik Portalı'nda nasıl tooview parola yönetimi raporları**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Görünüm parola sıfırlama kaydı etkinliği hello Klasik Portalı'nda, kuruluşunuzdaki**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Görünüm parola sıfırlama etkinliği, kuruluşunuzda hello Klasik portalında**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Parola yönetimi raporları genel bakış
Parola sıfırlama dağıttığınızda hello en yaygın sonraki adımlar, kuruluşunuzda nasıl kullanıldığını toosee biridir.  Örneğin, tooget Insight isteyebilir nasıl kullanıcılar parola sıfırlama veya kaç parola kaydediyorsunuz içine sıfırlar hello son birkaç günde yapılmış.  Bazı hello parola yönetimi raporlarıyla hello mevcut mümkün tooanswer olacak hello sık sorulan sorular [Azure Yönetim Portalı](https://manage.windowsazure.com) Bugün:

* Kaç kişinin parola sıfırlama için kayıtlı?
* Parola sıfırlama için kayıtlı olan kim?
* Verileri kaydetme kişiler nelerdir?
* Kaç kişinin son 7 gün hello parolalarını sıfırlama?
* Hello en yaygın yöntemleri kullanıcıları veya yöneticileri tooreset parolalarını kullanmak ne var mı?
* Ne ortak olan kullanıcıları veya yöneticileri yüz toouse parola sıfırlama çalışırken verir?
* Hangi yöneticileri kendi parolalarını sık sıfırlama?
* Parola sıfırlama ile geçmeden tüm şüpheli etkinlik mi?

## <a name="how-tooview-password-management-reports"></a>Parola yönetimi tooview raporları nasıl
Merhaba yeni içinde [Azure Portal](https://portal.azure.com) deneyimi, bir geliştirilmiş yolu tooview parola sıfırlama ve parola sıfırlama kayıt etkinlik sunuyoruz.  Merhaba adımları aşağıda toofind hello parola sıfırlama ve parola sıfırlama hello yeni kayıt olayları [Azure Portal](https://portal.azure.com):

1. Çok gidin[**portal.azure.com**](https://portal.azure.com)
2. Tıklatın hello üzerinde **daha fazla hizmet** hello ana Azure portalında sol taraftaki gezinti menüsünde
3. Arama **Azure Active Directory** hello hizmetlerin listesi ve seçin
4. Tıklayın **kullanıcıları ve grupları** hello Azure Active Directory Gezinti menüsünde
5. Tıklatın hello üzerinde **denetim günlüklerini** hello kullanıcıları ve grupları Gezinti menüsünde Gezinti öğesi. Bu, tüm hello denetim olayları gerçekleşmesini tüm hello kullanıcılara karşı dizininizde gösterir. Bu görünüm toosee tüm hello parola ilgili olayların de filtre uygulayabilirsiniz.
6. Bu görünüm tooonly hello parola yönetimi ile ilgili toofilter hello tıklama olayları, **filtre** hello dikey penceresinde hello üstündeki düğmesi.
7. Merhaba gelen **filtre** menüsü, select hello **kategori** açılan listesinde ve toohello değiştirmek **Self Servis parola yönetimi** kategori türü.
8. İsteğe bağlı olarak daha fazla filtre hello listesi hello özel seçerek **etkinlik** ilgilendiğiniz
### <a name="direct-link-toouser-audit-blade"></a>Doğrudan bağlantı tooUser denetim dikey penceresi
Tooyour Portalı'nda kaydolduysanız İşte doğrudan bağlantı toohello kullanıcı Denetim dikey bu olayları burada görebilirsiniz:

* [Toouser yönetim denetim görünüm doğrudan gidin](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Tooread raporları izin directory rolleri
Şu anda hello aşağıdaki dizin rollerini hello Klasik Azure portalında Azure AD parola yönetimi raporları okuyabilirsiniz:

* Genel yönetici

Bu raporlar mümkün tooread olmaya önce hello şirket'te genel yönetici seçti sekme veya denetim günlüklerini en az bir kere raporlama hello ziyaret ederek hello kuruluş adına alınan bu verileri toobe için bileşeni gerekir. Bunun yapılması kadar veri kuruluşunuz için toplanmaz.

Dizin rolleri ve ne yapabilir hakkında daha fazla bilgi bakın tooread [Azure Active Directory'de yönetici rolleri atama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Self Servis parola yönetimi etkinlik türleri
şu etkinlik türlerini hello görünür hello **Self Servis parola yönetimi** denetim olay kategorisi.  Bunların her biri için bir açıklama izler.

* [**Self Servis parola sıfırlama engellenen** ](#activity-type-blocked-from-self-service-password-reset) -bir kullanıcı bir parola tooreset çalıştı gösterir belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* [**Parola (Self Servis) değiştirme** ](#activity-type-change-password-self-service) -kullanıcı bir gönüllü gerçekleştirilen veya zorunlu gösterir (son tooexpiry) parola değiştirme.
* [**Parola sıfırlama (yönetici tarafından)** ](#activity-type-reset-password-by-admin) -parola sıfırlama hello Azure Portalı'ndan bir kullanıcı adına bir yönetici gerçekleştirilen gösterir.
* [**Parola sıfırlama (Self Servis)** ](#activity-type-reset-password-self-service) -kullanıcı başarıyla hello paroladan sıfırlama gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* [**Kendi kendine hizmet vermemesini parola sıfırlama akış etkinliği ilerleme** ](#activity-type-self-serve-password-reset-flow-activity-progress) -sıfırlama işlemi hello parola parçası olarak bir kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) her belirli adım gösterir.
* [**Kullanıcı hesabının (Self Servis) kilidini** ](#activity-type-unlock-user-account-self-service) -kullanıcı kilidi başarıyla açıldı Active Directory hesabını hello paroladan sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) Hello kullanarak [AD hesabının kilidini ayarlarına sıfırlamadan](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) özelliği.
* [**Kullanıcı Self Servis parola sıfırlama için kayıtlı** ](#activity-type-user-registered-for-self-service-password-reset) -bir kullanıcı parolasını hello şu anda belirtilen Kiracı parolası sıfırlama ilkesini göre tüm gerekli hello bilgi toobe mümkün tooreset kayıtlı belirtir.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Etkinlik türü: Self Servis parola sıfırlama engellendi
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – belirtir bir kullanıcı bir parola tooreset çalıştı, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* **Etkinlik aktör** -ek gerçekleştirmesini kısıtlanan hello kullanıcı sıfırlama işlemleri. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -ek gerçekleştirmesini kısıtlanan hello kullanıcı sıfırlama işlemleri. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı kısıtlanan gösteren herhangi bir ek sıfırlar gerçekleştirmeyi ek kimlik doğrulama yöntemleri deneyin veya herhangi bir ek telefon numaraları hello için sonraki 24 saat doğrula.
* **Etkinlik durumu hata nedeni** - geçerli değil

### <a name="activity-type-change-password-self-service"></a>Etkinlik türü: parola değiştirme (Self Servis)
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – bir kullanıcı bir gönüllü gerçekleştirilen veya zorunlu gösterir (son tooexpiry) parola değiştirme.
* **Etkinlik aktör** -parolasını değiştiren hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolasını değiştiren hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı parolasını başarıyla değiştirildiğini gösterir
 * _Hata_ -bir kullanıcı parolasını toochange başarısız gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu hata nedeni** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello kullanıcı seçilen çok sık kullanılan veya özellikle zayıf toobe bulma tooMicrosoft'ın yasaklanan parola algılama özellikleri otomatik olarak yasaklanan bir parola.

### <a name="activity-type-reset-password-by-admin"></a>Etkinlik türü: (yönetici tarafından) parola sıfırlama
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – yönetici gerçekleştirilen parola hello Azure Portalı'ndan bir kullanıcı adına sıfırlama gösterir.
* **Etkinlik aktör** -hello parola başka bir son kullanıcı veya yönetici adına sıfırlama gerçekleştiren hello Yöneticisi. Ya da bir genel yönetici, parola yönetici, kullanıcı veya Yardım Masası yönetici olması gerekir.
* **Etkinlik hedef** -hello kullanıcı parolasını sıfırlandı. Bir son kullanıcı veya farklı bir yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir yönetici kullanıcının parolası başarıyla sıfırlandı gösterir
 * _Hata_ -bir yönetici bir kullanıcının parolasını toochange başarısız gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.

### <a name="activity-type-reset-password-self-service"></a>Etkinlik türü: parola sıfırlama (Self Servis)
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı başarıyla hello paroladan sıfırlama gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* **Etkinlik aktör** -parolasını sıfırlama hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolasını sıfırlama hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı, kendi parola başarıyla sıfırlandı gösterir
 * _Hata_ -bir kullanıcı kendi parolasını tooreset başarısız gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu hata nedeni** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello Yöneticisi seçili çok sık kullanılan veya özellikle zayıf toobe bulma tooMicrosoft'ın yasaklanan parola algılama özellikleri otomatik olarak yasaklanan bir parola.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Etkinlik türü: kendi kendine parola sıfırlama akış etkinliği ilerleme hizmet
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) sıfırlama işlemi hello parola parçası olarak her belirli adım gösterir.
* **Etkinlik aktör** -hello parola parçası gerçekleştiren hello kullanıcı sıfırlama akış. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hello parola parçası gerçekleştiren hello kullanıcı sıfırlama akış. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı belirli bir adıma hello parola sıfırlama akışının başarıyla tamamlandı gösterir.
 * _Hata_ -belirli bir adıma hello parola sıfırlama başarısız akış gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu nedeniyle izin verilen**
 * İçin aşağıdaki tabloya bakın [tüm sıfırlama etkinliği durumu nedeniyle izin verilen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Etkinlik türü: kullanıcı hesabı (Self Servis) kilidini aç
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcının kilidi başarıyla açıldı Active Directory hesabını hello paroladan sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) hello kullanarak [AD hesabın kilidini ayarlarına sıfırlamadan](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) özelliği.
* **Etkinlik aktör** -hesabını, parola sıfırlama olmadan kilidi hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hesabını, parola sıfırlama olmadan kilidi hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı, kendi hesabını başarıyla kilidi gösterir
 * _Hata_ -bir kullanıcı hesabını toounlock başarısız gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Etkinlik türü: kullanıcı Self Servis parola sıfırlama için kayıtlı
liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – bir kullanıcı parolasını hello şu anda belirtilen Kiracı parolası sıfırlama ilkesini göre tüm gerekli hello bilgi toobe mümkün tooreset kayıtlı belirtir.
* **Etkinlik aktör** -parola sıfırlama için kaydolan hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola sıfırlama için kaydolan hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -parola sıfırlama hello geçerli ilkesiyle uygun şekilde başarıyla kayıtlı bir kullanıcı gösterir.
 * _Hata_ -parola sıfırlama için başarısız kullanıcı tooregister gösterir. Merhaba satıra tıklayarak etmenizi sağlar toosee hello **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi. Not - Bu gelmez bir kullanıcı erişilemiyor tooreset kendi çözemiyorsa hello kayıt işlemi tamamlanmadı yalnızca paroladır. (Doğrulanmazsa, bir telefon numarası gibi), doğru kendi hesabındaki doğrulanmamış verileri ise bunlar bu telefon numarası doğrulanmadı olsa bile, yine tooreset kullanabileceklerini parolalarını. Daha fazla bilgi için bkz: [kullanıcı kayıtları ne olur?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Azure AD raporları ve olayları API tooretrieve parola yönetimi olayları nasıl hello
Ağustos 2015'ten itibaren hello Azure AD raporları ve olayları API artık destekliyor tüm hello bilgileri hello parola sıfırlama ve parola sıfırlama kayıt raporlara dahil alınıyor. Bu API'yi kullanarak tek tek parola sıfırlama karşıdan yükleyebilir ve, choce teknolojisini raporlama hello ile tümleştirme için kayıt olayları parola sıfırlama.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Tooget hello raporlama API'si ile çalışmaya nasıl
tooaccess bu verileri toowrite küçük bir uygulama gereksinim ekleyeceksiniz veya tooretrieve komut dosyası, sunucularımızda. [Tooget Azure AD raporlama API'si ile Merhaba çalışmaya nasıl bilgi](active-directory-reporting-api-getting-started.md).

Bir çalışan betik olduktan sonra sonraki senaryolarınızı toomeet alabilirsiniz tooexamine hello parola sıfırlama ve kayıt olayları isteyeceksiniz.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): olayları parola sıfırlama için kullanılabilen hello sütunları listeler
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): kayıt olayları parola sıfırlama için kullanılabilen hello sütunları listeler

### <a name="reporting-api-data-retrieval-limitations"></a>Raporlama API veri alma sınırlamaları
Şu anda Azure AD raporları hello ve çok alır yukarı olayları API**75,000 olayları tek tek** Merhaba, [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) ve [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) türleri , hello kapsayıcı **son 30 gün**.

Tooretrieve gerekir veya bu pencereyi aşan veri depolamak, dış bir veritabanında kalıcı yapma ve neden hello API tooquery hello farkları kullanarak öneririz. En iyi uygulama parolanızı başlattığınızda bu veri alma toobegin kayıt işlemini kuruluşunuzdaki sıfırlama, harici olarak kalır ve tootrack hello farkları bu noktadan İleri devam ' dir.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>PowerShell ile hızlı bir şekilde kayıt olayları nasıl toodownload parola sıfırlama
Ayrıca toousing Merhaba Azure AD raporları ve olayları API doğrudan, dizininizde PowerShell komut dosyası toorecent kayıt olayları aşağıda hello de kullanabilirsiniz. Bu son kaydettirildi toosee istemeniz durumunda faydalı olur veya beklediğiniz gibi parolanızı sunum sıfırlama tooensure oluştuğunu gibi gerekir.

* [Azure AD SSPR'yi kayıt etkinlik PowerShell Betiği](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Merhaba Klasik Portalı'nda nasıl tooview parola yönetimi raporları
toofind hello parola yönetimi raporları, hello adımları izleyin:

1. Tıklatın hello üzerinde **Active Directory** hello uzantısında [Klasik Azure portalı](https://manage.windowsazure.com).
2. Dizininizi hello Portalı'nda görünür hello listesinden seçin.
3. Tıklatın hello üzerinde **raporları** sekmesi.
4. Konum altında hello **etkinlik günlükleri** bölümü.
5. Her iki hello seçin **parola sıfırlama etkinliği** rapor veya hello **parola sıfırlama kayıt etkinlik** rapor.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Görünüm parola sıfırlama hello Klasik Portalı'nda kaydı etkinliği
Merhaba parola sıfırlama kayıt etkinlik raporu, kuruluşunuzda oluşmuş kayıtlar tüm parola sıfırlama gösterir.  Hello parola kimlik doğrulaması bilgilerini başarılı bir şekilde kaydettirildi herhangi bir kullanıcı kayıt portalı sıfırlamak için bir parola sıfırlama kaydı Bu raporda görüntülenen ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns"></a>Rapor sütunları açıklaması
Merhaba aşağıdaki listede ayrıntılı hello rapor sütunların her biri açıklanmaktadır:

* **Kullanıcı** – bir parola deneyen hello kullanıcı sıfırlama kayıt işlemi.
* **Rol** – hello dizininde hello kullanıcı hello rolü.
* **Tarih ve saat** – hello tarih ve saat hello denemesinin.
* **Veri kayıtlı** – kayıt sırasında parola hangi kimlik doğrulama verileri hello kullanıcı tarafından sağlanan sıfırlayın.

### <a name="description-of-report-values"></a>Rapor değerlerinin açıklaması
Merhaba aşağıdaki tabloda her sütun için izin verilen hello farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kayıtlı veri |**Alternatif e-posta** – kullanıcı kullanılan alternatif e-posta veya kimlik doğrulama e-posta tooauthenticate<p><p>**Ofis telefonu**– kullanıcı kullanılan office telefon tooauthenticate<p>**Cep telefonu** -kullanıcı kullanılan cep telefonu veya kimlik doğrulama telefon tooauthenticate<p>**Güvenlik soruları** – kullanılan kullanıcı güvenlik sorularını tooauthenticate<p>**Herhangi bir bileşimini hello (örneğin, alternatif e-posta + cep telefonu) yukarıdaki** – 2 kapısı İlkesi belirtilir ve hangi iki yöntem kullanılan kullanıcı tooauthentication hello gösterir oluşur parolasını sıfırlama isteği. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Görünüm parola sıfırlama etkinliği hello Klasik portalında
Bu rapor, tüm parola sıfırlama, kuruluşunuzda oluşmuş denemeleri gösterir.

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns"></a>Rapor sütunları açıklaması
Merhaba aşağıdaki listede ayrıntılı hello rapor sütunların her biri açıklanmaktadır:

1. **Kullanıcı** – bir parola deneyen hello kullanıcı sıfırlama işlemi (Merhaba kullanıcı tooreset parola geldiğinde sağlanan hello kullanıcı kimliği temel alan).
2. **Rol** – hello dizininde hello kullanıcı hello rolü.
3. **Tarih ve saat** – hello tarih ve saat hello denemesinin.
4. **Yöntem kullanılan** – kullanılan kullanıcı kimlik doğrulama yöntemleri hello bu sıfırlama işlemi için.
5. **Sonuç** – hello nihai sonucu hello parola sıfırlama işlemi.
6. **Ayrıntılar** – neden hello parola sıfırlama ayrıntılarını hello olduğu hello değerinde sonuçlandı.  Ayrıca tooresolve beklenmeyen bir hata alabilir herhangi azaltma adımlarını içerir.

### <a name="description-of-report-values"></a>Rapor değerlerinin açıklaması
Merhaba aşağıdaki tabloda her sütun için izin verilen hello farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kullanılan yöntemler |**Alternatif e-posta** – kullanıcı kullanılan alternatif e-posta veya kimlik doğrulama e-posta tooauthenticate<p>**Ofis telefonu** – kullanıcı kullanılan office telefon tooauthenticate<p>**Cep telefonu** – kullanıcı kullanılan cep telefonu veya kimlik doğrulama telefon tooauthenticate<p>**Güvenlik soruları** – kullanılan kullanıcı güvenlik sorularını tooauthenticate<p>**Herhangi bir bileşimini hello (örneğin, alternatif e-posta + cep telefonu) yukarıdaki** – 2 kapısı İlkesi belirtilir ve hangi iki yöntem kullanılan kullanıcı tooauthentication hello gösterir oluşur parolasını sıfırlama isteği. |
| Sonuç |**Terk** – kullanıcı parola sıfırlama başladı, ancak yarı yarıya aracılığıyla tamamlamadan durdu<p>**Engellenen** – kullanıcının hesap idi önlenmiş toouse parola sıfırlama tooattempting toouse hello parola sıfırlama sayfasına veya bir 24 saatlik sürede çok sayıda ağ geçidi tek bir parola sıfırlama<p>**İptal** – kullanıcı parola sıfırlama başladı, ancak hello iptal düğmesi toocancel hello oturum parçası şekilde ile tıklattınız <p>**Yönetici ile bağlantı kurulamadı** – kullanıcı kendisinin çözümlenemedi kendi oturumu sırasında bir sorun var, hello kullanıcı sonlandırma yerine hello "yöneticinize başvurun" bağlantıyı tıklattığında şekilde akış hello parola sıfırlama<p>**Başarısız** – kullanıcı değildi mümkün tooreset büyük olasılıkla bir parola olduğundan hello kullanıcı olmayan yapılandırılmış toouse hello özelliği (örneğin kimlik bilgileri, yönetilen parola şirket içi ancak geri yazma eksik lisans, kapalıdır).<p>**Başarılı** – parola sıfırlama başarılı oldu. |
| Ayrıntılar |Aşağıdaki tabloya bakın |

### <a name="allowed-values-for-details-column"></a>İzin verilen değerler Ayrıntılar sütunu için
Sonuç türleri hello parola kullanarak Etkinlik Raporu sıfırladığınızda bekleyebilir hello listesi aşağıdadır:

| Ayrıntılar | Sonuç türü |
| --- | --- |
| Merhaba e-posta doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba mobil SMS doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba mobil sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba office sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba güvenlik soruları seçeneği tamamladıktan sonra terk kullanıcı |terk |
| Kullanıcı Kimliğini girdikten sonra terk kullanıcı |terk |
| Merhaba e-posta doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba mobil SMS doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba mobil sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba office sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba güvenlik soruları seçeneği başlattıktan sonra terk kullanıcı |terk |
| Yeni bir parola seçmeden önce terk kullanıcı |terk |
| Yeni bir parola seçerken terk kullanıcı |terk |
| Kullanıcı çok fazla geçersiz SMS doğrulama kodları girilen ve 24 saat engellendi |Engellendi |
| Kullanıcı, cep telefonu sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı office telefon sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı çok fazla kez tooanswer güvenlik soruları denedi ve 24 saat engellendi |Engellendi |
| Kullanıcı tooverify bir telefon numarası birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı gerekli hello kimlik doğrulama yöntemleri gönderilmeden önce iptal edildi. |İptal edildi |
| Kullanıcı yeni bir parola göndermeden önce iptal edildi. |İptal edildi |
| Kullanıcı bir yönetici hello e-posta doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello mobil SMS doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello mobil sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello office sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello Güvenlik sorusu doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Parola sıfırlama bu kullanıcı için etkin değil. Etkinleştir parola sıfırlama altında Merhaba yapılandırma sekmesi tooresolve bu |Başarısız oldu |
| Kullanıcı bir lisans yok. Bu lisans toohello kullanıcı tooresolve ekleyebilirsiniz. |Başarısız oldu |
| Kullanıcı bir aygıttan tooreset etkin tanımlama bilgileri çalıştı. |Başarısız oldu |
| Kullanıcı hesabı tanımlanan yetersiz kimlik doğrulama yöntemlerine sahiptir. Bu kimlik doğrulama bilgileri tooresolve Ekle |Başarısız oldu |
| Kullanıcının, yönetilen şirket içi paroladır. Bu parola geri yazma tooresolve etkinleştirebilirsiniz |Başarısız oldu |
| Şirket içi parola sıfırlama hizmetinizi erişemedi. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Merhaba kullanıcının şirket içi parolanızı sıfırlarken bir sorun oluştu. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Bu kullanıcı hello parola sıfırlama kullanıcılar grubunun bir üyesi değil. Bu kullanıcı toothat Grup tooresolve bu ekleyin. |Başarısız oldu |
| Parola sıfırlama tamamen bu Kiracı için devre dışı bırakıldı. Bkz: [burada](http://aka.ms/ssprtroubleshoot) tooresolve bu. |Başarısız oldu |
| Kullanıcı parolası başarıyla sıfırlandı |Başarılı oldu |

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki bağlantılar tooall Merhaba, Azure AD parola sıfırlama belge sayfalarının şunlardır:

* **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Nasıl çalışır** ](active-directory-passwords-how-it-works.md) -hello hizmeti ve ne altı farklı bileşeni hello hakkında bilgi edinin her mu
* [**Başlarken** ](active-directory-passwords-getting-started.md) -öğrenin nasıl tooallow, kullanıcıların tooreset ve Bulut veya şirket içi parolalarını değiştirme
* [**Özelleştirme** ](active-directory-passwords-customize.md) - toocustomize hello nasıl göründüğünü öğrenmek & kullanımında ve hello davranışını tooyour kuruluşunuzun gereksinimlerine hizmet
* [**En iyi uygulamalar** ](active-directory-passwords-best-practices.md) -nasıl tooquickly ve etkili bir şekilde kuruluşunuzdaki parolaları yönetmek öğrenin
* [**SSS** ](active-directory-passwords-faq.md) -get toofrequently sorular yanıtlanmaktadır
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -tooquickly hello hizmetinin ilgili sorunları nasıl sorun giderme öğrenin
* [**Daha fazla bilgi edinin** ](active-directory-passwords-learn-more.md) - hello hizmetinin nasıl çalıştığı derin hello teknik ayrıntılar uygulamasına gidin
