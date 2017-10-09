---
title: "Stream Analytics çıkışları: depolama, çözümleme için Seçenekler | Microsoft Docs"
description: "Stream Analytics veri çıkış seçenekleri analiz sonuçları için Power BI dahil olmak üzere hedefleme hakkında bilgi edinin."
keywords: "veri dönüştürme, analiz sonuçları, veri depolama seçenekleri"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Stream Analytics çıkışları: depolama, çözümleme için seçenekleri
Akış analizi işi yazarken hello sonuç verileri nasıl kullanılacağını düşünün. Merhaba Stream Analytics işi hello sonuçlarını nasıl görüntüler ve burada depolar?

Sipariş tooenable uygulama düzenleri çeşitli'da, Azure akış analizi çıkış depolamak ve çözümleme sonuçlarını görüntülemek için farklı seçenekler vardır. Bu, kolay tooview iş çıktısı kolaylaştırır ve veri ambarı ve diğer amaçlar için hello tüketim ve hello iş çıktısı depolama esnekliği sağlar. Merhaba işinde yapılandırılmış herhangi bir çıktı hello iş başlatıldı ve akan olayları başlatmak için önce mevcut olması gerekir. Blob Depolama çıkış olarak kullanırsanız, örneğin, hello iş bir depolama hesabı otomatik olarak oluşturmaz. Merhaba ASA işi başlatılmadan önce hello kullanıcı tarafından oluşturulan toobe gerekir.

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
Stream Analytics destekler [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Bu depolama işletimsel ve keşifsel analiz herhangi boyutu, türü ve alım hızına toostore veri sağlar. Ayrıca, Stream Analytics gereksinimlerini toobe tooaccess hello Data Lake Store yetkili. Yetkilendirme ve toosign hello (gerekirse) Data Lake Store kaydınızı hello tartışılır nasıl hakkında ayrıntılar [Data Lake çıktı makale](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Bir Azure Data Lake Store yetkilendirmek
Data Lake Storage hello Azure portalında bir çıkış olarak seçildiğinde, istendiğinde tooauthorize bir bağlantı tooan varolan Data Lake Store olacaktır.  

![Data Lake Store yetkilendirmek](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Ardından hello Data Lake Store aşağıda görüldüğü gibi çıktı hello özelliklerini doldurun:

![Data Lake Store yetkilendirmek](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Merhaba tabloda hello özellik adları ve Data Lake Store çıktı oluşturmak için gereken bunların açıklaması listelenmektedir.

<table>
<tbody>
<tr>
<td><B>ÖZELLİK ADI</B></td>
<td><B>AÇIKLAMA</B></td>
</tr>
<tr>
<td>Çıkış diğer adları</td>
<td>Bu sorguları toodirect hello sorgu çıktı toothis Data Lake Store kullanılan kolay bir addır.</td>
</tr>
<tr>
<td>Hesap Adı</td>
<td>Merhaba hello Burada, çıktı gönderen Data Lake Storage hesabının adıdır. Bir aşağı açılan listeden Data Lake Store hesaplarını toohello Portalı'nda oturum toowhich hello kullanıcı erişimi ile sunulur.</td>
</tr>
<tr>
<td>Yol önek deseni [<I>isteğe bağlı</I>]</td>
<td>dosya yolu kullanılan toowrite hello dosyalarınızı hello içinde belirtilen Data Lake Store hesabı. <BR>{date} {time}<BR>Örnek 1: klasör1/logs / {date} / {time}<BR>Örnek 2: klasör1/logs / {date}</td>
</tr>
<tr>
<td>Tarih biçimi [<I>isteğe bağlı</I>]</td>
<td>Merhaba bir tarih belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello tarih biçimi seçebilirsiniz. Örnek: YYYY/AA/GG</td>
</tr>
<tr>
<td>Saat biçimi [<I>isteğe bağlı</I>]</td>
<td>Merhaba zaman belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello saat biçimini belirtin. Şu anda HH yalnızca desteklenen hello değerdir.</td>
</tr>
<tr>
<td>Olayı seri hale getirme biçimi</td>
<td>Çıkış verileri seri hale getirme biçimi. JSON, CSV ve Avro desteklenir.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Bir kodlama, CSV veya JSON biçiminde, belirtilmiş olması gerekir. UTF-8 hello kodlama biçimi şu anda yalnızca desteklenir. ' dir.</td>
</tr>
<tr>
<td>sınırlayıcı</td>
<td>Yalnızca, CSV serileştirme için de geçerlidir. Akış analizi, CSV verileri seri hale getirme için bir dizi ortak sınırlayıcıları destekler. Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir.</td>
</tr>
<tr>
<td>Biçimi</td>
<td>Yalnızca JSON serileştirmesi için geçerlidir. Ayrılmış çizgi hello çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir. Dizi hello çıktı bir dizi JSON nesnesi biçimlendirileceğini belirtir.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Data Lake Store yetkilendirmeyi yenileyin
Toore gerekir-Data Lake Store hesabınızın parolasını işinizi oluşturulmuş veya son kimliği doğrulanmış oluşturulmasından sonra değiştirilmişse kimlik doğrulaması.

![Data Lake Store yetkilendirmek](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>SQL Database
[Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) çıkış olarak kendiliğinden ilişkisel veriler için veya ilişkisel bir veritabanında barındırılan içeriğe bağlı uygulamalar için kullanılabilir. Akış analizi işleri tooan var olan tablo bir Azure SQL veritabanı'nda yazacaksınız.  Bu hello tablo şemasını hello alanları ve işinizi çıktısını olan türlerinin tam olarak eşleşmelidir unutmayın. Bir [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) hello (Bu bir önizleme özelliği) SQL veritabanı çıkış seçeneği de aracılığıyla bir çıktı olarak da belirtilebilir. Merhaba tabloda hello özellik adları ve SQL veritabanı çıktı oluşturmak için bunların açıklaması listelenmektedir.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis veritabanında kullanılan kolay bir addır. |
| Database |Burada, Çıkış göndermeyi hello veritabanının Hello adı |
| Sunucu adı |Merhaba SQL veritabanı sunucusu adı |
| Kullanıcı adı |Merhaba erişim toowrite toohello veritabanı olan kullanıcı adı |
| Parola |Merhaba parola tooconnect toohello veritabanı |
| Tablo |Merhaba çıkış yazılacağı hello tablo adı. Merhaba tablo adı büyük/küçük harfe duyarlıdır ve bu tablonun hello şeması tam olarak toohello sayısı alanları ve, iş çıkışı tarafından oluşturulan türlerinin eşleşmesi gerekir. |

> [!NOTE]
> Şu anda hello Azure SQL veritabanı teklifi Stream Analytics işi çıktısında desteklenir. Ancak, bağlı olan bir veritabanı SQL Server çalıştıran bir Azure sanal makine desteklenmiyor. Bu konu toochange sonraki sürümlerde olur.
> 
> 

## <a name="blob-storage"></a>Blob depolama
BLOB storage hello buluta büyük miktarda yapılandırılmamış veriyi depolamak için uygun maliyetli ve ölçeklenebilir bir çözüm sunar.  Azure Blob Depolama ve kullanım giriş için hello belgelerine bakın [nasıl BLOB'ların toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

Merhaba tabloda hello özellik adları ve blob çıktı oluşturmak için bunların açıklaması listelenir.

<table>
<tbody>
<tr>
<td>ÖZELLİK ADI</td>
<td>AÇIKLAMA</td>
</tr>
<tr>
<td>Çıkış diğer adları</td>
<td>Bu sorguları toodirect hello sorgu çıktı toothis blob depolama alanına kullanılan kolay bir addır.</td>
</tr>
<tr>
<td>Depolama Hesabı</td>
<td>Burada, Çıkış göndermeyi hello depolama hesabı Hello adı.</td>
</tr>
<tr>
<td>Depolama hesabı anahtarı</td>
<td>Merhaba depolama hesabıyla ilişkili hello gizli anahtar.</td>
</tr>
<tr>
<td>Depolama kapsayıcısı</td>
<td>Kapsayıcılar hello Microsoft Azure Blob hizmeti depolanan BLOB'lar için mantıksal bir gruplandırmasını sağlar. Blob toohello Blob hizmeti karşıya yüklediğinde, o blob için bir kapsayıcı belirtmeniz gerekir.</td>
</tr>
<tr>
<td>Yol önek deseni [isteğe bağlı]</td>
<td>Merhaba dosya yolu toowrite hello belirtilen kapsayıcı içinde bloblarınızın kullanılır.<BR>Merhaba yol içinde hello BLOB'lar yazılan 2 değişkenleri toospecify hello sıklığı aşağıdaki bir veya daha fazla örneklerini toouse tercih edebilirsiniz:<BR>{date} {time}<BR>Örnek 1: cluster1/logs / {date} / {time}<BR>Örnek 2: cluster1/logs / {date}</td>
</tr>
<tr>
<td>[İsteğe bağlı] tarih biçimi</td>
<td>Merhaba bir tarih belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello tarih biçimi seçebilirsiniz. Örnek: YYYY/AA/GG</td>
</tr>
<tr>
<td>[İsteğe bağlı] saat biçimi</td>
<td>Merhaba zaman belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello saat biçimini belirtin. Şu anda HH yalnızca desteklenen hello değerdir.</td>
</tr>
<tr>
<td>Olayı seri hale getirme biçimi</td>
<td>Çıkış verileri seri hale getirme biçimi.  JSON, CSV ve Avro desteklenir.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Bir kodlama, CSV veya JSON biçiminde, belirtilmiş olması gerekir. UTF-8 hello kodlama biçimi şu anda yalnızca desteklenir. ' dir.</td>
</tr>
<tr>
<td>sınırlayıcı</td>
<td>Yalnızca, CSV serileştirme için de geçerlidir. Akış analizi, CSV verileri seri hale getirme için bir dizi ortak sınırlayıcıları destekler. Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir.</td>
</tr>
<tr>
<td>Biçimi</td>
<td>Yalnızca JSON serileştirmesi için geçerlidir. Ayrılmış çizgi hello çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir. Dizi hello çıktı bir dizi JSON nesnesi biçimlendirileceğini belirtir. Bu dizi hello işi durur veya Stream Analytics toohello sonraki zaman penceresi yalnızca zaman taşındı kapatılacak. Genel olarak, bu dosya hello çıktı hiçbir özel işlem gerektirmez beri ayrılmış JSON hala üzerine yazılan tercih toouse satırıdır.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Olay Hub'ı
[Olay hub'ları](https://azure.microsoft.com/services/event-hubs/) yüksek düzeyde ölçeklenebilir yayımlama-abone olma olay yutucu değil. Saniye başına milyonlarca olayı toplayabilirsiniz.  Akış analizi işi Hello çıktısını başka bir iş akışında hello girişi kullanırken bir olay hub'ı çıktı olarak kullanılır.

Gerekli tooconfigure olay hub'ı veri çıkış olarak akışlarıdır birkaç parametre vardır.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis olay hub'ı kullanılan kolay bir addır. |
| Hizmet veri yolu Namespace |Bir hizmet veri yolu ad alanı, Mesajlaşma varlıkları kümesine ilişkin bir kapsayıcıdır. Yeni bir olay hub'ı oluşturduğunuzda, hizmet veri yolu ad alanı da oluşturmuş |
| Olay Hub'ı |Olay hub'ı çıkışı Hello adı |
| Olay hub'ı ilke adı |Merhaba olay hub'ı yapılandırma sekmesinde oluşturulan hello paylaşılan erişim ilkesi. Her paylaşılan erişim ilkesinin bir ad, ayarladığınız izinler ve erişim anahtarları |
| Olay hub'ı İlkesi anahtarı |Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılan |
| Bölüm anahtarı sütunu [isteğe bağlı] |Bu sütun, olay hub'ı çıkışı için hello bölüm anahtarı içerir. |
| Olayı seri hale getirme biçimi |Çıkış verileri seri hale getirme biçimi.  JSON, CSV ve Avro desteklenir. |
| Encoding |Merhaba, kodlama biçimi yalnızca şu anda desteklenen. UTF-8 CSV ve JSON, içindir |
| sınırlayıcı |Yalnızca, CSV serileştirme için de geçerlidir. Akış Analizi, CSV biçiminde verilerin serileştirilmesi için yaygın olarak kullanılan bazı sınırlayıcıları destekler. Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir. |
| Biçimi |Yalnızca JSON türü için geçerlidir. Ayrılmış çizgi hello çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir. Dizi hello çıktı bir dizi JSON nesnesi biçimlendirileceğini belirtir. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) çıkış olarak bir akış analizi işi tooprovide çözümleme sonuçlarını bir zengin görselleştirme deneyimi için kullanılabilir. Bu özellik, işletimsel panoları, rapor oluşturma ve raporlama güdümlü ölçüm için kullanılabilir.

### <a name="authorize-a-power-bi-account"></a>Power BI hesabınız yetkilendirmek
1. Power BI'hello Azure portalında bir çıkış olarak seçildiğinde şunları yapacaksınız istendiğinde tooauthorize varolan bir Power BI kullanıcı veya toocreate yeni bir Power BI hesabınızın olması.  
   
   ![Power BI kullanıcı yetkilendirme](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Verme henüz bir tane ve şimdi Yetkilendir'i tıklatın, yeni bir hesap oluşturun.  Merhaba aşağıdaki gibi bir ekranı sunulur.  
   
   ![Azure hesabı Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. Bu adımda, hello iş sağlayın veya Okul hesabı hello Power BI çıkışı yetkilendirmek için. Zaten Power BI için kayıtlı değilsiniz, oturum şimdi seçin. Merhaba Power BI için kullandığınız iş veya Okul hesabı hello ile oturum açmış olduğunuz Azure aboneliği hesabı alanından farklı olabilir.

### <a name="configure-hello-power-bi-output-properties"></a>Merhaba Power BI çıktı özelliklerini yapılandırın
Kimliği doğrulanmış hello Power BI hesabınızı edindikten sonra Power BI çıktı için hello özelliklerini yapılandırabilirsiniz. Hello tabloda olduğundan hello özellik adlarının listesi ve bunların açıklama tooconfigure Power BI çıkışı.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis Powerbı çıkış kullanılan kolay bir addır. |
| Grup çalışma |seçebileceğiniz diğer Power BI kullanıcıları ile veri paylaşımı tooenable grupların Power BI içindeki hesap veya toowrite tooa Grup istemiyorsanız "Çalışma Alanım" seçin.  Varolan bir grup güncelleştirme hello Power BI kimlik doğrulamayı yenilemesini gerektirir. |
| Veri kümesi adı |Power BI hello için istendiğini bir veri kümesi adı toouse çıktı sağlayın |
| Tablo adı |Power BI çıktı Merhaba, hello veri kümesi altında bir tablo adı sağlayın. Şu anda Power BI çıkışı akış analizi işleri yalnızca bir tablo bir veri kümesinde olabilir |

Power BI çıkışı ve Pano yapılandırma kılavuz için lütfen hello bakın [Azure akış analizi & Power BI](stream-analytics-power-bi-dashboard.md) makalesi.

> [!NOTE]
> Açıkça hello veri kümesi ve tablo hello Power BI Panonuzda oluşturmayın. Merhaba veri kümesi ve tablo otomatik olarak hello iş başlatıldığında ve hello işini pompa çıkış Power BI'da oturum başlatır doldurulur. Merhaba iş sorgusu üretmez herhangi bir sonuç, hello veri kümesi ve tablo oluşturulmayacak unutmayın. Ayrıca Power BI veri kümesi ve tabloyla zaten sahipse hello hello adıyla aynı biri bu Stream Analytics işinde sağlanan, hello varolan verilerin üzerine yazılacak unutmayın.
> 
> 

### <a name="schema-creation"></a>Şema oluşturma
Bir zaten yoksa, azure Stream Analytics Power BI veri kümesi ve hello kullanıcı adına tablo oluşturur. Diğer durumlarda, yeni değerlerle hello tablosu güncelleştirilir. Şu anda bir hello sınırlaması yoktur, yalnızca bir tablo bir veri kümesi içinde bulunabilir.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>ASA tooPower BI dönüştürme veri türü
Azure Stream Analytics Hello şema değişiklikleri çıktı hello veri modeli çalışma zamanında dinamik olarak güncelleştirir. Sütun adı değişiklikleri, sütun türü değişiklikleri ve hello ekleme veya kaldırma sütunların tüm izlenir.

Bu tablo hello veri türü dönüştürmelerini gelen kapsar [Stream Analytics veri türleri](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [varlık veri modeli (EDM) türleri](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) POWER BI veri kümesi ve tablo yoksa.


Akış analizi | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | Dize
Tarih saat | Tarih saat
Kayan nokta | Çift
Kayıt dizisi | Türü, sabit değer "IRecord" veya "IArray" dize

### <a name="schema-update"></a>Şema güncelleştirmesi
Akış analizi hello veri modeli şeması hello çıkış olayları ilk dizi hello göre oluşturur. Daha sonra gerekirse, hello veri modeli schema hello özgün şemasına uygun değildir güncelleştirilmiş tooaccommodate gelen olayları'dır.

Merhaba `SELECT *` sorgu kaçınılmalıdır satırlar boyunca tooprevent dinamik şema güncelleştirmesi. Ayrıca toopotential performans etkileri de hello sonuçları için harcanan hello süre indeterminacy neden. Power BI Panosu üzerinde gösterilen toobe gereken hello alanları tam seçilmelidir. Ayrıca, hello veri değerleri veri türü seçilen hello ile uyumlu olması gerekir.


Önceki/geçerli | Int64 | Dize | Tarih saat | Çift
-----------------|-------|--------|----------|-------
Int64 | Int64 | Dize | Dize | Çift
Çift | Çift | Dize | Dize | Çift
Dize | Dize | Dize | Dize |  | Dize | 
Tarih saat | Dize | Dize |  Tarih saat | Dize


### <a name="renew-power-bi-authorization"></a>Power BI yetkilendirmeyi yenileyin
Toore gerekir-parolasını işinizi oluşturulmuş veya son kimliği doğrulanmış oluşturulmasından sonra değiştirilmişse Power BI hesabınızı kimlik doğrulaması. Çok faktörlü kimlik doğrulama (MFA), Azure Active Directory (AAD) Kiracı yapılandırılmışsa toorenew Power BI yetkilendirme 2 haftada de gerekir. Bu sorun belirtisi hiçbir iş çıktısı ve "kimlik doğrulama kullanıcı hatayla" Merhaba işlem günlükleri şöyledir:

  ![Power BI yenileme belirteci hata](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve Bu sorun, çalışan bir işi durdurmak ve tooyour Power BI çıkışı gidin.  Merhaba "Yenileme yetkilendirme" bağlantısına tıklayın ve hello son durdurulma zamanı tooavoid veri kaybı gelen işi yeniden başlatın.

  ![Power BI yenileme yetkilendirme](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Tablo Depolama
[Azure Table storage](../storage/common/storage-introduction.md) bir uygulamayı otomatik olarak toomeet kullanıcı talebine ölçeklendirmek yüksek oranda kullanılabilir, yüksek düzeyde ölçeklenebilir depolama sunar. Table storage hangisinin daha az kısıtlamalar hello şema ile yapılandırılmış veri için yararlanabilirsiniz Microsoft'un NoSQL anahtar/öznitelik deposudur. Azure Table storage Kalıcılık ve verimli alımı için kullanılan toostore veriler olabilir.

Merhaba tabloda hello özellik adlarının ve tablo çıktısı oluşturmak için bunların açıklaması listelenmektedir.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis tablo depolama alanına kullanılan kolay bir addır. |
| Depolama Hesabı |Burada, Çıkış göndermeyi hello depolama hesabı Hello adı. |
| Depolama hesabı anahtarı |Merhaba erişim tuşu Hello depolama hesabıyla ilişkilendirilmiş. |
| Tablo adı |Merhaba tablonun Hello adı. henüz yoksa hello tablosu oluşturulur. |
| Bölüm anahtarı |Merhaba çıkış sütunu içeren hello bölüm anahtarı Hello adı. Merhaba bölüm anahtarı hello bölüm bir varlığın birincil anahtarının ilk kısmı hello forms belirli bir tablodaki içinde benzersiz tanımlayıcısıdır. Too1 KB boyutunda yukarı olabilir bir dize değeridir. |
| Satır anahtarı |Merhaba çıkış sütunu içeren hello satır anahtarını Hello adı. Hello satır anahtarını belli bir bölüm içinde bir varlık için benzersiz bir tanımlayıcı değil. Bir varlığın birincil anahtarının hello ikinci bölümü oluşturur. Merhaba satır anahtarını too1 KB boyutunda yukarı olabilen bir dize değeridir. |
| Toplu iş boyutu |Merhaba toplu işlemi için kayıt sayısı. Genellikle hello varsayılan çoğu işleri için yeterliyse toohello başvuran [tablo toplu işlem spec](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) bu ayarını değiştirme hakkında daha fazla ayrıntı için. |

## <a name="service-bus-queues"></a>Service Bus Kuyrukları
[Hizmet veri yolu kuyrukları](https://msdn.microsoft.com/library/azure/hh367516.aspx) bir ilk olarak, ilk çıkar (FIFO) ileti teslim tooone veya birden çok rakip tüketiciye sunar. Genellikle, iletileri alınan ve hangi toohello sıraya eklendi ve her ileti alındı ve tek bir ileti tüketicisi tarafından alınıp hello zamana bağlı düzende hello alıcılar tarafından işlenen beklenen toobe edilir.

Merhaba tabloda hello özellik adları ve sıra çıktı oluşturmak için bunların açıklaması listelenmektedir.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis hizmet veri yolu kuyruğu kullanılan kolay bir addır. |
| Hizmet veri yolu Namespace |Bir hizmet veri yolu ad alanı, Mesajlaşma varlıkları kümesine ilişkin bir kapsayıcıdır. |
| Kuyruk adı |Hizmet veri yolu kuyruğu hello Hello adı. |
| Sıra ilke adı |Kuyruk oluşturduğunuzda, hello kuyruk yapılandırma sekmesinde paylaşılan erişim ilkeleri de oluşturabilirsiniz. Her paylaşılan erişim ilkesinin bir ad, ayarladığınız izinler ve erişim anahtarları. |
| Sıra ilke anahtarı |Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılan |
| Olayı seri hale getirme biçimi |Çıkış verileri seri hale getirme biçimi.  JSON, CSV ve Avro desteklenir. |
| Encoding |Merhaba, kodlama biçimi yalnızca şu anda desteklenen. UTF-8 CSV ve JSON, içindir |
| sınırlayıcı |Yalnızca, CSV serileştirme için de geçerlidir. Akış Analizi, CSV biçiminde verilerin serileştirilmesi için yaygın olarak kullanılan bazı sınırlayıcıları destekler. Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir. |
| Biçimi |Yalnızca JSON türü için geçerlidir. Ayrılmış çizgi hello çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir. Dizi hello çıktı bir dizi JSON nesnesi biçimlendirileceğini belirtir. |

## <a name="service-bus-topics"></a>Service Bus Konuları
Hizmet veri yolu kuyrukları gönderen tooreceiver, tek bir tooone iletişim yönteminden sunarken [Service Bus konu başlıklarına](https://msdn.microsoft.com/library/azure/hh367516.aspx) bir-çok form iletişim sağlar.

Merhaba tabloda hello özellik adlarının ve tablo çıktısı oluşturmak için bunların açıklaması listelenmektedir.

| Özellik adı | Açıklama |
| --- | --- |
| Çıkış diğer adları |Bu sorguları toodirect hello sorgu çıktı toothis hizmet veri yolu konusu kullanılan kolay bir addır. |
| Hizmet veri yolu Namespace |Bir hizmet veri yolu ad alanı, Mesajlaşma varlıkları kümesine ilişkin bir kapsayıcıdır. Yeni bir olay hub'ı oluşturduğunuzda, hizmet veri yolu ad alanı da oluşturmuş |
| Konu adı |Konular, varlıklar, benzer tooevent hub'ları ve kuyrukları Mesajlaşma varlıklarıdır. Bunlar, bir dizi farklı cihaz ve Hizmetleri tasarlanmış toocollect olay akışlardan demektir. Bir konu oluşturduğunuzda, ayrıca belirli bir ad verilir. Merhaba iletileri gönderilen bir abonelik yapılandırılmadığı sürece tooa konu kullanılabilir olmaz, bu nedenle olun hello konu altında bir veya daha fazla abonelik |
| Konu ilke adı |Bir konu oluşturduğunuzda, hello konu yapılandırma sekmesinde paylaşılan erişim ilkeleri de oluşturabilirsiniz. Her paylaşılan erişim ilkesinin bir ad, ayarladığınız izinler ve erişim anahtarları |
| Konu ilke anahtarı |Merhaba paylaşılan erişim anahtarı tooauthenticate erişim toohello Service Bus ad alanı kullanılan |
| Olayı seri hale getirme biçimi |Çıkış verileri seri hale getirme biçimi.  JSON, CSV ve Avro desteklenir. |
| Encoding |Bir kodlama, CSV veya JSON biçiminde, belirtilmiş olması gerekir. Merhaba, kodlama biçimi yalnızca şu anda desteklenen. UTF-8 dir |
| sınırlayıcı |Yalnızca, CSV serileştirme için de geçerlidir. Akış Analizi, CSV biçiminde verilerin serileştirilmesi için yaygın olarak kullanılan bazı sınırlayıcıları destekler. Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) sorgu ve işlemleri şemasız verileri, tahmin edilebilir ve güvenilir performans ve hızlı geliştirme sunan bir tam olarak yönetilen NoSQL belge veritabanı hizmetidir.

Merhaba listesi ayrıntıları hello özellik adları ve bir Azure Cosmos DB çıktı oluşturmak için bunların açıklaması aşağıda.

* **Diğer ad çıktı** – Bu çıktı ASA sorgunuzda bir diğer ad toorefer  
* **Hesap adı** – hello adı veya bitiş noktası hello Cosmos DB hesap URI'si.  
* **Anahtar hesap** – hello Cosmos DB hesap hello paylaşılan erişim anahtarı.  
* **Veritabanı** – hello Cosmos DB veritabanı adı.  
* **Koleksiyon adı deseni** – hello koleksiyon adı ya da kullanılan hello koleksiyonları toobe için kendi deseni. Merhaba koleksiyon adı biçimi, burada bölümlerin 0'dan başlar hello isteğe bağlı {partition} belirteci kullanılarak oluşturulabilir. Örnek geçerli girişler şunlardır:  
  1\) MyCollection – "MyCollection" adlı bir koleksiyon bulunmalıdır.  
  2\) – böyle koleksiyonları bulunmalıdır – MyCollection {partition} "MyCollection0", "MyCollection1", "MyCollection2" ve benzeri.  
* **Anahtar bölüm** – isteğe bağlıdır. Bu, yalnızca, koleksiyon adı deseni {bölümlendirmesini} belirteci kullanıyorsanız gereklidir. çıkışın koleksiyonlar üzerinde bölümlenmesine için çıktı kullanılan olayları toospecify hello anahtar hello alanında Hello adı. Tek koleksiyon çıktı için herhangi bir rastgele çıkış sütunu olabilir örneğin PartitionID kullanılır.  
* **Belge Kimliği** – isteğe bağlıdır. hangi ekleme veya güncelleştirme işlemleri dayalı toospecify hello birincil anahtar kullanılan çıkış olaylarındaki alanın hello Hello adı.  


## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
Sunulan tooStream Analytics, hello nesnelerin interneti verilerini analytics akış için yönetilen bir hizmet olan. Bu hizmet hakkında daha fazla toolearn bakın:

* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
