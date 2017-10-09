---
title: "aaaConfigure SSL bağlantısı PostgreSQL için Azure veritabanı'nda | Microsoft Docs"
description: "Yönergeler ve bilgi tooconfigure Azure veritabanı PostgreSQL ve ilişkili uygulamalar tooproperly için SSL bağlantılarını kullanın."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="9430f-103">SSL bağlantısı Azure veritabanı'nda PostgreSQL için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9430f-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="9430f-104">Azure veritabanı PostgreSQL için istemci uygulamaları toohello PostgreSQL hizmetini Güvenli Yuva Katmanı (SSL) kullanarak bağlanma tercih eder.</span><span class="sxs-lookup"><span data-stu-id="9430f-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="9430f-105">Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="9430f-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="9430f-106">Varsayılan olarak, PostgreSQL veritabanı hizmeti hello yapılandırılmış toorequire SSL bağlantı olur.</span><span class="sxs-lookup"><span data-stu-id="9430f-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="9430f-107">İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa tooyour veritabanı hizmeti bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9430f-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="9430f-108">SSL bağlantıları zorlama</span><span class="sxs-lookup"><span data-stu-id="9430f-108">Enforcing SSL connections</span></span>
<span data-ttu-id="9430f-109">Sağlanan hello Azure portal ve CLI PostgreSQL sunucuları için tüm Azure veritabanı için SSL bağlantılarını zorlama varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="9430f-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="9430f-110">Benzer şekilde, SSL kullanarak yaygın diller tooconnect tooyour veritabanı sunucusu için gerekli hello parametreleri sunucunuz hello Azure portal'ın altındaki hello "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9430f-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="9430f-111">Merhaba SSL parametre göre hello bağlayıcı, örneğin değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.</span><span class="sxs-lookup"><span data-stu-id="9430f-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="9430f-112">SSL zorlama yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9430f-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="9430f-113">İsteğe bağlı olarak zorunlu SSL bağlantısını devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9430f-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="9430f-114">Microsoft Azure önerir tooalways etkinleştirmek **Zorla SSL bağlantısı** için Gelişmiş güvenlik ayarı.</span><span class="sxs-lookup"><span data-stu-id="9430f-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="9430f-115">Hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="9430f-115">Using hello Azure portal</span></span>
<span data-ttu-id="9430f-116">Azure veritabanınız PostgreSQL sunucu için ziyaret edin ve tıklatın **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="9430f-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="9430f-117">Merhaba iki durumlu düğme tooenable kullanın veya hello devre dışı bırakma **Zorla SSL bağlantısı** ayarı.</span><span class="sxs-lookup"><span data-stu-id="9430f-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="9430f-118">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9430f-118">Then click **Save**.</span></span> 

