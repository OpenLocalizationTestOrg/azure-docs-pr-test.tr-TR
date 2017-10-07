---
title: "'büyük veri' veri kaynaklarıyla aaaHow toowork | Microsoft Docs"
description: "Azure Blob Storage, Azure Data Lake ve Hadoop HDFS dahil 'büyük veri' veri kaynaklarıyla Azure veri Kataloğu'nu kullanarak için vurgulama desenleri nasıl tooarticle."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Azure veri Kataloğu'nda toowork büyük veri ile nasıl kaynakları
## <a name="introduction"></a>Giriş
**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Bu, Bul, anlamak ve veri kaynaklarını kullanan kişilerin ve kuruluşların tooget daha fazla değer büyük veri dahil olmak üzere kendi mevcut veri kaynaklarından veri hakkında olur.

**Azure veri Kataloğu** hello Azure blogu depolama BLOB'ları ve dizinleri yanı sıra Hadoop HDFS dosyaları ve dizinleri kaydını destekler. Bu veri kaynaklarının yarı yapılandırılmış yapısını Hello büyük esneklik sağlar. Bununla birlikte, çoğu değerden bunlarla kaydetme hello tooget **Azure veri Kataloğu**, kullanıcıların hello veri kaynaklarını nasıl düzenlendiği düşünmeniz gerekir.

## <a name="directories-as-logical-data-sets"></a>Mantıksal veri kümeleri olarak dizinler
Büyük veri kaynakları düzenlemek için genel bir desen tootreat dizinleri olarak mantıksal veri kümeleri ' dir. Üst düzey dizinleri kullanılan toodefine bir veri kümesinin alt bölüm tanımlayın ve içerdikleri hello hello verilerin kendisini depolamak var.

Bu desen örneği olabilir:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

Bu örnekte, mantıksal veri kümeleri vehicle_maintenance_events ve location_tracking_events temsil eder. Bu klasörlerinin her biri, ay ve yıl alt klasörler halinde düzenlenmiştir veri dosyalarını içerir. Bu klasörlerinin her biri, yüzlerce veya binlerce dosya büyük olasılıkla içerebilir.

Bu modelinde tek tek dosyalarıyla kaydetme **Azure veri Kataloğu** büyük olasılıkla mantıklı değildir. Bunun yerine, hello verilerle çalışma anlamlı toohello kullanıcılar hello veri kümelerini temsil hello dizinleri kaydedin.

## <a name="reference-data-files"></a>Başvuru veri dosyaları
Tamamlayıcı düzeni toostore başvuru veri kümelerini tek tek dosyalar olarak ' dir. Bu veri kümeleri hello 'küçük' tarafı büyük veri olarak düşünülen ve genellikle bir analitik veri modelindeki benzer toodimensions bağlıdır. Başvuru veri dosyaları başka bir yerde hello büyük veri deposunda depolanan hello veri dosyalarının hello toplu kullanılan tooprovide bağlamının kayıtları içerir.

Bu desen örneği olabilir:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Bir analist veya veri Bilimcisi hello büyük dizin yapıları içinde yer alan hello verilerle çalışırken, bu başvuru dosyalardaki hello veriler kullanılan tooprovide olan varlıkları hello büyük veri tooonly adı veya kimliği tarafından başvurulan için daha ayrıntılı bilgi olabilir ayarlayın.

Bu modelinde tooregister hello tek referans veri dosyalarıyla mantıklıdır **Azure veri Kataloğu**. Her dosyanın bir veri kümesini temsil eder ve her bir açıklama ve tek tek bulunan.

## <a name="alternate-patterns"></a>Alternatif desenleri
Hello hello önceki bölümde açıklanan desenleri büyük veri deposu düzenlenebilir yalnızca iki olası yolları vardır, ancak her farklı bir uygulamasıdır. Nasıl veri kaynaklarınızı, büyük veri kaynaklarıyla kaydedilirken yapılandırılmıştır bağımsız olarak **Azure veri Kataloğu**, odak, değer tooothers içinde çeken hello veri kümelerini temsil hello dosyaları ve dizinleri kaydetmede, Kuruluş. Tüm dosyaları ve dizinleri kaydetme hello Kataloğu, kullanıcıların toofind için daha zor ne ihtiyaç duydukları kolaylaştırarak daraltabilir.

## <a name="summary"></a>Özet
Veri kaynakları ile kaydetme **Azure veri Kataloğu** daha kolay toodiscover yapar ve anladığınızdan emin olun. Kaydetme ve, mantıksal veri kümelerini temsil hello büyük veri dosyaları ve dizinleri yorumlama ihtiyaç duydukları hello büyük veri kaynaklarını bulabilir ve kullanıcıların yardımcı olur.
