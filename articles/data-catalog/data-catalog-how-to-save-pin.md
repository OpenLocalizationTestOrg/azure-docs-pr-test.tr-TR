---
title: "aaaSave arar ve Azure veri Kataloğu'nda PIN veri varlıkları | Microsoft Docs"
description: "Veri kaynakları ve daha sonra kullanmak için veri varlıklarını kaydetme nasıl tooarticle vurgulama yetenekleri Azure veri Kataloğu'nda."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Azure veri Kataloğu'nda arama ve PIN veri varlıklarını kaydetme
## <a name="introduction"></a>Giriş
Azure veri Kataloğu, veri kaynağı bulma için yetenekleri sağlar. Hızlı bir şekilde arayın ve da hello katalog toolocate veri kaynakları filtre ve amaçlarının, elinizdeki hello işi için daha kolay toofind hello doğru verilerin sağlama anlama.

Ancak tooregularly ihtiyacınız yoksa ne hello ile aynı iş veri? Ve ne sizin ve diğer kullanıcıların düzenli olarak bilgi toohello katkıda hello katalog aynı veri kaynaklarında? Bu durumda, aynı hello toorepeatedly sorun yaşıyor aramaları verimsiz olabilir. Kayıtlı arama ve sabitlenmiş veri varlıkları olduğu yardımcı olabilir budur.

## <a name="saved-searches"></a>Kaydedilen aramalar
Veri Kataloğu'nda kaydedilmiş bir aramayı bir yeniden kullanılabilir, kullanıcı başına arama tanımıdır. Arama terimleri, etiketler ve diğer filtreleri gibi bir arama tanımlamak ve kaydedin. Kaydedilen hello arama tanımı yeniden çalıştırabilirsiniz sonraki tooreturn kendi arama ölçütleriyle eşleşen hiçbir veri varlıklarını.

### <a name="create-a-saved-search"></a>Kaydedilmiş bir aramayı oluşturma
toocreate kaydedilmiş bir aramayı hello aşağıdaki:
1. Hello Azure veri Kataloğu portalında, hello **geçerli aramayı** penceresinde tıklatın **kaydetmek**. 

    ![Geçerli arama ayarları Kaydet bağlantısı](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Tooreuse istediğiniz ve ardından hello arama ölçütlerini girin **kaydetmek**.

    ![Kaydedilen arama adı geçerli arama ayarları](./media/data-catalog-how-to-save-pin/02-name.png)

3. İstendiğinde, kaydedilmiş aramayı hello için bir ad girin. Anlamlı bir ad seçin ve hello araması tarafından döndürülen hello veri varlıklarını açıklar.

### <a name="manage-saved-searches"></a>Kaydedilmiş aramaları Yönet
Bir veya daha fazla aramalar, kaydettiğiniz sonra bir **kayıtlı aramaları** seçeneği hello altında görüntülenen **geçerli aramayı** kutusu. Merhaba listesi genişletildiğinde tüm kaydedilmiş aramaları görüntülenir.

 ![Kaydedilmiş aramaları listesi](./media/data-catalog-how-to-save-pin/03-list.png)

Merhaba aşağıdakilerden birini yapın:

* bir arama tooexecute kaydedilmiş bir aramayı hello listesinde seçin.

* tooview kaydedilmiş bir aramayı Yönetimi seçeneklerinin listesi hello aşağı ok sonraki toohello arama adını tıklatın.

    ![Kaydedilmiş aramaları yönetmek için Seçenekler](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter hello kaydedilen arama için yeni bir ad seçin **yeniden adlandırma**. Merhaba arama tanımı değiştirilmez.

* tooremove hello kaydedilen arama seçin, listeden **silmek**ve ardından hello silme işlemini onaylayın.

* toomark hello kaydedilen arama seçin, varsayılan arama olarak **varsayılan olarak Kaydet**. "Boş" arama hello Azure veri Kataloğu giriş sayfasından gerçekleştirirseniz, varsayılan aramanızı yürütülür. Ayrıca, hello varsayılan arama hello hello üst kısmında görüntülenir olarak işaretlenen arama hello **kayıtlı aramaları** listesi.

### <a name="organizational-saved-searches"></a>Kuruluş Kaydedilmiş aramaları
Kuruluşunuzdaki tüm kullanıcı kendi kullanmak için aramaları kaydedebilirsiniz. Veri Kataloğu yöneticilerinin hello kuruluşunuzdaki tüm kullanıcılar için aramaları da kaydedebilirsiniz. Yöneticiler bir aramayı kaydettiğinizde, bunlar ile sunulan bir **paylaşımı hello şirket içinde** seçeneği. Bu seçenek paylaşımları hello kaydedilmiş hello kuruluşunuzdaki tüm kullanıcılar için arama seçme.

 ![Kuruluş Kaydedilmiş aramaları](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Sabitlenmiş veri varlıklarını
Kaydedilmiş aramaları ile kaydedebilir ve arama tanımları yeniden kullanabilirsiniz. Merhaba aramaları tarafından döndürülen hello veri varlıklarını hello katalog değişiklik Merhaba içeriğine olarak zaman içinde değişebilir. Veri varlıklarını PIN ne zaman, belirli veri varlıklarını toomake açıkça tanımlayabilirsiniz bunları toouse arama gerek olmadan daha kolay tooaccess.

Bir veri varlığına sabitleme basittir. tooadd hello veri varlık sabitlenmiş tooyour listesi, yalnızca tıklattığınız hello **PIN** simgesi. Merhaba simgesi hello köşesine hello varlık hello döşeme görünümünü ve hello en solundaki sütun hello Azure veri Kataloğu portalında hello liste görünümünde görüntülenir.

![Merhaba veri varlığına PIN simgesi](./media/data-catalog-how-to-save-pin/05-pinning.png)

Bir veri varlığına kaldırıldığında eşit olarak açıktır. Merhaba tıklamanız yeterlidir **sabitleme** hello seçili varlık için simge tootoggle hello ayarı.

![Merhaba veri varlığına sabitleme simgesi](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Merhaba My varlıklar bölümü
Merhaba veri Kataloğu portalı giriş sayfasını içeren bir **My varlıklar** ilgi toohello geçerli kullanıcının varlıklar görüntüler bölümü. Bu bölümde her iki sabitlenmiş varlıkları içerir ve kayıtlı aramalar.

![Merhaba hello giriş sayfasındaki My varlıklar bölümü](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Özet
Azure veri Kataloğu sizin ve diğer kuruluş üyelerinin verileri ve daha fazla süre ile çalışmak için arayan daha az süre beklemesini, böylece daha kolay toodiscover hello veri kaynakları ihtiyacınız olun yetenekleri sağlar. Kayıtlı aramalar ve kullanıcılar ile art arda çalıştıkları veri kaynaklarını kolayca tanıyacak şekilde varlıklar bu çekirdek özellikler yapı veri sabitlenir.
