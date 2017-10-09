---
title: "aaaScript Hdınsight - Azure ile eylemi geliştirme | Microsoft Docs"
description: "Betik eylemi ile nasıl toocustomize Hadoop kümeleri hakkında bilgi edinin. Betik eylemi bir kümeye yüklü uygulamaların Hadoop küme veya toochange hello yapılandırması üzerinde çalışan kullanılan tooinstall ek yazılım olabilir."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="68249-104">Hdınsight Windows tabanlı kümeler için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="68249-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="68249-105">Hdınsight için nasıl toowrite betik eylemi komutlar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="68249-105">Learn how toowrite Script Action scripts for HDInsight.</span></span> <span data-ttu-id="68249-106">Betik eylemi komut dosyalarını kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="68249-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="68249-107">Linux tabanlı Hdınsight kümeleri için yazılmış aynı makalenin Merhaba bkz [Hdınsight betik eylemi geliştirme betikleri](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="68249-107">For hello same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="68249-108">Bu belge yalnızca iş için Windows tabanlı Hdınsight kümeleri Hello adımları.</span><span class="sxs-lookup"><span data-stu-id="68249-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="68249-109">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="68249-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="68249-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="68249-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="68249-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="68249-112">Betik eylemleri Linux tabanlı kümelerde ile kullanma hakkında daha fazla bilgi için bkz: [(Linux) Hdınsight ile betik eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="68249-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="68249-113">Betik eylemi bir kümeye yüklü uygulamaların Hadoop küme veya toochange hello yapılandırması üzerinde çalışan kullanılan tooinstall ek yazılım olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-113">Script Action can be used tooinstall additional software running on a Hadoop cluster or toochange hello configuration of applications installed on a cluster.</span></span> <span data-ttu-id="68249-114">Betik eylemleri Hdınsight kümeleri dağıtıldığında hello küme düğümleri üzerinde çalışan bir komut dosyası olan ve hello kümedeki düğümler Hdınsight yapılandırmasını tamamladıktan sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="68249-114">Script actions are scripts that run on hello cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in hello cluster complete HDInsight configuration.</span></span> <span data-ttu-id="68249-115">Betik eylemi sistem yönetici hesabı ayrıcalıklarıyla yürütülür ve tam erişim hakları toohello küme düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="68249-115">A script action is executed under system admin account privileges and provides full access rights toohello cluster nodes.</span></span> <span data-ttu-id="68249-116">Her küme, belirtilen hello sırayla yürütülen betik eylemleri toobe listesiyle sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-116">Each cluster can be provided with a list of script actions toobe executed in hello order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="68249-117">Aşağıdaki hata iletisini hello karşılaşırsanız:</span><span class="sxs-lookup"><span data-stu-id="68249-117">If you experience hello following error message:</span></span>
>
> <span data-ttu-id="68249-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello terim 'Kaydet-HDIFile' hello adı cmdlet, işlev, komut dosyası veya çalıştırılabilir program olarak tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="68249-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : hello term 'Save-HDIFile' is not recognized as hello name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="68249-119">Merhaba hello adının yazımını denetleyin veya bir yol birlikte verildiyse, o hello yolun doğru olduğunu doğrulayın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="68249-119">Check hello spelling of hello name, or if a path was included, verify that hello path is correct and try again.</span></span>
> <span data-ttu-id="68249-120">Merhaba yardımcı yöntemler eklemediniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="68249-120">It is because you didn't include hello helper methods.</span></span>  <span data-ttu-id="68249-121">Bkz: [özel komut dosyaları için yardımcı yöntemleri](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span><span class="sxs-lookup"><span data-stu-id="68249-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="68249-122">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="68249-122">Sample scripts</span></span>
<span data-ttu-id="68249-123">Windows işletim sisteminde Hdınsight kümeleri oluşturmak için hello betik eylemi Azure PowerShell komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="68249-123">For creating HDInsight clusters on Windows operating system, hello Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="68249-124">Merhaba aşağıdaki betiği hello site yapılandırma dosyalarını yapılandırmaya ilişkin bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="68249-124">hello following script is a sample for configuring hello site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="68249-125">Merhaba betiği dört parametreleri, hello yapılandırma dosyasının adını, toomodify, tooset ve bir açıklama istediğiniz hello değeri istediğiniz hello özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="68249-125">hello script takes four parameters, hello configuration file name, hello property you want toomodify, hello value you want tooset, and a description.</span></span> <span data-ttu-id="68249-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="68249-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="68249-127">Bu parametreler hello hive-site.xml dosyasında hello hive.metastore.client.socket.timeout değeri too90 ayarlar.</span><span class="sxs-lookup"><span data-stu-id="68249-127">These parameters sets hello hive.metastore.client.socket.timeout value too90 in hello hive-site.xml file.</span></span>  <span data-ttu-id="68249-128">Merhaba varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="68249-128">hello default value is 60 seconds.</span></span>

<span data-ttu-id="68249-129">Bu örnek komut dosyası ayrıca bulunabilir [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span><span class="sxs-lookup"><span data-stu-id="68249-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="68249-130">Hdınsight birkaç betikler Hdınsight kümelerinde tooinstall ek bileşenleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="68249-130">HDInsight provides several scripts tooinstall additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="68249-131">Ad</span><span class="sxs-lookup"><span data-stu-id="68249-131">Name</span></span> | <span data-ttu-id="68249-132">Betik</span><span class="sxs-lookup"><span data-stu-id="68249-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="68249-133">**Spark yükleyin**</span><span class="sxs-lookup"><span data-stu-id="68249-133">**Install Spark**</span></span> |<span data-ttu-id="68249-134">https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="68249-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="68249-135">Bkz: [yükleme ve kullanma hdınsight'ta Spark kümeleri][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="68249-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="68249-136">**R yükleme**</span><span class="sxs-lookup"><span data-stu-id="68249-136">**Install R**</span></span> |<span data-ttu-id="68249-137">https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="68249-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="68249-138">Bkz: [yükleme ve kullanma R Hdınsight kümelerinde][hdinsight-r-scripts].</span><span class="sxs-lookup"><span data-stu-id="68249-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="68249-139">**Solr yükleyin**</span><span class="sxs-lookup"><span data-stu-id="68249-139">**Install Solr**</span></span> |<span data-ttu-id="68249-140">https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="68249-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="68249-141">Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="68249-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="68249-142">- **Giraph yükleyin**</span><span class="sxs-lookup"><span data-stu-id="68249-142">- **Install Giraph**</span></span> |<span data-ttu-id="68249-143">https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="68249-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="68249-144">Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="68249-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="68249-145">Betik eylemi hello Azure portal, Azure PowerShell dağıtılabilir veya Hdınsight .NET SDK kullanarak hello.</span><span class="sxs-lookup"><span data-stu-id="68249-145">Script Action can be deployed from hello Azure portal, Azure PowerShell or by using hello HDInsight .NET SDK.</span></span>  <span data-ttu-id="68249-146">Daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak][hdinsight-cluster-customize].</span><span class="sxs-lookup"><span data-stu-id="68249-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="68249-147">Merhaba örnek betikler yalnızca Hdınsight kümesi sürüm 3.1 veya üzeri çalışır.</span><span class="sxs-lookup"><span data-stu-id="68249-147">hello sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="68249-148">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="68249-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="68249-149">Özel komut dosyaları için yardımcı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="68249-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="68249-150">Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir.</span><span class="sxs-lookup"><span data-stu-id="68249-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="68249-151">Bu yöntemler tanımlanan [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), komut dosyalarınızı örnek aşağıdaki hello kullanarak eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="68249-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using hello following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="68249-152">Bu komut dosyası tarafından sağlanan hello yardımcı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="68249-152">Here are hello helper methods that are provided by this script:</span></span>

| <span data-ttu-id="68249-153">Yardımcı yöntemi</span><span class="sxs-lookup"><span data-stu-id="68249-153">Helper method</span></span> | <span data-ttu-id="68249-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="68249-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68249-155">**Kaydet-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="68249-155">**Save-HDIFile**</span></span> |<span data-ttu-id="68249-156">İndirme hello dosyasından Tekdüzen Kaynak Tanımlayıcısı (URI) tooa konumu hello Azure VM düğümü atanan toohello kümesi ile ilişkili hello yerel diskte belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="68249-156">Download a file from hello specified Uniform Resource Identifier (URI) tooa location on hello local disk that is associated with hello Azure VM node assigned toohello cluster.</span></span> |
| <span data-ttu-id="68249-157">**Genişletme HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="68249-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="68249-158">Sıkıştırılmış bir dosya sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="68249-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="68249-159">**Çağırma HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="68249-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="68249-160">Bir komut dosyası cmd.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="68249-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="68249-161">**Yazma HDILog**</span><span class="sxs-lookup"><span data-stu-id="68249-161">**Write-HDILog**</span></span> |<span data-ttu-id="68249-162">Bir komut dosyası eylemi için kullanılan hello özel komut dosyasından çıkış yazma.</span><span class="sxs-lookup"><span data-stu-id="68249-162">Write output from hello custom script used for a script action.</span></span> |
| <span data-ttu-id="68249-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="68249-163">**Get-Services**</span></span> |<span data-ttu-id="68249-164">Burada hello betiği yürüten hello makine üzerinde çalışan hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="68249-164">Get a list of services running on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="68249-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="68249-165">**Get-Service**</span></span> |<span data-ttu-id="68249-166">Giriş olarak Hello belirli hizmet adı ile belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) hello makinede burada hello betik yürütür.</span><span class="sxs-lookup"><span data-stu-id="68249-166">With hello specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="68249-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="68249-167">**Get-HDIServices**</span></span> |<span data-ttu-id="68249-168">Burada hello betiği yürüten hello bilgisayarda çalışan Hdınsight hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="68249-168">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="68249-169">**Get-HDIService**</span></span> |<span data-ttu-id="68249-170">Merhaba belirli Hdınsight hizmet adı ile giriş olarak, belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) hello makinede burada hello betik yürütür.</span><span class="sxs-lookup"><span data-stu-id="68249-170">With hello specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="68249-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="68249-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="68249-172">Burada hello betiği yürüten hello bilgisayarda çalışan hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="68249-172">Get a list of services that are running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="68249-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="68249-174">Burada hello betiği yürüten (adına göre) belirli bir hizmet hello bilgisayarda çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-174">Check if a specific service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="68249-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="68249-176">Burada hello betiği yürüten hello bilgisayarda çalışan Hdınsight hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="68249-176">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="68249-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="68249-178">Burada hello betiği yürüten (adına göre) belirli bir Hdınsight hizmet hello bilgisayarda çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-178">Check if a specific HDInsight service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="68249-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="68249-180">Burada hello betiği yürüten hello bilgisayarda yüklü Hadoop Hello sürümünü alır.</span><span class="sxs-lookup"><span data-stu-id="68249-180">Get hello version of Hadoop installed on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="68249-181">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="68249-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="68249-182">Merhaba bilgisayar burada hello betiği yürüten bir baş düğüm olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-182">Check if hello computer where hello script executes is a head node.</span></span> |
| <span data-ttu-id="68249-183">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="68249-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="68249-184">Burada hello betiği yürüten hello bilgisayar etkin bir baş düğüm olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-184">Check if hello computer where hello script executes is an active head node.</span></span> |
| <span data-ttu-id="68249-185">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="68249-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="68249-186">Burada hello betiği yürüten hello bilgisayar veri düğümü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-186">Check if hello computer where hello script executes is a data node.</span></span> |
| <span data-ttu-id="68249-187">**Düzen HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="68249-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="68249-188">Merhaba yapılandırma dosyaları hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml veya yarn-site.xml düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-188">Edit hello config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="68249-189">Komut dosyası geliştirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="68249-189">Best practices for script development</span></span>
<span data-ttu-id="68249-190">Hdınsight kümesi için özel bir komut dosyası geliştirirken göz önünde birkaç en iyi yöntemler tookeep vardır:</span><span class="sxs-lookup"><span data-stu-id="68249-190">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* <span data-ttu-id="68249-191">Merhaba Hadoop sürüm denetimi</span><span class="sxs-lookup"><span data-stu-id="68249-191">Check for hello Hadoop version</span></span>

    <span data-ttu-id="68249-192">Yalnızca Hdınsight sürüm 3.1 (Hadoop 2.4) ve betik eylemi tooinstall özel bileşenleri kullanan bir kümede desteği üstünde.</span><span class="sxs-lookup"><span data-stu-id="68249-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action tooinstall custom components on a cluster.</span></span> <span data-ttu-id="68249-193">Özel betiğinizde hello kullanmalısınız **Get-HDIHadoopVersion** yardımcı yöntem toocheck hello Hadoop sürüm hello komut dosyasında diğer görevleri gerçekleştirme ile devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="68249-193">In your custom script, you must use hello **Get-HDIHadoopVersion** helper method toocheck hello Hadoop version before proceeding with performing other tasks in hello script.</span></span>
