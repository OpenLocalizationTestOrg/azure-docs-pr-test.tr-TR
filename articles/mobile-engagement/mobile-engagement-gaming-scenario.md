---
title: "Oyun uygulaması için aaaAzure Mobile Engagement uygulaması"
description: "Oyun uygulaması senaryosu tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Oyun uygulaması ile Mobile Engagement uygulama
## <a name="overview"></a>Genel Bakış
Oyun başlatma yeni bir temel Balıkçılık role play/stratejisi oyun uygulaması sunmuştur. Merhaba oyun 6 ay için hazır ve çalışır olmuştur. Bu oyun büyük bir başarı ve yüklemeleri milyonlarca sahiptir ve hello bekletme çok yüksek karşılaştırılan tooother başlatma oyun uygulamaları. Merhaba üç aylık gözden geçirme toplantı adresindeki Paydaşlar (ARPU) kullanıcı başına ortalama gelir tooincrease ihtiyaç duydukları kabul etmiş olursunuz. Premium oyun paketlerin özel teklifler kullanılabilir. Bu oyun paketleri hello oyunda kullanıcılar tooupgrade hello görünümünü ve bunların Balıkçılık satırları ve lures veya tackles performansını izin verir. Bununla birlikte, paket satış çok düşük. Bunlar karar vermek için ilk tooanalyze hello Müşteri Deneyimi analiz aracı ile ve ardından bir katılım programı tooincrease satış kullanarak toodevelop kesimleme Gelişmiş.

Merhaba üzerinde temel [Azure Mobile Engagement - en iyi yöntemlerle Başlangıç Kılavuzu](mobile-engagement-getting-started-best-practices.md) bir katılım stratejisi oluşturmaya.

## <a name="objectives-and-kpis"></a>Hedefleri ve KPI'leri
Önemli katılımcılara hello oyun karşılamak için. Tüm bir ana hedef - % 15 göre tooincrease premium paket satış üzerinde kabul ediyorum. Bu amaç iş anahtar performans göstergelerini (KPI'lar) toomeasure ve sürücü oluşturun

* Merhaba oyun hangi düzeyde, bu paketleri satın alınan?
* Kullanıcı başına, oturumu başına, haftalık ve aylık hello gelir nedir?
* Merhaba sık kullanılan satın alma türleri nelerdir?

Merhaba 1 parçası [Başlarken Kılavuzu](mobile-engagement-getting-started-best-practices.md) toodefine nasıl hello hedefler ve KPI'ler açıklar. 

İş KPI'leri şimdi tanımlanan hello ile katılım KPI'leri toodetermine yeni kullanıcı eğilimlerini ve saklama başlangıç mobil ürün Yöneticisi oluşturur.

* İzleme bekletme ve aralıklarını aşağıdaki hello arasında kullanın: her gün, 2 günde, haftalık, aylık ve 3 ayda
* Etkin kullanıcı sayısı
* Merhaba Hello uygulama derecesi depolama

Merhaba BT Ekibi önerilerine dayalı olarak, hello teknik KPI'ları aşağıdaki soruları aşağıdaki tooanswer hello eklendi:

* My kullanıcı yolu nedir (hangi sayfasını ziyaret, ne kadar zaman kullanıcılar harcamanız üzerinde)
* Kilitlenme veya oturum başına karşılaşılan hataların sayısı
* İşletim sistemi sürümleri çalıştıran Kullanıcılarım nelerdir?
* Kullanıcılarım için ekranın hello ortalama boyutu nedir?
* Ne tür bir internet bağlantısı Kullanıcılarım var mı?

Her KPI için ihtiyaç duyacağı ve kendi playbook nerede hello veri hello mobil ürün Yöneticisi belirtir.

## <a name="engagement-program-and-integration"></a>Katılım programı ve tümleştirme
Gelişmiş katılım programı oluşturulmadan önce hello mobil proje Director hello proje sorumlu nasıl ve ne zaman ürünleri hello kullanıcılar tarafından tüketilen'ın derin bir anlayış olmalıdır.

3 ay sonra kendi uygulama anında iletme bildirimi satış yeterli veri tooenhance hello mobil proje Director topladı. Hüseyin, öğrenir:

* Merhaba ilk satın alma genellikle 14 hello düzeyinde gerçekleşir. Bu gibi durumlarda için % 90'ını, hello satınalma yeni efsanevi Silahlar için 3'dır.
* % 80 bu örneklerinin hello ürünle devam etmek ve daha fazla olun bir satın alma, yaptığınız kullanıcılar satın alır.
* Merhaba düzeyi 20 geçtiğinde, 10/hafta birden çok toospend Başlat kullanıcılar.
* Kullanıcılar, 16, 24 ve 32 düzeyinde toobuy premium paketleri eğilimi gösterir.

Merhaba mobil proje Director toocreate belirli anında iletme bildirimi dizileri tooincrease uygulama satış karar toothis analiz teşekkür eder. Halil, kendisine çağıran üç anında iletme sıralarını oluşturur: program, satış programı ve etkin olmayan programı'na Hoş Geldiniz. Daha fazla bilgi için toohello başvurun [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
