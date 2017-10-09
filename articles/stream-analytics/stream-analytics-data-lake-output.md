---
title: "aaaStream Analytics veri Gölü deposu çıkış | Microsoft Docs"
description: "Kimlik doğrulama ve yetkilendirme Stream Analytics işi bir Azure Data Lake Store'da ve yapılandırma"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Stream Analytics Data Lake Store çıktı
Akış analizi işleri birkaç çıktı yöntemlerini destekleyen bir anda bir [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Azure Data Lake Store, büyük veri analitik iş yükleri için kuruluş çapında hiper ölçekli bir depodur. Data Lake Store işletimsel ve keşifsel analiz herhangi boyutu, türü ve alım hızına toostore veri sağlar.

## <a name="authorize-a-data-lake-store-account"></a>Bir Data Lake Store hesabı yetki
1. Data Lake Store'hello Azure portalında bir çıkış olarak seçildiğinde istenir varolan Data Lake Store veya toorequest tooauthorize kullanımı toohello Data Lake Store'a hello Klasik Portal üzerinden erişim.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Zaten varsa tooData Lake Store'a erişmek, "Şimdi Yetkilendir"'i tıklatın ve bir sayfa kısa bir süre için pop "Yeniden yönlendirmek tooauthorization" belirten ayarlama. Başlangıç sayfası otomatik olarak kapanır ve tooconfigure hello Data Lake Store çıkış belirleyebilmesini hello sayfasıyla sunulur.

Data Lake Store için kaydolmadıysanız, hello "şimdi kaydolun" bağlantı tooinitiate hello isteği izleyin, veya hello izleyin [başlatılan yönergeleri almak](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Merhaba Data Lake Store çıktı özelliklerini yapılandırın
Kimliği doğrulanmış hello Data Lake Store hesabına sahip olduğunda, Data Lake Store çıktı için hello özelliklerini yapılandırabilirsiniz. Merhaba tabloda hello özellik adları ve Data Lake Store çıktı kendi açıklama tooconfigure listesidir.

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
<td>Data Lake Store hesabı</td>
<td>Burada, Çıkış göndermeyi hello depolama hesabı Hello adı. Kullanıcı oturum hello erişimi Data Lake Store hesapları listesiyle birlikte sunulur.</td>
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

## <a name="renew-data-lake-store-authorization"></a>Data Lake Store yetkilendirmeyi yenileyin
Şu anda, burada hello kimlik doğrulama belirteci el ile 90 günde Data Lake Store çıktıyla tüm işleri yenilenir toobe gereken bir sınırlama yoktur. Toore de gerekir-işinizi oluşturulmuş veya son kimliği doğrulanmış yana parolanızı değiştirdiyseniz Data Lake Store hesabınızın kimlik doğrulaması. Bu sorun belirtisi hiçbir iş çıktısı ve hello işlem günlükleri'ni yeniden yetkilendirme gereksinimini belirten bir hata var.

tooresolve Bu sorun, çalışan bir işi durdurmak ve tooyour Data Lake Store çıktı gidin. Merhaba "Yenileme yetkilendirme" bağlantısına tıklayın ve bir sayfa kısa bir süre için "Yeniden yönlendirmek tooauthorization.." belirten yukarı pop. Başlangıç sayfası otomatik olarak kapatılacak ve başarılı olursa, "Yetkilendirme başarıyla yenilendi" gösterir. Ardından tooclick "Kaydet" Merhaba hello sayfa sonunda ve gerekir, hello son durdurulma zamanı tooavoid veri kaybı işten başlatarak devam edebilirsiniz.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

