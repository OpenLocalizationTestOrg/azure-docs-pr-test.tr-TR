---
title: "RemoteApp karma koleksiyonu oluşturma aaaTroubleshoot | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot RemoteApp karma koleksiyonu oluşturma hataları"
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="7a278-103">Azure RemoteApp karma koleksiyonları oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="7a278-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7a278-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7a278-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7a278-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="7a278-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7a278-106">Karma koleksiyon, içinde barındırılan ve hello Azure bulut ancak de olanak tanır kullanıcıların access veri ve yerel ağınızda depolanan kaynakları verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="7a278-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="7a278-107">Kullanıcılar, Azure Active Directory ile eşitlenen ya da federasyonla yönetilen kurumsal kimlik bilgilerini kullanarak uygulamalara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="7a278-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="7a278-108">Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a278-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="7a278-109">Oluşturma veya bir sanal ağ alt beklenen gelişmeye Azure RemoteApp için bir CIDR aralığı büyüklükte kullanılmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="7a278-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="7a278-110">Koleksiyonunuz henüz oluşturmadınız?</span><span class="sxs-lookup"><span data-stu-id="7a278-110">Haven't created your collection yet?</span></span> <span data-ttu-id="7a278-111">Bkz: [karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md) hello adımlar için.</span><span class="sxs-lookup"><span data-stu-id="7a278-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="7a278-112">Koleksiyonunuzu oluşturma sorunu yaşıyor veya hello koleksiyonu çalışmıyorsa düşündüğünüz hello şekilde gerektiğini bilgisinden hello kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7a278-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="7a278-113">Görüntünüzü geçersiz</span><span class="sxs-lookup"><span data-stu-id="7a278-113">Your image is invalid</span></span>
<span data-ttu-id="7a278-114">Koleksiyonunuz için Azure tooprovision beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü hello karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="7a278-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="7a278-115">Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve toocreate koleksiyonunuzu yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7a278-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="7a278-116">Sanal ağınızı tanımlanan ağ güvenlik grupları var mı?</span><span class="sxs-lookup"><span data-stu-id="7a278-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="7a278-117">Koleksiyonunuz için kullandığınız hello alt ağdaki tanımlanan ağ güvenlik grupları varsa, bunlar emin olun [URL'lerin ve bağlantı noktalarının](remoteapp-ports.md) , alt ağ içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="7a278-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="7a278-118">Ek ağ güvenlik grupları toohello Vm'lerinde dağıtılan sizin tarafınızdan daha sıkı bir denetim için hello alt ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a278-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="7a278-119">Kendi DNS sunucularınızı kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="7a278-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="7a278-120">Ve sanal alt ağdan erişilebilir?</span><span class="sxs-lookup"><span data-stu-id="7a278-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="7a278-121">Sanal ağınızın DNS sunucularının her zaman çalışır durumda toomake emin hello ve hello VNET barındırılan her zaman mümkün tooresolve hello sanal makineler var.</span><span class="sxs-lookup"><span data-stu-id="7a278-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="7a278-122">Google DNS bu için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7a278-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="7a278-123">Karma koleksiyonlar için kendi DNS sunucularınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a278-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="7a278-124">Sanal ağınızı oluştururken bunları ağ yapılandırma Şeması veya hello Yönetim Portalı aracılığıyla belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a278-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="7a278-125">DNS sunucuları, bir yük devretme şekilde (karşılıklı tooround deneme) belirtildikleri hello sırada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7a278-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="7a278-126">Lütfen çok başvurun[VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake, DNS sunucularınızın yapılandırılmış correcly emin.</span><span class="sxs-lookup"><span data-stu-id="7a278-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="7a278-127">Koleksiyonunuz için Hello DNS sunucuları bu koleksiyon için belirtilen hello sanal ağ alt ağı üzerinden erişilebilir ve kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a278-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="7a278-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7a278-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![DNS sunucunuzun tanımlayın](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="7a278-130">Bir Active Directory etki alanı denetleyicisi koleksiyonunuzda kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="7a278-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="7a278-131">Yalnızca şu anda bir Active Directory etki alanı Azure RemoteApp ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a278-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="7a278-132">Merhaba karma koleksiyon DirSync aracıyla bir Windows Server Active Directory dağıtımdan eşitlenmiş Azure Active Directory hesaplarını destekler; Özellikle, hello parola eşitleme seçeneği ile eşitlenen ya da yapılandırılan Active Directory Federasyon Hizmetleri (AD FS) Federasyonuyla eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="7a278-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="7a278-133">Dizin tümleştirmesini ayarladıktan ve toocreate hello UPN etki alanı sonekiyle'şirket içi etki alanınız için özel bir etki alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a278-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="7a278-134">Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7a278-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="7a278-135">Sağlanan hello etki alanı ayrıntıları geçerli olduğundan ve VM Azure uzak uygulaması için kullanılan hello alt ağda oluşturulan hello hello etki alanı denetleyicisi erişilebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a278-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="7a278-136">Ayrıca hello hizmet hesabı etki alanı ve, sağlanan AD adı hello sağlanan kimlik bilgileri sağlandı izinleri tooadd bilgisayarlar toohello sahip hello hello VNET sağlanan DNS gelen çözümlenebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a278-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="7a278-137">Koleksiyonunuz oluşturduğunuzda hangi etki alanı adı belirttiğiniz?</span><span class="sxs-lookup"><span data-stu-id="7a278-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="7a278-138">oluşturulan ya da eklenen hello etki alanı adı bir iç etki alanı adı (, Azure AD etki alanı adı değil) olması ve çözümlenebilir DNS biçiminde (contoso.local) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a278-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="7a278-139">Örneğin, bir Active Directory iç adı (contoso.local) varsa ve Active Directory UPN (contoso.com) - koleksiyonunuzu oluşturduğunuzda toouse hello iç adına sahip.</span><span class="sxs-lookup"><span data-stu-id="7a278-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

