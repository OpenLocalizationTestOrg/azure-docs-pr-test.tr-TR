---
title: "Windows Azure File storage sorunlarını giderme | Microsoft Docs"
description: "Windows Azure File storage sorunlarını giderme"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 71a8f4edf7776556b383f446e5aad007748ef090
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="a94cc-103">Windows Azure File storage sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="a94cc-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="a94cc-104">Bu makalede Windows istemcilerinden gelen bağlandığınızda, Microsoft Azure dosya depolama alanına ilgili genel sorunları listeler.</span><span class="sxs-lookup"><span data-stu-id="a94cc-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="a94cc-105">Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a94cc-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="a94cc-106">Bu makaledeki sorun giderme adımlarını ek olarak da kullanabilirsiniz [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) Windows istemci ortamı doğru Önkoşullar olduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="a94cc-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="a94cc-107">AzFileDiagnostics algılama en iyi performansı elde etmek ortamınızı ayarlayın yardımcı olur ve bu makalede açıklanan Belirtiler çoğunu otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="a94cc-108">Bu bilgiler de bulabilirsiniz [Azure dosya paylaşımları sorun gidericisini](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) bağlanma/eşleme/bağlama Azure dosya paylaşımları sorunlara yardımcı olmak için adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a94cc-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="a94cc-109">Hata 53, hata 67 veya hata bağlama ya da Azure dosya paylaşımının çıkarın 87</span><span class="sxs-lookup"><span data-stu-id="a94cc-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="a94cc-110">Şirket içi veya farklı bir veri merkezinde bir dosya paylaşımını bağlama çalıştığınızda aşağıdaki hataları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a94cc-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="a94cc-111">53 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-111">System error 53 has occurred.</span></span> <span data-ttu-id="a94cc-112">Ağ yolu bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a94cc-112">The network path was not found.</span></span>
- <span data-ttu-id="a94cc-113">67 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-113">System error 67 has occurred.</span></span> <span data-ttu-id="a94cc-114">Ağ adı bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="a94cc-114">The network name cannot be found.</span></span>
- <span data-ttu-id="a94cc-115">87 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-115">System error 87 has occurred.</span></span> <span data-ttu-id="a94cc-116">Parametresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="a94cc-117">1. neden: Şifrelenmemiş bir iletişim kanalı</span><span class="sxs-lookup"><span data-stu-id="a94cc-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="a94cc-118">Güvenlik nedenleriyle, Azure dosya paylaşımları için bağlantılar iletişim kanalını şifrelenmiş değil ve bağlantı denemesi aynı veri merkezinden Azure dosya paylaşımları bulunduğu değil yaptıysanız engellenir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="a94cc-119">Yalnızca kullanıcının istemci işletim sistemi SMB şifrelemesi destekliyorsa iletişim kanalı şifreleme sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a94cc-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="a94cc-120">Windows 8, Windows Server 2012 ve sonraki sürümlerinde her sistem şifrelemeyi destekleyen SMB 3.0 içeren isteklerin anlaşmaları.</span><span class="sxs-lookup"><span data-stu-id="a94cc-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="a94cc-121">Neden 1 için çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-121">Solution for cause 1</span></span>

<span data-ttu-id="a94cc-122">Aşağıdakilerden birini yapan bir istemciden Bağlan:</span><span class="sxs-lookup"><span data-stu-id="a94cc-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="a94cc-123">Windows 8 ve Windows Server 2012 veya sonraki sürümler gereksinimlerini karşılayan</span><span class="sxs-lookup"><span data-stu-id="a94cc-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="a94cc-124">Azure dosya paylaşımı için kullanılan Azure depolama hesabı ile aynı veri merkezinde bir sanal makineden bağlanır</span><span class="sxs-lookup"><span data-stu-id="a94cc-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="a94cc-125">Neden 2: Bağlantı noktası 445 engellendi</span><span class="sxs-lookup"><span data-stu-id="a94cc-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="a94cc-126">Bağlantı noktası 445 giden iletişim Azure File storage veri merkezine engellenirse, sistem hatası 53 veya sistem hatası 67 ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="a94cc-127">İzin veren veya bağlantı noktası 445 erişimden izin vermeyecek ISS'ler özetini görmek için Git [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="a94cc-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="a94cc-128">Bu nedenle "Sistem hata 53" iletisi arkasında olup olmadığını anlamak için Portqry TCP:445 endpoint sorgulamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="a94cc-129">TCP:445 endpoint filtre olarak görüntüleniyorsa, TCP bağlantı noktasını engellendi.</span><span class="sxs-lookup"><span data-stu-id="a94cc-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="a94cc-130">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a94cc-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="a94cc-131">TCP bağlantı noktası 445 ağ yol kuralı tarafından engellenirse aşağıdaki çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="a94cc-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="a94cc-132">Portqry kullanma hakkında daha fazla bilgi için bkz: [Portqry.exe komut satırı yardımcı programının açıklaması](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="a94cc-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="a94cc-133">Neden 2 için çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-133">Solution for cause 2</span></span>

