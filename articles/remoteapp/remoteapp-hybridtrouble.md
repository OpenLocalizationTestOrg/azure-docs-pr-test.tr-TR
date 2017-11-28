---
title: "RemoteApp karma koleksiyonu oluşturma sorunlarını giderme | Microsoft Docs"
description: "RemoteApp karma koleksiyonu oluşturma hatalarını giderme öğrenin"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="24bcc-103">Azure RemoteApp karma koleksiyonları oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="24bcc-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="24bcc-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="24bcc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="24bcc-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="24bcc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="24bcc-106">Karma koleksiyon, içinde barındırılan ve Azure bulut ancak de olanak tanır kullanıcıların access veri ve yerel ağınızda depolanan kaynakları verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="24bcc-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="24bcc-107">Kullanıcılar, Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="24bcc-108">Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24bcc-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="24bcc-109">Oluşturma veya bir sanal ağ alt beklenen gelişmeye Azure RemoteApp için bir CIDR aralığı büyüklükte kullanılmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="24bcc-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="24bcc-110">Koleksiyonunuz henüz oluşturmadınız?</span><span class="sxs-lookup"><span data-stu-id="24bcc-110">Haven't created your collection yet?</span></span> <span data-ttu-id="24bcc-111">Bkz: [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) adımlar için.</span><span class="sxs-lookup"><span data-stu-id="24bcc-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="24bcc-112">Koleksiyonunuzu oluşturma sorunu yaşıyor veya koleksiyon biçimini çalışmıyorsa gerektiği düşünün, aşağıdaki bilgileri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="24bcc-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="24bcc-113">Görüntünüzü geçersiz</span><span class="sxs-lookup"><span data-stu-id="24bcc-113">Your image is invalid</span></span>
<span data-ttu-id="24bcc-114">Koleksiyonunuz sağlamak Azure için beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="24bcc-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="24bcc-115">Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve koleksiyonunuzu yeniden oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="24bcc-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="24bcc-116">Sanal ağınızı tanımlanan ağ güvenlik grupları var mı?</span><span class="sxs-lookup"><span data-stu-id="24bcc-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="24bcc-117">Koleksiyonunuz için kullandığınız alt ağdaki tanımlanan ağ güvenlik grupları varsa, bunlar emin olun [URL'lerin ve bağlantı noktalarının](remoteapp-ports.md) , alt ağ içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="24bcc-118">Sizin tarafınızdan daha sıkı bir denetim için alt ağda dağıtılan VM'ler için ek ağ güvenlik gruplarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="24bcc-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="24bcc-119">Kendi DNS sunucularınızı kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="24bcc-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="24bcc-120">Ve sanal alt ağdan erişilebilir?</span><span class="sxs-lookup"><span data-stu-id="24bcc-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="24bcc-121">VNET içinde barındırılan sanal makineleri çözümlemek her zaman kullanabilirsiniz ve sanal ağınızın DNS sunucularının her zaman çalıştığından emin olmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="24bcc-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="24bcc-122">Google DNS bu için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24bcc-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="24bcc-123">Karma koleksiyonlar için kendi DNS sunucularınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="24bcc-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="24bcc-124">Sanal ağınızı oluştururken bunları ağ yapılandırma Şeması veya Yönetim Portalı aracılığıyla belirtin.</span><span class="sxs-lookup"><span data-stu-id="24bcc-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="24bcc-125">DNS sunucuları (aksine, hepsini bir kez) bir yük devretme şekilde belirtildikleri sırada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24bcc-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="24bcc-126">Lütfen [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) DNS sunucunuzun emin olmak için yapılandırılmış correcly sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="24bcc-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="24bcc-127">DNS sunucuları koleksiyonunuz için erişilebilir olduğundan ve bu koleksiyon için belirtilen sanal alt ağdan kullanılabilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="24bcc-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="24bcc-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="24bcc-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![DNS sunucunuzun tanımlayın](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="24bcc-130">Bir Active Directory etki alanı denetleyicisi koleksiyonunuzda kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="24bcc-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="24bcc-131">Yalnızca şu anda bir Active Directory etki alanı Azure RemoteApp ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="24bcc-132">Karma koleksiyon DirSync aracıyla bir Windows Server Active Directory dağıtımdan eşitlenmiş Azure Active Directory hesaplarını destekler; Özellikle, parola eşitleme seçeneği ile eşitlenen ya da yapılandırılan Active Directory Federasyon Hizmetleri (AD FS) Federasyonuyla eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="24bcc-133">Şirket içi etki alanınız için UPN etki alanı sonekiyle özel bir etki alanı oluşturabilir ve dizin tümleştirmesini ayarladıktan gerekir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="24bcc-134">Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="24bcc-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="24bcc-135">Sağlanan etki alanı ayrıntıları geçerli olduğunu ve Azure RemoteApp için kullanılan alt ağda oluşturulan VM etki alanı denetleyicisi erişilebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="24bcc-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="24bcc-136">Ayrıca sağlanan hizmet hesabı kimlik bilgileri sağlanan etki alanına bilgisayar eklemek için izinlere sahip ve girilen AD adı sanal ağ içinde sağlanan DNS'den çözümlenebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="24bcc-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="24bcc-137">Koleksiyonunuz oluşturduğunuzda hangi etki alanı adı belirttiğiniz?</span><span class="sxs-lookup"><span data-stu-id="24bcc-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="24bcc-138">Oluşturulan ya da eklenen etki alanı adını bir iç etki alanı adı (, Azure AD etki alanı adı değil) olması ve çözümlenebilir DNS biçiminde (contoso.local) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24bcc-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="24bcc-139">Örneğin, bir Active Directory iç adı (contoso.local) ve Active Directory UPN (contoso.com) sahip - koleksiyonunuzu oluşturduğunuzda, iç adı kullanmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="24bcc-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

