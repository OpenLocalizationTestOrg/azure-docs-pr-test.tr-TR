---
title: "aaaAzure Service Fabric CLI komut dosyası örneği Kaldır"
description: "Bir uygulama hello Azure Service Fabric CLI kullanarak bir Azure Service Fabric kümesinden Kaldır"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Bir uygulama Service Fabric kümeden kaldırma

Bu örnek betik, çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü hello kümeden kaydını siler.  Silme hello uygulama örneği, bu uygulama ile ilişkili hizmet örneklerini çalıştıran tüm hello da siler. Ardından, hello uygulama dosyalarını hello görüntü deposundan silinir. 

Gerekirse, hello yükleyin [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Örnek komut dosyası

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: Merhaba [Service Fabric CLI belgelerine](../service-fabric-cli.md).

Azure Service Fabric için ek hizmet doku CLI örnek hello bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).
