---
title: "Azure veri Kataloğu'nda yönetilen etiketleme için hello iş sözlüğünü ayarlama aaaSet | Microsoft Docs"
description: "Kayıtlı veri varlıklarını nasıl tooarticle vurgulama hello iş sözlüğünü tanımlama ve ortak iş sözlüğünü tootag kullanmak için Azure veri Kataloğu'nda."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Merhaba iş sözlüğünü yönetilen etiketleme için ayarlama
## <a name="introduction"></a>Giriş
Kolayca bulmak ve tooperform analiz gerekir ve kararları hello veri kaynaklarını anlamak için azure veri Kataloğu veri kaynağı bulma sağlar. Bu özellikleri bulmak ve kullanılabilir veri kaynaklarını çok çeşitli hello anlamak hello büyük etkisi haline getirir.

Varlıklar veri büyük anlama yükseltir bir veri Kataloğu özellik etiketleme. Etiketleme kullanarak, bir varlık veya arama veya gözatma yoluyla daha kolay toodiscover hello varlık sırayla kolaylaştırır bir sütunu anahtar sözcükleri ilişkilendirebilirsiniz. Etiketleme da daha fazla kolayca hello bağlamı ve hello varlık amacı anlamanıza yardımcı olur.

Ancak, etiketleme bazen kendi sorunlara neden olabilir. Etiketleme getirebilir sorunları bazı örnekleri şunlardır:

* Merhaba bazı varlıkların üzerinde kısaltmalar ve diğerleri genişletilmiş metni kullanın. Merhaba hedefi tootag hello hello varlıklarla olmasına rağmen bu tutarsızlığı hello bulma varlıklar, yavaşlattığını aynı etiketi.
* Bağlam bağlı olarak bir anlam olası Çeşitlemeler. Örneğin, bir etiketi adlı *gelir* bir Müşteri geliri müşteri tarafından veri kümesi gelebilir, ancak hello üç aylık satış veri kümesi üzerinde aynı etiketi hello şirket için üç aylık gelir anlamına gelebilir.  

Bunlar ve diğer benzer zorluklar toohelp adres, veri kataloğu bir iş sözlüğü içerir.

Merhaba veri Kataloğu iş sözlüğünü kullanarak, bir kuruluşun önemli iş koşulları ve bunların tanımlarını toocreate ortak bir iş sözlüğü belge. Bu idare hello kuruluş genelinde tutarlılık veri kullanımı sağlar. Bir terim hello iş sözlüğünü tanımlandıktan sonra tooa veri varlığına hello kataloğunda atanabilir. Bu yaklaşım *etiketleme yönetilen*, olan hello etiketleme olarak aynı yaklaşımı.

## <a name="glossary-availability-and-privileges"></a>Sözlük kullanılabilirlik ve ayrıcalıkları
Merhaba iş sözlüğünü yalnızca hello, Azure veri Kataloğu standart sürümü kullanılabilir. Merhaba boş veri Kataloğu sürümü bir sözlük içermez ve yetenekleri yönetilen etiketleme için sağlamaz.

Merhaba iş sözlüğünü hello aracılığıyla erişebilirsiniz **sözlüğü** hello veri Kataloğu portal'ın gezinti menüsünde seçeneği.  

