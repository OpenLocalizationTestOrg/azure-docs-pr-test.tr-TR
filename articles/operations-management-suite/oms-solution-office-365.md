---
title: "aaaOffice 365 çözümü Operations Management Suite (OMS) | Microsoft Docs"
description: "Bu makale, yapılandırma ve kullanımı OMS çözümde hello Office 365 ile ilgili ayrıntıları sağlar.  Günlük analizi oluşturulan hello Office 365 kayıtları ayrıntılı açıklamasını içerir."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Office 365 çözümü Operations Management Suite (OMS)

![Office 365 logosu](media/oms-solution-office-365/icon.png)

Merhaba Office 365 çözümü Operations Management Suite (OMS) toomonitor verir günlük analizi, Office 365 ortamınızda.  

- Office 365 hesapları tooanalyze kullanım desenlerini kullanıcı etkinliklerini izlemek yanı sıra davranış eğilimlerini. Örneğin, kuruluşunuz veya hello en popüler SharePoint siteleri dışında paylaşılan dosyaları gibi belirli kullanım senaryoları ayıklayabilirsiniz.
- Yönetici etkinlikleri tootrack yapılandırma değişikliklerini veya yüksek ayrıcalıklı işlemleri izleyin.
- Algılama ve kuruluş gereksinimlerinize göre özelleştirilmiş istenmeyen kullanıcı davranışı araştırın.
- Denetim ve uyumluluk gösterir. Örneğin, dosya erişim işlemleri hello denetim ve uyumluluk işlemiyle yardımcı olabilecek gizli dosyalarda izleyebilirsiniz.
- OMS arama en üstünde, kuruluşunuzun Office 365 etkinlik verileri kullanarak işlemsel sorun giderme gerçekleştirir.

## <a name="prerequisites"></a>Ön koşullar
Merhaba, yüklenmiş ve yapılandırılmış gerekli önceki toothis çözüm aşağıdadır.

