---
title: "aaaAzure RemoteApp sorun giderme - uygulama başlatma ve bağlantı hataları | Microsoft Docs"
description: "Başlangıç ve Azure remoteapp'te tooapplications bağlanma tootroubleshoot nasıl sorunlar hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="63e4d-103">Azure RemoteApp - sorun giderme uygulama başlatma ve bağlantı hataları</span><span class="sxs-lookup"><span data-stu-id="63e4d-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="63e4d-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="63e4d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="63e4d-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="63e4d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="63e4d-106">Azure Remoteapp'te barındırılan uygulamalar toolaunch birkaç farklı nedenlerle başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-106">Applications hosted in Azure RemoteApp can fail toolaunch for a few different reasons.</span></span> <span data-ttu-id="63e4d-107">Çeşitli nedenlerle bu makalede açıklanır ve kullanıcıların alıp hata iletileri toolaunch uygulamaları çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="63e4d-107">This article describes various reasons and error messages users might receive when trying toolaunch applications.</span></span> <span data-ttu-id="63e4d-108">Ayrıca, bağlantı hataları hakkında alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="63e4d-108">It also talks about connection failures.</span></span> <span data-ttu-id="63e4d-109">(Ancak bu makalede sorunları hello Azure RemoteApp istemcisini imzalarken açıklanmaz.)</span><span class="sxs-lookup"><span data-stu-id="63e4d-109">(But this article does not describe issues when signing into hello Azure RemoteApp client.)</span></span>  

<span data-ttu-id="63e4d-110">Tooapp başlatma ve bağlantı hataları nedeniyle genel hata iletileri hakkında bilgi için okumaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="63e4d-110">Read on for information about common error messages due tooapp launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="63e4d-111">Ki şu anda, ayarladığınız alınıyor... 10 dakika içinde yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="63e4d-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="63e4d-112">Bu hata, Azure RemoteApp, Itanium tabanlı sistemler için toomeet hello kapasite gereksinimi kullanıcılarınızın ölçeklendirme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-112">This error means Azure RemoteApp is scaling up toomeet hello capacity need of your users.</span></span> <span data-ttu-id="63e4d-113">Merhaba arka planda daha fazla Azure RemoteApp VM örnekleri kullanıcılarınızın toohandle hello kapasite gereksinimlerini oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="63e4d-113">In hello background more Azure RemoteApp VM instances are being created toohandle hello capacity needs of your users.</span></span> <span data-ttu-id="63e4d-114">Genellikle yaklaşık beş dakika sürer ancak too10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-114">Typically this takes around five minutes but can take up too10 minutes.</span></span> <span data-ttu-id="63e4d-115">Bazı durumlarda, bu yeterince hızlı gerçekleşmez ve kaynakları hemen gereklidir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="63e4d-116">Örneğin çok sayıda kullanıcı gereken yeri toouse uygulamanızı Azure RemoteAppn içinde hello 09: 00 senaryo aynı zamanda.</span><span class="sxs-lookup"><span data-stu-id="63e4d-116">For example a 9 AM scenario where many users need toouse your app in Azure RemoteAppn at hello same time.</span></span> <span data-ttu-id="63e4d-117">Bu tooyou olursa etkinleştirme **kapasite modu** hello üzerinde arka uç.</span><span class="sxs-lookup"><span data-stu-id="63e4d-117">If this happens tooyou we can enable **capacity mode** on hello back end.</span></span> <span data-ttu-id="63e4d-118">Bu açık bir Azure destek bileti toodo.</span><span class="sxs-lookup"><span data-stu-id="63e4d-118">toodo this open an Azure Support ticket.</span></span> <span data-ttu-id="63e4d-119">Belirli tooinclude hello isteğindeki abonelik Kimliğinizi olabilir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-119">Be certain tooinclude your subscription ID in hello request.</span></span>  

