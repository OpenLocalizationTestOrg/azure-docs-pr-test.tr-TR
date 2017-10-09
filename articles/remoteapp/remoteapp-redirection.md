---
title: "Azure RemoteApp aaaUsing yeniden yönlendirmeyi | Microsoft Docs"
description: "Bilgi nasıl RemoteApp tooconfigure ve kullanım yeniden yönlendirme"
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="2100e-103">Azure Remoteapp'te yeniden yönlendirme kullanma</span><span class="sxs-lookup"><span data-stu-id="2100e-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2100e-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2100e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2100e-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="2100e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2100e-106">Aygıt yeniden yönlendirme kullanıcılarınızın hello aygıtları ekli tootheir yerel bilgisayar, telefon veya tablet kullanarak uzak uygulamaları ile etkileşime olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2100e-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="2100e-107">Örneğin, Azure RemoteApp aracılığıyla Skype verdiyse, kullanıcı kendi PC toowork Skype ile yüklenmiş hello kamera gerekir.</span><span class="sxs-lookup"><span data-stu-id="2100e-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="2100e-108">Bu da yazıcılar, konuşmacılar, izleyiciler ve aralığı, USB bağlantılı bir çevre birimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2100e-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="2100e-109">RemoteApp hello Uzak Masaüstü Protokolü (RDP) ve RemoteFX tooprovide yeniden yönlendirme yararlanır.</span><span class="sxs-lookup"><span data-stu-id="2100e-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="2100e-110">Hangi yeniden yönlendirme varsayılan olarak etkin mi?</span><span class="sxs-lookup"><span data-stu-id="2100e-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="2100e-111">RemoteApp kullandığınızda, yeniden yönlendirme aşağıdaki hello varsayılan olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2100e-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="2100e-112">Parantez içindeki Hello bilgileri hello RDP ayarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2100e-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="2100e-113">Ses hello yerel bilgisayarda yürütmek (**bu bilgisayarda yürütmek**).</span><span class="sxs-lookup"><span data-stu-id="2100e-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="2100e-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="2100e-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="2100e-115">Ses hello yerel bilgisayar ve gönderme toohello uzak bilgisayarda yakalama (**bu bilgisayardan kayıt**).</span><span class="sxs-lookup"><span data-stu-id="2100e-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="2100e-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="2100e-117">Yazdırma toolocal yazıcıları (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="2100e-118">COM bağlantı noktaları (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="2100e-119">Akıllı kart cihazı (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="2100e-120">Pano (özelliği toocopy ve Yapıştır) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="2100e-121">Yazı tipi düzeltmeye temizleyin (yazı tipi düzeltmeye izin ver: i:1)</span><span class="sxs-lookup"><span data-stu-id="2100e-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="2100e-122">Tüm desteklenen Tak ve Kullan cihazları yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="2100e-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="2100e-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="2100e-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="2100e-124">Başka bir yeniden yönlendirme ne var mı?</span><span class="sxs-lookup"><span data-stu-id="2100e-124">What other redirection is available?</span></span>
<span data-ttu-id="2100e-125">İki yeniden yönlendirme seçenekleri varsayılan olarak devre dışıdır:</span><span class="sxs-lookup"><span data-stu-id="2100e-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="2100e-126">Sürücü yeniden yönlendirme (sürücü eşleme): hello uzak oturumda eşlenen sürücüler, yerel bilgisayarınızın diskleri haline.</span><span class="sxs-lookup"><span data-stu-id="2100e-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="2100e-127">Merhaba uzak oturumda çalışırken bu kaydettiğinizde veya açık dosyalardan yerel sürücülerinizi olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2100e-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="2100e-128">USB yeniden yönlendirme: hello uzak oturumundan hello USB aygıtları ekli tooyour yerel bilgisayar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2100e-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="2100e-129">Remoteapp'te yeniden yönlendirme ayarlarınızı değiştirin</span><span class="sxs-lookup"><span data-stu-id="2100e-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="2100e-130">SDK ile Merhaba Microsoft Azure PowerShell kullanarak bir koleksiyon için hello aygıt yeniden yönlendirme ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2100e-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="2100e-131">Yükledikten sonra yeni PowerShell ve SDK Merhaba, ilk olarak, aboneliğinizin açıklanan toomanage yapılandırın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2100e-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="2100e-132">Ardından aşağıdaki tooset hello özel RDP özelliklere komutu benzer toohello kullanın:</span><span class="sxs-lookup"><span data-stu-id="2100e-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="2100e-133">(Unutmayın  *\`n*  ayrı ayrı özellikler arasında ayırıcı olarak kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="2100e-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="2100e-134">tooget hangi özel RDP özellikleri yapılandırılır, listesini hello aşağıdaki cmdlet'i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2100e-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="2100e-135">Yalnızca özel özellikler çıkış sonuçları olarak gösterilir ve varsayılan özellikleri hello değil dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="2100e-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="2100e-136">Özel özellikler ayarladığınızda, tüm özel özellikleri her zaman belirtmeniz gerekir; Aksi takdirde hello ayar toodisabled döner.</span><span class="sxs-lookup"><span data-stu-id="2100e-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="2100e-137">Ortak örnekler</span><span class="sxs-lookup"><span data-stu-id="2100e-137">Common examples</span></span>
<span data-ttu-id="2100e-138">Aşağıdaki cmdlet'i tooenable sürücü yönlendirmesi hello kullan:</span><span class="sxs-lookup"><span data-stu-id="2100e-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="2100e-139">Bu cmdlet tooenable kullanmak USB ve sürücü yeniden yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="2100e-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="2100e-140">Bu cmdlet toodisable Pano paylaşımı kullanın:</span><span class="sxs-lookup"><span data-stu-id="2100e-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="2100e-141">Emin toocompletely günlük hello koleksiyonundaki tüm kullanıcılar devre dışı olması (ve yalnızca kesmeden) hello değişiklik test önce.</span><span class="sxs-lookup"><span data-stu-id="2100e-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="2100e-142">tooensure kullanıcılar tamamen kapalı, Git toohello oturum **oturumları** sekmesinde hello koleksiyonundaki hello Azure portal ve bağlantısı kesilmiş veya oturum açtığı tüm kullanıcıları oturumunu.</span><span class="sxs-lookup"><span data-stu-id="2100e-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="2100e-143">Bazen bu hello oturumunda Explorer'da hello yerel sürücüler tooshow birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2100e-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="2100e-144">Windows istemci USB yeniden yönlendirme ayarlarını değiştirin</span><span class="sxs-lookup"><span data-stu-id="2100e-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="2100e-145">Toouse USB yeniden yönlendirme tooRemoteApp bağlanan bir bilgisayarda istiyorsanız toohappen gereksinim 2 eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="2100e-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="2100e-146">1 - yöneticinize Azure PowerShell kullanarak tooenable USB yeniden yönlendirme hello koleksiyonu düzeyinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="2100e-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="2100e-147">2 - toouse USB yeniden yönlendirme istediğiniz her cihazda tooenable izin bir Grup İlkesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2100e-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="2100e-148">Bu adım toouse USB yeniden yönlendirme istediği her kullanıcı için yapılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2100e-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="2100e-149">Azure RemoteApp ile USB yeniden yönlendirme yalnızca Windows bilgisayarları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2100e-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="2100e-150">Merhaba RemoteApp koleksiyonu için USB yeniden yönlendirme özelliğini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2100e-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="2100e-151">Cmdlet tooenable USB yeniden yönlendirme hello koleksiyonu düzeyinde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="2100e-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="2100e-152">Merhaba istemci bilgisayar için USB yeniden yönlendirme özelliğini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2100e-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="2100e-153">Bilgisayarınızda tooconfigure USB yeniden yönlendirme ayarları:</span><span class="sxs-lookup"><span data-stu-id="2100e-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="2100e-154">Açık hello yerel Grup İlkesi Düzenleyicisi'ni (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="2100e-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="2100e-155">(Gpedit.msc bir komut isteminden çalıştırın.)</span><span class="sxs-lookup"><span data-stu-id="2100e-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="2100e-156">Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="2100e-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="2100e-157">Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.</span><span class="sxs-lookup"><span data-stu-id="2100e-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="2100e-158">Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar hello RemoteFX USB yeniden yönlendirme erişim hakları**.</span><span class="sxs-lookup"><span data-stu-id="2100e-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="2100e-159">Yönetim izinleri olan bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2100e-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="2100e-160">Merhaba bilgisayarı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2100e-160">Restart hello computer.</span></span>

