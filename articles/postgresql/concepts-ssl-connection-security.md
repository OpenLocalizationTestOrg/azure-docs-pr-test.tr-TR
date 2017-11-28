---
title: "SSL bağlantısı Azure veritabanı'nda PostgreSQL için yapılandırma | Microsoft Docs"
description: "Yönergeleri ve bilgileri Azure veritabanı PostgreSQL ve düzgün şekilde SSL bağlantılarını kullanmak için ilişkili uygulamalar için yapılandırılır."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="059d3-103">SSL bağlantısı Azure veritabanı'nda PostgreSQL için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="059d3-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="059d3-104">Azure veritabanı PostgreSQL için istemci uygulamalarınızı Güvenli Yuva Katmanı (SSL) kullanarak PostgreSQL hizmetine bağlanma tercih eder.</span><span class="sxs-lookup"><span data-stu-id="059d3-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="059d3-105">Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "ortadaki adam" saldırılarına karşı uygulamanız ile sunucu arasındaki veri akışını şifreleyerek korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="059d3-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="059d3-106">Varsayılan olarak, PostgreSQL veritabanı hizmeti bir SSL bağlantısı gerektiren yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="059d3-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="059d3-107">İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa, veritabanı hizmete bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059d3-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="059d3-108">SSL bağlantıları zorlama</span><span class="sxs-lookup"><span data-stu-id="059d3-108">Enforcing SSL connections</span></span>
<span data-ttu-id="059d3-109">CLI ve Azure portalı sağlanan PostgreSQL sunucuları için tüm Azure veritabanı için SSL bağlantılarını zorlama varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="059d3-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="059d3-110">Benzer şekilde, SSL kullanarak, veritabanı sunucunuza bağlanmak yaygın diller için gerekli parametreler sunucunuz Azure portalında altındaki "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="059d3-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="059d3-111">SSL parametre örneğin bağlayıcı göre değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.</span><span class="sxs-lookup"><span data-stu-id="059d3-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="059d3-112">SSL zorlama yapılandırın</span><span class="sxs-lookup"><span data-stu-id="059d3-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="059d3-113">İsteğe bağlı olarak zorunlu SSL bağlantısını devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059d3-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="059d3-114">Microsoft Azure önerir her zaman etkinleştirmek için **Zorla SSL bağlantısı** için Gelişmiş güvenlik ayarı.</span><span class="sxs-lookup"><span data-stu-id="059d3-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="059d3-115">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="059d3-115">Using the Azure portal</span></span>
<span data-ttu-id="059d3-116">Azure veritabanınız PostgreSQL sunucu için ziyaret edin ve tıklatın **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="059d3-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="059d3-117">Etkinleştirmek veya devre dışı bırakmak için iki durumlu düğme kullanmak **Zorla SSL bağlantısı** ayarı.</span><span class="sxs-lookup"><span data-stu-id="059d3-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="059d3-118">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="059d3-118">Then click **Save**.</span></span> 

