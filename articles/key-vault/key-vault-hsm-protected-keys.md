---
title: "aaaHow toogenerate ve aktarım HSM korumalı anahtarları Azure anahtar kasası için | Microsoft Docs"
description: "Bu makale toohelp planlama, oluşturma ve ardından Azure anahtar kasası ile kendi HSM korumalı anahtarlar toouse aktarma kullanın. BYOK olarak da bilinen veya kendi anahtarını getir."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Nasıl toogenerate ve aktarım HSM korumalı anahtarları Azure anahtar kasası
## <a name="introduction"></a>Giriş
Ek güvence için Azure anahtar kasası kullandığınızda alabilir veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur. Bu senaryoda başvurulan tooas görülür *kendi anahtarını Getir*, veya BYOK. Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır. Azure anahtar kasası HSM'ler tooprotect Thales nShield ailesi anahtarlarınızı kullanır.

Bu konuda toohelp planlama, oluşturma ve ardından Azure anahtar kasası ile kendi HSM korumalı anahtarlar toouse aktarma Hello bilgileri kullanın.

Bu işlev Azure Çin için kullanılamıyor.

> [!NOTE]
> Azure anahtar kasası hakkında daha fazla bilgi için bkz: [Azure anahtar kasası nedir?](key-vault-whatis.md)  
>
> Bir anahtar kasası için HSM korumalı anahtarlar oluşturma içeren bir başlangıç öğreticisinde için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).
>
>

Oluşturma ve HSM korumalı anahtara hello Internet aktarma hakkında daha fazla bilgi için:

