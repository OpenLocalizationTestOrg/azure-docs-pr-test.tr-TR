---
title: "Get Öngörüler: Azure AD parola yönetimi raporları | Microsoft Docs"
description: "Bu makalede raporları, kuruluşunuzdaki parola yönetimi işlemleri hakkında bilgi edinme için nasıl kullanılacağını açıklar."
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
ms.openlocfilehash: ae83df618e3c392fe89878bcd1be0d6c6cb1edb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-get-operational-insights-with-password-management-reports"></a>Parola yönetimi raporlarıyla operasyonel Öngörüler alma
> [!IMPORTANT]
> **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Bu bölümde, Azure Active Directory'nin parola yönetimi raporları nasıl kullanıcılar parola sıfırlama kullanıyorsanız ve kuruluşunuzdaki değiştirmek görüntülemek için nasıl kullanabileceğinizi açıklar.

* [**Parola yönetimi raporları genel bakış**](#overview-of-password-management-reports)
* [**Yeni Azure Portalı'nda parola yönetimi raporları görüntüleme**](#how-to-view-password-management-reports)
 * [Raporları okuma izni directory rolleri](#directory-roles-allowed-to-read-reports)
* [**Self Servis parola yönetimi etkinlik türleri yeni Azure portalında**](#self-service-password-management-activity-types)
 * [Self Servis parola sıfırlama engellendi](#activity-type-blocked-from-self-service-password-reset)
 * [Parola değiştirme (Self Servis)](#activity-type-change-password-self-service)
 * [(Yönetici tarafından) parola sıfırlama](#activity-type-reset-password-by-admin)
 * [(Self Servis) parola sıfırlama](#activity-type-reset-password-self-service)
 * [Akış etkinliği ilerleme kendi hizmet vermemesini parola sıfırlama](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Kullanıcı hesabının (Self Servis) kilidi](#activity-type-unlock-user-account-self-service)
 * [Self Servis parola sıfırlama için kayıtlı kullanıcı](#activity-type-user-registered-for-self-service-password-reset)
* [**Parola yönetimi olayları Azure AD raporları ve olayları API alma**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Raporlama API veri alma sınırlamaları](#reporting-api-data-retrieval-limitations)
* [**Parola sıfırlama kayıt olayları hızla PowerShell ile karşıdan yükleme**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Klasik portalda parola yönetimi raporları görüntüleme**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Klasik Portalı'nda, kuruluşunuzdaki kayıt etkinliğini görünüm parola sıfırlama**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Görünüm parola sıfırlama etkinliği, kuruluşunuzda Klasik portalda**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Parola yönetimi raporları genel bakış
Parola sıfırlama dağıttığınızda, en yaygın sonraki adımlar, kuruluşunuzda nasıl kullanıldığını görmek için biridir.  Örneğin, hakkında bilgi edinme isteyebilirsiniz nasıl kullanıcılar parola sıfırlama veya kaç parola kaydediyorsunuz içine sıfırlar son birkaç günde yapılmış.  Parola yönetimi raporlarıyla mevcut yanıt kuramaz sık sorulan bazı [Azure Yönetim Portalı](https://manage.windowsazure.com) Bugün:

* Kaç kişinin parola sıfırlama için kayıtlı?
* Parola sıfırlama için kayıtlı olan kim?
* Verileri kaydetme kişiler nelerdir?
* Kaç kişinin son 7 gün içinde parolalarını sıfırlama?
* En yaygın yöntemleri kullanıcıları veya yöneticileri parolalarını sıfırlamak için kullanın ne var mı?
* Sık karşılaşılan sorunları kullanıcıları veya yöneticileri yüz parola sıfırlama kullanmaya çalışırken nelerdir?
* Hangi yöneticileri kendi parolalarını sık sıfırlama?
* Parola sıfırlama ile geçmeden tüm şüpheli etkinlik mi?

## <a name="how-to-view-password-management-reports"></a>Parola yönetimi raporları görüntüleme
Yeni [Azure Portal](https://portal.azure.com) deneyimi sahibiz parola sıfırlama görüntülemek için geliştirilmiş bir yol ve parola sıfırlama kayıt etkinlik.  Parola sıfırlama bulmak için aşağıdaki adımları izleyin ve parola kaydı olayları yeni sıfırlama [Azure Portal](https://portal.azure.com):

1. Gidin [ **portal.azure.com**](https://portal.azure.com)
2. Tıklayın **daha fazla hizmet** ana Azure portalında sol taraftaki gezinti menüsünde
3. Arama **Azure Active Directory** Hizmetler listesinde ve seçin
4. Tıklayın **kullanıcıları ve grupları** Azure Active Directory Gezinti menüsünde
5. Tıklayın **denetim günlüklerini** kullanıcıları ve grupları Gezinti menüsünde Gezinti öğesi. Bu, tüm denetim olaylarını ortaya çıkma tüm kullanıcılara karşı dizininizde gösterir. Bu görünüm tüm parola ile ilgili olayları de görmek için filtre uygulayabilirsiniz.
6. Parola yönetimi ile ilgili olaylar yalnızca bu görünüme filtre uygulamak için **filtre** dikey pencerenin üstündeki düğmesi.
7. Gelen **filtre** menüsünde, select **kategori** açılan listesinde ve şekilde değiştirin **Self Servis parola yönetimi** kategori türü.
8. İsteğe bağlı olarak daha fazla filtre belirli seçerek listeyi **etkinlik** ilgilendiğiniz
### <a name="direct-link-to-user-audit-blade"></a>Kullanıcı denetim dikey doğrudan bağlantı
Portalınıza açmış durumdaysanız, işte kullanıcı Denetim dikey doğrudan bağlantı burada bu olayları görebilirsiniz:

* [Kullanıcı Yönetimi denetim görünümü doğrudan gidin](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-to-read-reports"></a>Raporları okuma izni directory rolleri
Şu anda aşağıdaki dizin rollerini Klasik Azure portalında Azure AD parola yönetimi raporları okuyabilirsiniz:

* Genel yönetici

Bu raporlar okuyabilir olmaya önce genel yönetici şirket seçti kuruluş adına raporlama sekme veya denetim günlüklerini en az bir kez ziyaret ederek alınması bu veri bileşeni gerekir. Bunun yapılması kadar veri kuruluşunuz için toplanmaz.

Daha fazla bilgi için dizin rolleri ve yapabileceklerini hakkında bkz: [Azure Active Directory'de yönetici rolleri atama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Self Servis parola yönetimi etkinlik türleri
Aşağıdaki etkinlik türlerini görünür **Self Servis parola yönetimi** denetim olay kategorisi.  Bunların her biri için bir açıklama izler.

* [**Self Servis parola sıfırlama engellenen** ](#activity-type-blocked-from-self-service-password-reset) -parola sıfırlama, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulamak bir kullanıcı çalıştı gösterir.
* [**Parola (Self Servis) değiştirme** ](#activity-type-change-password-self-service) -bir kullanıcı bir gönüllü gerçekleştirilen ya da (Bitiş nedeniyle) zorunlu parola değiştirme.
* [**Parola sıfırlama (yönetici tarafından)** ](#activity-type-reset-password-by-admin) -parola sıfırlama Azure Portalı'ndan bir kullanıcı adına bir yönetici gerçekleştirilen gösterir.
* [**Parola sıfırlama (Self Servis)** ](#activity-type-reset-password-self-service) -kullanıcı başarıyla kendi parolasını sıfırlama gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* [**Kendi kendine hizmet vermemesini parola sıfırlama akış etkinliği ilerleme** ](#activity-type-self-serve-password-reset-flow-activity-progress) -sıfırlama işlemi parola parçası olarak bir kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) her belirli adım gösterir.
* [**Kullanıcı hesabının (Self Servis) kilidini** ](#activity-type-unlock-user-account-self-service) -kilidi başarıyla Active Directory hesabını bir kullanıcı parolasını gelen sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) kullanma [AD hesabının kilidini ayarlarına sıfırlamadan](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) özelliği.
* [**Kullanıcı Self Servis parola sıfırlama için kayıtlı** ](#activity-type-user-registered-for-self-service-password-reset) -bir kullanıcının parolasını sıfırlamak için gerekli tüm bilgileri kayıtlı olan veya şu anda belirtilen Kiracı parola uygun şekilde kendi parolasını sıfırlama İlkesi gösterir.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Etkinlik türü: Self Servis parola sıfırlama engellendi
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı denedi belirtir bir parola sıfırlama, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* **Etkinlik aktör** -ek gerçekleştirmesini kısıtlanan kullanıcı sıfırlama işlemlerinin. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -ek gerçekleştirmesini kısıtlanan kullanıcı sıfırlama işlemlerinin. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı kısıtlanan gösteren herhangi bir ek sıfırlar gerçekleştirmeyi, ek kimlik doğrulama yöntemleri deneyin veya sonraki 24 saat için hiçbir ek telefon numaralarını doğrulayın.
* **Etkinlik durumu hata nedeni** - geçerli değil

### <a name="activity-type-change-password-self-service"></a>Etkinlik türü: parola değiştirme (Self Servis)
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – bir kullanıcı bir gönüllü gerçekleştirilen ya da (Bitiş nedeniyle) zorunlu parola değiştirme.
* **Etkinlik aktör** -parolasını değiştiren kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolasını değiştiren kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı parolasını başarıyla değiştirildiğini gösterir
 * _Hata_ -kullanıcı başarısız parolasını değiştirmek gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu hata nedeni** -
 * _FuzzyPolicyViolationInvalidPassword_ -çok genel veya özellikle zayıf bulmakta Microsoft'un yasaklanan parola algılama özellikleri nedeniyle otomatik olarak yasaklanan bir parola seçilen kullanıcı.

### <a name="activity-type-reset-password-by-admin"></a>Etkinlik türü: (yönetici tarafından) parola sıfırlama
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – yönetici gerçekleştirilen parola Azure Portalı'ndan bir kullanıcı adına sıfırlama gösterir.
* **Etkinlik aktör** -parola sıfırlama başka bir son kullanıcı veya yönetici adına gerçekleştiren yönetici. Ya da bir genel yönetici, parola yönetici, kullanıcı veya Yardım Masası yönetici olması gerekir.
* **Etkinlik hedef** -kullanıcının parolasını sıfırlandı. Bir son kullanıcı veya farklı bir yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir yönetici kullanıcının parolası başarıyla sıfırlandı gösterir
 * _Hata_ -yönetici başarısız bir kullanıcının parolasını değiştirmek gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.

### <a name="activity-type-reset-password-self-service"></a>Etkinlik türü: parola sıfırlama (Self Servis)
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı başarıyla kendi parolasını sıfırlama belirtir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* **Etkinlik aktör** -kullanıcının parolasını sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -kullanıcının parolasını sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı, kendi parola başarıyla sıfırlandı gösterir
 * _Hata_ -bir kullanıcı, kendi parola sıfırlanamadı gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu hata nedeni** -
 * _FuzzyPolicyViolationInvalidPassword_ -çok genel veya özellikle zayıf bulmakta Microsoft'un yasaklanan parola algılama özellikleri nedeniyle otomatik olarak yasaklanan bir parola yönetici seçili.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Etkinlik türü: kendi kendine parola sıfırlama akış etkinliği ilerleme hizmet
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) sıfırlama işlemi parola parçası olarak her belirli adım gösterir.
* **Etkinlik aktör** -parola parçası gerçekleştiren kullanıcı Akış sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola parçası gerçekleştiren kullanıcı Akış sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -kullanıcı parolası sıfırlama akışının belirli bir adıma başarıyla tamamlandı gösterir.
 * _Hata_ -belirli bir adıma parola sıfırlama başarısız akış gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu nedeniyle izin verilen**
 * İçin aşağıdaki tabloya bakın [tüm sıfırlama etkinliği durumu nedeniyle izin verilen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Etkinlik türü: kullanıcı hesabı (Self Servis) kilidini aç
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kilidi başarıyla Active Directory hesabını bir kullanıcı parolasını gelen sıfırlamadan belirtir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) kullanarak [AD hesabı sıfırlama kilit açma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) özelliği.
* **Etkinlik aktör** -hesabını, parola sıfırlama olmadan kilidi kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hesabını, parola sıfırlama olmadan kilidi kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -bir kullanıcı, kendi hesabını başarıyla kilidi gösterir
 * _Hata_ -bir kullanıcı başarısız hesabını kilidini açmak gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Etkinlik türü: kullanıcı Self Servis parola sıfırlama için kayıtlı
Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – belirtir bir kullanıcının parolasını sıfırlamak için gerekli tüm bilgileri kayıtlı veya şu anda belirtilen Kiracı parola uygun şekilde kendi parolasını sıfırlama ilkesi.
* **Etkinlik aktör** -parola sıfırlama için kayıtlı olan kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola sıfırlama için kayıtlı olan kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
 * _Başarı_ -parola sıfırlama geçerli ilkesiyle uygun şekilde başarıyla kayıtlı bir kullanıcı gösterir.
 * _Hata_ -kullanıcı başarısız parola sıfırlama için kaydedilecek gösterir. Satırındaki tıklatarak etmenizi sağlar görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori. Not - Bu kullanıcı parolasını sıfırlama mümkün olmadığı anlamına veya kendi parola yalnızca o buldukça, kayıt işlemi tamamlanmadı. (Doğrulanmazsa, bir telefon numarası gibi), doğru kendi hesabındaki doğrulanmamış verileri ise bunlar bu telefon numarası doğrulanmadı olsa da, bunlar, parolasını sıfırlamak için kullanmaya devam edebilirsiniz. Daha fazla bilgi için bkz: [kullanıcı kayıtları ne olur?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Parola yönetimi olayları Azure AD raporları ve olayları API alma
Ağustos 2015'ten itibaren Azure AD raporları ve olayları API artık destekliyor parola sıfırlama ve parola sıfırlama kayıt raporlara dahil tüm bilgiler alınıyor. Bu API'yi kullanarak tek tek parola sıfırlama indirebilirsiniz ve kayıt olayları, choce raporlama teknolojisi ile tümleştirme için parola sıfırlama.

### <a name="how-to-get-started-with-the-reporting-api"></a>Nasıl raporlama API'si ile çalışmaya başlama
Bu verilere erişmek için küçük uygulama veya bizim sunuculardan verileri almak için komut dosyası yazmanız gerekir. [Azure AD raporlama API'si ile çalışmaya başlama öğrenin](active-directory-reporting-api-getting-started.md).

Bir çalışan betik olduktan sonra sonraki senaryolarınızı karşılayacak şekilde alabilirsiniz parola sıfırlama ve kayıt olayları inceleyin istersiniz.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): olayları parola sıfırlama için kullanılabilen sütunları listeler
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): kayıt olayları parola sıfırlama için kullanılabilen sütunları listeler

### <a name="reporting-api-data-retrieval-limitations"></a>Raporlama API veri alma sınırlamaları
Şu anda Azure AD raporları ve olayları API alır kadar **75,000 olayları tek tek** , [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) ve [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) türleri kapsayıcı **son 30 gün**.

Almak veya bu pencereyi aşan veri depolamak gerekiyorsa, dış bir veritabanında kalıcı yapma ve neden farkları sorgulamak için API kullanarak öneririz. Parolanızı başlattığınızda bu verileri kayıt işlemini kuruluşunuzdaki sıfırlama, harici olarak kalır ve bu noktadan itibaren farkları izlemek devam alma başlamak en iyi bir uygulamadır.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Parola sıfırlama kayıt olayları hızla PowerShell ile karşıdan yükleme
Azure AD raporları ve olayları API kullanarak doğrudan ek olarak, ayrıca kullanabilirsiniz PowerShell Betiği dizininizde yeni kayıt olayları aşağıda. Kim son kayıtlı olan veya beklediğiniz gibi parola sıfırlama sunum oluştuğunu sağlamak istediğiniz görmek istediğiniz durumlarda kullanışlıdır.

* [Azure AD SSPR'yi kayıt etkinlik PowerShell Betiği](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-to-view-password-management-reports-in-the-classic-portal"></a>Klasik portalda parola yönetimi raporları görüntüleme
Parola yönetimi raporları bulmak için aşağıdaki adımları izleyin:

1. Tıklayın **Active Directory** uzantısı'nda [Klasik Azure portalı](https://manage.windowsazure.com).
2. Dizininiz portalda görünen listesinden seçin.
3. Tıklayın **raporları** sekmesi.
4. Kısmına bakın **etkinlik günlükleri** bölümü.
5. Şunlardan birini seçin **parola sıfırlama etkinliği** rapor veya **parola sıfırlama kayıt etkinlik** rapor.

## <a name="view-password-reset-registration-activity-in-the-classic-portal"></a>Klasik Portalı'nda kaydı etkinliği görünüm parola sıfırlama
Parola sıfırlama kayıt etkinlik raporu, kuruluşunuzda oluşmuş kayıtlar tüm parola sıfırlama gösterir.  Parola kimlik doğrulaması bilgilerini başarılı bir şekilde kaydettirildi herhangi bir kullanıcı kayıt portalı sıfırlamak için bir parola sıfırlama kaydı Bu raporda görüntülenen ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns"></a>Rapor sütunları açıklaması
Aşağıdaki listede ayrıntılı raporu sütunların her biri açıklanmaktadır:

* **Kullanıcı** – bir parola deneyen kullanıcıya kayıt işlemi sıfırlayın.
* **Rol** – dizindeki kullanıcı rolü.
* **Tarih ve saat** – tarih ve saat girişimi.
* **Veri kayıtlı** – hangi kimlik doğrulama verileri kullanıcı sağlanan sırasında parola sıfırlama kaydı.

### <a name="description-of-report-values"></a>Rapor değerlerinin açıklaması
Aşağıdaki tabloda her sütun için izin verilen farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kayıtlı veri |**Alternatif e-posta** – kullanıcı kimlik doğrulaması için alternatif e-posta veya kimlik doğrulama e-posta kullanılır<p><p>**Ofis telefonu**– kimlik doğrulaması için kullanılan kullanıcı ofis telefonu<p>**Cep telefonu** -kullanıcı kullanılan cep telefonu veya kimlik doğrulaması için kimlik doğrulama telefon<p>**Güvenlik soruları** – kullanıcı kimlik doğrulaması için güvenlik soruları kullanılır<p>**Yukarıdakilerden herhangi bir birleşimini (örneğin, alternatif e-posta + cep telefonu)** – 2 kapısı İlkesi belirtilir ve kullanılan kullanıcı hangi iki yöntemi gösterilir oluşur kimlik doğrulama parolasını sıfırlama isteği. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Görünüm parola sıfırlama etkinliği Klasik portalda
Bu rapor, tüm parola sıfırlama, kuruluşunuzda oluşmuş denemeleri gösterir.

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns"></a>Rapor sütunları açıklaması
Aşağıdaki listede ayrıntılı raporu sütunların her biri açıklanmaktadır:

1. **Kullanıcı** – bir parola denemesi kullanıcının (kullanıcı parola sıfırlama geldiğinde sağlanan kullanıcı kimliği temel alan) işlemi Sıfırla.
2. **Rol** – dizindeki kullanıcı rolü.
3. **Tarih ve saat** – tarih ve saat girişimi.
4. **Yöntem kullanılan** – kullanıcının bu için kullanılan kimlik doğrulama yöntemleri sıfırlama işlemi.
5. **Sonuç** – sonuç parola sıfırlama işlemi.
6. **Ayrıntılar** – neden parola sıfırlama ayrıntılarını olduğu değerle sonuçlandı.  Ayrıca beklenmeyen bir hata çözümlemek için sürebilir herhangi azaltma adımlarını içerir.

### <a name="description-of-report-values"></a>Rapor değerlerinin açıklaması
Aşağıdaki tabloda her sütun için izin verilen farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kullanılan yöntemler |**Alternatif e-posta** – kullanıcı kimlik doğrulaması için alternatif e-posta veya kimlik doğrulama e-posta kullanılır<p>**Ofis telefonu** – kimlik doğrulaması için kullanılan kullanıcı ofis telefonu<p>**Cep telefonu** – kullanıcı kullanılan cep telefonu veya kimlik doğrulaması için kimlik doğrulama telefon<p>**Güvenlik soruları** – kullanıcı kimlik doğrulaması için güvenlik soruları kullanılır<p>**Yukarıdakilerden herhangi bir birleşimini (örneğin, alternatif e-posta + cep telefonu)** – 2 kapısı İlkesi belirtilir ve kullanılan kullanıcı hangi iki yöntemi gösterilir oluşur kimlik doğrulama parolasını sıfırlama isteği. |
| Sonuç |**Terk** – kullanıcı parola sıfırlama başladı, ancak yarı yarıya aracılığıyla tamamlamadan durdu<p>**Engellenen** – kullanıcı hesabının engelledi parola sıfırlama sayfası kullanmak için parola sıfırlama çalışırken nedeniyle kullanmanızı veya bir 24 saatlik sürede çok sayıda ağ geçidi tek bir parola sıfırlama<p>**İptal** – kullanıcı parola sıfırlama başladı, ancak parçası şekilde ile oturum iptal etmek için İptal düğmesine tıklandığında <p>**Yönetici ile bağlantı kurulamadı** – kullanıcı kendisinin çözümlenemedi kendi oturumu sırasında bir sorun var, kullanıcı tamamlama yerine "yöneticinize başvurun" bağlantısına tıkladığınız için akış parola sıfırlama<p>**Başarısız** – kullanıcı, kullanıcı (örneğin kimlik bilgileri, yönetilen parola şirket içi ancak geri yazma eksik lisans, kapalıdır) özelliğini kullanmak için yapılandırılmadığı için büyük olasılıkla bir parola sıfırlama mümkün değildi.<p>**Başarılı** – parola sıfırlama başarılı oldu. |
| Ayrıntılar |Aşağıdaki tabloya bakın |

### <a name="allowed-values-for-details-column"></a>İzin verilen değerler Ayrıntılar sütunu için
Parola kullanarak Etkinlik Raporu sıfırladığınızda bekleyebilir sonuç türleri listesi aşağıdadır:

| Ayrıntılar | Sonuç türü |
| --- | --- |
| Kullanıcı e-posta doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Kullanıcı mobil SMS doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Kullanıcı mobil sesli arama doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Office sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Kullanıcı seçeneği sorular güvenlik tamamladıktan sonra bırakıldı |terk |
| Kullanıcı Kimliğini girdikten sonra terk kullanıcı |terk |
| Kullanıcı e-posta doğrulama seçeneğini başlattıktan sonra terk |terk |
| Kullanıcı mobil SMS doğrulama seçeneğini başlattıktan sonra terk |terk |
| Kullanıcı mobil sesli arama doğrulama seçeneğini başlattıktan sonra terk |terk |
| Office sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Kullanıcı güvenlik başlangıç seçeneği sorular sonra bırakıldı |terk |
| Yeni bir parola seçmeden önce terk kullanıcı |terk |
| Yeni bir parola seçerken terk kullanıcı |terk |
| Kullanıcı çok fazla geçersiz SMS doğrulama kodları girilen ve 24 saat engellendi |Engellendi |
| Kullanıcı, cep telefonu sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı office telefon sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı güvenlik sorularını birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı bir telefon numarası çok fazla kez doğrulamaya çalıştı ve 24 saat engellendi |Engellendi |
| Gerekli kimlik doğrulama yöntemlerini geçirmeden önce kullanıcı iptal etti |İptal edildi |
| Kullanıcı yeni bir parola göndermeden önce iptal edildi. |İptal edildi |
| Kullanıcı bir yönetici e-posta doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı mobil SMS doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı mobil sesli arama doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici office sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı Güvenlik sorusu doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Parola sıfırlama bu kullanıcı için etkin değil. Parola sıfırlama bu sorunu çözmek için Yapılandır sekmesi altında etkinleştir |Başarısız oldu |
| Kullanıcı bir lisans yok. Bu sorunu çözmek için kullanıcıya bir lisans ekleyebilirsiniz. |Başarısız oldu |
| Kullanıcı tanımlama bilgilerinin etkin bir aygıttan sıfırlamaya |Başarısız oldu |
| Kullanıcı hesabı tanımlanan yetersiz kimlik doğrulama yöntemlerine sahiptir. Bu sorunu çözmek için kimlik bilgisi ekleyin |Başarısız oldu |
| Kullanıcının, yönetilen şirket içi paroladır. Bu sorunu gidermek parola geri yazma özelliğini etkinleştirme |Başarısız oldu |
| Şirket içi parola sıfırlama hizmetinizi erişemedi. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Kullanıcının sıfırlama parola içi ederken bir sorun oluştu. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Bu kullanıcının parola sıfırlama kullanıcılar grubunun bir üyesi değil. Bu kullanıcıyı bu sorunu çözmek için bu gruba ekleyin. |Başarısız oldu |
| Parola sıfırlama tamamen bu Kiracı için devre dışı bırakıldı. Bkz: [burada](http://aka.ms/ssprtroubleshoot) bu sorunu gidermek için. |Başarısız oldu |
| Kullanıcı parolası başarıyla sıfırlandı |Başarılı oldu |

## <a name="next-steps"></a>Sonraki adımlar
Aşağıda, tüm Azure AD Parola Sıfırlama belge sayfalarının bağlantıları verilmiştir:

* **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Nasıl çalışır?**](active-directory-passwords-how-it-works.md) - Hizmetin altı farklı bileşeni ve işlevleri hakkında bilgi edinin
* [**Başlarken** ](active-directory-passwords-getting-started.md) -sıfırlamak ve Bulut veya şirket içi parolalarını değiştirmek kullanıcıların öğrenin
* [**Özelleştirin**](active-directory-passwords-customize.md) - Hizmetin genel görünümünü ve hareketlerini kuruluşunuzun ihtiyaçlarına göre nasıl özelleştireceğinizi öğrenin
* [**En iyi uygulamalar**](active-directory-passwords-best-practices.md) - Kuruluşunuzdaki parolaları nasıl hızlı bir şekilde dağıtacağınızı ve etkili bir şekilde yöneteceğinizi öğrenin
* [**SSS**](active-directory-passwords-faq.md) - Sık sorulan soruların yanıtlarını alın
* [**Sorunları giderin**](active-directory-passwords-troubleshoot.md) - Hizmetle ilgili sorunların hızlı bir şekilde nasıl giderileceğini öğrenin
* [**Daha fazla bilgi edinin**](active-directory-passwords-learn-more.md) - Hizmetin çalışma biçimine ilişkin teknik bilgileri ayrıntılı olarak inceleyin
