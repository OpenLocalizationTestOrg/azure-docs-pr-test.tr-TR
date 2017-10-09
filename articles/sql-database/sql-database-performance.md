---
title: "aaaMonitor ve performansı - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanı performans sağlar hello geçerli sorgu performansını iyileştirebilir alanlarını tanımlayacak toohelp araçları."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>İzleme ve performansı
Azure SQL veritabanı veritabanınızdaki olası sorunlar tanımlanmakta ve akıllı ayarlama Eylemler ve öneriler sağlayarak İş yükünüzün performansını geliştirebilirsiniz Eylemler önerir.

tooreview veritabanı performansı, kullanım hello **performans** döşeme hello genel bakış sayfasında veya aşağı çok gidin "Destek + sorun giderme" bölümüne:

   ![Performans görünümü](./media/sql-database-performance/entries.png)

Merhaba "Destek + sorun giderme" bölümünde sayfaları aşağıdaki hello kullanabilirsiniz:


1. [Performans genel bakış](#performance-overview) veritabanınızın toomonitor performansını. 
2. [Performans önerileri](#performance-recommendations) İş yükünüzün performansını artırabilir toofind performans önerileri.
3. [Sorgu performansı öngörüleri](#query-performance-insight) kaynak tüketen sorguları toofind üst kaynak.
4. [Otomatik ayarlama](#automatic-tuning) toolet Azure SQL veritabanı, veritabanınızı otomatik olarak en iyi duruma getirme.

## <a name="performance-overview"></a>Performans genel bakış
Bu görünüm, veritabanınızın performansını özetini sağlar ve ve sorun gidermeyi performansla yardımcı olur. 

![Performans](./media/sql-database-performance/performance.png)

* Merhaba **önerileri** kutucuğu veritabanınız için öneriler ayarlama bir dökümünü sağlar (ilk üç önerileri gösterilen olup olmadığını daha fazla). Bu kutucuğa tıklayarak alır, çok**[performans önerileri](#performance-recommendations)**. 
* Merhaba **etkinlik ayarlama** kutucuğu hello devam eden ve veritabanınız için Eylemler ayarlama, etkinlik ayarlama, hello geçmişi hızlı bir görünüme vererek tamamlanan özetini sağlar. Bu kutucuğa tıklamak toohello veritabanınız için Geçmiş görünümünü ayarlama tam götürür.
* Merhaba **otomatik ayarı** kutucuğunda gösterilir hello [otomatik ayarı yapılandırma](sql-database-automatic-tuning-enable.md) (otomatik olarak uygulanan tooyour veritabanı seçenekleri ayarlama) veritabanı. Bu kutucuğa tıklayarak hello Otomasyon yapılandırması iletişim kutusunu açar.
* Merhaba **veritabanı sorguları** kutucuğunda gösterilir hello hello sorgu performansı (kaynak tüketen sorguları genel DTU kullanımı ve üst kaynak) veritabanı özeti. Bu kutucuğa tıklayarak alır, çok**[sorgu performansı öngörüleri](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Performans önerileri
Bu sayfa akıllı sağlar [önerileri ayarlama](sql-database-advisor.md) veritabanınızın performansı geliştirebilir. Bu sayfada şu önerilerin türlerini hello gösterilmektedir:

* Hangi dizin toocreate veya bırakma öneriler sunar.
* Şema sorunları hello veritabanında belirlendiğinde öneriler sunar.
* Sorguları parametreli sorgularından yararlanabilir kullanmayla ilgili öneriler.

![Performans](./media/sql-database-performance/recommendations.png)

Merhaba son uygulanan eylemler ayarlama, tam geçmişini de bulabilirsiniz.

Bilgi nasıl toofind apply performans önerileri [bulmak ve performans önerileri uygulamak](sql-database-advisor-portal.md) makale.

## <a name="automatic-tuning"></a>Otomatik ayarlama
Azure SQL veritabanları otomatik olarak ayarlamak veritabanı performansını uygulayarak [performans önerileri](sql-database-advisor.md). toolearn daha fazlasını okuyun [otomatik ayarlama makale](sql-database-automatic-tuning.md). tooenable, okuma [nasıl tooenable otomatik ayarlama](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Sorgu Performansı Öngörüleri
[Sorgu performansı öngörüleri](sql-database-query-performance.md) toospend sağlayarak veritabanı performans sorunlarını giderme daha az zaman verir:

* Veritabanları (DTU) kaynak tüketimi daha derin bir anlayış. 
* Merhaba üst CPU potansiyel olarak performansı için ayarlanmış sorguları kullanma. 
* özelliği toodrill aşağı sorgu hello ayrıntılarını hello. 

  ![Performans Panosu](./media/sql-database-query-performance/performance.png)

Bu sayfa hakkında daha fazla bilgi hello makalesinde Bul  **[nasıl toouse sorgu performansı öngörüleri](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Ek kaynaklar
* [Tek veritabanları için Azure SQL Database performans rehberi](sql-database-performance-guidance.md)
* [Bir esnek havuz ne zaman kullanılmalı?](sql-database-elastic-pool-guidance.md)

