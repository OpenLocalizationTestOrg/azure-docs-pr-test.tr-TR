---
title: "Azure AD Connect eşitleme: userCertificate özniteliği tarafından işleme LargeObject hatalardır | Microsoft Docs"
description: "Bu konuda userCertificate özniteliği tarafından LargeObject hatalardır hello düzeltme adımları sağlar."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Azure AD Connect eşitleme: userCertificate özniteliği tarafından kaynaklanan işleme LargeObject hataları

Azure AD, bir üst sınır zorlar **15** sertifika hello değerlerine **userCertificate** özniteliği. Azure AD Connect 15'ten fazla değerleri tooAzure AD sahip bir nesne aktarır, Azure AD'ye verir. bir **LargeObject** hata iletisi:

>*"hello sağlanan nesne çok büyük. Bu nesnedeki öznitelik değerleri Hello sayısı kesim. Merhaba işlemi hello sonraki eşitleme döngüsünde yeniden denenecek..."*

Diğer AD öznitelikleri tarafından Hello LargeObject hata neden olabilir. Bu gerçekten nedeni hello userCertificate özniteliği tarafından tooconfirm tooverify ya da şirket içi AD hello nesnesine karşı veya hello ihtiyacınız [Eşitleme Hizmeti Yöneticisi'ni meta veri deposu arama](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

tooobtain hello LargeObject hatalarla kiracınızda nesnelerin listesini yöntemler aşağıdaki hello birini kullanın:

 * Kiracınız için Azure AD Connect Health Eşitleme etkinse toohello başvurabilir [eşitleme hata raporu](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) sağlanan.
 
 * Her eşitleme döngüsü hello sonunda gönderilen hello bildirim e-posta için dizin eşitleme hatalarına LargeObject hataları nesneleriyle hello listesine sahiptir. 
 * Merhaba [Eşitleme Hizmeti Yöneticisi'ni işlemleri sekmesinde](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) hello son verme tooAzure AD işlemi tıklatırsanız hello LargeObject hataları olan nesnelerin listesini görüntüler.
 
## <a name="mitigation-options"></a>Azaltma seçenekleri
Merhaba LargeObject hata çözülene kadar aynı nesne olamaz diğer öznitelik değişiklikleri toohello tooAzure AD verildi. tooresolve hello hatası, aşağıdaki seçenekleri şu hello düşünebilirsiniz:

 * Azure AD Connect toobuild 1.1.524.0 yükseltin ya da sonra. Azure AD Connect 1.1.524.0 derleme, hello öznitelikleri 15'ten fazla değerleri varsa hello out-of-box eşitleme kuralları güncelleştirilmiş toonot verme öznitelikleri userCertificate ve userSMIMECertificate sağlanmıştır. Ayrıntılar için tooupgrade Azure AD Connect başvuran tooarticle [Azure AD Connect: son önceki bir sürüm toohello'den yükseltme](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Uygulama bir **giden eşitleme kuralı** aktarır Azure AD CONNECT'te bir **null değer 15'ten fazla sertifika değerlerle hello gerçek değerler nesneler için yerine**. Bu seçenek, herhangi bir hello sertifika değerleri dışarı toobe tooAzure AD 15'ten fazla değerlerle nesneler için ihtiyaç duymuyorsanız uygundur. Ayrıntılar için bu eşitleme kuralı, toonext bölümüne başvurun tooimplement [Implementing eşitleme kuralı toolimit verme userCertificate özniteliğinin](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Merhaba sertifika değerlerine Hello sayısını azaltın AD nesne (15 veya daha az) artık kuruluşunuz tarafından kullanılmakta olan değerleri kaldırarak şirket. Merhaba özniteliği oluşan şişirmeyi süresi dolmuş ya da kullanılmayan sertifikalar tarafından neden oluyorsa bu uygundur. Merhaba kullanabilirsiniz [PowerShell Betiği kullanılabilir burada](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp bulmak, yedekleme ve şirket içi süresi dolan sertifikaları sil AD. Hello sertifikaları silmeden önce kuruluşunuzda hello ortak anahtar altyapısı yöneticilerine olduğunu doğrulamanız önerilir.

 * Azure yapılandırma engeller AD Connect tooexclude hello userCertificate özniteliği dışarı tooAzure AD. Microsoft Online Services tooenable belirli senaryolar tarafından Hello özniteliği kullanılabilir beri genel olarak, bu seçenek önermiyoruz. Özellikle:
    * Merhaba userCertificate öznitelik hello kullanıcı nesnesindeki ileti imzalama ve şifreleme için Exchange Online ve Outlook istemcileri tarafından kullanılır. Bu özellik hakkında daha fazla toolearn başvuran tooarticle [S/MIME ileti imzalama ve şifreleme için](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * Merhaba userCertificate öznitelik hello bilgisayar nesnesinde Azure AD tooallow Windows 10 şirket içi etki alanına katılmış aygıtlar tooconnect tooAzure AD tarafından kullanılır. Bu özellik hakkında daha fazla toolearn tooarticle başvurun [Windows 10 deneyimleri için etki alanına katılmış aygıtlar tooAzure AD Connect](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Eşitleme kuralı toolimit verme userCertificate özniteliğinin uygulama
Merhaba userCertificate özniteliği tarafından neden tooresolve hello LargeObject hata verir Azure AD Connect bir giden eşitleme kuralı uygulayabilirsiniz bir **null değer hello gerçek değerlerle nesneler için 15'ten fazla sertifika değerleriniyerine**. Bu bölüm için hello adımları gerekli tooimplement hello eşitleme kuralı açıklar **kullanıcı** nesneleri. Merhaba adımları için uyarlanabilir **kişi** ve **bilgisayar** nesneleri.

> [!IMPORTANT]
> Null değer dışarı aktarma değerleri daha önce başarıyla tooAzure AD dışarı sertifika kaldırır.

Merhaba adımları olarak özetlenebilir:

1. Eşitleme Zamanlayıcı'yı devre dışı bırakın ve devam eden bir eşitleme doğrulayın.
3. Merhaba mevcut giden eşitleme kuralı için kullanıcı sertifikasını öznitelik bulunamadı.
4. Gerekli hello giden eşitleme kuralı oluşturun.
5. Merhaba yeni eşitleme kuralı LargeObject hatasıyla var olan bir nesne üzerinde doğrulayın.
6. Merhaba yeni eşitleme kuralı tooremaining nesneler LargeObject hata uygulayın.
7. Dışa aktarılan toobe tooAzure AD bekleyen beklenmeyen bir değişiklik bulunmamaktadır doğrulayın.
8. Merhaba değişiklikleri tooAzure AD verin.
9. Eşitleme Zamanlayıcı'yı yeniden etkinleştirin.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>1. Adım Eşitleme Zamanlayıcı'yı devre dışı bırakın ve devam eden bir eşitleme doğrulayın
Yeni bir eşitleme gerçekleştirilmesinin hello ortadaki durumdayken eşitleme kurulur olun kural tooavoid istenmeyen değişiklikler olma tooAzure AD dışarı. toodisable hello yerleşik eşitleme Zamanlayıcı:
1. Hello Azure AD Connect sunucusunda PowerShell oturumu başlatın.

2. Zamanlanan eşitleme cmdlet'ini çalıştırarak devre dışı bırakın:`Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Merhaba önceki adımları yalnızca geçerli toonewer (1.1.xxx.x) Azure AD Connect hello yerleşik Zamanlayıcı ile sürümleridir. Windows Görev Zamanlayıcısı'nı kullanan Azure AD Connect eski sürümleri (1.0.xxx.x) kullanarak ya da kendi özel Zamanlayıcı (ortak değil) tootrigger düzenli aralıklarla eşitleme kullanıyorsanız, toodisable gerekir bunları uygun şekilde.

3. Merhaba Başlat **Eşitleme Hizmeti Yöneticisi'ni** giderek tooSTART → tarafından eşitleme hizmeti.

4. Toohello Git **Operations** sekmesinde ve durumu olan işlem yok onaylayın *"sürüyor."*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>2. Adım Merhaba mevcut giden eşitleme kuralı için kullanıcı sertifikasını öznitelik bulunamadı
Etkin ve tooexport userCertificate özniteliği kullanıcı nesneleri tooAzure AD için yapılandırılan mevcut bir eşitleme kuralı olması gerekir. Bu eşitleme kuralı toofind çıkışı bulun, **öncelik** ve **kapsam filtresi** yapılandırma:

1. Merhaba Başlat **eşitleme kuralları Düzenleyicisi** giderek tooSTART → tarafından Düzenleyicisi eşitleme kuralları.

2. Merhaba arama filtreleri değerleri aşağıdaki hello ile yapılandırın:

    | Öznitelik | Değer |
    | --- | --- |
    | Yön |**Giden** |
    | MV nesne türü |**Kişi** |
    | Bağlayıcı |*Azure AD Bağlayıcısı adı* |
    | Bağlayıcı nesne türü |**Kullanıcı** |
    | MV özniteliği |**kullanıcı sertifikasını** |

3. Kullanıcı nesneleri için OOB (out-of-box) eşitleme kuralları tooAzure AD Bağlayıcısı tooexport userCertficiate özniteliği kullanıyorsanız, hello geri almanız gerekir *"Out tooAAD – kullanıcı ExchangeOnline"* kuralı.
4. Merhaba Not **öncelik** bu eşitleme kuralı değeri.
5. Merhaba eşitleme kuralı seçin ve tıklatın **Düzenle**.
6. Merhaba, *"Ayrılmış kural onay Düzenle"* açılan iletişim kutusunda, tıklatın **Hayır**. (Endişelenmeyin, biz toomake herhangi bir değişiklik toothis eşitleme kural yapmayacağınız).
7. Merhaba Hello düzenleme ekranında şunları seçin **Scoping filtre** sekmesi.
8. Filtre yapılandırma kapsamı hello unutmayın. Merhaba OOB eşitleme kuralı kullanıyorsanız, tam olarak olması gerektiğini **iki yan tümceleri içeren bir kapsam filtresi grubu**dahil:

    | Öznitelik | işleci | Değer |
    | --- | --- | --- |
    | sourceObjectType | EŞİTTİR | Kullanıcı |
    | cloudMastered | EŞİT DEĞİLDİR | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>3. Adım Gerekli hello giden eşitleme kuralı oluşturma
Merhaba yeni eşitleme kuralı gerekir sahip hello aynı **kapsam filtresi** ve **daha yüksek önceliği** mevcut eşitleme kuralı hello daha. Bu, o hello yeni eşitleme kuralı aynı nesnelerin hello mevcut eşitleme kuralı ve geçersiz kılmalar hello hello userCertificate özniteliği için mevcut eşitleme kuralı olarak ayarlanan toohello geçerlidir sağlar. toocreate hello eşitleme kuralı:
1. Hello eşitleme kuralları Düzenleyicisi, hello tıklatın **Yeni Kural Ekle** düğmesi.
2. Merhaba altında **Açıklama sekmesinin**, yapılandırma aşağıdaki hello sağlayın:

    | Öznitelik | Değer | Ayrıntılar |
    | --- | --- | --- |
    | Ad | *Bir ad sağlayın* | Örneğin, *"tooAAD Out – özel geçersiz kılma için userCertificate"* |
    | Açıklama | *Bir açıklama belirtin* | Örneğin, *"UserCertificate özniteliği 15'ten fazla değerlere sahipse, NULL verin."* |
    | Bağlı sistem | *Hello Azure AD Bağlayıcısı seçin* |
    | Bağlı sistem nesne türü | **Kullanıcı** | |
    | Meta veri deposu nesne türü | **kişi** | |
    | Bağlantı türü | **Birleştir** | |
    | Önceliği | *1-99 arasında bir sayı seçtiniz* | Merhaba seçilen sayı varolan herhangi bir eşitleme kural kullanılmamalıdır ve daha düşük bir değere sahip (ve bu nedenle, daha yüksek öncelik) mevcut eşitleme kuralı hello daha. |

3. Toohello Git **Scoping filtre** sekmesinde ve aynı kapsam filtresi hello mevcut eşitleme kuralı kullanarak hello uygulayın.
4. Atla hello **katılma kuralları** sekmesi.
5. Toohello Git **dönüşümleri** tooadd kullanarak yeni bir dönüştürme yapılandırma sekmesinde:

    | Öznitelik | Değer |
    | --- | --- |
    | Akış türü |**İfade** |
    | Target özniteliği |**kullanıcı sertifikasını** |
    | Kaynak özniteliği |*İfade aşağıdaki kullanım hello*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Merhaba tıklatın **Ekle** düğmesini toocreate hello eşitleme kuralı.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>4. Adım. Merhaba yeni eşitleme kuralı LargeObject hata ile varolan bir nesnede doğrulayın
Eşitleme hello tooverify budur oluşturulan kuralın düzgün şekilde çalışıp çalışmadığını LargeObject hatasıyla bir AD nesnesinde tooother nesneleri uygulamadan önce:
1. Toohello Git **Operations** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
2. Merhaba en son verme tooAzure AD işlemi seçin ve LargeObject hatalarla hello nesnelerden birini tıklatın.
3.  Hello bağlayıcı alanı nesne özellikleri açılan ekranda, üzerinde hello tıklatın **Önizleme** düğmesi.
4. Merhaba Önizleme açılır ekranında şunları seçin **tam eşitleme** tıklatıp **Commit Önizleme**.
5. Merhaba Önizleme ekran ve hello bağlayıcı alanı nesne özellikleri ekran kapatın.
6. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
7. Merhaba üzerinde sağ **Azure AD** Bağlayıcısı ve seçin **Çalıştır...**
8. Merhaba çalıştırmak bağlayıcı açılır pencerede seçin **verme** adım ve tıklatın **Tamam**.
9. Dışarı aktarma tooAzure AD toocomplete için bekleyin ve bu belirli bir nesnede LargeObject hata hakkında daha fazla olduğunu onaylayın.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>5. Adım. Merhaba yeni eşitleme kuralı tooremaining nesneler LargeObject hata Uygula
Merhaba eşitleme kuralı eklendiğinde toorun hello AD Bağlayıcısı üzerinde tam eşitleme adım gerekir:
1. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
2. Merhaba üzerinde sağ **AD** Bağlayıcısı ve seçin **Çalıştır...**
3. Merhaba çalıştırmak bağlayıcı açılır pencerede seçin **tam eşitleme** adım ve tıklatın **Tamam**.
4. Merhaba tam eşitleme adım toocomplete için bekleyin.
5. Birden fazla AD bağlayıcıları varsa, AD bağlayıcılar kalan Merhaba Hello yukarıdaki adımları yineleyin. Genellikle, birden çok şirket içi dizin varsa, birden çok bağlayıcı gereklidir.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>6. Adım. Dışa aktarılan toobe tooAzure AD bekleyen beklenmeyen bir değişiklik bulunmamaktadır doğrulayın
1. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
2. Merhaba üzerinde sağ **Azure AD** Bağlayıcısı ve select **arama bağlayıcı alanı**.
3. Merhaba arama bağlayıcı alanı açılır penceresinde:
    1. Kapsamı çok Ayarla**bekleyen dışarı**.
    2. Dahil olmak üzere tüm 3 checkboxes denetleyin **Ekle**, **Değiştir** ve **silmek**.
    3. Tıklatın **arama** düğmesini tooreturn tüm nesneleri dışarı toobe tooAzure AD bekleyen değişikliklerle.
    4. Beklenmeyen bir değişiklik yok doğrulayın. belirli bir nesne için tooexamine hello değişiklikleri hello nesnesinde çift tıklayın.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>7. Adım. Merhaba değişiklikleri tooAzure AD dışarı aktarma
tooexport hello değişiklikleri tooAzure AD:
1. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
2. Merhaba üzerinde sağ **Azure AD** Bağlayıcısı ve seçin **Çalıştır...**
4. Merhaba çalıştırmak bağlayıcı açılır pencerede seçin **verme** adım ve tıklatın **Tamam**.
5. Dışarı aktarma tooAzure AD toocomplete için bekleyin ve daha fazla LargeObject hatalar yoktur onaylayın.

### <a name="step-8-re-enable-sync-scheduler"></a>8. adım. Eşitleme Zamanlayıcı'yı yeniden etkinleştirin
Merhaba sorun çözüldüğünde, hello yerleşik Eşitleme Zamanlayıcısı'nı yeniden etkinleştirin:
1. PowerShell oturumu başlatın.
2. Zamanlanan eşitleme cmdlet'ini çalıştırarak yeniden etkinleştirin:`Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Merhaba önceki adımları yalnızca geçerli toonewer (1.1.xxx.x) Azure AD Connect hello yerleşik Zamanlayıcı ile sürümleridir. Windows Görev Zamanlayıcısı'nı kullanan Azure AD Connect eski sürümleri (1.0.xxx.x) kullanarak ya da kendi özel Zamanlayıcı (ortak değil) tootrigger düzenli aralıklarla eşitleme kullanıyorsanız, toodisable gerekir bunları uygun şekilde.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