* Merhaba saldırı yüzeyini azaltan bir çevrimdışı iş istasyonundan hello anahtarı oluşturur.
* başlangıç anahtarı bir anahtar değişim anahtarı (aktarılan toohello Azure anahtar kasası HSM'ler olana kadar şifrelenmiş olarak kalan KEK ile), şifrelenir. Yalnızca şifrelenmiş sürümü anahtarınızı hello hello özgün iş istasyonundan ayrılır.
* Merhaba araç takımı, anahtar toohello Azure anahtar kasası güvenlik dünyasına bağlar, Kiracı anahtarınızı özelliklerini ayarlar. Bu nedenle Hello Azure anahtar kasası HSM'ler almak ve anahtarınızı şifresini sonra yalnızca bu HSM'ler bunu kullanabilirsiniz. Anahtarınız dışarı aktarılamaz. Bu bağlama hello Thales Hsm'leri tarafından zorlanır.
* Başlangıç anahtarınızı hello Azure anahtar kasası Hsm'lerinin içinde oluşturulur ve dışarı aktarılabilir olmadığı kullanılan tooencrypt olan anahtar değişim anahtarı (KEK). Merhaba HSM'ler hello KEK hello HSM'ler dışında NET bir sürümü olabilir uygulayın. Ayrıca, hello araç takımı KEK dışarı aktarılabilir olmadığı ve Thales tarafından üretilmiş orijinal bir HSM içinde oluşturulduğu bu hello Thales kanıtı içerir.
* Merhaba araç takımı, hello Azure anahtar Kasası'nın güvenlik Dünyası da Thales tarafından üretilen orijinal bir HSM üzerinde oluşturulduğu Thales kanıtı içerir. Bu kanıtlama tooyou Microsoft orijinal donanım kullandığını kanıtlar.
* Microsoft ve her bir coğrafi bölge güvenlik Dünyaları ayrı ayrı kullanır. Bu ayrım anahtarınızı yalnızca veri merkezleri içinde şifrelediğiniz hello bölgede kullanılabilir olmasını sağlar. Örneğin, Avrupalı bir müşterinin bir anahtarı Kuzey Amerika veya Asya'daki veri merkezlerinde kullanılamaz.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Thales Hsm'leri ve Microsoft Hizmetleri hakkında daha fazla bilgi
Thales e güvenlikle ilgili bir başında genel veri şifreleme ve siber güvenlik çözümleri toohello finansal hizmetler, yüksek teknoloji, üretim, kamu ve teknoloji sektörlerine sağlayıcısıdır. 40 yıllık korumadaki Kurumsal ve resmi bilgileri ile Thales çözümleri dört hello beş büyük enerji ve Havacılık şirketler tarafından kullanılır. Çözümleri 22 NATO ülkesi tarafından da kullanılır ve birden fazla yüzde 80'tüm dünyadaki ödeme işlemlerinin güvenli.

Microsoft Thales tooenhance hello durumuyla resim HSM'ler için iş Birliği yapmaktadır. Bu geliştirmeler, tooget hello tipik yararları anahtarlarınızı üzerinde bırakmasını denetime sahip olmadan barındırılan hizmetler sağlar. Özellikle, bu geliştirmeler, Microsoft'un gerek yoktur, böylece hello HSM'ler yönetmesine izin. Hizmet, Azure anahtar kasası kısa bildirimi toomeet ölçeklendirir bulut olarak kuruluşunuzun kullanım ani. AT hello aynı zaman, anahtarınız, Microsoft'un Hsm'leri içerisinde korunur: hello anahtarı oluşturma ve tooMicrosoft'ın HSM'ler aktarma çünkü hello anahtar yaşam döngüsü üzerinde denetimi korumak.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Uygulama kendi anahtarını getir (BYOK) için Azure anahtar kasası
Kullanım Merhaba, kendi HSM korumalı anahtara oluşturmak ve tooAzure anahtar kasası aktarım bilgi ve yordamları izleyerek — hello kendi anahtarı (BYOK) senaryosu getirin.

## <a name="prerequisites-for-byok"></a>BYOK için Önkoşullar
Tablo için bir önkoşul listesi için aşağıdaki hello kendi anahtarını getir (BYOK) Azure anahtar kasası için bkz.

| Gereksinim | Daha fazla bilgi |
| --- | --- |
| Bir abonelik tooAzure |Azure anahtar kasası toocreate, bir Azure aboneliği gerekir: [ücretsiz deneme için kaydolun](https://azure.microsoft.com/pricing/free-trial/) |
| Azure anahtar kasası Premium Hizmet katmanını toosupport HSM korumalı anahtarlar hello |Azure anahtar kasası hello hizmet katmanları ve yetenekler hakkında daha fazla bilgi için bkz: Merhaba [Azure anahtar kasası fiyatlandırma](https://azure.microsoft.com/pricing/details/key-vault/) Web sitesi. |
| Thales HSM, akıllı kartlar ve destek yazılımı |Bilmeniz gereken erişim tooa Thales donanım güvenlik modülü ve Thales HSM'ler hakkında temel operasyonel bilginiz. Bkz: [Thales donanım güvenlik modülü](https://www.thales-esecurity.com/msrms/buy) uyumlu modellerin veya toopurchase bir yoksa bir HSM hello listesi için. |
| Donanım ve yazılım hello:<ol><li>Çevrimdışı bir x64 en az bir Windows işletim sistemi en az Windows 7 ve Thales nShield yazılımı sürümü ile iş istasyonu sürüm 11.50.<br/><br/>Bu iş istasyonu Windows 7 çalıştırıyorsa, şunları yapmalısınız [Microsoft .NET Framework 4.5 sürümünü yüklemeniz](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Bağlı toohello Internet ve Windows 7'in en az bir Windows işletim sistemi olan bir iş istasyonu ve [Azure PowerShell](/powershell/azure/overview) **en düşük sürüm 1.1.0** yüklü.</li><li>Bir USB sürücü veya en az 16 MB boş alana sahip başka bir taşınabilir depolama cihazı.</li></ol> |Güvenlik nedenleriyle, o hello ilk iş istasyonunun bağlı tooa ağ değil öneririz. Ancak, bu öneri program aracılığıyla zorlanmaz.<br/><br/>İzleyen hello yönergelerde başvurulan tooas hello bağlantısı kesilmiş iş istasyonu bu iş istasyonu olduğuna dikkat edin.</p></blockquote><br/>Ayrıca, Kiracı anahtarınız bir üretim ağı için ise, ikinci ve ayrı iş istasyonu toodownload hello araç takımını ve karşıya yükleme hello Kiracı anahtarı kullanmanızı öneririz. Ancak test amacıyla kullanabilirsiniz birinci hello gibi aynı iş istasyonunu hello.<br/><br/>İzleyen hello yönergelerde bu ikinci iş istasyonu başvurulan tooas hello Internet'e bağlı iş istasyonu olduğuna dikkat edin.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Oluşturma ve anahtar kasası HSM anahtar, tooAzure aktarma
Aşağıdaki beş adımları toogenerate hello kullanabilir ve Azure anahtar kasası HSM anahtar, tooan aktarım:

* [1. adım: Internet'e bağlı iş istasyonunuzu hazırlama](#step-1-prepare-your-internet-connected-workstation)
* [2. adım: bağlantısı kesilmiş iş istasyonunuzu hazırlama](#step-2-prepare-your-disconnected-workstation)
* [3. adım: anahtarınızı oluştur](#step-3-generate-your-key)
* [4. adım: anahtarınızı aktarım için hazırlama](#step-4-prepare-your-key-for-transfer)
* [5. adım: Aktarım, anahtar tooAzure anahtar kasası](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>1. adım: Internet'e bağlı iş istasyonunuzu hazırlama
Birinci adım için aşağıdaki bağlı toohello Internet olan iş istasyonunuza yordamlarını hello.

### <a name="step-11-install-azure-powershell"></a>1.1. adım: Azure PowerShell'i yükleme
Merhaba Internet'e bağlı iş istasyonundan, indirin ve hello cmdlet'leri toomanage Azure anahtar kasası içerir hello Azure PowerShell modülünü yükleyin. Bu 0.8.13 en az bir sürümünü gerektirir.

Yükleme yönergeleri için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>1.2. adım: Azure abonelik Kimliğinizi alma
Bir Azure PowerShell oturumu başlatın ve tooyour Azure hesabı komutu aşağıdaki hello kullanarak oturum açın:

        Add-AzureAccount
Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin. Ardından hello kullanın [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) komutu:

        Get-AzureSubscription
Merhaba çıktısını Azure anahtar kasası için kullanacağınız hello abonelik için hello Kimliğini bulun. Bu abonelik kimliği daha sonra ihtiyacınız olacak.

Hello Azure PowerShell penceresini kapatmayın.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>1.3. adım: Azure anahtar kasası için hello BYOK araç takımı indirme
Toohello Microsoft Download Center gidin ve [hello Azure anahtar kasası BYOK araç takımı indirme](http://www.microsoft.com/download/details.aspx?id=45345) coğrafi bölge veya Azure örneği. Merhaba aşağıdaki kullanın bilgi tooidentify hello paket adı toodownload ve karşılık gelen, SHA-256 karma paketi:

- - -
**Amerika Birleşik Devletleri:**

States.zip KeyVault-BYOK-araçları-birleşik

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Avrupa:**

BYOK araçları Europe.zip KeyVault

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Asya:**

BYOK araçları AsiaPacific.zip KeyVault

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**Latin Amerika:**

BYOK araçları LatinAmerica.zip KeyVault

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japonya:**

BYOK araçları Japan.zip KeyVault

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Kore:**

BYOK araçları Korea.zip KeyVault

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Avustralya:**

BYOK araçları Australia.zip KeyVault

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure kamu:**](https://azure.microsoft.com/features/gov/)

BYOK araçları USGovCloud.zip KeyVault

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**ABD hükümeti savunma Bakanlığı:**

BYOK araçları USGovernmentDoD.zip KeyVault

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Kanada:**

BYOK araçları Canada.zip KeyVault

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Almanya:**

BYOK araçları Germany.zip KeyVault

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**Hindistan:**

BYOK araçları India.zip KeyVault

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Birleşik Krallık:**

BYOK araçları UnitedKingdom.zip KeyVault

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

toovalidate Merhaba, indirilen BYOK araç takımı, kullanım Merhaba, Azure PowerShell oturumundan bütünlüğünü [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet'i.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

Merhaba araç takımı hello aşağıdakileri içerir:

* İle başlayan bir ada sahip olan bir anahtar değişim anahtarı (KEK) paketi **BYOK-KEK - pkg-.**
* İle başlayan bir ada sahip olan bir güvenlik Dünyası paketi **BYOK-SecurityWorld - pkg-.**
* Adlı bir python komut **verifykeypackage.py.**
* Adlı bir komut satırı yürütülebilir dosyası **KeyTransferRemote.exe** ve ilişkili DLL'ler.
* Adlı bir Visual C++ yeniden dağıtılabilir paketi, **vcredist_x64.exe.**

Merhaba paket tooa USB sürücü veya başka bir taşınabilir depolama kopyalayın.

## <a name="step-2-prepare-your-disconnected-workstation"></a>2. adım: bağlantısı kesilmiş iş istasyonunuzu hazırlama
Bu ikinci adım için bağlı tooa ağ (Merhaba Internet veya iç ağınıza) olup olmadığını hello iş istasyonunda aşağıdaki yordamlarını hello.

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>2.1. adım: Thales HSM ile hello bağlantısı kesilmiş iş istasyonunuzu hazırlama
Merhaba nCipher (Thales) destek yazılımını bir Windows bilgisayara yükleyin ve ardından bir Thales HSM toothat bilgisayar ekleyin.

Thales araçları bu hello yolunuzda olduğundan emin olun (**%nfast_home%\bin**). Örneğin, hello aşağıdakileri yazın:

        set PATH=%PATH%;"%nfast_home%\bin"

Daha fazla bilgi için Thales HSM hello ile Merhaba kullanıcı kılavuzuna bakın.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>2.2. adım: Merhaba bağlantısı kesilmiş iş istasyonunda yükleme hello BYOK araç takımı
Merhaba USB sürücü veya başka bir taşınabilir depolama Hello BYOK araç takımı paketini kopyalayın ve ardından aşağıdaki hello:

1. Merhaba dosyaları karşıdan hello paketinden herhangi bir klasöre ayıklayın.
2. Bu klasörden vcredist_x64.exe çalıştırın.
3. Toohello yükleme hello Visual C++ çalışma zamanı bileşenleri için Visual Studio 2013 hello yönergeleri izleyin.

## <a name="step-3-generate-your-key"></a>3. adım: anahtarınızı oluştur
Bu üçüncü adımı için aşağıdaki hello bağlantısı kesilmiş iş istasyonunda yordamlarını hello. toocomplete Bu adım, HSM başlatma modunda olmalıdır. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>3.1. adım: hello HSM modu too'I değiştirmek '
Thales nShield kenar, toochange hello modu kullanıyorsanız: 1. Merhaba düğmesi toohighlight hello gerekli modu kullanın. 2. Birkaç saniye içinde hello Temizle düğmesini basılı birkaç saniye için. Başlangıç modu değişirse, yeni modun yanıp LED durur ve Aydınlatma kalır hello. Merhaba durum LED birkaç saniye düzensiz flash ve düzenli olarak hello cihaz hazır olduğunda sonra yanıp sönen. Aksi takdirde'hello geçerli modunda hello uygun modu ışığı hello aygıt kalır aydınlatma.

### <a name="step-32-create-a-security-world"></a>3.2. adım: güvenlik Dünyası oluşturma
Bir komut istemi başlatın ve hello Thales yeni dünya programını çalıştırın.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Bu programın oluşturduğu bir **güvenlik Dünyası** % toohello C:\ProgramData\nCipher\Key Management Data\local klasörüne karşılık gelen NFAST_KMDATA%\local\world dosyası. Merhaba çekirdek için farklı değerler kullanabilirsiniz, ancak Bizim örneğimizde, istendiğinde tooenter üç adet boş kart ve her biri için PIN olduğunuz. Ardından, herhangi iki kart tam erişim toohello güvenlik Dünyası verin. Bu kartlar hello hale **yönetici kart Seti** hello yeni güvenlik Dünyası için.

Ardından aşağıdaki hello:

* Merhaba Dünya dosyasının yedeğini alın. Güvenli ve Merhaba Dünya dosyasını, hello yönetici kartlarını ve bunların PIN'lerini korumak ve tek bir kişinin erişim toomore bir kart daha olduğundan emin olun.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>3.3. adım: hello HSM modu too'O değiştirmek '
Thales nShield kenar, toochange hello modu kullanıyorsanız: 1. Merhaba düğmesi toohighlight hello gerekli modu kullanın. 2. Birkaç saniye içinde hello Temizle düğmesini basılı birkaç saniye için. Başlangıç modu değişirse, yeni modun yanıp LED durur ve Aydınlatma kalır hello. Merhaba durum LED birkaç saniye düzensiz flash ve düzenli olarak hello cihaz hazır olduğunda sonra yanıp sönen. Aksi takdirde'hello geçerli modunda hello uygun modu ışığı hello aygıt kalır aydınlatma.


### <a name="step-34-validate-hello-downloaded-package"></a>3.4. adım: hello indirilen paketi doğrulama
Bu adım isteğe bağlıdır hello aşağıdaki doğrulayabilmesi ancak önerilir:

* Merhaba hello araç takımında yer alan anahtar değişim anahtarı, orijinal bir Thales HSM'den oluşturulmuştur.
* hello hello araç takımında yer alan güvenlik World Hello karmasını orijinal bir Thales HSM'de oluşturulmuştur.
* Merhaba anahtar değişim anahtarı aktarılamaz.

> [!NOTE]
> Paket toovalidate hello indirilen, hello HSM bağlı olması gerekir, açık ve üzerindeki güvenlik Dünyası (örneğin, hello bir yeni oluşturduğunuz) olması gerekir.
>
>

toovalidate hello indirilen paketi:

1. Coğrafi bölge veya Azure örneği bağlı olarak hello aşağıdakilerden birini yazarak Hello verifykeypackage.py betiği çalıştırın:

   * Kuzey Amerika için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Avrupa için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Asya için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Latin Amerika için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Japonya için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Kore için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Avustralya için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * ABD hükümeti savunma Bakanlığı için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Kanada için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Almanya için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Hindistan için:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hello Thales yazılımı, %NFAST_HOME%\python\bin python içerir
     >
     >
2. Doğrulama başarılı gösterir hello aşağıdaki gördüğünüzü onaylayın: **Result: SUCCESS**

Bu komut dosyası toohello Thales kök anahtarına yukarı hello imzalayan zincirini doğrular. Bu kök anahtarın Hello karma hello komut dosyasında katıştırılmış ve değeri **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Ayrıca bu değeri ayrı ayrı hello ziyaret ederek doğrulayabilirsiniz [Thales Web sitesini](http://www.thalesesec.com/).

Şimdi hazır toocreate yeni bir anahtar olduğunuz.

### <a name="step-35-create-a-new-key"></a>3.5. adım: yeni bir anahtar oluşturun
Merhaba Thales kullanarak bir anahtar oluşturmak **generatekey** program.

Komut toogenerate hello anahtar aşağıdaki hello çalıştırın:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Bu komutu çalıştırdığınızda, aşağıdaki yönergeleri kullanın:

* parametre hello *korumak* toohello değerinin ayarlanması gereken **Modülü**gösterildiği gibi. Bu, modül korumalı bir anahtar oluşturur. Merhaba BYOK araç takımı, OCS korumalı anahtarları desteklemez.
* Merhaba değerini *contosokey* hello için **plainname** ve **contosokey** herhangi bir dize değeri ile. toominimize yönetim ek yüklerini ve hello riskini azaltmak aynı değeri her ikisi için hello kullanmanızı tavsiye ederiz hatalarının,. Merhaba **plainname** değeri yalnızca sayı, tire ve küçük harf içermelidir.
* Bu örnekte Hello pubexp (varsayılan) boş bırakılır, ancak özel değerler belirtebilirsiniz. Daha fazla bilgi için Thales belgelerine hello.

Bu komut, %NFAST_KMDATA%\local klasörünüzde adı ile bir simgeleştirilmiş anahtar dosyası oluşturur **key_simple_**hello ardından **plainname** hello komutta belirtildi. Örneğin: **key_simple_contosokey**. Bu dosya şifreli bir anahtar içerir.

Bu simgeleştirilmiş anahtar dosyasını güvenli bir konuma yedekleyin.

> [!IMPORTANT]
> Daha sonra anahtar tooAzure anahtar kasası aktardığınızda, Microsoft, anahtar ve güvenlik dünyanızı güvenli biçimde yedeklemeniz son derece önemli olacak şekilde bu anahtar geri tooyou dışarı aktaramazsınız. Kılavuzu ve anahtarınızı yedekleme için en iyi uygulamalar için Thales başvurun.
>
>

Artık hazır tootransfer, anahtar tooAzure anahtar kasası şunlardır.

## <a name="step-4-prepare-your-key-for-transfer"></a>4. adım: anahtarınızı aktarım için hazırlama
Dördüncü Bu adım için aşağıdaki hello bağlantısı kesilmiş iş istasyonunda yordamlarını hello.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>4.1. adım: sınırlı izinlerle anahtarınızın bir kopyasını oluşturma

Yeni bir komut istemi açın ve burada, hello BYOK ZIP dosyasının sıkıştırması açılmış hello geçerli dizin toohello konumunu değiştirin. bir komut isteminden anahtarınızı tooreduce hello izinleri coğrafi bölge veya Azure örneği bağlı olarak hello aşağıdakilerden birini çalıştırın:

* Kuzey Amerika için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Avrupa için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Asya için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Latin Amerika için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Japonya için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Kore için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Avustralya için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* ABD hükümeti savunma Bakanlığı için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Kanada için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Almanya için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Hindistan için:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Bu komutu çalıştırdığınızda, yerini *contosokey* hello ile aynı belirtilen değere **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.

Güvenlik Dünyası yönetim kartlarınızı tooplug istenir.

Merhaba komutu tamamlandığında, gördüğünüz **sonucu: başarı** ve hello anahtarınızın sınırlı izinlere sahip kopyası, key_xferacıd_ adlı hello dosyasında olan<contosokey>.

Merhaba ACL'ler inceler hello Thales yardımcı programlarını komutları kullanarak kullanarak:

* aclprint.PY:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Bu komutları çalıştırdığınızda, aynı değeri, belirtilen hello contosokey yerine **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>4.2. adım: Microsoft'un anahtar değişim anahtarını kullanarak anahtarınızı şifreleme
Komutları, coğrafi bölge veya Azure örneği bağlı olarak aşağıdaki hello birini çalıştırın:

* Kuzey Amerika için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Avrupa için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Asya için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Latin Amerika için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Japonya için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Kore için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Avustralya için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* ABD hükümeti savunma Bakanlığı için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Kanada için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Almanya için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Hindistan için:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Bu komutu çalıştırdığınızda, aşağıdaki yönergeleri kullanın:

* Değiştir *contosokey* toogenerate hello anahtarında kullanılan hello tanımlayıcıyla **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.
* Değiştir *Subscriptionıd* hello anahtar kasanızı içeren Azure aboneliği hello kimliği. Bu değer alınan önceden, **adım 1.2: Azure abonelik Kimliğinizi alın** hello gelen [Internet'e bağlı iş istasyonunuzu hazırlama](#step-1-prepare-your-internet-connected-workstation) adım.
* Değiştir *ContosoFirstHSMKey* , çıktı dosyanızın adı için kullanılan bir etikete sahip.

Bu başarıyla tamamlandığında görüntüler **sonucu: başarı** ve yeni bir dosya adı aşağıdaki hello sahip hello geçerli klasörde: KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>4.3. adım: anahtar aktarma paketini toohello Internet'e bağlı iş istasyonunuzu kopyalama
Bir USB sürücü veya diğer taşınabilir depolama toocopy hello çıktı dosyası hello önceki adım (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet'e bağlı iş istasyonundan kullanın.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>5. adım: Aktarım, anahtar tooAzure anahtar kasası
Bu son adım için hello Internet'e bağlı iş istasyonunda, hello kullan [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) hello kopyaladığınız cmdlet tooupload hello anahtar aktarma paketini bağlantısı kesilmiş iş istasyonu toohello Azure anahtar kasası HSM:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Merhaba karşıya yükleme başarılı olursa, eklediğiniz hello anahtarının görüntülenen hello özelliklerine bakın.

## <a name="next-steps"></a>Sonraki adımlar
Bu gibi durumlarda, bu HSM korumalı anahtara artık anahtar kasanız kullanabilirsiniz. Merhaba daha fazla bilgi için bkz: **toouse bir donanım güvenlik modülü (HSM) isteyip istemediğinizi** hello bölümünde [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) Öğreticisi.
