---
title: "aaaAzure SQL veritabanını dinamik veri maskeleme | Microsoft docs"
description: "SQL veritabanı dinamik veri maskeleme toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar."
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>SQL veritabanı dinamik veri maskeleme

SQL veritabanı dinamik veri maskeleme toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar. 

Dinamik veri maskeleme yardımcı olan müşteriler toodesignate etkinleştirerek yetkisiz erişim toosensitive verilerin engellemek hello hassas verileri tooreveal hello uygulama katmanı üzerinde en az etkiyle ne kadarının. Bunu hello verileri hello veritabanında değişip değişmediğini sırada, belirlenen veritabanı alanları hello hassas verileri sorgu hello sonuç kümesinde gizler ilke tabanlı güvenlik özelliğidir.

Örneğin, bir çağrı merkezinde bir temsilcisiyle arayanlar kendi kredi kartı numarası birkaç haneli tanımlayabilir, ancak toohello temsilcisiyle öğeleri tam olarak olmamalıdır bu verilerin açığa. Tüm maskeleri ancak hello herhangi bir kredi kartı numarası hello sonuç kümesindeki herhangi bir sorgu dört rakamı son bir maskeleme kuralı tanımlanabilir. Bir geliştirici uyumluluk düzenlemeleri ihlal etmeden sorun giderme amacıyla üretim ortamlarında sorgulayabilmesi başka bir örnek olarak, uygun veri maskesi tanımlı tooprotect kişisel bilgileri (PII) verileri olabilir.

## <a name="sql-database-dynamic-data-masking-basics"></a>SQL veritabanı dinamik veri maskeleme temelleri
Dinamik veri maskeleme hello ilkesinde Azure portal hello dinamik veri maskeleme işlemi SQL veritabanı yapılandırma dikey veya ayarları dikey penceresini seçerek ayarlarsınız.

### <a name="dynamic-data-masking-permissions"></a>Dinamik veri maskeleme izinleri
Dinamik veri maskeleme hello Azure veritabanı yöneticisi, sunucu yöneticisi veya güvenlik yetkilisi rolleri tarafından yapılandırılabilir.

### <a name="dynamic-data-masking-policy"></a>Dinamik veri maskeleme İlkesi
* **Maskeleme işlemi için hariç tutulan SQL kullanıcıları** - kümesi SQL kullanıcılarının veya hello SQL maskelenmemiş Veri Al AAD kimlikleri sorgu sonuçları. Yönetici ayrıcalıklarına sahip kullanıcılar maskeleme işlemi her zaman hariç tutulur ve herhangi bir maskesi olmadan hello özgün veriler bakın.
* **Kuralları maskeleme** -Maskelenmiş alanları toobe belirlenmiş hello ve maskeleme kullanılan işlevi hello tanımlayan kuralları kümesi. alanları belirlenmiş hello veritabanı şema adı, tablo adını ve sütun adı kullanılarak tanımlanabilir.
* **İşlevler maskeleme** -bir dizi farklı senaryolar için veri hello riskini kontrol yöntem.

| Maskeleme işlevi | Maskeleme mantığı |
| --- | --- |
| **Varsayılan** |**Tam according toohello veri maskeleme hello türlerini belirlenmiş alanları**<br/><br/>• Kullanım XXXX veya hello alan hello boyutu 4'ten az karakter dizesi veri türleriyle (nchar, ntext, nvarchar) için ise daha az Xs.<br/>• (Bigint, bit, ondalık, int, para, sayısal, smallint, küçük para, Mini tamsayı, kayan nokta, gerçek) sayısal veri türleri için sıfır değeri kullanın.<br/>• 01-01-1900 tarih/saat veri türleri (tarihi, datetime2, datetime, datetimeoffset, smalldatetime, saat) kullanın.<br/>• SQL variant hello varsayılan değer hello geçerli türü için kullanılır.<br/>• XML hello belge için <masked/> kullanılır.<br/>• Özel veri türleri için boş bir değer kullanın (zaman damgası tablo, hierarchyid, GUID, ikili, görüntü, değişken ikili uzamsal türler). |
| **Kredi kartı** |**En son dört rakamı alanları belirlenmiş hello hello sunan yöntemi maskeleme** ve kredi kartı hello biçiminde öneki olarak bir sabit dize ekler.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **E-posta** |**Merhaba ilk harfi gösterir ve hello etki alanı ile XXX.com değiştirir yöntemi maskeleme** bir sabit dize öneki hello biçiminde bir e-posta adresi kullanarak.<br/><br/>aXX@XXXX.com |
| **Rastgele sayı** |**Rastgele bir sayı oluşturur yöntemi maskeleme** toohello according seçili sınırları ve gerçek veri türleri. Ardından maskeleme işlevi hello sınırları belirlenmiş hello eşitse, sabit bir sayıdır.<br/><br/>![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Özel metin** |**Hangi açığa çıkarır hello ilk ve son karakter yöntemi maskeleme** ve bir özel doldurma dize hello ortadaki ekler. Merhaba özgün dizeye kullanıma sunulan hello önek ve sonek kısa ise yalnızca dize doldurma hello kullanılır. <br/>önek [doldurma] sonek<br/><br/>![Gezinti Bölmesi](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Önerilen alanlar toomask
Merhaba DDM önerileri altyapısı bayraklar veritabanınızdan belirli alanları maskeleme için iyi adaylar olabilir olası hassas alanları olarak. Merhaba dinamik veri maskeleme dikey penceresinde hello Portalı'nda, sütunları veritabanınız için önerilen hello görürsünüz. Tek toodo ihtiyacınız olan tıklatın **Maskesi Ekle** bir veya daha fazla sütun için ve ardından **kaydetmek** tooapply bu alanlar için bir maske.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Dinamik veri maskeleme Powershell cmdlet'lerini kullanarak, veritabanınız için ayarlama
Bkz: [Azure SQL veritabanı cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>REST API kullanarak veritabanınız için dinamik veri maskeleme ayarlama
Bkz: [işlemleri Azure SQL veritabanları için](https://msdn.microsoft.com/library/dn505719.aspx).

