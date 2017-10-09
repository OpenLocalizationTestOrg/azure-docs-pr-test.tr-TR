---
title: "Uygulama Proxy Aracısı Bağlayıcısı hello aaaProblem yükleme | Microsoft Docs"
description: "Nasıl tootroubleshoot, yüklerken yüz uygulama Proxy Aracısı Bağlayıcısı hello sorunlar"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="b7ba7-103">Merhaba uygulama Proxy Aracısı Bağlayıcısı yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="b7ba7-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="b7ba7-104">Microsoft AAD Application Proxy Connector hello bulut kullanılabilir uç nokta toohello iç etki alanından giden bağlantılar tooestablish hello bağlantı kullanan bir iç etki alanının bileşendir.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="b7ba7-105">Genel sorun alanlarından bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="b7ba7-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="b7ba7-106">Bir bağlayıcının Hello yüklemesi başarısız olduğunda hello kök nedeni genellikle alanları aşağıdaki hello biridir:</span><span class="sxs-lookup"><span data-stu-id="b7ba7-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="b7ba7-107">**Bağlantı** – toocomplete başarılı bir yükleme yeni bağlayıcı gereksinimlerini tooregister hello ve gelecekteki güven özellikleri oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="b7ba7-108">Bu, toohello AAD uygulama proxy'si bulut hizmetine bağlanarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="b7ba7-109">**Güven oluşturma** – hello yeni bir bağlayıcı otomatik olarak imzalanan bir sertifika oluşturur ve toohello bulut hizmetine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="b7ba7-110">**Hello Yöneticisi kimlik doğrulaması** – yükleme sırasında hello kullanıcı yönetici kimlik bilgilerini toocomplete hello Bağlayıcısı yükleme sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="b7ba7-111">Bağlantı toohello bulut uygulama proxy'si hizmeti ve Microsoft Login sayfasına doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b7ba7-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="b7ba7-112">**Hedef:** bu hello bağlayıcı makine toohello AAD uygulama proxy'si kayıt uç noktasını ve bunun yanı sıra Microsoft oturum açma sayfasına bağlanabilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="b7ba7-113">Web sayfası aşağıdaki tarayıcı ve Git toohello açın: <https://aadap-portcheck.connectorporttest.msappproxy.net> , o hello bağlantı tooCentral ABD doğrulayın ve bağlantı noktaları 9090 ve 9091 Doğu ABD veri merkezlerinde çalıştığından.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="b7ba7-114">Bu bağlantı noktalarının hiçbirinde yoksa başarılı (yeşil bir onay yok), o hello güvenlik duvarı doğrulamak veya arka uç proxy sahip \*. msappproxy.net 9090 ve doğru şekilde tanımlanan 9091 bağlantı noktasına sahip.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="b7ba7-115">Bir tarayıcı (ayrı sekmesi) açın ve web sayfasını aşağıdaki toohello: <https://login.microsoftonline.com>, toothat sayfasında oturum açabileceğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="b7ba7-116">Makine ve arka uç bileşenleri için uygulama proxy'si güven sertifikası desteklediğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b7ba7-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="b7ba7-117">**Hedef:** hello bağlayıcı makine, arka uç proxy ve güvenlik duvarı gelecekteki güven hello Bağlayıcısı tarafından oluşturulan hello sertifika destekleyebilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="b7ba7-118">Merhaba bağlayıcı toocreate TLS1.2 tarafından desteklenen bir SHA512 cert çalışır.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="b7ba7-119">Merhaba makine veya hello arka uç güvenlik duvarı ve proxy desteklemiyor TLS1.2 hello yükleme başarısız.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="b7ba7-120">**tooresolve hello sorunu:**</span><span class="sxs-lookup"><span data-stu-id="b7ba7-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="b7ba7-121">Merhaba makine TLS1.2 destekleyen – 2012 R2 sonra tüm Windows sürümlerinde TLS 1.2 desteklemelidir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="b7ba7-122">Bağlayıcı makinenizi 2012 R2 sürümü ya da önceki ise, aşağıdaki KB hello makinede yüklü o hello emin olun: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="b7ba7-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="b7ba7-123">Ağ yöneticinize başvurun ve hello arka uç proxy ve güvenlik duvarı SHA512 giden trafiği için engellemez tooverify isteyin.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="b7ba7-124">Kullanılan tooinstall hello Bağlayıcısı yönetici olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b7ba7-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="b7ba7-125">**Hedef:** tooinstall hello bağlayıcı çalıştığında bu hello kullanıcı doğru kimlik bilgilerine sahip bir yönetici olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="b7ba7-126">Şu anda hello kullanıcının hello yükleme toosucceed için genel yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="b7ba7-127">**tooverify hello kimlik bilgilerinin doğru olduğundan:**</span><span class="sxs-lookup"><span data-stu-id="b7ba7-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="b7ba7-128">Çok bağlanmak<https://login.microsoftonline.com> ve aynı kimlik bilgilerini hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="b7ba7-129">Merhaba oturum açma başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-129">Make sure hello login is successful.</span></span> <span data-ttu-id="b7ba7-130">Çok giderek hello kullanıcı rolü denetleyebilirsiniz**Azure Active Directory**  - &gt; **kullanıcılar ve gruplar**  - &gt; **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="b7ba7-131">Kullanıcı hesabınız, ardından "dizin rolü" Merhaba ortaya çıkan menüde seçin.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="b7ba7-132">Bu hello seçili rol "Genel yönetici" olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="b7ba7-133">Merhaba hiçbirini sayfaları adımları oluşturulamıyor tooaccess varsa, genel bir yönetici değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ba7-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ba7-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7ba7-134">Next steps</span></span>
[<span data-ttu-id="b7ba7-135">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="b7ba7-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
