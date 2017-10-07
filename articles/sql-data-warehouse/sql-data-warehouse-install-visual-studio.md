---
title: "aaaInstall Visual Studio ve SSDT SQL Data Warehouse için | Microsoft Docs"
description: "Azure SQL Data Warehouse için Visual Studio'yu ve SQL Server Veri Araçları'nı (SSDT) Yükleme"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>SQL Data Warehouse için Visual Studio ve SSDT yükleme
toodevelop uygulamalar SQL Data Warehouse için Visual Studio en son sürümünü hello hello en son sürümü SQL Server veri Araçları (SSDT) ile kullanmanızı öneririz.  Geriye dönük uyumluluk için SSDT ile Visual Studio 2013 Güncelleştirme 5 de desteklenir.  

SSDT ile Visual Studio kullanarak etmenizi sağlar toouse hello SQL Server Nesne Gezgini toovisually tabloları, görünümleri, saklı yordamları ve daha birçok nesneyi SQL veri ambarı keşfedin yanı sıra sorgular çalıştırın.

> [!NOTE]
> SQL Data Warehouse, henüz Visual Studio Veritabanı Projelerini desteklemiyor.  Bu özellik sonraki bir sürümde eklenecek.
> 
> 

## <a name="step-1-install-visual-studio"></a>1. adım: Visual Studio yükleme
Bu bağlantılar toodownload izleyin ve Visual Studio yükleyin. Zaten Visual Studio 2013 veya sonraki bir sürümü yüklü olduğunda tooStep 2 Atla, SSDT'yi yükleme.

1. [Visual Studio indirme][].
2. Merhaba izleyin [Visual Studio'yu yükleme] [ Installing Visual Studio] Kılavuzu MSDN'de ve hello varsayılan yapılandırmaları seçin.

## <a name="step-2-install-ssdt"></a>2. Adım: SSDT'yi yükleme
Visual Studio için SSDT tooinstall işaretlemeniz yeterli Visual Studio'da bir SSDT güncelleştirmesinin için aşağıdaki adımları izleyerek.

1. Visual Studio tıklayın **Araçları** / **Uzantılar ve güncelleştirmeler...** / **Güncelleştirmeleri**
2. **Ürün Güncelleştirmeleri**'ni seçip **Veritabanı araçları için Microsoft SQL Server Güncelleştirmesi** olup olmadığına bakın.

Bir güncelleştirme bulunmazsa, hello en son sürümü yüklü olmalıdır.  tooconfirm SSDT yüklü tıklayın **yardımcı** / **Microsoft Visual Studio hakkında** ve SQL Server veri araçları için hello listede olup olmadığına bakın.  14.0.60525.0 SSDT'nin en son sürümüne Hello olur.  Alternatif olarak Hello seçeneği tooinstall Visual Studio'dan kullanılabilir durumda değilse, hello ziyaret edebilirsiniz [SSDT indirme] [ SSDT Download] sayfasında toodownload ve SSDT'yi el ile yükleyin.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba SSDT'nin en son sürümüne sahip olduğunuza göre çok hazır olduğunuz[bağlanmak] [ connect] tooyour SQL veri ambarı.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio indirme]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
