---
title: "Veri Yönetimi ağ geçidi aaaTroubleshoot sorunları | Microsoft Docs"
description: "İpuçları tootroubleshoot sorunları ilgili tooData Yönetimi ağ geçidi sağlar."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="47d90-103">Veri Yönetimi Ağ Geçidi kullanımıyla ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="47d90-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="47d90-104">Bu makalede, veri yönetimi ağ geçidi kullanarak sorunlarını giderme hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="47d90-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="47d90-105">Merhaba bkz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) hello ağ geçidi hakkında ayrıntılı bilgi için makalenin.</span><span class="sxs-lookup"><span data-stu-id="47d90-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="47d90-106">Merhaba bkz [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) hello ağ geçidi kullanarak bir şirket içi SQL Server veritabanı tooMicrosoft Azure Blob Depolama veri taşıma makale kılavuz.</span><span class="sxs-lookup"><span data-stu-id="47d90-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="47d90-107">Tooinstall veya kaydı başarısız ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="47d90-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="47d90-108">1. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-108">1. Problem</span></span>
<span data-ttu-id="47d90-109">Yüklerken ve hello ağ geçidi yükleme dosyası indirilirken bir ağ geçidi özellikle kaydetme bu hata iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="47d90-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="47d90-110">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-110">Cause</span></span>
<span data-ttu-id="47d90-111">Merhaba makine tooinstall hello ağ geçidi çalıştığınız toodownload hello son ağ geçidi yükleme dosyasını hello İndirme Merkezi'nden tooa ağ sorunu nedeniyle başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="47d90-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-112">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-112">Resolution</span></span>
<span data-ttu-id="47d90-113">Merhaba bilgisayar toohello hello ağ bağlantısından Hello ayarları engelleyip engellemeyeceğini, güvenlik duvarı proxy sunucusu ayarları toosee denetleyin [İndirme Merkezinden](https://download.microsoft.com/)ve güncelleştirme hello ayarları buna göre.</span><span class="sxs-lookup"><span data-stu-id="47d90-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="47d90-114">Alternatif olarak, hello hello en son ağ geçidi için hello yükleme dosyası indirebilirsiniz [İndirme Merkezinden](https://www.microsoft.com/download/details.aspx?id=39717) diğer makinelere hello Yükleme Merkezi'nden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="47d90-115">Kopya hello yükleyici dosya toohello ağ geçidi ana bilgisayarı ve tooinstall ve güncelleştirme hello ağ geçidi el ile çalıştırın sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="47d90-116">2. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-116">2. Problem</span></span>
<span data-ttu-id="47d90-117">Tıklayarak tooinstall bir ağ geçidi denediğiniz olduğunda bu hata bkz **doğrudan bu bilgisayar Yükle** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="47d90-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="47d90-118">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-118">Cause</span></span>
<span data-ttu-id="47d90-119">Bir ağ geçidi hello makinede zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="47d90-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-120">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-120">Resolution</span></span>
<span data-ttu-id="47d90-121">Merhaba hello makinedeki mevcut ağ geçidi kaldırın ve hello tıklatın **doğrudan bu bilgisayar Yükle** yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="47d90-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="47d90-122">3. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-122">3. Problem</span></span>
<span data-ttu-id="47d90-123">Yeni bir ağ geçidi kaydederken, bu hatayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="47d90-124">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-124">Cause</span></span>
<span data-ttu-id="47d90-125">Merhaba aşağıdaki nedenlerden biri için bu iletiyi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47d90-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="47d90-126">Merhaba ağ geçidi anahtarı Hello biçimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="47d90-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="47d90-127">Merhaba ağ geçidi anahtarı geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="47d90-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="47d90-128">Merhaba ağ geçidi anahtarı hello portalından yeniden.</span><span class="sxs-lookup"><span data-stu-id="47d90-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="47d90-129">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-129">Resolution</span></span>
<span data-ttu-id="47d90-130">Merhaba portalından hello doğru ağ geçidi anahtarı kullanarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="47d90-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="47d90-131">Gerekirse, bir anahtarın yeniden oluşturulması ve hello anahtar tooregister hello ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="47d90-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="47d90-132">4. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-132">4. Problem</span></span>
<span data-ttu-id="47d90-133">Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![İçerik veya anahtar biçimi geçersiz](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="47d90-135">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-135">Cause</span></span>
<span data-ttu-id="47d90-136">Merhaba içerik veya hello giriş ağ geçidi anahtarı biçimi doğru değil.</span><span class="sxs-lookup"><span data-stu-id="47d90-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="47d90-137">Merhaba nedenlerden biri dolayısıyla hello anahtarının yalnızca bir kısmını hello portalından kopyalandığından veya geçersiz bir anahtar kullandığınız olabilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-138">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-138">Resolution</span></span>
<span data-ttu-id="47d90-139">Hello Portalı'nda bir ağ geçidi anahtarı oluşturur ve hello Kopyala düğmesine toocopy hello tüm tuşunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="47d90-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="47d90-140">Ardından bu pencere tooregister hello ağ geçidi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="47d90-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="47d90-141">5. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-141">5. Problem</span></span>
<span data-ttu-id="47d90-142">Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Ağ geçidi anahtarı geçersiz veya boş değil](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="47d90-144">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-144">Cause</span></span>
<span data-ttu-id="47d90-145">Merhaba ağ geçidi anahtarı yeniden veya hello Azure portal hello ağ geçidi silinmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="47d90-146">Merhaba veri yönetimi ağ geçidi Kurulum en son değilse de oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-147">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-147">Resolution</span></span>
<span data-ttu-id="47d90-148">Merhaba veri yönetimi ağ geçidi Kurulum hello en son sürüm ise, bulabilirsiniz hello en son sürümünü Microsoft hello üzerinde kontrol [İndirme Merkezinden](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="47d90-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="47d90-149">Kurulum geçerli / son ve ağ geçidi portalında hala var, hello ağ geçidi anahtarı hello Azure portal'ın yeniden hello Kopyala düğmesine toocopy hello tüm tuşunu kullanın ve bu pencere tooregister hello ağ geçidi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="47d90-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="47d90-150">Aksi takdirde hello ağ geçidi yeniden oluşturun ve baştan başlayın.</span><span class="sxs-lookup"><span data-stu-id="47d90-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="47d90-151">6. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-151">6. Problem</span></span>
<span data-ttu-id="47d90-152">Bir ağ geçidi kaydedilirken hata iletisi aşağıdaki hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Ağ geçidi anahtarı geçersiz veya boş değil](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="47d90-154">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-154">Cause</span></span>
<span data-ttu-id="47d90-155">Bu hata, hello ağ geçidi silinmiş olabilir ya da hello ilişkili ağ geçidi anahtarı yeniden olmadığından gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-156">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-156">Resolution</span></span>
<span data-ttu-id="47d90-157">Merhaba ağ geçidi silinip hello ağ geçidi hello portalından yeniden oluşturmak, tıklatın **kaydetmek**hello portalından hello anahtarı kopyalayın, yapıştırın ve tooregister hello ağ geçidi deneyin.</span><span class="sxs-lookup"><span data-stu-id="47d90-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="47d90-158">Merhaba ağ geçidi hala var, ancak kendi anahtarı yeniden hello yeni anahtar tooregister hello ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="47d90-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="47d90-159">Merhaba anahtar yoksa, hello portalından yeniden hello tuşunu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47d90-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="47d90-160">7. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-160">7. Problem</span></span>
<span data-ttu-id="47d90-161">Bir ağ geçidi kaydedilirken tooenter yolu ve parola için bir sertifika gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Sertifika belirtin](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="47d90-163">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-163">Cause</span></span>
<span data-ttu-id="47d90-164">Merhaba ağ geçidi, önce diğer makinelere kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="47d90-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="47d90-165">Merhaba ilk kaydı bir ağ geçidi sırasında bir şifreleme sertifikası hello ağ geçidi ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="47d90-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="47d90-166">Merhaba sertifika hello ağ geçidi tarafından otomatik olarak oluşturulan veya hello kullanıcı tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="47d90-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="47d90-167">Bu sertifika hello veri deposu (bağlantılı hizmeti) kullanılan tooencrypt kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="47d90-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Sertifika verme](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="47d90-169">Ne zaman bu sertifika toodecrypt daha önce kimlik bilgileri için farklı bir konak makinesi üzerinde hello ağ geçidi hello Kayıt Sihirbazı'nı ister geri Bu sertifika ile şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="47d90-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="47d90-170">Bu sertifika olmadan hello kimlik hello yeni ağ geçidi tarafından şifresi çözülemiyor ve bu yeni ağ geçidi ile ilişkili sonraki kopyalama etkinliği yürütmeleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="47d90-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="47d90-171">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-171">Resolution</span></span>
<span data-ttu-id="47d90-172">Merhaba kimlik bilgileri sertifikası hello kullanarak hello özgün ağ geçidi makineden dışarı aktardıysanız **verme** hello düğmesinde **ayarları** sekmesinde Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi'nde, hello kullanın Burada sertifikası.</span><span class="sxs-lookup"><span data-stu-id="47d90-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="47d90-173">Bu aşamada, ağ geçidi kurtarırken atlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="47d90-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="47d90-174">Merhaba sertifika yoksa, hello portalından toodelete hello ağ geçidine gereksinimi ve yeni bir ağ geçidi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47d90-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="47d90-175">Ayrıca, kullanıcıların kimlik bilgilerini yeniden girme ilgili toohello ağ geçidi olan tüm bağlantılı Hizmetleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="47d90-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="47d90-176">8. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-176">8. Problem</span></span>
<span data-ttu-id="47d90-177">Aşağıdaki hata iletisini hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="47d90-178">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-178">Cause</span></span>
<span data-ttu-id="47d90-179">Ağ geçidiniz bir HTTP proxy tooaccess Internet kaynakların gerektiren bir ortamda olduğunda bu hata oluşur veya proxy'nın kimlik doğrulaması parola değiştirilir, ancak uygun şekilde güncelleştirilmesi ağ geçidiniz içinde.</span><span class="sxs-lookup"><span data-stu-id="47d90-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-180">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-180">Resolution</span></span>
<span data-ttu-id="47d90-181">Merhaba Hello yönergeleri izleyin [Proxy sunucusu hususları](#proxy-server-considerations) bu bölümü makalesi ve veri yönetimi ağ geçidi Yapılandırma Yöneticisi ile proxy ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47d90-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="47d90-182">Ağ geçidi ile sınırlı işlevsellik çevrimiçi duruma</span><span class="sxs-lookup"><span data-stu-id="47d90-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="47d90-183">1. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-183">1. Problem</span></span>
<span data-ttu-id="47d90-184">Sınırlı işlevlerle çevrimiçi olarak hello ağ geçidi hello durumunu görebilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="47d90-185">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-185">Cause</span></span>
<span data-ttu-id="47d90-186">Hello durum hello ağ geçidinin çevrimiçi hello aşağıdaki nedenlerden biri için sınırlı işlevsellik ile görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="47d90-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="47d90-187">Ağ geçidi, Azure Service Bus toocloud hizmetine bağlanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="47d90-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="47d90-188">Bulut hizmeti, hizmet veri yolu toogateway bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="47d90-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="47d90-189">Merhaba ağ geçidi ile sınırlı işlevsellik çevrimiçi olduğunda, şirket içi veri depolarına veri tooor kopyalama mümkün toouse hello Data Factory Kopyalama Sihirbazı toocreate veri ardışık olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="47d90-190">Geçici bir çözüm olarak, Data Factory Düzenleyici hello portal, Visual Studio ya da Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-191">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-191">Resolution</span></span>
<span data-ttu-id="47d90-192">Bu sorun için çözüm (sınırlı işlevsellik ile çevrimiçi) olup olmadığını hello ağ geçidi olamaz toohello bulut hizmetine bağlanın ya da başka bir şekilde hello temel alan.</span><span class="sxs-lookup"><span data-stu-id="47d90-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="47d90-193">Aşağıdaki bölümlerde hello bu çözümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="47d90-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="47d90-194">2. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-194">2. Problem</span></span>
<span data-ttu-id="47d90-195">Aşağıdaki hata hello bakın.</span><span class="sxs-lookup"><span data-stu-id="47d90-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Ağ geçidi toocloud hizmetine bağlanılamıyor](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="47d90-197">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-197">Cause</span></span>
<span data-ttu-id="47d90-198">Ağ geçidi Service Bus toohello bulut hizmetine bağlanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="47d90-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-199">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-199">Resolution</span></span>
<span data-ttu-id="47d90-200">Bu adımları tooget hello ağ geçidi tekrar çevrimiçi izleyin:</span><span class="sxs-lookup"><span data-stu-id="47d90-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="47d90-201">IP adresi hello ağ geçidi makinesindeki ve hello Kurumsal güvenlik duvarı giden kuralları izin verir.</span><span class="sxs-lookup"><span data-stu-id="47d90-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="47d90-202">Merhaba Windows olay günlüğü IP adreslerinden bulabilirsiniz (kimliği 401 ==): bir girişim yapıldı, erişim izinleri XX Yasak şekilde yuva tooaccess yapılan. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="47d90-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="47d90-203">Merhaba ağ geçidinde proxy ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47d90-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="47d90-204">Merhaba bkz [Proxy sunucusu hususları](#proxy-server-considerations) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="47d90-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="47d90-205">Giden bağlantı noktası 5671 ve 9350-9354 hem ' % s'hello Windows Güvenlik Duvarı hello ağ geçidi makinesindeki ve hello Kurumsal güvenlik duvarı üzerinde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="47d90-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="47d90-206">Merhaba bkz [bağlantı noktalarını ve Güvenlik Duvarı](#ports-and-firewall) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="47d90-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="47d90-207">Bu adım isteğe bağlıdır, ancak performans açıklamasında öneririz.</span><span class="sxs-lookup"><span data-stu-id="47d90-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="47d90-208">3. Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-208">3. Problem</span></span>
<span data-ttu-id="47d90-209">Aşağıdaki hata hello bakın.</span><span class="sxs-lookup"><span data-stu-id="47d90-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="47d90-210">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-210">Cause</span></span>
<span data-ttu-id="47d90-211">Ağ bağlantısı geçici bir hata.</span><span class="sxs-lookup"><span data-stu-id="47d90-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-212">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-212">Resolution</span></span>
<span data-ttu-id="47d90-213">Bu adımları tooget hello ağ geçidi tekrar çevrimiçi izleyin:</span><span class="sxs-lookup"><span data-stu-id="47d90-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="47d90-214">Birkaç dakika bekleyin, hello hata kaldırılmıştır olduğunda hello bağlantısı otomatik olarak kurtarılacak.</span><span class="sxs-lookup"><span data-stu-id="47d90-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="47d90-215">Merhaba hata devam ederse hello ağ geçidi hizmeti yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="47d90-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="47d90-216">Başarısız tooauthor bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="47d90-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="47d90-217">Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-217">Problem</span></span>
<span data-ttu-id="47d90-218">Yeni bağlı hizmet için hello portal tooinput kimlik bilgilerini toouse kimlik bilgileri Yöneticisi deneyin ya da mevcut bir bağlı hizmeti için kimlik bilgilerini güncelleştirmeniz bu hatayı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="47d90-219">Bu hatayı gördüğünüzde hello Ayarları sayfası veri yönetimi ağ geçidi Yapılandırma Yöneticisi'nin ekran görüntüsü aşağıdaki hello gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Veritabanına erişilemiyor](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="47d90-221">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-221">Cause</span></span>
<span data-ttu-id="47d90-222">Merhaba SSL sertifikası hello ağ geçidi makinede kesilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="47d90-223">Merhaba ağ geçidi bilgisayarı SSL şifreleme için kullanılan hello sertifika şu anda yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="47d90-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="47d90-224">Bir hata iletisi hello olay günlüğünde, iletiden benzer toohello olduğunu da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="47d90-225">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-225">Resolution</span></span>
<span data-ttu-id="47d90-226">Bu adımları toosolve hello sorunu izleyin:</span><span class="sxs-lookup"><span data-stu-id="47d90-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="47d90-227">Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="47d90-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="47d90-228">Geçiş toohello **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="47d90-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="47d90-229">Merhaba tıklatın **değişiklik** düğmesini toochange hello SSL sertifikası.</span><span class="sxs-lookup"><span data-stu-id="47d90-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Değişiklik sertifika düğmesi](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="47d90-231">Merhaba SSL sertifikası olarak yeni bir sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="47d90-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="47d90-232">Sizin tarafınızdan oluşturulan herhangi bir SSL sertifikası veya herhangi bir kuruluştaki kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Sertifika belirtin](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="47d90-234">Kopyalama etkinliği başarısız</span><span class="sxs-lookup"><span data-stu-id="47d90-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="47d90-235">Sorun</span><span class="sxs-lookup"><span data-stu-id="47d90-235">Problem</span></span>
<span data-ttu-id="47d90-236">Ardışık Düzen hello portalında ayarladıktan sonra "UserErrorFailedToConnectToSqlserver" hatasının ardından hello fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="47d90-237">Nedeni</span><span class="sxs-lookup"><span data-stu-id="47d90-237">Cause</span></span>
<span data-ttu-id="47d90-238">Bu farklı nedenlerden kaynaklanabilir ve azaltma buna göre değişir.</span><span class="sxs-lookup"><span data-stu-id="47d90-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="47d90-239">Çözüm</span><span class="sxs-lookup"><span data-stu-id="47d90-239">Resolution</span></span>
<span data-ttu-id="47d90-240">Tooan SQL veritabanına bağlanmadan önce bağlantı noktası TCP/1433 hello veri yönetimi ağ geçidi istemci tarafı üzerinden giden TCP bağlantılarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="47d90-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="47d90-241">Hello hedef veritabanının Azure SQL veritabanını, SQL Server için Güvenlik Duvarı ayarlarını Azure de kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="47d90-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="47d90-242">Aşağıdaki bölümde tootest hello bağlantı toohello şirket içi veri deposu hello bakın.</span><span class="sxs-lookup"><span data-stu-id="47d90-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="47d90-243">Veri deposu bağlantısı veya sürücüsü ile ilgili hataları</span><span class="sxs-lookup"><span data-stu-id="47d90-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="47d90-244">Veri deposunda bağlantı veya sürücü ilgili hatalar görürseniz, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="47d90-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="47d90-245">Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi hello ağ geçidi makinede başlatın.</span><span class="sxs-lookup"><span data-stu-id="47d90-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="47d90-246">Geçiş toohello **tanılama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="47d90-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="47d90-247">İçinde **Bağlantıyı Sına**, hello ağ geçidi Grup değerlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="47d90-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="47d90-248">Tıklatın **Test** toohello bağlanabiliyorsa toosee şirket içi veri kaynağından hello ağ geçidi makinesi hello bağlantı bilgilerini ve kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="47d90-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="47d90-249">Bir sürücü yükledikten sonra hello bağlantı testi yine başarısız olursa yeniden hello ağ geçidi için toopick hello son değişiklik ayarlama.</span><span class="sxs-lookup"><span data-stu-id="47d90-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Tanılama sekmesinde bağlantıyı Sına](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="47d90-251">Ağ geçidi günlükleri</span><span class="sxs-lookup"><span data-stu-id="47d90-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="47d90-252">Ağ geçidi günlüklerini tooMicrosoft Gönder</span><span class="sxs-lookup"><span data-stu-id="47d90-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="47d90-253">Ağ geçidi sorunlarını giderme ile Microsoft Support tooget Yardım başvurduğunuzda tooshare istenebilir ağ geçidi günlüklerinizi.</span><span class="sxs-lookup"><span data-stu-id="47d90-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="47d90-254">Merhaba ağ geçidinin Hello sürümle birlikte, gerekli ağ geçidi günlüklerini iki düğme tıklama veri yönetimi ağ geçidi Yapılandırma Yöneticisi ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="47d90-255">Geçiş toohello **tanılama** sekmesini veri yönetimi ağ geçidi Yapılandırma Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="47d90-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Veri Yönetimi ağ geçidi Tanılama sekmesi](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="47d90-257">Tıklatın **günlükleri Gönder** iletişim kutusunda aşağıdaki toosee hello.</span><span class="sxs-lookup"><span data-stu-id="47d90-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Veri Yönetimi ağ geçidi Gönder günlükleri](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="47d90-259">(İsteğe bağlı) Tıklatın **günlüklerini görüntülemek** tooreview hello Olay Görüntüleyicisi'nde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="47d90-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="47d90-260">(İsteğe bağlı) Tıklatın **gizlilik** tooreview Microsoft web hizmetleri gizlilik bildirimi.</span><span class="sxs-lookup"><span data-stu-id="47d90-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="47d90-261">Tooupload hakkında olan ile memnun kaldığınızda, tıklatın **günlükleri Gönder** tooactually hello sorunlarını gidermeye yönelik olarak son yedi gün tooMicrosoft gelen hello günlüklerini gönderme.</span><span class="sxs-lookup"><span data-stu-id="47d90-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="47d90-262">Hello ekran aşağıdaki gösterildiği gibi hello günlükleri gönderme işlemi hello durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="47d90-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Veri Yönetimi ağ geçidi gönderme durumu günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="47d90-264">Merhaba işlemi tamamlandıktan sonra hello ekran aşağıdaki gösterildiği gibi bir iletişim kutusu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="47d90-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Veri Yönetimi ağ geçidi gönderme durumu günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="47d90-266">Merhaba Kaydet **rapor kimliği** ve Microsoft Support paylaşın.</span><span class="sxs-lookup"><span data-stu-id="47d90-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="47d90-267">Hello rapor sorun giderme için karşıya kullanılan toolocate hello ağ geçidi günlüklerini kimliktir.</span><span class="sxs-lookup"><span data-stu-id="47d90-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="47d90-268">Merhaba rapor kimliği de hello Olay Görüntüleyicisi'nde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="47d90-269">Merhaba olay kimliği "25" bakarak bulun ve başlangıç tarihi ve saati denetleyin.</span><span class="sxs-lookup"><span data-stu-id="47d90-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Veri Yönetimi ağ geçidi Gönderme Raporu Kimliği günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="47d90-271">Ağ geçidi ana makinede arşiv gateway günlükleri</span><span class="sxs-lookup"><span data-stu-id="47d90-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="47d90-272">Burada ağ geçidi sorunları varsa ve ağ geçidi günlüklerini doğrudan paylaşamaz bazı senaryolar vardır:</span><span class="sxs-lookup"><span data-stu-id="47d90-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="47d90-273">El ile Merhaba ağ geçidi yükleyin ve hello ağ geçidini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="47d90-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="47d90-274">Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi yeniden anahtar ile tooregister hello ağ geçidi deneyin.</span><span class="sxs-lookup"><span data-stu-id="47d90-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="47d90-275">Toosend günlükleri deneyin ve hello ağ geçidi ana bilgisayar hizmeti bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="47d90-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="47d90-276">Bu senaryolarda, ağ geçidi günlüklerini bir zip dosyası olarak kaydetmek ve Microsoft desteğe başvurduğunuzda paylaşın.</span><span class="sxs-lookup"><span data-stu-id="47d90-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="47d90-277">Merhaba ağ geçidi olarak kaydettiğiniz sırada bir hata alırsanız, örneğin, ekran aşağıdaki hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="47d90-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Veri Yönetimi ağ geçidi kayıt hatası](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="47d90-279">Merhaba tıklatın **arşiv gateway günlükleri** tooarchive bağlamak ve günlükleri kaydedin ve sonra hello zip dosyası Microsoft desteği ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Veri Yönetimi ağ geçidi arşiv günlükleri](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="47d90-281">Ağ geçidi günlüklerini bulun</span><span class="sxs-lookup"><span data-stu-id="47d90-281">Locate gateway logs</span></span>
<span data-ttu-id="47d90-282">Merhaba Windows Olay günlüklerinde ayrıntılı ağ geçidi günlük bilgilerini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47d90-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="47d90-283">Windows Başlat **Olay Görüntüleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="47d90-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="47d90-284">Hello günlüklerini bulmak **uygulama ve hizmet günlükleri** > **veri yönetimi ağ geçidi** klasör.</span><span class="sxs-lookup"><span data-stu-id="47d90-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="47d90-285">Ağ geçidi ile ilgili sorunları gidermeye çalışıyorsanız, hata düzeyi olayları hello Olay Görüntüleyicisi'nde arayın.</span><span class="sxs-lookup"><span data-stu-id="47d90-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Veri Yönetimi ağ geçidi Olay Görüntüleyicisi'nde günlüğe kaydeder](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
