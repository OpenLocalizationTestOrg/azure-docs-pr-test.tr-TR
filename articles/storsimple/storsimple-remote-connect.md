---
title: "StorSimple cihazınıza uzaktan bağlanma | Microsoft Docs"
description: "Cihazınızı uzaktan yönetim için yapılandırma ve HTTP veya HTTPS aracılığıyla StorSimple için Windows PowerShell için bağlanma açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="305e9-103">StorSimple 8000 serisi cihazınıza uzaktan bağlanma</span><span class="sxs-lookup"><span data-stu-id="305e9-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="305e9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="305e9-104">Overview</span></span>
<span data-ttu-id="305e9-105">StorSimple Cihazınızı bağlamak için Windows PowerShell uzaktan iletişimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="305e9-106">Bu şekilde bağlandığınızda, menü görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="305e9-107">(Yalnızca seri konsol cihazda bağlamak için kullanırsanız, bir menü bakın.) Windows PowerShell uzaktan iletişimini ile belirli bir çalışma bağlayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="305e9-108">Görüntüleme dili de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-108">You can also specify the display language.</span></span> 

<span data-ttu-id="305e9-109">Cihazınızı yönetmek için Windows PowerShell uzaktan iletişimini kullanma hakkında daha fazla bilgi için Git [StorSimple Cihazınızı yönetmek StorSimple için Windows PowerShell'i kullanın](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="305e9-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="305e9-110">Bu öğretici, Cihazınızı uzaktan yönetim için yapılandırma ve StorSimple için Windows PowerShell için bağlanma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="305e9-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="305e9-111">Windows PowerShell uzaktan iletişimini bağlanmak için HTTP veya HTTPS kullanın.</span><span class="sxs-lookup"><span data-stu-id="305e9-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="305e9-112">Ancak, StorSimple için Windows PowerShell'e bağlanmak nasıl karar verirken aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="305e9-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="305e9-113">Doğrudan cihaz seri konsoluna bağlanmak güvenlidir, ancak seri konsol ağ anahtarları bağlanma değil.</span><span class="sxs-lookup"><span data-stu-id="305e9-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="305e9-114">Cihaz seri konsoluna ağ anahtarları bağlanırken güvenlik riski dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="305e9-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="305e9-115">Bir HTTP oturumu aracılığıyla bağlanan ağ üzerinden seri konsol üzerinden bağlanma daha fazla güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="305e9-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="305e9-116">Bu en güvenli yöntemi olmamasına karşın, güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="305e9-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="305e9-117">Kendinden imzalı bir sertifika ile HTTPS oturumu aracılığıyla bağlanan en güvenli ve önerilen seçenek olur.</span><span class="sxs-lookup"><span data-stu-id="305e9-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="305e9-118">Windows PowerShell arabirimine uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="305e9-119">Ancak, Windows PowerShell arabirimi üzerinden StorSimple cihazınız için uzaktan erişim varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="305e9-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="305e9-120">İlk cihazda uzaktan yönetimi etkinleştirmek gereken ve ardından istemci üzerinde Cihazınızı erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="305e9-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="305e9-121">Bu makalede açıklanan adımları Windows Server 2012 R2 çalıştıran bir konak sisteminde gerçekleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="305e9-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="305e9-122">HTTP bağlanma</span><span class="sxs-lookup"><span data-stu-id="305e9-122">Connect through HTTP</span></span>
<span data-ttu-id="305e9-123">Windows PowerShell için StorSimple için bir HTTP oturumu aracılığıyla bağlanma StorSimple Cihazınızı seri konsol üzerinden bağlanma daha fazla güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="305e9-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="305e9-124">Bu en güvenli yöntemi olmamasına karşın, güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="305e9-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="305e9-125">Uzaktan yönetimini yapılandırmak için Klasik Azure portalı veya seri Konsolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="305e9-126">Aşağıdaki yordamlardan seçin:</span><span class="sxs-lookup"><span data-stu-id="305e9-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="305e9-127">HTTP üzerinden uzaktan yönetimi etkinleştirmek için Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="305e9-128">Seri konsol HTTP üzerinden uzaktan yönetimi etkinleştirmek için kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="305e9-129">Uzaktan Yönetimi etkinleştirdikten sonra istemci uzak bir bağlantı için hazırlamak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="305e9-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="305e9-130">Uzak bağlantı için istemci hazırlayın</span><span class="sxs-lookup"><span data-stu-id="305e9-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="305e9-131">HTTP üzerinden uzaktan yönetimi etkinleştirmek için Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="305e9-132">HTTP üzerinden uzaktan yönetimi etkinleştirmek için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="305e9-133">Klasik Azure portalı üzerinden uzaktan yönetimi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="305e9-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="305e9-134">Erişim **aygıtları** > **yapılandırma** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="305e9-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="305e9-135">Ekranı kaydırarak **Uzaktan Yönetim** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="305e9-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="305e9-136">**Uzaktan yönetimi Etkinleştir**’i **Evet** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="305e9-137">Artık HTTP kullanarak bağlanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="305e9-138">(HTTPS üzerinden bağlanmak için varsayılandır.) HTTP seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="305e9-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="305e9-139">HTTP üzerinden bağlanma yalnızca güvenilen ağlarda kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="305e9-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="305e9-140">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="305e9-141">Seri konsol HTTP üzerinden uzaktan yönetimi etkinleştirmek için kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="305e9-142">Uzaktan Yönetimi etkinleştirmek için cihaz seri konsoluna aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="305e9-143">Cihaz seri Konsolu aracılığıyla uzaktan yönetimini etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="305e9-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="305e9-144">Seri konsol menüsünde 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="305e9-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="305e9-145">Cihaza seri Konsolu kullanma hakkında daha fazla bilgi için Git [cihaz seri Konsolu aracılığıyla StorSimple için Windows PowerShell Bağlan](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="305e9-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="305e9-146">İstemine yazın:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="305e9-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="305e9-147">Cihaza bağlanmak için HTTP kullanmanın güvenlik açıkları hakkında bildirilir.</span><span class="sxs-lookup"><span data-stu-id="305e9-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="305e9-148">İstendiğinde, yazarak onaylayın **Y**.</span><span class="sxs-lookup"><span data-stu-id="305e9-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="305e9-149">HTTP yazarak etkin olduğunu doğrulayın:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="305e9-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="305e9-150">Doğrulayın **RemoteManagementMode** alan gösterir **HttpsAndHttpEnabled**. Aşağıdaki çizimde, bu ayarları içinde PuTTY gösterir.</span><span class="sxs-lookup"><span data-stu-id="305e9-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seri HTTPS ve HTTP Etkin](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="305e9-152">Uzak bağlantı için istemci hazırlayın</span><span class="sxs-lookup"><span data-stu-id="305e9-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="305e9-153">Uzaktan Yönetimi etkinleştirmek için istemcide aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="305e9-154">Uzak bağlantı için istemci hazırlamak için</span><span class="sxs-lookup"><span data-stu-id="305e9-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="305e9-155">Bir Windows PowerShell oturumu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="305e9-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="305e9-156">StorSimple cihazı IP adresi istemcinin güvenilir ana bilgisayarlar listesine eklemek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="305e9-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="305e9-157">Değiştir <*device_ip*> Cihazınızı; IP adresi ile örneğin:</span><span class="sxs-lookup"><span data-stu-id="305e9-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="305e9-158">Cihaz kimlik bilgileri bir değişkene kaydetmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="305e9-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="305e9-159">Görüntülenen iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="305e9-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="305e9-160">Kullanıcı adı şu biçimde yazın: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="305e9-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="305e9-161">Cihaz Kurulum Sihirbazı ile yapılandırıldığında ayarlandı aygıt yönetici parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="305e9-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="305e9-162">Varsayılan parola *Parola1*.</span><span class="sxs-lookup"><span data-stu-id="305e9-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="305e9-163">Bir Windows PowerShell oturumunda aşağıdaki komutu yazarak cihazda başlatın:</span><span class="sxs-lookup"><span data-stu-id="305e9-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="305e9-164">StorSimple sanal cihazı ile kullanmak için bir Windows PowerShell oturumu oluşturmak için Ekle `–Port` parametre ve Remoting StorSimple sanal Gereci için yapılandırılmış ortak bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="305e9-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="305e9-165">Bu aşamada, aygıta bir etkin uzaktan Windows PowerShell oturumu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="305e9-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![HTTP kullanarak PowerShell uzaktan iletişim](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="305e9-167">HTTPS bağlanır</span><span class="sxs-lookup"><span data-stu-id="305e9-167">Connect through HTTPS</span></span>
<span data-ttu-id="305e9-168">Windows PowerShell için StorSimple için bir HTTPS oturumu aracılığıyla bağlanma Microsoft Azure StorSimple cihazınıza uzaktan bağlanma en güvenli ve önerilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="305e9-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="305e9-169">Aşağıdaki yordamlar, seri konsol ve istemci bilgisayarları StorSimple için Windows PowerShell'e bağlanmak için HTTPS kullanacak şekilde ayarlamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="305e9-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="305e9-170">Uzaktan yönetimini yapılandırmak için Klasik Azure portalı veya seri Konsolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="305e9-171">Aşağıdaki yordamlardan seçin:</span><span class="sxs-lookup"><span data-stu-id="305e9-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="305e9-172">HTTPS üzerinden uzaktan yönetimi etkinleştirmek için Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="305e9-173">Seri konsol HTTPS üzerinden uzaktan yönetimi etkinleştirmek için kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="305e9-174">Uzaktan Yönetimi etkinleştirdikten sonra ana bilgisayar bir uzaktan yönetime hazırlamak ve aygıta uzak ana bilgisayara bağlanmak için aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="305e9-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="305e9-175">Konağın uzaktan yönetimi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="305e9-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="305e9-176">Uzak ana bilgisayardan cihaza bağlanın</span><span class="sxs-lookup"><span data-stu-id="305e9-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="305e9-177">HTTPS üzerinden uzaktan yönetimi etkinleştirmek için Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="305e9-178">HTTPS üzerinden uzaktan yönetimi etkinleştirmek için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="305e9-179">Klasik Azure portalından HTTPS üzerinden uzaktan yönetimi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="305e9-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="305e9-180">Erişim **aygıtları** > **yapılandırma** cihazınız için.</span><span class="sxs-lookup"><span data-stu-id="305e9-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="305e9-181">Ekranı kaydırarak **Uzaktan Yönetim** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="305e9-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="305e9-182">**Uzaktan yönetimi Etkinleştir**’i **Evet** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="305e9-183">Artık HTTPS kullanarak bağlanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305e9-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="305e9-184">(HTTPS üzerinden bağlanmak için varsayılandır.) HTTPS seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="305e9-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="305e9-185">Tıklatın **uzak yönetim sertifikası indir**.</span><span class="sxs-lookup"><span data-stu-id="305e9-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="305e9-186">Bu dosyayı kaydetmek için bir konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="305e9-186">Specify a location to save this file.</span></span> <span data-ttu-id="305e9-187">Bu sertifikayı cihaza bağlanmak için kullanacağınız istemci veya ana bilgisayarda yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="305e9-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="305e9-188">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="305e9-189">Seri konsol HTTPS üzerinden uzaktan yönetimi etkinleştirmek için kullanın</span><span class="sxs-lookup"><span data-stu-id="305e9-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="305e9-190">Uzaktan Yönetimi etkinleştirmek için cihaz seri konsoluna aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="305e9-191">Cihaz seri Konsolu aracılığıyla uzaktan yönetimini etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="305e9-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="305e9-192">Seri konsol menüsünde 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="305e9-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="305e9-193">Cihaza seri Konsolu kullanma hakkında daha fazla bilgi için Git [cihaz seri Konsolu aracılığıyla StorSimple için Windows PowerShell Bağlan](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="305e9-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="305e9-194">İstemine yazın:</span><span class="sxs-lookup"><span data-stu-id="305e9-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="305e9-195">Bu, Cihazınızda HTTPS etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="305e9-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="305e9-196">Yazarak HTTPS etkin olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="305e9-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="305e9-197">Olduğundan emin olun **RemoteManagementMode** alan gösterir **HttpsEnabled**. Aşağıdaki çizimde, bu ayarları içinde PuTTY gösterir.</span><span class="sxs-lookup"><span data-stu-id="305e9-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seri HTTPS etkin](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="305e9-199">Çıktısından `Get-HcsSystem`, cihazın seri numarası kopyalayın ve daha sonra kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="305e9-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="305e9-200">Seri numarası sertifikanın CN adı eşler.</span><span class="sxs-lookup"><span data-stu-id="305e9-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="305e9-201">Uzak Yönetim sertifikası yazarak alın:</span><span class="sxs-lookup"><span data-stu-id="305e9-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="305e9-202">Bir sertifika aşağıdakine benzer görünecektir.</span><span class="sxs-lookup"><span data-stu-id="305e9-202">A certificate similar to the following will appear.</span></span>
   
    ![Uzaktan Yönetim sertifikası alma](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="305e9-204">Sertifika bilgileri kopyalayın **---başlangıç sertifika---** için **---son SERTİFİKAYI---** .cer dosyası olarak bir metin düzenleyicisine Not Defteri gibi ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="305e9-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="305e9-205">(Konak hazırlarken bu dosyayı uzak ana bilgisayara kopyalayacak.)</span><span class="sxs-lookup"><span data-stu-id="305e9-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="305e9-206">Yeni bir sertifika oluşturmak için kullanın `Set-HcsRemoteManagementCert` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="305e9-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="305e9-207">Konağın uzaktan yönetimi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="305e9-207">Prepare the host for remote management</span></span>
<span data-ttu-id="305e9-208">Bir HTTPS oturumu kullanan uzak bir bağlantı için ana bilgisayarı hazırlamak için aşağıdaki yordamları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="305e9-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="305e9-209">[İstemci veya uzak ana bilgisayarın kök deposuna .cer dosyasını içeri](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="305e9-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="305e9-210">[Uzak ana bilgisayarda hosts dosyasını cihaz seri numaraları eklemek](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="305e9-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="305e9-211">Bu yordamların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="305e9-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="305e9-212">Uzak ana bilgisayarda sertifikasını içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="305e9-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="305e9-213">.Cer dosyasını sağ tıklatın ve seçin **yükleme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="305e9-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="305e9-214">Bu Sertifika Alma Sihirbazı'nı başlatır.</span><span class="sxs-lookup"><span data-stu-id="305e9-214">This will start the Certificate Import Wizard.</span></span>
   
    ![Sertifika Alma Sihirbazı 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="305e9-216">İçin **depo konumuna**seçin **yerel makine**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="305e9-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="305e9-217">Seçin **tüm sertifikaları aşağıdaki depolama alanına yerleştir**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="305e9-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="305e9-218">Uzak ana bilgisayarınız kök deposuna gidin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="305e9-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Sertifika Alma Sihirbazı'nı 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="305e9-220">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-220">Click **Finish**.</span></span> <span data-ttu-id="305e9-221">Alma işleminin başarılı olduğunu bildiren bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="305e9-221">A message that tells you that the import was successful appears.</span></span>
   
    ![Sertifika Alma Sihirbazı'nı 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="305e9-223">Cihaz seri numaraları uzak ana bilgisayara eklemek için</span><span class="sxs-lookup"><span data-stu-id="305e9-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="305e9-224">Not Defteri'ni yönetici olarak başlatın ve sonra \Windows\System32\Drivers\etc bulunan hosts dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="305e9-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="305e9-225">Aşağıdaki üç girdileri hosts dosyanıza ekleyin: **veri 0 IP adresi**, **denetleyici 0 sabit IP adresi**, ve **Denetleyici 1 sabit IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="305e9-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="305e9-226">Daha önce kaydettiğiniz cihaz seri numarasını girin.</span><span class="sxs-lookup"><span data-stu-id="305e9-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="305e9-227">Aşağıdaki görüntüde gösterildiği gibi bu IP adresine eşleyen.</span><span class="sxs-lookup"><span data-stu-id="305e9-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="305e9-228">Denetleyici 0 ve denetleyici 1 için sona **Controller0** ve **Controller1** seri numarasını (CN adı), sonunda.</span><span class="sxs-lookup"><span data-stu-id="305e9-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Konaklar dosyasına CN adı ekleme](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="305e9-230">Hosts dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="305e9-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="305e9-231">Uzak ana bilgisayardan cihaza bağlanın</span><span class="sxs-lookup"><span data-stu-id="305e9-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="305e9-232">Bir uzak ana bilgisayara veya istemci, Cihazınızda bir SSAdmin oturumu girmek için Windows PowerShell ve SSL kullanın.</span><span class="sxs-lookup"><span data-stu-id="305e9-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="305e9-233">1 seçeneğinde SSAdmin oturum eşlendiği [seri konsol](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) Cihazınızı menüsü.</span><span class="sxs-lookup"><span data-stu-id="305e9-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="305e9-234">Aşağıdaki yordam, uzak Windows PowerShell bağlantı kurmak istediğiniz bilgisayarda gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="305e9-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="305e9-235">Windows PowerShell ve SSL kullanarak aygıtta bir SSAdmin oturumu girmek için</span><span class="sxs-lookup"><span data-stu-id="305e9-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="305e9-236">Bir Windows PowerShell oturumu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="305e9-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="305e9-237">Aygıt IP adresi yazarak istemcinin güvenilir konaklar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="305e9-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="305e9-238">Burada <*device_ip*> cihazınızın IP adresidir; örneğin:</span><span class="sxs-lookup"><span data-stu-id="305e9-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="305e9-239">Yeni bir kimlik bilgisi yazarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="305e9-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="305e9-240">Burada <*hedef aygıtın IP*> cihazınız için; veri 0 IP adresidir Örneğin, **10.126.173.90** hosts dosyasını önceki görüntüde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="305e9-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="305e9-241">Ayrıca, cihazınız için yönetici parolasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="305e9-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="305e9-242">Bir oturum yazarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="305e9-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="305e9-243">Cmdlet - ComputerName parametresinde için sağlayın <*hedef cihaz seri numarasını*>.</span><span class="sxs-lookup"><span data-stu-id="305e9-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="305e9-244">Bu seri numarasına veri uzak ana bilgisayarda hosts dosyasında 0 IP adresine eşlendi; Örneğin, **SHX0991003G44MT** aşağıdaki görüntüde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="305e9-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="305e9-245">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="305e9-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="305e9-246">Birkaç dakika beklemeniz gerekir ve ardından, HTTPS üzerinden aygıtınıza SSL üzerinden bağlanır.</span><span class="sxs-lookup"><span data-stu-id="305e9-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="305e9-247">Cihazınıza bağlı belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="305e9-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![PowerShell uzaktan iletişimini HTTPS ve SSL kullanma](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="305e9-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="305e9-249">Next steps</span></span>
* <span data-ttu-id="305e9-250">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için Windows PowerShell kullanarak](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="305e9-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="305e9-251">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="305e9-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

