---
title: "Canlı akış için aaaTroubleshooting Kılavuzu | Microsoft Docs"
description: "Bu konuda nasıl tootroubleshoot canlı akış sorunları hakkında öneriler sağlar."
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
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="bc0dd-103">Canlı akış sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="bc0dd-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="bc0dd-104">Bu konu hakkında öneriler sunar tootroubleshoot bazı canlı akış sorunları.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="bc0dd-105">Tooon içi kodlayıcılar ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc0dd-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="bc0dd-106">Bu bölüm, gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar olan tootroubleshoot sorunları ilgili tooon içi kodlayıcılar toosend nasıl yapılandırılacağı hakkında öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="bc0dd-107">Sorun: toosee günlükleri istiyorsunuz</span><span class="sxs-lookup"><span data-stu-id="bc0dd-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="bc0dd-108">**Olası sorun**: Kodlayıcı günlüklerini bulma sorunları hata ayıklamaya yardımcı olabilecek olamaz.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="bc0dd-109">**Telestream Wirecast**: logs C:\Users altında genellikle bulabilirsiniz\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="bc0dd-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="bc0dd-110">**Elemental canlı**: sahip bağlantılar toologs hello yönetim portalında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="bc0dd-111">Tıklayın **istatistiği**, ardından **günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="bc0dd-112">Merhaba üzerinde **günlük dosyalarını** sayfası, tüm günlükleri listesi LiveEvent öğeleri hello; seçin, mevcut oturumunuzun eşleşen hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="bc0dd-113">**Canlı medya Kodlayıcı flash**: hello bulabilirsiniz **günlük dizini...**  toohello gezinme tarafından **kodlama günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="bc0dd-114">Sorun: Aşamalı bir akış çıktısı için bir seçenek yoktur</span><span class="sxs-lookup"><span data-stu-id="bc0dd-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="bc0dd-115">**Olası sorun**: kullanılan hello Kodlayıcı değil otomatik olarak Titreşimi Kaldırma.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="bc0dd-116">**Sorun giderme adımları**: hello Kodlayıcı arabiriminden Titreşim seçeneği arayın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="bc0dd-117">XML'deki tarama etkinleştirildikten sonra yeniden aşamalı çıkış ayarlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="bc0dd-118">Sorun: birkaç encoder çıkış ayarları ve hala tooconnect çalıştı.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="bc0dd-119">**Olası sorun**: Azure kodlama kanal değil düzgün sıfırlandı.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="bc0dd-120">**Sorun giderme adımları**: tooAMS yapma emin hello Kodlayıcı Ftp'den artık, durdurmak ve hello kanalını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="bc0dd-121">Yeniden çalıştırmayı sonra kodlayıcıyı hello yeni ayarlarla bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="bc0dd-122">Merhaba sorunu bu hala gidermezse, tamamen yeni bir kanal oluşturma deneyin, başarısız birkaç denemeden sonra bazen kanalları bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="bc0dd-123">**Olası sorun**: Merhaba GOP boyutu veya anahtar çerçeve ayarları en uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="bc0dd-124">**Sorun giderme adımları**: önerilen GOP boyutu veya ana kare aralığıdır 2 saniye.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="bc0dd-125">Başkalarının saniye kullanırken bazı kodlayıcılar çerçeve sayısı bu ayarda hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="bc0dd-126">Örneğin: 30 fps alırken hello GOP boyutu 60 çerçeve eşdeğer too2 saniye olduğu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="bc0dd-127">**Olası sorun**: kapalı bağlantı noktalarını hello akış engelleme.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="bc0dd-128">**Sorun giderme adımları**: RTMP akış, güvenlik duvarı ve/veya proxy ayarlarını tooconfirm 1935 ve 1936 giden bağlantı noktalarının açık olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="bc0dd-129">RTP akış kullanırken, giden bağlantı noktası 2010 açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="bc0dd-130">Sorun: RTP Protokolü hello ile Merhaba Kodlayıcı toostream yapılandırma olduğunda yer yok tooenter bir ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="bc0dd-131">**Olası sorun**: birçok RTP kodlayıcılar ana bilgisayar adları için izin vermez ve bir IP adresi toobe alınan ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="bc0dd-132">**Sorun giderme adımları**: toofind Merhaba IP adresinin, herhangi bir bilgisayarda bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="bc0dd-133">Windows, toodo açık çalışma Başlatıcısı (WIN + R) hello ve "cmd" tooopen yazın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="bc0dd-134">Merhaba komut istemi açıldıktan sonra "Ping [AMS ana bilgisayar adı]" yazın.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="bc0dd-135">Merhaba ana bilgisayar adı aşağıdaki örneğine hello vurgulu olarak hello Azure alım URL'sini, başlangıç bağlantı noktası numarasından kaldırarak türetilmiş olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="bc0dd-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="bc0dd-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="bc0dd-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="bc0dd-138">Aşağıdaki ise, hala başarıyla akış uygulayamazsınız hello sorun giderme adımları sonra hello Azure portal kullanarak bir destek bileti gönderin.</span><span class="sxs-lookup"><span data-stu-id="bc0dd-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="bc0dd-139">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="bc0dd-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bc0dd-140">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="bc0dd-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

