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
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>SSL bağlantısı Azure veritabanı'nda PostgreSQL için yapılandırın.
Azure veritabanı PostgreSQL için istemci uygulamaları toohello PostgreSQL hizmetini Güvenli Yuva Katmanı (SSL) kullanarak bağlanma tercih eder. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.

Varsayılan olarak, PostgreSQL veritabanı hizmeti hello yapılandırılmış toorequire SSL bağlantı olur. İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa tooyour veritabanı hizmeti bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz. 

## <a name="enforcing-ssl-connections"></a>SSL bağlantıları zorlama
Sağlanan hello Azure portal ve CLI PostgreSQL sunucuları için tüm Azure veritabanı için SSL bağlantılarını zorlama varsayılan olarak etkindir. 

Benzer şekilde, SSL kullanarak yaygın diller tooconnect tooyour veritabanı sunucusu için gerekli hello parametreleri sunucunuz hello Azure portal'ın altındaki hello "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir. Merhaba SSL parametre göre hello bağlayıcı, örneğin değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.

## <a name="configure-enforcement-of-ssl"></a>SSL zorlama yapılandırın
İsteğe bağlı olarak zorunlu SSL bağlantısını devre dışı bırakabilirsiniz. Microsoft Azure önerir tooalways etkinleştirmek **Zorla SSL bağlantısı** için Gelişmiş güvenlik ayarı.

### <a name="using-hello-azure-portal"></a>Hello Azure portalını kullanma
Azure veritabanınız PostgreSQL sunucu için ziyaret edin ve tıklatın **bağlantı güvenliği**. Merhaba iki durumlu düğme tooenable kullanın veya hello devre dışı bırakma **Zorla SSL bağlantısı** ayarı. Daha sonra **Kaydet**'e tıklayın. 

