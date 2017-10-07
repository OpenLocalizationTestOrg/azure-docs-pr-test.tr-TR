---
title: "aaaSplit birleştirme güvenlik yapılandırması | Microsoft Docs"
description: "X409 ayarlamak şifreleme için sertifikalar"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Bölünmüş birleştirme güvenlik yapılandırması
toouse hello bölünmüş/Merge hizmeti, güvenlik doğru şekilde yapılandırmanız gerekir. Merhaba hizmet hello esnek ölçek özelliği Microsoft Azure SQL veritabanı'nın bir parçasıdır. Daha fazla bilgi için bkz: [esnek ölçek bölme ve birleştirme hizmet öğretici](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Sertifikaları yapılandırma
Sertifikalar iki şekilde yapılandırılır. 

1. [tooConfigure hello SSL sertifikası](#to-configure-the-ssl-certificate)
2. [tooConfigure istemci sertifikaları](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain sertifikaları
Ortak sertifika yetkilileri (CA) ya da hello sertifikaları elde edilebilir [Windows sertifika hizmeti](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Bu tercih edilen hello yöntemleri tooobtain sertifikalardır.

Bu seçenek mevcut değilse, oluşturabileceğiniz **otomatik olarak imzalanan sertifikalar**.

## <a name="tools-toogenerate-certificates"></a>Araçlar toogenerate sertifikaları
* [MakeCert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [Pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>toorun hello araçları
* Bir geliştirici komut isteminden Visual stüdyoları için bkz: [Visual Studio komut istemi](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Yüklü değilse, aşağıdaki adrese gidin:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Alma gelen WDK hello [Windows 8.1: indirme setleri ve araçları](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>tooconfigure hello SSL sertifikası
Bir SSL sertifikası gerekli tooencrypt hello iletişim ve hello sunucusuna kimlik doğrulaması. Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:

### <a name="create-a-new-self-signed-certificate"></a>Yeni bir otomatik olarak imzalanan sertifika oluşturma
1. [Otomatik olarak imzalanan sertifika oluşturma](#create-a-self-signed-certificate)
2. [PFX dosyası için otomatik olarak imzalanan SSL sertifika oluşturun.](#create-pfx-file-for-self-signed-ssl-certificate)
3. [SSL sertifikası tooCloud hizmet karşıya yükle](#upload-ssl-certificate-to-cloud-service)
4. [Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir](#update-ssl-certificate-in-service-configuration-file)
5. [SSL sertifika yetkilisi alma](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>var olan bir sertifikayı hello sertifikasından toouse depolama
1. [SSL sertifikası, sertifika deposundan dışarı aktarma](#export-ssl-certificate-from-certificate-store)
2. [SSL sertifikası tooCloud hizmet karşıya yükle](#upload-ssl-certificate-to-cloud-service)
3. [Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>var olan bir sertifikayı bir PFX dosyasına toouse
1. [SSL sertifikası tooCloud hizmet karşıya yükle](#upload-ssl-certificate-to-cloud-service)
2. [Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>tooconfigure istemci sertifikaları
İstemci sertifikaları, sipariş tooauthenticate istekleri toohello hizmetinde gereklidir. Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:

### <a name="turn-off-client-certificates"></a>İstemci sertifikaları devre dışı bırakma
1. [İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Yeni otomatik olarak imzalanan istemci sertifikaları
1. [Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma](#create-a-self-signed-certification-authority)
2. [CA sertifikasını tooCloud hizmet karşıya yükle](#upload-ca-certificate-to-cloud-service)
3. [Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir](#update-ca-certificate-in-service-configuration-file)
4. [İstemci sertifikaları](#issue-client-certificates)
5. [PFX dosyaları için istemci sertifikaları oluşturma](#create-pfx-files-for-client-certificates)
6. [İstemci sertifikası Al](#Import-Client-Certificate)
7. [İstemci sertifikası parmak kopyalayın](#copy-client-certificate-thumbprints)
8. [Merhaba hizmet yapılandırma dosyası izin verilen istemcilerini yapılandırma](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Mevcut istemci sertifikalarını kullanın
1. [CA ortak anahtarı bulma](#find-ca-public-key)
2. [CA sertifikasını tooCloud hizmet karşıya yükle](#Upload-CA-certificate-to-cloud-service)
3. [Hizmet yapılandırma dosyasında CA sertifikasını güncelleştir](#Update-CA-Certificate-in-Service-Configuration-File)
4. [İstemci sertifikası parmak kopyalayın](#Copy-Client-Certificate-Thumbprints)
5. [Merhaba hizmet yapılandırma dosyası izin verilen istemcilerini yapılandırma](#configure-allowed-clients-in-the-service-configuration-file)
6. [İstemci sertifikası iptal denetimi yapılandırma](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>İzin verilen IP adresi
Erişim toohello hizmet uç noktaları kısıtlı toospecific aralıkları IP adresleri olabilir.

## <a name="tooconfigure-encryption-for-hello-store"></a>Merhaba deposu için tooconfigure şifreleme
Bir sertifika hello meta veri deposunda saklanır gerekli tooencrypt hello kimlik bilgileri yok. Merhaba hello üç senaryoları aşağıdaki en uygun seçin ve tüm adımları yürütün:

### <a name="use-a-new-self-signed-certificate"></a>Yeni bir otomatik olarak imzalanan sertifika kullan
1. [Otomatik olarak imzalanan sertifika oluşturma](#create-a-self-signed-certificate)
2. [PFX dosyası için otomatik olarak imzalanan şifreleme sertifika oluşturun.](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Şifreleme sertifikası tooCloud hizmet karşıya yükle](#upload-encryption-certificate-to-cloud-service)
4. [Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Varolan bir sertifikayı hello sertifika deposundan kullanın
1. [Şifreleme sertifikası sertifika deposundan dışarı aktarma](#export-encryption-certificate-from-certificate-store)
2. [Şifreleme sertifikası tooCloud hizmet karşıya yükle](#upload-encryption-certificate-to-cloud-service)
3. [Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Varolan bir sertifikayı bir PFX dosyası kullanın
1. [Şifreleme sertifikası tooCloud hizmet karşıya yükle](#upload-encryption-certificate-to-cloud-service)
2. [Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>Merhaba varsayılan yapılandırması
Merhaba varsayılan yapılandırması erişim toohello tüm HTTP uç noktası reddeder. Merhaba istekleri toothese uç noktaları veritabanı kimlik bilgileri gibi hassas bilgileri taşımak beri Önerilen ayar, hello budur.
Merhaba varsayılan yapılandırması erişim toohello tüm HTTPS uç noktası sağlar. Bu ayar daha fazla kısıtlanabilir.

### <a name="changing-hello-configuration"></a>Merhaba yapılandırmasını değiştirme
Merhaba tooand uç nokta geçerli erişim denetim kurallarını grubunun yapılandırılmış olan hello  **<EndpointAcls>**  hello bölümünde **hizmet yapılandırma dosyası**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

bir erişim denetimi grubu Hello kurallarında yapılandırılmış bir <AccessControl name=""> hello hizmet yapılandırma dosyasının. 

Merhaba biçimi ağ erişim denetimi listelerini belgelerinde açıklanmıştır.
Örneğin, tooallow yalnızca IP'leri hello aralığı 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS uç noktada hello kuralları şuna benzeyebilir:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Hizmet önleme reddi
İki farklı mekanizmaları toodetect desteklenen ve hizmet reddi saldırılarını vardır:

* Uzak ana bilgisayar başına eşzamanlı istek sayısını kısıtlayın (varsayılan olarak kapalıdır)
* Uzak ana bilgisayar başına erişimi oranını kısıtlamak (üzerinde varsayılan olarak)

Bunlar daha fazla dinamik IP Güvenlik IIS'de açıklandığı hello özellikleri temel alır. Ne zaman bu yapılandırmasını değiştirme Etkenler aşağıdaki Merhaba dikkat:

* Proxy ve ağ adresi çevirisi cihazların Merhaba uzak ana bilgisayar bilgilerini üzerinden Hello davranışı
* Her istek tooany kaynak hello web rolü (örn. yükleme komut dosyaları, görüntüler, vb.) olarak kabul edilir

## <a name="restricting-number-of-concurrent-accesses"></a>Eşzamanlı erişimi sayısını sınırlandırma
Bu davranışı yapılandırmak hello ayarlar şunlardır:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Bu koruma DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable değiştirin.

## <a name="restricting-rate-of-access"></a>Erişim kısıtlama oranı
Bu davranışı yapılandırmak hello ayarlar şunlardır:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Merhaba yanıt tooa yapılandırma isteğini reddetti
Merhaba aşağıdaki ayar isteğini reddetti hello yanıt tooa yapılandırır:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Desteklenen diğer değerler için IIS içinde dinamik IP Güvenlik toohello belgelerine başvurun.

## <a name="operations-for-configuring-service-certificates"></a>Hizmet sertifikaları yapılandırma işlemleri
Bu konu yalnızca başvuru amacıyla kullanılır. Lütfen özetlenen hello yapılandırma adımları izleyin:

* Merhaba SSL sertifikası yapılandırma
* İstemci sertifikaları yapılandırın

## <a name="create-a-self-signed-certificate"></a>Otomatik olarak imzalanan sertifika oluşturma
Yürütün:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n hello ile hizmet URL'si. Joker karakterler ("CN = * .cloudapp .net") ve diğer adları ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") desteklenir.
* -e hello sertifika sona erme tarihi ile güçlü bir parola oluşturmak ve istendiğinde belirtin.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Otomatik olarak imzalanan SSL Sertifika PFX dosyası oluşturma
Yürütün:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Bir parola girin ve sonra bu seçenekler ile sertifika verme:

* Evet, hello özel anahtarı dışarı aktar
* Tüm genişletilmiş özellikleri Dışarı Aktar

## <a name="export-ssl-certificate-from-certificate-store"></a>SSL sertifikası, sertifika deposundan dışarı aktarma
* Sertifika Bul
* Tıklatın Eylemler -> tüm görevleri Export ->...
* İçinde sertifika verme bir. Bu seçenekler PFX dosyası:
  * Evet, hello özel anahtarı dışarı aktar
  * Mümkünse hello sertifika yolundaki tüm sertifikaları dahil et * tüm genişletilmiş özellikleri Dışarı Aktar

## <a name="upload-ssl-certificate-toocloud-service"></a>SSL sertifika toocloud hizmeti karşıya yükle
Karşıya yükleme hello var olan sertifika veya oluşturulabilir. Merhaba SSL anahtar çifti PFX dosyası:

* Merhaba özel anahtar bilgisi koruma hello parolayı girin

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Hizmet yapılandırma dosyasında SSL sertifikasını güncelleştir
Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>SSL sertifika yetkilisi alma
Tüm hesap/hello hizmeti ile iletişim kuracak makinesinde aşağıdaki adımları izleyin:

* Merhaba çift tıklayın. Windows Gezgini'nde CER dosyasını
* Merhaba sertifikası iletişim kutusunda, sertifikayı yükle düğmesine...
* Sertifikayı güvenilir kök sertifika yetkilileri deposuna hello alın

## <a name="turn-off-client-certificate-based-authentication"></a>İstemci sertifikası tabanlı kimlik doğrulamasını devre dışı bırakma
Yalnızca istemci sertifika tabanlı kimlik doğrulaması desteklenmez ve diğer mekanizmaları (örneğin Microsoft Azure sanal ağı) yerinde olmadığı sürece, devre dışı bırakmasını genel erişim toohello hizmeti için uç noktaları, izin verir.

Bu ayarları toofalse hello hizmet yapılandırma dosyası tooturn hello özelliğindeki değişiklik devre dışı:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Ardından, aynı parmak izine hello SSL sertifika hello hello CA sertifikası ayarında kopyalayın:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Bir otomatik olarak imzalanan sertifika yetkilisi oluşturma
Aşağıdaki adımları toocreate bir sertifika yetkilisi olarak otomatik olarak imzalanan sertifika tooact hello yürütün:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize,

* -e hello sertifika sona erme tarihi

## <a name="find-ca-public-key"></a>CA ortak anahtarı bulma
İstemci sertifikalarının tümünü hello hizmeti tarafından güvenilen bir sertifika yetkilisi tarafından verilmiş olması gerekir. Merhaba ortak anahtar toohello toobe giderek hello istemci sertifikaları veren sertifika yetkilisi kimlik doğrulaması için sipariş tooupload ile toohello bulut hizmeti kullanılacağını öğrenin.

Merhaba dosya hello ortak anahtarla kullanılabilir durumda değilse, hello sertifika deposundan dışarı aktarın:

* Sertifika Bul
  * Merhaba aynı sertifika yetkilisi tarafından verilen bir istemci sertifikası arayın
* Merhaba sertifikayı çift tıklatın.
* Merhaba sertifikası iletişim kutusunda Hello sertifika yolu sekmesini seçin.
* Merhaba CA hello yolu girişi çift tıklatın.
* Hello sertifika özellikleri not alın.
* Kapat hello **sertifika** iletişim.
* Sertifika Bul
  * Merhaba yukarıda belirtilen CA'yı arayın.
* Tıklatın Eylemler -> tüm görevleri Export ->...
* İçinde sertifika verme bir. CER bu seçenekleri:
  * **Hayır, hello özel anahtarı verme**
  * Tüm sertifikaları hello sertifika yolunda mümkünse içerir.
  * Tüm genişletilmiş özellikleri dışarı aktarın.

## <a name="upload-ca-certificate-toocloud-service"></a>CA sertifika toocloud hizmeti karşıya yükle
Karşıya yükleme hello var olan sertifika veya oluşturulabilir. CER dosyasını hello CA ortak anahtara sahip.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Hizmet yapılandırma dosyasında güncelleştirme CA sertifikası
Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Merhaba ile aynı ayarı aşağıdaki hello Hello değerini güncelleştirmek parmak izi:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>İstemci sertifikaları
Her bireysel yetkili tooaccess hello hizmeti kullanmak özel his/hers için yayımlanan bir istemci sertifikasına sahip olmalıdır ve özel anahtarını his/hers güçlü parola tooprotect kendi seçmeniz gerekir. 

Aşağıdaki adımları hello burada hello CA sertifikası otomatik olarak imzalanan aynı makine oluşturulan ve depolanan hello yürütülmesi gerekir:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Özelleştirme:

* -n Bu sertifika ile kimlik doğrulaması yapılacak toohello istemci için bir kimliği
* -e hello sertifika sona erme tarihi
* MyID.pvk ve bu istemci sertifikası için benzersiz adlarıyla MyID.cer

Bu komut, oluşturulan ve bir kez kullanılan bir parola toobe için sorar. Güçlü bir parola kullanın.

## <a name="create-pfx-files-for-client-certificates"></a>PFX dosyaları için istemci sertifikaları oluşturma
Her oluşturulan istemci sertifikası için yürütün:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Özelleştirme:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Bir parola girin ve sonra bu seçenekler ile sertifika verme:

* Evet, hello özel anahtarı dışarı aktar
* Tüm genişletilmiş özellikleri Dışarı Aktar
* Bu sertifikayı veren hello tek tek toowhom hello verme parola seçmeniz gerekir

## <a name="import-client-certificate"></a>İstemci sertifikası Al
Kendisi için bir istemci sertifikası yayımlandığı her hello anahtar çifti almalısınız hello makinelerinizde klasöründe toocommunicate hello hizmetiyle kullanır:

* Merhaba çift tıklayın. Windows Gezgini'nde PFX dosyası
* Sertifikayı kişisel deposu ile en az bu seçenek hello alın:
  * Seçili tüm genişletilmiş özellikleri Ekle

## <a name="copy-client-certificate-thumbprints"></a>İstemci sertifikası parmak kopyalayın
Kendisi için bir istemci sertifikası yayımlandığı her sipariş tooobtain hello parmak izi his/hers'nda aşağıdaki adımları izlemelisiniz toohello hizmet yapılandırma dosyası eklenecek sertifikası:

* Certmgr.exe çalıştırın
* Merhaba kişisel sekmesini seçin
* Toobe kimlik doğrulaması için kullanılan hello istemci sertifikasına çift tıklayın
* Merhaba Ayrıntılar sekmesini açar hello sertifikası iletişim kutusunda, seçin
* Göster tüm görüntülediğinden emin olun
* Parmak izi hello listesinde adlı select hello alanı
* Merhaba hello parmak izi değerini kopyalayın ** hello ilk rakam önünde görünür olmayan Unicode karakterler silme ** tüm alanları Sil

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Merhaba hizmet yapılandırma dosyasında izin verilen istemcilerini yapılandırma
Merhaba hizmet yapılandırma dosyasında virgülle ayrılmış listesini içeren hello sertifikalarının parmak izleri erişim toohello hizmeti izin verilen hello istemci ayarı aşağıdaki hello Hello değerini güncelleştirin:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>İstemci sertifikası iptal denetimi yapılandırma
Merhaba varsayılan ayarı, istemcinin sertifika iptal durumunu Merhaba sertifika yetkilisi ile kontrol etmez. hello üzerinde tooturn denetler Hello hello istemci sertifikaları veren sertifika yetkilisi bu tür denetimler destekliyorsa, hello X509RevocationMode numaralandırma tanımlanan hello değerlerden biriyle ayarı aşağıdaki hello değiştirin:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Otomatik olarak imzalanan şifreleme sertifikaları için PFX dosyası oluşturun
Bir şifreleme sertifikası için yürütün:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Özelleştirme:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Bir parola girin ve sonra bu seçenekler ile sertifika verme:

* Evet, hello özel anahtarı dışarı aktar
* Tüm genişletilmiş özellikleri Dışarı Aktar
* Merhaba sertifika toohello bulut hizmeti karşıya yüklenirken hello parola gerekir.

## <a name="export-encryption-certificate-from-certificate-store"></a>Şifreleme sertifikası sertifika deposundan dışarı aktarma
* Sertifika Bul
* Tıklatın Eylemler -> tüm görevleri Export ->...
* İçinde sertifika verme bir. Bu seçenekler PFX dosyası: 
  * Evet, hello özel anahtarı dışarı aktar
  * Mümkünse hello sertifika yolundaki tüm sertifikaları dahil et 
* Tüm genişletilmiş özellikleri Dışarı Aktar

## <a name="upload-encryption-certificate-toocloud-service"></a>Şifreleme sertifikası toocloud hizmeti karşıya yükle
Karşıya yükleme hello var olan sertifika veya oluşturulabilir. Merhaba şifreleme anahtar çifti PFX dosyası:

* Merhaba özel anahtar bilgisi koruma hello parolayı girin

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Hizmet yapılandırma dosyasında şifreleme sertifikasını güncelleştir
Merhaba parmak izi hello karşıya sertifika toohello bulut hizmeti ile Merhaba hizmet yapılandırma dosyası ayarlarında aşağıdaki hello Hello parmak izi değerini güncelleştirin:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Ortak sertifika işlemleri
* Merhaba SSL sertifikası yapılandırma
* İstemci sertifikaları yapılandırın

## <a name="find-certificate"></a>Sertifika Bul
Şu adımları uygulayın:

1. MMC.exe çalıştırın.
2. Dosya -> Ekle/Kaldır ek bileşenini...
3. Seçin **Sertifikalar**.
4. **Ekle**'ye tıklayın.
5. Merhaba sertifika deposu konumu seçin.
6. **Son**'a tıklayın.
7. **Tamam** düğmesine tıklayın.
8. Genişletme **Sertifikalar**.
9. Merhaba sertifika deposu düğümünü genişletin.
10. Merhaba sertifika alt düğümünü genişletin.
11. Bir sertifika hello listeden seçin.

## <a name="export-certificate"></a>Sertifika verme
Merhaba, **Sertifika Verme Sihirbazı**:

1. **İleri**’ye tıklayın.
2. Seçin **Evet**, ardından **verme hello özel anahtarı**.
3. **İleri**’ye tıklayın.
4. Merhaba istenen çıktı dosyası biçimini seçin.
5. İstenen başlangıç seçeneklerini işaretleyin.
6. Denetleme **parola**.
7. Güçlü bir parola girin ve onaylayın.
8. **İleri**’ye tıklayın.
9. Yazın veya burada toostore hello sertifika filename göz atın (kullanan bir. PFX uzantılı).
10. **İleri**’ye tıklayın.
11. **Son**'a tıklayın.
12. **Tamam** düğmesine tıklayın.

## <a name="import-certificate"></a>Sertifika İçeri Aktar
Merhaba Sertifika Alma Sihirbazı:

1. Merhaba depolama konumu seçin.
   
   * Seçin **geçerli kullanıcı** geçerli kullanıcı altında çalışan işlemler hello hizmeti erişecek yalnızca
   * Seçin **yerel makine** bu bilgisayardaki diğer işlemlerin hello hizmet erişecekse
2. **İleri**’ye tıklayın.
3. Bir dosyadan içeri aktarma, hello dosya yolunu doğrulayın.
4. İçeri aktarma, bir. PFX dosyası:
   1. Merhaba özel anahtarın korunması hello parolayı girin
   2. İçeri aktarma seçenekleri seçin
5. Mağaza aşağıdaki hello "Yerine" Sertifikalar'ı seçin
6. **Gözat**’a tıklayın.
7. Merhaba istenen depolama alanı seçin.
8. **Son**'a tıklayın.
   
   * Merhaba güvenilen kök sertifika yetkilisi deposunda seçildiyse, tıklatın **Evet**.
9. Tıklatın **Tamam** tüm iletişim Windows.

## <a name="upload-certificate"></a>Sertifikayı karşıya yükleme
Merhaba, [Azure portalı](https://portal.azure.com/)

1. Seçin **bulut hizmetlerini**.
2. Merhaba bulut hizmeti seçin.
3. Merhaba üst menüsünde **Sertifikalar**.
4. Merhaba alt çubuğunda **karşıya**.
5. Merhaba sertifika dosyası seçin.
6. Bu doğruysa bir. PFX dosyası, hello parola hello özel anahtarı girin.
7. Tamamlandığında, hello sertifika parmak izi hello yeni giriş hello listesinde kopyalayın.

## <a name="other-security-considerations"></a>Diğer güvenlik konuları
Merhaba HTTPS uç noktası kullanıldığında, bu belgede açıklanan hello SSL ayarları hello hizmet ve istemcileri arasındaki iletişimi şifrelemek. Bu veritabanı erişimi için kimlik bilgilerini bu yana önemlidir ve hello iletişiminde büyük olasılıkla diğer hassas bilgiler yer alır. Ancak, hello hizmeti kimlik bilgileri, kendi iç Microsoft Azure aboneliğiniz meta veri depolama alanı için sağlanan hello Microsoft Azure SQL veritabanı tablolarında dahil olmak üzere, iç durum devam ederse unutmayın. Bu veritabanı ayarı hizmet yapılandırma dosyanızdaki aşağıdaki hello bir parçası olarak tanımlandı (. CSCFG dosyası): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Bu veritabanında depolanan kimlik bilgileri şifrelenir. Ancak, en iyi uygulama, hizmet dağıtımlarınız web ve çalışan rolleri toodate tutulur ve güvenli olarak hem şifreleme ve şifre çözme depolanan kimlik bilgileri için kullanılan erişim toohello meta veri veritabanı ve hello sertifika içerdiğinden emin olun. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

