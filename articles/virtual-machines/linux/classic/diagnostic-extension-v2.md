---
title: "bir Linux VM VM uzantısı ile aaaMonitoring | Microsoft Docs"
description: "Toouse nasıl hello Linux tanılama uzantısını toomonitor hello performans ve Tanılama verileri azure'da bir Linux VM öğrenin."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="3d191-103">Merhaba Linux tanılama uzantısını toomonitor hello performans ve bir Linux VM tanılama verilerini kullanın</span><span class="sxs-lookup"><span data-stu-id="3d191-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="3d191-104">Bu belgede hello Linux tanılama uzantısını 2.3 sürümü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d191-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d191-105">Bu sürüm kullanım dışıdır ve 30 Haziran 2018 sonra her zaman yayımdan olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d191-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="3d191-106">3.0 sürümünde değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3d191-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="3d191-107">Daha fazla bilgi için bkz: Merhaba [hello Linux tanılama uzantısı sürüm 3.0 belgelerine](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3d191-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="3d191-108">Giriş</span><span class="sxs-lookup"><span data-stu-id="3d191-108">Introduction</span></span>

<span data-ttu-id="3d191-109">(**Not**: Linux tanılama uzantısını açık kaynaklıdır hello [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) burada hello en güncel bilgiler hello uzantısındaki ilk yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="3d191-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="3d191-110">Toocheck hello isteyebilirsiniz [GitHub sayfası](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) ilk.)</span><span class="sxs-lookup"><span data-stu-id="3d191-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="3d191-111">Merhaba Linux tanılama uzantısını kullanıcı İzleyicisi Merhaba Microsoft Azure üzerinde çalışan Linux VM'ler yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3d191-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="3d191-112">Hello aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="3d191-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="3d191-113">Toplar ve tanılama ve syslog bilgiler dahil olmak üzere hello Linux VM toohello kullanıcının depolama tablosundan hello sistem performans bilgileri yükler.</span><span class="sxs-lookup"><span data-stu-id="3d191-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="3d191-114">Toplanan ve karşıya kullanıcılar toocustomize hello veri ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d191-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="3d191-115">Kullanıcıların tooupload belirtilen günlük dosyaları tooa atanan depolama tablosu sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d191-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="3d191-116">Merhaba geçerli sürümde 2.3 hello verileri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3d191-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="3d191-117">Sistem, güvenlik ve uygulama günlükleri de dahil olmak üzere tüm Linux Rsyslog günlükleri.</span><span class="sxs-lookup"><span data-stu-id="3d191-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="3d191-118">Belirtilen tüm sistem verileri [hello System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3d191-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="3d191-119">Kullanıcı tarafından belirtilen günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3d191-119">User-specified log files.</span></span>

<span data-ttu-id="3d191-120">Bu uzantı hello Klasik ve Resource Manager dağıtım modelleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="3d191-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="3d191-121">Geçerli sürümünü hello uzantısı ve eski sürümleri kullanımdan kaldırma</span><span class="sxs-lookup"><span data-stu-id="3d191-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="3d191-122">Merhaba uzantısı'nın en son sürüm Hello **2.3**, ve **eski sürümlerini (2.0, 2.1 ve 2.2) kullanım dışı ve, bu yılın sonuna (2017) tarafından yayımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="3d191-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="3d191-123">Merhaba Linux tanılama uzantısını devre dışı otomatik alt sürüm yükseltme işlemine yüklediyseniz, hello uzantısı kaldırıp etkin otomatik alt sürüm yükseltme işlemine yeniden yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="3d191-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="3d191-124">Klasik (ASM) Vm'lerinde, bu hello uzantısı Azure XPLAT CLI veya Powershell aracılığıyla yüklüyorsanız '2.*' hello sürümü belirterek elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d191-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="3d191-125">ARM Vm'leri üzerinde bu dahil ederek elde edebilirsiniz ' "olan": true' hello VM Dağıtım şablonu olarak.</span><span class="sxs-lookup"><span data-stu-id="3d191-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="3d191-126">Ayrıca, tüm yeni uzantısını yükleme işlemi hello hello otomatik alt sürüm yükseltme seçeneği açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d191-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="3d191-127">Merhaba uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3d191-127">Enable hello extension</span></span>

<span data-ttu-id="3d191-128">Bu uzantı hello kullanarak etkinleştirebilirsiniz [Azure portal](https://portal.azure.com/#), Azure PowerShell veya Azure CLI komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3d191-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="3d191-129">tooview hello sistem yapılandırmanıza ve performans verileri doğrudan Azure portal hello izleyin [hello Azure blogu üzerinde aşağıdaki adımları](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="3d191-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="3d191-130">Bu makalede odaklanılmaktadır tooenable ve Azure CLI komutları kullanarak hello uzantısı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3d191-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="3d191-131">Bu, tooread ve görünüm hello verileri doğrudan hello depolama tablosu sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d191-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="3d191-132">Burada açıklanan hello yapılandırma yöntemleri hello Azure portal çalışmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3d191-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="3d191-133">tooview ve hello sistem ve performans verileri doğrudan hello Azure portal yapılandırma, hello uzantısı hello Portalı aracılığıyla etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d191-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d191-134">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d191-134">Prerequisites</span></span>

* <span data-ttu-id="3d191-135">**Azure Linux Aracısı sürüm 2.0.6 veya daha sonra**.</span><span class="sxs-lookup"><span data-stu-id="3d191-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="3d191-136">Çoğu Azure VM Linux galeri görüntüleri sürümü 2.0.6 dahil Not veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="3d191-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="3d191-137">Çalıştırabilirsiniz **WAAgent-sürüm** tooconfirm hangi sürümünün hello VM üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="3d191-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="3d191-138">Merhaba VM 2.0.6 önceki bir sürümünü çalıştırıyorsa, takip edebilirsiniz [github'daki bu yönergeleri](https://github.com/Azure/WALinuxAgent "yönergeleri") tooupdate onu.</span><span class="sxs-lookup"><span data-stu-id="3d191-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="3d191-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="3d191-139">**Azure CLI**.</span></span> <span data-ttu-id="3d191-140">İzleyin [CLI yüklemek için bu Kılavuzu](../../../cli-install-nodejs.md) hello Azure CLI çevresi makinenizde tooset.</span><span class="sxs-lookup"><span data-stu-id="3d191-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="3d191-141">Azure CLI yüklendikten sonra hello kullanabilirsiniz **azure** , komut satırı arabirimi (Bash, Terminal veya komut istemi) tooaccess hello Azure CLI komutlarının komutu.</span><span class="sxs-lookup"><span data-stu-id="3d191-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="3d191-142">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3d191-142">For example:</span></span>

  * <span data-ttu-id="3d191-143">Çalıştırma **azure vm uzantısı kümesi--Yardım** ayrıntılı yardım bilgi.</span><span class="sxs-lookup"><span data-stu-id="3d191-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="3d191-144">Çalıştırma **azure oturum açma** tooAzure toosign.</span><span class="sxs-lookup"><span data-stu-id="3d191-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="3d191-145">Çalıştırma **azure vm listesi** toolist tüm hello Azure üzerinde sahip sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="3d191-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="3d191-146">Depolama hesabı toostore hello verileri.</span><span class="sxs-lookup"><span data-stu-id="3d191-146">A storage account toostore hello data.</span></span> <span data-ttu-id="3d191-147">Daha önce oluşturulmuş bir depolama hesabı adı ve bir erişim anahtarı tooupload hello veri tooyour depolama gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d191-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="3d191-148">Hello Azure CLI komutu tooenable hello Linux tanılama uzantısını kullanın</span><span class="sxs-lookup"><span data-stu-id="3d191-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="3d191-149">Senaryo 1.</span><span class="sxs-lookup"><span data-stu-id="3d191-149">Scenario 1.</span></span> <span data-ttu-id="3d191-150">Merhaba varsayılan veri kümesi Hello uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3d191-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="3d191-151">2.3 veya sonraki sürümü içinde toplanacağını hello varsayılan veri içerir:</span><span class="sxs-lookup"><span data-stu-id="3d191-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="3d191-152">Tüm Rsyslog bilgileri (Sistem, güvenlik ve uygulama günlükleri dahil).</span><span class="sxs-lookup"><span data-stu-id="3d191-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="3d191-153">Temel sistem verileri çekirdek kümesi.</span><span class="sxs-lookup"><span data-stu-id="3d191-153">A core set of basis system data.</span></span> <span data-ttu-id="3d191-154">Tam veri kümesi hello Not üzerinde hello açıklanan [System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3d191-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="3d191-155">Tooenable isterseniz ek veriler devam senaryoları 2 ve 3'te hello adımlara.</span><span class="sxs-lookup"><span data-stu-id="3d191-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="3d191-156">1. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-156">Step 1.</span></span> <span data-ttu-id="3d191-157">Aşağıdaki hello ile PrivateConfig.json adlı bir dosya içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3d191-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="3d191-158">2. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-158">Step 2.</span></span> <span data-ttu-id="3d191-159">Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --özel yapılandırma yolu PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3d191-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="3d191-160">Senaryo 2.</span><span class="sxs-lookup"><span data-stu-id="3d191-160">Scenario 2.</span></span> <span data-ttu-id="3d191-161">Merhaba Performans İzleyicisi ölçümlerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3d191-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="3d191-162">Bu bölümde toocustomize nasıl hello performans ve tanı veri tablosu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d191-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="3d191-163">1. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-163">Step 1.</span></span> <span data-ttu-id="3d191-164">Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d191-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3d191-165">Ayrıca PublicConfig.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d191-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="3d191-166">Hello belirli veri toocollect istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="3d191-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="3d191-167">Desteklenen tüm sağlayıcıları ve değişkenleri için hello başvuru [System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="3d191-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="3d191-168">Birden çok sorgu sahip ve birden fazla tabloya daha fazla sorguları toohello komut dosyası eklenerek depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d191-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="3d191-169">Varsayılan olarak, her zaman hello Rsyslog verileri toplanır.</span><span class="sxs-lookup"><span data-stu-id="3d191-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="3d191-170">2. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-170">Step 2.</span></span> <span data-ttu-id="3d191-171">Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--özel yapılandırma yolu PrivateConfig.json--ortak yapılandırma yolu PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3d191-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="3d191-172">Senaryo 3.</span><span class="sxs-lookup"><span data-stu-id="3d191-172">Scenario 3.</span></span> <span data-ttu-id="3d191-173">Kendi günlük dosyalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3d191-173">Upload your own log files</span></span>

<span data-ttu-id="3d191-174">Bu bölümde, nasıl tooyour depolama hesabı toocollect ve karşıya yükleme belirli günlük dosyalarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="3d191-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="3d191-175">Her iki hello yolu tooyour günlük dosya ve hello günlüğünüzün toostore istediğiniz yere Merhaba tablonun adını toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d191-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="3d191-176">Birden çok dosya/tablo girişleri toohello betik ekleyerek, birden çok günlük dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d191-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="3d191-177">1. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-177">Step 1.</span></span> <span data-ttu-id="3d191-178">Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d191-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3d191-179">Ardından aşağıdaki hello ile PublicConfig.json adlı başka bir dosya içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3d191-179">Then create another file named PublicConfig.json with hello following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="3d191-180">2. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-180">Step 2.</span></span> <span data-ttu-id="3d191-181">`azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3d191-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="3d191-182">Tüm günlükleri çok yazılmış hello uzantısı sürümleri önceki too2.3, bu ayarı ile unutmayın`/var/log/mysql.err` çok yinelenen`/var/log/syslog` (veya `/var/log/messages` hello Linux distro bağlı olarak) de.</span><span class="sxs-lookup"><span data-stu-id="3d191-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="3d191-183">Günlüğü bu yinelenen tooavoid kullanmak isterseniz, günlüğe dışlayabilirsiniz `local6` tesis rsyslog yapılandırmanızda günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3d191-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="3d191-184">Merhaba Linux distro üzerinde bağlıdır, ancak bir Ubuntu 14.04 sistemde hello dosya toomodify dir `/etc/rsyslog.d/50-default.conf` ve hello satır değiştirebilirsiniz `*.*;auth,authpriv.none -/var/log/syslog` çok`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="3d191-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="3d191-185">Merhaba en son düzeltme sürümünde 2.3 (2.3.9007), bu sorun düzeltilene şekilde hello uzantısı sürüm 2.3 varsa, bu sorun değil gerçekleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="3d191-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="3d191-186">Hala bile VM'yi yeniden başlatıldıktan sonra varsa, lütfen bizimle iletişime geçin ve hello en son düzeltme sürümü otomatik olarak yüklenmez neden gidermenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="3d191-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="3d191-187">Senaryo 4.</span><span class="sxs-lookup"><span data-stu-id="3d191-187">Scenario 4.</span></span> <span data-ttu-id="3d191-188">Herhangi bir günlük toplama gelen hello uzantısı Durdur</span><span class="sxs-lookup"><span data-stu-id="3d191-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="3d191-189">Bu bölümde, nasıl toplama gelen toostop hello uzantı günlükleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d191-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="3d191-190">İzleme Aracısı işlemi hello Not hala hazır ve çalışır bile bu yeniden yapılandırmaya olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3d191-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="3d191-191">İzleme Aracısı işlemi tamamen toostop hello isterseniz hello uzantı devre dışı bırakarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d191-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="3d191-192">Merhaba komutu toodisable hello uzantısı `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="3d191-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="3d191-193">1. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-193">Step 1.</span></span> <span data-ttu-id="3d191-194">Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d191-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="3d191-195">Aşağıdaki hello ile PublicConfig.json adlı başka bir dosya içerik oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3d191-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="3d191-196">2. Adım</span><span class="sxs-lookup"><span data-stu-id="3d191-196">Step 2.</span></span> <span data-ttu-id="3d191-197">Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--özel yapılandırma yolu PrivateConfig.json--ortak yapılandırma yolu PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="3d191-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="3d191-198">Verilerinizi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="3d191-198">Review your data</span></span>

<span data-ttu-id="3d191-199">Merhaba performans ve tanılama verilerini bir Azure Storage tablosunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="3d191-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="3d191-200">Gözden geçirme [nasıl toouse Ruby Azure tablo depolamasından](../../../cosmos-db/table-storage-how-to-use-ruby.md) hello depolama tooaccess hello verileri nasıl tablo Azure CLI komut dosyalarını kullanarak toolearn.</span><span class="sxs-lookup"><span data-stu-id="3d191-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="3d191-201">Ayrıca, kullanıcı Arabirimi araçlarını tooaccess hello verileri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3d191-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="3d191-202">Visual Studio Sunucu Gezgini.</span><span class="sxs-lookup"><span data-stu-id="3d191-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="3d191-203">Tooyour depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="3d191-203">Go tooyour storage account.</span></span> <span data-ttu-id="3d191-204">Merhaba VM yaklaşık beş dakika boyunca çalıştıktan sonra hello dört varsayılan tabloları görürsünüz: "LinuxCpu", "LinuxDisk", "LinuxMemory" ve "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="3d191-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="3d191-205">Merhaba tablo adları tooview hello verileri çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3d191-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="3d191-206">[Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/ "Azure Storage Gezgini").</span><span class="sxs-lookup"><span data-stu-id="3d191-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![Görüntü](./media/diagnostic-extension/no1.png)

<span data-ttu-id="3d191-208">FileCfg veya (senaryoları 2 ve 3'te açıklandığı gibi) perfCfg etkinleştirdiyseniz, Visual Studio Sunucu Gezgini ve Azure Storage Gezgini tooview varsayılan olmayan verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d191-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3d191-209">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3d191-209">Known issues</span></span>

* <span data-ttu-id="3d191-210">Rsyslog bilgi hello ve müşteri tarafından belirtilen günlük dosyası yalnızca komut dosyası aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="3d191-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