![Merhaba iş sözlüğünü erişme](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Veri Kataloğu üyelerinin ve yöneticilerin hello sözlüğü administrators rolünün oluşturabilir, düzenleyebilir ve terimler hello iş sözlüğü olarak silebilirsiniz. Tüm veri Kataloğu kullanıcılara hello terim tanımları ve sözlük terimlerini etiketi varlıkları görüntüleyebilirsiniz.

![Yeni bir sözlük terim ekleme](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Terimler oluşturma
Veri Kataloğu yöneticileri ve sözlük yöneticileri oluşturabilirsiniz terimler hello tıklayarak **yeni terim** düğmesi. Her sözlük terimi alanları izleyen hello içerir:

* Merhaba terim için bir iş tanımı
* Merhaba varlık veya sütun için hedeflenen hello kullanın ya da iş kuralları yakalayan bir açıklama
* Merhaba terim hakkında en hello bilen Paydaşlar listesi
* hangi hello terim düzenlenmiştir hello hiyerarşi tanımlar hello üst terim

## <a name="glossary-term-hierarchies"></a>Sözlük terimi hiyerarşileri
Merhaba veri Kataloğu iş sözlüğünü kullanarak, bir kuruluşun kendi iş sözlüğü terimlerin hiyerarşi olarak tanımlayabilir ve daha iyi iş sınıflandırması temsil eden bir sınıflandırma koşulları oluşturabilirsiniz.

Bir terim hiyerarşisinin belirli bir düzeyde benzersiz olması gerekir. Yinelenen adlara izin verilmiyor. Hiçbir toohello sayısı sınırı hiyerarşisindeki düzeylerin yoktur, ancak üç düzeyi veya daha az olduğunda bir hiyerarşi genellikle daha kolay anlaşılır.

Merhaba iş sözlüğünü hiyerarşileri Hello kullanımı isteğe bağlıdır. Bırakma hello üst terim alan terimler için boş (hiyerarşik olmayan) düz listesini koşulları hello sözlüğü oluşturur.  

## <a name="tagging-assets-with-glossary-terms"></a>Sözlük terimlerini varlıklarına etiketleme
Terimler hello katalog içindeki tanımlandıktan sonra bir kullanıcının bir etiket türleri gibi varlıklar etiketleme hello en iyi duruma getirilmiş toosearch hello sözlüğü deneyimidir. Merhaba veri Kataloğu portalını eşleşen sözlüğü koşulları toochoose listesini görüntüler. Merhaba kullanıcı hello listeden bir sözlük terimi seçerse, hello terim toohello varlık (bir sözlük etiketi olarak da bilinir) bir etiket olarak eklenir. Merhaba kullanıcı da toocreate yeni bir etiket hello değil bir terimi yazarak seçebilirsiniz (bir kullanıcı etiketi olarak da bilinir) sözlüğü.

![Bir kullanıcı etiketi ve iki sözlüğü etiketleri veri varlığına etiketli](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Desteklenen etiket türünü hello yalnızca boş veri Kataloğu sürümü kullanıcı etiketleri hello yöneliktir.
>
>

### <a name="hover-behavior-on-tags"></a>Etiketler hakkında vurgulu davranışı
Merhaba veri Kataloğu portalında hello iki etiketleri görsel olarak farklı ve mevcut farklı vurgulu davranışları türleridir. Bir kullanıcının etiket üzerine geldiğinizde hello etiket metni ve hello kullanıcı veya hello etiketi eklediğiniz kullanıcıları görebilirsiniz. Bir sözlük etiketi geldiğinizde hello hello sözlüğü terimin tanımını ve bir bağlantı tooopen hello iş sözlüğü tooview hello tam hello terimin tanımını de görebilirsiniz.

### <a name="search-filters-for-tags"></a>Etiketleri için arama filtreleri
Sözlük etiketleri kullanıcı etiketleri hem de aranabilir olması ve aramaya filtre uygulayabilirsiniz.

## <a name="summary"></a>Özet
Azure veri kataloğu ve yönetilen hello etkinleştirir etiketleme Hello iş sözlüğünü kullanarak tanımlamak, yönetmek ve tutarlı bir şekilde veri varlıklarını bulma. Merhaba iş sözlüğünü hello iş sözlüğü kuruluş üyeleri tarafından öğrenme yükseltebilirsiniz. Varlık bulma ve anlama basitleştirir anlamlı meta veri yakalama Hello sözlüğü de destekler.

## <a name="next-steps"></a>Sonraki adımlar
* [İş sözlüğü işlemleri için REST API belgeleri](https://msdn.microsoft.com/library/mt708855.aspx)