![Bağlantı güvenliği - devre dışı bırak SSL zorla](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Merhaba ayarı hello görüntüleyerek onaylayabilirsiniz **genel bakış** sayfa toosee hello **SSL zorlama durumu** göstergesi.

### <a name="using-azure-cli"></a>Azure CLI’yı kullanma
Etkinleştirmek veya devre dışı hello **ssl zorlama** parametresini kullanarak `Enabled` veya `Disabled` Azure CLI sırasıyla değerleri.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Uygulama veya framework destekler, SSL bağlantılarını emin olun
Veritabanı Hizmetleri, Drupal ve Django gibi PostgreSQL kullanmak birçok yaygın uygulama çerçeveleri SSL yüklemesi sırasında varsayılan olarak etkinleştirmez. SSL bağlantısı etkinleştirme yüklemeden sonra veya CLI komutları belirli toohello uygulaması aracılığıyla yapılmalıdır. PostgreSQL sunucunuz SSL bağlantılarını zorlama ve ilişkili hello uygulama düzgün yapılandırılmamış, Merhaba uygulaması tooconnect tooyour veritabanı sunucusu başarısız olabilir. Uygulamanızın belgelerine toolearn nasıl başvurun tooenable SSL bağlantıları.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Sertifika doğrulaması için SSL bağlantısı gerektiren uygulamalar
Bazı durumlarda, uygulamaların güvenilen bir sertifika yetkilisi (CA) sertifika dosyasını (.cer) tooconnect güvenli bir şekilde oluşturulan bir yerel sertifika dosyası gerektirir. Merhaba aşağıdaki adımları tooobtain hello .cer dosyasına bakın, kod çözme hello sertifikası ve tooyour uygulama bağlayın.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Sertifika yetkilisi (CA) hello Hello sertifika dosyasını indirin 
PostgreSQL server bulunduğu için hello sertifikası toocommunicate Azure veritabanınızla SSL üzerinden gerekli [burada](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Merhaba sertifika dosyasını yerel olarak yükleyin.

### <a name="download-and-install-openssl-on-your-machine"></a>OpenSSL makinenize yükleyip 
Uygulama tooconnect için güvenli bir şekilde gerekli toodecode hello sertifika dosyası tooyour veritabanı sunucusu, yerel bilgisayarınızda tooinstall OpenSSL gerekir.

#### <a name="for-linux-os-x-or-unix"></a>Linux, OS X veya Unix için
Merhaba OpenSSL kitaplıkları hello doğrudan kaynak kodunda sağlanır [OpenSSL yazılım Foundation](http://www.openssl.org). Merhaba aşağıdaki yönergeler size hello adımları gerekli tooinstall OpenSSL Linux Bilgisayarınızda yol. Bu makalede toowork Ubuntu 12.04 ve daha yüksek bilinen komutları kullanır.

Bir terminal oturumu açın ve OpenSSL yükleyin
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Merhaba yükleme paketinden Hello dosyaları ayıklayın
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Merhaba dosyalarını ayıkladığınız Hello dizini girin. Varsayılan olarak, aşağıdaki gibi olması gerekir.

```bash
cd openssl-1.1.0e
```
OpenSSL komutu aşağıdaki hello yürüterek yapılandırın. Merhaba dosyaları bir klasör içinde /usr/local/openssl farklı istiyorsanız emin toochange hello aşağıdaki uygun şekilde olun.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
OpenSSL'ın düzgün yapılandırıldığından, toocompile gerekir, tooconvert sertifikanızı. toocompile, hello aşağıdaki komutu çalıştırın:

```bash
make
```
Derleme işlemi tamamlandıktan sonra hazır tooinstall OpenSSL bir yürütülebilir dosya hello aşağıdaki komutu çalıştırarak demektir:
```bash
make install
```
tooconfirm, sisteminizde OpenSSL başarıyla yükledikten çalışma hello aşağıdaki komut ve toomake hello alma emin denetleyin aynı çıktı.

```bash
/usr/local/openssl/bin/openssl version
```
Başarılı olursa iletiden hello görmeniz gerekir.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Windows için
Bir Windows Bilgisayarına OpenSSL yükleme yolu izleyerek hello yapılabilir:
1. **(Önerilen)**  Kullanarak hello yerleşik Windows için Bash işlevini penceresi 10 ve üzeri sürümlerde, OpenSSL varsayılan olarak yüklenir. Windows 10 için Windows Bash işlevi tooenable nasıl bulunabilir yönergeleri [burada](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Merhaba topluluk tarafından sağlanan bir Win32/64 uygulama indiriliyor aracılığıyla. Merhaba OpenSSL yazılım Foundation sağlamaz veya herhangi belirli Windows Installer'lar onaylamaz olsa da, kullanılabilir yükleyicileri listesini sağladıkları [burada](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Sertifika dosyanızın kod çözme
Merhaba kök CA'ın şifreli biçimde dosyasıdır indirilir. OpenSSL toodecode hello sertifika dosyasını kullanın. toodo, bu nedenle, bu OpenSSL komutu çalıştırın:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>SSL sertifika kimlik doğrulaması ile bağlanan tooAzure PostgreSQL için veritabanı
Sertifikanızı başarıyla kodunu çözdü olduğunuza göre şimdi tooyour veritabanı sunucusu güvenli bir şekilde SSL üzerinden bağlanabilirsiniz. tooallow sunucu sertifika doğrulaması hello sertifika hello dosya ~/.postgresql/root.crt hello kullanıcının giriş dizini içinde yerleştirilmelidir. (Microsoft Windows hello dosyada % APPDATA%\postgresql\root.crt olarak adlandırılır.). Merhaba aşağıdaki tooAzure veritabanı için PostgreSQL bağlama yönergeleri sağlanır.

> [!NOTE]
> Şu anda olduğunda bir bilinen sorun kullanırsanız "sslmode doğrulayın tam =" bağlantı toohello hizmetinde hello bağlantı hello aşağıdaki hata ile başarısız olur: _için sunucu sertifikası "&lt;bölge&gt;. Control.Database.Windows.NET"(ve diğer adları 7) ana bilgisayar adı eşleşmiyor"&lt;servername&gt;. postgres.database.azure.com "._
> Varsa "sslmode doğrulayın tam =" olan gerekli, lütfen hello sunucu adlandırma kuralını kullanın  **&lt;servername&gt;. database.windows.net** , bağlantı dizesi ana bilgisayar adı olarak. Biz bu sınırlamaya hello gelecekteki içinde tooremove planlayın. Diğer kullanarak bağlantı [SSL modları](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) toouse hello tercih edilen konak adlandırma kuralı devam etmesi gerektiğini  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Psql komut satırı yardımcı programını kullanma
Aşağıdaki örnek hello toosuccessfully tooyour PostgreSQL sunucusunu hello psql komut satırı yardımcı programını kullanarak nasıl bağlanacağını gösterir. Kullanım hello `root.crt` oluşturulan dosya ve hello `sslmode=verify-ca` veya `sslmode=verify-full` seçeneği.

Merhaba PostgreSQL komut satırı arabirimi kullanarak, hello aşağıdaki komutu yürütün:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
Başarılı olursa, çıktı aşağıdaki hello alırsınız:
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

#### <a name="using-pgadmin-gui-tool"></a>PgAdmin GUI aracını kullanma
PgAdmin 4 tooconnect SSL üzerinden güvenli bir şekilde yapılandırma gerektirir, tooset hello `SSL mode = Verify-CA` veya `SSL mode = Verify-Full` gibi:

![Ekran görüntüsü - bağlantı - pgAdmin SSL modu gerektirir](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki çeşitli uygulama bağlantı seçenekleri gözden [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