* <span data-ttu-id="68249-194">Kararlı tooscript kaynaklara bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="68249-194">Provide stable links tooscript resources</span></span>

    <span data-ttu-id="68249-195">Kullanıcılar tüm hello betikler ve bir küme hello özelleştirmesinde kullanılan diğer yapıları hello küme hello ömrü kullanılabilir kalmasını ve bu dosyaların sürümleri hello hello süresince değiştirmeyin emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-195">Users should make sure that all hello scripts and other artifacts used in hello customization of a cluster remain available throughout hello lifetime of hello cluster and that hello versions of these files do not change for hello duration.</span></span> <span data-ttu-id="68249-196">Merhaba kümedeki düğümlerin Hello yeniden görüntüsünü oluşturuyor gerekliyse, bu kaynakları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="68249-196">These resources are required if hello reimaging of nodes in hello cluster is required.</span></span> <span data-ttu-id="68249-197">Merhaba en iyi uygulama toodownload olduğunu ve kullanıcı denetimleri hello depolama hesabındaki her şeyi arşivleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-197">hello best practice is toodownload and archive everything in a Storage account that hello user controls.</span></span> <span data-ttu-id="68249-198">Bu hello varsayılan depolama hesabı ya da herhangi bir anda hello dağıtımının özelleştirilmiş bir küme için belirtilen hello ek depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-198">This can be hello default Storage account or any of hello additional Storage accounts specified at hello time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="68249-199">Merhaba belgelerinde, örneğin, biz hello kaynakları yerel bir kopyasını bu depolama hesabında yapmış olduğunuz sağlanan hello Spark ve R küme örnekleri özelleştirilmiş: https://hdiconfigactions.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="68249-199">In hello Spark and R customized cluster samples provided in hello documentation, for example, we have made a local copy of hello resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="68249-200">Komut dosyasını Hello kümede özelleştirme ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="68249-200">Ensure that hello cluster customization script is idempotent</span></span>

    <span data-ttu-id="68249-201">Hdınsight kümesi hello düğümlerinin hello küme ömrü boyunca yeniden olduğunu beklediğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-201">You must expect that hello nodes of an HDInsight cluster is reimaged during hello cluster lifetime.</span></span> <span data-ttu-id="68249-202">bir küme yeniden her hello küme özelleştirme betiği çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="68249-202">hello cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="68249-203">Bu komut dosyası tasarlanmış toobe ıdempotent yeniden görüntüsünü oluşturuyor bağlı hello betik bu hello küme aynı yalnızca hello betik Merhaba zaman hello küme başlangıçta olan ilk kez çalıştırdıktan sonra durumla durumu özelleştirilmiş toohello döndürülür emin olması hello herkese açık olması gerekir oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="68249-203">This script must be designed toobe idempotent in hello sense that upon reimaging, hello script should ensure that hello cluster is returned toohello same customized state that it was in just after hello script ran for hello first time when hello cluster was initially created.</span></span> <span data-ttu-id="68249-204">Örneğin, özel bir komut dosyası D:\AppLocation uygulama yüklerseniz, ilk çalıştırın, sonra yeniden görüntüsünü oluşturuyor, bağlı her sonraki çalıştırmada hello betik Merhaba uygulaması hello D:\AppLocation konumu diğer işlemine devam etmeden önce mevcut olup olmadığını denetlemeniz gerekir Merhaba betik adımları.</span><span class="sxs-lookup"><span data-stu-id="68249-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, hello script should check whether hello application exists at hello D:\AppLocation location before proceeding with other steps in hello script.</span></span>
