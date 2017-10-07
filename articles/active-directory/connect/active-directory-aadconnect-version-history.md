---
title: "Azure AD Connect: Sürüm yayımlama geçmişi | Microsoft Docs"
description: "Bu makalede Azure AD Connect ve Azure AD eşitleme'nin tüm sürümlerinde listeler"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: Sürüm yayımlama geçmişi
Hello Azure Active Directory (Azure AD) ekibi, yeni özellikler ve işlevsellik ile Azure AD Connect düzenli olarak güncelleştirir. Tüm ekleme geçerli tooall izleyicileri şunlardır.

Bu makalede, izlemek çıkarılan hello sürümleri tasarlanmış toohelp ve toounderstand olan veya olmayan tooupdate toohello en yeni sürüme gerekip gerekmediği.

İlgili Konular listesidir:


Konu |  Ayrıntılar
--------- | --------- |
Azure AD Connect adımları tooupgrade | Farklı yöntemler çok[son önceki bir sürüm toohello'den yükseltme](active-directory-aadconnect-upgrade-previous-version.md) Azure AD Connect sürüm.
Gerekli izinler | Bir güncelleştirme tooapply gereken izinler için bkz: [hesapları ve izinleri](./active-directory-aadconnect-accounts-permissions.md#upgrade).
İndir| [Azure AD Connect'i indirme](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Durum: 23 Temmuz 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Sabit sorunu

* Merhaba out-of-box eşitleme kuralı neden olan sorunu sabit "Out tooAD - kullanıcı İmmutableıd" toobe kaldırıldı:

  * Azure AD Connect yükseltildiğinde Hello sorun oluşur veya ne zaman, görev seçeneği hello *güncelleştirme eşitleme yapılandırması* kullanılan tooupdate Azure AD Connect eşitleme yapılandırması hello Azure AD Connect sihirbazıdır.
  
  * Bu eşitleme kuralı hello etkinleştirdiyseniz geçerli toocustomers olan [msDS-ConsistencyGuid kaynak bağlantısı özellik olarak](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Bu özellik sürümünde 1.1.524.0 ve sonra sunulmuştur. Merhaba eşitleme kuralı kaldırıldığında, Azure AD Connect artık şirket içi doldurabilir AD ms DS ConsistencyGuid özniteliğiyle hello objectGUID özniteliğinin değeri. Yeni kullanıcıların Azure AD ile sağlanan engellemez.
  
  * Merhaba özelliği etkin olduğu sürece bu hello eşitleme kuralı artık yükseltme sırasında ya da yapılandırma değişikliği sırasında kaldırılacak hello düzeltme sağlar. Bu sorundan etkilenen mevcut müşteriler için geri Azure AD Connect toothis sürümüne yükseltme yaptıktan sonra bu hello eşitleme kuralı eklenir hello düzeltme de sağlar.

* Out-of-box eşitleme kuralları 100'den az toohave öncelik değeri neden olan bir sorunu sabit:

  * Genel olarak, öncelik değerler 0 - 99 özel eşitleme kuralları için ayrılmıştır. Yükseltme sırasında hello öncelik out-of-box eşitleme kuralları için güncelleştirilmiş tooaccommodate eşitleme kuralı değişiklikleri değerlerdir. Toothis sorunu out-of-box eşitleme kuralları 100'den az öncelik değeri atanabilir.
  
  * Merhaba düzeltme hello sorunu yükseltme sırasında oluşmasını engeller. Ancak, bunu hello öncelik değerleri hello sorundan etkilenen mevcut müşteriler geri yüklemez. Ayrı bir düzeltme hello gelecekteki toohelp hello geri yükleme ile de sağlanır.

* Bir sorun hello yerlerde sabit [etki alanı ve OU filtreleme ekran](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect Sihirbazı'nı gösteren *tüm etki alanları ve OU'lar eşitleme* seçeneği olarak seçili OU tabanlı filtreleme etkinleştirilmiş olsa bile.

*   Bir sorun nedeniyle bu hello sabit [dizin bölümlerini Yapılandır ekran](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) hello Eşitleme Hizmeti Yöneticisi'ni tooreturn hello ise hata olarak *yenileme* düğmesine tıklandığında. Merhaba hata iletisi *"etki alanları yenilenirken bir hata oluştu: %s toocast nesne türü 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Merhaba hata yeni AD etki alanı tooan var olan AD ormanına eklendi ve tooupdate Azure çalıştığınız oluşur hello Yenile düğmesini kullanarak AD Bağlan.

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri

* [Otomatik yükseltme özelliği](active-directory-aadconnect-feature-automatic-upgrade.md) yapılandırmaları aşağıdaki hello genişletilmiş toosupport müşterilerle bırakıldı:
  * Merhaba cihaz geri yazma özelliğini etkinleştirdiniz.
  * Merhaba grup geri yazma özelliğini etkinleştirdiniz.
  * Merhaba yüklemesi hızlı ayarları veya DirSync yükseltme değil.
  * 100. 000'den fazla nesneleri hello meta veri deposunda sahiptir.
  * Bir ormandaki daha toomore bağlanırsınız. Hızlı Kurulum yalnızca tooone orman bağlanır.
  * Merhaba AD Bağlayıcısı hesabı hello varsayılan MSOL_ hesabı artık değil.
  * Merhaba sunucu hazırlama modu toobe ayarlanır.
  * Merhaba kullanıcı geri yazma özelliğini etkinleştirdiniz.
  
  >[!NOTE]
  >Otomatik yükseltme hello özelliğinin Hello kapsamı genişletme sonra Azure AD Connect yapı 1.1.105.0 ile müşterileri etkiler. Otomatik olarak yükseltme, Azure AD Connect sunucusu toobe istemiyorsanız, Azure AD Connect sunucunuzda aşağıdaki cmdlet'i çalıştırmanız gerekir: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Etkinleştirme/otomatik yükseltme devre dışı bırakma hakkında daha fazla bilgi için tooarticle başvuran [Azure AD Connect: Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Durum: yayımlanan değil. Bu yapı değişiklikleri sürüm 1.1.561.0 dahil edilir.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Sabit sorunu

* Merhaba out-of-box eşitleme kuralı "çıkış tooAD - kullanıcı İmmutableıd" neden olan sorunu sabit toobe ne zaman kaldırılan OU tabanlı filtreleme yapılandırma güncelleştirilir. Bu eşitleme kuralı Merhaba gereklidir [msDS-ConsistencyGuid kaynak bağlantısı özellik olarak](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Bir sorun hello yerlerde sabit [etki alanı ve OU filtreleme ekran](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect Sihirbazı'nı gösteren *tüm etki alanları ve OU'lar eşitleme* seçeneği olarak seçili OU tabanlı filtreleme etkinleştirilmiş olsa bile.

*   Bir sorun nedeniyle bu hello sabit [dizin bölümlerini Yapılandır ekran](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) hello Eşitleme Hizmeti Yöneticisi'ni tooreturn hello ise hata olarak *yenileme* düğmesine tıklandığında. Merhaba hata iletisi *"etki alanları yenilenirken bir hata oluştu: %s toocast nesne türü 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Merhaba hata yeni AD etki alanı tooan var olan AD ormanına eklendi ve tooupdate Azure çalıştığınız oluşur hello Yenile düğmesini kullanarak AD Bağlan.

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri

* [Otomatik yükseltme özelliği](active-directory-aadconnect-feature-automatic-upgrade.md) yapılandırmaları aşağıdaki hello genişletilmiş toosupport müşterilerle bırakıldı:
  * Merhaba cihaz geri yazma özelliğini etkinleştirdiniz.
  * Merhaba grup geri yazma özelliğini etkinleştirdiniz.
  * Merhaba yüklemesi hızlı ayarları veya DirSync yükseltme değil.
  * 100. 000'den fazla nesneleri hello meta veri deposunda sahiptir.
  * Bir ormandaki daha toomore bağlanırsınız. Hızlı Kurulum yalnızca tooone orman bağlanır.
  * Merhaba AD Bağlayıcısı hesabı hello varsayılan MSOL_ hesabı artık değil.
  * Merhaba sunucu hazırlama modu toobe ayarlanır.
  * Merhaba kullanıcı geri yazma özelliğini etkinleştirdiniz.
  
  >[!NOTE]
  >Otomatik yükseltme hello özelliğinin Hello kapsamı genişletme sonra Azure AD Connect yapı 1.1.105.0 ile müşterileri etkiler. Otomatik olarak yükseltme, Azure AD Connect sunucusu toobe istemiyorsanız, Azure AD Connect sunucunuzda aşağıdaki cmdlet'i çalıştırmanız gerekir: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Etkinleştirme/otomatik yükseltme devre dışı bırakma hakkında daha fazla bilgi için tooarticle başvuran [Azure AD Connect: Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Durum: Temmuz 2017

>[!NOTE]
>Bu yapı hello Azure AD Connect Yükseltmesi otomatik özelliği aracılığıyla kullanılabilir toocustomers değil.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Sabit sorunu
* Geçerli bir etki alanı hala olsa bile, değiştirilen hello varolan hizmet bağlantı noktası nesne toobe üzerinde yapılandırılmış hello doğrulanmış etki alanının neden hello Initialize-ADSyncDomainJoinedComputerSync cmdlet ile ilgili bir sorun düzeltilmiştir. Azure AD kiracınıza hello hizmet bağlantı noktası yapılandırmak için kullanılan birden fazla doğrulanan etki alanına sahip olduğunda bu sorun oluşur.

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri
* Parola geri yazma için Microsoft Azure kamu Bulut ve Microsoft Cloud Almanya önizlemesi kullanıma sunulmuştur. Hello farklı hizmet örneği için Azure AD Connect destek hakkında daha fazla bilgi için tooarticle başvuran [Azure AD Connect: özel konular örnekleri](active-directory-aadconnect-instances.md).

* Merhaba Initialize-ADSyncDomainJoinedComputerSync cmdlet'ine şimdi AzureADDomain adlı yeni bir isteğe bağlı parametre vardır. Bu parametre hangi hello hizmet bağlantı noktası yapılandırmak için kullanılan etki alanı toobe doğrulandı belirtmenize olanak sağlar.

### <a name="pass-through-authentication"></a>Doğrudan Kimlik Doğrulama

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri
* Merhaba Aracısı doğrudan kimlik doğrulama değiştirildi için gerekli Hello adını *Microsoft Azure AD uygulama ara sunucusu Bağlayıcısı* çok*Microsoft Azure AD Connect kimlik doğrulama Aracısı*.

* Doğrudan kimlik doğrulama artık etkinleştirme parola karması eşitlemesi varsayılan olarak etkinleştirir.


## <a name="115530"></a>1.1.553.0
Durum: Haziran 2017

> [!IMPORTANT]
> Bu yapı içinde sunulan şema ve eşitleme kuralı değişiklikler vardır. Azure AD Connect eşitleme hizmeti yükseltmeden sonra tam içeri aktarma ve tam eşitleme adımları tetikler. Merhaba değişikliklerinin ayrıntılarını aşağıda açıklanmıştır. tootemporarily yükseltmeden sonra tam içeri aktarma ve tam eşitleme adımları erteleneceği, tooarticle başvuran [nasıl toodefer tam eşitleme yükselttikten sonra](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect Sync

#### <a name="known-issue"></a>Bilinen bir sorun
* Kullanan müşteriler etkileyen bir sorun [OU tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) Azure AD Connect eşitleme ile. Gidin zaman toohello [etki alanı ve OU filtreleme sayfası](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect Sihirbazı'nda, aşağıdaki davranış hello bekleniyor:
  * OU tabanlı filtreleme etkinleştirilirse hello **seçilen etki alanları ve OU'lar eşitleme** seçeneği işaretlidir.
  * Aksi takdirde hello **tüm etki alanları ve OU'lar eşitleme** seçeneği işaretlidir.

Merhaba ortaya bu hello sorundur **tüm etki alanları ve OU'lar seçeneği eşitleme** hello Sihirbazı'nı çalıştırdığınızda, her zaman işaretlidir.  OU tabanlı filtreleme önceden yapılandırılmış olsa bile bu oluşur. AAD Connect yapılandırma değişiklikleri kaydetmeden önce emin hello olun **seçili etki alanı eşitleme ve OU'lar seçeneği belirlendiğinde** ve toosynchronize gereken tüm OU'larda yeniden etkinleştirildiğini onaylayın. Aksi takdirde, OU tabanlı filtreleme devre dışı bırakılır.

#### <a name="fixed-issues"></a>Giderilen sorunlar

* Bir sorun sabit bir şirket içi hello parolasını bir Azure AD Yöneticisi tooreset veren parola geri yazma ile AD ayrıcalıklı kullanıcı hesabı. Azure AD Connect hello ayrıcalıklı hesap hello parola sıfırlama izin verildiğinde hello sorun oluşur. Merhaba sorunu ele hello Yöneticisi hello hesabının sahibi söz konusu değilse bu sürümünde bir Azure AD Yöneticisi tooreset rasgele şirket içi hello parolasını sağlayarak değil, Azure AD Connect, AD kullanıcı hesabı ayrıcalıklı. Daha fazla bilgi için çok başvurun[güvenlik önerisi 4033453](https://technet.microsoft.com/library/security/4033453).

* İlgili bir sorun sabit toohello [msDS-ConsistencyGuid kaynak bağlantısı olarak](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) burada Azure AD Connect mu değil geri yazma tooon içi özelliği AD msDS-ConsistencyGuid özniteliği. birden çok şirket içi olduğunda hello sorun AD ormanına eklenen tooAzure AD Connect ve hello *kullanıcı kimlikleri arasında birden çok dizin seçeneği mevcut* seçilir. Bu tür yapılandırma kullanıldığında, hello sonuç eşitleme kuralları hello sourceAnchorBinary hello meta veri deposu özniteliğinde doldurmayın. Merhaba sourceAnchorBinary öznitelik, msDS-ConsistencyGuid özniteliği için hello kaynak özniteliği kullanılır. Sonuç olarak, geri yazma toohello ms-DSConsistencyGuid özniteliği gerçekleşmez. toofix hello sorun, aşağıdaki eşitleme kuralları meta veri deposu her zaman doldurulur hello sourceAnchorBinary özniteliğinde hello güncelleştirilmiş tooensure bırakıldı:
  * İçinde AD'den - InetOrgPerson AccountEnabled.xml
  * İçinde AD'den - InetOrgPerson Common.xml
  * İçinde AD'den - kullanıcı AccountEnabled.xml
  * İçinde AD'den - kullanıcı Common.xml
  * İçinde AD - kullanıcı katılımı SOAInAAD.xml

* Daha önce hatta hello varsa [msDS-ConsistencyGuid kaynak bağlantısı olarak](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) özelliği etkin değil, hello "tooAD Out – kullanıcı İmmutableıd" tooAzure AD eşitleme kuralı eklenen hala Bağlan. Merhaba etkisi çalıştırmak ve msDS-ConsistencyGuid özniteliği toooccur geri yazma neden olmaz. tooavoid Karışıklığı önlemek için eşitleme kuralı hello tooensure hello özelliği etkinleştirilmişse, yalnızca eklenen mantığı eklendi.

* Parola karma eşitlemesi toofail hata olayı 611 neden bir sorun düzeltilmiştir. Daha fazla etki alanı denetleyicileri kaldırılmış olan şirket içi AD veya bir sonra bu sorun oluşur. Verilen eşitleme tanımlama bilgisi her parola eşitleme döngüsü Hello sonunda hello şirket içi AD USN (güncelleştirme sıra numarası) değeri 0 olan çağırma kimlikleri kaldırılan hello etki alanı denetleyicilerinin içerir. Parola Eşitleme Yöneticisi Hello oluşturulamıyor toopersist eşitleme tanımlama bilgisi içeren USN değeri 0 ve hata olayı 611 başarısız olur. Merhaba sonraki eşitleme sırasında döngüsü, USN değeri 0 içermeyen Parola Eşitleme Yöneticisi yeniden kullanır hello son kalıcı eşitleme tanımlama bilgisi hello. Bu, aynı parola değişikliğini hello neden olur getirilmesinden toobe. Bu düzeltmeyle, doğru şekilde hello eşitleme tanımlama bilgisi hello Parola Eşitleme Yöneticisi devam ettirir.

* Daha önce Otomatik yükseltme hello Set-ADSyncAutoUpgrade cmdlet'i kullanılarak devre dışı bırakılmış olsa bile hello otomatik yükseltme işlemi toocheck yükseltme için düzenli olarak devam eder ve indirilen hello yükleyici toohonor disablement üzerinde dayanır. Bu düzeltmeyle hello otomatik yükseltme işlemi artık yükseltme için düzenli olarak denetler. Bu Azure AD Connect sürümü için yükseltme yükleyici kez yürütüldüğünde hello düzeltme otomatik olarak uygulanır.

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri

* Daha önce hello [msDS-ConsistencyGuid kaynak bağlantısı olarak](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) özelliği olan yalnızca kullanılabilir toonew dağıtımları. Şimdi, kullanılabilir tooexisting dağıtımları geldi. Daha ayrıntılı belirtmek gerekirse:
  * tooaccess hello özelliği, hello Azure AD Connect Sihirbazı'nı başlatın ve hello seçin *güncelleştirme kaynak bağlantısı* seçeneği.
  * Bu seçenek yalnızca objectGUID olarak sourceAnchor özniteliği kullanılarak görünen tooexisting dağıtımlar olur.
  * Merhaba seçeneği yapılandırırken, Başlangıç Sihirbazı'nı şirket içi Active Directory'de hello msDS-ConsistencyGuid özniteliği hello durumunu doğrular. Merhaba özniteliği hello dizinde herhangi bir kullanıcı nesnesindeki yapılandırılmazsa hello Sihirbazı hello msDS-ConsistencyGuid hello sourceAnchor özniteliği olarak kullanır. Merhaba dizininde bir veya daha fazla kullanıcı nesnelerinde Hello özniteliği yapılandırdıysanız, Başlangıç Sihirbazı'nı hello özniteliği diğer uygulamalar tarafından kullanılıyor ve sourceAnchor özniteliği olarak uygun değil ve hello kaynak bağlantısı değişiklik tooproceed izin vermez sonlanır. Bu hello özniteliği var olan uygulamalar tarafından kullanılmaz, nasıl toosuppress hata hello hakkında bilgi için destek toocontact gerekir.

* Belirli çok**userCertificate** cihaz nesneleri, Azure AD Connect artık öznitelikte arar için gerekli sertifikaları değerler için [etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimi için AD bağlanma](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) ve tooAzure AD eşitlemeden önce hello rest çıkış filtreleri. Bu davranış, "tooAAD - cihaz Katıl SOAInAD" Merhaba out-of-box eşitleme kuralı güncelleştirilmiş tooenable.

* Azure AD Connect şimdi destekler geri yazma Exchange Online **cloudPublicDelegates** özniteliği tooon içi AD **publicDelegates** özniteliği. Bu, bir Exchange Online posta kutusu SendOnBehalfTo hakları toousers ile şirket içi Exchange posta kutusu olduğu verilebilir hello senaryosu sağlar. toosupport bu özellik, yeni bir out-of-box eşitleme kuralı "Out tooAD – kullanıcı Exchange karma PublicDelegates geri yazma" eklendi. Bu eşitleme kuralı yalnızca tooAzure AD eklenir Exchange karma özelliği etkinleştirilmişse, bağlanın.

*   Merhaba eşitleme azure AD Connect şimdi destekler **altRecipient** Azure AD'den özniteliği. Out-of-box eşitleme kuralları aşağıdaki bu değişiklik, olmuştur toosupport tooinclude hello gerekli öznitelik akışı güncelleştirildi:
  * İçinde AD'den – kullanıcı Exchange
  * TooAAD – kullanıcı ExchangeOnline
  
* Merhaba **cloudSOAExchMailbox** hello meta veri deposu özniteliği belirli bir kullanıcının veya Exchange Online posta kutusu sahip olup olmadığını gösterir. Tanımına güncelleştirilmiş tooinclude bırakıldı tür donanım ve Konferans odası posta kutularını olarak ek Exchange Online RecipientDisplayTypes. Bu değişiklik, hello tanımı "Olarak gelen AAD – kullanıcı Exchange karma", out-of-box eşitleme kuralı altında bulunan hello cloudSOAExchMailbox özniteliğin tooenable gelen güncelleştirilmiştir:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello aşağıdaki:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* Eşitleme kuralı ifadeleri toohandle sertifika değerlerini hello userCertificate özniteliğinde oluşturmak için X509Certificate2 uyumlu işlevlerin eklenen hello aşağıdakileri ayarlayın:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|Certthumbprınt|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Şunu seçin:|
    |CertKeyAlgorithmParams|CertHashString|Burada|
    |||İle|

* Şema değişiklikleri izleyen sunulan tooallow müşteriler toocreate özel eşitleme kuralları tooflow sAMAccountName, domainNetBios ve Grup nesneleri için domainFQDN yanı sıra, kullanıcı nesnelerinin distinguishedName sağlanmıştır:

  * Aşağıdaki öznitelikler tooMV şema eklenmiştir:
    * Grup: AccountName
    * Grup: domainNetBios
    * Grup: domainFQDN
    * Kişi: distinguishedName

  * Aşağıdaki öznitelikler tooAzure AD Bağlayıcısı şema eklenmiştir:
    * Grup: OnPremisesSamAccountName
    * Grup: NetBiosName
    * Grup: DNSEtkiAlanıAdı
    * Kullanıcı: OnPremisesDistinguishedName

* Merhaba ADSyncDomainJoinedComputerSync cmdlet betik şimdi AzureEnvironment adlı yeni bir isteğe bağlı parametre vardır. Merhaba, hangi bölge hello karşılık gelen Azure Active Directory Kiracı içinde barındırılan kullanılan toospecify parametresidir. Geçerli değerler şunlardır:
  * AzureCloud (varsayılan)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Güncelleştirilmiş eşitleme kuralı Düzenleyicisi toouse bağlantı türünün hello varsayılan değer olarak (sağlamak yerine) eşitleme kuralı oluşturma sırasında katılın.

### <a name="ad-fs-management"></a>AD FS Yönetimi

#### <a name="issues-fixed"></a>Giderilen sorunlar

* URL'leri Azure AD kimlik doğrulama kesinti karşı tooimprove dayanıklılık tarafından sunulan yeni WS-Federasyon uç noktaları ve eklenen tooon içi taraf güven yapılandırması yanıtlama AD FS olacaktır:
  * https://ests.Login.microsoftonline.com/Login.srf
  * https://stamp2.Login.microsoftonline.com/Login.srf
  * https://ccs.Login.microsoftonline.com/Login.srf
  * https://ccs-sdf.Login.microsoftonline.com/Login.srf
  
* AD FS toogenerate yanlış talep değeri için IssuerID neden bir sorun düzeltilmiştir. Merhaba sorun hello Azure AD Kiracı ve hello userPrincipalName kullanılan öznitelik toogenerate hello etki alanı soneki birden çok doğrulanmış etki alanı varsa hello IssuerID talep olan en az 3 düzeyleri derin (örneğin, johndoe@us.contoso.com). Merhaba talep kuralları tarafından kullanılan hello regex güncelleştirerek Hello sorun çözüldüğünde.

#### <a name="new-features-and-improvements"></a>Yeni özellikleri ve geliştirmeleri
* Daha önce Azure AD Connect tarafından sağlanan hello ADFS sertifika yönetimi özelliği yalnızca Azure AD Connect aracılığıyla yönetilen ADFS grupları ile kullanılır. Şimdi, Azure AD Connect'i kullanarak yönetilmeyen ADFS grupları ile Merhaba özelliğini kullanabilirsiniz.

## <a name="115240"></a>1.1.524.0
Yayımlanma tarihi: Mayıs 2017

> [!IMPORTANT]
> Bu yapı içinde sunulan şema ve eşitleme kuralı değişiklikler vardır. Azure AD Connect eşitleme hizmeti yükseltmeden sonra tam içeri aktarma ve tam eşitleme adımları tetikler. Merhaba değişikliklerinin ayrıntılarını aşağıda açıklanmıştır.
>
>

**Giderilen sorunlar:**

Azure AD Connect Eşitleme

* Müşteri hello kümesi ADSyncAutoUpgrade cmdlet'ini kullanarak hello özelliğini devre dışı bıraktı olsa bile, Otomatik yükseltme toooccur hello Azure AD Connect sunucuda neden olan bir sorun düzeltilmiştir. Bu düzeltmeyle hello hello sunucuda otomatik yükseltme işlemi hala yükseltme için düzenli olarak denetler ancak hello indirilen yükleyiciyi geliştirir hello otomatik yükseltme yapılandırma.
* DirSync yerinde yükseltme sırasında Azure AD Connect Azure AD ile eşitlemek için hello Azure AD Bağlayıcısı tarafından kullanılan bir Azure AD hizmet hesabı toobe oluşturur. Merhaba hesabı oluşturulduktan sonra Azure AD Connect hello hesabı kullanarak Azure AD ile kimliğini doğrular. Bazı durumlarda, sırayla DirSync yerinde yükseltme toofail hatasıyla neden olan kimlik doğrulama geçici sorunları nedeniyle başarısız *"yapılandırma AAD eşitleme görevini yürütme bir hata oluştu: AADSTS50034: toosign bu uygulamaya hello hesabı toohello xxx.onmicrosoft.com directory eklenmesi gerekir."* Merhaba esnekliğini DirSync yükseltme tooimprove, Azure AD Connect artık hello kimlik doğrulama adımı yeniden dener.
* Yapı 443 ile DirSync yerinde yükseltme toosucceed neden olan bir sorun oluştu, ancak dizin eşitlenmesi için gereken çalıştırma profillerini oluşturulmaz. Mantığı düzeltme bu Azure AD Connect derlemede dahil edilir. Müşteri toothis yapı yükseltildiğinde, Azure AD Connect çalıştırma profillerini eksik algılar ve bunları oluşturur.
* Parola Eşitleme işlemi toofail toostart olay kimliği 6900 ve hata neden olan bir sorunu sabit *"Merhaba aynı anahtarı zaten eklenmiş bir öğesiyle"*. Yapılandırma tooinclude AD yapılandırma bölümü filtreleme OU güncelleştirirseniz bu sorun oluşur. Bu sorun, parola eşitleme işlem şimdi toofix AD etki alanı bölümlerini yalnızca parola değişikliklerini eşitler. Yapılandırma bölümü gibi etki alanı dışı bölümleri atlanır.
* Hızlı yükleme sırasında bir şirket içi Azure AD Connect oluşturur AD DS hesap toobe hello AD Bağlayıcısı toocommunicate şirket içi tarafından kullanılan AD. Daha önce hello kullanıcı hesabı denetimi öznitelikte hello PASSWD_NOTREQD bayrağı hello hesabı oluşturulur ve rasgele bir parola hello hesabında ayarlanır. Şimdi, Azure AD Connect, açıkça Hello parola hello hesabında ayarlandıktan sonra hello PASSWD_NOTREQD bayrağını kaldırır.
* DirSync yükseltme toofail hatasıyla neden olan bir sorunu sabit *"kilitlenme sql Server'da hangi çalışırken tooacquire bir uygulama kilidi oluştu"* hello mailNickname özniteliği hello bulunduğunda şirket içi AD şema, ancak değil sınırlanmış toohello AD kullanıcı nesne sınıfı.
* Sabit bir yöneticinin Azure AD Connect Sihirbazı'nı kullanarak Azure AD Connect eşitleme yapılandırması güncelleştirilirken cihaz geri yazma özelliğini tooautomatically neden olan bir sorunu devre dışı. Merhaba varolan cihaz geri yazma yapılandırmasında şirket içi AD ve hello denetimi başarısız bu hello Sihirbazı gerçekleştirme Önkoşul denetimi tarafından kaynaklanır. Cihaz geri yazma zaten daha önce etkinleştirilmişse hello düzeltme tooskip hello olup olmadığını denetler.
* OU filtreleme, hello Azure AD Connect Sihirbazı'nı kullanın veya Eşitleme Hizmeti Yöneticisi'ni hello tooconfigure. Hello Azure AD Connect Sihirbazı tooconfigure OU filtreleme kullanırsanız, daha önce oluşturduğunuz yeni OU'lar daha sonra için dizin eşitleme dahil edilir. Dahil edilen yeni OU'lar toobe istemiyorsanız, OU yapılandırmalısınız hello Eşitleme Hizmeti Yöneticisi'ni kullanarak filtreleme. Şimdi, elde edebilirsiniz hello Azure AD Connect Sihirbazı'nı kullanarak aynı davranışı.
* Yönetici, yerine hello dbo şemasında altında yükleme hello hello şeması altında oluşturulan Azure AD Connect toobe gerektirdiği saklı yordamlar neden olan bir sorunu sabit.
* Azure AD toobe hello AAD Connect sunucu olay günlükleri atlanmış tarafından döndürülen hello Trackingıd özniteliği neden olan bir sorunu sabit. Azure AD Connect, Azure AD'den bir yeniden yönlendirme iletisi alır ve Azure AD Connect sağlanan oluşturulamıyor tooconnect toohello uç nokta ise Hello sorun oluşur. Merhaba Trackingıd, sorun giderme sırasında hizmet tarafı günlükleri ile destek mühendisleri toocorrelate tarafından kullanılır.
* Azure AD Connect Azure AD'den LargeObject hata aldığında, Azure AD Connect EventID 6941 ve ileti sahip bir olay oluşturur *"Merhaba sağlanan nesne çok büyük. Bu nesnedeki öznitelik değerleri Hello sayısı kırpma."* Merhaba aynı zaman, Azure AD Connect ayrıca EventID 6900 ve ileti yanıltıcı bir olay oluşturur *"Microsoft.Online.Coexistence.ProvisionRetryException: oluşturulamıyor toocommunicate hello Windows ile Azure Active Directory Hizmeti."* toominimize Karışıklığı önlemek için Azure AD Connect artık LargeObject hata alındığında hello ikinci olay oluşturur.
* Merhaba Eşitleme Hizmeti Yöneticisi'ni toobecome yanıt vermeyen tooupdate hello yapılandırması için genel LDAP Bağlayıcısı çalışırken neden olan bir sorunu sabit.

**Yeni özellikler/iyileştirmeleri:**

Azure AD Connect Eşitleme
* Eşitleme kuralı değişiklikleri – hello aşağıdaki eşitleme kuralı değişiklikler uygulanmamış olabilir:
  * Güncelleştirilmiş varsayılan eşitleme kural kümesi toonot dışarı aktarım öznitelikleri **userCertificate** ve **userSMIMECertificate** hello öznitelikleri 15'ten fazla değerleri varsa.
  * AD öznitelikleri **EmployeeID** ve **msExchBypassModerationLink** şimdi hello varsayılan eşitleme kuralı kümesine eklenir.
  * AD özniteliği **fotoğraf** varsayılan eşitleme kuralı kümesinden kaldırılmıştır.
  * Eklenen **preferredDataLocation** toohello meta veri deposu şeması ve AAD bağlayıcı şema. Azure AD içinde her iki öznitelik uygulayabilirsiniz tooupdate özel isteyen müşteriler kuralları toodo şekilde eşitleyin. hello özniteliği hakkında daha fazla toofind tooarticle bölümüne başvurun [Azure AD Connect eşitleme: nasıl toomake değişiklik toohello varsayılan yapılandırması - PreferredDataLocation etkinleştir eşitlenmesi](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Eklenen **userType** toohello meta veri deposu şeması ve AAD bağlayıcı şema. Azure AD içinde her iki öznitelik uygulayabilirsiniz tooupdate özel isteyen müşteriler kuralları toodo şekilde eşitleyin.

* Otomatik olarak etkinleştirir hello ConsistencyGuid özniteliği olarak kullanımını hello kaynak bağlantısı öznitelik için AD nesnelerini şirket içi şimdi, azure AD Connect. Boş ise daha, Azure AD Connect hello ConsistencyGuid özniteliği hello objectGUID özniteliğinin değeri ile doldurur. Yalnızca geçerli toonew dağıtımı özelliğidir. Bu özellik hakkında daha fazla toofind tooarticle bölümüne başvurun [Azure AD Connect: tasarım kavramları - sourceAnchor msDS-ConsistencyGuid kullanarak](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Invoke-ADSyncDiagnostics süredir cmdlet sorun giderme yeni eklenen toohelp tanılamak parola karma eşitlemesi ile ilgili sorunlar. Hello cmdlet kullanma hakkında daha fazla bilgi için tooarticle başvuran [Parola Eşitleme ile Azure AD Connect eşitleme sorunlarını giderme](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect eşitleme Mail-Enabled ortak klasör destekler nesnelerin artık AD tooAzure AD şirket içi. İsteğe bağlı özellikler altında Azure AD Connect Sihirbazı kullanarak hello özelliğini etkinleştirebilirsiniz. Bu özellik hakkında daha fazla toofind başvuran tooarticle [şirket içi posta etkinleştirilmiş ortak klasörleri Office 365 dizin dayalı kenar engelleme desteği](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect gerektiren bir AD DS hesap toosynchronize şirket içi AD. Daha önce Azure AD Connect yüklediyseniz hello hızlı mod, kullanarak hello bir Kurumsal Yönetici hesabının kimlik bilgilerini sağlayabilir ve Azure AD Connect gerekli hello AD DS hesap oluşturursunuz. Bununla birlikte, özel bir yükleme ve ormanlar tooan var olan dağıtım eklemek için gerekli tooprovide hello AD DS hesabı yerine yoktu. Şimdi, özel bir yükleme sırasında bir Kurumsal Yönetici hesabının kimlik bilgilerini hello ve gerekli hello AD DS hesabı oluşturma Azure AD Connect izin hello seçeneği tooprovide da vardır.
* Azure AD Connect artık SQL AOA destekler. Azure AD Connect yüklemeden önce SQL AOA etkinleştirmeniz gerekir. Yükleme sırasında Azure AD Connect veya sağlanan hello SQL örneği için SQL AOA etkin olup olmadığını algılar. SQL AOA etkinleştirilirse, daha fazla Azure AD Connect SQL AOA yapılandırılmış toouse zaman uyumlu veya zaman uyumsuz çoğaltma olup olmadığını rakamlar. Kullanılabilirlik grubu dinleyicisi Hello ayarlarken hello RegisterAllProvidersIP özelliği too0 ayarlamanız önerilir. Azure AD Connect SQL Native Client tooconnect tooSQL şu anda kullandığı ve SQL Native Client hello MultiSubNetFailover özelliğinin kullanımını desteklemez nedeni budur.
* Yerel veritabanı hello veritabanı olarak Azure AD Connect sunucunuz için kullandığınız ve 10 GB boyut sınırına ulaştı, hello eşitleme hizmeti artık başlatır. Daha önce tooperform hello LocalDB tooreclaim SHRINKDATABASE işlemi hello eşitleme hizmeti toostart için yeterli DB alanı gerekir. Sonra da, kullanım hello Eşitleme Hizmeti Yöneticisi'ni toodelete daha fazla DB alan geçmişi tooreclaim çalıştırabilirsiniz. Artık, geçmiş verileri LocalDB tooreclaim DB alanından çalıştırma başlangıç ADSyncPurgeRunHistory cmdlet toopurge kullanabilirsiniz. Ayrıca, bu cmdlet Çevrimdışı mod destekler (belirterek hello - offline parametresini) olduğunda kullanılır eşitleme hizmeti hello olabilen çalışmıyor. Not: hello çevrimdışı modda yalnızca hello eşitleme hizmeti çalışmıyor ve kullanılan hello veritabanı LocalDB ise kullanılabilir.
* tooreduce hello depolama alanı miktarı gerekli, artık Azure AD Connect yerel veritabanı/SQL veritabanlarında depolamadan önce eşitleme hata ayrıntıları sıkıştırır. Azure AD Connect toothis sürümü eski bir sürümden yükseltirken, Azure AD Connect üzerinde var olan eşitleme hata ayrıntılarını bir kerelik sıkıştırma gerçekleştirir.
* Daha önce OU filtreleme yapılandırması güncelleştirdikten sonra elle çalıştırmanız gerekir tam içeri aktarma tooensure varolan düzgün dahil/dizin eşitlemesini dışlanan nesneleridir. Şimdi, Azure AD Connect tam içeri aktarma otomatik olarak tetikler hello sonraki eşitleme sırasında döngüsü. Daha fazla, tam alma hello güncelleştirmesinden etkilenen uygulanan toohello AD bağlayıcıları yalnızca olabilir. Not: Bu geliştirme yalnızca hello Azure AD Connect Sihirbazı kullanılarak yapılan güncelleştirmeler filtreleme geçerli tooOU ' dir. Merhaba Eşitleme Hizmeti Yöneticisi kullanılarak yapılan güncelleştirme filtreleme geçerli tooOU değil.
* Daha önce kullanıcıları, grupları, Grup tabanlı filtreleme destekler ve kişi yalnızca nesneleri. Şimdi, Grup tabanlı filtreleme ayrıca bilgisayar nesneleri destekler.
* Daha önce Azure AD Connect Eşitleme Zamanlayıcısı'nı devre dışı bırakmadan bağlayıcı alanı verilerini silebilirsiniz. Şimdi, o hello Zamanlayıcı algılarsa hello bağlayıcı alanı veri eşitleme hizmeti Yöneticisi'ni blokları hello silinmesini etkinleştirildi. Ayrıca, bir uyarı Hello bağlayıcı alanı verilerini silinirse olası veri kaybı tooinform müşterilerinden döndürülür.
* Daha önce Azure AD Connect Sihirbazı toorun için PowerShell transcription doğru devre dışı bırakmalısınız. Bu sorunu kısmen çözümlenir. Azure AD Connect Sihirbazı toomanage eşitleme yapılandırması kullanıyorsanız, PowerShell transcription etkinleştirebilirsiniz. Azure AD Connect Sihirbazı toomanage ADFS yapılandırması kullanıyorsanız, PowerShell transcription devre dışı bırakmanız gerekir.



## <a name="114860"></a>1.1.486.0
Yayımlanma tarihi: Nisan 2017

**Giderilen sorunlar:**
* Burada Azure AD Connect'i başarıyla yerelleştirilmiş Windows Server sürümünde yüklenmez Hello sorun düzeltilmiştir.

## <a name="114840"></a>1.1.484.0
Yayımlanma tarihi: Nisan 2017

**Bilinen sorunlar:**

* Koşullar aşağıdaki hello tümü doğru olduğunda bu sürümü, Azure AD Connect'in başarılı bir şekilde yüklenmez:
   1. Ya da DirSync yerinde yükseltme veya yeni Azure AD Connect yüklemesi yapıyorsunuz.
   2. Burada "Yöneticiler" Merhaba hello sunucusunda yerleşik yönetici grubunun adını değil Windows Server'ın yerelleştirilmiş bir sürümün kullanıyor.
   3. Merhaba varsayılan SQL Server 2012 Express yerine kendi tam SQL sağlayan Azure AD Connect ile yüklenen LocalDB kullanıyor.

**Giderilen sorunlar:**

Azure AD Connect Eşitleme
* Çalıştırma profili bu eşitleme adımı için bir veya daha fazla bağlayıcılar eksikse hello eşitleme Zamanlayıcı hello tüm eşitleme adım burada atlar bir sorun düzeltilmiştir. Örneğin, el ile çalıştırma profili için bir Delta alma oluşturmadan hello Eşitleme Hizmeti Yöneticisi'ni kullanarak bir bağlayıcı eklendi. Bu düzeltme, o hello eşitleme Zamanlayıcı toorun Delta içeri aktarma için diğer bağlayıcıları devam sağlar.
* Bir sorun olduğu hello eşitleme hizmeti hemen çalıştırma profili işlemeyi durdurur sabit olduğu zaman çalıştırın hello adımlardan biri ile ilgili bir sorunu karşılaşır. Bu düzeltme, hello adım çalıştıran ve tooprocess hello rest devam eşitleme hizmeti atlar sağlar. Örneğin, bir Delta alma (her AD etki alanı içi) ile birden çok çalışma adımları çalıştırma profili AD Bağlayıcısı için gerekir. bunlardan biri ağ bağlantısı sorunları olsa bile hello eşitleme hizmeti ile Merhaba Delta içeri aktarma diğer AD etki alanları çalıştırın.
* Otomatik yükseltme sırasında atlandı hello Azure AD Bağlayıcısı güncelleştirme toobe neden olan bir sorunu sabit.
* Bir sorun sabit Bu nedenler Azure AD Connect tooincorrectly olup olmadığını belirleme hello sunucu bir etki alanı denetleyicisi toofail yükseltme hangi Aç nedenler DirSync kurulumu sırasında.
* Sabit DirSync yerinde yükseltme toonot oluşturma herhangi neden olan bir sorunu profili hello Azure AD Bağlayıcısı için çalıştırın.
* Bir sorun olduğu hello Eşitleme Hizmeti Yöneticisi kullanıcı arabirimi tooconfigure genel LDAP Bağlayıcısı çalışırken yanıt vermeyi sabit.

AD FS Yönetimi
* Merhaba AD FS birincil düğüm taşınan tooanother sunucu yüklediyse hello Azure AD Connect Sihirbazı nerede başarısız bir sorun düzeltilmiştir.

Masaüstü SSO
* Bir sorun olduğu hello oturum açma ekranında, parola eşitleme, oturum açma seçeneği yeni yüklemesi sırasında olarak seçerseniz, Masaüstü SSO özelliği etkinleştirmek izin vermez hello Azure AD Connect Sihirbazı'nda sabit.

**Yeni özellikler/iyileştirmeleri:**

Azure AD Connect Eşitleme
* Azure AD Connect eşitleme artık hello kullanımını sanal hizmet hesabı, yönetilen hizmet hesabı ve Grup yönetilen hizmet hesabı hizmet hesabı olarak destekler. Bu, yalnızca Azure AD Connect toonew yüklemesi geçerlidir. Azure AD Connect yüklerken:
    * Varsayılan olarak, Azure AD Connect Sihirbazı sanal bir hizmet hesabı oluşturur ve hizmet hesabı olarak kullanır.
    * Bir etki alanı denetleyicisinde yüklüyorsanız, Azure AD Connect burada bir etki alanı kullanıcı hesabı oluşturur ve bunun yerine, hizmet hesabı olarak kullandığı tooprevious davranışı geri döner.
    * Merhaba aşağıdakilerden birini sağlayarak hello varsayılan davranışı geçersiz kılabilirsiniz:
      * Bir grup yönetilen hizmet hesabı
      * Yönetilen hizmet hesabı
      * Bir etki alanı kullanıcı hesabı
      * Yerel bir kullanıcı hesabı
* Daha önce Azure AD Connect içeren yeni derleme tooa yükseltirseniz bağlayıcılar güncelleştirin veya eşitleme kuralı değişiklikleri, Azure AD Connect bir tam eşitleme döngüsü tetikler. Şimdi, Azure AD Connect seçmeli olarak tam alma adımı güncelleştirme bağlayıcıları için yalnızca ve yalnızca eşitleme kuralı değişikliklerle bağlayıcıları için tam eşitleme adımı tetikler.
* Daha önce dışarı aktarma silme eşiği hello yalnızca hello eşitleme Zamanlayıcı tetiklenen tooexports geçerlidir. Şimdi, hello özelliğini el ile Merhaba Eşitleme Hizmeti Yöneticisi'ni kullanarak hello müşteri tarafından tetiklenen tooinclude dışarı genişletilir.
* Azure AD kiracınıza veya parola eşitleme özelliği kiracınız için etkin olup olmadığını gösteren bir hizmet yapılandırması yok. Daha önce hello hizmet yapılandırma toobe etkin ve Hazırlama sunucusu varsa, Azure AD Connect tarafından yanlış yapılandırılmış için kolaydır. Şimdi, Azure AD Connect tookeep hello hizmet yapılandırması, etkin ile tutarlı çalışacak yalnızca Azure AD Connect sunucusu.
* Sihirbaz şimdi algılar ve bir uyarı verir azure AD Connect AD AD geri dönüşüm kutusu etkin olmayan şirket içi.
* Daha önce AD zaman aşımına uğradı ve hello hello nesnelerin hello toplu iş boyutu birleştirildiğinde başarısız verme tooAzure belirli eşiği aşıyor. Şimdi, Hello sorunla karşılaşılırsa hello eşitleme hizmeti tooresend hello nesneleri ayrı, daha küçük gruplar halinde yeniden deneyecek.
* Merhaba eşitleme hizmeti anahtar yönetimi uygulaması Windows Başlat menüsünden kaldırılmıştır. Şifreleme anahtarı yönetimi miiskmu.exe kullanarak komut satırı arabirimi aracılığıyla desteklenen toobe devam eder. Şifreleme anahtarını yönetme hakkında daha fazla bilgi için tooarticle başvurun [Abandoning hello Azure AD Connect eşitleme şifreleme anahtarı](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Hello Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirirseniz, hello şifreleme anahtarı terk ve hello Azure AD Connect eşitleme hizmeti hesabının parolasını yeniden kadar daha önce hello eşitleme hizmeti mümkün başlangıç doğru olmaz. Şimdi, bu artık gerekli değildir.

Masaüstü SSO

* Azure AD Connect Sihirbazı artık doğrudan kimlik doğrulama ve Masaüstü SSO yapılandırırken hello ağda açılan bağlantı noktası 9090 toobe gerektirir. Yalnızca bağlantı noktası 443 gereklidir. 

## <a name="114430"></a>1.1.443.0
Yayımlanma tarihi: Mart 2017

**Giderilen sorunlar:**

Azure AD Connect Eşitleme
* Hello Azure AD Bağlayıcısı Hello görünen adını hello ilk onmicrosoft.com etki alanı atanan toohello Azure AD Kiracı içermiyorsa, Azure AD Connect Sihirbazı toofail neden olan bir sorun düzeltilmiştir.
* Azure AD Connect Sihirbazı toofail hello eşitleme hizmeti hesabını hello parolasını kesme işareti, virgül ve boşluk gibi özel karakterler içeriyorsa, bağlantı tooSQL veritabanı yaparken neden olan bir sorun düzeltilmiştir.
* Hazırlama modunda bir Azure AD Connect sunucusunda toooccur "Merhaba dimage hello görüntüden daha farklı bir bağlantı var" Merhaba hata neden olan bir sorunu sabit, sonra geçici olarak Dışladığınız bir şirket içi AD nesne eşitlenmesini ve onu yeniden dahil eşitleniyor.
* Hazırlama modundaki bir Azure AD Connect sunucusu üzerinde "Merhaba nesne DN bulunan hayali olduğu" toooccur hello hata neden olan bir sorunu sabit, sonra geçici olarak Dışladığınız bir şirket içi AD nesne eşitlenmesini ve ardından, yeniden eşitleme için dahil.

AD FS Yönetimi
* Burada Azure AD Connect Sihirbazı değil AD FS yapılandırmasını güncelleştirin ve hello alternatif oturum açma Kimliğini yapılandırıldıktan sonra bağlı olan taraf güveni hello sağ talep kümesi bir sorun düzeltilmiştir.
* Azure AD Connect Sihirbazı oluşturulamıyor toocorrectly tanıtıcı AD FS sunucuları, hizmet hesapları yerine sAMAccountName biçimi userPrincipalName biçimi kullanılarak yapılandırılmış olan olduğu bir sorun sabit.

Doğrudan Kimlik Doğrulama
* Azure AD Connect Sihirbazı toofail geçirmek aracılığıyla kimlik doğrulaması seçildiğinde ancak kendi bağlayıcı kaydı başarısız olursa neden olan bir sorun düzeltilmiştir.
* Azure AD Connect Sihirbazı toobypass doğrulama Masaüstü SSO özelliği etkinleştirilmişse, seçili oturum açma yöntemi üzerinde denetler neden olan bir sorun düzeltilmiştir.

Parola sıfırlama
* Hello Azure AAD Connect sunucu toonot girişimi toore neden olabilecek bir sorun sabit-bağlanmak hello Bağlantısı Güvenlik Duvarı veya proxy tarafından sonlandırıldı.

**Yeni özellikler/iyileştirmeleri:**

Azure AD Connect Eşitleme
* Get-ADSyncScheduler cmdlet şimdi SyncCycleInProgress adlı yeni bir Boolean özelliği döndürür. Merhaba değeri döndürülürse true, zamanlanmış eşitleme döngüsü sürmekte olduğu anlamına gelir.
* Azure AD Connect yükleme ve Kurulum günlüklerini depolamak için hedef klasör %localappdata%\AADConnect too%programdata%\AADConnect tooimprove erişilebilirlik toohello günlük dosyalarından taşındı.

AD FS Yönetimi
* AD FS sunucu grubu SSL sertifikasını güncelleştirmek için destek eklendi.
* AD FS 2016 yönetmek için destek eklendi.
* Şimdi, AD FS yükleme sırasında mevcut gMSA (Grup yönetilen hizmet hesabı) belirtebilirsiniz.
* Azure AD bağlı olan taraf güveni hello imza karma algoritma olarak SHA-256 artık yapılandırabilirsiniz.

Parola sıfırlama
* Geliştirmeleri tooallow hello ürün toofunction ortamlarda daha sıkı güvenlik duvarı kuralları ile kullanıma sunuldu.
* Geliştirilmiş bağlantı güvenilirlik tooAzure hizmet veri yolu.

## <a name="113800"></a>1.1.380.0
Yayımlanma tarihi: Aralık 2016

**Sabit sorunu:**

* Bu derlemede sabit hello sorun nerede hello issuerid talep kuralı Active Directory Federasyon Hizmetleri (AD FS) eksik.

>[!NOTE]
>Bu yapı hello Azure AD Connect Yükseltmesi otomatik özelliği aracılığıyla kullanılabilir toocustomers değil.

## <a name="113710"></a>1.1.371.0
Yayımlanma tarihi: Aralık 2016

**Bilinen bir sorun:**

* Bu derlemede Hello issuerid talep kuralı AD FS için eksik. Azure Active Directory (Azure AD) ile birden çok etki alanı ad'niz hello issuerid talep kuralı gereklidir. Şirket içi Azure AD Connect toomanage kullanıyorsanız, AD FS dağıtımı, toothis yapı yükseltme, AD FS yapılandırmasından hello varolan issuerid talep kuralı kaldırır. Merhaba yükleme/yükseltme sonrasında hello issuerid talep kuralı ekleyerek hello sorunun geçici çözümü. Merhaba issuerid ekleme ile ilgili ayrıntılar talep kuralı, toothis makale üzerinde bakın [Azure AD ile Federasyon için çoklu etki alanı desteği](active-directory-aadconnect-multiple-domains.md).

**Sabit sorunu:**

* Merhaba giden bağlantı için bağlantı noktası 9090 açılmadı hello Azure AD Connect yüklemesi veya yükseltmesi başarısız olur.

>[!NOTE]
>Bu yapı hello Azure AD Connect Yükseltmesi otomatik özelliği aracılığıyla kullanılabilir toocustomers değil.

## <a name="113700"></a>1.1.370.0
Yayımlanma tarihi: Aralık 2016

**Bilinen sorunlar:**

* Bu derlemede Hello issuerid talep kuralı AD FS için eksik. Azure AD ile birden çok etki alanı ad'niz hello issuerid talep kuralı gereklidir. Şirket içi Azure AD Connect toomanage kullanıyorsanız, AD FS dağıtımı, toothis yapı yükseltme, AD FS yapılandırmasından hello varolan issuerid talep kuralı kaldırır. Hello sorunun geçici çözümü için yükleme/yükseltme sonrasında hello issuerid talep kuralı ekleyerek. Kural issuerid ekleme ile ilgili ayrıntılar talep, toothis makale üzerinde bakın [Azure AD ile Federasyon için çoklu etki alanı desteği](active-directory-aadconnect-multiple-domains.md).
* Bağlantı noktası 9090 açık giden toocomplete yükleme olmalıdır.

**Yeni Özellikler:**

* Doğrudan kimlik doğrulama (Önizleme).

>[!NOTE]
>Bu yapı hello Azure AD Connect Yükseltmesi otomatik özelliği aracılığıyla kullanılabilir toocustomers değil.

## <a name="113430"></a>1.1.343.0
Yayımlanma tarihi: Kasım 2016

**Bilinen bir sorun:**

* Bu derlemede Hello issuerid talep kuralı AD FS için eksik. Azure AD ile birden çok etki alanı ad'niz hello issuerid talep kuralı gereklidir. Şirket içi Azure AD Connect toomanage kullanıyorsanız, AD FS dağıtımı, toothis yapı yükseltme, AD FS yapılandırmasından hello varolan issuerid talep kuralı kaldırır. Hello sorunun geçici çözümü için yükleme/yükseltme sonrasında hello issuerid talep kuralı ekleyerek. Kural issuerid ekleme ile ilgili ayrıntılar talep, toothis makale üzerinde bakın [Azure AD ile Federasyon için çoklu etki alanı desteği](active-directory-aadconnect-multiple-domains.md).

**Giderilen sorunlar:**

* Bazı durumlarda, oluşturulamıyor toocreate parolasını hello kuruluşunuzun parola ilkesi tarafından belirtilen karmaşıklık hello düzeyi karşılayan bir yerel hizmet hesabı olduğundan Azure AD Connect yükleme başarısız olur.
* Merhaba bağlayıcı alanı içindeki bir nesneyi aynı anda kapsam dışı olduğunda burada birleştirme kuralları yeniden değerlendirilerek olmayan bir sorunu sabit bir birleştirme kuralı ve kapsam içinde hale başka için. Bu durum, birleştirme koşulları karşılıklı olarak birbirini dışlar iki veya daha fazla birleşim kurallar varsa meydana gelebilir.
* Bir sorun birleştirme kuralları içeren olandan daha düşük öncelik değerleri varsa birleştirme kuralları içeren değil, gelen eşitleme kurallarından (Azure AD), burada işlenmez sabit.

**İyileştirmeleri:**

* Windows Server 2016 standart veya yüksek Azure AD Connect'i yüklemek için destek eklendi.
* SQL Server 2016 için Azure AD Connect hello Uzak veritabanı olarak kullanmak için destek eklendi.

## <a name="112810"></a>1.1.281.0
Yayımlanma tarihi: Ağustos 2016

**Giderilen sorunlar:**

* Değişiklikleri toosync aralığı değil ele yer hello sonra bir sonraki eşitleme döngüsü tamamlanana kadar.
* Azure AD Connect Sihirbazı, kullanıcı adı alt çizgi ile başlayan bir Azure AD hesabının kabul etmedi (\_).
* Azure AD Connect Sihirbazı Hello hesap parolası çok fazla özel karakterler içeriyorsa tooauthenticate hello Azure AD hesabının başarısız olur. Hata iletisi "oluşturulamıyor toovalidate kimlik bilgileri. Beklenmeyen bir hata oluştu." döndürülür.
* Sunucu hazırlama kaldırma, Azure AD kiracısında parola eşitleme devre dışı bırakır ve parola eşitleme toofail etkin sunucusuyla neden olur.
* Parola Eşitleme hello kullanıcı depolanan hiçbir parola karması olduğunda seyrek durumlarda başarısız olur.
* Azure AD Connect sunucusu için hazırlama modu etkinleştirildiğinde, parola geri yazma geçici olarak devre dışı değil.
* Sunucu hazırlama modunda olduğunda azure AD Connect Sihirbazı hello gerçek parola eşitleme ve parola geri yazma yapılandırma göstermez. Bu her zaman bunları devre dışı olarak gösterilir.
* Sunucu hazırlama modunda olduğunda yapılandırma değişiklikleri toopassword eşitleme ve parola geri yazma özelliğini Azure AD Connect Sihirbazı tarafından kalıcı değildir.

**İyileştirmeleri:**

* Bu mümkün toosuccessfully başlangıç yeni bir eşitleme döngüsü olsun veya olmasın hello başlangıç ADSyncSyncCycle cmdlet tooindicate güncelleştirildi.
* Devam eden eklenen hello Stop-ADSyncSyncCycle cmdlet'i tooterminate eşitleme döngüsü ve işlem.
* Devam eden güncelleştirilmiş hello Stop-ADSyncScheduler cmdlet'i tooterminate eşitleme döngüsü ve işlem.
* Yapılandırırken [dizin uzantıları](active-directory-aadconnectsync-feature-directory-extensions.md) Azure AD Connect Sihirbazı'nda hello Azure AD öznitelik türü "Teletex dizesi" şimdi seçilebilir.

## <a name="111890"></a>1.1.189.0
Yayımlanma tarihi: Haziran 2016

**Giderilen sorunlar ve iyileştirmeleri:**

* Azure AD Connect artık FIPS ile uyumlu bir sunucuya yüklenebilir.
  * Parola eşitlemesi için bkz: [parola eşitleme ve FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Bir sorun olduğu bir NetBIOS adı hello Active Directory Bağlayıcısı FQDN çözümlenmiş toohello bulunamadı sabit.

## <a name="111800"></a>1.1.180.0
Yayımlanma tarihi: Mayıs 2016

**Yeni Özellikler:**

* Sizi uyarır ve, Azure AD Connect çalıştırmadan önce bunu siz etki alanları doğrulamanıza yardımcı olur.
* Desteği eklendi [Microsoft Cloud Almanya](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Son hello desteği eklendi [Microsoft Azure kamu bulut](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) yeni URL gereksinimlerini altyapısıyla.

**Giderilen sorunlar ve iyileştirmeleri:**

* Eklenen filtreleme toohello eşitleme kuralı Düzenleyicisi toomake, kolay toofind eşitleme kuralları.
* Bağlayıcı alanı silerken performansı.
* Aynı nesne hem silinmiş ve eklenen hello hello olduğunda aynı (çağrılan silme/add) çalıştıran bir sorun düzeltilmiştir.
* Devre dışı bırakılmış bir eşitleme kuralı artık nesneler dahil yeniden etkinleştirir ve yükseltme veya dizin şeması özniteliklerinde yenileyin.

## <a name="111300"></a>1.1.130.0
Yayımlanma tarihi: Nisan 2016

**Yeni Özellikler:**

* Birden çok değerli öznitelikler için destek çok eklenen[dizin uzantıları](active-directory-aadconnectsync-feature-directory-extensions.md).
* Daha fazla yapılandırma farklılıkları için desteği eklendi [otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md) toobe kabul yükseltme için uygun değildir.
* Bazı cmdlet'ler için eklenen [özel Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Yayımlanma tarihi: Mart 2016

**Giderilen sorunlar:**

* Yapılan emin parola eşitleme için Windows Server 2008 (R2 öncesi) hızlı yükleme kullanılamaz bu işletim sisteminde desteklenmiyor.
* Özel filtre yapılandırmasıyla dirsync'ten yükseltme, beklendiği gibi çalışmadı.
* Tooa daha yeni sürüm yükseltme sırasında herhangi bir değişiklik toohello yapılandırma, tam alma/eşitleme zamanlanmadı.

## <a name="111100"></a>1.1.110.0
Yayımlanma tarihi: Şubat 2016

**Giderilen sorunlar:**

* Merhaba yükleme hello varsayılan C:\Program Files klasöründe değilse, önceki sürümlerinden yükseltme çalışmaz.
* Yüklediğinizde ve temizleyin **Başlat hello eşitleme işlemi** hello Yükleme Sihirbazı'nı hello sonunda, çalışan hello Yükleme Sihirbazı'nı ikinci kez hello Zamanlayıcı izin vermez.
* Merhaba Zamanlayıcı hello ABD-İngilizcesi tarih/saat biçimi değil kullanıldığı sunucularda beklendiği gibi çalışmıyor. Ayrıca engeller `Get-ADSyncScheduler` zamanlarını doğru tooreturn.
* Oturum açma seçeneği ve yükseltme hello gibi AD FS ile Azure AD Connect'in önceki bir sürümünü yüklediyseniz, hello Yükleme Sihirbazı'nı yeniden çalıştırılamıyor.

## <a name="111050"></a>1.1.105.0
Yayımlanma tarihi: Şubat 2016

**Yeni Özellikler:**

* [Otomatik yükseltmeyi](active-directory-aadconnect-feature-automatic-upgrade.md) özellik hızlı ayarları müşteriler için.
* Merhaba Yükleme Sihirbazı'nda Azure çok faktörlü kimlik doğrulaması ve Privileged Identity Management kullanarak genel yönetici hello desteği.
  * Tooallow gereken çok faktörlü kimlik doğrulaması kullanıyorsanız, proxy tooalso izin trafiği toohttps://secure.aadcdn.microsoftonline-p.com.
  * Çok faktörlü kimlik doğrulaması tooproperly iş için tooadd https://secure.aadcdn.microsoftonline-p.com tooyour Güvenilen siteler listesine gerekir.
* İlk yüklemeden sonra Hello kullanıcının oturum açma yöntemini değiştirme izin verin.
* İzin [etki alanı ve OU filtreleme](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Yükleme Sihirbazı'nda. Bu, aynı zamanda tüm etki alanları kullanılabildiği tooforests bağlanma sağlar.
* [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md) toohello eşitleme altyapısı içinde yerleşik olarak bulunur.

**Önizleme tooGA yükseltilen özellikleri:**

* [Cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md).
* [Dizin genişletmeleri](active-directory-aadconnectsync-feature-directory-extensions.md).

**Yeni Önizleme özellikleri:**

* aralığıdır 30 dakika hello yeni varsayılan eşitleme döngüsü. Toobe üç saat tüm önceki sürümleri için kullanılır. Destek toochange hello ekler [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md) davranışı.

**Giderilen sorunlar:**

* Merhaba doğrulayın DNS etki alanları sayfasına hello etki alanı her zaman tanımak alamadık.
* AD FS yapılandırma sırasında etki alanı yönetici kimlik bilgilerini ister.
* Merhaba AD hesapları farklı bir DNS ağaç daha hello kök etki alanı ile bir etki alanında değilse hello Yükleme Sihirbazı tarafından tanınmıyor. şirket içi.

## <a name="1091310"></a>1.0.9131.0
Yayımlanma tarihi: Aralık 2015

**Giderilen sorunlar:**

* Bir parola ayarladığınızda, Active Directory etki alanı Hizmetleri (AD DS), ancak works parolalarda değiştirdiğinizde, parola eşitleme çalışmayabilir.
* Bir proxy sunucusu kimlik doğrulaması tooAzure AD yüklemesi sırasında başarısız olabilir veya yükseltme olsa hello yapılandırma sayfasında iptal edilir.
* Bir SQL Server Sistem Yöneticisi (SA) değilse, bir tam SQL Server örneği ile Azure AD Connect'in önceki bir sürümünden güncelleştirme başarısız olur.
* Uzak bir SQL Server ile Azure AD Connect'in önceki bir sürümünden güncelleştirme hello "oluşturulamıyor tooaccess ADSync SQL veritabanı hello" hata gösterir.

## <a name="1091250"></a>1.0.9125.0
Yayımlanma tarihi: Kasım 2015

**Yeni Özellikler:**

* AD FS tooAzure AD güven yeniden yapılandırabilirsiniz.
* Merhaba Active Directory şemasını yenileyin ve eşitleme kuralları yeniden kullanabilirsiniz.
* Bir eşitleme kuralının devre dışı bırakabilirsiniz.
* "AuthoritativeNull" bir eşitleme kuralında yeni bir hazır değer olarak tanımlayabilirsiniz.

**Yeni Önizleme özellikleri:**

* [Azure AD Connect Health eşitleme](../connect-health/active-directory-aadconnect-health-sync.md).
* Desteği [Azure AD etki alanı Hizmetleri](../active-directory-passwords-update-your-own-password.md) parola eşitleme.

**Yeni desteklenen senaryo:**

* Birden çok şirket içi Exchange kuruluşu destekler. Daha fazla bilgi için bkz: [birden çok Active Directory ormanına karma dağıtımlarında](https://technet.microsoft.com/library/jj873754.aspx).

**Giderilen sorunlar:**

* Parola eşitleme sorunlarını:
  * Bir nesne kapsam tooin-kapsamdan taşındı eşitlenen parolasını sahip olmaz. Bu, OU ve öznitelik filtreleme içerir.
  * Yeni bir OU tooinclude eşitlenmiş seçerek tam parola eşitlemesini gerektirmez.
  * Devre dışı bir kullanıcı etkinleştirildiğinde hello parola eşitlemez.
  * Hello parola yeniden deneme kuyruğu sonsuzdur ve hello önceki Çekildi 5.000 nesneleri toobe sınırının kaldırılmıştır.
* Windows Server 2016 orman işlev düzeyi erişilemiyor tooconnect tooActive dizini.
* Merhaba ilk yüklemeden sonra Grup filtreleme için kullanılan erişilemiyor toochange hello grubu.
* Artık parola geri yazma etkinleştirilmiş bir parola değişikliği yapan her kullanıcı için hello Azure AD Connect sunucusu üzerinde yeni bir kullanıcı profili oluşturur.
* Eşitleme kuralları kapsamları erişilemiyor toouse uzun tamsayı değerleri.
* erişilemeyen etki alanı denetleyicileri varsa hello onay kutusu "cihaz geri yazma" devre dışı kalır.

## <a name="1086670"></a>1.0.8667.0
Yayımlanma tarihi: Ağustos 2015

**Yeni Özellikler:**

* Hello Azure AD Connect Yükleme Sihirbazı'nı sunulmuştur tooall Windows Server dillerine yerelleştirilmiş.
* Hesap için destek eklendi Azure AD parola yönetimi kullanırken kilidini açın.

**Giderilen sorunlar:**

* Başka bir kullanıcı ilk hello yükleme başlatıldı hello kişi yerine yükleme devam ederse, azure AD Connect Yükleme Sihirbazı'nı çöküyor.
* Azure AD Connect'in önceki kaldırılması toouninstall Azure AD Connect eşitleme düzgün bir şekilde başarısız olursa, olası tooreinstall değil.
* Azure AD Connect hello kullanıcı hello ormanın hello kök etki alanında değilse veya Active Directory İngilizce olmayan bir sürümü kullanılırsa, hızlı yükleme kullanarak yükleyemezsiniz.
* Merhaba hello Active Directory kullanıcı hesabı'nın FQDN'si çözümlenemezse, yanıltıcı bir hata iletisi "Başarısız toocommit hello şema" gösterilir.
* Active Directory Bağlayıcısı Hello üzerinde kullanılan hello hesabı dışında hello Sihirbazı değiştirdiyseniz, Başlangıç Sihirbazı'nı sonraki çalışır başarısız olur.
* Azure AD Connect, bazen bir etki alanı denetleyicisinde tooinstall başarısız olur.
* Oluşturulamıyor etkinleştirmek ve uzantı öznitelikleri eklediyseniz "Hazırlama modu" devre dışı bırakın.
* Parola geri yazma bazı yapılandırmalarda hello Active Directory Bağlayıcısı hatalı bir parola nedeniyle başarısız olur.
* Ayırt edici ad (DN) öznitelik filtrelemesi kullanılıyorsa DirSync yükseltilemiyor.
* Parola sıfırlama kullanırken, aşırı CPU kullanımı.

**Kaldırılan Önizleme özellikleri:**

* Merhaba önizleme özelliği [kullanıcı geri yazma](active-directory-aadconnect-feature-preview.md#user-writeback) geçici olarak Önizleme müşterilerimizden geri bildirim dayanan kaldırıldı. Biz geri bildirim sağlanan hello ele sonra daha sonra yeniden eklenir.

## <a name="1086410"></a>1.0.8641.0
Yayımlanma tarihi: Haziran 2015

**Azure AD Connect ilk sürümünü.**

Değiştirilen adından Azure AD eşitleme tooAzure AD Connect.

**Yeni Özellikler:**

* [Hızlı Ayarlar](active-directory-aadconnect-get-started-express.md) yükleme
* Yapabilirsiniz [AD FS yapılandırma](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* Yapabilirsiniz [dirsync'ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Sunulan [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode)

**Yeni Önizleme özellikleri:**

* [Kullanıcı geri yazma](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Grup geri yazma](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md)
* [Dizin genişletmeleri](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Yayımlanma tarihi: Mayıs 2015

**Yeni gereksinimi:**

* Azure AD eşitleme artık yüklü hello .NET Framework sürümünün 4.5.1 toobe gerektirir.

**Giderilen sorunlar:**

* Parola geri yazma özelliğini Azure AD'den Azure Service Bus bağlantı hatasıyla başarısız oluyor.

## <a name="104910413"></a>1.0.491.0413
Yayımlanma tarihi: Nisan 2015

**Giderilen sorunlar ve iyileştirmeleri:**

* Merhaba Active Directory Bağlayıcısı siler doğru hello geri dönüşüm kutusu etkinse ve hello ormanda birden çok etki alanı olan işlemez.
* Merhaba performans alma işlemlerinin Azure Active Directory Bağlayıcısı hello için geliştirilmiştir.
* Ne zaman bir grup aştı hello üyelik sınırı (varsayılan olarak, too50, 000 nesneleri hello sınırı ayarlanır), Azure Active Directory'de hello grubu silindi. Merhaba yeni davranış, hello Grup silinmez, bir hata oluşturulur ve yeni üyelik değişiklikleri aktarılmaz.
* Aynı DN zaten hello ile hazırlanmış bir silme hello bağlayıcı alanı mevcut değilse yeni bir nesne sağlanamıyor.
* Merhaba nesne üzerinde hazırlanmış herhangi bir değişiklik olsa bile bazı nesneler delta eşitlemesi sırasında eşitleme için işaretlenir.
* Parola Eşitleme zorlama, tercih edilen hello DC listesi kaldırır.
* CSExportAnalyzer bazı nesneler durumları sorunları vardır.

**Yeni Özellikler:**

* Bir birleştirme artık çok "tüm" Merhaba MV nesne türünün bağlanabilir.

## <a name="104850222"></a>1.0.485.0222
Yayımlanma tarihi: Şubat 2015

**İyileştirmeleri:**

* Geliştirilmiş alma performans.

**Giderilen sorunlar:**

* Parola Eşitleme, öznitelik filtrelemesi tarafından kullanılan hello cloudFiltered özniteliği geliştirir. Filtrelenmiş nesneler artık parola eşitleme kapsamında değildir.
* Burada hello topoloji birçok etki alanı denetleyicileri olan nadir durumlarda, parola eşitleme çalışmıyor.
* Azure AD/Intune'da "Durduruldu-server" Azure AD Bağlayıcısı hello sonra Aygıt Yönetimi alırken etkinleştirildi.
* Yabancı güvenlik sorumlusu (FSP) aynı ormandaki birden çok etki alanından birleştirme birleştirme belirsiz hataya neden olur.

## <a name="104751202"></a>1.0.475.1202
Yayımlanma tarihi: Aralık 2014

**Yeni Özellikler:**

* Parola Eşitleme'öznitelik tabanlı filtreleme ile artık desteklenmektedir. Daha fazla bilgi için bkz: [filtreleme ile parola eşitlemesini](active-directory-aadconnectsync-configure-filtering.md).
* Merhaba msDS-ExternalDirectoryObjectID özniteliği tooActive dizin geri yazılır. Bu özellik, Office 365 uygulamaları için destek ekler. OAuth2 tooaccess çevrimiçi ve şirket içi posta kutularını Exchange karma dağıtımı kullanır.

**Sabit yükseltme sorunlar:**

* Merhaba sunucuda hello oturum açma Yardımcısı'nın daha yeni bir sürümü kullanılabilir.
* Özel bir yükleme yolu kullanılan tooinstall Azure AD eşitleme oluştu.
* Geçersiz özel birleştirme ölçüt blokları hello sürümüne yükseltme.

**Diğer düzeltmeleri:**

* Office Pro Plus için sabit hello şablonları.
* Bir tire ile başlayan kullanıcı adlarını nedeniyle oluşan sabit yükleme sorunları.
* Kaybeden hello sourceAnchor ayarı hello Yükleme Sihirbazı'nı ikinci kez çalıştırırken düzeltildi.
* Parola Eşitleme için sabit ETW İzleme.

## <a name="104701023"></a>1.0.470.1023
Yayımlanma tarihi: Ekim 2014

**Yeni Özellikler:**

* Parola Eşitleme birden çok Active Directory tooAzure AD şirket içi.
* Yükleme kullanıcı Arabirimi tooall Windows Server dillerine yerelleştirilmiş.

**Modu'nu 1.0 GA ' yükseltme**

Azure AD eşitleme zaten varsa, hello out-of-box eşitleme kurallardan herhangi birinin değişmiş durumda tootake sahip ek bir adım yoktur. Toohello 1.0.470.1023 yayın yükselttikten sonra değiştirilmiş hello eşitleme kuralları yineleniyor. Her değiştirilmiş eşitleme kuralı için aşağıdaki hello:

1.  Değiştirilmiş ve hello değişiklikleri bir not alın hello eşitleme kuralını bulun.
* Merhaba eşitleme kuralını silin.
* Azure AD Sync tarafından oluşturulan hello yeni eşitleme kuralı bulun ve hello değişiklikleri yeniden uygulayın.

**Merhaba Active Directory hesabı için izinler**

Hello Active Directory hesabına ek izinler toobe mümkün tooread hello parola karmalarını Active Directory'den verilmesi gerekir. Merhaba izinleri toogrant "Dizin Değişikliklerini Çoğaltma" adlı ve "Tüm çoğaltma dizini değiştirir." Her iki gerekli toobe mümkün tooread hello parola karmaları izinlerdir.

## <a name="104190911"></a>1.0.419.0911
Yayımlanma tarihi: Eylül 2014

**Azure AD eşitleme ilk sürümünü.**

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
