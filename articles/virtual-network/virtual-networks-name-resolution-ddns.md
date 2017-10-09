---
title: "aaaUsing dinamik DNS tooregister ana bilgisayar adları"
description: "Bu sayfa hakkında ayrıntılar verir tooset kendi DNS sunucularınızı dinamik DNS tooregister konak adları ayarlama."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="1864a-103">Dinamik DNS tooregister ana bilgisayar adları kendi DNS sunucusu kullanma</span><span class="sxs-lookup"><span data-stu-id="1864a-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="1864a-104">[Azure ad çözümlemesi sağlar](virtual-networks-name-resolution-for-vms-and-role-instances.md) sanal makineleri (VM'ler) ve rol örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="1864a-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="1864a-105">Ancak, ad çözümlemesi Azure tarafından sağlanan ötesinde olduğunuzda, kendi DNS sunucularınızı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1864a-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="1864a-106">DNS çözüm toosuit güç tootailor hello kazandırır belirli gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="1864a-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="1864a-107">Örneğin, Active Directory etki alanı denetleyicinizi tooaccess şirket içi kaynakları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1864a-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="1864a-108">Azure VM'ler, iletebileceği özel DNS sunucularınızın barındırıldığında hostname Merhaba aynı sorgular vnet tooAzure tooresolve ana bilgisayar adları.</span><span class="sxs-lookup"><span data-stu-id="1864a-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="1864a-109">Bu yol toouse istemiyorsanız, VM ana bilgisayar adları DNS sunucunuzun dinamik DNS kullanarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1864a-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="1864a-110">Azure alternatif düzenlemeleri genellikle gerektiği şekilde kayıtları, DNS sunucularınızın oluşturmak hello özelliği (örneğin, kimlik bilgileri) toodirectly sahip değil.</span><span class="sxs-lookup"><span data-stu-id="1864a-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="1864a-111">Burada, Alternatiflerle birlikte ortak bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="1864a-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="1864a-112">Windows istemcileri</span><span class="sxs-lookup"><span data-stu-id="1864a-112">Windows clients</span></span>
<span data-ttu-id="1864a-113">Olmayan etki alanına katılmış Windows istemcileri güvenli olmayan dinamik DNS (DDNS) güncelleştirmeleri bunlar önyüklediğinizde veya IP adreslerini değiştiğinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="1864a-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="1864a-114">Merhaba DNS hello hostname artı hello birincil DNS soneki adıdır.</span><span class="sxs-lookup"><span data-stu-id="1864a-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="1864a-115">Azure hello birincil DNS soneki boş bırakır, ancak hello VM hello aracılığıyla bu ayarlayabilirsiniz [UI](https://technet.microsoft.com/library/cc794784.aspx) veya [Otomasyon kullanarak](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="1864a-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="1864a-116">Etki alanına katılmış Windows istemcileri güvenli dinamik DNS kullanarak IP adreslerini hello etki alanı denetleyicisi ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1864a-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="1864a-117">Merhaba etki alanına katılma işlemi hello istemcide hello birincil DNS soneki ayarlar ve oluşturur ve hello güven ilişkisini korur.</span><span class="sxs-lookup"><span data-stu-id="1864a-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="1864a-118">Linux istemcileri</span><span class="sxs-lookup"><span data-stu-id="1864a-118">Linux clients</span></span>
<span data-ttu-id="1864a-119">Linux istemcileri genellikle başlangıçta hello DNS sunucusuyla kendilerini yok, hello DHCP sunucusu mevcut varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1864a-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="1864a-120">Azure'nın DHCP sunucuları, DNS sunucusu veya kimlik bilgilerini tooregister kayıtları hello yeteneği yok.</span><span class="sxs-lookup"><span data-stu-id="1864a-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="1864a-121">Adlı bir aracı kullanabilirsiniz *nsupdate*hello bağlama paketine dahil, dinamik DNS toosend güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1864a-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="1864a-122">Merhaba dinamik DNS protokolü standartlaştırılmış için kullanabileceğiniz *nsupdate* bile zaman bağlama hello DNS sunucusunda kullanmakta olduğunuz değil.</span><span class="sxs-lookup"><span data-stu-id="1864a-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="1864a-123">Merhaba hostname hello DNS sunucusu girişi korumak ve hello DHCP istemci toocreate tarafından sağlanan hello kancaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1864a-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="1864a-124">Merhaba DHCP döngüsü sırasında hello istemci hello komut dosyalarında yürütür */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="1864a-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="1864a-125">Bu, tooregister hello yeni IP adresini kullanarak kullanılan *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="1864a-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="1864a-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1864a-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="1864a-127">Merhaba de kullanabilirsiniz *nsupdate* komutu tooperform güvenli dinamik DNS güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1864a-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="1864a-128">Örneğin, bir BIND DNS sunucusu kullanırken, bir genel-özel anahtar çifti [oluşturulan](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="1864a-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="1864a-129">Merhaba DNS sunucusu [yapılandırılmış](http://linux.yyz.us/dns/ddns-server.html) hello ortak anahtarının bir parçası olan hello isteği hello imza doğrulayabilmeniz için hello ile.</span><span class="sxs-lookup"><span data-stu-id="1864a-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="1864a-130">Merhaba kullanmalısınız *-k* seçeneği tooprovide hello anahtar çifti çok*nsupdate* hello için dinamik DNS güncelleştirme imzalı istek toobe sırayla.</span><span class="sxs-lookup"><span data-stu-id="1864a-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="1864a-131">Bir Windows DNS sunucusu kullanırken, Kerberos kimlik doğrulaması ile Merhaba kullanabilirsiniz *-g* parametresinde *nsupdate* (Merhaba Windows sürümünde kullanılabilir *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="1864a-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="1864a-132">toodo Bu, kullanım *kinit* tooload hello kimlik bilgilerini (örneğin bir [keytab dosya](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="1864a-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="1864a-133">Ardından *nsupdate -g* hello önbelleğinden hello kimlik bilgileri çeker.</span><span class="sxs-lookup"><span data-stu-id="1864a-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="1864a-134">Gerekli olursa, DNS Arama soneki tooyour VM'ler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1864a-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="1864a-135">Merhaba DNS soneki hello belirtilen */etc/resolv.conf* dosya.</span><span class="sxs-lookup"><span data-stu-id="1864a-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="1864a-136">Çoğu Linux distro'lar hello içeriği otomatik olarak yönetir bu dosya, bu nedenle genellikle düzenleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1864a-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="1864a-137">Ancak, hello DHCP istemcisinin kullanarak hello soneki geçersiz kılabilirsiniz *yerine geçen* komutu.</span><span class="sxs-lookup"><span data-stu-id="1864a-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="1864a-138">toodo Bu, */etc/dhcp/dhclient.conf*, ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1864a-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

