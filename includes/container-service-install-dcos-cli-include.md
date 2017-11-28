---
title: "DC/OS CLI’yi yükleme | Microsoft Belgeleri"
description: "DC/OS CLI’yi yükleyin."
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
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="47146-104">DC/OS tabanlı ACS kümeleriyle çalışmak içindir.</span><span class="sxs-lookup"><span data-stu-id="47146-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="47146-105">Swarm tabanlı ACS kümeleri için bunu yapmaya gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="47146-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="47146-106">Önce, [DC/OS tabanlı ACS kümenize bağlanın](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="47146-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="47146-107">Bunu yaptıktan sonra aşağıdaki komutlarla istemci makinenize DC/OS CLI’yi yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47146-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="47146-108">Python’un eski bir sürümünü kullanıyorsanız, birkaç "InsecurePlatformWarnings" fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47146-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="47146-109">Bunları güvenle yok sayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47146-109">You can safely ignore these.</span></span>

<span data-ttu-id="47146-110">Kabuğunuzu yeniden başlatmadan başlamak için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="47146-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="47146-111">Yeni kabukları başlattığınızda bu adım gerekmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="47146-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="47146-112">Artık CLI’nin yüklü olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47146-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```