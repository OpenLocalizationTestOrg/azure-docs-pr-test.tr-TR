---
title: "Kişisel Aktarımdaki verileri şifreleme Azure ile koruma | Microsoft Docs"
description: "Kişisel verilerinizi korumak için Azure'da şifreleme kullanma"
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
ms.openlocfilehash: 99e40b8a09a2f151e7f83fbb58bdfc00ae4b1268
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="b3ab8-103">Azure şifreleme teknolojilerini: şifrelemesi ile Aktarım kişisel verileri koruma</span><span class="sxs-lookup"><span data-stu-id="b3ab8-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="b3ab8-104">Bu makalede anlamak ve Azure şifreleme teknolojilerini verilerin güvenliğini sağlamak için aktarım sırasında kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-104">This article will help you understand and use Azure encryption technologies to secure data in transit.</span></span> 

<span data-ttu-id="b3ab8-105">Ağ üzerinden geçen gibi kişisel verilerin gizliliği koruma, çok katmanlı savunma güvenlik stratejisinin önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-105">Protecting the privacy of personal data as it travels across the network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="b3ab8-106">Şifreleme Aktarımdaki görüntüleyebilir veya verileri kullanma engeller iletimleri karşılar bir saldırganın önlemek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-106">Encryption in transit is designed to prevent an attacker who intercepts transmissions from being able to view or use the data.</span></span>

## <a name="scenario"></a><span data-ttu-id="b3ab8-107">Senaryo</span><span class="sxs-lookup"><span data-stu-id="b3ab8-107">Scenario</span></span>

<span data-ttu-id="b3ab8-108">Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, masraflarını Akdeniz, Adriatic ve Baltık seas yanı sıra İngiliz Adaları arasında içinde sunmaya işlemlerini genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="b3ab8-109">Bu çalışmalarını desteklemek için daha küçük birkaç seyahat satırlarını İtalya, Almanya, Danimarka ve İngiltere göre aldı</span><span class="sxs-lookup"><span data-stu-id="b3ab8-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="b3ab8-110">Şirket Microsoft Azure bulutta şirket verilerini depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="b3ab8-111">Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="b3ab8-112">Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="b3ab8-113">Seyahat satır de geçerli ve geçmiş müşterilerle ilişkilerini izlemek için kişisel bilgi içeren büyük bir veritabanı ödül ve bağlılık programı üyelerinin tutar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="b3ab8-114">Müşteriler, kişisel verileri şirketin şubelere ve seyahat tüm dünyada bulunan aracılardan gelen veritabanında girilir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-114">Personal data of customers is entered in the database from the company’s remote offices and from travel agents located around the world.</span></span> <span data-ttu-id="b3ab8-115">Müşteri bilgilerini içeren belgeleri, Azure depolama alanına ağ üzerinden aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-115">Documents containing customer information are transferred across the network to Azure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="b3ab8-116">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="b3ab8-116">Problem statement</span></span>

<span data-ttu-id="b3ab8-117">Aktarım için ve Azure hizmetlerinden ederken şirket müşterilerin ve çalışanların kişisel verilerin gizliliği korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-117">The company must protect the privacy of customers’ and employees’ personal data while it is in transit to and from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="b3ab8-118">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="b3ab8-118">Company goal</span></span>

<span data-ttu-id="b3ab8-119">Kişisel veriler disk zaman devre dışı şifrelendiğinden emin olmak için şirket hedef.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-119">The company goal to ensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="b3ab8-120">Yetkisiz kişilerin disk kapalı kişisel verilere müdahale okunamaz kılacak bir formda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-120">If unauthorized persons intercept the off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="b3ab8-121">Şifreleme uygulama kolay ya da kullanıcılar ve Yöneticiler için tamamen saydam olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="b3ab8-122">Çözümler</span><span class="sxs-lookup"><span data-stu-id="b3ab8-122">Solutions</span></span>

<span data-ttu-id="b3ab8-123">Birden çok Araçlar ve teknolojiler aktarım kişisel verileri korumaya yardımcı olmak için Azure hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-123">Azure services provide multiple tools and technologies to help you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="b3ab8-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b3ab8-124">Azure Storage</span></span>