- Kuruluş Office 365 aboneliği.
- Genel yönetici olan bir kullanıcı hesabı için kimlik bilgileri.
- tooreceive denetim verilerini gerekir [denetimini yapılandırmak](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) Office 365 aboneliğinizde.  Unutmayın [posta kutusu denetimi](https://technet.microsoft.com/library/dn879651.aspx) ayrı olarak yapılandırılır.  Hala hello çözümü yüklemek ve denetim yapılandırılmamışsa diğer verileri toplar.
 


## <a name="management-packs"></a>Yönetim paketleri
Bu çözüm, bağlı yönetim gruplarında herhangi bir Yönetim Paketi yüklemez.
  

## <a name="configuration"></a>Yapılandırma
Bir kez, [hello Office 365 çözümü tooyour Abonelik Ekle](../log-analytics/log-analytics-add-solutions.md), tooconnect sahip, tooyour Office 365 aboneliği.

1. Merhaba işlemi kullanarak OMS çalışma açıklanan hello uyarı yönetimi çözümü tooyour eklemek [çözümleri Ekle](../log-analytics/log-analytics-add-solutions.md).
2. Çok Git**ayarları** hello OMS portalında.
3. Altında **bağlı kaynakları**seçin **Office 365**.
4. Tıklayın **Office 365 bağlanmak**.<br>![Bağlantı Office 365](media/oms-solution-office-365/configure.png)
5. TooOffice 365 aboneliğiniz için bir genel yönetici olan bir hesapla oturum. 
6. Merhaba abonelik hello çözüm izleyeceğiniz hello iş yükleri ile listelenir.<br>![Bağlantı Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Veri toplama
### <a name="supported-agents"></a>Desteklenen aracılar
Merhaba Office 365 çözümü veri alma değil hello hiçbirini [OMS Aracısı](../log-analytics/log-analytics-data-sources.md).  Office 365'ten doğrudan verileri alır.

### <a name="collection-frequency"></a>Toplama sıklığı
Office 365 gönderir bir [Web kancası bildirim](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) ayrıntılı veri tooLog ile Analytics her zaman bir kayıt oluşturulur.

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak
Merhaba Office 365 çözümü tooyour OMS çalışma eklediğinizde, hello **Office 365** döşeme tooyour OMS Pano eklenir. Bu kutucuğu ortamınıza ve güncelleştirme uyumluluklarını sayısı ve grafik gösterimi hello bilgisayarların sayısını görüntüler.<br><br>
![Office 365 Özet kutucuğu](media/oms-solution-office-365/tile.png)  

Tıklatın hello üzerinde **Office 365** döşeme tooopen hello **Office 365** Pano.

![Office 365 Panosu](media/oms-solution-office-365/dashboard.png)  

Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir. Her sütun sütunun ölçütleri hello için kapsam ve zaman aralığını belirtilen sayısı eşleşen tarafından hello üst on uyarıları listeler. Bkz: hello sütunun hello altındaki tüm tıklatarak veya hello sütun başlığını tıklatarak hello tüm listesini sağlayan bir günlük arama yapabilirsiniz.

| Sütun | Açıklama |
|:--|:--|
| İşlemler | İzlenen tüm Office 365 aboneliklerinizi etkin kullanıcılardan hello hakkında bilgi sağlar. Ayrıca, mümkün toosee hello zaman içinde gerçekleşen etkinliklerin sayısını olacaktır.
| Exchange | Posta Kutusu Ekle izni veya Set-Mailbox gibi Exchange Server etkinlikleri Hello dökümünü gösterir. |
| SharePoint | Kullanıcılar SharePoint belgelerindeki gerçekleştirmek Hello üst etkinlikleri gösterir. Bu kutucuğunda detaya zaman hello arama sayfası hello hedef belge ve bu etkinliği hello konumunu gibi bu etkinlikler hello ayrıntılarını gösterir. Örneğin, dosyaya erişim bir olay için erişiliyor, mümkün toosee hello belge siz olacaksınız ilişkili hesap adı ve IP adresi. |
| Azure Active Directory | Kullanıcı parola sıfırlama ve oturum açma denemesi gibi en çok kullanan kullanıcı etkinlikleri içerir. Ayrıntıya mümkün toosee hello sonuç durumu hello gibi bu etkinlikler ayrıntılarını olacaktır. Bu genellikle, Azure Active Directory toomonitor kuşkulu etkinlikleri istiyorsanız yararlıdır. |




## <a name="log-analytics-records"></a>Log Analytics kayıtları

Merhaba günlük analizi çalışma alanında hello Office 365 çözümü tarafından oluşturulan tüm kayıtlarına sahip bir **türü** , **OfficeActivity**.  Merhaba **OfficeWorkload** özelliği belirler çok Exchange, AzureActiveDirectory, SharePoint veya OneDrive, Office 365 hizmet hello kaydı başvuruyor.  Merhaba **RecordType** özelliği hello işlemi türünü belirtir.  Merhaba özellikleri her işlem türü için değişir ve hello aşağıdaki tablolarda gösterilmiştir.

### <a name="common-properties"></a>Ortak Özellikler
aşağıdaki özelliklere hello ortak tooall Office 365 kayıtlarıdır.

| Özellik | Açıklama |
|:--- |:--- |
| Tür | *OfficeActivity* |
| ClientIP | Merhaba etkinlik oturum açıldığında, kullanılan hello aygıt Hello IP adresi. Başlangıç IP adresi, bir IPv4 veya IPv6 adresi biçiminde görüntülenir. |
| OfficeWorkload | Kayıt hello office 365 hizmet ifade eder.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| İşlem | Merhaba kullanıcı veya yönetici etkinliği Hello adı.  |
| OrganizationId | Merhaba, kuruluşunuzun Office 365 Kiracı için GUID. Bu değer her zaman olması Merhaba aynı kuruluşunuz için ne olursa olsun, hangi BT hello Office 365 hizmetinde oluşur. |
| RecordType | Gerçekleştirilen işlem türü. |
| ResultStatus | Merhaba eylem (belirtilen hello işlemi özelliği) başarılı olup olmadığını gösterir. Olası değerler, başarılı, PartiallySucceded veya başarısız olur. Exchange yönetici etkinliği için hello değer her iki true'dur ya da yanlış. |
| Kullanıcı Kimliği | Merhaba günlüğe kaydedilmesini hello kaydında sonuçlandı hello eylem gerçekleştiren hello kullanıcının UPN'sini (kullanıcı asıl adı); Örneğin, my_name@my_domain_name. Sistem hesapları (örneğin, SHAREPOINT\system veya ntauthority\system adlı) tarafından gerçekleştirilen etkinlik kayıtlarını da dahil olduğunu unutmayın. | 
| UserKey | Merhaba UserId özelliği tanımlanan hello kullanıcı için alternatif bir kimliği.  Örneğin, bu özellik, iş ve Exchange için SharePoint, OneDrive bulunan kullanıcılar tarafından gerçekleştirilen olaylar için hello passport benzersiz kimliği ile (PUID) doldurulur. Bu özellik de hello diğer hizmetler ve olayları gerçekleşen olayların UserId özelliği aynı değere sistem hesapları tarafından gerçekleştirilen hello belirtebilir|
| UserType | Merhaba işlemi gerçekleştirilen kullanıcı Hello türü.<br><br>Yönetici<br>Uygulama<br>DcAdmin<br>Normal<br>Ayrılmış<br>ServicePrincipal<br>Sistem |


### <a name="azure-active-directory-base"></a>Azure Active Directory temel
aşağıdaki özelliklere hello ortak tooall Azure Active Directory kayıtlarıdır.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | Azure AD olay Hello türü. |
| extendedProperties | Merhaba hello Azure AD olay özelliklerini genişletilmiş. |


### <a name="azure-active-directory-account-logon"></a>Azure Active Directory hesabı oturum açma
Bir Active Directory kullanıcı üzerinde toolog çalıştığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| Uygulama | Office 15 gibi hello hesap oturum açma olayı tetikler Merhaba uygulaması. |
| İstemci | Merhaba istemci ayrıntılarını aygıt, cihaz işletim sistemi ve hello hesap oturum açma olayı hello için kullanılan cihazdır. |
| loginStatus | Bu özellik, doğrudan OrgIdLogon.LoginStatus olur. çeşitli ilginç oturum açma hatalarının Hello eşleme algoritmaları uyarı tarafından yapılabilir. |
| UserDomain | Merhaba Kiracı kimlik bilgileri (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Değiştirme veya ekleme tooAzure Active Directory nesnelerini yapıldığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | (Merhaba işlemi özelliği tarafından tanımlanan) eylemin hello hello kullanıcı üzerinde gerçekleştirildi. |
| Aktör | Merhaba kullanıcı veya hello gerçekleştirdiğini hizmet sorumlusu. |
| ActorContextId | Merhaba aktör hello hello kuruluşun GUID ait. |
| ActorIpAddress | Aktör'ın IP adresi IPv4 veya IPv6 adresi biçiminde hello. |
| InterSystemsId | Merhaba hello Office 365 hizmet içinde bileşenleri arasında hello eylemleri izlemek GUID. |
| IntraSystemId |   Hello Azure Active Directory tootrack hello eylemi tarafından üretilen GUID. |
| SupportTicketId | Merhaba müşteri durumlarda "act-üzerinde-adına-of" Merhaba eylemi için bilet kimliği destekler. |
| TargetContextId | Merhaba hedeflenen kullanıcı hello hello kuruluşun GUID ait. |


### <a name="data-center-security"></a>Veri Merkezi güvenlik
Bu kayıtları veri merkezi güvenlik denetim verilerden oluşturulur.  

| Özellik | Açıklama |
|:--- |:--- |
| EffectiveOrganization | Yükseltme/cmdlet hello hello Kiracı Hello adı hedefleyen. |
| ElevationApprovedTime | Merhaba zaman, hello ayrıcalık onaylandığı zaman damgası. |
| ElevationApprover | bir Microsoft Yöneticisi Hello adı. |
| ElevationDuration | Yükseltme için hangi hello etkin hello süresi. |
| ElevationRequestId |  Merhaba yükseltme isteği için benzersiz bir tanımlayıcı. |
| ElevationRole | Merhaba rol hello yükseltme için istendi. |
| ElevationTime | Merhaba hello yükseltme süresini başlatın. |
| Start_Time | Merhaba hello cmdlet'ini yürütme zamanı başlatın. |


### <a name="exchange-admin"></a>Exchange yönetici
TooExchange yapılandırma değişiklik yapıldığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  Merhaba cmdlet kuruluşunuz, Microsoft datacenter personeli tarafından veya bir veri merkezi hizmet hesabı bir kullanıcı tarafından veya yönetici temsilcisi tarafından çalıştırılıp çalıştırılmadığını belirtir. Bu hello cmdlet, kuruluşunuzdaki bir kişi tarafından çalıştırıldığı Hello değeri False gösterir. Hello değeri True, o hello cmdlet datacenter personel, bir veri merkezi hizmet hesabı veya yönetici temsilcisi tarafından çalıştırıldığı gösterir. |
| ModifiedObjectResolvedName |  Bu hello kullanıcı kolay hello cmdlet tarafından değiştirilen hello nesnesinin adıdır. Bu, yalnızca hello cmdlet hello nesne değiştiriyorsa kaydedilir. |
| Kuruluş adı | Merhaba Kiracı Hello adı. |
| OriginatingServer | Merhaba hangi hello cmdlet yürütülen hello sunucunun adıdır. |
| Parametreler | Merhaba adı ve hello işlemleri özelliği tanımlanan hello cmdlet ile kullanılan tüm parametreler için değer. |


### <a name="exchange-mailbox"></a>Exchange posta kutusu
Değişiklikler ve eklemeler tooExchange posta kutularını yapıldığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | Kullanılan tooperform hello işleminden, tarayıcı sürümü, Outlook sürümü ve mobil aygıt bilgileri gibi hello e-posta istemcisi hakkında bilgi. |
| Client_IPAddress | Merhaba işlemi oturum açıldığında, kullanılan hello aygıt Hello IP adresi. Başlangıç IP adresi, bir IPv4 veya IPv6 adresi biçiminde görüntülenir. |
| ClientMachineName | Merhaba Outlook istemcisi barındıran hello makine adı. |
| ClientProcessName | kullanılan tooaccess hello posta kutusu olduğu hello e-posta istemcisi. |
| ClientVersion | Merhaba hello e-posta istemcisi sürümü. |
| InternalLogonType | İç kullanım için ayrılmıştır. |
| Logon_Type | Hello posta kutusu erişilen ve günlüğe hello işlemi gerçekleştiren kullanıcı Hello türünü belirtir. |
| LogonUserDisplayName |    Merhaba kullanıcı dostu hello işlemi gerçekleştiren hello kullanıcı adıdır. |
| LogonUserSid | Merhaba hello işlemi gerçekleştiren hello kullanıcı SID'si. |
| MailboxGuid | Merhaba erişilen hello posta kutusunun Exchange GUID. |
| MailboxOwnerMasterAccountSid | Posta kutusu sahibi hesabının yönetici hesabı SID'si. |
| MailboxOwnerSid | Merhaba hello posta kutusu sahibi SID'si. |
| MailboxOwnerUPN | erişilen hello posta kutusu sahibi hello kişinin Hello e-posta adresi. |


### <a name="exchange-mailbox-audit"></a>Exchange posta kutusu denetimi
Bir posta kutusu denetim girdisi oluşturulduğunda bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| Öğe | İşlem sırasında hangi hello gerçekleştirildi hello öğeyi temsil eder | 
| SendAsUserMailboxGuid | Merhaba edildi hello posta kutusunun Exchange GUID toosend e-posta olarak erişilir. |
| SendAsUserSmtp | Kimliğine bürünülen hello kullanıcının SMTP adresi. |
| SendonBehalfOfUserMailboxGuid | Merhaba edildi hello posta kutusunun Exchange GUID toosend posta adına erişilir. |
| SendOnBehalfOfUserSmtp | E-posta adına hello üzerinde hello kullanıcının SMTP adresi gönderilir. |


### <a name="exchange-mailbox-audit-group"></a>Exchange posta kutusu denetim grubu
Değişiklikler ve eklemeler tooExchange grupları yapıldığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Merhaba gruptaki her öğe hakkında bilgiler. |
| CrossMailboxOperations | Hello işlemi birden fazla posta kutusu dahil olmadığını gösterir. |
| DestMailboxId | Yalnızca hello CrossMailboxOperations parametresi True ise ayarlayın. Merhaba hedef posta kutusu GUID belirtir. |
| DestMailboxOwnerMasterAccountSid | Yalnızca hello CrossMailboxOperations parametresi True ise ayarlayın. Hello yöneticisi hesabı hello hedef posta kutusu sahibi SID'si için SID Hello belirtir. |
| DestMailboxOwnerSid | Yalnızca hello CrossMailboxOperations parametresi True ise ayarlayın. Merhaba hello hedef posta kutusu SID'si belirtir. |
| DestMailboxOwnerUPN | Yalnızca hello CrossMailboxOperations parametresi True ise ayarlayın. Merhaba hello hedef posta kutusu hello sahibinin UPN belirtir. |
| DestFolder | Taşıma gibi işlemleri için hedef klasör Hello. |
| Klasör | bir öğe grubunu bulunduğu hello klasör. |
| Klasörler |     Merhaba kaynak klasörleri bir işlemde yer alan hakkında bilgi; Örneğin, klasörleri seçtiyseniz ve ardından silinir. |


### <a name="sharepoint-base"></a>SharePoint tabanı
Bu özellikler yaygın tooall SharePoint kayıtlarıdır.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Bir olay SharePoint'te oluştuğunu tanımlar. Olası değerler, SharePoint veya ObjectModel olur. |
| itemType | erişilen veya değiştirilmiş nesnesinin Hello türü. Bkz: Merhaba ItemType tablo hello türdeki nesneler hakkında ayrıntılı bilgi için. |
| MachineDomainInfo | Aygıt eşitleme işlemleri hakkında bilgi. Bu bilgiler, yalnızca hello istekte mevcut değilse bildirilir. |
| ResourceId |   Aygıt eşitleme işlemleri hakkında bilgi. Bu bilgiler, yalnızca hello istekte mevcut değilse bildirilir. |
| Site_ | Merhaba hello dosya veya klasör hello kullanıcı tarafından erişilen bulunduğu hello sitesinin GUID. |
| Source_Name | Merhaba tetiklenen hello varlık işlemi denetleniyor. Olası değerler, SharePoint veya ObjectModel olur. |
| UserAgent | Merhaba kullanıcının istemci veya tarayıcı ilgili bilgiler. Bu bilgiler hello istemci veya tarayıcı tarafından sağlanır. |


### <a name="sharepoint-schema"></a>SharePoint şeması
Yapılandırma değişiklikleri tooSharePoint yapıldığında bu kayıtları oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Özel olaylar için isteğe bağlı dize. |
| Event_Data |  Özel olaylar için isteğe bağlı yükü. |
| ModifiedProperties | Merhaba özelliğini bir site veya bir site koleksiyonu yönetici grubunun bir üyesi olarak kullanıcı ekleme gibi yönetim olaylar için dahil edilmiştir. Merhaba özelliği (örneğin, hello Site Yönetici grubu), hello özelliği (site yöneticisi olarak eklenmiş gibi hello kullanıcının) hello değerini değiştiren ve nesne hello önceki hello değerini değiştiren yeni değiştirildiği hello özelliğinin hello adını içerir. |


### <a name="sharepoint-file-operations"></a>SharePoint dosya işlemleri
Bu kayıtları SharePoint yanıt toofile işlemlerinde oluşturulur.

| Özellik | Açıklama |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | kopyalanan veya taşınan bir dosyanın dosya uzantısını Hello. Bu özellik yalnızca FileCopied ve FileMoved olaylar için görüntülenir. |
| DestinationFileName öğesinin | kopyalanan veya taşınan hello dosyasının Hello adı. Bu özellik yalnızca FileCopied ve FileMoved olaylar için görüntülenir. |
| DestinationRelativeUrl | Burada bir dosya kopyalanan taşınmış veya hello hedef klasörü Hello URL'si. hello değerleri SiteURL, DestinationRelativeURL ve destinationFileName öğesinin parametreleri için Hello birleşimi olan hello hello tam yol adı kopyalanmıştır hello dosyası için hello objectID özelliği için hello değer ile aynı. Bu özellik yalnızca FileCopied ve FileMoved olaylar için görüntülenir. |
| SharingType | Paylaşım hello kaynak ile paylaşıldı toohello kullanıcı atanmış izinleri hello türü. Bu kullanıcı hello UserSharedWith parametresi tarafından tanımlanır. |
| Site_Url | Merhaba dosya veya klasör hello kullanıcı tarafından erişilen bulunduğu hello site Hello URL'si. |
| SourceFileExtension | Merhaba kullanıcı tarafından erişilen hello dosya Hello dosya uzantısı. Bu özellik, erişilen hello nesnesi bir klasör ise boştur. |
| SourceFileName |  Merhaba dosya veya klasör hello kullanıcı tarafından erişilen Hello adı. |
| SourceRelativeUrl | Merhaba kullanıcı tarafından erişilen hello dosya içeren hello klasörü Hello URL'si. Merhaba SiteURL, SourceRelativeURL ve SourceFileName parametreleri hello değerlerinin Hello bileşimi olan hello hello tam yol adı hello kullanıcı tarafından erişilen hello dosyası için hello objectID özelliği için hello değer ile aynı. |
| UserSharedWith |  bir kaynak ile paylaşıldı hello kullanıcı. |




## <a name="sample-log-searches"></a>Örnek günlük aramaları
Aşağıdaki tablonun hello bu çözümü tarafından toplanan güncelleştirme kayıtları için örnek günlük aramaları sağlar.

| Sorgu | Açıklama |
| --- | --- |
|Office 365 aboneliğinizin tüm hello işlemlerinin sayısı |' Türü OfficeActivity = | İşlem tarafından Count() ölçmek ' |
|SharePoint siteleri kullanımı|' Türü OfficeActivity OfficeWorkload = sharepoint = | Ölçü count() SiteUrl bazında sayı olarak | Count asc sıralama '|
|Kullanıcı türüne göre dosya erişim işlemleri|' Türü OfficeActivity OfficeWorkload = sharepoint işlemi = FileAccessed = | UserType tarafından Count() ölçmek '|
|Belirli bir anahtar sözcük ile arama|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Exchange dış eylemlerini izleme|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Sorun giderme

Office 365 çözümünüzü veri beklendiği gibi topluyor değil, hello OMS portalında durumunu denetleyin. **ayarları** -> **bağlı kaynakları** -> **Office 365** . Aşağıdaki tablonun hello her durumu açıklar.

| Durum | Açıklama |
|:--|:--|
| Etkin | Merhaba Office 365 abonelik etkin ve hello iş yükü başarıyla bağlı tooyour OMS çalışma. |
| Beklemede | Merhaba Office 365 aboneliği etkindir ancak hello iş yükü değil henüz tooyour OMS çalışma başarıyla bağlandı. başarıyla bağlanıldı kadar hello hello Office 365 aboneliği ilk bağlandığınızda tüm hello iş yükleri bu durum olmayacaktır. Lütfen tüm hello iş yükleri tooswitch tooActive için 24 saat bekleyin. |
| Etkin olmayan | Merhaba Office 365 abonelik etkin olmayan bir durumda. Ayrıntılar için Office 365 Yönetici sayfanızı denetleyin. Office 365 aboneliğinize etkinleştirdikten sonra OMS çalışma alanından bağlantısını ve veri alma toostart yeniden bağlayın. |



## <a name="next-steps"></a>Sonraki adımlar
* Günlük aramalarda kullanması [günlük analizi](../log-analytics/log-analytics-log-searches.md) tooview ayrıntılı veri güncelleştir.
* [Kendi panolar oluşturun](../log-analytics/log-analytics-dashboards.md) toodisplay sık kullanılan Office 365 arama sorgularınızı.
* [Uyarı oluşturma](../log-analytics/log-analytics-alerts.md) önemli Office 365 etkinliklerini önceden bildirimde toobe.  
