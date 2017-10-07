---
title: "aaaHow toocreate hello Azure portalında bir hizmet veri yolu ad alanı | Microsoft Docs"
description: "Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturma

Ad alanı, tüm mesajlaşma bileşenlerini kapsayan bir kapsayıcıdır. Tek bir ad alanında birden fazla kuyruk ve konu bulunabilir ve ad alanları genellikle uygulama kapsayıcıları olarak görev yapar. İki farklı şekilde toocreate bir hizmet veri yolu ad alanı vardır:

1. Azure portalı (bu makale)
2. [Resource Manager şablonları][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Hello Azure portalında bir ad alanı oluşturma

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

Tebrikler! Bir Service Bus Mesajlaşması ad alanı oluşturdunuz.

## <a name="next-steps"></a>Sonraki adımlar

Kullanıma bizim [GitHub örnekleri][github-samples], hangi Göster daha gelişmiş özellikler Azure Service Bus Mesajlaşma hizmetinin hello bazıları.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
