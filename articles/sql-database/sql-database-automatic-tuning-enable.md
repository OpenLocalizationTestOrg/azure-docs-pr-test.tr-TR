---
title: "Azure SQL veritabanı için ayarlama otomatik aaaEnable | Microsoft Docs"
description: "Otomatik Azure SQL veritabanınızda kolayca ayarlama etkinleştirebilirsiniz."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Otomatik ayarlamayı etkinleştirme

Azure SQL veritabanı sürekli sorgularınızı izler ve İş yükünüzün performansını tooimprove gerçekleştirebileceğiniz hello işlem tanımlayan bir otomatik olarak yönetilen veri hizmetidir. Önerileri gözden geçirin ve el ile uygulamadan veya için otomatik olarak düzeltme eylemleri uygulamak Azure SQL veritabanı sağlar - bu olarak bilinir **otomatik ayarlama modu**. Otomatik ayarlama hello sunucu veya hello veritabanı düzeyinde etkinleştirilebilir.

## <a name="enable-automatic-tuning-on-server"></a>Otomatik sunucu üzerinde ayarlama etkinleştir

tooenable otomatik Azure portal ve ardından toohello Server'da gidin Azure SQL veritabanı sunucusunda ayarlama **otomatik ayarlama** hello menüsünde. Select hello tooenable istediğiniz ve seçin otomatik ayarlama seçenekleri **Uygula**:

![Sunucu](./media/sql-database-automatic-tuning-enable/server.png)

Merhaba sunucudaki uygulanan tooall veritabanları sunucusunda seçeneklerini ayarlama otomatik olarak yapılır. Varsayılan olarak, tüm veritabanları, kendi üst sunucusundan hello yapılandırmasını devralmak, ancak bu kullanılabilir geçersiz kılındı ve tek tek her veritabanı için belirtilen.

## <a name="configure-automatic-tuning-on-database"></a>Otomatik veritabanı ayarlama yapılandırın

Merhaba, tooindividually belirtin hello otomatik ayarlama yapılandırma her veritabanını Azure portal sağlar.

> [!NOTE]
> Merhaba genel öneri yapılandırmadır toomanage hello otomatik ayarlama sunucu düzeyinde aynı yapılandırma ayarları uygulanabilir her veritabanı üzerinde otomatik olarak bunu hello. Merhaba veritabanı bazılarında aynı sunucu hello farklı ise tek bir veritabanının üzerine otomatik ayarlama yapılandırın.
>

tek bir veritabanı üzerinde ayarlama otomatik tooenable toohello veritabanında hello Azure portal gidin ve sonra hem de seçin **otomatik ayarlama**. Ayrı ayrı bir veritabanı için başlangıç yapılandırması belirtin veya hello onay kutusunu seçerek hello veritabanından tek veritabanı tooinherit hello ayarlarını yapılandırabilirsiniz.

![Database](./media/sql-database-automatic-tuning-enable/database.png)

Uygun yapılandırma seçtikten sonra tıklatın **Uygula**.

## <a name="next-steps"></a>Sonraki adımlar
* Okuma hello [otomatik ayarlama makale](sql-database-automatic-tuning.md) toolearn nasıl performansınızı geliştirmenize yardımcı olabilir ve otomatik ayarlama hakkında daha fazla bilgi.
* Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.
* Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı hello performans etkisini görüntüleme hakkında toolearn.
