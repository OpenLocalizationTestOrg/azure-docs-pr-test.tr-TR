---
title: "aaaAzure Service Fabric CLI komut dosyası örneği dağıtma"
description: "Hello Azure Service Fabric CLI kullanarak bir uygulama tooan Azure Service Fabric kümesi dağıtma"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Bir uygulama tooa Service Fabric kümesi dağıtma

Bu örnek betik bir uygulama paketi tooa kümenin görüntü deposu kopyalar, hello kümede hello uygulama türü kaydeder ve hello uygulama türünden uygulama örneğini oluşturur. Varsayılan hizmetlerin de şu anda oluşturulur.

Gerekirse, hello yükleyin [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Örnek komut dosyası

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

İşiniz bittiğinde, hello [kaldırmak](cli-remove-application.md) betik kullanılan tooremove hello uygulama olabilir. Merhaba kaldırma komut dosyası hello uygulama örneği siler, hello uygulama türü kaydını siler ve görüntü deposundan hello uygulama paketini siler.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: Merhaba [Service Fabric CLI belgelerine](../service-fabric-cli.md).

Azure Service Fabric için ek hizmet doku CLI örnek hello bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).