![Şu anda, ayarladığınız alınıyor](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a><span data-ttu-id="63e4d-121">Otomatik-tooyour yeniden bağlanılamadı uygulamalar, Lütfen uygulamanızı yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="63e4d-121">Could not auto-reconnect tooyour applications, please re-launch your application</span></span>
<span data-ttu-id="63e4d-122">Bu hata iletisini çok Azure RemoteApp kullanmakta olduğunuz ve ardından 4 saatten uzun, PC toosleep alın ve bilgisayarınıza uyandırdı hello Azure RemoteApp istemci girişimi tooauto yeniden bağlanın ve zaman aşımı oluştu görülür.</span><span class="sxs-lookup"><span data-stu-id="63e4d-122">This error message is often seen if you were using Azure RemoteApp and then put your PC toosleep longer than 4 hours and then woke your PC up and hello Azure RemoteApp client attempt tooauto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="63e4d-123">Kullanıcıların toonavigate geri toohello uygulama istemek ve tooopen denemek hello Azure RemoteApp istemci ondan.</span><span class="sxs-lookup"><span data-stu-id="63e4d-123">Instruct users toonavigate back toohello application and attempt tooopen it from hello Azure RemoteApp client.</span></span>

![Otomatik-tooyour uygulamaları yeniden bağlanılamadı](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a><span data-ttu-id="63e4d-125">Merhaba geçici profille sorunları</span><span class="sxs-lookup"><span data-stu-id="63e4d-125">Problems with hello temp profile</span></span>
<span data-ttu-id="63e4d-126">Kullanıcı profilinizin (kullanıcı profili diski) toomount başarısız oldu ve geçici bir profil hello kullanıcı alınan bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="63e4d-126">This error occurs when your user profile (User Profile Disk) failed toomount and hello user received a temporary profile.</span></span>  <span data-ttu-id="63e4d-127">Yöneticiler toohello koleksiyonunda hello Azure portalına gidin ve toohello Git **oturumları** sekmesinde ve çok Dene**Oturumu Kapat** hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="63e4d-127">Administrators should navigate toohello collection in hello Azure portal and then go toohello **Sessions** tab and attempt too**Log Off** hello user.</span></span> <span data-ttu-id="63e4d-128">Merhaba kullanıcı oturumunu - tam bir oturum zorla sonra hello kullanıcı girişimi toolaunch bir uygulamayı yeniden sahip.</span><span class="sxs-lookup"><span data-stu-id="63e4d-128">This will force a full log off of hello user session - then have hello user attempt toolaunch an app again.</span></span> <span data-ttu-id="63e4d-129">Azure desteğine başvurun başarısız olursa.</span><span class="sxs-lookup"><span data-stu-id="63e4d-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="63e4d-130">Azure RemoteApp çalışmayı durdurdu</span><span class="sxs-lookup"><span data-stu-id="63e4d-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="63e4d-131">Bu hata iletisini hello Azure RemoteApp istemcisi bir sorunu yaşıyor ve yeniden toobe gerekiyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="63e4d-131">This error message means hello Azure RemoteApp client is having an issue and needs toobe restarted.</span></span> <span data-ttu-id="63e4d-132">Kullanıcıların tooclose isteyin: seçin **Programı Kapat** ve hello Azure RemoteApp istemcisini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="63e4d-132">Instruct users tooclose: select **Close program** and then launch hello Azure RemoteApp client again.</span></span>  <span data-ttu-id="63e4d-133">Açık ve Azure destek bileti Hello sorun devam ederse.</span><span class="sxs-lookup"><span data-stu-id="63e4d-133">If hello issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp çalışmayı durdurdu](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a><span data-ttu-id="63e4d-135">Uzak Masaüstü bağlantısı bu kaynağa erişme bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="63e4d-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="63e4d-136">Merhaba bağlanmayı yeniden deneyin veya sistem yöneticinize başvurun</span><span class="sxs-lookup"><span data-stu-id="63e4d-136">Retry hello connection or contact your system administrator</span></span>
<span data-ttu-id="63e4d-137">Bu genel bir hata iletisi - biz araştırmak için Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="63e4d-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![Genel Azure RemoteApp iletisi](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

