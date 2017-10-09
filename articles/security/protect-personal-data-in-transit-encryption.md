---
title: "aaaProtect kişisel Aktarımdaki verileri şifreleme Azure ile | Microsoft Docs"
description: "Azure tooprotect kişisel verileri şifreleme kullanma"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="d1af6-103">Azure şifreleme teknolojilerini: şifrelemesi ile Aktarım kişisel verileri koruma</span><span class="sxs-lookup"><span data-stu-id="d1af6-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="d1af6-104">Bu makalede anlamak ve Azure şifreleme teknolojileri toosecure veri aktarım sırasında kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="d1af6-105">Kişisel veri koruma hello gizliliğini hello ağ üzerinden geçen çok katmanlı savunma güvenlik stratejisinin önemli bir parçası aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="d1af6-106">Şifreleme Aktarımdaki tasarlanmış tooprevent engeller mümkün tooview veya kullanım hello veri aktarımları karşılar bir saldırgan ' dir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="d1af6-107">Senaryo</span><span class="sxs-lookup"><span data-stu-id="d1af6-107">Scenario</span></span>

<span data-ttu-id="d1af6-108">Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="d1af6-109">toosupport bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere</span><span class="sxs-lookup"><span data-stu-id="d1af6-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="d1af6-110">Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="d1af6-111">Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="d1af6-112">Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="d1af6-113">Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="d1af6-114">Kişisel veriler müşterilerin hello veritabanında hello şirketin şubelere ve seyahat Merhaba Dünya bulunan aracılardan gelen girilir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="d1af6-115">Müşteri bilgilerini içeren belgeleri hello ağ tooAzure depolama aktarılır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d1af6-116">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="d1af6-116">Problem statement</span></span>

<span data-ttu-id="d1af6-117">Merhaba şirket müşterilerin hello gizliliğini korumak gerekir ve çalışanların kişisel veriler, Azure hizmetlerinden geçiş tooand içinde.</span><span class="sxs-lookup"><span data-stu-id="d1af6-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="d1af6-118">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="d1af6-118">Company goal</span></span>

<span data-ttu-id="d1af6-119">Şirket hedef tooensure hello disk zaman devre dışı kişisel veriler şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="d1af6-120">Yetkisiz kişilerin hello disk kapalı kişisel verilere müdahale okunamaz kılacak bir formda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="d1af6-121">Şifreleme uygulama kolay ya da kullanıcılar ve Yöneticiler için tamamen saydam olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="d1af6-122">Çözümler</span><span class="sxs-lookup"><span data-stu-id="d1af6-122">Solutions</span></span>

<span data-ttu-id="d1af6-123">Azure hizmetleri sağlayan birden çok Araçlar ve teknolojiler toohelp kişisel Aktarımdaki verileri korumak.</span><span class="sxs-lookup"><span data-stu-id="d1af6-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="d1af6-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d1af6-124">Azure Storage</span></span>