<span data-ttu-id="b3ab8-125">Bulutta depolanan verileri Azure veri merkezine dünyada fiziksel olarak bulunan herhangi bir yere olabilecek istemciden gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-125">Data that is stored in the cloud must travel from the client, which can be physically located anywhere in the world, to the Azure data center.</span></span> <span data-ttu-id="b3ab8-126">Bu verileri kullanıcılar tarafından alındığında, yeniden ters yönde dolaşır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-126">When that data is retrieved by users, it travels again, in the opposite direction.</span></span> <span data-ttu-id="b3ab8-127">Aktarımdaki verileri ortak Internet üzerinden saldırganlar tarafından riskinin her zaman altındadır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-127">Data that is in transit over the public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="b3ab8-128">Konumlar arasında hareket ederken güvenliğini sağlamak için aktarım düzeyinde şifreleme kullanılarak kişisel verilerin gizliliği korumak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-128">It is important to protect the privacy of personal data by using transport-level encryption to secure it as it moves between locations.</span></span>

<span data-ttu-id="b3ab8-129">HTTPS protokolü, Internet üzerinden güvenli, şifrelenmiş iletişim kanalı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-129">The HTTPS protocol provides a secure, encrypted communications channel over the Internet.</span></span> <span data-ttu-id="b3ab8-130">HTTPS, REST API'leri çağrılırken Azure Storage ve nesneleri erişmek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-130">HTTPS should be used to access objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="b3ab8-131">Kullanırken, HTTPS protokolünü kullanılmasını zorunlu [paylaşılan erişim imzaları](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) Azure Storage nesnelere erişimi devretmek için (SAS).</span><span class="sxs-lookup"><span data-stu-id="b3ab8-131">You enforce use of the HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) to delegate access to Azure Storage objects.</span></span> <span data-ttu-id="b3ab8-132">SAS iki tür vardır: hizmet SAS ve hesap SAS.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="b3ab8-133">Hizmet SAS nasıl oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="b3ab8-134">Hizmet SAS depolama hizmetleri (blob, kuyruk, tablo veya dosya hizmeti) yalnızca birinde bir kaynağa erişim atar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-134">A Service SAS delegates access to a resource in just one of the storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="b3ab8-135">Hizmet SAS oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="b3ab8-135">To construct a Service SAS, do the following:</span></span>

1. <span data-ttu-id="b3ab8-136">İmzalı sürüm alanını belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-136">Specify the Signed Version Field</span></span>

2. <span data-ttu-id="b3ab8-137">İmzalı kaynak (Blob ve yalnızca dosya hizmeti) belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-137">Specify the Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="b3ab8-138">Yanıt Üstbilgileri (Blob hizmeti ve yalnızca dosya hizmeti) geçersiz kılmak için sorgu parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-138">Specify Query Parameters to Override Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="b3ab8-139">(Yalnızca tablo hizmeti) tablo adı belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-139">Specify the Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="b3ab8-140">Erişim ilkesini belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-140">Specify the Access Policy</span></span>

6. <span data-ttu-id="b3ab8-141">İmza geçerlilik aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-141">Specify the Signature Validity Interval</span></span>

8. <span data-ttu-id="b3ab8-142">İzinleri belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-142">Specify Permissions</span></span>

9. <span data-ttu-id="b3ab8-143">IP adresi veya IP aralığını belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="b3ab8-144">HTTP protokolünü belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-144">Specify the HTTP Protocol</span></span>

11. <span data-ttu-id="b3ab8-145">Tablo erişim aralıkları belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="b3ab8-146">İmzalı tanımlayıcısını belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-146">Specify the Signed Identifier</span></span>

13. <span data-ttu-id="b3ab8-147">İmza belirtin</span><span class="sxs-lookup"><span data-stu-id="b3ab8-147">Specify the Signature</span></span>

