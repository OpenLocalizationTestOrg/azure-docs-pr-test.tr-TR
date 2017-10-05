---
title: "Uygulama veya kullanıcıya özel Marathon hizmeti | Microsoft Belgeleri"
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
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="dd242-104">Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd242-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="dd242-105">Azure Kapsayıcı Hizmeti, Apache Mesos ve Marathon’u önceden üzerinde yapılandırdığımız bir grup ana sunucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd242-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="dd242-106">Bunlar, uygulamalarınızı kümede düzenlemek için kullanılabilir, ancak en iyisi ana sunucuları bu amaç için kullanmamaktır.</span><span class="sxs-lookup"><span data-stu-id="dd242-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="dd242-107">Örneğin, Marathon yapılandırmasına ince ayar yapma ana sunucuların kendilerinde oturum açmayı ve değişiklikler yapmayı gerektirir; bu, standart olandan biraz daha farklı olan benzersiz ana sunucuları teşvik eder ve bağımsız olarak ilgilenilmeli ve yönetilmelidir.</span><span class="sxs-lookup"><span data-stu-id="dd242-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="dd242-108">Ayrıca, bir takım tarafından istenen yapılandırma başka bir takım için en uygun yapılandırma olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="dd242-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="dd242-109">Bu makalede size bir uygulamaya veya kullanıcıya özel Marathon hizmeti ekleme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd242-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="dd242-110">Bu hizmet bir tek bir kullanıcı veya ekibe ait olduğundan bunlar istenen herhangi bir şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="dd242-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="dd242-111">Ayrıca, Azure Container Service hizmetin çalışmaya devam etmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd242-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="dd242-112">Hizmet başarısız olursa Azure Container Service sizin için yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="dd242-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="dd242-113">Çoğu zaman kesinti yaşandığının farkına varmazsınız bile.</span><span class="sxs-lookup"><span data-stu-id="dd242-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd242-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dd242-114">Prerequisites</span></span>
<span data-ttu-id="dd242-115">[DC/OS orchestrator türüyle Azure Container Service örneğini dağıtın](container-service-deployment.md) ve [istemcinizin kümenize bağlanabildiğinden emin olun](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dd242-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="dd242-116">Ayrıca aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="dd242-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="dd242-117">Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd242-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="dd242-118">Oluşturmak istediğiniz uygulama hizmeti adını tanımlayan bir JSON yapılandırma dosyası oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="dd242-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="dd242-119">Burada çerçeve adı olarak `marathon-alice` kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="dd242-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="dd242-120">Dosyayı `marathon-alice.json` benzeri şekilde kaydedin:</span><span class="sxs-lookup"><span data-stu-id="dd242-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="dd242-121">Ardından, Marathon örneğini yapılandırma dosyanızda ayarlanan seçenek grubuyla yüklemek için DC/OS CLI’yı kullanın:</span><span class="sxs-lookup"><span data-stu-id="dd242-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="dd242-122">Şimdi, DC/OS kullanıcı arabiriminizin Hizmetler sekmesinde `marathon-alice` hizmetinizin çalıştığını görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="dd242-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="dd242-123">Doğrudan erişmek isterseniz kullanıcı arabirimi `http://<hostname>/service/marathon-alice/` olur.</span><span class="sxs-lookup"><span data-stu-id="dd242-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="dd242-124">Hizmete erişmek için DC/OS CLI’yı ayarlama</span><span class="sxs-lookup"><span data-stu-id="dd242-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="dd242-125">İsteğe bağlı olarak, `marathon.url` özelliğini aşağıdaki şekilde `marathon-alice` örneğini işaret edecek şekilde ayarlayarak DC/OS CLI’nizi bu yeni hizmete erişmek üzere yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd242-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="dd242-126">CLI’nizin hangi Marathon örneğine karşı çalıştığını `dcos config show` komutuyla doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd242-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="dd242-127">`dcos config unset marathon.url` komutuyla ana Marathon hizmetinizi kullanmaya geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd242-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