<span data-ttu-id="d1af6-125">Merhaba bulutta depolanan veriler toohello Azure veri merkezi, hello world fiziksel olarak herhangi bir yerde bulunabilir hello istemciden gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="d1af6-126">Bu verileri kullanıcılar tarafından alındığında, onu yeniden hello geçen yönü ters.</span><span class="sxs-lookup"><span data-stu-id="d1af6-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="d1af6-127">Aktarım sırasında veriler üzerinde hello genel Internet saldırganlar tarafından riskinin her zaman altındadır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="d1af6-128">Bu önemli tooprotect hello gizlilik kişisel veri aktarım düzeyinde şifreleme toosecure gibi konumlar arasında taşır kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="d1af6-129">Merhaba HTTPS protokolünü hello Internet güvenli, şifrelenmiş iletişim kanalı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1af6-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="d1af6-130">HTTPS, REST API'leri çağrılırken Azure Storage ve kullanılan tooaccess nesneleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="d1af6-131">Kullanırken hello HTTPS protokolünü kullanılmasını zorunlu [paylaşılan erişim imzaları](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate erişim tooAzure depolama nesneleri.</span><span class="sxs-lookup"><span data-stu-id="d1af6-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="d1af6-132">SAS iki tür vardır: hizmet SAS ve hesap SAS.</span><span class="sxs-lookup"><span data-stu-id="d1af6-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="d1af6-133">Hizmet SAS nasıl oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="d1af6-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="d1af6-134">Bir hizmet SAS temsilciler erişim tooa kaynak yalnızca bir hello depolama hizmetleri (blob, kuyruk, tablo veya dosya hizmeti).</span><span class="sxs-lookup"><span data-stu-id="d1af6-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="d1af6-135">bir hizmet SAS tooconstruct hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="d1af6-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="d1af6-136">Merhaba imzalandı sürüm alanını belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="d1af6-137">Merhaba imzalandı kaynak (Blob ve sadece dosya hizmeti) belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="d1af6-138">Sorgu parametreleri tooOverride yanıt üstbilgilerini (Blob hizmeti ve sadece dosya hizmeti) belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="d1af6-139">Merhaba (yalnızca tablo hizmeti) tablo adı belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="d1af6-140">Merhaba erişim ilkesini belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="d1af6-141">Merhaba imza geçerlilik aralığı belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="d1af6-142">İzinleri belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-142">Specify Permissions</span></span>

9. <span data-ttu-id="d1af6-143">IP adresi veya IP aralığını belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="d1af6-144">Merhaba HTTP protokolü belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="d1af6-145">Tablo erişim aralıkları belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="d1af6-146">Merhaba imzalandı tanımlayıcısını belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="d1af6-147">Merhaba imza belirtin</span><span class="sxs-lookup"><span data-stu-id="d1af6-147">Specify hello Signature</span></span>

