---
title: aaaInstall hello DC/OS CLI | Microsoft Docs
description: "Merhaba DC/OS CLI yükleyin."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, Mikro hizmetler, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> DC/OS tabanlı ACS kümeleriyle çalışmak içindir. Var. gerek toodo bu Swarm tabanlı ACS kümeleri için
> 
> 

İlk olarak, [tooyour DC/OS tabanlı ACS kümesine bağlanın](../articles/container-service/container-service-connect.md). Bunu yaptıktan sonra aşağıdaki hello komutlarla istemci makinenize DC/OS CLI hello yükleyebilirsiniz:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Python’un eski bir sürümünü kullanıyorsanız, birkaç "InsecurePlatformWarnings" fark edebilirsiniz. Bunları güvenle yok sayabilirsiniz.

Kabuğunuzu yeniden başlatmadan başlatılan sipariş tooget içinde çalıştırın:

```bash
source ~/.bashrc
```

Yeni kabukları başlattığınızda bu adım gerekmeyecektir.

Artık CLI'nin yüklü o hello doğrulayabilirsiniz:

```bash
dcos --help
```