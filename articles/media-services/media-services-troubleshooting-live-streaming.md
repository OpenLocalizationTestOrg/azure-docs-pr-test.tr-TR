---
title: "Canlı akış için sorun giderme kılavuzu | Microsoft Docs"
description: "Bu konuda canlı akış sorunlarını giderme hakkında öneriler sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="4000e-103">Canlı akış sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="4000e-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="4000e-104">Bu konuda bazı canlı akış sorunlarını giderme hakkında öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4000e-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="4000e-105">Şirket içi kodlayıcılardan ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="4000e-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="4000e-106">Bu bölüm, gerçek zamanlı kodlama için etkinleştirilmiş AMS kanallar tek bit hızlı akış göndermek için yapılandırılmış olan şirket içi kodlayıcılardan ilgili sorunları giderme konusunda öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4000e-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="4000e-107">Sorun: günlükleri görmek istediğiniz</span><span class="sxs-lookup"><span data-stu-id="4000e-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="4000e-108">**Olası sorun**: Kodlayıcı günlüklerini bulma sorunları hata ayıklamaya yardımcı olabilecek olamaz.</span><span class="sxs-lookup"><span data-stu-id="4000e-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="4000e-109">**Telestream Wirecast**: logs C:\Users altında genellikle bulabilirsiniz\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="4000e-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="4000e-110">**Elemental canlı**: sahip bağlantılar günlükleri için yönetim portalında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4000e-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="4000e-111">Tıklayın **istatistiği**, ardından **günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="4000e-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="4000e-112">Üzerinde **günlük dosyalarını** sayfasında, günlükleri tüm LiveEvent öğelerin bir listesini görürsünüz; geçerli oturumunuz eşleşen birini seçin.</span><span class="sxs-lookup"><span data-stu-id="4000e-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="4000e-113">**Canlı medya Kodlayıcı flash**: bulabileceğiniz **günlük dizini...**  giderek **kodlama günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4000e-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="4000e-114">Sorun: Aşamalı bir akış çıktısı için bir seçenek yoktur</span><span class="sxs-lookup"><span data-stu-id="4000e-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="4000e-115">**Olası sorun**: kullanılan kodlayıcı otomatik olarak titreşimsiz görüntü değil.</span><span class="sxs-lookup"><span data-stu-id="4000e-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="4000e-116">**Sorun giderme adımları**: Titreşim seçeneği Kodlayıcı arabiriminden arayın.</span><span class="sxs-lookup"><span data-stu-id="4000e-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="4000e-117">XML'deki tarama etkinleştirildikten sonra yeniden aşamalı çıkış ayarlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4000e-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="4000e-118">Sorun: birkaç encoder çıkış ayarları denedi ve hala bağlanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="4000e-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="4000e-119">**Olası sorun**: Azure kodlama kanal değil düzgün sıfırlandı.</span><span class="sxs-lookup"><span data-stu-id="4000e-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="4000e-120">**Sorun giderme adımları**: emin olun Kodlayıcı artık gönderilmesi için AMS, durdurmak ve kanal sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="4000e-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="4000e-121">Yeniden çalıştırmayı sonra yeni ayarlarla kodlayıcıyı bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="4000e-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="4000e-122">Sorun bu hala gidermezse, tamamen yeni bir kanal oluşturma deneyin, başarısız birkaç denemeden sonra bazen kanalları bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="4000e-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="4000e-123">**Olası sorun**: GOP boyutu veya anahtar çerçeve ayarları en uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="4000e-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="4000e-124">**Sorun giderme adımları**: önerilen GOP boyutu veya ana kare aralığıdır 2 saniye.</span><span class="sxs-lookup"><span data-stu-id="4000e-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="4000e-125">Başkalarının saniye kullanırken bazı kodlayıcılar çerçeve sayısı bu ayarda hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="4000e-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="4000e-126">Örneğin: 30 fps alırken GOP boyutu 60 çerçeve 2 saniyeye eşdeğerdir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4000e-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="4000e-127">**Olası sorun**: kapalı bağlantı noktalarını akış engelleme.</span><span class="sxs-lookup"><span data-stu-id="4000e-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="4000e-128">**Sorun giderme adımları**: RTMP akış, 1935 ve 1936 giden bağlantı noktalarının açık olduğunu onaylamak için güvenlik duvarı ve/veya proxy ayarlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4000e-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="4000e-129">RTP akış kullanırken, giden bağlantı noktası 2010 açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4000e-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="4000e-130">Sorun: RTP protokolüyle akış kodlayıcıya yapılandırma olduğunda hiçbir girilebileceği bir ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="4000e-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="4000e-131">**Olası sorun**: birçok RTP kodlayıcılar ana bilgisayar adları için izin vermez ve bir IP adresi elde edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4000e-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="4000e-132">**Sorun giderme adımları**: IP adresini bulmak için herhangi bir bilgisayarda bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="4000e-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="4000e-133">Bu Windows yapmak için çalışma Başlatıcısı (WIN + R) açın ve "cmd" yazın açın.</span><span class="sxs-lookup"><span data-stu-id="4000e-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="4000e-134">Komut istemi açıldıktan sonra "Ping [AMS ana bilgisayar adı]" yazın.</span><span class="sxs-lookup"><span data-stu-id="4000e-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="4000e-135">Ana bilgisayar adı, aşağıdaki örnekte vurgulanmış olarak Azure alım URL'sini bağlantı noktası numarasından kaldırarak türetilmiş olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="4000e-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="4000e-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="4000e-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="4000e-138">Aşağıdaki ise, hala başarıyla akış uygulayamazsınız sorun giderme adımları sonra Azure portalını kullanarak bir destek bileti gönderin.</span><span class="sxs-lookup"><span data-stu-id="4000e-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="4000e-139">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="4000e-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4000e-140">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="4000e-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

