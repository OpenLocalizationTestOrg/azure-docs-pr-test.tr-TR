---
title: "aaaMicrosoft Power BI Embedded - bağlanan tooa veri kaynağı"
description: "Power BI Embedded, toodata kaynaklarına bağlanın"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Tooa veri kaynağına bağlanma
İle **Power BI Embedded**, raporlar, kendi uygulamanıza eklenebilir. Power BI raporu uygulamanıza bulunmadığında, arka plandaki tarafından veri toohello hello rapor bağlanır **alma** hello veri ya da bir kopyasını **doğrudan bağlanma** toohello veri kaynağını kullanan  **DirectQuery**.

Kullanarak arasındaki farklar hello işte **alma** ve **DirectQuery**.

| İçeri Aktarma | DirectQuery |
| --- | --- |
| Tablolar, sütunlar *ve veri* içeri aktarılan veya hello raporun kümesine kopyalar. toosee bu oluştu toohello temel alınan veriler değiştiğinde, yenileme veya alma, bir tam, güncel veri kümesini yeniden. |Yalnızca *tablolar ve sütunlar* içeri aktarılan veya hello raporun kümesine kopyalar. Her zaman hello en güncel verileri görüntülediğiniz. |

Power BI Embedded ile DirectQuery bulut veri kaynaklarıyla kullanabilirsiniz, ancak veri kaynakları şu anda şirket içi değil.

> [!NOTE]
> Merhaba şirket içi veri ağ geçidi Power BI Embedded ile şu anda desteklenmiyor. Bu, şirket içi veri kaynakları ile DirectQuery kullanamayacağınız anlamına gelir.

## <a name="supported-data-sources"></a>Desteklenen veri kaynakları

**DirectQuery**
* Azure SQL veritabanı
* Azure SQL Veri Ambarı

**İçeri Aktarma**

Tüm hello kullanılabilir veri kaynaklarını Power BI Desktop içinde kullanarak içeri aktarabilirsiniz. Şunları yapacaksınız **değil** mümkün toorefresh Power BI Embedded içinde bu verileri olabilir. Tooupload değişiklikleri olacaktır tooyour PBIX dosyası tooPower BI Embedded. Bu toono kullanılabilir ağ geçididir. 

## <a name="benefits-of-using-directquery"></a>DirectQuery kullanmanın yararları
İki birincil avantajları vardır kullanırken **DirectQuery**:

* **DirectQuery** sağlar, yapı görselleştirmeleri Burada, aksi takdirde olacaktır unfeasible toofirst alma çok büyük veri kümeleri üzerinde tüm veri hello.
* Veri değişikliklerini temel alınan veri yenileme gerektirebilir ve bazı raporlar için hello toodisplay geçerli verileri büyük veri aktarımları, yeniden içeri aktarılmasını verilerin unfeasible sağlama gerektirebilir. Bunun aksine, **DirectQuery** raporları her zaman güncel verileri kullanın.

## <a name="limitations-of-directquery"></a>DirectQuery sınırlamaları
   Bazı sınırlamalar toousing vardır **DirectQuery**:

* Tüm tablolar tek bir veritabanından gelmelidir.
* Merhaba sorgu fazla karmaşık olması durumunda bir hata ortaya çıkar. en az karmaşık olacak şekilde tooremedy hello hata, hello sorgu yeniden düzenlemeniz gerekir. Merhaba sorgu karmaşık olması gerekiyorsa kullanmak yerine tooimport hello verilere ihtiyaç duyarsınız **DirectQuery**.
* İlişki filtreleme, her iki yönde yerine sınırlı tooa tek yön olur.
* Merhaba bir sütunun veri türünü değiştiremezsiniz.
* Varsayılan olarak, sınırlamalar ölçüler izin DAX ifadeleri yerleştirilir. Bkz: [DirectQuery ve ölçüleri](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery ve ölçüleri
kabul edilebilir performans toohello veri kaynağındaki gönderilen tooensure sorguların vardır, sınırlamalar ölçüler üzerinde uygulanmaz. Kullanırken **Power BI Desktop**, Gelişmiş kullanıcılar seçebilirsiniz toobypass bu sınırlamaya seçerek **Dosya > Seçenekler ve Ayarlar > Seçenekler**. Merhaba, **seçenekleri** iletişim kutusunda, seçin **DirectQuery**ve hello seçeneğini belirleyin **DirectQuery modunda Kısıtlanmamış ölçümlere izin**. Bu seçenek belirlendiğinde, bir ölçü için geçerli olan herhangi bir DAX ifade kullanılabilir. Kullanıcıların farkında olması gerekir; Ancak, hello verileri içe aktarıldığında bazı ifadeleri, çok iyi gerçekleştireceğini çok yavaş sorguları toohello arka neden olabilir, kaynağı **DirectQuery** modu. 

## <a name="see-also"></a>Ayrıca Bkz.
* [Microsoft Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