<span data-ttu-id="d1af6-148">Daha ayrıntılı yönergeler için bkz: [hizmet SAS oluşturma](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="d1af6-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="d1af6-149">Bir hesap SAS nasıl oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="d1af6-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="d1af6-150">Bir hesap SAS bir veya daha fazla hello depolama hizmet erişim tooresources atar.</span><span class="sxs-lookup"><span data-stu-id="d1af6-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="d1af6-151">Ayrıca, erişim tooread, yazma ve silme işlemleri blob kapsayıcılar, tablolar, kuyruklar ve hizmet SAS ile izin verilmiyor dosya paylaşımları üzerinde devredebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1af6-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="d1af6-152">Bir hesap SAS yapımı hizmet SAS, benzer toothat ' dir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="d1af6-153">Ayrıntılı yönergeler için bkz: [bir hesap SAS oluşturma.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="d1af6-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="d1af6-154">HTTPS nasıl REST API'leri çağrılırken zorunlu?</span><span class="sxs-lookup"><span data-stu-id="d1af6-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="d1af6-155">REST API'leri tooaccess nesneleri depolama hesaplarında çağrılırken HTTPS tooenforce hello kullanımı, hello depolama hesabı için güvenli aktarım gerekli etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1af6-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="d1af6-156">Hello Azure portal, seçin **depolama hesabı oluştur**, veya mevcut bir depolama hesabını seçin **ayarları** ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="d1af6-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="d1af6-157">Altında **güvenli aktarım gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="d1af6-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Bir depolama hesabı oluşturma](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="d1af6-159">Daha ayrıntılı yönergeler için de dahil olmak üzere tooenable güvenli aktarım gerekli programlı olarak bkz nasıl [gerektiren güvenli aktarım](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="d1af6-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="d1af6-160">Nasıl Azure dosya depolama birimindeki verileri şifreliyor mu?</span><span class="sxs-lookup"><span data-stu-id="d1af6-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="d1af6-161">Aktarım ile tooencrypt verileri [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), SMB kullanabilirsiniz 3.x Windows 8, 8.1 ve 10 ve Windows Server 2012 R2 ve Windows Server 2016 ile.</span><span class="sxs-lookup"><span data-stu-id="d1af6-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="d1af6-162">Hello Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="d1af6-163">Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve bazı özellikleri hello Linux SMB istemcisi kullanarak senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="d1af6-164">Azure istemci tarafı şifreleme</span><span class="sxs-lookup"><span data-stu-id="d1af6-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="d1af6-165">Bir istemci uygulaması ve Azure Storage arasında aktarıldığı sırada kişisel verileri korumak için başka bir seçenek [istemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="d1af6-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="d1af6-166">Azure depolama alanına aktarılmadan önce Hello veri şifrelenir ve Azure depolama biriminden hello veri aldığınızda hello istemci tarafında alındıktan sonra hello veri şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="d1af6-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="d1af6-167">Azure siteden siteye VPN</span><span class="sxs-lookup"><span data-stu-id="d1af6-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="d1af6-168">Etkili şekilde bir tooprotect kişisel verileri şirket ağı veya kullanıcı ve hello Azure sanal ağı arasında aktarımda toouse olan bir [siteden siteye](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) veya [noktası site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) sanal özel ağ (VPN).</span><span class="sxs-lookup"><span data-stu-id="d1af6-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="d1af6-169">Bir VPN bağlantısı hello Internet şifrelenmiş güvenli bir tünel oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="d1af6-170">Siteden siteye VPN bağlantısı nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="d1af6-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="d1af6-171">Siteden siteye VPN hello şirket ağı tooAzure birden fazla kullanıcı bağlanır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="d1af6-172">toocreate hello Azure portal'ın bir siteden siteye bağlantı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="d1af6-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="d1af6-173">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-173">Create a virtual network.</span></span>

2. <span data-ttu-id="d1af6-174">Bir DNS sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="d1af6-175">Merhaba ağ geçidi alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="d1af6-176">Merhaba VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="d1af6-177">Merhaba yerel ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="d1af6-178">VPN Cihazınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d1af6-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="d1af6-179">Merhaba VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="d1af6-180">Merhaba VPN bağlantısını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d1af6-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="d1af6-181">Daha fazla hakkında ayrıntılı yönergeler için nasıl toocreate bir site siteye bağlantı hello Azure portal, bkz: [Create bir Site siteye bağlantı hello Azure Portal'ın.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="d1af6-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="d1af6-182">Bir noktadan siteye VPN bağlantısı nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="d1af6-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="d1af6-183">Bir noktadan siteye VPN bir tek bir istemci bilgisayar tooa sanal ağdan güvenli bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="d1af6-184">Uzak bir konumdan tooconnect tooAzure gibi giriş veya bir otel veya konferans Merkezi'nden istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="d1af6-185">bir noktadan siteye bağlantı hello Azure portal'ın toocreate,</span><span class="sxs-lookup"><span data-stu-id="d1af6-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="d1af6-186">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-186">Create a virtual network.</span></span>

2. <span data-ttu-id="d1af6-187">Bir ağ geçidi alt ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="d1af6-188">Bir DNS sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-188">Specify a DNS server.</span></span> <span data-ttu-id="d1af6-189">(isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="d1af6-189">(optional)</span></span>

4. <span data-ttu-id="d1af6-190">Bir sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1af6-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="d1af6-191">Sertifikaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-191">Generate certificates.</span></span>

6. <span data-ttu-id="d1af6-192">Merhaba istemcisi adres havuzunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="d1af6-193">Merhaba kök sertifika ortak sertifikası verileri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="d1af6-194">Oluştur ve hello VPN istemcisi yapılandırma paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="d1af6-195">Dışarı aktarılan istemci sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1af6-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="d1af6-196">TooAzure bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d1af6-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="d1af6-197">Bağlantınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d1af6-197">Verify your connection.</span></span>

<span data-ttu-id="d1af6-198">Daha ayrıntılı yönergeler için bkz: [bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="d1af6-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="d1af6-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="d1af6-199">SSL/TLS</span></span>

<span data-ttu-id="d1af6-200">Microsoft, her zaman farklı konumlar arasında SSL/TLS protokolleri tooexchange veri kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="d1af6-201">Toouse seçin kuruluşlar [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove büyük veri kümeleri ayrılmış bir yüksek hızlı WAN bağlantısı üzerinden de hello SSL/TLS veya diğer protokoller için ek koruma kullanarak uygulama düzeyi hello verileri şifrelemek.</span><span class="sxs-lookup"><span data-stu-id="d1af6-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="d1af6-202">Varsayılan şifreleme</span><span class="sxs-lookup"><span data-stu-id="d1af6-202">Encryption by default</span></span>

<span data-ttu-id="d1af6-203">Microsoft, müşteriler ve Azure bulut hizmetleri arasında aktarımda şifreleme tooprotect verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="d1af6-204">Hello Azure portalı Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="d1af6-205">[Aktarım Katmanı Güvenliği](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protokolüdür Microsoft veri merkezleri toonegotiate tooMicrosoft bulut hizmetlerine bağlanacak istemci sistemleriyle çalışacak hello.</span><span class="sxs-lookup"><span data-stu-id="d1af6-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="d1af6-206">TLS, güçlü kimlik doğrulaması, ileti gizliliği ve bütünlük (ileti oynama, kişiler tarafından ele ve sahtekarlığı saptama etkinleştirir), birlikte çalışabilirlik, algoritma esnekliği, dağıtım ve kullanım kolaylığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1af6-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="d1af6-207">[Kusursuz iletme gizliliği](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) de işe benzersiz anahtarlar böylece müşterilerin istemci sistemleri ve Microsoft'un bulut hizmetleri arasında her bağlantı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="d1af6-208">Bağlantıları tooMicrosoft bulut hizmetleri de dayalı RSA 2.048 bit şifreleme anahtar uzunluklarını yararlanın.</span><span class="sxs-lookup"><span data-stu-id="d1af6-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="d1af6-209">Merhaba TLS, RSA 2.048 bit anahtar uzunluğu, birleşimi ve PFS kılar çok daha zor birisi için Microsoft bulut hizmetlerine ve müşterileri arasında aktarımda toointercept ve erişim veriler.</span><span class="sxs-lookup"><span data-stu-id="d1af6-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="d1af6-210">Aktarımdaki verileri [Data Lake Store'da] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview) her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="d1af6-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="d1af6-211">Ayrıca tooencrypting veri önceki toostoring toopersistent medya hello veri ayrıca her zaman aktarım sırasında HTTPS kullanılarak korunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d1af6-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="d1af6-212">HTTPS için Data Lake Store REST arabirimleri hello desteklenir hello tek protokoldür.</span><span class="sxs-lookup"><span data-stu-id="d1af6-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="d1af6-213">Özet</span><span class="sxs-lookup"><span data-stu-id="d1af6-213">Summary</span></span>

<span data-ttu-id="d1af6-214">Merhaba şirket HTTPS bağlantıları tooAzure depolama zorlama, paylaşılan erişim imzaları kullanarak ve güvenli aktarım gerekli hello depolama hesaplarında etkinleştirme kişisel veri ve hello gizlilik bu tür veri korumanın amacı gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1af6-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="d1af6-215">Bunlar aynı zamanda kişisel verileri SMB 3.0 bağlantıları kullanarak ve istemci tarafı şifreleme uygulama koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1af6-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="d1af6-216">Siteden siteye VPN bağlantılarından şirket ağı toohello Azure sanal ağı hello ve bireysel kullanıcılardan noktadan siteye VPN bağlantıları üzerinden güvenli bir şekilde kişisel veriler seyahat güvenli bir tünel oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1af6-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="d1af6-217">Microsoft'un varsayılan şifreleme yöntemler kişisel verilerin hello gizliliği daha fazla koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1af6-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1af6-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1af6-218">Next steps</span></span>

- [<span data-ttu-id="d1af6-219">Azure veri güvenliği ve şifreleme en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d1af6-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="d1af6-220">VPN Gateway için planlama ve tasarım</span><span class="sxs-lookup"><span data-stu-id="d1af6-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="d1af6-221">VPN Gateway ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="d1af6-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="d1af6-222">Satın alma ve Azure uygulama hizmetiniz için bir SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d1af6-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
