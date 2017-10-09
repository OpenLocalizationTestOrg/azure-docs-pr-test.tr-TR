---
title: "Varolan aaaWork şirket içi proxy sunucuları ve Azure AD | Microsoft Docs"
description: "Nasıl varolan toowork proxy sunucuları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="6fe8a-103">Mevcut şirket içi proxy sunucuları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="6fe8a-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="6fe8a-104">Bu makalede açıklanır nasıl tooconfigure Azure Active Directory (Azure AD) uygulama proxy'si bağlayıcılar toowork giden proxy sunucuları ile.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="6fe8a-105">Varolan proxy'leri sahip ağ ortamları olan müşteriler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="6fe8a-106">Bu ana dağıtım senaryolarında bakarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="6fe8a-107">Bağlayıcılar toobypass, şirket içi giden proxy'leri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="6fe8a-108">Bağlayıcılar toouse bir giden proxy tooaccess Azure AD uygulama proxy'si yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="6fe8a-109">Bağlayıcıları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="6fe8a-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="6fe8a-110">Merhaba giden proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="6fe8a-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="6fe8a-111">Ortamınızda bir giden proxy varsa, uygun izinleri tooconfigure hello giden proxy ile bir hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="6fe8a-112">Merhaba yükleyici hello hello yükleme yapan hello kullanıcının bağlamında çalıştığından, Microsoft Edge veya başka bir Internet tarayıcısı kullanarak hello yapılandırmasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="6fe8a-113">Microsoft edge'de tooconfigure hello proxy ayarları:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="6fe8a-114">Çok Git**ayarları** > **görünüm Gelişmiş ayarları** > **açık Proxy ayarlarını** > **el ile Ara Sunucusu Kurulumu** .</span><span class="sxs-lookup"><span data-stu-id="6fe8a-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="6fe8a-115">Ayarlama **bir proxy sunucu kullanacak** çok**üzerinde**seçin hello **hello proxy sunucusu için yerel (intranet) adresleri kullanmayın** onay kutusunu ve ardından değişiklik hello adresi ve bağlantı noktası tooreflect Yerel proxy sunucunuzun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="6fe8a-116">Merhaba gerekli proxy ayarlarını doldurun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-116">Fill in hello necessary proxy settings.</span></span>

   ![Proxy ayarları iletişim kutusu](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="6fe8a-118">Giden proxy atlama</span><span class="sxs-lookup"><span data-stu-id="6fe8a-118">Bypass outbound proxies</span></span>

<span data-ttu-id="6fe8a-119">Bağlayıcılar giden isteklerde temel işletim sistemi bileşeni vardır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="6fe8a-120">Bu bileşenler toolocate hello ağdaki bir proxy sunucusu otomatik olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="6fe8a-121">Merhaba ortamında etkinleştirilirse Web Proxy Otomatik Bulma (WPAD) kullanırlar.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="6fe8a-122">Merhaba işletim sistemi bileşenlerini wpad.domainsuffix için DNS araması gerçekleştirerek toolocate bir proxy sunucusu deneyin.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="6fe8a-123">Bu DNS çözümlenirse, HTTP isteğinden sonra toohello IP yapılır wpad.dat adresi.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="6fe8a-124">Bu isteği hello proxy yapılandırma betiği, ortamınızdaki haline gelir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="6fe8a-125">Merhaba bağlayıcı bu komut dosyası tooselect bir giden proxy sunucusunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="6fe8a-126">Ancak, bağlayıcı trafiği hala aracılığıyla, hello proxy gereken ek yapılandırma ayarları nedeniyle geçebilir değil.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="6fe8a-127">Merhaba bağlayıcı toobypass kullanır, şirket içi proxy tooensure doğrudan bağlantı toohello Azure yapılandırabilirsiniz Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="6fe8a-128">Bu yaklaşım (ağ ilkeniz için izin veriyorsa) öneririz, çünkü bu daha az bir yapılandırma toomaintain olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="6fe8a-129">Merhaba bağlayıcı için toodisable giden proxy kullanım hello C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve hello eklemek *system.net* Bu kod örneğinde gösterildiği bölümü :</span><span class="sxs-lookup"><span data-stu-id="6fe8a-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="6fe8a-130">Merhaba bağlayıcı güncelleştirici hizmetini de hello proxy atladığı tooensure C:\Program Files\Microsoft AAD uygulama Proxy Connector Updater bulunan bir benzer değişiklik toohello ApplicationProxyConnectorUpdaterService.exe.config dosyasını olun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="6fe8a-131">Toorevert toohello varsayılan .config dosyaları gerektiğinde toomake hello özgün dosyalarının kopyalarını emin olun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="6fe8a-132">Merhaba giden proxy sunucu kullan</span><span class="sxs-lookup"><span data-stu-id="6fe8a-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="6fe8a-133">Bazı ortamlar özel durum olmadan bir giden proxy üzerinden tüm giden trafiği toogo gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="6fe8a-134">Sonuç olarak, hello proxy atlama bir seçenek değil.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="6fe8a-135">Merhaba bağlayıcı trafiği toogo hello giden proxy üzerinden hello Aşağıdaki diyagramda gösterildiği gibi yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Bağlayıcı trafiği toogo bir giden proxy tooAzure AD aracılığıyla yapılandırma uygulama proxy'si](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="6fe8a-137">Sonuç olarak yalnızca giden trafiğe sahip olan olduğundan hiç gerek tooconfigure gelen, güvenlik duvarları üzerinden erişim.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="6fe8a-138">1. adım: hello bağlayıcısını yapılandırın ve Hizmetleri toogo hello giden proxy ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="6fe8a-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="6fe8a-139">WPAD hello ortamında etkin ve uygun şekilde yapılandırılmış varsa daha önce anlatıldığı gibi hello bağlayıcı hello giden proxy sunucusu ve girişimi toouse otomatik olarak keşfeder onu.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="6fe8a-140">Ancak, bir giden proxy üzerinden hello bağlayıcı toogo açıkça yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="6fe8a-141">toodo bunu hello C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve hello eklemek *system.net* Bu kod örneğinde gösterildiği bölümü.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="6fe8a-142">Değişiklik *proxyserver:8080* yerel ara sunucu adı veya IP adresi ve başlangıç bağlantı noktası üzerinde dinleme yaptığı tooreflect.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="6fe8a-143">Ardından, C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı Updater\ApplicationProxyConnectorUpdaterService.exe.config bulunan benzer bir değişiklik toohello dosyasını yaparak hello Connector Updater hizmet toouse hello proxy yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="6fe8a-144">2. adım: hello bağlayıcı ve ilgili hizmetler tooflow aracılığıyla hello proxy tooallow trafiği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fe8a-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="6fe8a-145">Merhaba giden proxy dört yönlerini tooconsider vardır:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="6fe8a-146">Proxy giden kuralları</span><span class="sxs-lookup"><span data-stu-id="6fe8a-146">Proxy outbound rules</span></span>
* <span data-ttu-id="6fe8a-147">Proxy kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="6fe8a-147">Proxy authentication</span></span>
* <span data-ttu-id="6fe8a-148">Proxy bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="6fe8a-148">Proxy ports</span></span>
* <span data-ttu-id="6fe8a-149">SSL denetleme</span><span class="sxs-lookup"><span data-stu-id="6fe8a-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="6fe8a-150">Proxy giden kuralları</span><span class="sxs-lookup"><span data-stu-id="6fe8a-150">Proxy outbound rules</span></span>
<span data-ttu-id="6fe8a-151">Bağlayıcı hizmeti erişimi için uç noktalar aşağıdaki erişim toohello izin ver:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="6fe8a-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="6fe8a-152">*.msappproxy.net</span></span>
* <span data-ttu-id="6fe8a-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6fe8a-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="6fe8a-154">İlk kaydı için uç noktalar aşağıdaki erişim toohello izin ver:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="6fe8a-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="6fe8a-155">login.windows.net</span></span>
* <span data-ttu-id="6fe8a-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6fe8a-156">login.microsoftonline.com</span></span>

<span data-ttu-id="6fe8a-157">FQDN DEĞERİNE göre bağlantı sağlar ve bunun yerine toospecify IP aralıkları gerekir, bu seçenekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="6fe8a-158">Merhaba bağlayıcı giden erişim tooall hedefleri izin verin.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="6fe8a-159">Merhaba bağlayıcı giden çok erişime[Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6fe8a-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="6fe8a-160">Azure veri merkezi IP aralıkları hello listesini kullanarak ile Merhaba haftalık güncelleştirilmiş iştir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="6fe8a-161">Bir işlemde yer tooensure erişim kuralları buna göre güncelleştirilir tooput gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="6fe8a-162">Proxy kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="6fe8a-162">Proxy authentication</span></span>

<span data-ttu-id="6fe8a-163">Proxy kimlik doğrulaması şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="6fe8a-164">Geçerli Bizim önerimiz tooallow hello bağlayıcı anonim erişim toohello Internet hedefleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="6fe8a-165">Proxy bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="6fe8a-165">Proxy ports</span></span>

<span data-ttu-id="6fe8a-166">Merhaba bağlayıcı hello BAĞLAN yöntemini kullanarak giden SSL tabanlı bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="6fe8a-167">Bu yöntem temelde hello giden proxy üzerinden tünel ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="6fe8a-168">Merhaba proxy sunucu tooallow tooports 443 ve 80 tünel yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="6fe8a-169">Hizmet veri yolu HTTPS üzerinden çalıştığında, 443 numaralı bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="6fe8a-170">Ancak, varsayılan olarak, hizmet veri yolu doğrudan TCP bağlantıları çalışır ve yalnızca doğrudan bağlantı başarısız olursa tooHTTPS geri döner.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="6fe8a-171">Service Bus trafiği de hello giden proxy sunucu üzerinden gönderilen Merhaba, bu hello bağlayıcı doğrudan toohello bağlanamıyor olun tooensure 9350, 9352 ve 5671 bağlantı noktaları için Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="6fe8a-172">SSL denetleme</span><span class="sxs-lookup"><span data-stu-id="6fe8a-172">SSL inspection</span></span>
<span data-ttu-id="6fe8a-173">Hello bağlayıcı trafiği için sorunlara neden olduğu SSL denetlemesi hello bağlayıcı trafiği için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="6fe8a-174">Bağlayıcı proxy sorunları ve hizmet bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6fe8a-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="6fe8a-175">Şimdi hello proxy üzerinden akan tüm trafiği görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="6fe8a-176">Sorunlarınız varsa, sorun giderme bilgileri aşağıdaki hello yardımcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="6fe8a-177">en iyi şekilde tooidentify hello ve bağlayıcı bağlantı sorunlarını giderme sorunları olan bir ağ yakalama hello bağlayıcı hizmetini hello bağlayıcı hizmeti başlatılırken tootake.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="6fe8a-178">Bu zorlu bir görev olabilir, bu nedenle yakalama ve ağ izlemelerini filtreleme hızlı ipuçları bakalım.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="6fe8a-179">İzleme aracı tercih ettiğiniz hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="6fe8a-180">Bu makalede Hello amaçları doğrultusunda, Microsoft Network Monitor 3.4 kullandık.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="6fe8a-181">Yapabilecekleriniz [Microsoft'tan indirmeniz](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="6fe8a-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="6fe8a-182">belirli tooNetwork İzleyicisi Merhaba örnekler ve bölümler aşağıdaki hello kullanırız filtreleri olan ancak hello ilkeleri uygulanan tooany çözümleme aracı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="6fe8a-183">Ağ İzleyicisi'ni kullanarak bir görüntüsü alın</span><span class="sxs-lookup"><span data-stu-id="6fe8a-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="6fe8a-184">bir yakalama toostart:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-184">toostart a capture:</span></span>

1. <span data-ttu-id="6fe8a-185">Ağ İzleyicisi'ni açın ve tıklatın **yeni yakalama**.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="6fe8a-186">Merhaba tıklatın **Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-186">Click hello **Start** button.</span></span>

   ![Ağ İzleyicisi penceresi](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="6fe8a-188">Bir yakalama tamamladıktan sonra hello tıklayın **durdurmak** düğmesini tooend onu.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="6fe8a-189">Bağlayıcı trafik görüntüsü alın</span><span class="sxs-lookup"><span data-stu-id="6fe8a-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="6fe8a-190">İlk sorun giderme için hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="6fe8a-191">Services.msc hello Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini durdurun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="6fe8a-192">Merhaba ağ yakalama başlatın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-192">Start hello network capture.</span></span>
3. <span data-ttu-id="6fe8a-193">Hello Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="6fe8a-194">Merhaba ağ yakalama işlemini durdurun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-194">Stop hello network capture.</span></span>

   ![Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetinde](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="6fe8a-196">Merhaba isteklerinin hello bağlayıcı toohello proxy sunucusundan arayın</span><span class="sxs-lookup"><span data-stu-id="6fe8a-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="6fe8a-197">Bir ağ yakalama olduğuna göre hazır toofilter demektir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="6fe8a-198">Merhaba anahtar toolooking hello izleme sırasında nasıl toofilter hello yakalama anlamaktır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="6fe8a-199">Bir filtre (8080 hello proxy hizmet bağlantı noktası olduğu) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="6fe8a-200">**(http. İstek veya http. Yanıt) ve tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="6fe8a-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="6fe8a-201">Bu filtre hello girerseniz, **görüntüleme filtresi** penceresini açın ve select **Uygula**, yakalanan hello trafiği hello filtreye bağlı filtreler.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="6fe8a-202">Merhaba önceki filtre yalnızca hello HTTP istekleri ve yanıtları hello proxy bağlantı noktası/gruptan gösterir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="6fe8a-203">Merhaba bağlayıcı yapılandırılmış toouse bir proxy sunucusu olduğu bir bağlayıcı başlatma için hello filtresi şöyle bir şey gösterir:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Filtrelenmiş HTTP istekleri ve yanıtları örnek listesi](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="6fe8a-205">Şimdi özellikle hello proxy sunucusu ile iletişim gösterin BAĞLAN istekleri hello aradığınız.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="6fe8a-206">Başarı bir HTTP Tamam (200) yanıt alın.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="6fe8a-207">407 veya 502, gibi diğer yanıt kodlarını görürseniz hello proxy kimlik doğrulaması gerektiren veya başka bir nedenle hello trafiğe izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="6fe8a-208">Bu noktada, proxy sunucusu destek ekibinize göster.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="6fe8a-209">TCP bağlantı girişimleri başarısız tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6fe8a-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="6fe8a-210">Merhaba ilginizi çekebilir diğer yaygın bir senaryo hello bağlayıcı tooconnect doğrudan çalışıyor, ancak başarısız olduğu durumdur.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="6fe8a-211">Bu sorunu belirlemeye tooeasily yardımcı olan başka bir Ağ İzleyicisi filtredir:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="6fe8a-212">**özellik. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="6fe8a-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="6fe8a-213">Eşitlemeye paket hello ilk paket tooestablish bir TCP bağlantı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="6fe8a-214">Bu paket yanıt döndürmezse hello Eşitlemeye reattempted.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="6fe8a-215">Merhaba filtre toosee önceki tüm yeniden iletilen SYN isteklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="6fe8a-216">Ardından, bu SYN isteklerini tooany Bağlayıcısı ilgili trafik karşılık olup olmadığını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="6fe8a-217">Merhaba aşağıdaki örnek başarısız bağlantı denemesi tooService veri yolu bağlantı noktası 9352 gösterir:</span><span class="sxs-lookup"><span data-stu-id="6fe8a-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Başarısız bağlantı denemesi için örnek yanıt](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="6fe8a-219">Yanıt önceki hello gibi bir şey görürseniz, hello bağlayıcı hello Azure Service Bus hizmeti ile doğrudan toocommunicate çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="6fe8a-220">Merhaba bağlayıcı toomake doğrudan bağlantılar toohello Azure beklediğiniz, hizmetleri, bu yanıt olan bir ağ veya güvenlik duvarı sorunu olduğunu NET bir belirti.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="6fe8a-221">Yapılandırılmış toouse bir proxy sunucusu varsa, bu yanıt Service Bus tooattempting bağlantı HTTPS üzerinden geçmeden önce doğrudan bir TCP bağlantı çalışıyor anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="6fe8a-222">Ağ izleme çözümleme herkes için değil.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="6fe8a-223">Ancak, ağ ile neler olduğunu bir hakkında değerli bir araç tooget hızlı bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="6fe8a-224">Bağlayıcı bağlantı sorunları ile toostruggle devam ederseniz, bir bilet destek ekibimiz ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="6fe8a-225">Merhaba takım daha fazla sorun giderme konusunda yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6fe8a-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="6fe8a-226">Uygulama Ara sunucusu Bağlayıcısı ile hataları çözümleme hakkında daha fazla bilgi için bkz: [sorun giderme uygulaması proxy'si](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="6fe8a-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fe8a-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6fe8a-227">Next steps</span></span>

[<span data-ttu-id="6fe8a-228">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="6fe8a-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="6fe8a-229">
[Nasıl toosilently yükleme hello Azure AD uygulama ara sunucusu Bağlayıcısı](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="6fe8a-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
