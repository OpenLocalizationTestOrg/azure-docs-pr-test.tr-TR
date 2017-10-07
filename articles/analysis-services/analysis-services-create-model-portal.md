---
title: "aaaCreate hello Azure Analysis Services Web Tasarımcısı kullanarak tablolu model | Microsoft Docs"
description: "Nasıl toocreate kullanarak bir Azure Analysis Services tablolu model hello Azure portalında Web Tasarımcısı hakkında bilgi edinin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Azure portalında bir model oluşturma

Hello Azure Analysis Services web Tasarımcısı (Önizleme) Özelliği Azure portalında hızlı ve kolay bir şekilde toocreate sağlar ve tablolu modeller ve sorgu modelini veri sağ tarayıcınızda düzenleyin. 

Unutmayın, hello web Designer **Önizleme**. Yeni işlevselliği Önizleme, tüm başlangıç saatinin eklenen sırada işlevselliği sınırlıdır. Daha gelişmiş modeli geliştirme ve test amacıyla, bu en iyi toouse Visual Studio (SSDT) ve SQL Server Management Studio (SSMS) olur.

## <a name="prerequisites"></a>Ön koşullar

- Bir hello standart veya Geliştirici katmanı Azure Analysis Services sunucusunda. Merhaba Web Tasarımcısı kullanılarak oluşturulan yeni modelleri DirectQuery, bu Katmanlar tarafından desteklenen ' dir.
- Bir Azure SQL Database, Azure SQL Data Warehouse veya Power BI Desktop (.pbix) dosyası olarak bir veri kaynağı. Yeni modelleri veri kaynaklarını Power BI Desktop dosyaları destek Azure SQL Database, Azure SQL Data Warehouse, Oracle ve Teradata oluşturulur.
- Bir SQL Server hesabı ve tooAzure SQL veritabanına veya Azure SQL veri ambarı veri kaynaklarına bağlanmak için parola.

## <a name="toocreate-a-new-tabular-model"></a>Yeni bir tablolu model toocreate

1. Sunucunuzun içinde **genel bakış** dikey > **Web Tasarımcısı**, tıklatın **açık**.

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. İçinde **Web Tasarımcısı** > **modelleri**, tıklatın **+ Ekle**.

    ![Azure portalında bir model oluşturma](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. İçinde **yeni model**, model adını yazın ve ardından bir veri kaynağı seçin.

    ![Azure portalında yeni model iletişim kutusu](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. İçinde **Bağlan**, hello bağlantı özelliklerini girin. Kullanıcı adı ve parola bir SQL Server hesabı olması gerekir.

     ![Azure portalında iletişim Bağlan](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. İçinde **tabloları ve görünümleri**modelinizde hello tabloları tooinclude seçin ve ardından **oluşturma**. Bir anahtar çifti ile tablolar arasında ilişkiler otomatik olarak oluşturulur.

     ![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Yeni modelinizi tarayıcınızda görüntülenir. Buradan, şunları yapabilirsiniz:   

- Model veri alanları toohello Sorgu Tasarımcısı sürükleme ve filtreler ekleyerek sorgu.
- Yeni ölçüleri tablolarda oluşturun.
- Merhaba json Düzenleyicisi'ni kullanarak model meta verilerini düzenleyin.
- Merhaba modeli, Visual Studio (SSDT), Power BI Desktop veya Excel'de açın.

![Tabloları ve görünümleri seçin](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Model meta verilerini düzenleyin veya yeni ölçüleri tarayıcınızda oluşturduğunuzda, bu değişiklikleri tooyour modeli Azure'da kaydediyorsanız. Ayrıca SSDT, Power BI Desktop veya Excel modelinizde üzerinde çalışıyorsanız, modelinizi eşitlenmemiş elde edebilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar 
[Veritabanı rolleri ve kullanıcıları yönetme](analysis-services-database-users.md)  
[Excel ile bağlanma](analysis-services-connect-excel.md)  


