---
title: "aaaConnector sürüm yayımlama geçmişi | Microsoft Docs"
description: "Bu konu hello bağlayıcılar tüm sürümleri, Forefront Identity Manager (FIM) ve Microsoft Identity Manager (MIM) için listeler."
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Bağlayıcı Sürümü Yayınlama Geçmişi
Merhaba bağlayıcıları Forefront Identity Manager (FIM) ve Microsoft Identity Manager (MIM) için sıkça güncelleştirilir.

> [!NOTE]
> Bu konuda FIM ve MIM yalnızca bilinmiyor. Bu bağlayıcıların üzerinde Azure AD Connect yüklemesi için desteklenmiyor. Yayımlanan bağlayıcılar AADConnect üzerinde toospecified yapı yükseltirken önceden yüklenmiş.

Bu konuda hello çıkarılan bağlayıcılar tüm sürümlerini listeler.

İlgili bağlantılar:

* [En son bağlayıcılar indirin](http://go.microsoft.com/fwlink/?LinkId=717495)
* [Genel LDAP Bağlayıcısı](active-directory-aadconnectsync-connector-genericldap.md) başvuru belgelerini
* [Genel SQL bağlayıcı](active-directory-aadconnectsync-connector-genericsql.md) başvuru belgelerini
* [Web Hizmetleri Bağlayıcısı](http://go.microsoft.com/fwlink/?LinkID=226245) başvuru belgelerini
* [PowerShell Bağlayıcısı](active-directory-aadconnectsync-connector-powershell.md) başvuru belgelerini
* [Lotus Domino Bağlayıcısı](active-directory-aadconnectsync-connector-domino.md) başvuru belgelerini


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (sürüm bekleyen AADConnect)


### <a name="fixed-issues"></a>Giderilen sorunlar:

* Genel Web Hizmetleri:
  * İki veya daha fazla uç noktaları zamanki oluşturulan bir SOAP proje engelleyen bir sorun düzeltilmiştir.
* Genel SQL:
  * Merhaba alma işleminde hello GSQL saati doğru kaydedildiğinde dönüştürülürken değil tooconnector alanı. Merhaba hello GSQL bağlayıcı alanı için varsayılan tarih ve saat Biçim 'yyyy-aa-gg: ssZ' too'yyyy-aa-gg: ssZ değiştirildi '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Giderilen sorunlar:

* Genel Web Hizmetleri:
  * Merhaba Wsconfig aracı doğru hello Json dizisi isteğinden"örnek" Merhaba REST hizmeti yöntemi için dönüştürmemenizi. Bu, bu Json dizisi hello REST isteği için seri hale getirme sorunlara neden oldu.
  * Web Hizmeti Bağlayıcısı Yapılandırması aracını JSON öznitelik adları alanı simgeleri kullanımını desteklemiyor 
    * Değiştirme deseni el ile toohello WSConfigTool.exe.config dosyasına, örneğin eklenebilir```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * Seçenek'ne zaman hello **kuruluşun/kuruluş birimleri için özel certifiers izin** hello bağlayıcı başarısız (Merhaba verme akış sonra tüm öznitelikleri güncelleştirme) dışarı aktarılırken dışarı aktarılan tooDomino sonra ancak hello sırasındaki devre dışı bırakıldı dışarı aktarma bir KeyNotFoundException tooSync döndürülür. 
    * Merhaba yeniden adlandırmak olduğundan işlem başarısız toochange DN (kullanıcı adı özniteliği) çalıştığında, aşağıdaki hello özniteliklerinden biri değiştirerek olur:  
      - Soyadı
      - FirstName
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - OU
      - altcommonname

  * Zaman **kuruluşun/kuruluş birimleri için özel certifiers izin** seçeneği etkin ancak gerekli certifiers hala boş sonra KeyNotFoundException oluşur.

### <a name="enhancements"></a>Geliştirmeleri:

* Genel SQL:
  * **Senaryo: Gerçekleştirilmedi yeniden tasarlanmıştır:** "*" özelliği
  * **Çözüm açıklaması:** değiştirilmiş bir yaklaşım [birden çok değerli başvuru öznitelikleri işleme](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Giderilen sorunlar:

* Genel Web Hizmetleri:
  * Web Hizmeti Bağlayıcısı varsa, sunucu yapılandırmasını içeri aktarılamıyor
  * Web Hizmeti Bağlayıcısı ile birden çok Web Hizmetleri çalışmıyor

* Genel SQL:
  * Tek değer başvurulan özniteliği için hiçbir nesne türleri listelenir
  * Delta içeri aktarma nesnesindeki değeri birden çok değerli tablosundan kaldırıldığında değişiklik izleme stratejisi siler
  * OverflowException GSQL Bağlayıcısı ile DB2 AS / 400

Lotus:
  * Eklenen seçeneği tooenable\disable GlobalParameters sayfa açmadan önce OU'lar arama

## <a name="114430"></a>1.1.443.0

Yayımlanma tarihi: 2017 Mart

### <a name="enhancements"></a>Geliştirmeleri

* Genel SQL:</br>
  **Senaryo Belirtiler:** hello SQL burada biz yalnızca başvuru tooone nesne türüne izin ve çapraz başvuru üyeleriyle gerektiren Connector ile iyi bilinen bir sınırlama geçerlidir. </br>
  **Çözüm açıklaması:** başvurular için hello işleme adımda olan "*" seçeneği seçildiğinde, nesne türlerinin tüm bileşimleri geri toohello eşitleme altyapısı döndürülür.

>[!Important]
- Bu çok sayıda yer tutucuları oluşturur
- Gerekli toomake hello adlandırma nesne türleri benzersiz olduğundan emin olur.


* Genel LDAP:</br>
 **Senaryo:** yalnızca birkaç kapsayıcıları belirli bir bölüm seçildiğinde sonra hello arama hala tüm bölümünde yapılır. Özel eşitleme hizmeti, ancak bir değil, performans düşüşüne neden MA filtrelenir. </br>

 **Çözüm açıklaması:** değiştirilen GLDAP bağlayıcı'nın kodunu toomake mümkün tüm kapsayıcıları gidin ve her biri hello tüm bölümünde arama yerine nesneleri arayın.


* Lotus Domino:

  **Senaryo:** Domino posta silme bir dışa aktarma sırasında kişi kaldırma desteği. </br>
  **Çözüm:** bir dışa aktarma sırasında kişi kaldırılmak üzere yapılandırılabilir posta silme desteği.

### <a name="fixed-issues"></a>Giderilen sorunlar:
* Genel Web Hizmetleri:
 * Aşağıdaki hata hello olur sonra hello hizmeti URL'si varsayılan değiştirirken SAP wsconfig WebService yapılandırma aracı aracılığıyla projeleri: hello yolunun bir bölümü bulunamadı.

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* Genel LDAP:
 * AD LDS tüm öznitelikleri GLDAP bağlayıcı görmez
 * UPN özniteliklere hello LDAP dizin şemadan algılandığında Sihirbazı sonları
 * Delta içeri aktarmalar başarısız bulma hatalı "objectclass" özniteliği seçilmediğinde tam içeri aktarma sırasında mevcut değil
 * Bir "Bölümleri ve hiyerarşileri Yapılandır" yapılandırma sayfası eşit toohello bölümdür hello genel yeni sunucular için hangi tür nesneleri göster değil  
LDAP MA. Bunlar yalnızca nesneleri RootDSE bölümünden gösterdi.


* Genel SQL:
 * Delta içeri aktarma öznitelikte içeri hata Genel SQL filigran için düzeltme
 * Birden çok değerli öznitelik deleted\added değerlerini verilirken deleted\added veri kaynağındaki değiller.  


* Lotus Notes:
 * Belirli bir alan "Tam adı" Merhaba meta veri deposunda doğru değeri verme tooNotes hello ancak hello özniteliği Null veya boş olduğunda gösterilir.
 * Yinelenen Certifier hata düzeltme
 * Merhaba nesne herhangi bir veri olmadan hello Lotus Domino Bağlayıcısı diğer nesnelerle seçildiğinde sonra hello bulma hatası tam içeri aktarma işlemi gerçekleştirilirken aldığımız.
 * Delta içeri aktarma olduğunda Lotus Domino Bağlayıcısı hello üzerinde hello çalıştırma, o hello sonunda Microsoft.IdentityManagement.MA.LotusDomino.Service.exe hizmeti bazen çalıştıran bir uygulama hatası döndürür.
 * Genel grup üyelikleri düzgün çalışır ve hello verme tootry tooremove kullanıcı çalıştırırken üyeliğinden içeren bir güncelleştirme başarılı olarak gösterir, ancak hello kullanıcı gerçekte Lotus Notes üyeliğinin kaldırılmaları değil dışında tutulur.
 * Bir fırsat toochoose modu "Append öğesi en altındaki" olarak dışa aktarma yapılandırma Lotus GUI MA tooappend yeni öğeler en altında birden çok değerli öznitelikler için hello dışa aktarma sırasında eklendi.
 * Bağlayıcı hello mantığı toodelete hello hello posta klasörünün dosyasından ve kimliği kasa gerekli ekler.
 * Üyelik için NAB üye çalışmıyor silin.
 * Değerleri başarıyla birden çok değerli özniteliğinden silinmelidir

## <a name="111170"></a>1.1.117.0
Yayımlanma tarihi: 2016 Mart

**Yeni bir bağlayıcı**  
İlk hello sürümü [Genel SQL bağlayıcı](active-directory-aadconnectsync-connector-genericsql.md).

**Yeni Özellikler:**

* Genel LDAP Bağlayıcısı:
  * Delta içeri aktarma Isode ile desteği eklendi.
* Web Hizmetleri Bağlayıcısı:
  * Güncelleştirilmiş hello csEntryChangeResult etkinliği ve setImportErrorCode etkinlik tooallow nesne düzeyi hataları toobe döndürülen geri toohello eşitleme altyapısı.
  * Güncelleştirilmiş hello SAP6 ve SAP6User şablonları toouse hello yeni nesne düzeyinde hata işlevselliği.
* Lotus Domino Bağlayıcısı:
  * Dışarı aktarma için adres defteri başına bir certifier gerekir. Kullanım hello artık aynı yapabilecekleriniz parola tüm certifiers toomake hello yönetimi için daha kolay.

**Giderilen sorunlar:**

* Genel LDAP Bağlayıcısı:
  * IBM Tivoli DS için bazı başvuru öznitelikleri doğru algılanmadı.
  * Delta içeri aktarma sırasında açık LDAP için hello başına ve dizeleri sonunda boşluk kesildi.
  * Novell ve NetIQ için bir nesne hello adresindeki OU'lar/kapsayıcıları arasında taşındı verme aynı yeniden adlandırılmış hello nesnesi oluşturulamadı zaman.
* Web Hizmetleri Bağlayıcısı:
  * Merhaba web hizmeti aynı bağlama için birden çok uç noktalarının olsaydı, ardından hello bağlayıcı doğru Bu uç noktalarının bulamadı.
* Lotus Domino Bağlayıcısı:
  * Bir verme posta hello fullName özniteliği tooa veritabanının çalışmadı.
  * Bir gruptan kaldırılan ve eklendi üye yalnızca hello dışarı verme üyeleri eklendi.
  * Notlar belge geçersizse (Merhaba özniteliği IsValid toofalse ayarlanır), bağlayıcı başarısız hello.

## <a name="older-releases"></a>Eski sürümleri
Mart 2016 öncesinde hello bağlayıcılar destek konuları yayımlanmıştır.

**Genel LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, Eylül 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, Mart 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, Ocak 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, 2014 Eylül
* [KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, Mart 2014

**Webservices'a**

* [KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, 2014 Eylül

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, 2014 Eylül

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, Eylül 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, Mart 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, 2014 Ağustos
* [KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, Şubat 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, Ekim 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, 2013 Ağustos

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
