---
title: "aaaConnect uzaktan tooyour StorSimple cihazı | Microsoft Docs"
description: "Açıklar nasıl tooconfigure Cihazınızı uzaktan yönetimi için nasıl ve ne tooconnect tooWindows HTTP veya HTTPS aracılığıyla StorSimple için PowerShell."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="10cdb-103">Uzaktan tooyour StorSimple 8000 serisi aygıtı bağlayın</span><span class="sxs-lookup"><span data-stu-id="10cdb-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="10cdb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="10cdb-104">Overview</span></span>

<span data-ttu-id="10cdb-105">Windows PowerShell aracılığıyla tooyour aygıt uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="10cdb-106">Bu şekilde bağlandığınızda, menü görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="10cdb-107">(Yalnızca hello seri konsol hello aygıt tooconnect üzerinde kullanıyorsanız, bir menü bakın.) Windows PowerShell uzaktan iletişimini ile tooa belirli çalışma bağlayın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="10cdb-108">Merhaba görüntüleme dili de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-108">You can also specify hello display language.</span></span>

<span data-ttu-id="10cdb-109">Windows PowerShell uzaktan iletişim toomanage Cihazınızı kullanma hakkında daha fazla bilgi için çok Git[StorSimple tooadminister için Windows PowerShell'i kullanın StorSimple Cihazınızı](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="10cdb-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="10cdb-110">Bu öğretici açıklar nasıl tooconfigure cihazınız için uzaktan yönetim ve ardından nasıl tooconnect tooWindows StorSimple için PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10cdb-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="10cdb-111">HTTPS tooremotely Windows PowerShell ile bağlanmak veya HTTP kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="10cdb-112">Ancak, ne zaman karar tooconnect tooWindows StorSimple, PowerShell bilgisinden hello nasıl dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="10cdb-113">Doğrudan toohello bağlanma cihaz seri konsoluna güvenlidir, ancak ağ anahtarları üzerinden bağlanan toohello seri konsol değil.</span><span class="sxs-lookup"><span data-stu-id="10cdb-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="10cdb-114">Toohello cihaz seri konsoluna ağ anahtarları bağlanırken hello güvenlik riskini dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="10cdb-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="10cdb-115">Bir HTTP oturumu aracılığıyla bağlanma hello ağ üzerinden hello seri konsol üzerinden bağlanma daha fazla güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="10cdb-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="10cdb-116">Bu en güvenli yöntemi hello olmamasına karşın, güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="10cdb-117">Kendinden imzalı bir sertifika ile HTTPS oturumu aracılığıyla bağlanma hello en güvenli ve önerilen seçenek hello olur.</span><span class="sxs-lookup"><span data-stu-id="10cdb-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="10cdb-118">Toohello Windows PowerShell arabirimi uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="10cdb-119">Ancak, uzaktan erişim tooyour StorSimple cihazı hello Windows PowerShell arabirimi üzerinden varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="10cdb-120">İlk hello cihazda uzaktan yönetimi etkinleştirmek ve ardından üzerinde Cihazınızı kullanılan tooaccess istemcisi hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="10cdb-121">Bu makalede açıklanan başlangıç adımları Windows Server 2012 R2 çalıştıran bir konak sisteminde gerçekleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="10cdb-122">HTTP bağlanma</span><span class="sxs-lookup"><span data-stu-id="10cdb-122">Connect through HTTP</span></span>

<span data-ttu-id="10cdb-123">TooWindows PowerShell StorSimple için bir HTTP oturumu aracılığıyla bağlanma hello seri konsol StorSimple cihazınızın üzerinden bağlanma daha fazla güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="10cdb-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="10cdb-124">Bu en güvenli yöntemi hello olmamasına karşın, güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="10cdb-125">Her iki hello Azure portal veya hello seri konsol tooconfigure uzaktan yönetimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="10cdb-126">Yordamları izleyerek hello seçin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="10cdb-127">HTTP üzerinden Hello Azure portal tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="10cdb-128">HTTP üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="10cdb-129">Uzaktan Yönetimi etkinleştirdikten sonra uzak bağlantı için yordamı tooprepare hello istemcisi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="10cdb-130">İçin Uzak bağlantı Hello istemcisini hazırla</span><span class="sxs-lookup"><span data-stu-id="10cdb-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="10cdb-131">HTTP üzerinden Hello Azure portal tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="10cdb-132">HTTP üzerinden adımlara hello Azure portal tooenable Uzaktan Yönetimi'nde hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="10cdb-133">tooenable hello Azure portalı üzerinden uzaktan yönetim</span><span class="sxs-lookup"><span data-stu-id="10cdb-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="10cdb-134">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="10cdb-135">Seçin **aygıtları** seçin ve Uzaktan Yönetim için kullanmak istediğiniz tooconfigure hello cihaz seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="10cdb-136">Çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="10cdb-137">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **Uzaktan Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="10cdb-138">Merhaba, **uzaktan yönetimi** dikey penceresinde ayarlamak **uzaktan yönetimini etkinleştirme** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="10cdb-139">Artık HTTP kullanarak tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="10cdb-140">(Merhaba tooconnect HTTPS üzerinden varsayılandır.) HTTP seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="10cdb-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10cdb-141">HTTP üzerinden bağlanma yalnızca güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="10cdb-142">Tıklatın **kaydetmek** ve onaylamanız istendiğinde seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="10cdb-143">HTTP üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="10cdb-144">Aşağıdaki adımları hello cihaz seri konsoluna tooenable uzaktan yönetimi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="10cdb-145">tooenable hello cihaz seri Konsolu aracılığıyla uzaktan yönetim</span><span class="sxs-lookup"><span data-stu-id="10cdb-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="10cdb-146">Merhaba seri konsol menüsünde 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="10cdb-147">Hello aygıtta hello seri Konsolu kullanma hakkında daha fazla bilgi için çok Git[tooWindows PowerShell StorSimple için cihaz seri konsoluna bağlanmak](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="10cdb-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="10cdb-148">Merhaba istemine yazın:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="10cdb-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="10cdb-149">HTTP tooconnect toohello cihaz kullanımının hello güvenlik açıkları hakkında bilgilendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="10cdb-150">İstendiğinde, yazarak onaylayın **Y**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="10cdb-151">HTTP yazarak etkin olduğunu doğrulayın:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="10cdb-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="10cdb-152">Bu hello doğrulayın **RemoteManagementMode** alan gösterir **HttpsAndHttpEnabled**çizim aşağıdaki .hello PuTTY bu ayarları gösterir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seri HTTPS ve HTTP Etkin](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="10cdb-154">İçin Uzak bağlantı Hello istemcisini hazırla</span><span class="sxs-lookup"><span data-stu-id="10cdb-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="10cdb-155">Aşağıdaki adımları hello istemci tooenable uzaktan yönetimi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="10cdb-156">Uzak bağlantı için tooprepare hello istemcisi</span><span class="sxs-lookup"><span data-stu-id="10cdb-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="10cdb-157">Bir Windows PowerShell oturumu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="10cdb-158">Merhaba komutu tooadd hello IP adresini hello StorSimple cihaz toohello istemcinin güvenilir konaklar listesine aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="10cdb-159">Değiştir <*device_ip*> merhaba IP adresiyle Cihazınızı; örneğin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="10cdb-160">Bir değişken komutu toosave hello aygıt kimlik bilgilerini aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="10cdb-161">Merhaba iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="10cdb-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="10cdb-162">Tür hello kullanıcı adı şu biçimde: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="10cdb-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="10cdb-163">Hello aygıt hello Kurulum Sihirbazı ile yapılandırıldığında bu ayarlanan hello cihaz Yöneticisi parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="10cdb-164">Merhaba varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="10cdb-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="10cdb-165">Bir Windows PowerShell oturumunda aşağıdaki komutu yazarak hello cihazda başlatın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="10cdb-166">toocreate hello StorSimple sanal cihazı ile kullanmak için Windows PowerShell oturumu sona hello `–Port` parametre ve Remoting StorSimple sanal Gereci için yapılandırılan hello genel bağlantı noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="10cdb-167">Bu noktada, bir etkin uzaktan Windows PowerShell oturumu toohello cihaz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![HTTP kullanarak PowerShell uzaktan iletişim](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="10cdb-169">HTTPS bağlanır</span><span class="sxs-lookup"><span data-stu-id="10cdb-169">Connect through HTTPS</span></span>

<span data-ttu-id="10cdb-170">TooWindows PowerShell StorSimple için bir HTTPS oturumu aracılığıyla bağlanma hello en güvenli olduğundan ve uzaktan bağlanan tooyour Microsoft Azure StorSimple cihaz yöntemi önerilir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="10cdb-171">yordamları izleyerek hello nasıl tooset yukarı hello seri konsol ve istemci bilgisayarları için StorSimple HTTPS tooconnect tooWindows PowerShell kullanabilmesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="10cdb-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="10cdb-172">Her iki hello Azure portal veya hello seri konsol tooconfigure uzaktan yönetimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="10cdb-173">Yordamları izleyerek hello seçin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="10cdb-174">HTTPS üzerinden Hello Azure portal tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="10cdb-175">HTTPS üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="10cdb-176">Uzaktan Yönetimi etkinleştirdikten sonra Uzaktan Yönetim için yordamlar tooprepare hello konak aşağıdaki hello kullanın ve toohello aygıt hello uzak ana bilgisayara bağlanın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="10cdb-177">Merhaba konak uzaktan yönetimi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="10cdb-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="10cdb-178">Toohello aygıt hello uzak ana bilgisayara bağlanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="10cdb-179">HTTPS üzerinden Hello Azure portal tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="10cdb-180">HTTPS üzerinden adımlara hello Azure portal tooenable Uzaktan Yönetimi'nde hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="10cdb-181">tooenable hello Azure portal'den HTTPS üzerinden uzaktan yönetim</span><span class="sxs-lookup"><span data-stu-id="10cdb-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="10cdb-182">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="10cdb-183">Seçin **aygıtları** seçin ve Uzaktan Yönetim için kullanmak istediğiniz tooconfigure hello cihaz seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="10cdb-184">Çok Git**Aygıt Ayarları > Güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="10cdb-185">Merhaba, **güvenlik ayarları** dikey penceresinde tıklatın **Uzaktan Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="10cdb-186">Ayarlama **uzaktan yönetimini etkinleştirme** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="10cdb-187">Artık HTTPS kullanarak tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="10cdb-188">(Merhaba tooconnect HTTPS üzerinden varsayılandır.) HTTPS seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="10cdb-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="10cdb-189">Tıklatın ve ardından **uzaktan yönetim sertifikası indir**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="10cdb-190">Konum toosave bu dosyayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-190">Specify a location toosave this file.</span></span> <span data-ttu-id="10cdb-191">Bu sertifika tooconnect toohello aygıtını kullanacak hello istemci veya konak bilgisayarda tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="10cdb-192">Tıklatın **kaydetmek** ve ardından **Evet** onaylamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="10cdb-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="10cdb-193">HTTPS üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="10cdb-194">Aşağıdaki adımları hello cihaz seri konsoluna tooenable uzaktan yönetimi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="10cdb-195">tooenable hello cihaz seri Konsolu aracılığıyla uzaktan yönetim</span><span class="sxs-lookup"><span data-stu-id="10cdb-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="10cdb-196">Merhaba seri konsol menüsünde 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="10cdb-197">Hello aygıtta hello seri Konsolu kullanma hakkında daha fazla bilgi için çok Git[tooWindows PowerShell StorSimple için cihaz seri konsoluna bağlanmak](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="10cdb-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="10cdb-198">Merhaba istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="10cdb-199">Bu, Cihazınızda HTTPS etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="10cdb-200">Yazarak HTTPS etkin olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="10cdb-201">Bu hello emin olun **RemoteManagementMode** alan gösterir **HttpsEnabled**çizim aşağıdaki .hello PuTTY bu ayarları gösterir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seri HTTPS etkin](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="10cdb-203">Hello çıktısından `Get-HcsSystem`, kopyalama hello aygıtının hello seri numarasını ve daha sonra kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10cdb-204">Merhaba seri numarası toohello CN adı hello sertifikasında eşler.</span><span class="sxs-lookup"><span data-stu-id="10cdb-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="10cdb-205">Uzak Yönetim sertifikası yazarak alın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="10cdb-206">Sertifika benzer toohello aşağıdaki görünür.</span><span class="sxs-lookup"><span data-stu-id="10cdb-206">A certificate similar toohello following will appear.</span></span>
   
    ![Uzaktan Yönetim sertifikası alma](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="10cdb-208">Hello bilgi hello sertifikadan kopyalayın **---başlangıç sertifika---** çok**---son SERTİFİKAYI---** .cer dosyası olarak bir metin düzenleyicisine Not Defteri gibi ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="10cdb-209">(Merhaba konak hazırlarken bu dosya tooyour uzak ana kopyalayacak.)</span><span class="sxs-lookup"><span data-stu-id="10cdb-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10cdb-210">toogenerate yeni bir sertifika kullanmak hello `Set-HcsRemoteManagementCert` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="10cdb-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="10cdb-211">Merhaba konak uzaktan yönetimi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="10cdb-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="10cdb-212">tooprepare hello ana bilgisayar kullanan bir HTTPS oturumu uzaktan bağlantı hello yordamları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="10cdb-213">[İçeri aktarma hello .cer dosyası hello istemci ya da uzak ana hello kök deposuna](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="10cdb-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="10cdb-214">[Merhaba cihaz seri numaraları toohello hosts dosyasını uzak ana bilgisayarınızda eklemek](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="10cdb-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="10cdb-215">Her bir yordam, önceki hello aşağıda tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="10cdb-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="10cdb-216">Merhaba uzak ana bilgisayarda tooimport hello sertifika</span><span class="sxs-lookup"><span data-stu-id="10cdb-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="10cdb-217">Merhaba .cer dosyasını sağ tıklatın ve seçin **yükleme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="10cdb-218">Bu hello Sertifika Alma Sihirbazı'nı başlatır.</span><span class="sxs-lookup"><span data-stu-id="10cdb-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Sertifika Alma Sihirbazı 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="10cdb-220">İçin **depo konumuna**seçin **yerel makine**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="10cdb-221">Seçin **tüm sertifikaları deposu aşağıdaki hello Yerleştir**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="10cdb-222">Uzak ana bilgisayarınız toohello bir kök depoya gidin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Sertifika Alma Sihirbazı'nı 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="10cdb-224">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-224">Click **Finish**.</span></span> <span data-ttu-id="10cdb-225">Merhaba alma işleminin başarılı olduğunu bildiren bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="10cdb-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Sertifika Alma Sihirbazı'nı 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="10cdb-227">tooadd cihaz seri numaraları toohello uzak ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="10cdb-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="10cdb-228">Not Defteri'ni yönetici olarak başlatın ve sonra \Windows\System32\Drivers\etc bulunan hello hosts dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="10cdb-229">Aşağıdaki üç girişleri tooyour hosts dosyasına hello ekleyin: **veri 0 IP adresi**, **denetleyici 0 sabit IP adresi**, ve **Denetleyici 1 sabit IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="10cdb-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="10cdb-230">Daha önce kaydettiğiniz Hello cihaz seri numarasını girin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="10cdb-231">Bu toohello IP adresini hello görüntü aşağıdaki gösterildiği gibi eşleyin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="10cdb-232">Denetleyici 0 ve denetleyici 1 için sona **Controller0** ve **Controller1** hello sonunda hello seri numarası (CN adı).</span><span class="sxs-lookup"><span data-stu-id="10cdb-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![CN adı toohosts dosyası ekleme](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="10cdb-234">Kaydet hello hosts dosyasını.</span><span class="sxs-lookup"><span data-stu-id="10cdb-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="10cdb-235">Toohello aygıt hello uzak ana bilgisayara bağlanın</span><span class="sxs-lookup"><span data-stu-id="10cdb-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="10cdb-236">Windows PowerShell ve SSL kullanmak SSAdmin oturum bir uzak ana bilgisayara veya istemci, Cihazınızda bir tooenter.</span><span class="sxs-lookup"><span data-stu-id="10cdb-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="10cdb-237">Merhaba SSAdmin oturum eşlemeleri toooption 1 hello içinde [seri konsol](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) Cihazınızı menüsü.</span><span class="sxs-lookup"><span data-stu-id="10cdb-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="10cdb-238">Aşağıdaki yordamı toomake hello uzaktan Windows PowerShell bağlantı istediğiniz hello bilgisayarda hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="10cdb-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="10cdb-239">bir Windows PowerShell ve SSL kullanarak hello aygıt SSAdmin oturum tooenter</span><span class="sxs-lookup"><span data-stu-id="10cdb-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="10cdb-240">Bir Windows PowerShell oturumu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="10cdb-241">Merhaba aygıt IP adresi toohello istemcinin güvenilir konaklar yazarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="10cdb-242">Burada <*device_ip*> Cihazınızı hello IP adresidir; örneğin:</span><span class="sxs-lookup"><span data-stu-id="10cdb-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="10cdb-243">toocreate yeni bir kimlik bilgisi türü:</span><span class="sxs-lookup"><span data-stu-id="10cdb-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="10cdb-244">Burada <*hedef aygıtın IP*> hello IP adresi veri 0 aygıtınızın; Örneğin, **10.126.173.90** hello hosts dosyasını görüntüsü önceki hello gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="10cdb-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="10cdb-245">Ayrıca, Cihazınızı hello yönetici parolasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="10cdb-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="10cdb-246">Bir oturum yazarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10cdb-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="10cdb-247">Merhaba - ComputerName parametresi için Merhaba, hello sağlayın <*hedef cihaz seri numarasını*>.</span><span class="sxs-lookup"><span data-stu-id="10cdb-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="10cdb-248">Bu seri numarasına eşlendi veri uzak ana bilgisayarınızda; hello hosts dosyasında 0 toohello IP adresi Örneğin, **SHX0991003G44MT** hello görüntü aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="10cdb-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="10cdb-249">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="10cdb-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="10cdb-250">Birkaç dakika toowait gerekir ve ardından HTTPS üzerinden bağlı tooyour aygıt SSL üzerinden olacaktır.</span><span class="sxs-lookup"><span data-stu-id="10cdb-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="10cdb-251">Bağlı tooyour aygıt olduğunuz belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="10cdb-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![PowerShell uzaktan iletişimini HTTPS ve SSL kullanma](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="10cdb-253">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10cdb-253">Next steps</span></span>

* <span data-ttu-id="10cdb-254">Daha fazla bilgi edinmek [Windows PowerShell tooadminister StorSimple Cihazınızı kullanarak](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="10cdb-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="10cdb-255">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="10cdb-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

