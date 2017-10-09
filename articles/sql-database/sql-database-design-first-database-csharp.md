---
title: "aaaDesign ilk Azure SQL veritabanınızı - C# | Microsoft Docs"
description: "İlk Azure SQL veritabanınızı toodesign öğrenin ve ADO.NET kullanarak C# programı ile tooit bağlanın."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a>Bir Azure SQL veritabanı tasarlamak ve C & #x23 bağlanın; ve ADO.NET

Azure SQL veritabanı bir ilişkisel veritabanı-olarak-a (DBaaS) hello Microsoft Cloud ("Azure") hizmetidir. Bu öğreticide, toouse nasıl hello Azure portalı ve Visual Studio ile ADO.NET öğrenin: 

> [!div class="checklist"]
> * Hello Azure portalında bir veritabanı oluşturun
> * Hello Azure portal sunucu düzeyinde güvenlik duvarı kuralında ayarlama
> * ADO.NET ve Visual Studio ile toohello veritabanına bağlanın
> * ADO.NET ile tabloları oluşturma
> * Ekle, Güncelleştir ve ADO.NET verilerle silme 
> * ADO.NET veri sorgulama

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

[Visual Studio Community 2017, Visual Studio Professional 2017 veya Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/) yüklemesi.

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide temel veritabanı görevlerini gibi bir veritabanı ve tablo oluşturma hakkında bilgi edindiniz, yükleme ve verileri sorgulamak ve zaman içinde hello veritabanı tooa önceki noktası geri. Şunları öğrendiniz:
> [!div class="checklist"]
> * Veritabanı oluşturma
> * Bir güvenlik duvarı kuralı ayarlamak
> * Toohello veritabanı ile bağlantı [Visual Studio ve C#](sql-database-connect-query-dotnet-visual-studio.md)
> * Tabloları oluşturma
> * Ekle, Güncelleştir ve verilerini sil
> * Verileri sorgulama

Verilerinizi geçirme hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
>[SQL Server veritabanı tooAzure SQL veritabanına geçirme](sql-database-migrate-your-sql-server-database.md)

