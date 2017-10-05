---
title: "Windows kimlik doğrulaması ve Azure MFA Sunucusu | Microsoft Belgeleri"
description: "Bu, Windows Kimlik Doğrulaması ve Azure Multi-Factor Authentication Sunucusu’nu dağıtmada yardımcı olacak Azure Multi-factor authentication sayfasıdır."
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
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="3beca-103">Windows Kimlik Doğrulaması ve Azure Multi-Factor Authentication Sunucusu</span><span class="sxs-lookup"><span data-stu-id="3beca-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="3beca-104">Uygulamalara yönelik Windows kimlik doğrulamasını etkinleştirmek ve yapılandırmak için Azure Multi-Factor Authentication Sunucusunun Windows Kimlik Doğrulaması bölümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3beca-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="3beca-105">Windows Kimlik Doğrulamasını ayarlamadan önce aşağıdaki listeyi aklınızda bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3beca-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="3beca-106">Ayarladıktan sonra Terminal Hizmetlerinin etkili olması için Azure Multi-Factor Authentication’ı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="3beca-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="3beca-107">“Azure Multi-Factor Authentication kullanıcı eşleşmesi gerektir” seçeneği işaretliyse ve kullanıcı listesinden değilseniz, yeniden başlatma sonrası makinede oturum açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3beca-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="3beca-108">Güvenilen IP'ler uygulamanın ile kimlik doğrulaması ile istemci IP’si sağlayıp sağlayamayacağına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3beca-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="3beca-109">Şu anda yalnızca Terminal Hizmetleri desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3beca-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="3beca-110">Bu özellik, Windows Server 2012 R2’de Terminal Hizmetleri’ni güvenli hale getirmek için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="3beca-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="3beca-111">Bir uygulamayı Windows Kimlik Doğrulaması ile güvenli hale getirmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3beca-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="3beca-112">Azure Multi-Factor Authentication Sunucusu’nda Windows Kimlik Doğrulaması simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3beca-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="3beca-113">![Windows Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="3beca-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="3beca-114">**Windows Kimlik Doğrulamasını Etkinleştir** onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="3beca-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="3beca-115">Varsayılan olarak, bu kutu işaretlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="3beca-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="3beca-116">Uygulamalar sekmesi yöneticinin Windows Kimlik Doğrulaması için bir veya daha fazla uygulamayı yapılandırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3beca-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="3beca-117">Bir sunucu veya uygulama seçin – sunucusu/uygulama etkin olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3beca-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="3beca-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3beca-118">Click **OK**.</span></span>
5. <span data-ttu-id="3beca-119">**Ekle...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3beca-119">Click **Add…**</span></span>
6. <span data-ttu-id="3beca-120">Güvenilen IP'ler sekmesi belirli IP'lerden gelen Windows oturumları için Azure Multi-Factor Authentication’ı atlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3beca-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="3beca-121">Örneğin, çalışanlar ofiste ve evden uygulama kullanıyorsa, ofisteyken Azure Multi-Factor Authentication için telefonlarının çalmasını istemediğinize karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3beca-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="3beca-122">Bunun için ofis alt ağını Güvenilen IP’ler girişi olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3beca-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="3beca-123">**Ekle...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3beca-123">Click **Add…**</span></span>
8. <span data-ttu-id="3beca-124">Tek bir IP adresini atlamak istiyorsanız, **Tek IP**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3beca-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="3beca-125">Tüm IP aralığını atlamak istiyorsanız, **IP Aralığı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="3beca-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="3beca-126">Örnek: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="3beca-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="3beca-127">Bir alt ağ gösterimini kullanarak IP aralığı belirtmek istiyorsanız, **Alt Ağ**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3beca-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="3beca-128">Alt ağın başlangıç IP’sini girin ve açılır listede uygun ağ maskesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3beca-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="3beca-129">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3beca-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3beca-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3beca-130">Next steps</span></span>

- [<span data-ttu-id="3beca-131">Azure MFA Sunucusu için üçüncü taraf VPN cihazları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3beca-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="3beca-132">Azure MFA’ya yönelik NPS uzantısı ile mevcut kimlik doğrulama altyapınızı büyütün</span><span class="sxs-lookup"><span data-stu-id="3beca-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
