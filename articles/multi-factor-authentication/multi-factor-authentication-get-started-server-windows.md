---
title: "aaaWindows kimlik doğrulaması ve Azure MFA sunucusu | Microsoft Docs"
description: "Bu, Windows kimlik doğrulaması ve Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="41713-103">Windows Kimlik Doğrulaması ve Azure Multi-Factor Authentication Sunucusu</span><span class="sxs-lookup"><span data-stu-id="41713-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="41713-104">Merhaba Windows kimlik doğrulaması hello Azure çok faktörlü kimlik doğrulama sunucusu tooenable bölümünü kullanın ve uygulamaları için Windows kimlik doğrulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41713-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="41713-105">Windows kimlik doğrulamasını ayarlamadan önce göz önünde listesinde aşağıdaki hello tutun:</span><span class="sxs-lookup"><span data-stu-id="41713-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="41713-106">Kurulum sonrasında, Terminal Hizmetleri tootake etkisi için Azure multi-Factor Authentication hello yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="41713-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="41713-107">' Azure multi-Factor Authentication kullanıcılarının eşleşmesini gerektir' seçeneği işaretliyse ve hello kullanıcı listesinde olmayan, yeniden başlatmanın ardından hello makine içine mümkün toolog olmaz.</span><span class="sxs-lookup"><span data-stu-id="41713-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="41713-108">IP'leri hello uygulama hello istemci IP hello kimlik doğrulamasına sahip olup olmadığını sağlayabilir bağlı olduğu güvenilen.</span><span class="sxs-lookup"><span data-stu-id="41713-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="41713-109">Şu anda yalnızca Terminal Hizmetleri desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="41713-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="41713-110">Bu özellik Windows Server 2012 R2'de desteklenen toosecure Terminal Hizmetleri'ni değil.</span><span class="sxs-lookup"><span data-stu-id="41713-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="41713-111">Windows kimlik doğrulaması, aşağıdaki yordamı kullanın hello uygulamayla toosecure.</span><span class="sxs-lookup"><span data-stu-id="41713-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="41713-112">Hello Azure çok faktörlü kimlik doğrulama sunucusu hello Windows kimlik doğrulaması simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41713-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="41713-113">![Windows Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="41713-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="41713-114">Merhaba denetleyin **Windows kimlik doğrulamasını etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="41713-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="41713-115">Varsayılan olarak, bu kutu işaretlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="41713-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="41713-116">Merhaba uygulamalar sekmesini hello yönetici tooconfigure bir veya daha fazla uygulamayı Windows kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="41713-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="41713-117">Bir sunucu veya uygulama seçin – hello sunucusunun/uygulamanın etkinleştirilip etkinleştirilmeyeceğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="41713-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="41713-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41713-118">Click **OK**.</span></span>
5. <span data-ttu-id="41713-119">**Ekle...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41713-119">Click **Add…**</span></span>
6. <span data-ttu-id="41713-120">Merhaba güvenilen IP'ler sekmesi belirli ıp'lerden gelen tooskip Azure çok faktörlü kimlik doğrulaması Windows oturumları için sağlar.</span><span class="sxs-lookup"><span data-stu-id="41713-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="41713-121">Örneğin, çalışanlar hello ofisten ve evden hello uygulama kullanıyorsa, hello ofisteki Azure multi-Factor Authentication için telefonlarının çalmasını istemediğiniz karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41713-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="41713-122">Bunun için güvenilen IP'ler girişi olarak hello ofis alt belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41713-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="41713-123">**Ekle...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41713-123">Click **Add…**</span></span>
8. <span data-ttu-id="41713-124">Seçin **tek bir IP** tooskip tek bir IP adresi istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="41713-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="41713-125">Seçin **IP aralığı** tooskip tüm IP aralığını istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="41713-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="41713-126">Örnek: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="41713-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="41713-127">Seçin **alt** bir alt ağ gösterimini kullanarak IP aralığı toospecify istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="41713-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="41713-128">Merhaba alt ağın başlangıç IP'sini girin ve hello hello aşağı açılan listeden uygun ağ maskesini seçin.</span><span class="sxs-lookup"><span data-stu-id="41713-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="41713-129">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41713-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41713-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41713-130">Next steps</span></span>

- [<span data-ttu-id="41713-131">Azure MFA Sunucusu için üçüncü taraf VPN cihazları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41713-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="41713-132">Varolan kimlik altyapınızı hello NPS uzantısı ile Azure MFA için büyütmek</span><span class="sxs-lookup"><span data-stu-id="41713-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
