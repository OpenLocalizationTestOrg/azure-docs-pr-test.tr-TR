---
title: "tooAzure Analysis Services bağlanmak için gereken aaaClient kitaplığı | Microsoft Docs"
description: "İstemci uygulamaları ve araçları tooconnect için Azure Analysis Services gerekli istemci kitaplıkları açıklar"
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>TooAzure Analysis Services bağlanmak için istemci kitaplıkları

İstemci uygulamaları ve araçları tooconnect tooAnalysis Services sunucuları için istemci kitaplıkları gereklidir. 

Analysis Services üç istemci kitaplıkları kullanın. ADOMD.NET ve Analysis Services yönetim nesneleri (AMO), yönetilen istemci kitaplıkları markalarıdır. Merhaba Analysis Services OLE DB sağlayıcısı (MSOLAP DLL) yerel istemci Kitaplığı'dır. Genellikle, tüm üç hello yüklenir aynı anda. Azure Analysis Services hello en son sürümlerini gerektirir. 

Microsoft Power BI Desktop ve Excel gibi istemci uygulamalarını, tüm üç istemci kitaplıkları yükleyin. Ancak, hello sürümü veya güncelleştirmelerinin sıklığını bağlı olarak, istemci kitaplıkları hello en son sürümleri Azure Analysis Services tarafından gerekli olmayabilir. Merhaba aynı toocustom uygulamaları veya AsCmd, ZEL, ADOMD.NET gibi diğer arabirimleri için geçerlidir. Bu uygulamalar, el ile Merhaba kitaplıkları yükleme gerektirir. Merhaba istemci kitaplıkları el ile yükleme için SQL Server özellik paketlerinde dağıtılabilir paketleri dahil edilir. Ancak, bu istemci kitaplıkları bağlı toohello SQL Server sürümü ve hello son olmayabilir.  

İstemci bağlantıları için istemci kitaplıkları, Azure Analysis Services sunucusu tooa veri kaynağından veri sağlayıcıları gerekli tooconnect farklıdır. veri kaynağı bağlantıları hakkında daha fazla toolearn bkz [veri kaynağı bağlantıları](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Merhaba son istemci kitaplıkları indirin  
Bir üretim ortamında olan ve tam olarak yayımlanan ve desteklenen sürümlerini gerektirir istemci kitaplıkları aşağıdaki hello kullanın.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Sonraki adımlar
[Excel ile bağlanma](analysis-services-connect-excel.md)    
[Power BI ile bağlanma](analysis-services-connect-pbi.md)