<span data-ttu-id="a94cc-134">445 bağlantı noktası için giden açmak için BT departmanınızın ile çalışırsınız [Azure IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="a94cc-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="a94cc-135">3. neden: NTLMv1 etkin</span><span class="sxs-lookup"><span data-stu-id="a94cc-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="a94cc-136">İstemcide NTLMv1 iletişim etkinse, sistem hatası 53 veya sistem hatası 87 ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="a94cc-137">Azure File storage yalnızca NTLMv2 kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a94cc-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="a94cc-138">Etkin NTLMv1 sahip daha az güvenli bir istemci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a94cc-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="a94cc-139">Bu nedenle, iletişim için Azure File storage engellendi.</span><span class="sxs-lookup"><span data-stu-id="a94cc-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="a94cc-140">Bu hatanın nedenini olup olmadığını belirlemek için aşağıdaki kayıt defteri alt anahtarı 3 değerine ayarlandığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="a94cc-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="a94cc-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="a94cc-142">Daha fazla bilgi için bkz: [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) TechNet'te konu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="a94cc-143">Neden 3 için çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-143">Solution for cause 3</span></span>

<span data-ttu-id="a94cc-144">Geri **LmCompatibilityLevel** varsayılan değeri aşağıdaki kayıt defteri alt anahtarında 3 değerine:</span><span class="sxs-lookup"><span data-stu-id="a94cc-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="a94cc-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="a94cc-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="a94cc-146">Hata 1816 "yeterli kotası, bu komutu işlemek için kullanılabilir" bir Azure dosya paylaşımına kopyaladığınızda</span><span class="sxs-lookup"><span data-stu-id="a94cc-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="a94cc-147">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a94cc-147">Cause</span></span>

<span data-ttu-id="a94cc-148">Dosya paylaşımının nerede bağlı bilgisayar için bir dosya izin verilen eşzamanlı açık tanıtıcıların sayısı üst sınırı ulaştığında hata 1816 olur.</span><span class="sxs-lookup"><span data-stu-id="a94cc-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="a94cc-149">Çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-149">Solution</span></span>

<span data-ttu-id="a94cc-150">Bazı tanıtıcıları kapatarak eşzamanlı açık tanıtıcı sayısını azaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a94cc-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="a94cc-151">Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="a94cc-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="a94cc-152">Ve Windows Azure dosya depolama biriminden dosya kopyalama yavaş</span><span class="sxs-lookup"><span data-stu-id="a94cc-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="a94cc-153">Azure dosya hizmeti dosyaları aktarmaya çalıştığınızda yavaş performans görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="a94cc-154">Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu 1 MB kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="a94cc-155">Son yazma ile genişletme dosya boyutunu bildiğiniz ve dosyada unwritten tail sıfır içerdiğinde yazılımınızı uyumluluk sorunlarına sahip değil, önceden bir genişletme yazma her yazma yapmak yerine dosya boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="a94cc-156">Sağ copy yöntemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="a94cc-157">Kullanım [AzCopy](storage-use-azcopy.md#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.</span><span class="sxs-lookup"><span data-stu-id="a94cc-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="a94cc-158">Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.</span><span class="sxs-lookup"><span data-stu-id="a94cc-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="a94cc-159">Windows 8.1 veya Windows Server 2012 R2 için ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="a94cc-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="a94cc-160">Windows 8.1 veya Windows Server 2012 R2 çalıştıran istemciler için olduğundan emin olun, [KB3114025](https://support.microsoft.com/help/3114025) düzeltme yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="a94cc-161">Bu düzeltme oluşturma performansını artırır ve tanıtıcıları kapatın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="a94cc-162">Düzeltme yüklü olup olmadığını denetlemek için aşağıdaki betiği çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a94cc-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="a94cc-163">Düzeltme yüklediyseniz, aşağıdaki çıkış görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="a94cc-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="a94cc-164">Windows Server 2012 R2 Azure Marketi görüntülerinde düzeltme aralık 2015'ten başlayarak varsayılan olarak yüklenen KB3114025 sahip.</span><span class="sxs-lookup"><span data-stu-id="a94cc-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="a94cc-165">Bir sürücü harfine sahip bir klasör bulunmadığından **Bilgisayarım**</span><span class="sxs-lookup"><span data-stu-id="a94cc-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="a94cc-166">Yönetici olarak net Kullan'ı kullanarak Azure dosya paylaşımının eşlerseniz paylaşım eksik gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a94cc-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="a94cc-167">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a94cc-167">Cause</span></span>

<span data-ttu-id="a94cc-168">Varsayılan olarak, bir yönetici olarak Windows dosya Gezgini çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="a94cc-169">Bir yönetici komut isteminden net kullanım çalıştırırsanız, yönetici olarak ağ sürücüsü eşlemeli.</span><span class="sxs-lookup"><span data-stu-id="a94cc-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="a94cc-170">Eşlenen sürücüler kullanıcı merkezli olduğundan, farklı bir kullanıcı hesabı altında bağlarsanız oturum kullanıcı hesabı sürücüleri görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="a94cc-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="a94cc-171">Çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-171">Solution</span></span>
<span data-ttu-id="a94cc-172">Paylaşımı, yönetici olmayan komut satırından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="a94cc-173">Alternatif olarak, izleyebilirsiniz [bu TechNet konusuna](https://technet.microsoft.com/library/ee844140.aspx) yapılandırmak için **EnableLinkedConnections** kayıt defteri değeri.</span><span class="sxs-lookup"><span data-stu-id="a94cc-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="a94cc-174">Depolama hesabı eğik içeriyorsa net use komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a94cc-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="a94cc-175">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a94cc-175">Cause</span></span>

<span data-ttu-id="a94cc-176">Net use komutunu eğik çizgi (/) komut satırı seçeneği olarak yorumlar.</span><span class="sxs-lookup"><span data-stu-id="a94cc-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="a94cc-177">Kullanıcı hesap adınızı eğik çizgiyle başlıyorsa, sürücü eşleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a94cc-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="a94cc-178">Çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-178">Solution</span></span>

<span data-ttu-id="a94cc-179">Sorunu çözmek için aşağıdaki adımlardan birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a94cc-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="a94cc-180">Aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="a94cc-181">Bir toplu iş dosyasından bu şekilde komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a94cc-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="a94cc-182">İlk karakter eğik olmadığı sürece bu soruna geçici bir çözüm--anahtar etrafında çift tırnak işareti koyun.</span><span class="sxs-lookup"><span data-stu-id="a94cc-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="a94cc-183">İse, etkileşimli mod kullanabilir ve ayrıca, parolanızı girin veya eğik çizgiyle başlamaması anahtarını almak için anahtarları yeniden.</span><span class="sxs-lookup"><span data-stu-id="a94cc-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="a94cc-184">Uygulama veya hizmet bağlı Azure dosya depolama sürücü erişemiyor</span><span class="sxs-lookup"><span data-stu-id="a94cc-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="a94cc-185">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a94cc-185">Cause</span></span>

<span data-ttu-id="a94cc-186">Kullanıcı başına bağlı sürücüler.</span><span class="sxs-lookup"><span data-stu-id="a94cc-186">Drives are mounted per user.</span></span> <span data-ttu-id="a94cc-187">Uygulama veya hizmet takılı sürücü olandan farklı bir kullanıcı hesabı altında çalışıyorsa, uygulama sürücü görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="a94cc-188">Çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-188">Solution</span></span>

<span data-ttu-id="a94cc-189">Şu çözümlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="a94cc-190">Sürücü uygulamayı içeren kullanıcı hesabından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="a94cc-191">PsExec gibi bir araç kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a94cc-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="a94cc-192">Kullanıcı adı depolama hesabı adı ve anahtarı geçirin ve net parola parametrelerini komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="a94cc-193">Bu yönergeleri izledikten sonra sistem/ağ hizmeti hesabı için net kullanım çalıştırdığınızda aşağıdaki hata iletisini alabilirsiniz: "1312 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="a94cc-194">Belirtilen oturum yok.</span><span class="sxs-lookup"><span data-stu-id="a94cc-194">A specified logon session does not exist.</span></span> <span data-ttu-id="a94cc-195">Bunu zaten kapatılmış olabilir."</span><span class="sxs-lookup"><span data-stu-id="a94cc-195">It may already have been terminated."</span></span> <span data-ttu-id="a94cc-196">Bu gerçekleşirse, net use yöntemine geçirilen kullanıcı adı etki alanı bilgileri içerdiğinden emin olun (örneğin: "[depolama hesabı adı]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="a94cc-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="a94cc-197">"Dosya şifreleme desteklemeyen bir hedefe Kopyalamakta olduğunuz" hatası</span><span class="sxs-lookup"><span data-stu-id="a94cc-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="a94cc-198">Bir dosya ağ üzerinden kopyalandığında, dosya kaynak bilgisayarda şifresi, düz metin olarak iletilen ve hedefte yeniden şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="a94cc-199">Ancak, şifrelenmiş bir dosya kopyalamaya çalışırken aşağıdaki hatayı görebilirsiniz: "Şifrelemeyi desteklemiyor bir hedef dosya kopyalıyorsunuz."</span><span class="sxs-lookup"><span data-stu-id="a94cc-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="a94cc-200">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a94cc-200">Cause</span></span>
<span data-ttu-id="a94cc-201">Şifreleme Dosya Sistemi (EFS) kullanıyorsanız, bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="a94cc-202">BitLocker ile şifrelenmiş dosyaları Azure dosya depolama alanına kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="a94cc-203">Ancak, Azure File storage NTFS EFS desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a94cc-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="a94cc-204">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="a94cc-204">Workaround</span></span>
<span data-ttu-id="a94cc-205">Ağ üzerinden dosya kopyalamak için önce şifresini gerekir.</span><span class="sxs-lookup"><span data-stu-id="a94cc-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="a94cc-206">Aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-206">Use one of the following methods:</span></span>

- <span data-ttu-id="a94cc-207">Kullanım **/d kopyalama** komutu.</span><span class="sxs-lookup"><span data-stu-id="a94cc-207">Use the **copy /d** command.</span></span> <span data-ttu-id="a94cc-208">Hedef konumda şifresi çözülen dosyaları olarak kaydedilecek şifrelenmiş dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a94cc-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="a94cc-209">Aşağıdaki kayıt defteri anahtarını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a94cc-209">Set the following registry key:</span></span>
  - <span data-ttu-id="a94cc-210">Yol HKLM\Software\Policies\Microsoft\Windows\System =</span><span class="sxs-lookup"><span data-stu-id="a94cc-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="a94cc-211">Değer türü = DWORD</span><span class="sxs-lookup"><span data-stu-id="a94cc-211">Value type = DWORD</span></span>
  - <span data-ttu-id="a94cc-212">Adı CopyFileAllowDecryptedRemoteDestination =</span><span class="sxs-lookup"><span data-stu-id="a94cc-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="a94cc-213">Değer = 1</span><span class="sxs-lookup"><span data-stu-id="a94cc-213">Value = 1</span></span>

<span data-ttu-id="a94cc-214">Kayıt defteri anahtarı ayarı ağ paylaşımlarına yapılan tüm kopyalama işlemleri etkilediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a94cc-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="a94cc-215">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="a94cc-215">Need help?</span></span> <span data-ttu-id="a94cc-216">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="a94cc-216">Contact support.</span></span>
<span data-ttu-id="a94cc-217">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözülmüş sorununuzu almak için.</span><span class="sxs-lookup"><span data-stu-id="a94cc-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
