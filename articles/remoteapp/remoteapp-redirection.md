---
title: "Azure Remoteapp'te yeniden yönlendirme kullanma | Microsoft Docs"
description: "Yapılandırma ve Remoteapp'te yeniden yönlendirmeyi kullanma hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="8f28b-103">Azure Remoteapp'te yeniden yönlendirme kullanma</span><span class="sxs-lookup"><span data-stu-id="8f28b-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f28b-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="8f28b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8f28b-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="8f28b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8f28b-106">Aygıt yeniden yönlendirme, yerel bilgisayar, telefon veya tablet bağlı cihazların kullanarak uzak uygulamaları ile etkileşim kullanıcılarınızın olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8f28b-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="8f28b-107">Örneğin, Azure RemoteApp aracılığıyla Skype verdiyse, kullanıcı Skype ile çalışmak için kendi bilgisayarlarında yüklü kamera gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="8f28b-108">Bu da yazıcılar, konuşmacılar, izleyiciler ve aralığı, USB bağlantılı bir çevre birimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="8f28b-109">RemoteApp RemoteFX ve Uzak Masaüstü Protokolü (RDP) yeniden yönlendirme sağlamak için yararlanır.</span><span class="sxs-lookup"><span data-stu-id="8f28b-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="8f28b-110">Hangi yeniden yönlendirme varsayılan olarak etkin mi?</span><span class="sxs-lookup"><span data-stu-id="8f28b-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="8f28b-111">RemoteApp kullandığınızda, aşağıdaki yeniden yönlendirme varsayılan olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="8f28b-112">Parantez içindeki bilgileri RDP ayarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="8f28b-113">Yerel bilgisayarda bulunan ses çıkar (**bu bilgisayarda yürütmek**).</span><span class="sxs-lookup"><span data-stu-id="8f28b-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="8f28b-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="8f28b-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="8f28b-115">Yerel bilgisayardan ses yakalamak ve uzak bilgisayara Gönder (**bu bilgisayardan kayıt**).</span><span class="sxs-lookup"><span data-stu-id="8f28b-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="8f28b-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="8f28b-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="8f28b-117">Yerel yazıcılara (redirectprinters:i:1) yazdırma</span><span class="sxs-lookup"><span data-stu-id="8f28b-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="8f28b-118">COM bağlantı noktaları (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="8f28b-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="8f28b-119">Akıllı kart cihazı (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="8f28b-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="8f28b-120">Pano (kopyalamak ve yapıştırmak için yeteneği) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="8f28b-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="8f28b-121">Yazı tipi düzeltmeye temizleyin (yazı tipi düzeltmeye izin ver: i:1)</span><span class="sxs-lookup"><span data-stu-id="8f28b-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="8f28b-122">Tüm desteklenen Tak ve Kullan cihazları yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="8f28b-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="8f28b-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="8f28b-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="8f28b-124">Başka bir yeniden yönlendirme ne var mı?</span><span class="sxs-lookup"><span data-stu-id="8f28b-124">What other redirection is available?</span></span>
<span data-ttu-id="8f28b-125">İki yeniden yönlendirme seçenekleri varsayılan olarak devre dışıdır:</span><span class="sxs-lookup"><span data-stu-id="8f28b-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="8f28b-126">Sürücü yeniden yönlendirme (sürücü eşleme): uzak oturumda eşlenen sürücüler, yerel bilgisayarınızın diskleri haline.</span><span class="sxs-lookup"><span data-stu-id="8f28b-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="8f28b-127">Uzak oturumda çalışırken bu kaydettiğinizde veya açık dosyalardan yerel sürücülerinizi olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8f28b-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="8f28b-128">USB yeniden yönlendirme: uzaktan oturumunda yerel bilgisayarınıza bağlı USB aygıtlarını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="8f28b-129">Remoteapp'te yeniden yönlendirme ayarlarınızı değiştirin</span><span class="sxs-lookup"><span data-stu-id="8f28b-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="8f28b-130">SDK ile Microsoft Azure PowerShell kullanarak bir koleksiyon için cihaz yeniden yönlendirme ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f28b-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="8f28b-131">Yeni PowerShell ve SDK'yı yükledikten sonra açıklandığı gibi aboneliğinizi yönetmek için ilk yapılandırma [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8f28b-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8f28b-132">Ardından özel RDP özelliği ayarlamak için aşağıdakine benzer bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f28b-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="8f28b-133">(Unutmayın  *\`n*  ayrı ayrı özellikler arasında ayırıcı olarak kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="8f28b-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="8f28b-134">Hangi özel RDP özellikleri yapılandırılmış bir listesini almak için aşağıdaki cmdlet'i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8f28b-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="8f28b-135">Yalnızca özel özellikler çıkış sonuçları ve varsayılan özellikleri gösterildiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="8f28b-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="8f28b-136">Özel özellikler ayarladığınızda, tüm özel özellikleri her zaman belirtmeniz gerekir; Aksi takdirde ayarı devre dışı olarak döner.</span><span class="sxs-lookup"><span data-stu-id="8f28b-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="8f28b-137">Ortak örnekler</span><span class="sxs-lookup"><span data-stu-id="8f28b-137">Common examples</span></span>
<span data-ttu-id="8f28b-138">Sürücü yeniden yönlendirmeyi etkinleştirmek için aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f28b-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="8f28b-139">USB ve sürücü etkinleştirmek için bu cmdlet'i kullanın yeniden yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="8f28b-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="8f28b-140">Pano paylaşımını devre dışı bırakmak için bu cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f28b-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="8f28b-141">Koleksiyondaki tüm kullanıcı tamamen oturumunu (yalnızca kesmeden) emin olun ve değişiklik test önce.</span><span class="sxs-lookup"><span data-stu-id="8f28b-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="8f28b-142">Tamamen oturum emin olmak için Git **oturumları** sekmesinde Azure portalında koleksiyonundaki ve bağlantısı kesilmiş veya oturum açtığı tüm kullanıcıları oturumunu.</span><span class="sxs-lookup"><span data-stu-id="8f28b-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="8f28b-143">Bazen yerel sürücüler Explorer'da oturum içinde göstermek için birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="8f28b-144">Windows istemci USB yeniden yönlendirme ayarlarını değiştirin</span><span class="sxs-lookup"><span data-stu-id="8f28b-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="8f28b-145">RemoteApp bağlayan bir bilgisayardaki USB yeniden yönlendirme kullanmak istiyorsanız, gerçekleşmesi gereken 2 eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="8f28b-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="8f28b-146">1 - USB yeniden yönlendirme koleksiyon düzeyinde Azure PowerShell kullanarak etkinleştirmek yöneticinize gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="8f28b-147">2 - USB yeniden yönlendirme kullanmak istediğiniz her cihazda BT bir Grup İlkesi etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="8f28b-148">Bu adım, USB yeniden yönlendirme kullanmak istediği her kullanıcı için yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="8f28b-149">Azure RemoteApp ile USB yeniden yönlendirme yalnızca Windows bilgisayarları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8f28b-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="8f28b-150">RemoteApp koleksiyonu için USB yeniden yönlendirme özelliğini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="8f28b-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="8f28b-151">Koleksiyon düzeyinde USB yeniden yönlendirmeyi etkinleştirmek için aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f28b-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="8f28b-152">İstemci bilgisayar için USB yeniden yönlendirme özelliğini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="8f28b-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="8f28b-153">Bilgisayarınızda USB yeniden yönlendirme ayarlarını yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="8f28b-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="8f28b-154">Yerel Grup İlkesi Düzenleyicisi'ni (GPEDIT. açın MSC).</span><span class="sxs-lookup"><span data-stu-id="8f28b-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="8f28b-155">(Gpedit.msc bir komut isteminden çalıştırın.)</span><span class="sxs-lookup"><span data-stu-id="8f28b-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="8f28b-156">Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="8f28b-157">Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="8f28b-158">Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar RemoteFX USB yeniden yönlendirme erişim hakları**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="8f28b-159">Yönetim izinleri olan bir komut istemi açın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f28b-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="8f28b-160">Bilgisayarı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="8f28b-160">Restart the computer.</span></span>

<span data-ttu-id="8f28b-161">Grup İlkesi Yönetimi aracını, oluşturmak ve etki alanınızdaki tüm bilgisayarlar için USB yeniden yönlendirme ilkesini uygulamak için de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f28b-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="8f28b-162">Etki alanı denetleyicisi ile etki alanı yöneticisi olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8f28b-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="8f28b-163">Grup İlkesi Yönetim Konsolu'nu açın.</span><span class="sxs-lookup"><span data-stu-id="8f28b-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="8f28b-164">(Tıklatın **Başlat > Yönetim Araçları > Grup İlkesi Yönetimi**.)</span><span class="sxs-lookup"><span data-stu-id="8f28b-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="8f28b-165">Etki alanı veya bir ilke oluşturmak istediğiniz kuruluş birimine gidin.</span><span class="sxs-lookup"><span data-stu-id="8f28b-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="8f28b-166">Sağ **varsayılan etki alanı ilkesi**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="8f28b-167">Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="8f28b-168">Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="8f28b-169">Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar RemoteFX USB yeniden yönlendirme erişim hakları**.</span><span class="sxs-lookup"><span data-stu-id="8f28b-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="8f28b-170">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f28b-170">Click **OK**.</span></span>  

