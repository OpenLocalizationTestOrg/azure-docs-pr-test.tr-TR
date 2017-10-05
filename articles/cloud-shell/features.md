---
title: "Azure bulut Kabuk (Önizleme) özellikleri | Microsoft Docs"
description: "Azure bulut Kabuk özelliklerine genel bakış"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="8e2a5-103">Özellikler ve Araçlar Azure bulut Kabuğu</span><span class="sxs-lookup"><span data-stu-id="8e2a5-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="8e2a5-104">Azure bulut Kabuk, yönetmek ve Azure kaynaklarını geliştirmek için bir tarayıcı tabanlı kabuk deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="8e2a5-105">Bulut Kabuk, sürümü, yükleme ve bir makineyi kendiniz koruma yükünü olmadan Azure kaynaklarını yönetmek için bir tarayıcı erişilebilir, önceden yapılandırılmış Kabuk deneyimi sunar.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="8e2a5-106">İstek başına temelinde makineler bulut Kabuk sağlar ve sonuç olarak makine durumu oturumlarında kalıcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="8e2a5-107">Bulut Kabuk etkileşimli oturumları için kurulu olduğundan Kabukları Kabuğu kaldıktan 20 dakika sonra otomatik olarak sonlanır.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="8e2a5-108">Bulut Kabuğu'nda bash</span><span class="sxs-lookup"><span data-stu-id="8e2a5-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="8e2a5-109">Araçlar</span><span class="sxs-lookup"><span data-stu-id="8e2a5-109">Tools</span></span>
|<span data-ttu-id="8e2a5-110">Kategori</span><span class="sxs-lookup"><span data-stu-id="8e2a5-110">Category</span></span>   |<span data-ttu-id="8e2a5-111">Ad</span><span class="sxs-lookup"><span data-stu-id="8e2a5-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="8e2a5-112">Linux Kabuk yorumlayıcı</span><span class="sxs-lookup"><span data-stu-id="8e2a5-112">Linux shell interpreter</span></span>|<span data-ttu-id="8e2a5-113">Bash</span><span class="sxs-lookup"><span data-stu-id="8e2a5-113">Bash</span></span><br> <span data-ttu-id="8e2a5-114">Paylaş</span><span class="sxs-lookup"><span data-stu-id="8e2a5-114">sh</span></span>               |
|<span data-ttu-id="8e2a5-115">Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="8e2a5-115">Azure tools</span></span>            |<span data-ttu-id="8e2a5-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) ve [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="8e2a5-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="8e2a5-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="8e2a5-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="8e2a5-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="8e2a5-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="8e2a5-119">Metin düzenleyiciler</span><span class="sxs-lookup"><span data-stu-id="8e2a5-119">Text editors</span></span>           |<span data-ttu-id="8e2a5-120">VIM</span><span class="sxs-lookup"><span data-stu-id="8e2a5-120">vim</span></span><br> <span data-ttu-id="8e2a5-121">nano</span><span class="sxs-lookup"><span data-stu-id="8e2a5-121">nano</span></span><br> <span data-ttu-id="8e2a5-122">emacs</span><span class="sxs-lookup"><span data-stu-id="8e2a5-122">emacs</span></span>       |
|<span data-ttu-id="8e2a5-123">Kaynak denetimi</span><span class="sxs-lookup"><span data-stu-id="8e2a5-123">Source control</span></span>         |<span data-ttu-id="8e2a5-124">Git</span><span class="sxs-lookup"><span data-stu-id="8e2a5-124">git</span></span>                    |
|<span data-ttu-id="8e2a5-125">Derleme araçları</span><span class="sxs-lookup"><span data-stu-id="8e2a5-125">Build tools</span></span>            |<span data-ttu-id="8e2a5-126">Yapma</span><span class="sxs-lookup"><span data-stu-id="8e2a5-126">make</span></span><br> <span data-ttu-id="8e2a5-127">maven</span><span class="sxs-lookup"><span data-stu-id="8e2a5-127">maven</span></span><br> <span data-ttu-id="8e2a5-128">npm</span><span class="sxs-lookup"><span data-stu-id="8e2a5-128">npm</span></span><br> <span data-ttu-id="8e2a5-129">PIP</span><span class="sxs-lookup"><span data-stu-id="8e2a5-129">pip</span></span>         |
|<span data-ttu-id="8e2a5-130">Kapsayıcılar</span><span class="sxs-lookup"><span data-stu-id="8e2a5-130">Containers</span></span>             |<span data-ttu-id="8e2a5-131">[Docker CLI](https://github.com/docker/cli)/[Docker makine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="8e2a5-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="8e2a5-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="8e2a5-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="8e2a5-133">Taslak</span><span class="sxs-lookup"><span data-stu-id="8e2a5-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="8e2a5-134">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="8e2a5-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="8e2a5-135">Veritabanları</span><span class="sxs-lookup"><span data-stu-id="8e2a5-135">Databases</span></span>              |<span data-ttu-id="8e2a5-136">MySQL istemci</span><span class="sxs-lookup"><span data-stu-id="8e2a5-136">MySQL client</span></span><br> <span data-ttu-id="8e2a5-137">PostgreSql istemci</span><span class="sxs-lookup"><span data-stu-id="8e2a5-137">PostgreSql client</span></span><br> [<span data-ttu-id="8e2a5-138">SQLCMD yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="8e2a5-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="8e2a5-139">MSSQL komut dosyası yazarları</span><span class="sxs-lookup"><span data-stu-id="8e2a5-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="8e2a5-140">Diğer</span><span class="sxs-lookup"><span data-stu-id="8e2a5-140">Other</span></span>                  |<span data-ttu-id="8e2a5-141">iPython istemci</span><span class="sxs-lookup"><span data-stu-id="8e2a5-141">iPython Client</span></span><br> [<span data-ttu-id="8e2a5-142">Foundry CLI bulut</span><span class="sxs-lookup"><span data-stu-id="8e2a5-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="8e2a5-143">Dil desteği</span><span class="sxs-lookup"><span data-stu-id="8e2a5-143">Language support</span></span>
|<span data-ttu-id="8e2a5-144">Dil</span><span class="sxs-lookup"><span data-stu-id="8e2a5-144">Language</span></span>   |<span data-ttu-id="8e2a5-145">Sürüm</span><span class="sxs-lookup"><span data-stu-id="8e2a5-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="8e2a5-146">.NET</span><span class="sxs-lookup"><span data-stu-id="8e2a5-146">.NET</span></span>       |<span data-ttu-id="8e2a5-147">1.01</span><span class="sxs-lookup"><span data-stu-id="8e2a5-147">1.01</span></span>       |
|<span data-ttu-id="8e2a5-148">Başlayın</span><span class="sxs-lookup"><span data-stu-id="8e2a5-148">Go</span></span>         |<span data-ttu-id="8e2a5-149">1.7</span><span class="sxs-lookup"><span data-stu-id="8e2a5-149">1.7</span></span>        |
|<span data-ttu-id="8e2a5-150">Java</span><span class="sxs-lookup"><span data-stu-id="8e2a5-150">Java</span></span>       |<span data-ttu-id="8e2a5-151">1.8</span><span class="sxs-lookup"><span data-stu-id="8e2a5-151">1.8</span></span>        |
|<span data-ttu-id="8e2a5-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="8e2a5-152">Node.js</span></span>    |<span data-ttu-id="8e2a5-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="8e2a5-153">6.9.4</span></span>      |
|<span data-ttu-id="8e2a5-154">Python</span><span class="sxs-lookup"><span data-stu-id="8e2a5-154">Python</span></span>     |<span data-ttu-id="8e2a5-155">2.7 ve 3.5 (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="8e2a5-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="8e2a5-156">Güvenli otomatik kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8e2a5-156">Secure automatic authentication</span></span>
<span data-ttu-id="8e2a5-157">Bulut Kabuğu güvenli bir şekilde ve otomatik olarak hesap erişim için Azure CLI 2.0 kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="8e2a5-158">Azure dosyaları kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="8e2a5-158">Azure Files persistence</span></span>
<span data-ttu-id="8e2a5-159">Bulut Kabuğu'nu kullanarak geçici bir makine bir istek başına temelinde ayrıldığından dosyaları $Home ve makine durumu dışında oturumlarında kalıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="8e2a5-160">Dosyaları oturumlarında kalıcı hale getirmek için bulut Kabuk, ilk kez başlatıldığında Azure dosya paylaşımında ekleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="8e2a5-161">Bir kez tamamlanmış bulut Kabuk otomatik olarak tüm sonraki oturumlar için depolama alanınızı ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="8e2a5-162">Azure dosya paylaşımları için bulut Kabuk ekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="8e2a5-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="8e2a5-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e2a5-163">Next steps</span></span>
[<span data-ttu-id="8e2a5-164">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="8e2a5-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="8e2a5-165">
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="8e2a5-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>