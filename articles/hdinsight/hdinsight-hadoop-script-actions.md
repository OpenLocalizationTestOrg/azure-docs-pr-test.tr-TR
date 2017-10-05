---
title: "Betik eylemi geliştirme Hdınsight - Azure ile | Microsoft Docs"
description: "Betik eylemi olan Hadoop kümeleri özelleştirmeyi öğrenin. Betik eylemi, Hadoop küme üzerinde çalışan ek yazılım yüklemesi veya bir kümeye yüklü uygulamalar yapılandırmasını değiştirmek için kullanılabilir."
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
ms.openlocfilehash: 0e182e6b43fd2d17524c1da36cf4c204bb1b865a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="05b8a-104">Hdınsight Windows tabanlı kümeler için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="05b8a-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="05b8a-105">Hdınsight için betik eylemi betikler yazma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-105">Learn how to write Script Action scripts for HDInsight.</span></span> <span data-ttu-id="05b8a-106">Betik eylemi komut dosyalarını kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="05b8a-107">Linux tabanlı Hdınsight kümeleri için yazılmış aynı makale için bkz: [Hdınsight betik eylemi geliştirme betikleri](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-107">For the same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="05b8a-108">Bu belgede yer alan adımlar, yalnızca Windows tabanlı Hdınsight kümeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="05b8a-109">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="05b8a-110">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="05b8a-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="05b8a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="05b8a-112">Betik eylemleri Linux tabanlı kümelerde ile kullanma hakkında daha fazla bilgi için bkz: [(Linux) Hdınsight ile betik eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="05b8a-113">Betik eylemi, Hadoop küme üzerinde çalışan ek yazılım yüklemesi veya bir kümeye yüklü uygulamalar yapılandırmasını değiştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-113">Script Action can be used to install additional software running on a Hadoop cluster or to change the configuration of applications installed on a cluster.</span></span> <span data-ttu-id="05b8a-114">Hdınsight kümeleri dağıtıldığında küme düğümleri üzerinde çalışan bir komut dosyası komut dosyası eylemlerdir ve kümedeki düğümlerin Hdınsight yapılandırmasını tamamladıktan sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="05b8a-114">Script actions are scripts that run on the cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in the cluster complete HDInsight configuration.</span></span> <span data-ttu-id="05b8a-115">Betik eylemi sistem yönetici hesabı ayrıcalıklarıyla yürütülür ve küme düğümleri için tam erişim hakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="05b8a-115">A script action is executed under system admin account privileges and provides full access rights to the cluster nodes.</span></span> <span data-ttu-id="05b8a-116">Her küme, belirtilen sırada yürütülecek komut dosyası eylemlerin bir listesi ile sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-116">Each cluster can be provided with a list of script actions to be executed in the order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="05b8a-117">Aşağıdaki hata iletisini karşılaşırsanız:</span><span class="sxs-lookup"><span data-stu-id="05b8a-117">If you experience the following error message:</span></span>
>
> <span data-ttu-id="05b8a-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage: Terimi 'Kaydet-HDIFile' cmdlet, işlev, komut dosyası veya çalıştırılabilir program adı olarak tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="05b8a-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : The term 'Save-HDIFile' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="05b8a-119">Adının yazımını denetleyin veya bir yol dahilse, yolun doğru olduğundan emin olun ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-119">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>
> <span data-ttu-id="05b8a-120">Yardımcı yöntemler eklemediniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-120">It is because you didn't include the helper methods.</span></span>  <span data-ttu-id="05b8a-121">Bkz: [özel komut dosyaları için yardımcı yöntemleri](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span><span class="sxs-lookup"><span data-stu-id="05b8a-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="05b8a-122">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="05b8a-122">Sample scripts</span></span>
<span data-ttu-id="05b8a-123">Betik eylemi, Windows işletim sisteminde Hdınsight kümeleri oluşturmak için Azure PowerShell komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-123">For creating HDInsight clusters on Windows operating system, the Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="05b8a-124">Aşağıdaki komut dosyasını site yapılandırma dosyalarını yapılandırmaya ilişkin bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="05b8a-124">The following script is a sample for configuring the site configuration files:</span></span>

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
        Write-HDILog "Unable to configure $ConfigFileName because it is not part of the HDI configuration files."
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

<span data-ttu-id="05b8a-125">Komut dosyası, dört parametre, yapılandırma dosyasının adını, ayarlamak istediğiniz değeri değiştirmek istediğiniz özellik ve açıklamasını alır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-125">The script takes four parameters, the configuration file name, the property you want to modify, the value you want to set, and a description.</span></span> <span data-ttu-id="05b8a-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="05b8a-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="05b8a-127">Bu parametreler hive-site.xml dosyasında 90 ila hive.metastore.client.socket.timeout değeri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="05b8a-127">These parameters sets the hive.metastore.client.socket.timeout value to 90 in the hive-site.xml file.</span></span>  <span data-ttu-id="05b8a-128">Varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-128">The default value is 60 seconds.</span></span>

<span data-ttu-id="05b8a-129">Bu örnek komut dosyası ayrıca bulunabilir [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span><span class="sxs-lookup"><span data-stu-id="05b8a-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="05b8a-130">Hdınsight Hdınsight kümelerinde ek bileşenleri yüklemek için çeşitli komut dosyaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="05b8a-130">HDInsight provides several scripts to install additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="05b8a-131">Ad</span><span class="sxs-lookup"><span data-stu-id="05b8a-131">Name</span></span> | <span data-ttu-id="05b8a-132">Betik</span><span class="sxs-lookup"><span data-stu-id="05b8a-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="05b8a-133">**Spark yükleyin**</span><span class="sxs-lookup"><span data-stu-id="05b8a-133">**Install Spark**</span></span> |<span data-ttu-id="05b8a-134">https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="05b8a-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="05b8a-135">Bkz: [yükleme ve kullanma hdınsight'ta Spark kümeleri][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="05b8a-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="05b8a-136">**R yükleme**</span><span class="sxs-lookup"><span data-stu-id="05b8a-136">**Install R**</span></span> |<span data-ttu-id="05b8a-137">https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="05b8a-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="05b8a-138">Bkz: [yükleme ve kullanma R Hdınsight kümelerinde][hdinsight-r-scripts].</span><span class="sxs-lookup"><span data-stu-id="05b8a-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="05b8a-139">**Solr yükleyin**</span><span class="sxs-lookup"><span data-stu-id="05b8a-139">**Install Solr**</span></span> |<span data-ttu-id="05b8a-140">https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="05b8a-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="05b8a-141">Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="05b8a-142">- **Giraph yükleyin**</span><span class="sxs-lookup"><span data-stu-id="05b8a-142">- **Install Giraph**</span></span> |<span data-ttu-id="05b8a-143">https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="05b8a-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="05b8a-144">Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="05b8a-145">Betik eylemi, Azure portalı, Azure PowerShell veya Hdınsight .NET SDK kullanarak dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-145">Script Action can be deployed from the Azure portal, Azure PowerShell or by using the HDInsight .NET SDK.</span></span>  <span data-ttu-id="05b8a-146">Daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak][hdinsight-cluster-customize].</span><span class="sxs-lookup"><span data-stu-id="05b8a-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="05b8a-147">Örnek betikler yalnızca Hdınsight kümesi sürüm 3.1 veya üzeri çalışır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-147">The sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="05b8a-148">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="05b8a-149">Özel komut dosyaları için yardımcı yöntemleri</span><span class="sxs-lookup"><span data-stu-id="05b8a-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="05b8a-150">Betik eylem Yardımcısı yöntemleri özel komut dosyaları yazılırken kullanabileceğiniz yardımcı programları ' dir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="05b8a-151">Bu yöntemler tanımlanan [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), komut dosyalarınızı aşağıdaki örneği kullanarak eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="05b8a-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using the following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module to make writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed to load HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="05b8a-152">Bu komut dosyası tarafından sağlanan yardımcı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="05b8a-152">Here are the helper methods that are provided by this script:</span></span>

| <span data-ttu-id="05b8a-153">Yardımcı yöntemi</span><span class="sxs-lookup"><span data-stu-id="05b8a-153">Helper method</span></span> | <span data-ttu-id="05b8a-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05b8a-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05b8a-155">**Kaydet-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="05b8a-155">**Save-HDIFile**</span></span> |<span data-ttu-id="05b8a-156">Bir dosya belirtilen Tekdüzen Kaynak Tanımlayıcısı (URI) gelen kümeye atanan Azure VM düğümle ilişkilendirilen yerel diskteki bir konuma indirin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-156">Download a file from the specified Uniform Resource Identifier (URI) to a location on the local disk that is associated with the Azure VM node assigned to the cluster.</span></span> |
| <span data-ttu-id="05b8a-157">**Genişletme HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="05b8a-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="05b8a-158">Sıkıştırılmış bir dosya sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="05b8a-159">**Çağırma HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="05b8a-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="05b8a-160">Bir komut dosyası cmd.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="05b8a-161">**Yazma HDILog**</span><span class="sxs-lookup"><span data-stu-id="05b8a-161">**Write-HDILog**</span></span> |<span data-ttu-id="05b8a-162">Bir komut dosyası eylemi için kullanılan özel komut dosyasından çıkış yazma.</span><span class="sxs-lookup"><span data-stu-id="05b8a-162">Write output from the custom script used for a script action.</span></span> |
| <span data-ttu-id="05b8a-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="05b8a-163">**Get-Services**</span></span> |<span data-ttu-id="05b8a-164">Burada betiği yürüten makinede çalışan hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-164">Get a list of services running on the machine where the script executes.</span></span> |
| <span data-ttu-id="05b8a-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="05b8a-165">**Get-Service**</span></span> |<span data-ttu-id="05b8a-166">Giriş olarak belirli hizmet adı ile belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) burada betiği yürüten makinede.</span><span class="sxs-lookup"><span data-stu-id="05b8a-166">With the specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="05b8a-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="05b8a-167">**Get-HDIServices**</span></span> |<span data-ttu-id="05b8a-168">Burada betiği yürüten bilgisayarda çalışan Hdınsight hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-168">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="05b8a-169">**Get-HDIService**</span></span> |<span data-ttu-id="05b8a-170">Özel Hdınsight hizmet adı ile giriş olarak, belirli bir hizmet için ayrıntılı bilgi almak (hizmet adı, işlem kimliği, durum, vb.) burada betiği yürüten makinede.</span><span class="sxs-lookup"><span data-stu-id="05b8a-170">With the specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on the machine where the script executes.</span></span> |
| <span data-ttu-id="05b8a-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="05b8a-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="05b8a-172">Burada betiği yürüten bilgisayarda çalışan hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-172">Get a list of services that are running on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="05b8a-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="05b8a-174">Burada komut dosyasını çalıştırır (adına göre) belirli bir hizmet bilgisayar üzerinde çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-174">Check if a specific service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="05b8a-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="05b8a-176">Burada betiği yürüten bilgisayarda çalışan Hdınsight hizmetlerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-176">Get a list of HDInsight services running on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="05b8a-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="05b8a-178">Burada komut dosyasını çalıştırır (adına göre) belirli bir Hdınsight hizmet bilgisayarda çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-178">Check if a specific HDInsight service (by name) is running on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="05b8a-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="05b8a-180">Hadoop burada komut dosyasını çalıştırır bilgisayarda yüklü sürümünü alır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-180">Get the version of Hadoop installed on the computer where the script executes.</span></span> |
| <span data-ttu-id="05b8a-181">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="05b8a-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="05b8a-182">Burada betiği yürüten bilgisayar bir baş düğüm olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-182">Check if the computer where the script executes is a head node.</span></span> |
| <span data-ttu-id="05b8a-183">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="05b8a-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="05b8a-184">Burada betiği yürüten bilgisayar etkin bir baş düğüm olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-184">Check if the computer where the script executes is an active head node.</span></span> |
| <span data-ttu-id="05b8a-185">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="05b8a-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="05b8a-186">Burada betiği yürüten bilgisayar veri düğümü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-186">Check if the computer where the script executes is a data node.</span></span> |
| <span data-ttu-id="05b8a-187">**Düzen HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="05b8a-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="05b8a-188">Yapılandırma dosyaları hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml veya yarn-site.xml düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-188">Edit the config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="05b8a-189">Komut dosyası geliştirme için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="05b8a-189">Best practices for script development</span></span>
<span data-ttu-id="05b8a-190">Hdınsight kümesi için özel bir komut dosyası geliştirirken dikkate alınması gereken birkaç en iyi yöntemler vardır:</span><span class="sxs-lookup"><span data-stu-id="05b8a-190">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* <span data-ttu-id="05b8a-191">Hadoop sürüm denetimi</span><span class="sxs-lookup"><span data-stu-id="05b8a-191">Check for the Hadoop version</span></span>

    <span data-ttu-id="05b8a-192">Yalnızca Hdınsight sürüm 3.1 (Hadoop 2.4) ve bir kümede özel bileşenleri yüklemek için betik eylemi kullanarak destek üstünde.</span><span class="sxs-lookup"><span data-stu-id="05b8a-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action to install custom components on a cluster.</span></span> <span data-ttu-id="05b8a-193">Özel betiğinizde kullanmalısınız **Get-HDIHadoopVersion** komut dosyasında diğer görevleri gerçekleştirme ile devam etmeden önce Hadoop sürümünü denetlemek için yardımcı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05b8a-193">In your custom script, you must use the **Get-HDIHadoopVersion** helper method to check the Hadoop version before proceeding with performing other tasks in the script.</span></span>
* <span data-ttu-id="05b8a-194">Komut dosyası kaynaklara kararlı bağlantılar sağlar</span><span class="sxs-lookup"><span data-stu-id="05b8a-194">Provide stable links to script resources</span></span>

    <span data-ttu-id="05b8a-195">Kullanıcılar tüm betikler ve bir küme özelleştirmesinde kullanılan diğer yapıları kümenin kullanım ömrü kullanılabilir kalmasını ve bu dosyaların sürümleri süresince değiştirmeyin emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-195">Users should make sure that all the scripts and other artifacts used in the customization of a cluster remain available throughout the lifetime of the cluster and that the versions of these files do not change for the duration.</span></span> <span data-ttu-id="05b8a-196">Kümedeki düğümler yeniden görüntüleme gerekliyse, bu kaynakları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-196">These resources are required if the reimaging of nodes in the cluster is required.</span></span> <span data-ttu-id="05b8a-197">Karşıdan yüklemek ve bir depolama hesabındaki kullanıcı denetimleri her şeyi arşivlemek için en iyi uygulamadır bakın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-197">The best practice is to download and archive everything in a Storage account that the user controls.</span></span> <span data-ttu-id="05b8a-198">Bu, varsayılan depolama hesabı veya herhangi bir dağıtım zaman özelleştirilmiş bir küme için belirtilen ek depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-198">This can be the default Storage account or any of the additional Storage accounts specified at the time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="05b8a-199">Belgelerde, örneğin, biz kaynakları yerel bir kopyasını bu depolama hesabında yapmış olduğunuz sağlanan küme örnekleri özelleştirilmiş Spark ve R: https://hdiconfigactions.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="05b8a-199">In the Spark and R customized cluster samples provided in the documentation, for example, we have made a local copy of the resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="05b8a-200">Küme özelleştirme betik ıdempotent olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="05b8a-200">Ensure that the cluster customization script is idempotent</span></span>

    <span data-ttu-id="05b8a-201">Hdınsight kümesi düğümleri küme ömrü boyunca yeniden olduğunu beklediğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-201">You must expect that the nodes of an HDInsight cluster is reimaged during the cluster lifetime.</span></span> <span data-ttu-id="05b8a-202">Bir küme yeniden her küme özelleştirme komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-202">The cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="05b8a-203">Bu komut dosyasını yeniden görüntüsünü oluşturuyor sonra komut dosyasını aynı küme döndürülür emin olması herkese açık ıdempotent yalnızca küme başlangıçta oluşturulduğu ilk kez betiği çalıştırdıktan sonra durumla durumu özelleştirilmiş olacak şekilde tasarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-203">This script must be designed to be idempotent in the sense that upon reimaging, the script should ensure that the cluster is returned to the same customized state that it was in just after the script ran for the first time when the cluster was initially created.</span></span> <span data-ttu-id="05b8a-204">Özel bir komut dosyası ilk çalıştırılmasında D:\AppLocation uygulama yüklediyseniz, örneğin, sonra yeniden görüntüsünü oluşturuyor, bağlı her sonraki çalıştırmada betik adımları diğer işlemine devam etmeden önce uygulama D:\AppLocation konumda var olup olmadığını kontrol komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="05b8a-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, the script should check whether the application exists at the D:\AppLocation location before proceeding with other steps in the script.</span></span>
* <span data-ttu-id="05b8a-205">En iyi konumda özel bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="05b8a-205">Install custom components in the optimal location</span></span>

    <span data-ttu-id="05b8a-206">Küme düğümleri yeniden, D:\ sistem sürücüsü ve C:\ kaynak sürücü, veri kaybına ve bu sürücülerde yüklemiş olduğu uygulamalar sonuçlanır yeniden biçimlendirilen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-206">When cluster nodes are reimaged, the C:\ resource drive and D:\ system drive can be reformatted, resulting in the loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="05b8a-207">Kümenin parçası olan bir Azure sanal makine (VM) düğüm arıza ve yeni bir düğüm tarafından değiştirilirse bu de olabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-207">This could also happen if an Azure virtual machine (VM) node that is part of the cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="05b8a-208">Bileşenleri D:\ sürücüsüne veya küme C:\apps yerde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-208">You can install components on the D:\ drive or in the C:\apps location on the cluster.</span></span> <span data-ttu-id="05b8a-209">C:\ sürücüsü üzerindeki diğer tüm konumlara ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-209">All other locations on the C:\ drive are reserved.</span></span> <span data-ttu-id="05b8a-210">Burada uygulamalar veya kitaplıkları küme özelleştirme betik yüklenecek konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-210">Specify the location where applications or libraries are to be installed in the cluster customization script.</span></span>
* <span data-ttu-id="05b8a-211">Küme mimari yüksek kullanılabilirliğini sağlamak</span><span class="sxs-lookup"><span data-stu-id="05b8a-211">Ensure high availability of the cluster architecture</span></span>

    <span data-ttu-id="05b8a-212">Hdınsight bir baş düğüm (Hdınsight Hizmetleri çalıştırdığınız) etkin modda bir baş düğüm olup (hangi Hdınsight'ta Hizmetleri çalışmıyor) bekleme modunda olduğundan, yüksek kullanılabilirlik için bir Aktif-Pasif mimarisi vardır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where the HDInsight services are running) and the other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="05b8a-213">Hdınsight Hizmetleri kesilirse düğümleri etkin ve Pasif modları.</span><span class="sxs-lookup"><span data-stu-id="05b8a-213">The nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="05b8a-214">Yüksek kullanılabilirlik için her iki baş düğümünde hizmetlerini yüklemek için bir betik eylemi kullandıysanız, Hdınsight yük devretme mekanizması otomatik olarak bu kullanıcı tarafından yüklenen hizmetleri başarısız mümkün olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-214">If a script action is used to install services on both head nodes for high availability, note that the HDInsight failover mechanism is not able to automatically fail over these user-installed services.</span></span> <span data-ttu-id="05b8a-215">Bu nedenle kullanıcı yüklü hizmetler yüksek oranda kullanılabilir olması beklenen Hdınsight baş düğümler üzerinde kendi Aktif-Pasif modu, yük devretme yönteminde sahip veya etkin-etkin modunda olması.</span><span class="sxs-lookup"><span data-stu-id="05b8a-215">So user-installed services on HDInsight head nodes that are expected to be highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="05b8a-216">Baş düğüm rolünü bir değer olarak belirtildiğinde bir Hdınsight betik eylemi komutu her iki baş düğümler üzerinde çalışır *ClusterRoleCollection* parametresi.</span><span class="sxs-lookup"><span data-stu-id="05b8a-216">An HDInsight Script Action command runs on both head nodes when the head-node role is specified as a value in the *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="05b8a-217">Bu nedenle özel bir komut dosyası tasarlarken, kodunuzu bu kurulumu farkında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="05b8a-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="05b8a-218">Burada aynı hizmetleri yüklenir ve her iki baş düğümü üzerinde başlatıldı ve birbirleri ile rekabet bitiş sorunlar çalışmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-218">You should not run into problems where the same services are installed and started on both of the head nodes and they end up competing with each other.</span></span> <span data-ttu-id="05b8a-219">Betik eylemi yüklenen yazılım bu tür olayların dayanıklı olması gerekir böylece Ayrıca, yeniden görüntüleme sırasında veri kaybı olmamasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has to be resilient to such events.</span></span> <span data-ttu-id="05b8a-220">Uygulamalar birçok düğümüne dağıtılmış yüksek oranda kullanılabilir verilerle çalışmak için tasarlanmış.</span><span class="sxs-lookup"><span data-stu-id="05b8a-220">Applications should be designed to work with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="05b8a-221">Aynı anda kadar 1/5 kümedeki düğümlerin yeniden olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-221">Note that as many as 1/5 of the nodes in a cluster can be reimaged at the same time.</span></span>
* <span data-ttu-id="05b8a-222">Azure Blob storage kullanma özel bileşenlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05b8a-222">Configure the custom components to use Azure Blob storage</span></span>

    <span data-ttu-id="05b8a-223">Küme düğümlerine yükleyin özel bileşenler Hadoop dağıtılmış dosya sistemi (HDFS) depolama kullanmak için bir varsayılan yapılandırmaya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-223">The custom components that you install on the cluster nodes might have a default configuration to use Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="05b8a-224">Azure Blob storage kullanmayı yapılandırmasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-224">You should change the configuration to use Azure Blob storage instead.</span></span> <span data-ttu-id="05b8a-225">Bir küme yeniden görüntü oluşturma, HDFS dosya sistemi ile biçimlendirilmiş ve orada depolanan tüm verileri kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-225">On a cluster reimage, the HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="05b8a-226">Azure Blob storage kullanarak, bunun yerine, verilerinizi tutulur sağlar.</span><span class="sxs-lookup"><span data-stu-id="05b8a-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="05b8a-227">Genel kullanım desenleri</span><span class="sxs-lookup"><span data-stu-id="05b8a-227">Common usage patterns</span></span>
<span data-ttu-id="05b8a-228">Bu bölümde, kendi özel bir komut dosyası yazılırken içine çalışabilir ortak kullanım desenlerini bazıları uygulama yönergeler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-228">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="05b8a-229">Ortam değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="05b8a-229">Configure environment variables</span></span>
<span data-ttu-id="05b8a-230">Genellikle betik eylemi geliştirme ortam değişkenlerini ayarlama gerek düşündüğünüz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-230">Often in script action development, you feel the need to set environment variables.</span></span> <span data-ttu-id="05b8a-231">Bir ikili dış sitesinden, kümede yüklemek ve, 'PATH' ortam değişkeni yüklendiği konumun eklediğinizde örneği için en olası senaryodur.</span><span class="sxs-lookup"><span data-stu-id="05b8a-231">For instance, a most likely scenario is when you download a binary from an external site, install it on the cluster, and add the location of where it is installed to your ‘PATH’ environment variable.</span></span> <span data-ttu-id="05b8a-232">Aşağıdaki kod parçacığında özel betik ortam değişkenlerini ayarlama gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-232">The following snippet shows you how to set environment variables in the custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="05b8a-233">Bu bildirimi ortam değişkenini ayarlar **MDS_RUNNER_CUSTOM_CLUSTER** makine genelinde olması için bu değişkenin kapsamını 'true' hem de değerine ayarlar.</span><span class="sxs-lookup"><span data-stu-id="05b8a-233">This statement sets the environment variable **MDS_RUNNER_CUSTOM_CLUSTER** to the value 'true' and also sets the scope of this variable to be machine-wide.</span></span> <span data-ttu-id="05b8a-234">Zaman zaman ortam değişkenleri uygun kapsamda – makine ya da kullanıcı ayarlanır önemlidir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-234">At times it is important that environment variables are set at the appropriate scope – machine or user.</span></span> <span data-ttu-id="05b8a-235">Başvuru [burada] [ 1] ortam değişkenlerini ayarlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="05b8a-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="05b8a-236">Özel komut dosyaları depolandığı konumuna erişim</span><span class="sxs-lookup"><span data-stu-id="05b8a-236">Access to locations where the custom scripts are stored</span></span>
<span data-ttu-id="05b8a-237">Bir küme özelleştirmek için kullanılan komut ya da küme için varsayılan depolama hesabı veya başka bir depolama hesabı üzerinde genel bir salt okunur kapsayıcı olması.</span><span class="sxs-lookup"><span data-stu-id="05b8a-237">Scripts used to customize a cluster needs to either be in the default storage account for the cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="05b8a-238">Kodunuzu başka bir yerde bulunan kaynaklara erişirse bunlar bir ortak olarak erişilebilen olmanız gerekir (en az genel salt okunur).</span><span class="sxs-lookup"><span data-stu-id="05b8a-238">If your script accesses resources located elsewhere these need to be in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="05b8a-239">Örneğin bir dosyaya erişmek ve SaveFile HDI komutunu kullanarak kaydetmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-239">For instance you might want to access a file and save it using the SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="05b8a-240">Bu örnekte 'somestorageaccount' depolama hesabındaki ' somecontainer' kapsayıcı genel olarak erişilebilir olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="05b8a-240">In this example, you must ensure that the container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="05b8a-241">Aksi takdirde, komut dosyası 'Bulunamadı' bir özel durum oluşturur ve başarısız.</span><span class="sxs-lookup"><span data-stu-id="05b8a-241">Otherwise, the script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-to-the-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="05b8a-242">Add-AzureRmHDInsightScriptAction cmdlet parametreleri</span><span class="sxs-lookup"><span data-stu-id="05b8a-242">Pass parameters to the Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="05b8a-243">Birden çok parametre Ekle AzureRmHDInsightScriptAction cmdlet'e için komut dosyası için tüm parametreleri içeren dize değeri biçimlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-243">To pass multiple parameters to the Add-AzureRmHDInsightScriptAction cmdlet, you need to format the string value to contain all parameters for the script.</span></span> <span data-ttu-id="05b8a-244">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="05b8a-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="05b8a-245">or</span><span class="sxs-lookup"><span data-stu-id="05b8a-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="05b8a-246">Başarısız Küme dağıtımı için özel durum</span><span class="sxs-lookup"><span data-stu-id="05b8a-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="05b8a-247">Doğru bir şekilde, bildirim istiyorsanız özelleştirme küme olgu başarılı olmadı beklendiği gibi bir özel durum ve küme oluşturma başarısız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-247">If you want to get accurately notified of the fact that cluster customization did not succeed as expected, it is important to throw an exception and fail the cluster creation.</span></span> <span data-ttu-id="05b8a-248">Örneğin, bir dosya varsa işlemek ve burada dosya yok hata durumu işlemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-248">For instance, you might want to process a file if it exists and handle the error case where the file does not exist.</span></span> <span data-ttu-id="05b8a-249">Bu, komut dosyası düzgün biçimde çıkar ve küme durumunu doğru şekilde bilinen emin olun.</span><span class="sxs-lookup"><span data-stu-id="05b8a-249">This would ensure that the script exits gracefully and the state of the cluster is correctly known.</span></span> <span data-ttu-id="05b8a-250">Aşağıdaki kod parçacığında, bunu başarmak nasıl bir örnek sağlar:</span><span class="sxs-lookup"><span data-stu-id="05b8a-250">The following snippet gives an example of how to achieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="05b8a-251">Dosya olmasaydı, bu parçacığında, bunu burada komut gerçekte düzgün biçimde hata iletisini yazdırdıktan sonra çıkar ve küme "başarılı" Küme özelleştirme işlemi tamamlandı varsayılarak çalışır duruma ulaştığında bir duruma yol açar.</span><span class="sxs-lookup"><span data-stu-id="05b8a-251">In this snippet, if the file did not exist, it would lead to a state where the script actually exits gracefully after printing the error message, and the cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="05b8a-252">Özelleştirme temelde küme olgu doğru olarak bildirilmesini istiyorsanız, eksik dosya nedeniyle beklendiği gibi başarılı olmadı, bir özel durum ve küme özelleştirme adımı başarısız daha uygundur.</span><span class="sxs-lookup"><span data-stu-id="05b8a-252">If you want to be accurately notified of the fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate to throw an exception and fail the cluster customization step.</span></span> <span data-ttu-id="05b8a-253">Bunu başarmak için aşağıdaki örnek kod parçacığını yerine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-253">To achieve this you must use the following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="05b8a-254">Betik eylemi dağıtma denetim listesi</span><span class="sxs-lookup"><span data-stu-id="05b8a-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="05b8a-255">Biz bu komut dosyaları dağıtmak hazırlarken sürdü adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="05b8a-255">Here are the steps we took when preparing to deploy these scripts:</span></span>

1. <span data-ttu-id="05b8a-256">Dağıtım sırasında küme düğümleri tarafından erişilebilen bir yerde özel komut dosyaları içeren dosyaları yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-256">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="05b8a-257">Bu varsayılan veya Küme dağıtımı ya da başka bir genel olarak erişilebilir depolama kapsayıcısı sırada belirtilen ek depolama hesapları olabilir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-257">This can be any of the default or additional Storage accounts specified at the time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="05b8a-258">Komut dosyası birden çok kez aynı düğümde yürütülebilir. böylece idempotently, yürütme emin olmak için betikler içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-258">Add checks into scripts to make sure that they execute idempotently, so that the script can be executed multiple times on the same node.</span></span>
3. <span data-ttu-id="05b8a-259">Kullanım **Write-Output** STDERR yanı sıra STDOUT yazdırmak için Azure PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="05b8a-259">Use the **Write-Output** Azure PowerShell cmdlet to print to STDOUT as well as STDERR.</span></span> <span data-ttu-id="05b8a-260">Kullanmayın **Write-Host**.</span><span class="sxs-lookup"><span data-stu-id="05b8a-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="05b8a-261">$Env gibi bir geçici dosya klasörünü kullanabilirsiniz: betikler tarafından kullanılan indirilen dosya korumak ve komut dosyaları çalıştırdıktan sonra sonra bunları temizlemek için TEMP.</span><span class="sxs-lookup"><span data-stu-id="05b8a-261">Use a temporary file folder, such as $env:TEMP, to keep the downloaded file used by the scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="05b8a-262">Özel yazılım D:\ veya C:\apps yalnızca yükleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="05b8a-263">Ayrılmış olarak C: sürücüsündeki diğer konumlarda kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-263">Other locations on the C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="05b8a-264">C:\apps klasörü dışında C: sürücüsündeki dosyaları yükleme kurulum hataları sırasında düğümün reimages neden olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-264">Note that installing files on the C: drive outside of the C:\apps folder may result in setup failures during reimages of the node.</span></span>
6. <span data-ttu-id="05b8a-265">İşletim sistemi düzeyinde ayarları veya Hadoop hizmeti yapılandırma dosyaları değiştirilmiş gelmesi durumunda, böylece ortam değişkenleri komut kümesini gibi herhangi bir işletim sistemi düzeyinde ayarlarını seçebilirsiniz Hdınsight hizmetlerini yeniden isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-265">In the event that OS-level settings or Hadoop service configuration files were changed, you may want to restart HDInsight services so that they can pick up any OS-level settings, such as the environment variables set in the scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="05b8a-266">Özel komut dosyaları hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="05b8a-266">Debug custom scripts</span></span>
<span data-ttu-id="05b8a-267">Komut dosyası hata günlüklerini oluşturulduktan konumundaki küme için belirtilen varsayılan depolama hesabındaki diğer çıktı birlikte depolanır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-267">The script error logs are stored, along with other output, in the default Storage account that you specified for the cluster at its creation.</span></span> <span data-ttu-id="05b8a-268">Günlükler, adı olan bir tabloda depolanır *u < \cluster-name-fragment >< \time-stamp > setuplog*.</span><span class="sxs-lookup"><span data-stu-id="05b8a-268">The logs are stored in a table with the name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="05b8a-269">Tüm betik kümede çalışan düğümleri (baş düğüm ve çalışan düğümleri) kayıtları toplanmış günlükleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-269">These are aggregated logs that have records from all of the nodes (head node and worker nodes) on which the script runs in the cluster.</span></span>
<span data-ttu-id="05b8a-270">Günlükleri denetlemek için kolay bir yol, Visual Studio için Hdınsight araçları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-270">An easy way to check the logs is to use HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="05b8a-271">Araçları yüklemek için bkz: [Visual Studio Hadoop araçlarını için Hdınsight kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="05b8a-271">For installing the tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="05b8a-272">**Visual Studio kullanarak günlüğünü denetlemek için**</span><span class="sxs-lookup"><span data-stu-id="05b8a-272">**To check the log using Visual Studio**</span></span>

1. <span data-ttu-id="05b8a-273">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="05b8a-274">Tıklatın **Görünüm**ve ardından **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="05b8a-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="05b8a-275">"Azure" sağ tıklayın, Bağlan **Microsoft Azure abonelikleri**ve ardından kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-275">Right-click "Azure", click Connect to **Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="05b8a-276">Genişletme **depolama**, varsayılan dosya sistemi olarak kullanılan Azure depolama hesabı genişletin, **tabloları**ve tablo adı çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="05b8a-276">Expand **Storage**, expand the Azure storage account used as the default file system, expand **Tables**, and then double-click the table name.</span></span>

<span data-ttu-id="05b8a-277">Ayrıca uzak STDOUT ve STDERR için özel komut dosyaları görmek için küme düğümleri olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-277">You can also remote into the cluster nodes to see both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="05b8a-278">Her düğümde günlükleri yalnızca bu düğüme özgüdür ve oturum açtığınız **C:\HDInsightLogs\DeploymentAgent.log**.</span><span class="sxs-lookup"><span data-stu-id="05b8a-278">The logs on each node are specific only to that node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="05b8a-279">Bu günlük dosyaları, özel komut dosyasından tüm çıkış kaydedin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-279">These log files record all outputs from the custom script.</span></span> <span data-ttu-id="05b8a-280">Spark betik eylemi için bir örnek günlük parçacığı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="05b8a-280">An example log snippet for a Spark script action looks like this:</span></span>

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


<span data-ttu-id="05b8a-281">Bu günlük, Spark betik eylemi HEADNODE0 adlı VM üzerinde yürütüldüğü ve yürütme sırasında hiçbir özel durum oluştu, temizleyin.</span><span class="sxs-lookup"><span data-stu-id="05b8a-281">In this log, it is clear that the Spark script action has been executed on the VM named HEADNODE0 and that no exceptions were thrown during the execution.</span></span>

<span data-ttu-id="05b8a-282">Bir yürütme hatası meydana gelmesi durumunda, bu açıklayan çıkış bu günlük dosyasında da yer alır.</span><span class="sxs-lookup"><span data-stu-id="05b8a-282">In the event that an execution failure occurs, the output describing it is also contained in this log file.</span></span> <span data-ttu-id="05b8a-283">Bu günlükler sağlanan bilgilerin kaynaklanabilecek betik sorunları hata ayıklamaya yardımcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="05b8a-283">The information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="05b8a-284">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="05b8a-284">See also</span></span>
* <span data-ttu-id="05b8a-285">[Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="05b8a-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="05b8a-286">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="05b8a-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="05b8a-287">[Yükleme ve Hdınsight kümelerinde R kullanma][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="05b8a-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="05b8a-288">[Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="05b8a-289">[Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="05b8a-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
