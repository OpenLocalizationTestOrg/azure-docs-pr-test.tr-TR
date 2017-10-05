---
title: "Azure Service Fabric CLI komut dosyası Kaldır örneği"
description: "Azure Service Fabric CLI kullanarak bir Azure Service Fabric kümesinden bir uygulamayı kaldırma"
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Bir uygulama Service Fabric kümeden kaldırma

Bu örnek betik, çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü kümesinden bir küme kaydını siler.  Uygulama örneğinin silinmesi da siler çalışan tüm hizmet örnekleri uygulama ile ilişkilendirilmiş. Ardından, uygulama dosyaları görüntü deposundan silinir. 

Gerekirse, yükleme [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Örnek komut dosyası

[!code-sh[Ana](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "bir uygulamayı kümeden kaldırma")]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: [Service Fabric CLI belgelerine](../service-fabric-cli.md).

Azure Service Fabric için ek hizmet doku CLI örnek bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).
