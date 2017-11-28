---
title: "aaaApplication veya kullanıcıya özel Marathon hizmeti | Microsoft Docs"
description: "Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, Marathon, Mikro hizmetler, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="b0cd6-104">Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0cd6-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="b0cd6-105">Azure Kapsayıcı Hizmeti, Apache Mesos ve Marathon’u önceden üzerinde yapılandırdığımız bir grup ana sunucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="b0cd6-106">Bunlar kullanılan tooorchestrate olabilir uygulamalarınızı hello küme, ancak buna ait toouse hello ana sunucuları bu amaç için en iyi.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="b0cd6-107">Örneğin, Marathon hello yapılandırmasını uyguladıkça hello ana sunucuların kendilerini günlüğü--bu değişiklik gerektirir ve biraz farklı hello standart ve gerek toobe ilgilenilmeli ve yönetilen benzersiz ana sunucuları teşvik eder bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="b0cd6-108">Ayrıca, bir takım tarafından istenen hello yapılandırma hello başka bir takım için en uygun yapılandırma olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="b0cd6-109">Bu makalede, açıklayacağız nasıl tooadd bir uygulama veya kullanıcıya özel Marathon hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="b0cd6-110">Bu hizmet tooa tek bir kullanıcı veya ekibe ait olduğundan, ücretsiz tooconfigure olduklarından, istenen herhangi bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="b0cd6-111">Ayrıca, Azure kapsayıcı hizmeti hello hizmetini toorun sürdürür güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="b0cd6-112">Merhaba hizmet başarısız olursa, Azure kapsayıcı hizmeti onu sizin için yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="b0cd6-113">Başlangıç zamanının çoğunu bile kesinti yaşandığının farkına olmaz.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0cd6-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b0cd6-114">Prerequisites</span></span>
<span data-ttu-id="b0cd6-115">[Azure kapsayıcı hizmeti örneğini dağıtın](container-service-deployment.md) orchestrator ile DC/OS yazın ve [istemciniz tooyour küme bağlanabildiğinizden emin olun](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b0cd6-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="b0cd6-116">Ayrıca, adımları hello.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="b0cd6-117">Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0cd6-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="b0cd6-118">Merhaba toocreate istediğiniz hello uygulama hizmeti adını tanımlayan bir JSON yapılandırma dosyası oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="b0cd6-119">Burada kullandığımız `marathon-alice` hello çerçeve adı olarak.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="b0cd6-120">Merhaba dosya benzeri şekilde kaydedin `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="b0cd6-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="b0cd6-121">Ardından, hello DC/OS CLI tooinstall hello Marathon örneğini yapılandırma dosyanızda ayarlanan hello seçenekleri ile kullanın:</span><span class="sxs-lookup"><span data-stu-id="b0cd6-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="b0cd6-122">Artık görmelisiniz, `marathon-alice` hello Hizmetleri sekmesinde DC/OS kullanıcı Arabirimi çalışan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="b0cd6-123">Merhaba UI olacaktır `http://<hostname>/service/marathon-alice/` tooaccess istiyorsanız doğrudan.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="b0cd6-124">Merhaba DC/OS CLI tooaccess hello hizmetini Ayarla</span><span class="sxs-lookup"><span data-stu-id="b0cd6-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="b0cd6-125">İsteğe bağlı olarak, DC/OS CLI tooaccess bu yeni hizmet ayarı hello tarafından yapılandırabileceğiniz `marathon.url` özelliği toopoint toohello `marathon-alice` gibi örneği:</span><span class="sxs-lookup"><span data-stu-id="b0cd6-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="b0cd6-126">Hangi, CLI ile Merhaba karşı çalıştığından Marathon örneğine doğrulayabilirsiniz `dcos config show` komutu.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="b0cd6-127">Merhaba komutuyla ana Marathon hizmetinizi toousing döndürebilirsiniz `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="b0cd6-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

