---
title: "aaaWhat toomy Web işi projesinin oldu (Visual Studio Azure depolama bağlı hizmeti)? | Microsoft Belgeleri"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir Azure Web işi projesi ne açıklar"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ed0ce75f5b23eca3c41dacb48564d6e5b846f395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>Ne oldu toomy Web işi projesinin (Visual Studio Azure depolama bağlı hizmeti)?
## <a name="references-added"></a>Eklenen başvuruları
Hello Azure depolama NuGet paketini Visual Studio projenizde güncelleştirilmiş tooor eklendi.  
Bu paket .NET başvurularını aşağıdaki hello ekler:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Azure eklenen depolama alanı için bağlantı dizesi
Merhaba App.config dosyasında projenizin hello **AzureWebJobsStorage** ve **AzureWebJobsDashboard** girişleri hello seçili depolama hesabına ait bağlantı dizesini ve anahtarla güncelleştirildi.

Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

