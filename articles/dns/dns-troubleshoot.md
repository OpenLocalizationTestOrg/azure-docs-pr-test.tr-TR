---
title: "aaaAzure DNS sorun giderme kılavuzu | Microsoft Docs"
description: "Azure DNS ile nasıl tootroubleshoot ortak sorunları"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="1c080-103">Azure DNS sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="1c080-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="1c080-104">Bu sayfa, ortak Azure DNS sorular için sorun giderme bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c080-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="1c080-105">Bu adımları sorununuzu çözmüyorsa, ayrıca arayın veya sorununuzu ileti bizim [MSDN topluluk Destek Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="1c080-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="1c080-106">Alternatif olarak, bir Azure destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="1c080-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="1c080-107">Bir DNS bölgesi oluşturma kullanılamaz</span><span class="sxs-lookup"><span data-stu-id="1c080-107">I can't create a DNS zone</span></span>

<span data-ttu-id="1c080-108">tooresolve sık karşılaşılan sorunları, bir veya daha fazla hello aşağıdaki adımları deneyin:</span><span class="sxs-lookup"><span data-stu-id="1c080-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="1c080-109">Azure DNS denetim gözden geçirme hello toodetermine hello başarısızlık nedeniyle günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1c080-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="1c080-110">Her DNS bölge adı, kaynak grubu içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c080-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="1c080-111">Diğer bir deyişle, iki DNS bölgeleri hello ile aynı adı, bir kaynak grubu paylaşamaz.</span><span class="sxs-lookup"><span data-stu-id="1c080-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="1c080-112">Farklı bir bölge adı veya farklı bir kaynak grubu kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c080-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="1c080-113">"Ulaştınız veya bu abonelikte {abonelik kimliği} bölgelerinin hello en büyük sayıyı aştı." bir hata görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1c080-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="1c080-114">Ya da farklı bir Azure aboneliği kullanma, bazı bölgeleri silin veya abonelik sınırınızı Azure destek tooraise başvurun.</span><span class="sxs-lookup"><span data-stu-id="1c080-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="1c080-115">Bir hata görebilirsiniz "Merhaba bölge '{bölge name}' kullanılamaz."</span><span class="sxs-lookup"><span data-stu-id="1c080-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="1c080-116">Bu hata Azure DNS bu DNS bölgesi için ad sunucularını oluşturulamıyor tooallocate anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1c080-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="1c080-117">Farklı bir bölge adı kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c080-117">Try using a different zone name.</span></span> <span data-ttu-id="1c080-118">Alternatif olarak, hello etki alanı adı sahibi varsa, kimin ad sunucuları sizin için ayırabilirsiniz Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="1c080-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="1c080-119">**Önerilen belgeler**</span><span class="sxs-lookup"><span data-stu-id="1c080-119">**Recommended documents**</span></span>