* <span data-ttu-id="68249-205">Merhaba en iyi konumda özel bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="68249-205">Install custom components in hello optimal location</span></span>

    <span data-ttu-id="68249-206">Küme düğümleri yeniden zaman hello C:\ kaynak sürücüde ve D:\ sistem sürücüsünde, hello veri kaybına ve bu sürücülerde yüklemiş olduğu uygulamalar sonuçta yeniden biçimlendirilebileceği.</span><span class="sxs-lookup"><span data-stu-id="68249-206">When cluster nodes are reimaged, hello C:\ resource drive and D:\ system drive can be reformatted, resulting in hello loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="68249-207">Merhaba kümesinin parçası olan bir Azure sanal makine (VM) düğüm arıza ve yeni bir düğüm tarafından değiştirilirse bu de olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-207">This could also happen if an Azure virtual machine (VM) node that is part of hello cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="68249-208">Merhaba D:\ sürücüsüne veya hello C:\apps konumda hello küme bileşenleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68249-208">You can install components on hello D:\ drive or in hello C:\apps location on hello cluster.</span></span> <span data-ttu-id="68249-209">Diğer tüm konumlara hello C:\ sürücüsü üzerindeki ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="68249-209">All other locations on hello C:\ drive are reserved.</span></span> <span data-ttu-id="68249-210">Uygulamaları veya kitaplıkları toobe komut dosyasını hello kümede özelleştirme yüklü olduğu hello konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="68249-210">Specify hello location where applications or libraries are toobe installed in hello cluster customization script.</span></span>