<span data-ttu-id="b3ab8-148">Daha ayrıntılı yönergeler için bkz: [hizmet SAS oluşturma](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="b3ab8-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="b3ab8-149">Bir hesap SAS nasıl oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="b3ab8-150">Bir hesap SAS bir veya daha fazla depolama hizmetindeki kaynaklara erişim atar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-150">An Account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="b3ab8-151">Bununla birlikte hizmet SAS ile izin verilmeyen blob kapsayıcılar, tablolar kuyruklar ve dosya paylaşımları üzerinde okuma, yazma ve silme işlemleri için yetkilendirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="b3ab8-152">Bir hesap SAS yapımı, bir hizmet SAS benzer.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-152">Construction of an Account SAS is similar to that of a Service SAS.</span></span> <span data-ttu-id="b3ab8-153">Ayrıntılı yönergeler için bkz: [bir hesap SAS oluşturma.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="b3ab8-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="b3ab8-154">HTTPS nasıl REST API'leri çağrılırken zorunlu?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="b3ab8-155">REST API'leri depolama hesaplarındaki erişim nesnelere çağrılırken HTTPS kullanımını zorunlu kılmak için güvenli aktarım gerekli depolama hesabı için etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-155">To enforce the use of HTTPS when calling REST APIs to access objects in storage accounts, you can enable Secure Transfer Required for the storage account.</span></span> 

1. <span data-ttu-id="b3ab8-156">Azure portalında seçin **depolama hesabı oluştur**, veya mevcut bir depolama hesabını seçin **ayarları** ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-156">In the Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="b3ab8-157">Altında **güvenli aktarım gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Bir depolama hesabı oluşturma](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="b3ab8-159">Daha ayrıntılı yönergeler için güvenli aktarım gerekli program aracılığıyla etkinleştirmek için bkz: nasıl dahil olmak üzere [gerektiren güvenli aktarım](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="b3ab8-159">For more detailed instructions, including how to enable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="b3ab8-160">Nasıl Azure dosya depolama birimindeki verileri şifreliyor mu?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="b3ab8-161">İle Aktarımdaki verileri şifrelemek için [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), SMB kullanabilirsiniz 3.x Windows 8, 8.1 ve 10 ve Windows Server 2012 R2 ve Windows Server 2016 ile.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-161">To encrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="b3ab8-162">Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-162">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="b3ab8-163">Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve Linux SMB istemcisi bazı özellikleri kullanarak senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="b3ab8-164">Azure istemci tarafı şifreleme</span><span class="sxs-lookup"><span data-stu-id="b3ab8-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="b3ab8-165">Bir istemci uygulaması ve Azure Storage arasında aktarıldığı sırada kişisel verileri korumak için başka bir seçenek [istemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="b3ab8-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="b3ab8-166">Azure depolama alanına aktarılmadan önce veriler şifrelenir ve verileri Azure depolama biriminden aldığınızda, istemci tarafında alındıktan sonra verilerin şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-166">The data is encrypted before being transferred into Azure Storage and when you retrieve the data from Azure Storage, the data is decrypted after it is received on the client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="b3ab8-167">Azure siteden siteye VPN</span><span class="sxs-lookup"><span data-stu-id="b3ab8-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="b3ab8-168">Bir şirket ağı veya kullanıcı ve Azure sanal ağı arasında aktarımda kişisel verilerinizi korumak için etkili bir yol kullanmaktır bir [siteden siteye](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) veya [noktası site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) sanal özel ağ (VPN).</span><span class="sxs-lookup"><span data-stu-id="b3ab8-168">An effective way to protect personal data in transit between a corporate network or user and the Azure virtual network is to use a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="b3ab8-169">Bir VPN bağlantısı Internet üzerinden şifrelenmiş güvenli bir tünel oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-169">A VPN connection creates a secure encrypted tunnel across the Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="b3ab8-170">Siteden siteye VPN bağlantısı nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="b3ab8-171">Siteden siteye VPN şirket ağındaki birden çok kullanıcı için Azure bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-171">A site-to-site VPN connects multiple users on the corporate network to Azure.</span></span> <span data-ttu-id="b3ab8-172">Azure portalında bir siteden siteye bağlantı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="b3ab8-172">To create a site-to-site connection in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="b3ab8-173">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-173">Create a virtual network.</span></span>

2. <span data-ttu-id="b3ab8-174">Bir DNS sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="b3ab8-175">Ağ geçidi alt ağını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-175">Create the gateway subnet.</span></span>

4. <span data-ttu-id="b3ab8-176">VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-176">Create the VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="b3ab8-177">Yerel ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-177">Create the local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="b3ab8-178">VPN Cihazınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="b3ab8-179">VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-179">Create the VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="b3ab8-180">VPN bağlantısını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-180">Verify the VPN connection.</span></span>

<span data-ttu-id="b3ab8-181">Azure portalında bir siteden siteye bağlantı oluşturma konusunda daha ayrıntılı yönergeler için bkz. [Azure Portalı'nda bir siteden siteye bağlantı oluşturun.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="b3ab8-181">For more detailed instructions on how to create a site-to-site connection in the Azure portal, see [Create a Site-to-Site  connection in the Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="b3ab8-182">Bir noktadan siteye VPN bağlantısı nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="b3ab8-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="b3ab8-183">Noktadan siteye VPN, tek bir istemci bilgisayardan bir sanal ağa güvenli bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-183">A Point-to-Site VPN creates a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="b3ab8-184">Uzak bir konumdan Azure gibi giriş veya bir otel veya konferans Merkezi'nden bağlanmak istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-184">This is useful when you  want to connect to Azure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="b3ab8-185">Azure portalında bir noktadan siteye bağlantı oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="b3ab8-185">To create a point-to-site  connection in the Azure portal,</span></span>

1. <span data-ttu-id="b3ab8-186">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-186">Create a virtual network.</span></span>

2. <span data-ttu-id="b3ab8-187">Bir ağ geçidi alt ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="b3ab8-188">Bir DNS sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-188">Specify a DNS server.</span></span> <span data-ttu-id="b3ab8-189">(isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="b3ab8-189">(optional)</span></span>

4. <span data-ttu-id="b3ab8-190">Bir sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="b3ab8-191">Sertifikaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-191">Generate certificates.</span></span>

6. <span data-ttu-id="b3ab8-192">İstemcisi adres havuzunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-192">Add the client address pool.</span></span>

7. <span data-ttu-id="b3ab8-193">Kök sertifika ortak sertifikası verileri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-193">Upload the root certificate public certificate data.</span></span>

8. <span data-ttu-id="b3ab8-194">Oluştur ve VPN istemcisi yapılandırma paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-194">Generate and install the VPN client configuration package.</span></span>

9. <span data-ttu-id="b3ab8-195">Dışarı aktarılan istemci sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="b3ab8-196">Azure'a bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-196">Connect to Azure.</span></span>

11. <span data-ttu-id="b3ab8-197">Bağlantınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-197">Verify your connection.</span></span>

<span data-ttu-id="b3ab8-198">Daha ayrıntılı yönergeler için bkz: [sertifika kimlik doğrulaması kullanarak bir sanal ağa noktadan siteye bağlantı yapılandırma: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="b3ab8-198">For more detailed instructions, see [Configure a Point-to-Site connection to a VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="b3ab8-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="b3ab8-199">SSL/TLS</span></span>

<span data-ttu-id="b3ab8-200">Microsoft, her zaman SSL/TLS protokolleri farklı konumlar arasında veri değişimi için kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-200">Microsoft recommends that you always use SSL/TLS protocols to exchange data across different locations.</span></span> <span data-ttu-id="b3ab8-201">Kullanmayı tercih kuruluşlar [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) ayrılmış bir yüksek hızlı WAN üzerinden büyük veri kümeleri taşımak için bağlantı verilerinin uygulama düzeyinde de şifreleyebilirsiniz SSL/TLS ya da diğer protokolleri kullanarak koruma eklendi.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-201">Organizations that choose to use [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) to move large data sets over a dedicated high-speed WAN link can also encrypt the data at the application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="b3ab8-202">Varsayılan şifreleme</span><span class="sxs-lookup"><span data-stu-id="b3ab8-202">Encryption by default</span></span>

<span data-ttu-id="b3ab8-203">Microsoft, müşteriler ve Azure bulut hizmetleri arasında Aktarımdaki verileri korumak için şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-203">Microsoft uses encryption to protect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="b3ab8-204">Azure Portalı aracılığıyla Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-204">If you are interacting with Azure Storage through the Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="b3ab8-205">[Aktarım Katmanı Güvenliği](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protokolüdür, Microsoft veri merkezleri Microsoft bulut hizmetlerine bağlanmak istemci sistemleri ile belirlemeye çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is the protocol that Microsoft data centers will attempt to negotiate with client systems that connect to Microsoft cloud services.</span></span> <span data-ttu-id="b3ab8-206">TLS, güçlü kimlik doğrulaması, ileti gizliliği ve bütünlük (ileti oynama, kişiler tarafından ele ve sahtekarlığı saptama etkinleştirir), birlikte çalışabilirlik, algoritma esnekliği, dağıtım ve kullanım kolaylığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="b3ab8-207">[Kusursuz iletme gizliliği](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) de işe benzersiz anahtarlar böylece müşterilerin istemci sistemleri ve Microsoft'un bulut hizmetleri arasında her bağlantı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="b3ab8-208">Microsoft bulut hizmetlerine bağlantıları da temel RSA 2.048 bit şifreleme anahtar uzunluklarını yararlanın.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-208">Connections to Microsoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="b3ab8-209">TLS, RSA 2.048 bit anahtar uzunluğu, birleşimi ve PFS kılar çok daha zor birisi için Microsoft bulut hizmetlerine ve müşterileri arasında aktarımda ıntercept ve erişim veriler için.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-209">The combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone to intercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="b3ab8-210">Aktarımdaki verileri [Data Lake Store'da] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview) her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="b3ab8-211">Kalıcı medyaya depolama önce veri şifrelemeye ek olarak, aktarımdaki veriler de her zaman HTTPS kullanılarak korunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-211">In addition to encrypting data prior to storing to persistent media, the data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="b3ab8-212">HTTPS, Data Lake Store REST arabirimleri için desteklenen tek protokoldür.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-212">HTTPS is the only protocol that is supported for the Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="b3ab8-213">Özet</span><span class="sxs-lookup"><span data-stu-id="b3ab8-213">Summary</span></span>

<span data-ttu-id="b3ab8-214">Şirket HTTPS bağlantıları için Azure Storage zorlama, paylaşılan erişim imzaları kullanarak ve güvenli aktarım gerekli depolama hesaplarında etkinleştirme kişisel veriler ve bu tür verilerin gizliliği korumanın amacı gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-214">The company can accomplish its goal of protecting personal data and the privacy of such data by enforcing HTTPS connections to Azure Storage, using Shared Access Signatures and enabling Secure Transfer Required on the storage accounts.</span></span> <span data-ttu-id="b3ab8-215">Bunlar aynı zamanda kişisel verileri SMB 3.0 bağlantıları kullanarak ve istemci tarafı şifreleme uygulama koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="b3ab8-216">Siteden siteye VPN bağlantıları Azure sanal ağı için Kurumsal ağdan ve bireysel kullanıcılardan noktadan siteye VPN bağlantıları üzerinden güvenli bir şekilde kişisel veriler seyahat güvenli bir tünel oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-216">Site-to-site VPN connections from the corporate network to the Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="b3ab8-217">Microsoft'un varsayılan şifreleme yöntemler kişisel verilerin gizliliği daha fazla koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3ab8-217">Microsoft’s default encryption practices will further protect the privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3ab8-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3ab8-218">Next steps</span></span>

- [<span data-ttu-id="b3ab8-219">Azure veri güvenliği ve şifreleme en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="b3ab8-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="b3ab8-220">VPN Gateway için planlama ve tasarım</span><span class="sxs-lookup"><span data-stu-id="b3ab8-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="b3ab8-221">VPN Gateway ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="b3ab8-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="b3ab8-222">Satın alma ve Azure uygulama hizmetiniz için bir SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3ab8-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