![Bağlantı güvenliği - devre dışı bırak SSL zorla](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="9430f-120">Merhaba ayarı hello görüntüleyerek onaylayabilirsiniz **genel bakış** sayfa toosee hello **SSL zorlama durumu** göstergesi.</span><span class="sxs-lookup"><span data-stu-id="9430f-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="9430f-121">Azure CLI’yı kullanma</span><span class="sxs-lookup"><span data-stu-id="9430f-121">Using Azure CLI</span></span>
<span data-ttu-id="9430f-122">Etkinleştirmek veya devre dışı hello **ssl zorlama** parametresini kullanarak `Enabled` veya `Disabled` Azure CLI sırasıyla değerleri.</span><span class="sxs-lookup"><span data-stu-id="9430f-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="9430f-123">Uygulama veya framework destekler, SSL bağlantılarını emin olun</span><span class="sxs-lookup"><span data-stu-id="9430f-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="9430f-124">Veritabanı Hizmetleri, Drupal ve Django gibi PostgreSQL kullanmak birçok yaygın uygulama çerçeveleri SSL yüklemesi sırasında varsayılan olarak etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="9430f-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="9430f-125">SSL bağlantısı etkinleştirme yüklemeden sonra veya CLI komutları belirli toohello uygulaması aracılığıyla yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9430f-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="9430f-126">PostgreSQL sunucunuz SSL bağlantılarını zorlama ve ilişkili hello uygulama düzgün yapılandırılmamış, Merhaba uygulaması tooconnect tooyour veritabanı sunucusu başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="9430f-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="9430f-127">Uygulamanızın belgelerine toolearn nasıl başvurun tooenable SSL bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="9430f-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="9430f-128">Sertifika doğrulaması için SSL bağlantısı gerektiren uygulamalar</span><span class="sxs-lookup"><span data-stu-id="9430f-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="9430f-129">Bazı durumlarda, uygulamaların güvenilen bir sertifika yetkilisi (CA) sertifika dosyasını (.cer) tooconnect güvenli bir şekilde oluşturulan bir yerel sertifika dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9430f-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="9430f-130">Merhaba aşağıdaki adımları tooobtain hello .cer dosyasına bakın, kod çözme hello sertifikası ve tooyour uygulama bağlayın.</span><span class="sxs-lookup"><span data-stu-id="9430f-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="9430f-131">Sertifika yetkilisi (CA) hello Hello sertifika dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="9430f-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="9430f-132">PostgreSQL server bulunduğu için hello sertifikası toocommunicate Azure veritabanınızla SSL üzerinden gerekli [burada](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="9430f-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="9430f-133">Merhaba sertifika dosyasını yerel olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9430f-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="9430f-134">OpenSSL makinenize yükleyip</span><span class="sxs-lookup"><span data-stu-id="9430f-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="9430f-135">Uygulama tooconnect için güvenli bir şekilde gerekli toodecode hello sertifika dosyası tooyour veritabanı sunucusu, yerel bilgisayarınızda tooinstall OpenSSL gerekir.</span><span class="sxs-lookup"><span data-stu-id="9430f-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="9430f-136">Linux, OS X veya Unix için</span><span class="sxs-lookup"><span data-stu-id="9430f-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="9430f-137">Merhaba OpenSSL kitaplıkları hello doğrudan kaynak kodunda sağlanır [OpenSSL yazılım Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="9430f-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="9430f-138">Merhaba aşağıdaki yönergeler size hello adımları gerekli tooinstall OpenSSL Linux Bilgisayarınızda yol.</span><span class="sxs-lookup"><span data-stu-id="9430f-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="9430f-139">Bu makalede toowork Ubuntu 12.04 ve daha yüksek bilinen komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="9430f-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="9430f-140">Bir terminal oturumu açın ve OpenSSL yükleyin</span><span class="sxs-lookup"><span data-stu-id="9430f-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="9430f-141">Merhaba yükleme paketinden Hello dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="9430f-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="9430f-142">Merhaba dosyalarını ayıkladığınız Hello dizini girin.</span><span class="sxs-lookup"><span data-stu-id="9430f-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="9430f-143">Varsayılan olarak, aşağıdaki gibi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9430f-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="9430f-144">OpenSSL komutu aşağıdaki hello yürüterek yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9430f-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="9430f-145">Merhaba dosyaları bir klasör içinde /usr/local/openssl farklı istiyorsanız emin toochange hello aşağıdaki uygun şekilde olun.</span><span class="sxs-lookup"><span data-stu-id="9430f-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="9430f-146">OpenSSL'ın düzgün yapılandırıldığından, toocompile gerekir, tooconvert sertifikanızı.</span><span class="sxs-lookup"><span data-stu-id="9430f-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="9430f-147">toocompile, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9430f-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="9430f-148">Derleme işlemi tamamlandıktan sonra hazır tooinstall OpenSSL bir yürütülebilir dosya hello aşağıdaki komutu çalıştırarak demektir:</span><span class="sxs-lookup"><span data-stu-id="9430f-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="9430f-149">tooconfirm, sisteminizde OpenSSL başarıyla yükledikten çalışma hello aşağıdaki komut ve toomake hello alma emin denetleyin aynı çıktı.</span><span class="sxs-lookup"><span data-stu-id="9430f-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="9430f-150">Başarılı olursa iletiden hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9430f-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="9430f-151">Windows için</span><span class="sxs-lookup"><span data-stu-id="9430f-151">For Windows</span></span>
<span data-ttu-id="9430f-152">Bir Windows Bilgisayarına OpenSSL yükleme yolu izleyerek hello yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="9430f-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="9430f-153">**(Önerilen)**  Kullanarak hello yerleşik Windows için Bash işlevini penceresi 10 ve üzeri sürümlerde, OpenSSL varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9430f-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="9430f-154">Windows 10 için Windows Bash işlevi tooenable nasıl bulunabilir yönergeleri [burada](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="9430f-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="9430f-155">Merhaba topluluk tarafından sağlanan bir Win32/64 uygulama indiriliyor aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="9430f-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="9430f-156">Merhaba OpenSSL yazılım Foundation sağlamaz veya herhangi belirli Windows Installer'lar onaylamaz olsa da, kullanılabilir yükleyicileri listesini sağladıkları [burada](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="9430f-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="9430f-157">Sertifika dosyanızın kod çözme</span><span class="sxs-lookup"><span data-stu-id="9430f-157">Decode your certificate file</span></span>
<span data-ttu-id="9430f-158">Merhaba kök CA'ın şifreli biçimde dosyasıdır indirilir.</span><span class="sxs-lookup"><span data-stu-id="9430f-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="9430f-159">OpenSSL toodecode hello sertifika dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="9430f-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="9430f-160">toodo, bu nedenle, bu OpenSSL komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9430f-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="9430f-161">SSL sertifika kimlik doğrulaması ile bağlanan tooAzure PostgreSQL için veritabanı</span><span class="sxs-lookup"><span data-stu-id="9430f-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="9430f-162">Sertifikanızı başarıyla kodunu çözdü olduğunuza göre şimdi tooyour veritabanı sunucusu güvenli bir şekilde SSL üzerinden bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9430f-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="9430f-163">tooallow sunucu sertifika doğrulaması hello sertifika hello dosya ~/.postgresql/root.crt hello kullanıcının giriş dizini içinde yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9430f-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="9430f-164">(Microsoft Windows hello dosyada % APPDATA%\postgresql\root.crt olarak adlandırılır.).</span><span class="sxs-lookup"><span data-stu-id="9430f-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="9430f-165">Merhaba aşağıdaki tooAzure veritabanı için PostgreSQL bağlama yönergeleri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="9430f-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="9430f-166">Şu anda olduğunda bir bilinen sorun kullanırsanız "sslmode doğrulayın tam =" bağlantı toohello hizmetinde hello bağlantı hello aşağıdaki hata ile başarısız olur: _için sunucu sertifikası "&lt;bölge&gt;. Control.Database.Windows.NET"(ve diğer adları 7) ana bilgisayar adı eşleşmiyor"&lt;servername&gt;. postgres.database.azure.com "._</span><span class="sxs-lookup"><span data-stu-id="9430f-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="9430f-167">Varsa "sslmode doğrulayın tam =" olan gerekli, lütfen hello sunucu adlandırma kuralını kullanın  **&lt;servername&gt;. database.windows.net** , bağlantı dizesi ana bilgisayar adı olarak.</span><span class="sxs-lookup"><span data-stu-id="9430f-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="9430f-168">Biz bu sınırlamaya hello gelecekteki içinde tooremove planlayın.</span><span class="sxs-lookup"><span data-stu-id="9430f-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="9430f-169">Diğer kullanarak bağlantı [SSL modları](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) toouse hello tercih edilen konak adlandırma kuralı devam etmesi gerektiğini  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="9430f-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="9430f-170">Psql komut satırı yardımcı programını kullanma</span><span class="sxs-lookup"><span data-stu-id="9430f-170">Using psql command-line utility</span></span>
<span data-ttu-id="9430f-171">Aşağıdaki örnek hello toosuccessfully tooyour PostgreSQL sunucusunu hello psql komut satırı yardımcı programını kullanarak nasıl bağlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9430f-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="9430f-172">Kullanım hello `root.crt` oluşturulan dosya ve hello `sslmode=verify-ca` veya `sslmode=verify-full` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="9430f-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="9430f-173">Merhaba PostgreSQL komut satırı arabirimi kullanarak, hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="9430f-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="9430f-174">Başarılı olursa, çıktı aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="9430f-174">If successful, you receive hello following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="9430f-175">PgAdmin GUI aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="9430f-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="9430f-176">PgAdmin 4 tooconnect SSL üzerinden güvenli bir şekilde yapılandırma gerektirir, tooset hello `SSL mode = Verify-CA` veya `SSL mode = Verify-Full` gibi:</span><span class="sxs-lookup"><span data-stu-id="9430f-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Ekran görüntüsü - bağlantı - pgAdmin SSL modu gerektirir](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="9430f-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9430f-178">Next steps</span></span>
<span data-ttu-id="9430f-179">Aşağıdaki çeşitli uygulama bağlantı seçenekleri gözden [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9430f-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
