---
title: "aaaPowerShell bağlayıcı | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure Microsoft'un Windows PowerShell Bağlayıcısı."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Windows PowerShell Bağlayıcısı Teknik Başvurusu
Bu makalede hello Windows PowerShell Bağlayıcısı açıklanmaktadır. Merhaba makale ürünleri aşağıdaki toohello geçerlidir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Düzeltme 4.1.3671.0 kullanmanız gerekir ya da daha sonra [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 ve FIM2010R2 için hello bağlayıcı olarak hello Merkezi'nden kullanılabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Merhaba PowerShell Bağlayıcısı genel bakış
Merhaba PowerShell Bağlayıcısı toointegrate hello eşitleme hizmeti API'ları Windows PowerShell tabanlı teklif dış sistemlerle sağlar. Merhaba Bağlayıcısı, 2 (ECMA2) framework ve Windows PowerShell hello arama tabanlı Genişletilebilir bağlantı yönetim Aracısı'nın hello özellikleri arasında bir köprü sağlar. Merhaba hello ECMA framework hakkında daha fazla bilgi için bkz: [Genişletilebilir bağlantı 2.2 Yönetim Aracı başvurusu](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Ön koşullar
Merhaba bağlayıcı kullanmadan önce hello eşitleme sunucusunda hello şunlara sahip olmanız emin olun:

* 4.5.2 Microsoft .NET Framework veya daha yenisi
* Windows PowerShell 2.0, 3.0 veya 4.0

Merhaba yürütme İlkesi hello eşitleme hizmeti sunucuda yapılandırılmış tooallow hello bağlayıcı toorun Windows PowerShell betikleri olması gerekir. Merhaba betikleri hello bağlayıcı çalıştırır dijital olarak imzalanmış sürece, şu komutu çalıştırarak hello yürütme ilkesi yapılandırın:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Yeni bir bağlayıcı oluşturun
toocreate hello eşitleme hizmeti bir Windows PowerShell Bağlayıcısı, bir dizi hello eşitleme hizmeti tarafından istenen hello adımlarını yerine getirmesi Windows PowerShell komut dosyalarını sağlamanız gerekir. İhtiyaç duyduğunuz tooand hello işlevselliği bağlanmak hello veri kaynağı bağlı olarak, uygulamanız gereken hello betikleri değişir. Bu bölümde her, uygulanabilir ve gerekli olduklarında hello betikleri özetlenmektedir.

Merhaba Windows PowerShell Bağlayıcısı toostore her hello komut dosyalarının hello eşitleme hizmeti veritabanı içinde tasarlanmıştır. Merhaba dosya sisteminde depolanan olası toorun komut dosyaları olmakla birlikte, her komut dosyası toohello bağlayıcı yapılandırmasında doğrudan daha kolay tooinsert hello gövdesi oluyor.

tooCreate PowerShell Bağlayıcısı, **eşitleme hizmeti** seçin **yönetim Aracısı** ve **oluşturma**. Select hello **PowerShell (Microsoft)** bağlayıcı.

![Bağlayıcı oluşturma](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Bağlantı
Tooa uzak sisteme bağlanmak için yapılandırma parametreleri sağlayın. Bu değerler güvenli bir şekilde hello eşitleme hizmeti tarafından depolanan ve hello bağlayıcı çalıştırdığınızda kullanılabilir tooyour Windows PowerShell betikleri yapılan.

![Bağlantı](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Bağlantı parametrelerini aşağıdaki hello yapılandırabilirsiniz:

**Bağlantı**

| Parametre | Varsayılan değer | Amaç |
| --- | --- | --- |
| Sunucu |<Blank> |Bağlayıcı hello sunucu adı için bağlanmanız gerekir. |
| Etki alanı |<Blank> |Merhaba kimlik bilgisi toostore hello bağlayıcı çalıştırdığınızda kullanmak için etki alanı. |
| Kullanıcı |<Blank> |Merhaba kimlik bilgisi toostore hello bağlayıcı çalıştırdığınızda kullanmak için kullanıcı adı. |
| Parola |<Blank> |Merhaba kimlik bilgisi toostore hello bağlayıcı çalıştırdığınızda kullanmak için parola. |
| Bağlayıcı hesabının kimliğine bürün |False |Doğru olduğunda, hello eşitleme hizmeti hello hello kimlik bilgileri sağlandı bağlamında hello Windows PowerShell komut dosyaları çalıştırılır. Mümkün olduğunda, o hello önerilir **$Credentials** parametre tooeach geçirilen komut dosyası, kimliğe bürünme yerine kullanılır. Bu seçenek toouse ek izinler hakkında daha fazla bilgi gerekli için bkz: [kimliğe bürünme için ek yapılandırma](#additional-configuration-for-impersonation). |
| Belirlerken kullanıcı profilini yükle |False |Windows tooload hello kullanıcı profili hello bağlayıcı'nın kimlik bilgilerinin kimliğe bürünme sırasında bildirir. Merhaba Kimliğine bürünülen kullanıcı gezici profili varsa, hello bağlayıcı hello dolaşım profili yüklemez. Bu parametre toouse ek izinler hakkında daha fazla bilgi gerekli için bkz: [kimliğe bürünme için ek yapılandırma](#additional-configuration-for-impersonation). |
| Belirlerken oturum açma türü |None |Kimliğe bürünme sırasında oturum açma türü. Daha fazla bilgi için bkz: Merhaba [dwLogonType] [ dw] belgeleri. |
| Yalnızca imzalı komut dosyaları |False |TRUE ise, hello Windows PowerShell Bağlayıcısı her komut dosyası geçerli bir dijital imzaya sahip olduğunu doğrular. False ise, hello eşitleme hizmeti sunucunun Windows PowerShell yürütme İlkesi RemoteSigned veya Kısıtlanmamış olduğundan emin olun. |

**Ortak Modülü**  
Merhaba Bağlayıcısı hello yapılandırmasında toostore paylaşılan bir Windows PowerShell modülü sağlar. Merhaba bağlayıcı bir komut dosyası çalıştığında, böylece her komut dosyası tarafından içe aktarılabilir hello Windows PowerShell modülü toohello dosya sistemi ayıklandı.

İçeri aktarma, dışarı aktarma ve parola eşitleme betikleri hello ortak modülü ayıklanan toohello bağlayıcı'nın MAData klasörüdür. Şema, doğrulama, hiyerarşi ve bölüm bulma betikler için hello ortak ayıklanan toohello % TEMP % klasöründe modülüdür. Her iki durumda da, genel komut dosyası toohello ortak modülü betik adı ayarı göre adlı modül hello ayıklandı.

tooload bir modül hello MAData klasöründen FIMPowerShellConnectorModule.psm1 adında, aşağıdaki ifadeyi hello kullanın:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload bir modül FIMPowerShellConnectorModule.psm1 hello % TEMP % klasöründen adında, aşağıdaki ifadeyi hello kullanın:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Parametre doğrulama**  
Hello doğrulama betiği kullanılan tooensure hello Yöneticisi tarafından sağlanan bağlayıcı yapılandırma parametreleri geçerli olabilecek isteğe bağlı bir Windows PowerShell komut dosyasıdır. Doğrulanıyor, bağlantı kimlik bilgileri ve bağlantı parametreleri hello doğrulama betiği, yaygın kullanımları şunlardır. Merhaba aşağıdaki sekmeleri ve iletişim kutuları değiştirildiğinde sonra hello doğrulama betiği çağrılır:

* Bağlantı
* Genel Parametreler
* Bölüm yapılandırma

Merhaba doğrulama betiği hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |Merhaba yapılandırma sekmesi veya hello doğrulama isteği tetiklenen iletişim. |
| ConfigParameters |[KeyedCollection] [ keyk] [dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |

Merhaba doğrulama betiği, tek bir ParameterValidationResult nesne toohello ardışık düzen döndürmelidir.

**Şema bulma**  
Merhaba şema bulma komut dosyasını zorunludur. Bu komut dosyası hello nesne türleri, öznitelikleri ve öznitelik kısıtlamalarını öznitelik akışı kurallarını yapılandırırken eşitleme hizmeti kullanan bu hello döndürür. Merhaba şema bulma komut dosyasını Bağlayıcısı oluşturma sırasında çalıştırılır ve hello bağlayıcı'nın şema doldurur. Ayrıca, hello hello Synchronization Service Manager şema Yenile eylemi tarafından kullanılır.

şu parametreler hello bağlayıcısından hello Hello şema bulma komut dosyasını alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection] [ keyk] [dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |

Merhaba komut dosyası, tek bir döndürmelidir [şema] [ schema] nesne toohello ardışık düzen. Merhaba şema nesnesi oluşur [SchemaType] [ schemaT] nesne türleri temsil eden nesneler (örneğin: kullanıcılar ve gruplar). Merhaba SchemaType nesne koleksiyonunu tutan [SchemaAttribute] [ schemaA] hello özniteliklerini temsil eden nesneler (örneğin: verilen ad, Soyadı ve posta adresi) hello türü.

**Ek parametreler**  
Ayrıca toohello standart yapılandırma ayarları, belirli toohello hello bağlayıcı örneği olan ek özel yapılandırma ayarlarını tanımlayabilirsiniz. Bu parametreleri bölümü hello bağlayıcı belirtilebilir veya çalışma adımı düzeyleri ve hello ilgili Windows PowerShell komut dosyasından erişilebilir. Özel yapılandırma ayarlarına düz metin biçiminde hello eşitleme hizmeti veritabanında depolanabilir veya şifrelenmiş. Merhaba eşitleme hizmeti otomatik olarak şifreler ve gerektiğinde güvenli yapılandırma ayarlarını şifresini çözer.

toospecify özel yapılandırma ayarları, her bir parametreyi virgülle (,) ayrı hello adı.

tooaccess özel yapılandırma ayarlarını bir komut dosyasından hello adı alt çizgi ile soneki gerekir ( \_ ) ve hello kapsamı hello parametre (Genel, bölüm veya RunStep). Örneğin, tooaccess genel FileName parametresi Merhaba, bu kod parçacığını kullanın:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Özellikler
Merhaba yönetim aracı Tasarımcısı Hello özellikleri sekmesinde hello davranışı ve hello bağlayıcı işlevselliğini tanımlar. Merhaba Bağlayıcısı oluşturduğunuzda, bu sekmede yapılan hello seçimleri değiştirilemez. Bu tablo hello yetenek ayarları listeler.

![Özellikler](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Özellik | Açıklama |
| --- | --- |
| [Ayırt edici ad stili][dnstyle] |Merhaba bağlayıcı ayırt edici ad destekliyorsa ve bu nedenle, ne stil gösterir. |
| [Dışarı aktarma türü][exportT] |Merhaba toohello dışa aktarma betiği sunulan nesnelerin türünü belirler. <li>AttributeReplace – hello öznitelik değiştiğinde birden çok değerli bir öznitelik değerlerini hello kümesini içerir.</li><li>AttributeUpdate – hello öznitelik değiştiğinde yalnızca hello farkları tooa birden çok değerli özniteliği içerir.</li><li>MultivaluedReferenceAttributeUpdate - başvuru olmayan birden çok değerli öznitelikler için değerler ve birden çok değerli başvuru özniteliği için yalnızca farkları tam kümesi içerir.</li><li>ObjectReplace – herhangi bir öznitelik değişiklikleri olduğunda bir nesne için tüm özniteliklerini içerir</li> |
| [Veri normalleştirme][DataNorm] |Tooscripts sağlanan önce hello eşitleme hizmeti toonormalize bağlantı öznitelikleri bildirir. |
| [Nesne onayı][oconf] |Bekleyen alma davranışını Hello hello eşitleme hizmetini yapılandırır. <li>Normal – içeri aktarma onaylanıp tüm verilen değişiklikleri toobe bekliyor varsayılan davranışı</li><li>NoDeleteConfirmation – bir nesnesi silindiğinde var. oluşturulan hiçbir bekleyen alma</li><li>NoAddAndDeleteConfirmation – bir nesne oluşturulduğunda veya silindiğinde var. oluşturulan hiçbir bekleyen alma</li> |
| DN bağlantı kullanın |Merhaba ayırt edici adı stil tooLDAP ayarlanmamışsa, hello bağlantı hello bağlayıcı alanı için de hello ayırt edici ad özniteliğidir. |
| Eşzamanlı operasyonlar birkaç bağlayıcı |İşaretlendiğinde, birden çok Windows PowerShell bağlayıcı aynı anda çalışabilir. |
| Bölümler |İşaretlendiğinde, hello Bağlayıcısı birden fazla bölüm ve bölüm bulma destekler. |
| Hiyerarşisi |İşaretlendiğinde, bir LDAP stili hiyerarşik yapısı hello bağlayıcıyı destekler. |
| İçeri aktarma etkinleştir |İşaretlendiğinde, hello Bağlayıcısı verileri içe aktarma komut dosyaları aracılığıyla alır. |
| Delta içeri aktarma etkinleştir |İşaretlendiğinde, hello bağlayıcı farkları hello gelen komut dosyalarını almak isteyebilirsiniz. |
| Vermeyi etkinleştir |İşaretlendiğinde, hello bağlayıcı dışarı aktarma komut dosyaları aracılığıyla veri aktarır. |
| Tam vermeyi etkinleştir |İşaretlendiğinde, hello hello tüm bağlayıcı alanı dışarı aktarma betikleri destek verin. toouse bu seçenek, etkinleştirme verme ayrıca denetlenmesi gerekir. |
| İlk verme geçişi başvuru değer yok |Başvuru özniteliği, bu onay kutusu işaretlendiğinde, ikinci bir dışarı aktarma geçişinde dışarı aktarılır. |
| Nesne yeniden adlandırma etkinleştir |İşaretlendiğinde, ayırt edici ad değiştirilebilir. |
| Değiştirirken DELETE Ekle |İşaretlendiğinde,-işlemlerini tek bir değiştirme dışarı aktarılır delete ekleyin. |
| Parola işlemleri etkinleştir |İşaretlendiğinde, parola eşitleme komut dosyaları desteklenir. |
| Dışarı aktarma parolasını ilk seferde etkinleştir |Hello nesnesi oluşturulduğunda, bu onay kutusu işaretlendiğinde, sağlama işlemi sırasında ayarlamak parolalar dışa. |

### <a name="global-parameters"></a>Genel Parametreler
Merhaba yönetim aracı Tasarımcısı Hello genel parametreleri sekmesinde hello bağlayıcı tarafından çalıştırılan tooconfigure hello Windows PowerShell komut dosyaları sağlar. Merhaba bağlantı sekmesinde tanımlanan özel yapılandırma ayarları için genel değerleri de yapılandırabilirsiniz.

**Bölüm bulma**  
Bir bölüm bir paylaşılan şema içinde ayrı bir ad alanıdır. Örneğin, Active Directory'de bir bölüm bir ormandaki her etki alanıdır. Mantıksal bir gruplandırma hello içeri aktarma için bir bölümdür ve verme işlemleri. Bir bağlam ve tüm işlemler olduğu sürece bu bağlamda içeri ve dışarı aktarma bölümü olmalıdır. Bölümler toorepresent bir hiyerarşi LDAP'de beklenen. bir bölüm ayırt edici adını Hello döndürülen tüm nesneleri hello bir bölüm kapsamındaki alma tooverify kullanılır. Merhaba bölüm ayırt edici adı de bölümünden dışa aktarma sırasında nesne ile ilişkili olmalıdır hello meta veri deposu toohello bağlayıcı alanı toodetermine hello sağlama sırasında kullanılır.

şu parametreler hello bağlayıcısından hello Hello bölüm bulma komut dosyasını alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |

Merhaba betik bir ya da tek bir döndürmelidir [bölüm] [ part] nesne veya bölüm nesneleri toohello ardışık [T] listesi.

**Hiyerarşi bulma**  
Merhaba hiyerarşi bulma komut dosyası, yalnızca Hello ayırt edici adı stil özelliği LDAP olduğunda kullanılır. Merhaba, toobrowse seçin ya da için kapsam dışına olarak kabul edilen bir dizi kapsayıcıları alma ve verme işlemleri kullanılan tooallow betiğidir. Merhaba betik yalnızca hello kök düğümü sağlanan toohello betik doğrudan alt düğümleri listesini sağlaması gerekir.

şu parametreler hello bağlayıcısından hello Hello hiyerarşi bulma komut dosyasını alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| ParentNode |[HierarchyNode][hn] |Merhaba kök düğümü hello hiyerarşisinin hangi hello doğrudan alt betik döndürmelidir. |

Merhaba betik bir ya da tek alt HierarchyNode nesne veya alt HierarchyNode nesneleri toohello ardışık listesi [T] döndürmelidir.

#### <a name="import"></a>İçeri Aktarma
İçeri aktarma işlemlerini destekleyen bağlayıcılar üç betikleri uygulamalıdır.

**Başlangıç alma**  
Merhaba başlamak alma betiği Çalıştır alma adımı hello başında çalıştırın. Bu adım sırasında bir bağlantı toohello kaynak sistemi oluşturun ve hello veri alma sisteme bağlı önce hazırlık adımları uygulayın.

Merhaba başlamak alma betiği şu parametreler hello bağlayıcısından hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Merhaba betik hello türü (Değişim veya tam) almayı Çalıştır bölüm, hiyerarşi, filigran ve beklenen sayfa boyutu hakkında bilgilendirir. |
| Türler |[Şema][schema] |Alınan hello bağlayıcı alanı için şema. |

Merhaba komut dosyası, tek bir döndürmelidir [OpenImportConnectionResults] [ oicres] nesne toohello ardışık düzen, örneğin:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Veri alma**  
Merhaba komut dosyası hiçbir daha fazla veri tooimport olduğunu gösterir kadar hello alma veri betiği hello bağlayıcı tarafından çağrılır. Merhaba Windows PowerShell Bağlayıcısı 9.999 nesnelerin bir sayfa boyutu vardır. Kodunuzu almak için birden fazla 9.999 nesneleri döndürürse, disk belleği desteklemelidir. hello bağlayıcı çıkarır, her zaman hello içe veri betik böylece tooa deposunu Filigran kullanabileceğiniz bir özel veri özelliği olarak adlandırılır, kaldığı yerden nesneleri içe aktarma komut dosyanızı sürdürür.

Merhaba alma veri betiği hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Disk belleğine alınan içeri aktarımlar sırasında kullanılan Filigran (CustomData) ayrı tutma hello ve delta alır. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Merhaba betik hello türü (Değişim veya tam) almayı Çalıştır bölüm, hiyerarşi, filigran ve beklenen sayfa boyutu hakkında bilgilendirir. |
| Türler |[Şema][schema] |Alınan hello bağlayıcı alanı için şema. |

Merhaba alma veri betiği listesini yazmalısınız [[CSEntryChange][csec]] nesne toohello ardışık düzen. Bu koleksiyon, içeri aktarılan her nesneyi temsil eden CSEntryChange özniteliklerini oluşur. Tam içeri aktarma çalıştırması sırasında bu koleksiyonu tüm öznitelikleri her nesne için sahip CSEntryChange nesneleri tam bir dizi olmalıdır. Delta içeri aktarma sırasında hello CSEntryChange nesne ya da her nesne tooimport veya (değiştirme modu) değiştirilen hello nesneleri tam bir gösterimini hello öznitelik düzeyi farkları içermelidir.

**Son alma**  
Hello sonuç çalıştırmak hello alma işleminin hello son alma betiği çalıştırılır. Bu komut tüm temizleme gerekli görevleri (örneğin, Kapat bağlantıları toosystems ve yanıt toofailures) gerçekleştirmeniz gerekir.

Merhaba son alma betiği şu parametreler hello bağlayıcısından hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Merhaba betik hello türü (Değişim veya tam) almayı Çalıştır bölüm, hiyerarşi, filigran ve beklenen sayfa boyutu hakkında bilgilendirir. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Merhaba betik hello alma sonlandırıldı hello nedeni hakkında bilgilendirir. |

Merhaba komut dosyası, tek bir döndürmelidir [CloseImportConnectionResults] [ cicres] nesne toohello ardışık düzen, örneğin:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Dışarı Aktarma
Merhaba bağlayıcı aynı toohello alma mimarisi, üç komut dosyaları dışarı aktarma desteği bağlayıcılar uygulamalıdır.

**Begin dışarı aktarma**  
Merhaba başlamak dışa aktarma betiği Çalıştır verme adımını hello başında çalıştırın. Bu adım sırasında bir bağlantı toohello kaynak sistemi oluşturun ve veri toohello verme sistemine bağlanan önce herhangi bir hazırlık adımı gerçekleştirin.

Merhaba başlamak dışa aktarma betiği hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Merhaba betik hello türü (Değişim veya tam) verme çalıştırma bölüm, hiyerarşi ve beklenen sayfa boyutu hakkında bilgilendirir. |
| Türler |[Şema][schema] |Dışa aktarılan hello bağlayıcı alanı için şema. |

Merhaba betik, hiçbir çıkış toohello ardışık düzen vermemelidir.

**Verileri dışarı aktarma**  
Merhaba eşitleme hizmeti hello veri dışarı aktarma betiği gerekli tooprocess tüm bekleyen dışarı aktarmalar olduğu gibi birçok kez olarak çağırır. Merhaba bağlayıcı alanı bağlayıcı sayfa boyutu hello olandan daha fazla bekleyen dışarı aktarmalar varsa, veri betiği birden çok kez çağrılabilir hello verme ve büyük olasılıkla birden çok kez için aynı nesne hello.

Merhaba dışarı aktarma veri betiği hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| CSEntries |IList[CSEntryChange][csec] |Merhaba bağlayıcı alanı bekleyen tüm nesneler ile bu geçişi sırasında işlenen dışarı toobe listesi. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Merhaba betik hello türü (Değişim veya tam) verme çalıştırma bölüm, hiyerarşi ve beklenen sayfa boyutu hakkında bilgilendirir. |
| Türler |[Şema][schema] |Dışa aktarılan hello bağlayıcı alanı için şema. |

Merhaba dışarı aktarma veri betiği döndürmelidir bir [PutExportEntriesResults] [ peeres] nesne toohello ardışık düzen. Bir hata ya da değişiklik toohello bağlantı özniteliği oluşmadığı sürece bu nesne için dışarı aktarılan her bağlayıcı tooinclude sonuç bilgilerini gerekli değildir. Örneğin, tooreturn PutExportEntriesResults nesne toohello işlem hattı:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Son verme**  
Merhaba sonuç hello dışa aktarma sırasında çalıştırın, komut dosyası toorun son verme hello. Bu komut tüm temizleme gerekli görevleri (örneğin, Kapat bağlantıları toosystems ve yanıt toofailures) gerçekleştirmeniz gerekir.

Merhaba son dışa aktarma betiği hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Merhaba betik hello türü (Değişim veya tam) verme çalıştırma bölüm, hiyerarşi ve beklenen sayfa boyutu hakkında bilgilendirir. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Merhaba betik hello verme sonlandırıldı hello nedeni hakkında bilgilendirir. |

Merhaba betik, hiçbir çıkış toohello ardışık düzen vermemelidir.

#### <a name="password-synchronization"></a>Parola Eşitleme
Windows PowerShell bağlayıcılar parola değişiklikleri/sıfırlama için hedef olarak kullanılabilir.

Merhaba parola betik hello bağlayıcısından şu parametreler hello alır:

| Ad | Veri türü | Açıklama |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][dize [ConfigParameter][cp]] |Merhaba Bağlayıcısı için yapılandırma parametreleri Tablo. |
| Kimlik Bilgisi |[PSCredential][pscred] |Hello Yöneticisi tarafından hello bağlantı sekmesinde girilmiş olan kimlik bilgileri içerir. |
| Bölüm |[Bölüm][part] |CSEntry hello dizini bölümü kullanılıyor. |
| CSEntry |[CSEntry][cse] |Bağlayıcı alanı girdisi hello nesne için bir parola değiştirme veya sıfırlama aldı. |
| OperationType |Dize |Merhaba işlemi sıfırlama olup olmadığını gösterir (**SetPassword**) veya bir değiştirme (**parola değiştirme**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Merhaba belirtin bayrakları davranışı parola sıfırlama amaçlanmıştır. Bu parametre yalnızca OperationType ise kullanılabilir **SetPassword**. |
| EskiParola |Dize |Parola değişiklikleri için hello nesnenin eski parola ile doldurulur. Bu parametre yalnızca OperationType ise kullanılabilir **parola değiştirme**. |
| #Newpassword |Dize |Merhaba betik ayarlaması gereken hello nesnenin yeni parola ile doldurulur. |

Merhaba parola betik değil beklenen tooreturn tüm sonuçları toohello Windows PowerShell komut zincirini olduğu. Merhaba parola komut dosyasında bir hata meydana gelirse hello betik hello sorun hakkında özel durumları tooinform hello eşitleme hizmeti aşağıdaki hello birini oluşturması gerekir:

* [PasswordPolicyViolationException] [ pwdex1] – hello parola bağlı hello sistemde hello parola ilkesi karşılamıyorsa oluşturulur.
* [PasswordIllFormedException] [ pwdex2] – hello parola bağlı hello sistemi için kabul edilebilir değilse oluşturulur.
* [PasswordExtension] [ pwdex3] – hello parola betik diğer tüm hatalar için oluşturulur.

## <a name="sample-connectors"></a>Örnek bağlayıcılar
Merhaba kullanılabilir örnek bağlayıcılar eksiksiz bir genel bakış için bkz: [Windows PowerShell Bağlayıcısı örnek bağlayıcı koleksiyonu][samp].

## <a name="other-notes"></a>Diğer Notlar
### <a name="additional-configuration-for-impersonation"></a>Kimliğe bürünme için ek yapılandırma
Merhaba hello eşitleme hizmeti sunucu üzerindeki izinleri aşağıdaki Kimliğine bürünülen hello kullanıcı verin:

Kayıt defteri anahtarlarını aşağıdaki okuma erişimi toohello:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID] \Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID] \Environment

toodetermine hello hello aşağıdaki PowerShell komutlarını çalıştırın, hello eşitleme hizmeti hizmet hesabının güvenlik tanımlayıcısı (SID):

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Okuma erişimi toohello aşağıdaki sistem klasörlerinin dosya:

* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Hello {ConnectorName} yer tutucusu hello Windows PowerShell Bağlayıcısı Hello adını değiştirin.

## <a name="troubleshooting"></a>Sorun giderme
* Merhaba nasıl tooenable günlük tootroubleshoot hello Bağlayıcısı hakkında daha fazla bilgi için bkz [nasıl tooEnable ETW İzleme bağlayıcıların](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
