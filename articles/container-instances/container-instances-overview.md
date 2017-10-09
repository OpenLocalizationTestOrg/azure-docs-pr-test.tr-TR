---
title: "aaaAzure kapsayıcı örnekleri genel bakış | Azure belgeleri"
description: "Azure Container Instances’ı Anlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Azure Container Instances

Kapsayıcıları hızlı bir şekilde hello tercih edilen yol toopackage gelmektedir, dağıtın ve bulut uygulamalarını yönetin. Azure kapsayıcı örnekleri hello en hızlı ve kolay şekilde toorun bir kapsayıcıda Azure, herhangi bir sanal makine tooprovision kalmadan ve üst düzey hizmet tooadopt kalmadan sunar. 

Yalıtılmış kapsayıcılarda çalışabileceğiniz senaryolar (basit uygulamalar, görev otomasyonu ve sürüm işleri gibi) için Azure Container Instances harika bir çözümdür. Merhaba öneririz burada dosyalarda tam birden çok kapsayıcı, otomatik ölçeklendirme ve Eşgüdümlü uygulama yükseltmelerini arasında hizmet bulma de dahil olmak üzere, kapsayıcı orchestration senaryoları için [Azure kapsayıcı hizmeti](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Hızlı başlangıç süreleri

Kapsayıcılar, sanal makinelerde önemli başlangıç süresi avantajları sunar. Azure kapsayıcı örnekleriyle bir kapsayıcı Azure'da hello gerek tooprovision olmadan saniye başlatmak ve VM'ler yönetin.

## <a name="hypervisor-level-security"></a>Hiper yönetici düzeyinde güvenlik

Geçmişte kapsayıcılar, uygulama bağımlılığı yalıtımı ve kaynak idaresi olanakları sağlıyor ancak birden çok kiracılı zorlu kullanımlar için yeterli kabul edilmiyordu. Azure Container Instances ile uygulamanız,sanal makine yerine kapsayıcıda yalıtılır.

## <a name="custom-sizes"></a>Özel boyutlar

Yalnızca tek bir uygulama, ancak bu uygulamaların tam gereksinimlerini hello büyük ölçüde değişebilir genellikle en iyi duruma getirilmiş toorun kapsayıcılardır. Azure Container Instances kullandığınızda, CPU çekirdekleri ve bellek açısından tam olarak gerek duyduğunuz kadar kaynak isteyebilirsiniz. Ne istemcinin göre tarafından hello fatura ödeme, gereksinimlerinize göre harcama ince iyileştirebilirsiniz şekilde ikinci.

## <a name="public-ip-connectivity"></a>Genel IP bağlantısı

Azure kapsayıcı örnekleriyle kapsayıcılarınızı getirebilir doğrudan toohello Internet ortak IP adresine sahip. Hello gelecekteki, biz bizim ağ yeteneklerini tooinclude tümleştirme sanal ağlarla genişletin, yük dengeleyicileri ve diğer çekirdek bölümleri hello Azure ağ altyapısı.

## <a name="persistent-storage"></a>Kalıcı depolama

tooretrieve ve Azure kapsayıcı örnekleri durumuyla kalıcı, doğrudan bağlama Azure dosya paylaşımları sunuyoruz.

## <a name="linux-and-windows-containers"></a>Linux ve Windows kapsayıcıları

Azure kapsayıcı örnekleri, hem Windows zamanlayabilir ve aynı API ile Linux kapsayıcıları hello. Yalnızca hello temel işletim sistemi türü ve şey aynı göstermek.

## <a name="co-scheduled-groups"></a>Birlikte zamanlanmış gruplar

Azure Container Instances, aynı ana makineyi, yerel ağı, depolama alanını ve yaşam döngüsünü paylaşan birden çok kapsayıcı grubunun zamanlanmasını destekler. Bu, toocombine ana uygulamanızı başkalarıyla sağlar destekleyen bir rol, günlüğe kaydetme gibi davranan.

## <a name="next-steps"></a>Sonraki adımlar

Tek bir komut kullanarak bir kapsayıcı tooAzure dağıtmayı deneyin bizim [Hızlı Başlangıç Kılavuzu](container-instances-quickstart.md).
