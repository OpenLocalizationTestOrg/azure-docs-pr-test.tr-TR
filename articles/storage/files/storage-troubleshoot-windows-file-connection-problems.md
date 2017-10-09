---
title: "Windows'ta aaaTroubleshoot Azure File storage sorunlarını | Microsoft Docs"
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
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="fbaac-103">Windows Azure File storage sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fbaac-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="fbaac-104">Bu makalede Windows istemcilerinden gelen bağlandığınızda, ilgili tooMicrosoft Azure File storage genel sorunları listeler.</span><span class="sxs-lookup"><span data-stu-id="fbaac-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="fbaac-105">Ayrıca olası nedenleri ve çözümlemeleri için bu sorunları sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbaac-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="fbaac-106">Ayrıca bu makalede toohello sorun giderme adımları, aynı zamanda [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) , Windows hello emin olmak için istemci ortamın doğru önkoşulları vardır.</span><span class="sxs-lookup"><span data-stu-id="fbaac-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="fbaac-107">Bu makalede açıklanan hello belirtileri ve ortam, tooget en iyi performans ayarlama yardımcı çoğunu algılanması AzFileDiagnostics otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="fbaac-108">Bu bilgileri hello bulabilirsiniz [Azure dosya paylaşımları sorun gidericisini](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) adımları tooassist sağlayan sorunlarıyla bağlanma/eşleme/bağlama Azure dosya paylaşımlarını.</span><span class="sxs-lookup"><span data-stu-id="fbaac-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="fbaac-109">Hata 53, hata 67 veya hata bağlama ya da Azure dosya paylaşımının çıkarın 87</span><span class="sxs-lookup"><span data-stu-id="fbaac-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="fbaac-110">Bir dosya paylaşımı şirket içi veya farklı bir veri merkezinde toomount çalıştığınızda aşağıdaki hatalar hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbaac-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="fbaac-111">53 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-111">System error 53 has occurred.</span></span> <span data-ttu-id="fbaac-112">Merhaba ağ yolu bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="fbaac-112">hello network path was not found.</span></span>
- <span data-ttu-id="fbaac-113">67 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-113">System error 67 has occurred.</span></span> <span data-ttu-id="fbaac-114">Merhaba ağ adı bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="fbaac-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="fbaac-115">87 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-115">System error 87 has occurred.</span></span> <span data-ttu-id="fbaac-116">Merhaba parametresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="fbaac-117">1. neden: Şifrelenmemiş bir iletişim kanalı</span><span class="sxs-lookup"><span data-stu-id="fbaac-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="fbaac-118">Güvenlik nedenleriyle, tooAzure dosya paylaşımları hello iletişim kanalını şifreli değildir ve hello bağlantı denemesi yapılan değil engellenen bağlantıları hello Azure dosya paylaşımları bulunduğu aynı veri merkezinde hello.</span><span class="sxs-lookup"><span data-stu-id="fbaac-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="fbaac-119">Yalnızca hello kullanıcının istemci işletim sistemi SMB şifrelemesi destekliyorsa iletişim kanalı şifreleme sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fbaac-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="fbaac-120">Windows 8, Windows Server 2012 ve sonraki sürümlerinde her sistem şifrelemeyi destekleyen SMB 3.0 içeren isteklerin anlaşmaları.</span><span class="sxs-lookup"><span data-stu-id="fbaac-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="fbaac-121">Neden 1 için çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-121">Solution for cause 1</span></span>

<span data-ttu-id="fbaac-122">Merhaba aşağıdakilerden birini yapan bir istemciden Bağlan:</span><span class="sxs-lookup"><span data-stu-id="fbaac-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="fbaac-123">Windows 8 ve Windows Server 2012 veya sonraki sürümler Hello gereksinimlerini karşılayan</span><span class="sxs-lookup"><span data-stu-id="fbaac-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="fbaac-124">Merhaba, bir sanal makineden aynı bağlayan hello Azure dosya paylaşımı için kullanılan Azure depolama hesabı hello gibi veri merkezi</span><span class="sxs-lookup"><span data-stu-id="fbaac-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="fbaac-125">Neden 2: Bağlantı noktası 445 engellendi</span><span class="sxs-lookup"><span data-stu-id="fbaac-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="fbaac-126">Bağlantı noktası 445 giden iletişim tooan Azure File storage datacenter engellenirse, sistem hatası 53 veya sistem hatası 67 ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="fbaac-127">toosee hello izin veren veya bağlantı noktası 445, erişimden izin vermeyecek ISS'ler özetini Git çok[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbaac-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="fbaac-128">toounderstand bu hello "Sistem hata 53" iletisi arkasında hello neden olup olmadığını Portqry tooquery hello TCP:445 uç noktası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="fbaac-129">Merhaba TCP:445 endpoint filtre olarak görüntüleniyorsa hello TCP bağlantı noktası engellendi.</span><span class="sxs-lookup"><span data-stu-id="fbaac-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="fbaac-130">Örnek bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fbaac-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="fbaac-131">TCP bağlantı noktası 445 hello ağ yol kuralı tarafından engellenirse çıktı aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fbaac-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="fbaac-132">Hakkında daha fazla bilgi için bkz toouse Portqry, [hello Portqry.exe komut satırı yardımcı programının açıklaması](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="fbaac-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="fbaac-133">Neden 2 için çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-133">Solution for cause 2</span></span>

