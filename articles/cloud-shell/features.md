---
title: "aaaAzure bulut Kabuk (Önizleme) özellikleri | Microsoft Docs"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="0f8e9-103">Özellikler ve Araçlar Azure bulut Kabuğu</span><span class="sxs-lookup"><span data-stu-id="0f8e9-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="0f8e9-104">Azure bulut Kabuk tarayıcı tabanlı Kabuğu deneyiminin toomanage olduğunu ve Azure kaynaklarını geliştirin.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="0f8e9-105">Bulut Kabuk Kabuğu deneyiminin hello yükünü, sürümü, yükleme ve bir makineyi kendiniz koruma olmadan Azure kaynaklarını yönetmek için önceden yapılandırılmış, bir tarayıcı erişilebilir sunar.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="0f8e9-106">İstek başına temelinde makineler bulut Kabuk sağlar ve sonuç olarak makine durumu oturumlarında kalıcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="0f8e9-107">Bulut Kabuk etkileşimli oturumları için kurulu olduğundan Kabukları Kabuğu kaldıktan 20 dakika sonra otomatik olarak sonlanır.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="0f8e9-108">Bulut Kabuğu'nda bash</span><span class="sxs-lookup"><span data-stu-id="0f8e9-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="0f8e9-109">Araçlar</span><span class="sxs-lookup"><span data-stu-id="0f8e9-109">Tools</span></span>
|<span data-ttu-id="0f8e9-110">Kategori</span><span class="sxs-lookup"><span data-stu-id="0f8e9-110">Category</span></span>   |<span data-ttu-id="0f8e9-111">Ad</span><span class="sxs-lookup"><span data-stu-id="0f8e9-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="0f8e9-112">Linux Kabuk yorumlayıcı</span><span class="sxs-lookup"><span data-stu-id="0f8e9-112">Linux shell interpreter</span></span>|<span data-ttu-id="0f8e9-113">Bash</span><span class="sxs-lookup"><span data-stu-id="0f8e9-113">Bash</span></span><br> <span data-ttu-id="0f8e9-114">Paylaş</span><span class="sxs-lookup"><span data-stu-id="0f8e9-114">sh</span></span>               |
|<span data-ttu-id="0f8e9-115">Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="0f8e9-115">Azure tools</span></span>            |<span data-ttu-id="0f8e9-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) ve [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="0f8e9-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="0f8e9-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="0f8e9-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="0f8e9-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="0f8e9-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="0f8e9-119">Metin düzenleyiciler</span><span class="sxs-lookup"><span data-stu-id="0f8e9-119">Text editors</span></span>           |<span data-ttu-id="0f8e9-120">VIM</span><span class="sxs-lookup"><span data-stu-id="0f8e9-120">vim</span></span><br> <span data-ttu-id="0f8e9-121">nano</span><span class="sxs-lookup"><span data-stu-id="0f8e9-121">nano</span></span><br> <span data-ttu-id="0f8e9-122">emacs</span><span class="sxs-lookup"><span data-stu-id="0f8e9-122">emacs</span></span>       |
|<span data-ttu-id="0f8e9-123">Kaynak denetimi</span><span class="sxs-lookup"><span data-stu-id="0f8e9-123">Source control</span></span>         |<span data-ttu-id="0f8e9-124">Git</span><span class="sxs-lookup"><span data-stu-id="0f8e9-124">git</span></span>                    |
|<span data-ttu-id="0f8e9-125">Derleme araçları</span><span class="sxs-lookup"><span data-stu-id="0f8e9-125">Build tools</span></span>            |<span data-ttu-id="0f8e9-126">Yapma</span><span class="sxs-lookup"><span data-stu-id="0f8e9-126">make</span></span><br> <span data-ttu-id="0f8e9-127">maven</span><span class="sxs-lookup"><span data-stu-id="0f8e9-127">maven</span></span><br> <span data-ttu-id="0f8e9-128">npm</span><span class="sxs-lookup"><span data-stu-id="0f8e9-128">npm</span></span><br> <span data-ttu-id="0f8e9-129">PIP</span><span class="sxs-lookup"><span data-stu-id="0f8e9-129">pip</span></span>         |
|<span data-ttu-id="0f8e9-130">Kapsayıcılar</span><span class="sxs-lookup"><span data-stu-id="0f8e9-130">Containers</span></span>             |<span data-ttu-id="0f8e9-131">[Docker CLI](https://github.com/docker/cli)/[Docker makine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="0f8e9-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="0f8e9-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="0f8e9-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="0f8e9-133">Taslak</span><span class="sxs-lookup"><span data-stu-id="0f8e9-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="0f8e9-134">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="0f8e9-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="0f8e9-135">Veritabanları</span><span class="sxs-lookup"><span data-stu-id="0f8e9-135">Databases</span></span>              |<span data-ttu-id="0f8e9-136">MySQL istemci</span><span class="sxs-lookup"><span data-stu-id="0f8e9-136">MySQL client</span></span><br> <span data-ttu-id="0f8e9-137">PostgreSql istemci</span><span class="sxs-lookup"><span data-stu-id="0f8e9-137">PostgreSql client</span></span><br> [<span data-ttu-id="0f8e9-138">SQLCMD yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="0f8e9-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="0f8e9-139">MSSQL komut dosyası yazarları</span><span class="sxs-lookup"><span data-stu-id="0f8e9-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="0f8e9-140">Diğer</span><span class="sxs-lookup"><span data-stu-id="0f8e9-140">Other</span></span>                  |<span data-ttu-id="0f8e9-141">iPython istemci</span><span class="sxs-lookup"><span data-stu-id="0f8e9-141">iPython Client</span></span><br> [<span data-ttu-id="0f8e9-142">Foundry CLI bulut</span><span class="sxs-lookup"><span data-stu-id="0f8e9-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="0f8e9-143">Dil desteği</span><span class="sxs-lookup"><span data-stu-id="0f8e9-143">Language support</span></span>
|<span data-ttu-id="0f8e9-144">Dil</span><span class="sxs-lookup"><span data-stu-id="0f8e9-144">Language</span></span>   |<span data-ttu-id="0f8e9-145">Sürüm</span><span class="sxs-lookup"><span data-stu-id="0f8e9-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="0f8e9-146">.NET</span><span class="sxs-lookup"><span data-stu-id="0f8e9-146">.NET</span></span>       |<span data-ttu-id="0f8e9-147">1.01</span><span class="sxs-lookup"><span data-stu-id="0f8e9-147">1.01</span></span>       |
|<span data-ttu-id="0f8e9-148">Başlayın</span><span class="sxs-lookup"><span data-stu-id="0f8e9-148">Go</span></span>         |<span data-ttu-id="0f8e9-149">1.7</span><span class="sxs-lookup"><span data-stu-id="0f8e9-149">1.7</span></span>        |
|<span data-ttu-id="0f8e9-150">Java</span><span class="sxs-lookup"><span data-stu-id="0f8e9-150">Java</span></span>       |<span data-ttu-id="0f8e9-151">1.8</span><span class="sxs-lookup"><span data-stu-id="0f8e9-151">1.8</span></span>        |
|<span data-ttu-id="0f8e9-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="0f8e9-152">Node.js</span></span>    |<span data-ttu-id="0f8e9-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="0f8e9-153">6.9.4</span></span>      |
|<span data-ttu-id="0f8e9-154">Python</span><span class="sxs-lookup"><span data-stu-id="0f8e9-154">Python</span></span>     |<span data-ttu-id="0f8e9-155">2.7 ve 3.5 (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="0f8e9-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="0f8e9-156">Güvenli otomatik kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0f8e9-156">Secure automatic authentication</span></span>
<span data-ttu-id="0f8e9-157">Bulut Kabuk hesap erişim hello Azure CLI 2.0 için güvenli bir şekilde ve otomatik olarak doğrular.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="0f8e9-158">Azure dosyaları kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="0f8e9-158">Azure Files persistence</span></span>
<span data-ttu-id="0f8e9-159">Bulut Kabuğu'nu kullanarak geçici bir makine bir istek başına temelinde ayrıldığından dosyaları $Home ve makine durumu dışında oturumlarında kalıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="0f8e9-160">oturumlar, Azure dosya ekleme aracılığıyla paylaştığınız bulut Kabuk yetenekte, ilk başlatılırken arasında toopersist dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="0f8e9-161">Bir kez tamamlanmış bulut Kabuk otomatik olarak tüm sonraki oturumlar için depolama alanınızı ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="0f8e9-162">Azure dosya paylaşımları tooCloud Kabuk ekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0f8e9-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="0f8e9-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f8e9-163">Next steps</span></span>
[<span data-ttu-id="0f8e9-164">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="0f8e9-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="0f8e9-165">
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="0f8e9-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>