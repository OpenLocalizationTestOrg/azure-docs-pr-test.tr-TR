---
title: "Azure SQL veritabanı için otomatik olarak ayarlamayı etkinleştirmek | Microsoft Docs"
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
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a>Otomatik ayarlamayı etkinleştirme

Azure SQL veritabanı sürekli sorgularınızı izler ve İş yükünüzün performansını iyileştirmek için yapabileceğiniz eylemi tanımlayan bir otomatik olarak yönetilen veri hizmetidir. Önerileri gözden geçirin ve el ile uygulamadan veya için otomatik olarak düzeltme eylemleri uygulamak Azure SQL veritabanı sağlar - bu olarak bilinir **otomatik ayarlama modu**. Otomatik ayarlama sunucu veya veritabanı düzeyinde etkinleştirilebilir.

## <a name="enable-automatic-tuning-on-server"></a>Otomatik sunucu üzerinde ayarlama etkinleştir

Azure SQL veritabanı sunucusuna otomatik olarak ayarlamayı etkinleştirmek için Azure portalında sunucusuna gidin ve ardından **otomatik ayarlama** menüde. İstediğiniz etkinleştirmek ve seçmek için otomatik ayarlama seçenekleri seçin **Uygula**:

![Sunucu](./media/sql-database-automatic-tuning-enable/server.png)

Sunucuda otomatik ayarlama seçenekleri, sunucudaki tüm veritabanları için uygulanır. Varsayılan olarak, tüm veritabanları, kendi üst sunucusundan yapılandırmasını devralmak, ancak bu kullanılabilir geçersiz kılındı ve tek tek her veritabanı için belirtilen.

## <a name="configure-automatic-tuning-on-database"></a>Otomatik veritabanı ayarlama yapılandırın

Azure portalı ayrı ayrı her veritabanını ayarlama yapılandırmasını otomatik belirtmenize olanak sağlar.

> [!NOTE]
> Aynı yapılandırma ayarları her veritabanı üzerinde otomatik olarak uygulanabilir şekilde otomatik ayarlama yapılandırma sunucusu düzeyinde yönetmek için genel yüklenmemesi önerilir. Veritabanı farklı ise tek bir veritabanının üzerine otomatik ayarlama başkalarının aynı sunucuda yapılandırın.
>

Otomatik üzerinde tek bir veritabanı ayarlamayı etkinleştirmek için Azure portalında veritabanına gidin ve sonra hem de seçin **otomatik ayarlama**. Onay kutusunu seçerek veritabanından ayarları devralmak için tek bir veritabanı yapılandırabilir veya yapılandırma veritabanı için ayrı ayrı belirtin.

![Database](./media/sql-database-automatic-tuning-enable/database.png)

Uygun yapılandırma seçtikten sonra tıklatın **Uygula**.

## <a name="next-steps"></a>Sonraki adımlar
* Okuma [otomatik ayarlama makale](sql-database-automatic-tuning.md) nasıl performansınızı geliştirmenize yardımcı olabilir ve otomatik ayarlama hakkında daha fazla bilgi edinmek için.
* Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.
* Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı performans etkisini görüntüleme hakkında bilgi edinmek için.