<span data-ttu-id="fbaac-134">BT departmanı tooopen 445 bağlantı noktası ile giden çok çalışma[Azure IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="fbaac-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="fbaac-135">3. neden: NTLMv1 etkin</span><span class="sxs-lookup"><span data-stu-id="fbaac-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="fbaac-136">NTLMv1 iletişimi hello istemcide etkinse, sistem hatası 53 veya sistem hatası 87 ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="fbaac-137">Azure File storage yalnızca NTLMv2 kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fbaac-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="fbaac-138">Etkin NTLMv1 sahip daha az güvenli bir istemci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fbaac-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="fbaac-139">Bu nedenle, iletişim için Azure File storage engellendi.</span><span class="sxs-lookup"><span data-stu-id="fbaac-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="fbaac-140">toodetermine bu hello hatasının hello neden olup olmadığını doğrulayın aşağıdaki kayıt defteri alt anahtarı bu hello tooa değeri 3 ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="fbaac-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="fbaac-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="fbaac-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="fbaac-142">Daha fazla bilgi için bkz: Merhaba [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) TechNet'te konu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="fbaac-143">Neden 3 için çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-143">Solution for cause 3</span></span>

<span data-ttu-id="fbaac-144">Merhaba geri **LmCompatibilityLevel** değeri 3'te kayıt defteri alt anahtarını aşağıdaki hello toohello varsayılan değeri:</span><span class="sxs-lookup"><span data-stu-id="fbaac-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="fbaac-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="fbaac-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="fbaac-146">Hata 1816 "yeterli kotası kullanılabilir tooprocess bu komuttur" tooan Azure dosya paylaşımı kopyaladığınızda</span><span class="sxs-lookup"><span data-stu-id="fbaac-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="fbaac-147">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fbaac-147">Cause</span></span>

<span data-ttu-id="fbaac-148">Hata 1816, burada hello dosya paylaşımı takılı hello bilgisayar için bir dosya izin verilen eşzamanlı açık tanıtıcıların sayısı üst sınırı hello ulaştığında oluşur.</span><span class="sxs-lookup"><span data-stu-id="fbaac-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="fbaac-149">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-149">Solution</span></span>

<span data-ttu-id="fbaac-150">Bazı tanıtıcıları kapatarak Hello eşzamanlı açık tanıtıcı sayısını azaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="fbaac-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="fbaac-151">Daha fazla bilgi için bkz: [Microsoft Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbaac-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="fbaac-152">Windows Azure File storage tooand kopyalama yavaş dosya</span><span class="sxs-lookup"><span data-stu-id="fbaac-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="fbaac-153">Tootransfer dosyaları toohello Azure dosya hizmeti çalıştığınızda yavaş performans görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="fbaac-154">Belirli bir en düşük g/ç boyutu gereksinim yoksa, en iyi performans için g/ç boyutu hello gibi 1 MB kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="fbaac-155">Biliyorsanız hello son ile genişletme dosya boyutunu yazar ve hello hello dosyada unwritten tail sıfırlar, önceden bir genişletme yazma her yazma yapmak yerine sonra hello dosya boyutunu Ayarla içerdiğinde yazılımınızı uyumluluk sorunlarına sahip değil.</span><span class="sxs-lookup"><span data-stu-id="fbaac-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="fbaac-156">Merhaba sağ copy yöntemini kullanın:</span><span class="sxs-lookup"><span data-stu-id="fbaac-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="fbaac-157">Kullanım [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) iki dosya paylaşımları arasında herhangi bir aktarım için.</span><span class="sxs-lookup"><span data-stu-id="fbaac-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="fbaac-158">Kullanım [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) bir şirket içi bilgisayar dosya paylaşımlarına arasında.</span><span class="sxs-lookup"><span data-stu-id="fbaac-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="fbaac-159">Windows 8.1 veya Windows Server 2012 R2 için ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="fbaac-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="fbaac-160">Windows 8.1 veya Windows Server 2012 R2 çalıştıran istemciler için olduğundan emin olun, hello [KB3114025](https://support.microsoft.com/help/3114025) düzeltme yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="fbaac-161">Bu düzeltme oluşturma hello performansını artırır ve tanıtıcıları kapatın.</span><span class="sxs-lookup"><span data-stu-id="fbaac-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="fbaac-162">Komut dosyası toocheck hello düzeltmesinin yüklü olup olmadığını aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbaac-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="fbaac-163">Düzeltme yüklüyse, hello aşağıdaki çıktısı görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="fbaac-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="fbaac-164">Windows Server 2012 R2 Azure Marketi görüntülerinde düzeltme aralık 2015'ten başlayarak varsayılan olarak yüklenen KB3114025 sahip.</span><span class="sxs-lookup"><span data-stu-id="fbaac-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="fbaac-165">Bir sürücü harfine sahip bir klasör bulunmadığından **Bilgisayarım**</span><span class="sxs-lookup"><span data-stu-id="fbaac-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="fbaac-166">Yönetici olarak net Kullan'ı kullanarak Azure dosya paylaşımının eşlerseniz hello toobe göründükten eksik.</span><span class="sxs-lookup"><span data-stu-id="fbaac-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="fbaac-167">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fbaac-167">Cause</span></span>

<span data-ttu-id="fbaac-168">Varsayılan olarak, bir yönetici olarak Windows dosya Gezgini çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="fbaac-169">Bir yönetici komut isteminden net kullanım çalıştırırsanız, yönetici olarak hello ağ sürücüsü eşlemeli.</span><span class="sxs-lookup"><span data-stu-id="fbaac-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="fbaac-170">Eşlenen sürücüler kullanıcı merkezli olduğundan, farklı bir kullanıcı hesabı altında bağlarsanız oturum hello kullanıcı hesabı hello sürücüleri görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="fbaac-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="fbaac-171">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-171">Solution</span></span>
<span data-ttu-id="fbaac-172">Merhaba paylaşımı, yönetici olmayan komut satırından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbaac-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="fbaac-173">Alternatif olarak, izleyebilirsiniz [bu TechNet konusuna](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** kayıt defteri değeri.</span><span class="sxs-lookup"><span data-stu-id="fbaac-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="fbaac-174">Merhaba depolama hesabı eğik içeriyorsa net use komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fbaac-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="fbaac-175">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fbaac-175">Cause</span></span>

<span data-ttu-id="fbaac-176">eğik çizgi (/) Hello net use komutunu bir komut satırı seçeneği olarak yorumlar.</span><span class="sxs-lookup"><span data-stu-id="fbaac-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="fbaac-177">Kullanıcı hesap adınızı eğik çizgiyle başlıyorsa, hello sürücü eşleştirmesi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fbaac-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="fbaac-178">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-178">Solution</span></span>

<span data-ttu-id="fbaac-179">Merhaba soruna geçici bir çözüm adımları toowork aşağıdaki hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbaac-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="fbaac-180">Merhaba aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fbaac-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="fbaac-181">Bir toplu iş dosyasından bu şekilde hello komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbaac-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="fbaac-182">Merhaba eğik hello ilk karakter olmadıkça hello anahtar toowork--bu soruna geçici bir çözüm etrafında çift tırnak işareti koyun.</span><span class="sxs-lookup"><span data-stu-id="fbaac-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="fbaac-183">İse, hello etkileşimli mod kullanın ve parolanızı ayrı ayrı girin ya da, anahtarları tooget eğik çizgiyle başlamaması bir anahtarı yeniden oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="fbaac-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="fbaac-184">Uygulama veya hizmet bağlı Azure dosya depolama sürücü erişemiyor</span><span class="sxs-lookup"><span data-stu-id="fbaac-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="fbaac-185">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fbaac-185">Cause</span></span>

<span data-ttu-id="fbaac-186">Kullanıcı başına bağlı sürücüler.</span><span class="sxs-lookup"><span data-stu-id="fbaac-186">Drives are mounted per user.</span></span> <span data-ttu-id="fbaac-187">Uygulama veya hizmet hello takılı hello sürücü bir daha farklı bir kullanıcı hesabı altında çalışıyorsa, Merhaba uygulaması hello sürücü görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="fbaac-188">Çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-188">Solution</span></span>

<span data-ttu-id="fbaac-189">Çözümleri aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="fbaac-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="fbaac-190">Hello Hello sürücü bağlama hello uygulamayı içeren aynı kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="fbaac-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="fbaac-191">PsExec gibi bir araç kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbaac-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="fbaac-192">Merhaba depolama hesabı adı ve anahtar hello kullanıcı adı ve parola parametrelerini hello net use komutunu içinde geçirin.</span><span class="sxs-lookup"><span data-stu-id="fbaac-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="fbaac-193">Bu yönergeleri izledikten sonra hello net kullanım hello sistem/ağ hizmeti hesabı için çalıştırdığınızda aşağıdaki hata iletisi alabilirsiniz: "1312 sistem hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="fbaac-194">Belirtilen oturum yok.</span><span class="sxs-lookup"><span data-stu-id="fbaac-194">A specified logon session does not exist.</span></span> <span data-ttu-id="fbaac-195">Bunu zaten kapatılmış olabilir."</span><span class="sxs-lookup"><span data-stu-id="fbaac-195">It may already have been terminated."</span></span> <span data-ttu-id="fbaac-196">Bu meydana gelirse, toonet kullanım geçirilen o hello kullanıcı adı, etki alanı bilgileri içerdiğinden emin olun (örneğin: "[depolama hesabı adı]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="fbaac-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="fbaac-197">"Şifreleme desteklemeyen tooa hedef dosyasını kopyaladığınız" hatası</span><span class="sxs-lookup"><span data-stu-id="fbaac-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="fbaac-198">Bir dosya hello ağ üzerinden kopyaladığınızda hello düz metin olarak aktarılan ve hello hedefte yeniden şifrelenir hello kaynak bilgisayarda, şifresi çözülen dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="fbaac-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="fbaac-199">Ancak, şifrelenmiş bir dosya toocopy çalışırken aşağıdaki hata hello görebilirsiniz: "Şifrelemeyi desteklemiyor hello dosya tooa hedef kopyalıyorsunuz."</span><span class="sxs-lookup"><span data-stu-id="fbaac-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="fbaac-200">Nedeni</span><span class="sxs-lookup"><span data-stu-id="fbaac-200">Cause</span></span>
<span data-ttu-id="fbaac-201">Şifreleme Dosya Sistemi (EFS) kullanıyorsanız, bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="fbaac-202">BitLocker ile şifrelenmiş dosyaları kopyalanan tooAzure dosya depolama olabilir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="fbaac-203">Ancak, Azure File storage NTFS EFS desteklemez.</span><span class="sxs-lookup"><span data-stu-id="fbaac-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="fbaac-204">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="fbaac-204">Workaround</span></span>
<span data-ttu-id="fbaac-205">toocopy hello ağ üzerinden dosya, ilk şifresini gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbaac-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="fbaac-206">Yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="fbaac-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="fbaac-207">Kullanım hello **/d kopyalama** komutu.</span><span class="sxs-lookup"><span data-stu-id="fbaac-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="fbaac-208">Şifrelenmiş hello verir hello hedefte şifresi çözülen dosyaları olarak kaydedilen toobe dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fbaac-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="fbaac-209">Kayıt defteri anahtarını aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="fbaac-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="fbaac-210">Yol HKLM\Software\Policies\Microsoft\Windows\System =</span><span class="sxs-lookup"><span data-stu-id="fbaac-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="fbaac-211">Değer türü = DWORD</span><span class="sxs-lookup"><span data-stu-id="fbaac-211">Value type = DWORD</span></span>
  - <span data-ttu-id="fbaac-212">Adı CopyFileAllowDecryptedRemoteDestination =</span><span class="sxs-lookup"><span data-stu-id="fbaac-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="fbaac-213">Değer = 1</span><span class="sxs-lookup"><span data-stu-id="fbaac-213">Value = 1</span></span>

<span data-ttu-id="fbaac-214">Bu ayar hello kayıt defteri toonetwork paylaşımları yapılan tüm kopyalama işlemleri etkiler unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fbaac-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="fbaac-215">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="fbaac-215">Need help?</span></span> <span data-ttu-id="fbaac-216">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="fbaac-216">Contact support.</span></span>
<span data-ttu-id="fbaac-217">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , sorunun giderilmiş hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="fbaac-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
