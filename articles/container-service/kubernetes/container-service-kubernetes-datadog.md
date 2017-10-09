---
title: "aaaMonitor Azure Kubernetes küme ile Datadog | Microsoft Docs"
description: "Kubernetes Datadog kullanarak Azure kapsayıcı hizmeti kümesinde izleme"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Azure kapsayıcı hizmeti kümesi DataDog ile izleme

## <a name="prerequisites"></a>Ön koşullar
Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).

Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.

Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:

```console
$ az --version
```

Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).

Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:

```console
$ kubectl version
```

Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>DataDog
Datadog, Azure kapsayıcı hizmeti kümesi kapsayıcılara gelen izleme verilerini toplayan izleme bir hizmettir. Datadog Docker tümleştirmesi, kapsayıcılara belirli ölçümleri görebileceğiniz bir Pano vardır. Kapsayıcılardan toplanan ölçümleri CPU, bellek, ağ ve g/ç tarafından düzenlenir. Datadog ölçümleri kapsayıcıları ve görüntüleri halinde ayırır.

İlk çok gereksinim[bir hesap oluşturun](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>DaemonSet ile Merhaba Datadog aracı yükleme
DaemonSets Kubernetes toorun tarafından kullanılan bir kapsayıcı hello kümedeki her ana bilgisayarda tek bir örneği.
Bunlar izleme aracıları çalıştırmak için mükemmel.

Datadog oturum açtıktan sonra hello izleyebilirsiniz [Datadog yönergeleri](https://app.datadoghq.com/account/settings#agent/kubernetes) bir DaemonSet kullanarak kümenizde tooinstall Datadog aracıları.

## <a name="conclusion"></a>Sonuç
İşte bu kadar! Bir kez hello aracıları ayarlama ve çalıştırdığınız hello konsol verilerde birkaç dakika içinde görmeniz gerekir. Tümleşik hello ziyaret ettiğiniz [kubernetes Pano](https://app.datadoghq.com/screen/integration/kubernetes) toosee kümenizi özetini.
