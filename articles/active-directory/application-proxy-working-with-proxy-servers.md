---
title: "Var olan iş şirket içi proxy sunucuları ve Azure AD | Microsoft Docs"
description: "Mevcut şirket içi proxy sunucularıyla çalışacak şekilde nasıl ele alınmaktadır."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="5eb4a-103">Mevcut şirket içi proxy sunucuları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="5eb4a-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="5eb4a-104">Bu makalede, giden proxy sunucuları ile çalışmak için Azure Active Directory (Azure AD) uygulama proxy'si bağlayıcıları yapılandırın açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="5eb4a-105">Varolan proxy'leri sahip ağ ortamları olan müşteriler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="5eb4a-106">Bu ana dağıtım senaryolarında bakarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="5eb4a-107">Şirket içi giden proxy atlama için bağlayıcıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="5eb4a-108">Azure AD uygulama proxy'si erişmek için bir giden proxy kullanmak için bağlayıcıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="5eb4a-109">Bağlayıcıları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="5eb4a-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="5eb4a-110">Giden proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="5eb4a-110">Configure the outbound proxy</span></span>

<span data-ttu-id="5eb4a-111">Ortamınızda bir giden proxy varsa, bir hesap uygun izinlere sahip giden proxy yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="5eb4a-112">Yükleyici yüklemeyi yapan kullanıcının bağlamında çalıştığından, Microsoft Edge veya başka bir Internet tarayıcısı kullanarak yapılandırmasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="5eb4a-113">Microsoft Edge'de proxy ayarlarını yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="5eb4a-114">Git **ayarları** > **görünüm Gelişmiş ayarları** > **Proxy ayarları** > **el ile Proxy Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="5eb4a-115">Ayarlama **bir proxy sunucu kullanacak** için **üzerinde**seçin **(intranet) yerel adresler için proxy sunucusu kullanma** onay kutusunu işaretleyin ve ardından adresi ve bağlantı noktası yerel yansıtacak şekilde değiştirin proxy sunucusu.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="5eb4a-116">Gerekli proxy ayarlarını doldurun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-116">Fill in the necessary proxy settings.</span></span>

   ![Proxy ayarları iletişim kutusu](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="5eb4a-118">Giden proxy atlama</span><span class="sxs-lookup"><span data-stu-id="5eb4a-118">Bypass outbound proxies</span></span>

<span data-ttu-id="5eb4a-119">Bağlayıcılar giden isteklerde temel işletim sistemi bileşeni vardır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="5eb4a-120">Bu bileşenleri otomatik olarak ağ üzerinde bir proxy sunucu bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="5eb4a-121">Ortamında etkinleştirilirse Web Proxy Otomatik Bulma (WPAD) kullanırlar.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="5eb4a-122">İşletim sistemi bileşenlerini wpad.domainsuffix için DNS araması gerçekleştirerek bir proxy sunucu bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="5eb4a-123">Bu DNS çözümlenirse, bir HTTP isteği wpad.dat için IP adresi için yapılır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="5eb4a-124">Bu istek proxy yapılandırması komut dosyası, ortamınızdaki olur.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="5eb4a-125">Bağlayıcı, bir giden proxy sunucusu seçmek için bu komut dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="5eb4a-126">Ancak, bağlayıcı trafiği hala aracılığıyla, proxy gereken ek yapılandırma ayarları nedeniyle geçebilir değil.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="5eb4a-127">Azure hizmetlerine doğrudan bağlantı kullandığından emin olmak için şirket içi proxy atlama bağlayıcıyı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="5eb4a-128">Bu yaklaşım (ağ ilkeniz için izin veriyorsa) öneririz, çünkü korumak için daha az bir yapılandırmaya sahip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="5eb4a-129">Bağlayıcı için giden proxy kullanımını devre dışı bırakmak için C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve ekleme *system.net* Bu kod örneğinde gösterildiği bölümü:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="5eb4a-130">Bağlayıcı güncelleştirici hizmetini de proxy atladığı emin olmak için benzer C:\Program Files\Microsoft AAD uygulama Proxy Connector Updater bulunan ApplicationProxyConnectorUpdaterService.exe.config dosyasını değişiklik.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="5eb4a-131">Varsayılan .config dosyaları geri gerekebileceği özgün dosyaların kopyalarını yaptığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="5eb4a-132">Giden proxy sunucusu kullan</span><span class="sxs-lookup"><span data-stu-id="5eb4a-132">Use the outbound proxy server</span></span>

<span data-ttu-id="5eb4a-133">Bazı ortamlar özel durum olmadan bir giden proxy gitmesi tüm giden trafiği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="5eb4a-134">Sonuç olarak, proxy atlama bir seçenek değil.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="5eb4a-135">Aşağıdaki çizimde gösterildiği gibi giden proxy üzerinden gitmek için bağlayıcı trafiğini yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Azure AD uygulama proxy'si giden bir proxy üzerinden gitmek için trafiği bağlayıcı yapılandırma](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="5eb4a-137">Yalnızca giden trafiğe sahip sonucu olarak, güvenlik duvarı üzerinden gelen erişimi yapılandırmak için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="5eb4a-138">Adım 1: giden proxy üzerinden gitmek için ilgili hizmetler ve bağlayıcı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5eb4a-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="5eb4a-139">WPAD ortamda etkin ve uygun şekilde yapılandırılmış varsa daha önce anlatıldığı gibi bağlayıcı otomatik olarak giden proxy sunucusunu bulmak ve bunu kullanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="5eb4a-140">Ancak, bir giden proxy üzerinden gitmek için bağlayıcı açıkça yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="5eb4a-141">Bunu yapmak için C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve ekleme *system.net* Bu kod örneğinde gösterildiği bölümü.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="5eb4a-142">Değişiklik *proxyserver:8080* yerel proxy sunucunuzun adını veya IP adresi ve üzerinde dinleme bağlantı noktasını yansıtmak için.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="5eb4a-143">Ardından, bağlayıcı güncelleştirici hizmetini C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı Updater\ApplicationProxyConnectorUpdaterService.exe.config bulunan dosyasına benzer bir değişiklik yapılarak proxy kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="5eb4a-144">Adım 2: proxy Bağlayıcısı ve ilgili hizmetler akışına trafiğe izin verecek şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5eb4a-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="5eb4a-145">Giden proxy dikkate alınması gereken dört nokta vardır:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="5eb4a-146">Proxy giden kuralları</span><span class="sxs-lookup"><span data-stu-id="5eb4a-146">Proxy outbound rules</span></span>
* <span data-ttu-id="5eb4a-147">Proxy kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5eb4a-147">Proxy authentication</span></span>
* <span data-ttu-id="5eb4a-148">Proxy bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="5eb4a-148">Proxy ports</span></span>
* <span data-ttu-id="5eb4a-149">SSL denetleme</span><span class="sxs-lookup"><span data-stu-id="5eb4a-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="5eb4a-150">Proxy giden kuralları</span><span class="sxs-lookup"><span data-stu-id="5eb4a-150">Proxy outbound rules</span></span>
<span data-ttu-id="5eb4a-151">Bağlayıcı hizmeti erişim şu uç noktalar için erişim izni ver:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="5eb4a-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="5eb4a-152">*.msappproxy.net</span></span>
* <span data-ttu-id="5eb4a-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="5eb4a-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="5eb4a-154">İlk kayıt için aşağıdaki uç noktalarına erişime izin ver:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="5eb4a-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="5eb4a-155">login.windows.net</span></span>
* <span data-ttu-id="5eb4a-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="5eb4a-156">login.microsoftonline.com</span></span>

<span data-ttu-id="5eb4a-157">FQDN DEĞERİNE göre bağlantı sağlar ve bunun yerine IP aralıklarını belirtmeniz gerekir, bu seçenekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="5eb4a-158">Tüm hedefler bağlayıcı giden erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="5eb4a-159">Bağlayıcı giden erişmesine izin vermek [Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="5eb4a-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="5eb4a-160">Azure veri merkezi IP aralıkları listesi kullanarak haftalık güncelleştirilmiş iştir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="5eb4a-161">Bir işlem, erişim kuralları buna göre güncelleştirilir emin olmak için yerleştirdiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="5eb4a-162">Proxy kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5eb4a-162">Proxy authentication</span></span>

<span data-ttu-id="5eb4a-163">Proxy kimlik doğrulaması şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="5eb4a-164">Bizim geçerli Internet hedeflere bağlayıcı anonim erişime izin vermek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="5eb4a-165">Proxy bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="5eb4a-165">Proxy ports</span></span>

<span data-ttu-id="5eb4a-166">Bağlayıcı BAĞLAN yöntemini kullanarak giden SSL tabanlı bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="5eb4a-167">Bu yöntem temelde giden proxy üzerinden tünel ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="5eb4a-168">Bağlantı noktaları için 443 ve 80 tünel izin vermek için proxy sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="5eb4a-169">Hizmet veri yolu HTTPS üzerinden çalıştığında, 443 numaralı bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="5eb4a-170">Ancak, varsayılan olarak, hizmet veri yolu doğrudan TCP bağlantıları çalışır ve yalnızca doğrudan bağlantı başarısız olursa HTTPS'ye geri döner.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="5eb4a-171">Hizmet veri yolu trafiği de giden proxy sunucu üzerinden gönderilen emin olmak için bağlayıcı 9350, 9352 ve 5671 bağlantı noktaları için Azure hizmetlerine doğrudan bağlanamıyor emin olun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="5eb4a-172">SSL denetleme</span><span class="sxs-lookup"><span data-stu-id="5eb4a-172">SSL inspection</span></span>
<span data-ttu-id="5eb4a-173">Bağlayıcı trafiği için sorunlara neden olduğu SSL denetleme bağlayıcı trafiği için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="5eb4a-174">Bağlayıcı proxy sorunları ve hizmet bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="5eb4a-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="5eb4a-175">Şimdi proxy akan tüm trafiği görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="5eb4a-176">Sorunlarınız varsa, aşağıdaki sorun giderme bilgileri yardımcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="5eb4a-177">Tanımlamak ve bağlayıcı bağlantı sorunlarını gidermek için en iyi yolu bir ağ yakalama bağlayıcı hizmetini bağlayıcı hizmeti başlatılırken almaktır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="5eb4a-178">Bu zorlu bir görev olabilir, bu nedenle yakalama ve ağ izlemelerini filtreleme hızlı ipuçları bakalım.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="5eb4a-179">Tercih ettiğiniz izleme aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="5eb4a-180">Bu makalede amaçları doğrultusunda, Microsoft Network Monitor 3.4 kullandık.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="5eb4a-181">Yapabilecekleriniz [Microsoft'tan indirmeniz](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="5eb4a-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="5eb4a-182">Aşağıdaki bölümlerde kullanırız filtreleri ve örnekler Ağ İzleyicisi belirli, ancak herhangi bir analiz aracı ilkeleri uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="5eb4a-183">Ağ İzleyicisi'ni kullanarak bir görüntüsü alın</span><span class="sxs-lookup"><span data-stu-id="5eb4a-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="5eb4a-184">Bir yakalama başlatmak için:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-184">To start a capture:</span></span>

1. <span data-ttu-id="5eb4a-185">Ağ İzleyicisi'ni açın ve tıklatın **yeni yakalama**.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="5eb4a-186">Tıklatın **Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-186">Click the **Start** button.</span></span>

   ![Ağ İzleyicisi penceresi](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="5eb4a-188">Bir yakalama tamamladıktan sonra tıklayın **durdurmak** onu sonuna düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="5eb4a-189">Bağlayıcı trafik görüntüsü alın</span><span class="sxs-lookup"><span data-stu-id="5eb4a-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="5eb4a-190">İlk sorun giderme için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="5eb4a-191">Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini durdurun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="5eb4a-192">Ağ Yakalama başlatın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-192">Start the network capture.</span></span>
3. <span data-ttu-id="5eb4a-193">Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="5eb4a-194">Ağ yakalama işlemini durdurun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-194">Stop the network capture.</span></span>

   ![Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetinde](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="5eb4a-196">Proxy sunucusuna bir bağlayıcı isteklerinin arayın</span><span class="sxs-lookup"><span data-stu-id="5eb4a-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="5eb4a-197">Bir ağ yakalama olduğuna göre onu filtrelemek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="5eb4a-198">İzleme sırasında arayan anahtarını yakalama filtreleme anlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="5eb4a-199">Bir filtre (8080 proxy hizmet bağlantı noktası olduğu) aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="5eb4a-200">**(http. İstek veya http. Yanıt) ve tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="5eb4a-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="5eb4a-201">Bu filtre girerseniz, **görüntüleme filtresi** penceresini açın ve select **Uygula**, filtreye bağlı yakalanan trafik filtreleri.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="5eb4a-202">Önceki filtresinin denetleyicisinden proxy bağlantı noktası yalnızca HTTP istekleri ve yanıtları gösterir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="5eb4a-203">Bağlayıcı bir proxy sunucu kullanmak için yapılandırıldığı bağlayıcı başlangıç filtresi şöyle bir şey gösterir:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Filtrelenmiş HTTP istekleri ve yanıtları örnek listesi](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="5eb4a-205">Şimdi özellikle proxy sunucusu ile iletişim Göster CONNECT isteklerini aradığınız.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="5eb4a-206">Başarı bir HTTP Tamam (200) yanıt alın.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="5eb4a-207">407 veya 502, gibi diğer yanıt kodlarını görürseniz proxy kimlik doğrulaması gerektiren veya başka bir nedenle trafiğe izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="5eb4a-208">Bu noktada, proxy sunucusu destek ekibinize göster.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="5eb4a-209">TCP bağlantı girişimleri başarısız tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5eb4a-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="5eb4a-210">İlginizi çekebilir bir ortak senaryoyu bağlayıcıyı doğrudan bağlanmak çalışıyor, ancak başarısız olduğu durumdur.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="5eb4a-211">Bu sorunu kolayca tanımlamaya yardımcı olan başka bir Ağ İzleyicisi filtredir:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="5eb4a-212">**özellik. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="5eb4a-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="5eb4a-213">Bir TCP bağlantı kurmak üzere gönderilen ilk paket Eşitlemeye pakettir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="5eb4a-214">Bu paket yanıt döndürmezse Eşitlemeye reattempted.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="5eb4a-215">Yeniden aktarılan tüm SYN isteklerini görmek için yukarıdaki filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="5eb4a-216">Ardından, bu SYN istekleri Bağlayıcısı ile ilgili tüm trafik için karşılık gelen olup olmadığını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="5eb4a-217">Aşağıdaki örnek, 9352 adlı hizmet veri yolu bağlantı başarısız bağlantı girişimi gösterir:</span><span class="sxs-lookup"><span data-stu-id="5eb4a-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Başarısız bağlantı denemesi için örnek yanıt](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="5eb4a-219">Önceki yanıt şöyle görürseniz, bağlayıcı doğrudan Azure Service Bus hizmeti ile iletişim kurmaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="5eb4a-220">Azure hizmetlerine doğrudan bağlantı bağlayıcı bekliyorsanız, bu yanıt, bir ağ veya güvenlik duvarı sorunu olduğunu NET bir belirti ' dir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="5eb4a-221">Bir proxy sunucu kullanacak şekilde yapılandırıldıysa, bu yanıt hizmet veri yolu bağlantı HTTPS üzerinden çalışıyor geçmeden önce doğrudan bir TCP bağlantı çalışıyor anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="5eb4a-222">Ağ izleme çözümleme herkes için değil.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="5eb4a-223">Ancak, ağ ile neler olup bittiğini hakkında hızlı bilgi almak için değerli bir araç olabilir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="5eb4a-224">Bağlayıcı bağlantı sorunları güçlük Devam ederseniz, bir bilet destek ekibimiz ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="5eb4a-225">Takım daha fazla sorun giderme konusunda yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5eb4a-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="5eb4a-226">Uygulama Ara sunucusu Bağlayıcısı ile hataları çözümleme hakkında daha fazla bilgi için bkz: [sorun giderme uygulaması proxy'si](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="5eb4a-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eb4a-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5eb4a-227">Next steps</span></span>

[<span data-ttu-id="5eb4a-228">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="5eb4a-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="5eb4a-229">
[Azure AD uygulama ara sunucusu Bağlayıcısı sessiz yükleme](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="5eb4a-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
