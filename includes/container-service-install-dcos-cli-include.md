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
> <span data-ttu-id="a3b85-104">DC/OS tabanlı ACS kümeleriyle çalışmak içindir.</span><span class="sxs-lookup"><span data-stu-id="a3b85-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="a3b85-105">Var. gerek toodo bu Swarm tabanlı ACS kümeleri için</span><span class="sxs-lookup"><span data-stu-id="a3b85-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="a3b85-106">İlk olarak, [tooyour DC/OS tabanlı ACS kümesine bağlanın](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a3b85-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="a3b85-107">Bunu yaptıktan sonra aşağıdaki hello komutlarla istemci makinenize DC/OS CLI hello yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3b85-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="a3b85-108">Python’un eski bir sürümünü kullanıyorsanız, birkaç "InsecurePlatformWarnings" fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3b85-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="a3b85-109">Bunları güvenle yok sayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3b85-109">You can safely ignore these.</span></span>

<span data-ttu-id="a3b85-110">Kabuğunuzu yeniden başlatmadan başlatılan sipariş tooget içinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a3b85-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="a3b85-111">Yeni kabukları başlattığınızda bu adım gerekmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="a3b85-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="a3b85-112">Artık CLI'nin yüklü o hello doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3b85-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```