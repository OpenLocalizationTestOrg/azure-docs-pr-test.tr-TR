---
title: "aaaGeneric LDAP Bağlayıcısı | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure Microsoft'un genel LDAP Bağlayıcısı."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Genel LDAP Bağlayıcısı Teknik Başvurusu
Bu makalede hello genel LDAP Bağlayıcısı açıklanmaktadır. Merhaba makale ürünleri aşağıdaki toohello geçerlidir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Düzeltme 4.1.3671.0 kullanmanız gerekir ya da daha sonra [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 ve FIM2010R2 için hello bağlayıcı olarak hello Merkezi'nden kullanılabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

TooIETF RFC'leri söz konusu olduğunda, bu belgede hello biçimini kullanarak (RFC [RFC numarası] / [bölüm RFC belgede]), örneğin (RFC 4512/4.3).
Http://tools.ietf.org/html/rfc4500 (Merhaba doğru RFC numarasıyla tooreplace 4500 gerekir), daha fazla bilgi bulabilirsiniz.

## <a name="overview-of-hello-generic-ldap-connector"></a>Merhaba genel LDAP Bağlayıcısı genel bakış
Merhaba genel LDAP Bağlayıcısı, toointegrate hello eşitleme hizmeti ile bir LDAP v3 sunucusu sağlar.

Bu tooperform delta içeri aktarma, gerektiği gibi belirli işlemler ve şema öğeleri, hello IETF RFC belirtilmedi. Bu işlemler için açıkça belirtilen yalnızca LDAP dizinleri desteklenir.

Üst düzey açısından bakıldığında, özellikler aşağıdaki hello hello sürümü geçerli hello bağlayıcı tarafından desteklenir:

| Özellik | Destek |
| --- | --- |
| Bağlı veri kaynağı |Merhaba bağlayıcı tüm LDAP v3 sunucuları (RFC 4510 uyumlu) desteklenir. Merhaba aşağıdakilerle sınanmıştır: <li>Microsoft Active Directory Basit Dizin Hizmetleri (AD LDS)</li><li>Microsoft Active Directory genel katalog (GC AD)</li><li>389 dizin sunucusu</li><li>Apache dizin sunucusu</li><li>IBM Tivoli DS</li><li>Isode dizini</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Açık DJ</li><li>Açık DS</li><li>Açık LDAP (openldap.org)</li><li>Oracle (önceden Sun) dizin Server Enterprise Edition</li><li>RadiantOne sanal dizin sunucusu (VDS)</li><li>Sun bir dizin sunucusu</li>**Önemli dizinler desteklenmiyor:** <li>Microsoft Active Directory etki alanı Hizmetleri (AD DS) [kullanım hello yerleşik Active Directory Bağlayıcısı yerine]</li><li>Oracle Internet dizini (OID)</li> |
| Senaryolar |<li>Nesne yaşam döngüsü yönetimi</li><li>Grup Yönetimi</li><li>Parola Yönetimi</li> |
| İşlemler |aşağıdaki işlemleri hello tüm LDAP dizinleri desteklenir: <li>Tam içeri aktarma</li><li>Dışarı Aktarma</li>aşağıdaki işlemleri hello yalnızca belirtilen dizinleri desteklenir:<li>Delta içeri aktarma</li><li>Parola, parola değiştirme</li> |
| Şema |<li>Şema hello LDAP şemadan (RFC3673 ve RFC4512/4.2) algılandı</li><li>Yapısal sınıflar, aux sınıfları ve extensibleObject nesne sınıfı (RFC4512/4.3) destekler</li> |

### <a name="delta-import-and-password-management-support"></a>Delta içeri aktarma ve parola yönetimi desteği
Delta içeri aktarma ve parola yönetimi için desteklenen dizinler:

* Microsoft Active Directory Basit Dizin Hizmetleri (AD LDS)
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ayarlama destekler
* Microsoft Active Directory genel katalog (GC AD)
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ayarlama destekler
* 389 dizin sunucusu
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Apache dizin sunucusu
  * Bu dizin kalıcı değişiklik günlüğü olmadığından delta içeri aktarma desteklemiyor
  * Parola ayarlama destekler
* IBM Tivoli DS
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Isode dizini
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Novell eDirectory ve NetIQ eDirectory
  * Delta içeri aktarma için ekleme, güncelleştirme ve yeniden adlandırma işlemlerini destekler
  * Delta içeri aktarma için silme işlemlerini desteklemiyor
  * Parola ve parola değiştirme destekler ayarlayın
* Açık DJ
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Açık DS
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Açık LDAP (openldap.org)
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ayarlama destekler
  * Parola değiştirme desteklemiyor
* Oracle (önceden Sun) dizin Server Enterprise Edition
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* RadiantOne sanal dizin sunucusu (VDS)
  * Sürüm 7.1.1 kullanıyor olmanız gerekir veya üzeri
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın
* Sun bir dizin sunucusu
  * Delta içeri aktarma için tüm işlemleri destekler
  * Parola ve parola değiştirme destekler ayarlayın

### <a name="prerequisites"></a>Ön koşullar
Merhaba bağlayıcı kullanmadan önce hello eşitleme sunucusunda hello şunlara sahip olmanız emin olun:

* 4.5.2 Microsoft .NET Framework veya daha yenisi

### <a name="detecting-hello-ldap-server"></a>Merhaba LDAP sunucusu algılama
Hello bağlayıcı üzerinde çeşitli teknikleri toodetect güvenir ve hello LDAP sunucusu belirleyin. Merhaba bağlayıcı kullandığı kök DSE, satıcı adı/sürümü, hello ve hello şema toofind benzersiz nesneleri ve belirli LDAP sunucuları tooexist bilinen öznitelikleri inceler. Bu veriler, varsa bulundu, kullanılan toopre olduğu-hello bağlayıcı hello yapılandırma seçenekleri doldurun.

### <a name="connected-data-source-permissions"></a>Bağlı veri kaynağı izinleri
tooperform alma ve verme işlemleri hello bağlı dizin hello nesnelerde, hello bağlayıcı hesabı yeterli izinlere sahip olmalıdır. Merhaba Bağlayıcısı izinleri toobe mümkün tooexport yazma ve Okuma izinleri toobe mümkün tooimport olması gerekir. İzni yapılandırması hello yönetim deneyimleriyle hello hedef dizinin kendisi içinde gerçekleştirilir.

### <a name="ports-and-protocols"></a>Bağlantı noktalarını ve protokolleri
Merhaba bağlayıcı hello yapılandırmasında, olan varsayılan LDAP için 389 ve 636 LDAPS için belirtilen başlangıç bağlantı noktası numarası kullanır.

LDAPS için SSL 3.0 veya TLS kullanmanız gerekir. SSL 2.0 desteklenmez ve devre dışı bırakılamaz.

### <a name="required-controls-and-features"></a>Gerekli denetimleri ve özellikleri
Merhaba aşağıdaki LDAP denetimleri/özellikleri düzgün şekilde hello bağlayıcı toowork için hello LDAP sunucusundaki kullanılabilir olması gerekir:  
`1.3.6.1.4.1.4203.1.5.3`True/False filtreleri

Merhaba True/False filtre sık LDAP dizinleri tarafından desteklenen olarak bildirilmedi ve üzerinde hello gösterebilir **genel sayfa** altında **zorunlu özellikleri bulunamadı**. Kullanılan toocreate olan **veya** birden çok nesne türlerini alırken örneğin LDAP sorguları filtreleri. Birden fazla nesne türü içe aktarırsanız, LDAP sunucunuzun bu özelliğini destekler.

Benzersiz bir tanımlayıcı bulunduğu bir dizin kullanın hello bağlantı hello aşağıdakileri de kullanılabilir olması gerekir (Merhaba daha fazla bilgi için bkz [yapılandırma bağlayıcılarını](#configure-anchors) bölümü):  
`1.3.6.1.4.1.4203.1.5.1`Tüm işlem öznitelikleri

Merhaba dizin ne bir çağrı toohello dizininde sığabilecek daha çok nesne varsa, toouse disk belleği önerilir. Disk belleği toowork için aşağıdaki seçenekleri şu hello biri gerekir:

**Seçenek 1:**  
`1.2.840.113556.1.4.319`pagedResultsControl

**Seçenek 2:**  
`2.16.840.1.113730.3.4.9`VLVControl  
`1.2.840.113556.1.4.473`SortControl

Her iki seçenek hello bağlayıcı yapılandırmasında etkinleştirilirse, pagedResultsControl kullanılır.

`1.2.840.113556.1.4.417`ShowDeletedControl

ShowDeletedControl yalnızca hello USNChanged delta içeri aktarma yöntemini toobe mümkün toosee silinmiş nesneler ile kullanılır.

Merhaba bağlayıcı toodetect hello seçeneklerini mevcut hello sunucusunda çalışır. Başlangıç seçenekleri algılanamaz ise bir uyarı hello bağlayıcı özelliklerinde hello genel sayfasında mevcuttur. Mevcut tüm LDAP sunucuları tüm denetimler/destekler ve bu uyarıyı varsa, bağlayıcı hello özellikleri sorunsuz çalışabilir.

### <a name="delta-import"></a>Delta içeri aktarma
Delta içeri aktarma yalnızca için destek directory algılandı. yöntemler aşağıdaki hello şu anda kullanılır:

* LDAP Accesslog. Bkz: [http://www.openldap.org/doc/admin24/overlays.html#Access günlüğe kaydetme](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP değişim günlüğü. Bkz: [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* Zaman damgası. Novell/NetIQ eDirectory hello bağlayıcı kullanan son tarih tooget oluşturulur ve nesnelerin güncelleştirilmiş. Novell/NetIQ eDirectory tooretrieve silinmiş nesneleri eşdeğer bir anlamına gelir sağlamaz. Diğer bir delta alma yöntemini hello LDAP sunucusunda etkinse, bu seçenek de kullanılabilir. Bu seçenek mümkün tooimport silinmiş nesneleri değil.
* USNChanged. Bkz: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Desteklenmiyor
LDAP özellikler aşağıdaki hello desteklenmez:

* Sunucuları (RFC 4511/4.1.10) arasında LDAP başvuruları

## <a name="create-a-new-connector"></a>Yeni bir bağlayıcı oluşturun
tooCreate genel LDAP Bağlayıcısı, **eşitleme hizmeti** seçin **yönetim Aracısı** ve **oluşturma**. Select hello **genel LDAP (Microsoft)** bağlayıcı.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Bağlantı
Merhaba bağlantı sayfasında hello konak, bağlantı noktası ve bağlama bilgilerini belirtmeniz gerekir. Bağlama olduğu bağlı olarak seçilen, ek bölümler aşağıdaki hello bilgileri sağlamış.

![Bağlantı](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* Merhaba bağlantı zaman aşımı ayarını, yalnızca hello şema tespit edilirken hello ilk bağlantı toohello sunucusu için kullanılır.
* Varsa bağlama anonim, ardından hiçbiri kullanıcı adı / parola veya sertifika kullanılır.
* Diğer bağlamaları için bilgi ya da kullanıcı adı girin / parola veya bir sertifika seçin.
* Kerberos tooauthenticate kullanıyorsanız, aynı zamanda hello hello kullanıcının bölge/etki alanı belirtin.

Merhaba **öznitelik diğer adları** metin kutusu RFC4522 sözdizimi ile Merhaba şemasında tanımlanan öznitelikleri için kullanılır. Bu öznitelikler şeması algılama sırasında algılanamıyor ve hello bağlayıcı tooidentify özniteliklerle Yardım. Örneğin aşağıdaki hello öznitelik diğer adları kutusunu toocorrectly girilmelidir hello tanımlayın hello userCertificate özniteliği bir ikili öznitelik olarak:

`userCertificate;binary`

Merhaba, bu yapılandırma gibi nasıl görünebilir için örneği aşağıdadır:

![Bağlantı](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Select hello **işletimsel öznitelikleri şemada yer** onay kutusunu tooalso hello sunucusu tarafından oluşturulan öznitelikleri içerir. Bunlar zaman hello nesne oluşturuldu ve en son güncelleştirme zamanı gibi öznitelikleri içerir.

Seçin **Genişletilebilir öznitelikleri şemada yer** genişletilebilen nesneler (RFC4512/4.3) kullanılır ve bu seçeneğin etkinleştirilmesi, tüm nesne üzerinde kullanılan her özniteliği toobe sağlar. Merhaba bağlı dizin kullanmadığınız sürece bu özellik hello öneri tookeep hello seçeneği seçili olması için bu seçeneğin belirlenmesi hello şeması çok büyük yapar.

### <a name="global-parameters"></a>Genel Parametreler
Merhaba genel parametreleri sayfasında hello DN toohello delta değişiklik günlüğü ve ek LDAP özelliklerini yapılandırın. Merhaba hello LDAP sunucusu tarafından sağlanan hello bilgilerle önceden doldurulmuş haldedir sayfasıdır.

![Bağlantı](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

Merhaba üst kısmında hello sunucusunun kendisi de hello sunucusunun hello adı gibi tarafından sağlanan bilgileri gösterir. Merhaba bağlayıcı ayrıca hello zorunlu denetimleri hello kök DSE mevcut olduğunu doğrular. Bu denetimler listelenmiyorsa, bir uyarı görüntülenir. Bazı LDAP dizinleri hello kök DSE'ındaki tüm özelliklere listelemez ve bir uyarı mevcut olsa bile, bir sorun olmadan bağlayıcı works hello mümkün olur.

Merhaba **denetimler desteklenen** onay kutularını kontrol hello davranışı belirli işlemler için:

* Seçili ağaç silme ile bir hiyerarşi silinmiş bir LDAP çağrısı ile. Seçili ağaç silme ile Merhaba bağlayıcı gerekirse bir özyinelemeli silme yapar.
* Seçili disk belleğine alınan sonuçlarla hello bağlayıcı çalıştırmak hello adımları belirtilen hello boyutuna sahip bir disk belleğine alınan alma yapar.
* Merhaba VLVControl SortControl ise bir alternatif toohello pagedResultsControl tooread verileri hello LDAP dizini.
* Her üç seçenek (pagedResultsControl, VLVControl ve SortControl) seçilmemiş ise ardından hello bağlayıcı büyük bir dizin ise, hangi başarısız olabilir tek bir işlemde tüm nesne alır.
* Merhaba Delta alma yöntemini USNChanged olduğunda ShowDeletedControl yalnızca kullanılır.

Merhaba değişiklik günlüğü DN olduğunda hello adlandırma bağlamı örneğin hello delta değişiklik günlüğü tarafından kullanılan **cn = değişim günlüğü**. Bu değer olmalıdır toobe mümkün toodo delta içeri aktarma belirtildi.

Merhaba, varsayılan değişiklik günlüğü DNs listesi aşağıdadır:

| Dizin | Delta değişiklik günlüğü |
| --- | --- |
| Microsoft AD LDS ve AD GC |Otomatik olarak algılanır. USNChanged. |
| Apache dizin sunucusu |Mevcut değil. |
| Dizin 389 |Değişiklik günlüğü. Varsayılan değer toouse: **cn = değişim günlüğü** |
| IBM Tivoli DS |Değişiklik günlüğü. Varsayılan değer toouse: **cn = değişim günlüğü** |
| Isode dizini |Değişiklik günlüğü. Varsayılan değer toouse: **cn = değişim günlüğü** |
| Novell/NetIQ eDirectory |Mevcut değil. Zaman damgası. Merhaba bağlayıcı kullanan son güncelleştirilmiş tarih tooget eklenir ve kayıtlar güncelleştirildi. |
| Açık DJ/DS |Değişiklik günlüğü.  Varsayılan değer toouse: **cn = değişim günlüğü** |
| Açık LDAP |Erişim günlüğü. Varsayılan değer toouse: **cn accesslog =** |
| Oracle DSEE |Değişiklik günlüğü. Varsayılan değer toouse: **cn = değişim günlüğü** |
| RadiantOne VDS |Sanal dizin. Merhaba bağlı dizin tooVDS üzerinde bağlıdır. |
| Sun bir dizin sunucusu |Değişiklik günlüğü. Varsayılan değer toouse: **cn = değişim günlüğü** |

Merhaba parola hello özniteliği hello bağlayıcı hello adını tooset hello Parolada parola değiştirme ve parola ayarlama işlemleri kullanması gereken özniteliğidir.
Çok ayarlanmış varsayılan olarak bu değer**userPassword** ancak belirli bir LDAP sistemi için gerektiğinde değiştirilebilir.

Hello ek bölümlere listesinde otomatik olarak algılanan olası tooadd ek ad alanlarını değil. Bu ayar, tüm hello aktarılması gereken mantıksal kümesi birkaç sunucuya yaparsanız, örneğin, kullanılabilir aynı anda. Yalnızca Active Directory birden çok etki alanı bir ormanda olabilir ancak bir şema, aynı bu kutuya hello ek ad alanlarını girerek benzetimi yapılabilir hello tüm etki alanları paylaşın. Her ad alanı farklı sunuculardan alabilir ve daha fazla hello yapılandırma bölümleri ve hiyerarşileri sayfasında yapılandırılır. Ctrl + Enter tooget yeni bir satır kullanın.

### <a name="configure-provisioning-hierarchy"></a>Sağlama hiyerarşisini Yapılandır
Bu sayfada sağlanan, kullanılan toomap hello DN bileşeni, örneğin OU toohello nesne örneğin organizationalUnit türüdür.

![Hiyerarşi sağlama](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Sağlama hiyerarşisini yapılandırarak yapılandırabilirsiniz hello bağlayıcı tooautomatically gerektiğinde bir yapı oluşturabilir. Ad alanı dc ise contoso, örneğin, = dc = com ve yeni bir nesne cn = Joe, ou = Seattle, = c = US, dc = contoso, dc = com sağlandığına sonra hello Bağlayıcısı, bir nesne türü ülke ABD için ve bir kuruluş birimi Seattle için oluşturabilir, bu zaten değilse Merhaba dizininde mevcut.

### <a name="configure-partitions-and-hierarchies"></a>Bölümleri ve hiyerarşileri Yapılandır
Merhaba bölümleri ve hiyerarşileri sayfasında, tüm ad alanlarını seçin nesneleriyle tooimport ve dışarı aktarma planlayın.

![Bölümler](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Her ad alanı için hello bağlantı ekranda belirtilen hello değerleri geçersiz kılarsınız olası tooconfigure bağlantı ayarları de olabilir. Bu değerleri tootheir varsayılan değer boş bırakılırsa, hello bağlantı ekranından hello bilgiler kullanılır.

Bu da olası tooselect hangi kapsayıcılar ve OU'lar hello Bağlayıcısı almak ve vermek olur.

Bir arama yaparken bu hello bölümündeki tüm kapsayıcıları üzerinden gerçekleştirilir. Durumlarda kapsayıcıları çok sayıda olduğu Bu davranış tooperformance düşmesine yol açar.

>[!NOTE]
Merhaba Mart 2017 güncelleştirme toohello genel LDAP başlangıç bağlayıcı arama kapsamı tooonly seçili Merhaba kapsayıcılara sınırlı olabilir. Bu görüntüde hello aşağıda gösterildiği gibi hello onay kutusunu 'Aramada yalnızca seçili kapsayıcıları' seçerek yapılabilir.

![Yalnızca seçili kapsayıcısında arama](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Yer işaretlerini Yapılandır
Bu sayfa, her zaman önceden yapılandırılmış bir değere sahip ve değiştirilemez. Merhaba sunucusunun satıcısı tanımladıysanız hello bağlantı bir nesne için örnek hello GUID için sabit bir özniteliği olan doldurulabilir. Toonot bilinen veya değil algıladı, sabit bir özniteliği bulunması, sonra hello bağlayıcı dn (ayırt edici adı) hello bağlantı kullanır.

![tutturucular](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


Merhaba, LDAP sunucuları ve kullanılan hello bağlantı listesi aşağıdadır:

| Dizin | Bağlantı özniteliği |
| --- | --- |
| Microsoft AD LDS ve AD GC |objectGUID |
| 389 dizin sunucusu |DN |
| Apache dizini |DN |
| IBM Tivoli DS |DN |
| Isode dizini |DN |
| Novell/NetIQ eDirectory |GUID |
| Açık DJ/DS |DN |
| Açık LDAP |DN |
| Oracle ODSEE |DN |
| RadiantOne VDS |DN |
| Sun bir dizin sunucusu |DN |

## <a name="other-notes"></a>Diğer Notlar
Bu bölüm yalnızca belirli toothis bağlayıcı olan veya başka nedenlerle önemli tooknow olan yönlerinden bilgi sağlar.

### <a name="delta-import"></a>Delta içeri aktarma
Açık LDAP Hello delta Filigran UTC tarih/saat ' dir. Bu nedenle, FIM eşitleme hizmeti ile Merhaba açık LDAP arasındaki hello saatler eşitlenmelidir. Aksi durumda, bazı girişler hello delta değişiklik günlüğü devre dışı bırakılacak.

Novell eDirectory için hello delta içeri aktarma hiçbir nesne silme algılama değil. Bu nedenle, gerekli toorun tam alma düzenli aralıklarla toofind tüm silinmiş nesneleri.

Tarih/saat üzerine temel günlük delta dizinlerle değiştirmek için yüksek oranda olduğundan tam içeri aktarma düzenli zamanlarda toorun önerilir. Bu işlem hello eşitleme altyapısı toofind ve dissimilarities hello LDAP sunucusu arasında şu anda hello bağlayıcı alanı nedir sağlar.

## <a name="troubleshooting"></a>Sorun giderme
* Merhaba nasıl tooenable günlük tootroubleshoot hello Bağlayıcısı hakkında daha fazla bilgi için bkz [nasıl tooEnable ETW İzleme bağlayıcıların](http://go.microsoft.com/fwlink/?LinkId=335731).