![Bağlantı güvenliği - devre dışı bırak SSL zorla](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="059d3-120">Ayar görüntüleyerek onaylayabilirsiniz **genel bakış** görmek için sayfayı **SSL zorlama durumu** göstergesi.</span><span class="sxs-lookup"><span data-stu-id="059d3-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="059d3-121">Azure CLI’yı kullanma</span><span class="sxs-lookup"><span data-stu-id="059d3-121">Using Azure CLI</span></span>
<span data-ttu-id="059d3-122">Etkinleştirmek veya devre dışı bırakabileceğiniz **ssl zorlama** parametresini kullanarak `Enabled` veya `Disabled` Azure CLI sırasıyla değerleri.</span><span class="sxs-lookup"><span data-stu-id="059d3-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="059d3-123">Uygulama veya framework destekler, SSL bağlantılarını emin olun</span><span class="sxs-lookup"><span data-stu-id="059d3-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="059d3-124">Veritabanı Hizmetleri, Drupal ve Django gibi PostgreSQL kullanmak birçok yaygın uygulama çerçeveleri SSL yüklemesi sırasında varsayılan olarak etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="059d3-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="059d3-125">SSL bağlantısı etkinleştirme yüklemeden sonra veya uygulamaya özgü CLI komutları aracılığıyla yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="059d3-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="059d3-126">PostgreSQL sunucunuz SSL bağlantılarını zorlama ve ilişkili uygulama düzgün yapılandırılmamış, uygulama, veritabanı sunucunuza bağlanmaya başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="059d3-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="059d3-127">SSL bağlantıları etkinleştirme hakkında bilgi edinmek için uygulamanızın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="059d3-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="059d3-128">Sertifika doğrulaması için SSL bağlantısı gerektiren uygulamalar</span><span class="sxs-lookup"><span data-stu-id="059d3-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="059d3-129">Bazı durumlarda, uygulamaları güvenli bir şekilde bağlanmak için bir güvenilen sertifika yetkilisi (CA) sertifika dosyasından (.cer) oluşturulan bir yerel sertifika dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="059d3-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="059d3-130">.Cer dosyasını edinme, kod çözme sertifikası ve uygulamanıza bağlamak için aşağıdaki adımları bakın.</span><span class="sxs-lookup"><span data-stu-id="059d3-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="059d3-131">Sertifika yetkilisi (CA) sertifika dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="059d3-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="059d3-132">PostgreSQL sunucu bulunuyor Azure veritabanınızla SSL üzerinden iletişim kurması için gereken sertifikayı [burada](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="059d3-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="059d3-133">Sertifika dosyası yerel olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="059d3-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="059d3-134">OpenSSL makinenize yükleyip</span><span class="sxs-lookup"><span data-stu-id="059d3-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="059d3-135">Güvenli, veritabanı sunucunuza bağlanmak, uygulamanız için gerekli sertifika dosyası kodunu çözmek için yerel bilgisayarınızda OpenSSL yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="059d3-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="059d3-136">Linux, OS X veya Unix için</span><span class="sxs-lookup"><span data-stu-id="059d3-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="059d3-137">OpenSSL kitaplıkları doğrudan kaynak kodunda sağlanır [OpenSSL yazılım Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="059d3-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="059d3-138">Aşağıdaki yönergeler OpenSSL Linux bilgisayarınıza yüklemek gereken adımlarda size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="059d3-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="059d3-139">Bu makalede komutları Ubuntu 12.04 üzerinde çalışmak için bilinen ve daha yüksek kullanır.</span><span class="sxs-lookup"><span data-stu-id="059d3-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="059d3-140">Bir terminal oturumu açın ve OpenSSL yükleyin</span><span class="sxs-lookup"><span data-stu-id="059d3-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="059d3-141">Yükleme paketinden dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="059d3-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="059d3-142">Dizin dosyaları ayıkladığınız girin.</span><span class="sxs-lookup"><span data-stu-id="059d3-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="059d3-143">Varsayılan olarak, aşağıdaki gibi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="059d3-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="059d3-144">Aşağıdaki komutu çalıştırarak OpenSSL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="059d3-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="059d3-145">Bir klasördeki dosyaları /usr/local/openssl farklı istiyorsanız, aşağıdaki uygun şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="059d3-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="059d3-146">OpenSSL'ın düzgün yapılandırıldığından, sertifikanızı dönüştürmek için derleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="059d3-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="059d3-147">Derlemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="059d3-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="059d3-148">Derleme işlemi tamamlandıktan sonra aşağıdaki komutu çalıştırarak bir yürütülebilir dosya OpenSSL yüklemeye hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="059d3-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="059d3-149">Sisteminizde OpenSSL başarıyla yükledikten onaylamak için onay ve aşağıdaki komutu, aynı çıktı alırsınız emin olmak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="059d3-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="059d3-150">Başarılı olursa şu iletiyi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="059d3-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="059d3-151">Windows için</span><span class="sxs-lookup"><span data-stu-id="059d3-151">For Windows</span></span>
<span data-ttu-id="059d3-152">Bir Windows Bilgisayarına OpenSSL yükleme aşağıdaki şekillerde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="059d3-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="059d3-153">**(Önerilen)**  Penceresi 10'daki yerleşik Windows için Bash işlevini kullanarak ve yukarıdaki OpenSSL varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="059d3-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="059d3-154">Windows 10 için Windows Bash işlevselliğini etkinleştirmek yönergeler bulunabilir [burada](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="059d3-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="059d3-155">Topluluk tarafından sağlanan bir Win32/64 uygulama indiriliyor aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="059d3-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="059d3-156">OpenSSL yazılım Foundation sağlamaz veya herhangi belirli Windows Installer'lar onaylamaz olsa da, kullanılabilir yükleyicileri listesini sağladıkları [burada](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="059d3-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="059d3-157">Sertifika dosyanızın kod çözme</span><span class="sxs-lookup"><span data-stu-id="059d3-157">Decode your certificate file</span></span>
<span data-ttu-id="059d3-158">İndirilen kök CA'ın dosya şifreli biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="059d3-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="059d3-159">Sertifika dosyası çözecek OpenSSL kullanın.</span><span class="sxs-lookup"><span data-stu-id="059d3-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="059d3-160">Bunu yapmak için bu OpenSSL komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="059d3-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="059d3-161">Azure veritabanına PostgreSQL için SSL sertifikası kimlik doğrulaması ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="059d3-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="059d3-162">Sertifikanızı başarıyla kodunu çözdü olduğunuza göre şimdi veritabanı sunucunuz için güvenli bir şekilde SSL üzerinden bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059d3-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="059d3-163">Sunucu sertifika doğrulaması izin vermek için kullanıcının giriş dizini içinde dosya ~/.postgresql/root.crt Sertifika yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="059d3-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="059d3-164">(Microsoft Windows dosya % APPDATA%\postgresql\root.crt olarak adlandırılır.).</span><span class="sxs-lookup"><span data-stu-id="059d3-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="059d3-165">Aşağıdakiler için PostgreSQL Azure veritabanına bağlanmak için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="059d3-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="059d3-166">Şu anda olduğunda bir bilinen sorun kullanırsanız "sslmode doğrulayın tam =" hizmet, bağlantı bağlantı şu hatayı vererek başarısız olur: _için sunucu sertifikası "&lt;bölge&gt;. Control.Database.Windows.NET"(ve diğer adları 7) ana bilgisayar adı eşleşmiyor"&lt;servername&gt;. postgres.database.azure.com "._</span><span class="sxs-lookup"><span data-stu-id="059d3-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="059d3-167">Varsa "sslmode doğrulayın tam =" olan gerekli, lütfen sunucu adlandırma kuralı kullanmak  **&lt;servername&gt;. database.windows.net** bağlantı dizesi ana bilgisayar adı olarak.</span><span class="sxs-lookup"><span data-stu-id="059d3-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="059d3-168">Bu sınırlama gelecekte kaldırmak planlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="059d3-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="059d3-169">Diğer kullanarak bağlantı [SSL modları](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) tercih edilen konak adlandırma kuralını kullanmaya devam etmelidir  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="059d3-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="059d3-170">Psql komut satırı yardımcı programını kullanma</span><span class="sxs-lookup"><span data-stu-id="059d3-170">Using psql command-line utility</span></span>
<span data-ttu-id="059d3-171">Aşağıdaki örnek başarıyla psql komut satırı yardımcı programını kullanarak PostgreSQL sunucunuza bağlanmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="059d3-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="059d3-172">Kullanım `root.crt` oluşturulan dosya ve `sslmode=verify-ca` veya `sslmode=verify-full` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="059d3-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="059d3-173">PostgreSQL komut satırı arabirimi kullanarak, aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="059d3-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="059d3-174">Başarılı olursa, aşağıdaki çıkış alırsınız:</span><span class="sxs-lookup"><span data-stu-id="059d3-174">If successful, you receive the following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="059d3-175">PgAdmin GUI aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="059d3-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="059d3-176">PgAdmin güvenli SSL üzerinden bağlanmak için 4 yapılandırma gerektirir ayarlamak `SSL mode = Verify-CA` veya `SSL mode = Verify-Full` gibi:</span><span class="sxs-lookup"><span data-stu-id="059d3-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Ekran görüntüsü - bağlantı - pgAdmin SSL modu gerektirir](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="059d3-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="059d3-178">Next steps</span></span>
<span data-ttu-id="059d3-179">Aşağıdaki çeşitli uygulama bağlantı seçenekleri gözden [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="059d3-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