<span data-ttu-id="2100e-161">Ayrıca, hello Grup İlkesi Yönetimi Aracı toocreate kullanabilir ve etki alanınızdaki hello USB yeniden yönlendirme ilkesi tüm bilgisayarlar için uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2100e-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="2100e-162">Merhaba etki alanı denetleyicisi olarak hello etki alanı yöneticisi olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="2100e-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="2100e-163">Merhaba Grup İlkesi Yönetim Konsolu'nu açın.</span><span class="sxs-lookup"><span data-stu-id="2100e-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="2100e-164">(Tıklatın **Başlat > Yönetim Araçları > Grup İlkesi Yönetimi**.)</span><span class="sxs-lookup"><span data-stu-id="2100e-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="2100e-165">Toohello etki alanı veya toocreate hello İlkesi istediğiniz kuruluş birimine gidin.</span><span class="sxs-lookup"><span data-stu-id="2100e-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="2100e-166">Sağ **varsayılan etki alanı ilkesi**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="2100e-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="2100e-167">Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="2100e-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="2100e-168">Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.</span><span class="sxs-lookup"><span data-stu-id="2100e-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="2100e-169">Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar hello RemoteFX USB yeniden yönlendirme erişim hakları**.</span><span class="sxs-lookup"><span data-stu-id="2100e-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="2100e-170">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2100e-170">Click **OK**.</span></span>  

