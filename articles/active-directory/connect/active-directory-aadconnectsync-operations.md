---
title: "Azure AD Connect eşitleme: işletimsel görevleri ve ilgili önemli noktalar | Microsoft Docs"
description: "Bu konu, Azure AD Connect eşitleme için işletimsel görevleri açıklar ve nasıl bu bileşen işletim tooprepare."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Azure AD Connect eşitleme: işletimsel görevleri ve değerlendirme
Bu konuda Hello amacı toodescribe işletimsel görevler için Azure AD Connect Eşitleme ' dir.

## <a name="staging-mode"></a>Hazırlama modu
Hazırlama modu dahil olmak üzere çeşitli senaryoları için kullanılabilir:

* Yüksek kullanılabilirlik.
* Test ve yeni yapılandırma değişikliği dağıtın.
* Yeni bir sunucu getirir ve hello eski yetkisini alın.

Merhaba sunucu etkin hale getirmeden önce hazırlama modunda bir sunucuyla değişiklikleri toohello yapılandırma ve önizleme hello değişiklik yapabilirsiniz. Ayrıca, toorun tam içeri aktarma ve tam eşitleme tooverify sağlar bu yapmadan önce tüm değişiklikleri beklenen üretim ortamınıza değiştirir.

Yükleme sırasında hello sunucu toobe seçebilirsiniz **hazırlama modu**. Bu eylemin hello sunucu içeri aktarma ve eşitleme için etkin hale getirir, ancak hiçbir dışarı aktarma çalışmaz. Bu özellikler yüklemesi sırasında seçilen olsa bile sunucu hazırlama modunda bir parola eşitleme ya da parola geri yazma çalışmıyor. Hazırlama modunu devre dışı bıraktığınızda, hello server dışarı aktarma başlatır, parola eşitleme sağlar ve parola geri yazma özelliğini etkinleştirir.

Bir verme hello Eşitleme Hizmeti Yöneticisi'ni kullanarak hala zorlayabilirsiniz.

Sunucu hazırlama modunda bir Active Directory ve Azure AD tooreceive değişikliklerden devam eder. Her zaman bir kopyasını hello en son değişiklikleri ve can çok hızlı gerçekleştirin başka bir sunucunun hello sorumlulukları vardır. Yapılandırma değişiklikleri tooyour birincil sunucusu yapın, sorumluluk toomake hello hazırlama modunda aynı değişiklikleri toohello sunucusu olur.

Merhaba sunucu kendi SQL veritabanı olduğundan bu, eski eşitleme teknolojilerinin bilgi ile hazırlama modunda hello farklıdır. Bu mimarisi, farklı bir veri merkezinde bulunan modu sunucu toobe hazırlama hello sağlar.

### <a name="verify-hello-configuration-of-a-server"></a>Bir sunucunun Hello yapılandırmasını doğrulama
tooapply bu yöntem, şu adımları izleyin:

1. [Hazırlama](#prepare)
2. [Yapılandırma](#configuration)
3. [İçeri aktarma ve eşitleme](#import-and-synchronize)
4. [Doğrulayın](#verify)
5. [Anahtar active server](#switch-active-server)

#### <a name="prepare"></a>Hazırlama
1. Azure AD Connect'i yüklemek, seçin **hazırlama modu**ve işaretini **Eşitlemeyi Başlat** hello son sayfasında hello Yükleme Sihirbazı'nda. Bu mod toorun hello eşitleme altyapısı el ile sağlar.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Oturum Kapat/oturum açma ve hello Başlat menüsünü seçin **eşitleme hizmeti**.

#### <a name="configuration"></a>Yapılandırma
Sunucu hazırlama hello ile özel değişiklikler toohello birincil sunucu ve istediğiniz toocompare hello yapılandırma yaptıysanız, daha sonra kullanmak [Azure AD Connect yapılandırma Belgeleyici'yi](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>İçeri aktarma ve eşitleme
1. Seçin **Bağlayıcılar**, ve seçin hello hello türüne sahip ilk bağlayıcı **Active Directory etki alanı Hizmetleri**. Tıklatın **çalıştırmak**seçin **tam alma**, ve **Tamam**. Bu türdeki tüm bağlayıcıları için bu adımları uygulayın.
2. Select hello bağlayıcı türü olan **Azure Active Directory (Microsoft)**. Tıklatın **çalıştırmak**seçin **tam alma**, ve **Tamam**.
3. Merhaba sekmesini bağlayıcılar hala seçili olduğundan emin olun. Her bağlayıcı türü olan **Active Directory etki alanı Hizmetleri**, tıklatın **çalıştırmak**seçin **Delta eşitlemesi**, ve **Tamam**.
4. Select hello bağlayıcı türü olan **Azure Active Directory (Microsoft)**. Tıklatın **çalıştırmak**seçin **Delta eşitlemesi**, ve **Tamam**.

Hazırlanan verme tooAzure AD değiştirir ve AD (Exchange karma dağıtımı kullanıyorsanız) şirket içi yazdınız. Merhaba sonraki adımlar gerçekte hello verme toohello dizinleri başlamadan önce toochange hakkında nedir tooinspect izin verin.

#### <a name="verify"></a>Doğrulama
1. Bir komut istemi başlatın ve çok gidin`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Çalıştır: `csexport "Name of Connector" %temp%\export.xml /f:x` hello bağlayıcı hello adını eşitleme hizmetinde bulunabilir. Bu ad benzer too"contoso.com – AAD için Azure AD var."
3. Merhaba bölümünden Hello PowerShell Betiği kopyalayın [CSAnalyzer](#appendix-csanalyzer) adlı tooa dosya `csanalyzer.ps1`.
4. Bir PowerShell penceresi açın ve hello PowerShell komut dosyasını oluşturduğunuz toohello klasörü bulun.
5. Çalıştır: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Şimdi adlı bir dosyanız varsa **processedusers1.csv** , incelenmesi Microsoft Excel'de. Tüm değişiklikleri hazırlanan dışarı toobe tooAzure AD bu dosyada bulunamadı.
7. Gerekli değişiklikleri toohello veriler veya yapılandırma olun ve dışarı toobe hakkında değişikliklerini beklenen hello kadar bu adımları tekrar (içeri aktarma ve eşitleme ve doğrula) çalıştırın.

#### <a name="switch-active-server"></a>Anahtar active server
1. Merhaba şu anda etkin sunucuda tooAzure AD verme olmayan şekilde hello sunucu (FIM/DirSync/Azure AD eşitleme) devre dışı etkinleştirmek ya da hazırlama modu (Azure AD Connect) ayarlayın.
2. Merhaba sunucusunda Hello Yükleme Sihirbazı'nı çalıştırdığınız **hazırlama modu** ve devre dışı bırakma **hazırlama modu**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Olağanüstü durum kurtarma
Durumunda bir olağanüstü durum hello eşitleme sunucusu kaybetmek burada hello uygulama tasarım hangi toodo tooplan parçasıdır. Farklı modelleri toouse ve hangi bir toouse dahil olmak üzere birkaç unsur vardır:

* Mümkün yapma olmaması tooobjects hello kapalı kalma süresi sırasında Azure AD değişiklikleri için tolerans aralığınız nedir?
* Parola Eşitleme kullanırsanız, hello kullanıcılar durumda bunlar şirket içi değişiklik toouse hello eski parola Azure AD'de sahip oldukları kabul ediyor musunuz?
* Parola geri yazma gibi gerçek zamanlı işlemler üzerinde bir bağımlılık var mı?

Merhaba yanıtlar toothese sorular ve kuruluşunuzun ilkesini bağlı olarak, stratejileri aşağıdaki hello birini uygulanabilir:

* Gerektiğinde yeniden oluşturun.
* Bilinen bir yedek bir bekleme sunucusunun **hazırlama modu**.
* Sanal makineler kullanır.

Merhaba yerleşik SQL Express veritabanı kullanmayın sonra hello da gözden geçirmelisiniz [SQL yüksek kullanılabilirlik](#sql-high-availability) bölümü.

### <a name="rebuild-when-needed"></a>Gerektiğinde yeniden oluşturma
Gerektiğinde bir sunucusu yeniden oluşturma için tooplan bir uygulanabilir stratejidir. Genellikle, yükleme ve eşitleme altyapısı hello ilk alma hello ve eşitleme birkaç saat içinde tamamlanabilir. Kullanılabilir bir yedek sunucu değilse, olası tootemporarily bir etki alanı denetleyicisi toohost hello eşitleme altyapısı kullanılır.

Active Directory ve Azure AD hello verilerden Hello veritabanı yeniden şekilde hello eşitleme altyapısı sunucusu hello nesneler hakkında herhangi bir durum depolamaz. Merhaba **sourceAnchor** özniteliktir kullanılan toojoin hello nesneleri şirket içi ve bulut hello. Yeniden oluşturursanız şirket içi hello server varolan nesnelerle ve hello bulut sonra hello altyapısı eşleşmeleri bu nesneleri yeniden yeniden üzerinde birlikte eşitleyin. Kaydet ve toodocument gerekir hello filtreleme ve eşitleme kuralları gibi toohello sunucusu hello yapılandırma değişikliklerini noktalardır. Eşitlemeye başlamadan önce bu özel yapılandırmalar yeniden gerekir.

### <a name="have-a-spare-standby-server---staging-mode"></a>Hazırlama modu yedek bir bekleme sunucusunun-
Daha karmaşık bir ortamınız varsa, bir veya daha fazla yedek sunucular olması önerilir. Yükleme sırasında bir sunucu toobe etkinleştirebilirsiniz **hazırlama modu**.

Daha fazla bilgi için bkz: [hazırlama modu](#staging-mode).

### <a name="use-virtual-machines"></a>Sanal makineler kullanın
Bir ortak ve desteklenen bir sanal makinede toorun hello eşitleme altyapısı yöntemidir. Merhaba konak bir sorun var. durumda hello eşitleme altyapısı sunucusu hello görüntüsüyle geçirilen tooanother sunucusu olabilir.

### <a name="sql-high-availability"></a>SQL yüksek kullanılabilirlik
Hello Azure AD Connect ile birlikte gelen SQL Server Express'in kullanmıyorsanız, sonra SQL Server için yüksek kullanılabilirlik da dikkate alınmalıdır. desteklenen hello yüksek oranda kullanılabilirlik çözümleri SQL Kümeleme ve AOA (Always On kullanılabilirlik grupları) içerir. Yansıtma desteklenmeyen çözümleri içerir.

SQL AOA için destek tooAzure AD eklendi sürümünde 1.1.524.0 Bağlan. Azure AD Connect yüklemeden önce SQL AOA etkinleştirmeniz gerekir. Yükleme sırasında Azure AD Connect veya sağlanan hello SQL örneği için SQL AOA etkin olup olmadığını algılar. SQL AOA etkinleştirilirse, daha fazla Azure AD Connect SQL AOA yapılandırılmış toouse zaman uyumlu veya zaman uyumsuz çoğaltma olup olmadığını rakamlar. Kullanılabilirlik grubu dinleyicisi Hello ayarlarken hello RegisterAllProvidersIP özelliği too0 ayarlamanız önerilir. Azure AD Connect SQL Native Client tooconnect tooSQL şu anda kullandığı ve SQL Native Client hello MultiSubNetFailover özelliğinin kullanımını desteklemez nedeni budur.

## <a name="appendix-csanalyzer"></a>Ek CSAnalyzer
Merhaba bölümüne bakın [doğrulayın](#verify) nasıl toouse bu komut dosyası.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**  

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)  
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)  