<span data-ttu-id="1c080-120">[DNS bölgeleri ve kayıtları](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="1c080-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="1c080-121">
[DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1c080-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="1c080-122">DNS kaydı oluşturamıyorum</span><span class="sxs-lookup"><span data-stu-id="1c080-122">I can't create a DNS record</span></span>

<span data-ttu-id="1c080-123">tooresolve sık karşılaşılan sorunları, bir veya daha fazla hello aşağıdaki adımları deneyin:</span><span class="sxs-lookup"><span data-stu-id="1c080-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="1c080-124">Azure DNS denetim gözden geçirme hello toodetermine hello başarısızlık nedeniyle günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1c080-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="1c080-125">Merhaba kayıt kümesi zaten var mı?</span><span class="sxs-lookup"><span data-stu-id="1c080-125">Does hello record set exist already?</span></span>  <span data-ttu-id="1c080-126">Azure DNS kaydı kullanarak kayıtları yönetir *ayarlar*, aynı ad ve aynı hello hello kayıtlarının hello koleksiyonu olan türü.</span><span class="sxs-lookup"><span data-stu-id="1c080-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="1c080-127">Aynı ad ve zaten yazın hello içeren bir kayıt varsa, tooadd kaydı varolan hello düzenlemelisiniz gibi başka bir kayıtla ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c080-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="1c080-128">Merhaba DNS bölge tepesinde (Merhaba hello bölgenin ' kök') bir kaydı toocreate çalışıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="1c080-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="1c080-129">Bu nedenle, hello DNS kuralı toouse hello ise ' @' karakteri hello kayıt adı.</span><span class="sxs-lookup"><span data-stu-id="1c080-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="1c080-130">Ayrıca hello DNS standartlarında hello bölge tepesinde CNAME kayıtları vermez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1c080-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="1c080-131">CNAME çakışmanız mı var?</span><span class="sxs-lookup"><span data-stu-id="1c080-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="1c080-132">Merhaba DNS standartlarında hello aynı kayıt diğer herhangi bir tür olarak ad ile bir CNAME kaydı izin vermez.</span><span class="sxs-lookup"><span data-stu-id="1c080-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="1c080-133">Farklı bir tür aynı adı başarısız hello ile bir kayıt oluşturma, varolan bir CNAME varsa.</span><span class="sxs-lookup"><span data-stu-id="1c080-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="1c080-134">Varolan bir kaydı, farklı bir tür Hello adıyla eşleşen benzer şekilde, bir CNAME oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1c080-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="1c080-135">Başka bir kaydı veya farklı bir kayıt adını seçmek, Hello çakışma hello kaldırarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1c080-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="1c080-136">Hello hello DNS bölgesinde izin verilen kayıt kümesi sayısı sınırına? Merhaba geçerli kayıt kümesi sayısı ve hello en fazla kayıt kümesi sayısı hello hello 'Özellikler' hello bölgenin altında Azure portal'ın gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1c080-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="1c080-137">Bu sınıra ulaştınız, ardından bazı kaydı kümeleri silmek ya da Azure destek tooraise bu bölge için kayıt kümesi sınırınızı başvurun, sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c080-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="1c080-138">**Önerilen belgeler**</span><span class="sxs-lookup"><span data-stu-id="1c080-138">**Recommended documents**</span></span>

<span data-ttu-id="1c080-139">[DNS bölgeleri ve kayıtları](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="1c080-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="1c080-140">
[DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1c080-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="1c080-141">DNS kaydımı çözümleyemiyorum</span><span class="sxs-lookup"><span data-stu-id="1c080-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="1c080-142">DNS ad çözümlemesi, çeşitli nedenlerle başarısız olabilecek çok adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1c080-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="1c080-143">Merhaba aşağıdaki adımlar neden Azure DNS'de barındırılan bir bölgedeki bir DNS kaydı için DNS çözümlemesi başarısız araştırmanıza yardımcı.</span><span class="sxs-lookup"><span data-stu-id="1c080-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="1c080-144">Merhaba DNS kayıtlarını Azure DNS'de doğru şekilde yapılandırıldığını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1c080-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="1c080-145">Merhaba hello bölge adı, kayıt adı ve kayıt türünün doğru olduğunu denetleme Azure portal Hello DNS kayıtlarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1c080-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="1c080-146">Merhaba DNS kayıtları doğru hello Azure DNS ad sunucuları üzerinde çözümleme onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1c080-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="1c080-147">DNS sorguları yerel Bilgisayarınızdan yaparsanız hello ad sunucuları hello geçerli durumunu yansıtmaz önbelleğe alınan sonuçları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c080-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="1c080-148">Ayrıca, şirket ağlarına DNS proxy sunucuları, sık kullandığınız toospecific ad sunucuları, DNS sorgularını engellemek yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="1c080-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="1c080-149">tooavoid bu sorunları kullanan bir web tabanlı ad çözümleme hizmeti gibi [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="1c080-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="1c080-150">Emin toospecify hello Azure portal gösterildiği gibi hello doğru ad sunucuları, DNS bölgesi için olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c080-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="1c080-151">Merhaba DNS adı (Merhaba bölge adı dahil toospecify hello tam olarak nitelenmiş adını olması) doğru olduğundan ve hello kayıt türü doğru olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="1c080-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="1c080-152">Merhaba DNS etki alanı adının doğru bir şekilde açıldı onaylayın [toohello Azure DNS ad sunucuları temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1c080-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="1c080-153">[DNS temsilci seçme doğrulaması hizmeti sunan birçok 3. taraf web sitesi](https://www.bing.com/search?q=dns+check+tool) vardır.</span><span class="sxs-lookup"><span data-stu-id="1c080-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="1c080-154">Bu test bir *bölge* temsilci test hello DNS bölge adı ve hello tam kayıt adını değil yalnızca girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c080-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="1c080-155">Yukarıdaki Hello tamamlandığını DNS kaydınız artık doğru çözümlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c080-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="1c080-156">tooverify, yeniden kullanabileceğiniz [digwebinterface](http://digwebinterface.com), hello varsayılan ad sunucusu ayarlarını kullanarak bu süre.</span><span class="sxs-lookup"><span data-stu-id="1c080-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="1c080-157">**Önerilen belgeler**</span><span class="sxs-lookup"><span data-stu-id="1c080-157">**Recommended documents**</span></span>

[<span data-ttu-id="1c080-158">Bir etki alanı tooAzure DNS temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="1c080-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="1c080-159">Nasıl ı hello 'service' ve 'Protokolü' bir SRV kaydı için belirtin?</span><span class="sxs-lookup"><span data-stu-id="1c080-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="1c080-160">Azure DNS kayıt kümelerini olarak DNS kayıtlarını yönetir — kayıtları koleksiyonu ile aynı ad ve aynı hello hello hello türü.</span><span class="sxs-lookup"><span data-stu-id="1c080-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="1c080-161">SRV kayıt kümesi için hello 'service' ve 'Protokolü' hello kayıt kümesi adı bir parçası olarak belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c080-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="1c080-162">Merhaba diğer SRV parametreler ('priority', 'weight', 'bağlantı noktası' ve 'target') ayrı olarak hello kayıt kümesindeki her kayıt için belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1c080-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="1c080-163">Örnek SRV kayıt adları (hizmet adı 'sip', protokol 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="1c080-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="1c080-164">\_SIP. \_tcp (kayıt hello bölgenin tepesinde kümesi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="1c080-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="1c080-165">\_sip.\_tcp.sipservice ('sipservice' adlı bir kayıt kümesi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="1c080-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="1c080-166">**Önerilen belgeler**</span><span class="sxs-lookup"><span data-stu-id="1c080-166">**Recommended documents**</span></span>

<span data-ttu-id="1c080-167">[DNS bölgeleri ve kayıtları](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="1c080-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="1c080-168">
[Hello Azure portal kullanarak DNS kayıt kümelerini ve kayıtları oluşturma](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="1c080-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="1c080-169">
[SRV kayıt türü (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="1c080-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c080-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c080-170">Next steps</span></span>

* <span data-ttu-id="1c080-171">Hakkında bilgi edinin [Azure DNS bölgeleri ve kayıtları](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="1c080-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="1c080-172">Azure DNS kullanarak toostart öğrenin nasıl çok[bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md) ve [DNS kayıtlarını oluşturun](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1c080-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="1c080-173">Varolan bir DNS bölgesi toomigrate öğrenin nasıl çok[içeri ve dışarı aktarma bir DNS bölge dosyasına](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="1c080-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