* <span data-ttu-id="68249-211">Yüksek kullanılabilirlik hello küme mimarisinin emin olun</span><span class="sxs-lookup"><span data-stu-id="68249-211">Ensure high availability of hello cluster architecture</span></span>

    <span data-ttu-id="68249-212">Yüksek kullanılabilirlik için bir Aktif-Pasif mimari Hdınsight sahipse, hangi bir baş düğüm (Merhaba Hdınsight Hizmetleri çalıştırdığınız) etkin modda hello diğer olup baş düğüm (hangi Hdınsight'ta Hizmetleri çalışmıyor) bekleme modunda olur.</span><span class="sxs-lookup"><span data-stu-id="68249-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where hello HDInsight services are running) and hello other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="68249-213">Hdınsight Hizmetleri kesilirse hello düğümleri etkin ve Pasif modları.</span><span class="sxs-lookup"><span data-stu-id="68249-213">hello nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="68249-214">Betik eylemi yüksek kullanılabilirlik için iki baş düğümler üzerinde kullanılan tooinstall Hizmetleri ise, o hello Hdınsight yük devretme mekanizması mümkün tooautomatically başarısız bu kullanıcı tarafından yüklenen hizmetleri olup olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68249-214">If a script action is used tooinstall services on both head nodes for high availability, note that hello HDInsight failover mechanism is not able tooautomatically fail over these user-installed services.</span></span> <span data-ttu-id="68249-215">Bu nedenle kullanıcı yüklü hizmetler beklenen toobe yüksek oranda kullanılabilir olan Hdınsight baş düğümler üzerinde kendi Aktif-Pasif modu, yük devretme yönteminde sahip veya etkin-etkin modunda olması.</span><span class="sxs-lookup"><span data-stu-id="68249-215">So user-installed services on HDInsight head nodes that are expected toobe highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="68249-216">Merhaba baş düğüm rolünü hello değer olarak belirtildiğinde bir Hdınsight betik eylemi komutu her iki baş düğümler üzerinde çalışır *ClusterRoleCollection* parametresi.</span><span class="sxs-lookup"><span data-stu-id="68249-216">An HDInsight Script Action command runs on both head nodes when hello head-node role is specified as a value in hello *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="68249-217">Bu nedenle özel bir komut dosyası tasarlarken, kodunuzu bu kurulumu farkında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="68249-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="68249-218">Burada hello aynı hizmetleri yüklenir ve her iki hello baş düğümü üzerinde başlatıldı ve birbirleri ile rekabet bitiş sorunlar çalışmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="68249-218">You should not run into problems where hello same services are installed and started on both of hello head nodes and they end up competing with each other.</span></span> <span data-ttu-id="68249-219">Betik eylemi yüklenen yazılım toobe dayanıklı toosuch olayları nedenle Ayrıca, yeniden görüntüleme sırasında veri kaybı olmamasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="68249-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has toobe resilient toosuch events.</span></span> <span data-ttu-id="68249-220">Uygulamaları birçok düğümüne dağıtılmış yüksek oranda kullanılabilir verilerle tasarlanmış toowork olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="68249-220">Applications should be designed toowork with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="68249-221">Hello kadar 1/5 bir kümede hello düğümlerinin yeniden olduğunu unutmayın aynı anda.</span><span class="sxs-lookup"><span data-stu-id="68249-221">Note that as many as 1/5 of hello nodes in a cluster can be reimaged at hello same time.</span></span>
* <span data-ttu-id="68249-222">Merhaba özel bileşenler toouse Azure Blob depolama alanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="68249-222">Configure hello custom components toouse Azure Blob storage</span></span>

    <span data-ttu-id="68249-223">Merhaba küme düğümlerine yükleyin hello özel bileşenler varsayılan yapılandırma toouse Hadoop dağıtılmış dosya sistemi (HDFS) depolama olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-223">hello custom components that you install on hello cluster nodes might have a default configuration toouse Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="68249-224">Bunun yerine hello yapılandırma toouse Azure Blob Depolama değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-224">You should change hello configuration toouse Azure Blob storage instead.</span></span> <span data-ttu-id="68249-225">Bir küme yeniden görüntü oluşturma, hello HDFS dosya sistemi ile biçimlendirilmiş ve orada depolanan tüm verileri kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="68249-225">On a cluster reimage, hello HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="68249-226">Azure Blob storage kullanarak, bunun yerine, verilerinizi tutulur sağlar.</span><span class="sxs-lookup"><span data-stu-id="68249-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="68249-227">Genel kullanım desenleri</span><span class="sxs-lookup"><span data-stu-id="68249-227">Common usage patterns</span></span>
<span data-ttu-id="68249-228">Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilecek hello ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="68249-228">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="68249-229">Ortam değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="68249-229">Configure environment variables</span></span>
<span data-ttu-id="68249-230">Genellikle betik eylemi geliştirme tooset ortam değişkenleri gereksinim hello düşündüğünüz.</span><span class="sxs-lookup"><span data-stu-id="68249-230">Often in script action development, you feel hello need tooset environment variables.</span></span> <span data-ttu-id="68249-231">Bir ikili dış sitesinden, hello kümede yüklemek ve yüklü tooyour 'PATH' ortam değişkeni olduğu, hello konumu eklediğinizde örneği için en olası senaryodur.</span><span class="sxs-lookup"><span data-stu-id="68249-231">For instance, a most likely scenario is when you download a binary from an external site, install it on hello cluster, and add hello location of where it is installed tooyour ‘PATH’ environment variable.</span></span> <span data-ttu-id="68249-232">Aşağıdaki kod parçacığında hello nasıl özel bir komut dosyası tooset ortam değişkenleri hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="68249-232">hello following snippet shows you how tooset environment variables in hello custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="68249-233">Bu bildirimi hello ortam değişkenini ayarlar **MDS_RUNNER_CUSTOM_CLUSTER** toohello değeri 'true' ve ayrıca kümeleri hello Bu değişken toobe makine genelinde kapsamı.</span><span class="sxs-lookup"><span data-stu-id="68249-233">This statement sets hello environment variable **MDS_RUNNER_CUSTOM_CLUSTER** toohello value 'true' and also sets hello scope of this variable toobe machine-wide.</span></span> <span data-ttu-id="68249-234">Zaman zaman ortam değişkenleri hello uygun kapsamda – makine ya da kullanıcı ayarlanır önemlidir.</span><span class="sxs-lookup"><span data-stu-id="68249-234">At times it is important that environment variables are set at hello appropriate scope – machine or user.</span></span> <span data-ttu-id="68249-235">Başvuru [burada] [ 1] ortam değişkenlerini ayarlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="68249-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="68249-236">Merhaba özel komut dosyalarının depolandığı toolocations erişim</span><span class="sxs-lookup"><span data-stu-id="68249-236">Access toolocations where hello custom scripts are stored</span></span>
<span data-ttu-id="68249-237">Kullanılan komut toocustomize küme gereksinimlerini tooeither hello küme için hello varsayılan depolama hesabı veya başka bir depolama hesabı üzerinde genel bir salt okunur kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-237">Scripts used toocustomize a cluster needs tooeither be in hello default storage account for hello cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="68249-238">Kodunuzu başka bir yerde bulunan kaynaklara erişirse bu genel olarak erişilebilir içinde toobe gerekir (en az genel salt okunur).</span><span class="sxs-lookup"><span data-stu-id="68249-238">If your script accesses resources located elsewhere these need toobe in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="68249-239">Örneği için bir dosya tooaccess istediğiniz ve hello SaveFile HDI komutunu kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="68249-239">For instance you might want tooaccess a file and save it using hello SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="68249-240">Bu örnekte, bu hello kapsayıcı 'somestorageaccount' depolama hesabındaki ' somecontainer' genel olarak erişilebilir olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="68249-240">In this example, you must ensure that hello container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="68249-241">Aksi takdirde hello betik 'Bulunamadı' bir özel durum oluşturur ve başarısız.</span><span class="sxs-lookup"><span data-stu-id="68249-241">Otherwise, hello script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="68249-242">Parametreleri toohello Ekle-AzureRmHDInsightScriptAction cmdlet'i geçirin</span><span class="sxs-lookup"><span data-stu-id="68249-242">Pass parameters toohello Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="68249-243">toopass birden çok parametre toohello Ekle-AzureRmHDInsightScriptAction cmdlet'i hello komut dosyası için tüm parametreleri tooformat hello dize değeri toocontain gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-243">toopass multiple parameters toohello Add-AzureRmHDInsightScriptAction cmdlet, you need tooformat hello string value toocontain all parameters for hello script.</span></span> <span data-ttu-id="68249-244">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="68249-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="68249-245">or</span><span class="sxs-lookup"><span data-stu-id="68249-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="68249-246">Başarısız Küme dağıtımı için özel durum</span><span class="sxs-lookup"><span data-stu-id="68249-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="68249-247">Tooget doğru şekilde hello olgu bildirim istiyorsanız o küme özelleştirme beklendiği gibi başarılı olmadı, önemli toothrow bir işlemdir ve hello küme oluşturma işlemi başarısız.</span><span class="sxs-lookup"><span data-stu-id="68249-247">If you want tooget accurately notified of hello fact that cluster customization did not succeed as expected, it is important toothrow an exception and fail hello cluster creation.</span></span> <span data-ttu-id="68249-248">Örneğin, tooprocess bir dosya varsa istediğiniz ve burada hello dosya yok hello hata durumu işlemek.</span><span class="sxs-lookup"><span data-stu-id="68249-248">For instance, you might want tooprocess a file if it exists and handle hello error case where hello file does not exist.</span></span> <span data-ttu-id="68249-249">Bu, başlangıç komut dosyası düzgün biçimde çıkar ve hello kümenin hello durumunu doğru şekilde bilinen emin olun.</span><span class="sxs-lookup"><span data-stu-id="68249-249">This would ensure that hello script exits gracefully and hello state of hello cluster is correctly known.</span></span> <span data-ttu-id="68249-250">Merhaba aşağıdaki kod parçacığında verir nasıl bir örnek tooachieve bu:</span><span class="sxs-lookup"><span data-stu-id="68249-250">hello following snippet gives an example of how tooachieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="68249-251">Merhaba dosya olmasaydı, bu parçacığında, bunu burada hello komut gerçekte düzgün biçimde hello hata iletisini yazdırdıktan sonra çıkar ve hello küme "başarılı" Küme özelleştirme işlemi tamamlandı varsayılarak çalışır duruma ulaştığında tooa durumu yol açar.</span><span class="sxs-lookup"><span data-stu-id="68249-251">In this snippet, if hello file did not exist, it would lead tooa state where hello script actually exits gracefully after printing hello error message, and hello cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="68249-252">Toobe doğru şekilde hello olgu bildirim istiyorsanız, o küme özelleştirme temelde eksik dosya nedeniyle beklendiği gibi başarılı olmadı, daha uygun toothrow bir işlemdir ve hello küme özelleştirme adımı başarısız.</span><span class="sxs-lookup"><span data-stu-id="68249-252">If you want toobe accurately notified of hello fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate toothrow an exception and fail hello cluster customization step.</span></span> <span data-ttu-id="68249-253">tooachieve Bu örnek kod parçacığını bunun yerine aşağıdaki hello kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-253">tooachieve this you must use hello following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="68249-254">Betik eylemi dağıtma denetim listesi</span><span class="sxs-lookup"><span data-stu-id="68249-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="68249-255">Biz toodeploy bu komut dosyalarını hazırlanırken sürdü hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="68249-255">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

1. <span data-ttu-id="68249-256">Merhaba, dağıtım sırasında hello küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren hello dosyaları yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="68249-256">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="68249-257">Bu hello varsayılan veya Küme dağıtımı ya da başka bir genel olarak erişilebilir depolama kapsayıcısı hello sırasında belirtilen ek depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="68249-257">This can be any of hello default or additional Storage accounts specified at hello time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="68249-258">Komut dosyaları toomake idempotently, yürütme emin içine denetimleri ekleyebilirsiniz, böylece Hello betik hello üzerinde birden çok kez çalıştırılabilir aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="68249-258">Add checks into scripts toomake sure that they execute idempotently, so that hello script can be executed multiple times on hello same node.</span></span>
3. <span data-ttu-id="68249-259">Kullanım hello **Write-Output** STDERR yanı sıra Azure PowerShell cmdlet tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="68249-259">Use hello **Write-Output** Azure PowerShell cmdlet tooprint tooSTDOUT as well as STDERR.</span></span> <span data-ttu-id="68249-260">Kullanmayın **Write-Host**.</span><span class="sxs-lookup"><span data-stu-id="68249-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="68249-261">$Env gibi bir geçici dosya klasörünü kullanabilirsiniz: TEMP tookeep hello hello komut dosyaları tarafından kullanılan indirilen dosya ve komut dosyaları çalıştırdıktan sonra sonra bunları Temizle.</span><span class="sxs-lookup"><span data-stu-id="68249-261">Use a temporary file folder, such as $env:TEMP, tookeep hello downloaded file used by hello scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="68249-262">Özel yazılım D:\ veya C:\apps yalnızca yükleyin.</span><span class="sxs-lookup"><span data-stu-id="68249-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="68249-263">Ayrılmış olarak hello C: sürücüsündeki başka konumlarda kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="68249-263">Other locations on hello C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="68249-264">Merhaba C:\apps klasörü dışında hello C: sürücüsündeki dosyaları yükleme kurulum hataları sırasında hello düğümünün reimages neden olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68249-264">Note that installing files on hello C: drive outside of hello C:\apps folder may result in setup failures during reimages of hello node.</span></span>
6. <span data-ttu-id="68249-265">Böylece hello ortam değişkenleri hello komut dosyalarında ayarlama gibi herhangi bir işletim sistemi düzeyinde ayarlarını seçebilirsiniz, işletim sistemi düzeyinde ayarları veya Hadoop hizmeti yapılandırma dosyaları değiştirilmiş hello olayda toorestart Hdınsight Hizmetleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68249-265">In hello event that OS-level settings or Hadoop service configuration files were changed, you may want toorestart HDInsight services so that they can pick up any OS-level settings, such as hello environment variables set in hello scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="68249-266">Özel komut dosyaları hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="68249-266">Debug custom scripts</span></span>
<span data-ttu-id="68249-267">Merhaba komut dosyası hata günlüklerini diğer çıktısında hello küme oluşturma sırasında belirtilen hello varsayılan depolama hesabı ile birlikte saklanır.</span><span class="sxs-lookup"><span data-stu-id="68249-267">hello script error logs are stored, along with other output, in hello default Storage account that you specified for hello cluster at its creation.</span></span> <span data-ttu-id="68249-268">Merhaba günlükleri hello adı olan bir tabloda depolanır *u < \cluster-name-fragment >< \time-stamp > setuplog*.</span><span class="sxs-lookup"><span data-stu-id="68249-268">hello logs are stored in a table with hello name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="68249-269">Tüm düğümlerinin üzerinde hangi hello hello kümede komut dosyasını çalıştırır hello (baş düğüm ve çalışan düğümleri) kayıtları toplanmış günlükleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="68249-269">These are aggregated logs that have records from all of hello nodes (head node and worker nodes) on which hello script runs in hello cluster.</span></span>
<span data-ttu-id="68249-270">Toocheck hello günlükleri olan toouse kolay bir yolu, Visual Studio için Hdınsight araçları.</span><span class="sxs-lookup"><span data-stu-id="68249-270">An easy way toocheck hello logs is toouse HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="68249-271">Merhaba araçları yüklemek için bkz: [Visual Studio Hadoop araçlarını için Hdınsight kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="68249-271">For installing hello tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="68249-272">**Visual Studio kullanarak toocheck hello günlük**</span><span class="sxs-lookup"><span data-stu-id="68249-272">**toocheck hello log using Visual Studio**</span></span>

1. <span data-ttu-id="68249-273">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="68249-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="68249-274">Tıklatın **Görünüm**ve ardından **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="68249-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="68249-275">"Azure" sağ tıklayın, çok Bağlan**Microsoft Azure abonelikleri**ve ardından kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="68249-275">Right-click "Azure", click Connect too**Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="68249-276">Genişletme **depolama**, hello varsayılan dosya sistemi olarak kullanılan hello Azure depolama hesabı genişletin, **tabloları**ve hello tablo adına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68249-276">Expand **Storage**, expand hello Azure storage account used as hello default file system, expand **Tables**, and then double-click hello table name.</span></span>

<span data-ttu-id="68249-277">Merhaba küme düğümleri toosee yapabilecekleriniz Ayrıca uzak STDOUT ve STDERR özel komut dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="68249-277">You can also remote into hello cluster nodes toosee both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="68249-278">Merhaba günlükleri her düğümde belirli yalnızca toothat düğümü ve oturum açtığınız **C:\HDInsightLogs\DeploymentAgent.log**.</span><span class="sxs-lookup"><span data-stu-id="68249-278">hello logs on each node are specific only toothat node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="68249-279">Bu günlük dosyaları hello özel komut dosyasından tüm çıkış kaydedin.</span><span class="sxs-lookup"><span data-stu-id="68249-279">These log files record all outputs from hello custom script.</span></span> <span data-ttu-id="68249-280">Spark betik eylemi için bir örnek günlük parçacığı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="68249-280">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="68249-281">Bu günlük, Temizle hello Spark betik eylemi hello HEADNODE0 adlı VM üzerinde yürütüldüğü ve hiçbir özel hello yürütme sırasında durum oluştu.</span><span class="sxs-lookup"><span data-stu-id="68249-281">In this log, it is clear that hello Spark script action has been executed on hello VM named HEADNODE0 and that no exceptions were thrown during hello execution.</span></span>

<span data-ttu-id="68249-282">Bir yürütme hatası oluşursa hello olayda, onu açıklayan hello çıkış de bu günlük dosyasında yer alır.</span><span class="sxs-lookup"><span data-stu-id="68249-282">In hello event that an execution failure occurs, hello output describing it is also contained in this log file.</span></span> <span data-ttu-id="68249-283">Bu günlükler sağlanan hello bilgilerin kaynaklanabilecek betik sorunları hata ayıklamaya yardımcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="68249-283">hello information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="68249-284">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="68249-284">See also</span></span>
* <span data-ttu-id="68249-285">[Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="68249-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="68249-286">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="68249-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="68249-287">[Yükleme ve Hdınsight kümelerinde R kullanma][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="68249-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="68249-288">[Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="68249-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="68249-289">[Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="68249-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
