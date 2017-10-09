---
title: "Azure AD Connect eşitleme ile aaaTroubleshoot parola eşitleme | Microsoft Docs"
description: "Bu makalede hakkında bilgi sağlar tootroubleshoot parola eşitleme sorunlarını."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Parola Eşitleme ile Azure AD Connect eşitleme sorunlarını giderme
Bu konu, parola eşitleme ile nasıl tootroubleshoot sorunlar için adımları sağlar. Parolalar beklendiği gibi eşitlemiyor, bir kullanıcı alt kümesini veya tüm kullanıcılar için olabilir. Azure Active Directory (Azure AD) için dağıtım 1.1.524.0 sürümüyle bağlanın ya da daha sonra artık tootroubleshoot parola eşitleme sorunlarını kullanabileceğiniz bir tanı cmdlet:

* Burada hiçbir parolalar eşitlenir bir sorun varsa, toohello başvurun [hiçbir parolalar eşitlenir: hello tanılama cmdlet'ini kullanarak sorun giderme](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) bölümü.

* Ayrı ayrı nesneleri ile ilgili bir sorun varsa, toohello başvuran [bir nesne değil parolaları eşitleme: hello tanılama cmdlet'ini kullanarak sorun giderme](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) bölümü.

Azure AD Connect dağıtımı daha eski sürümleri için:

* Burada hiçbir parolalar eşitlenir bir sorun varsa, toohello başvurmak [hiçbir parolalar eşitlenir: sorun giderme adımları el ile](#no-passwords-are-synchronized-manual-troubleshooting-steps) bölümü.

* Ayrı ayrı nesneleri ile ilgili bir sorun varsa, toohello başvuran [bir nesne değil parolaları eşitleme: sorun giderme adımları el ile](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) bölümü.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Hiçbir parolalar eşitlenir: hello tanılama cmdlet'ini kullanarak sorun giderme
Merhaba kullanabilirsiniz `Invoke-ADSyncDiagnostics` hiçbir parolalar neden eşitlenir çıkışı cmdlet toofigure.

> [!NOTE]
> Merhaba `Invoke-ADSyncDiagnostics` cmdlet'ini veya üstünü yalnızca Azure AD Connect sürüm 1.1.524.0 için kullanılabilir.

### <a name="run-hello-diagnostics-cmdlet"></a>Merhaba tanılama cmdlet'ini çalıştırın
Burada hiçbir parolalar eşitlenir tootroubleshoot sorunlar:

1. Merhaba ile Azure AD Connect sunucunuzdaki yeni bir Windows PowerShell oturumu açın **yönetici olarak çalıştır** seçeneği.

2. Çalıştırma `Set-ExecutionPolicy RemoteSigned` veya `Set-ExecutionPolicy Unrestricted`.

3. `Import-Module ADSyncDiagnostics` öğesini çalıştırın.

4. `Invoke-ADSyncDiagnostics -PasswordSync` öğesini çalıştırın.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Merhaba hello cmdlet'inin sonuçlarını anlama
Merhaba tanılama cmdlet'i denetimleri aşağıdaki hello gerçekleştirir:

* Bu hello doğrular parola eşitleme özelliği, Azure AD kiracınız için etkinleştirildi.

* Bu hello Azure AD Connect sunucusu hazırlama modunda değil doğrular.

* Varolan her (tooan var olan Active Directory ormanı karşılık gelir) Active Directory Bağlayıcısı şirket için:

   * Bu hello doğrular parola eşitleme özelliği etkinleştirildi.
   
   * Parola eşitleme sinyali olayları hello arar Windows uygulama olay günlükleri.

   * Her Active Directory etki alanı için hello şirket içi Active Directory Bağlayıcısı altında:

      * Bu hello doğrular etki alanıdır hello Azure AD Connect sunucudan erişilebilir.

      * Hello doğru kullanıcı adı, parola ve parola eşitlemesi için gerekli izinlere sahip olduğundan'Hello şirket içi Active Directory Bağlayıcısı tarafından kullanılan hello Active Directory etki alanı Hizmetleri (AD DS) hesaplarını doğrular.

Diyagram aşağıdaki hello hello cmdlet'i bir tek etki alanı, şirket içi Active Directory topolojisi için hello sonuçlarını gösterir:

![Parola Eşitleme için tanılama çıktıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Bu bölümde Hello kalan hello cmdlet tarafından döndürülen belirli sonuçları açıklar ve ilgili konular.

#### <a name="password-synchronization-feature-isnt-enabled"></a>Parola eşitleme özelliği etkin değil
Parola Eşitleme hello Azure AD Connect Sihirbazı'nı kullanarak etkinleştirmediyseniz hello aşağıdaki hata döndürdü:

![Parola Eşitleme etkin değil](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Azure AD Connect'i hazırlama modunda sunucusudur
Hazırlama modu Hello Azure AD Connect sunucusu ise, parola eşitleme geçici olarak devre dışıdır ve hello aşağıdaki hata döndürülür:

![Azure AD Connect'i hazırlama modunda sunucusudur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Parola eşitleme sinyali olayı yok
Her bir şirket içi Active Directory Bağlayıcısı kendi parola eşitleme kanalının sahiptir. Merhaba parola eşitleme kanalının kurulur ve eşitlenen tüm parola değişiklikleri toobe yok, bir sinyal olayı (EventID 654) her 30 dakikada hello Windows uygulama olay günlüğü altında oluşturulur. Her şirket içi Active Directory Bağlayıcısı için hello cmdlet hello karşılık gelen sinyal olayları son üç saat arar. Sinyal Olayı bulunamadı, hello aşağıdaki hata döndürülür:

![Olay yok parola eşitleme Kalp yapı](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>AD DS hesap doğru izinlere sahip değil
Merhaba tarafından kullanılan hello AD DS hesabı içi bağlı Active Directory Bağlayıcısı toosynchronize parola karmaları hello uygun izinlere sahip değil, hello aşağıdaki hata döndürülür:

![Yanlış kimlik bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Kullanıcı adı veya parola yanlış AD DS hesap
Merhaba AD DS hesap tarafından kullanılan hello şirket içi Active Directory Bağlayıcısı toosynchronize parola karmaları sahip bir yanlış kullanıcı adı veya parola, hello aşağıdaki hata döndürülür:

![Yanlış kimlik bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Bir nesne değil parolaları eşitleme: hello tanılama cmdlet'ini kullanarak sorun giderme
Merhaba kullanabilirsiniz `Invoke-ADSyncDiagnostics` neden bir nesne not synchronızıng parolaları cmdlet toodetermine.

> [!NOTE]
> Merhaba `Invoke-ADSyncDiagnostics` cmdlet'ini veya üstünü yalnızca Azure AD Connect sürüm 1.1.524.0 için kullanılabilir.

### <a name="run-hello-diagnostics-cmdlet"></a>Merhaba tanılama cmdlet'ini çalıştırın
Burada hiçbir parolalar eşitlenir tootroubleshoot sorunlar:

1. Merhaba ile Azure AD Connect sunucunuzdaki yeni bir Windows PowerShell oturumu açın **yönetici olarak çalıştır** seçeneği.

2. Çalıştırma `Set-ExecutionPolicy RemoteSigned` veya `Set-ExecutionPolicy Unrestricted`.

3. `Import-Module ADSyncDiagnostics` öğesini çalıştırın.

4. Hello aşağıdaki cmdlet'i çalıştırın:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Örneğin:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Merhaba hello cmdlet'inin sonuçlarını anlama
Merhaba tanılama cmdlet'i denetimleri aşağıdaki hello gerçekleştirir:

* Merhaba Active Directory Bağlayıcısı alanı, meta veri deposu ve Azure Active Directory nesnesindeki hello Hello durumunu inceler AD bağlayıcı alanı.

* Parola Eşitleme ile eşitleme kuralları etkinleştirilmiş ve toohello Active Directory nesnesi geçerli olduğunu doğrular.

* Merhaba son girişimi toosynchronize hello nesnesi için parolayı hello tooretrieve ve görüntü hello sonuçlarını çalışır.

Aşağıdaki diyagramda hello hello hello cmdlet'inin sonuçlarını tek bir nesne için parola eşitleme sorunlarını giderirken gösterilmektedir:

![Parola Eşitleme - tek nesne için tanılama çıktıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Bu bölümde Hello kalan hello cmdlet tarafından döndürülen belirli sonuçları açıklar ve ilgili konular.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>dışarı aktarılan tooAzure AD Hello Active Directory nesnesi değil
Hello Azure AD kiracısında karşılık gelen hiçbir nesne olduğundan bu şirket içi Active Directory hesabı için parola eşitleme başarısız olur. Merhaba aşağıdaki hata döndürdü:

![Azure AD nesnesi eksik.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>Kullanıcının geçici bir parolaya sahip
Şu anda Azure AD Connect geçici parolaları Azure AD ile eşitleme desteklemez. Bir parola toobe geçici hello durumunda olduğu kabul edilir **sonraki oturumda parola Değiştir** seçeneği hello şirket içi Active Directory kullanıcı ayarlanır. Merhaba aşağıdaki hata döndürdü:

![Geçici parolayı verilmez](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Son deneme toosynchronize parola sonuçlarını kullanılamaz
Varsayılan olarak, Azure AD Connect yedi gün için parola eşitleme denemesi hello sonuçlarını depolar. Seçili hello Active Directory nesne için kullanılabilen hiç sonuç yoksa uyarı aşağıdaki hello verilir:

![Tanılama çıktıları tek nesnesi - parola eşitleme geçmişi yok](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Hiçbir parolalar eşitlenir: sorun giderme adımları el ile
Hiçbir parolalar neden eşitlenir bu adımları toodetermine izleyin:

1. Merhaba Bağlan sunucu, [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode)? Bir sunucu hazırlama modunda parolaları eşitlemez.

2. Hello Hello komut dosyasını çalıştırmak [alma, parola eşitleme ayarları hello durum](#get-the-status-of-password-sync-settings) bölümü. Merhaba parola eşitleme yapılandırmasına genel bakış sağlar.  

    ![Parola Eşitleme ayarlarını PowerShell komut dosyası çıktısı](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Azure AD'de Hello özelliği etkin değilse veya hello eşitleme kanal durumu etkin değilse, hello Connect Yükleme Sihirbazı'nı çalıştırın. Seçin **eşitleme seçeneklerini özelleştirme**ve Parola Eşitleme'seçimini kaldırın. Bu değişiklik hello özelliğini geçici olarak devre dışı bırakır. Ardından hello Sihirbazı'nı yeniden çalıştırın ve parola eşitleme yeniden etkinleştirin. Merhaba komut dosyasını çalıştırmak yeniden yapılandırma hello tooverify doğrudur.

4. Hatalar için hello olay günlüğüne bakın. Bir sorunu gösterir olayları aşağıdaki hello arayın:
    * Kaynak: "Dizin eşitleme" kimliği: 0, 611, 652, bu olayları görürseniz 655 bağlantı sorun oluştu. Merhaba olay günlüğü iletisi bir sorun olduğu orman ile ilgili bilgi içerir. Daha fazla bilgi için bkz: [bağlantı sorunu](#connectivity problem).

5. Sinyal alınmadı bakın veya başka bir şey çalışılan gerekiyorsa, çalıştırmak [tüm parolaların tam eşitlemesi](#trigger-a-full-sync-of-all-passwords). Merhaba komut yalnızca bir kez çalıştırın.

6. Merhaba bkz [parolaları eşitleme değil bir nesne sorun giderme](#one-object-is-not-synchronizing-passwords) bölümü.

### <a name="connectivity-problems"></a>Bağlantı sorunları

Azure AD ile bağlantı var mı?

Mu hello hesap gerekli izinleri tooread hello parola karmaları tüm etki alanlarında? Hızlı ayarları kullanarak bağlan yüklediyseniz hello izinleri zaten doğru olması gerekir. 

Özel yükleme kullandıysanız, hello izinlerini el ile Merhaba aşağıdakileri yaparak ayarlayın:
    
1. Merhaba Active Directory Bağlayıcısı, başlangıç tarafından kullanılan toofind hello hesabı **Eşitleme Hizmeti Yöneticisi'ni**. 
 
2. Çok Git**Bağlayıcılar**ve hello şirket içi Active Directory ormanı sorun giderme için arama yapın. 
 
3. Merhaba bağlayıcıyı seçin ve ardından **özellikleri**. 
 
4. Çok Git**tooActive Directory ormanına Bağlan**.  
    
    ![Active Directory Bağlayıcısı tarafından kullanılan hesap](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Merhaba kullanıcı adını ve parolayı hello hesabının bulunduğu hello unutmayın.
    
5. Başlat **Active Directory Kullanıcıları ve Bilgisayarları**ve ardından daha önce bulunan hello hesabının hello kökündeki ormanınızdaki tüm etki alanlarının hello izleyin izinlere sahip olduğunu doğrulayın:
    * Dizin Değişikliklerini Çoğaltma
    * Tüm çoğaltma dizini değiştirir

6. Merhaba, etki alanı denetleyicileri ulaşılabilir Azure AD Connect tarafından misiniz? Merhaba Connect sunucusu tooall etki alanı denetleyicileri bağlanamıyorsanız, yapılandırma **yalnızca tercih edilen etki alanı denetleyicisini kullanmasını**.  
    
    ![Active Directory Bağlayıcısı tarafından kullanılan etki alanı denetleyicisi](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Çok dön**Eşitleme Hizmeti Yöneticisi'ni** ve **yapılandırma dizini bölümü**. 
 
8. Etki alanınızda seçin **dizin bölümlerini Seç**seçin hello **yalnızca tercih edilen etki alanı denetleyicilerinin kullandığı** onay kutusunu işaretleyin ve ardından **yapılandırma**. 

9. Merhaba listesinde Bağlan parola eşitleme için kullanması gereken hello etki alanı denetleyicileri girin. Merhaba aynı liste içeri ve dışarı aktarma de için kullanılır. Tüm etki alanları için bu adımları uygulayın.

10. Merhaba komut dosyası hiçbir sinyal olduğunu gösteriyorsa, hello komut dosyasını Çalıştır [tüm parolaların tam eşitlemesi](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Bir nesne değil parolaları eşitleme: sorun giderme adımları el ile
Bir nesnenin hello durumunu gözden geçirerek kolayca parola eşitleme sorunlarını giderebilirsiniz.

1. İçinde **Active Directory Kullanıcıları ve Bilgisayarları**hello kullanıcı için arama yapın ve ardından bu hello doğrulayın **kullanıcı bir sonraki oturumda parola değiştirmeli** onay kutusu işaretli.  

    ![Active Directory üretken parolaları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Merhaba onay kutusu seçiliyse, hello kullanıcı toosign isteyin ve hello parolayı değiştirin. Geçici parolalar Azure AD ile eşitlenmemiş.

2. Merhaba parolası Active Directory'de doğru görünüyorsa, hello eşitleme altyapısı hello kullanıcı izleyin. Şirket içi Active Directory tooAzure AD alanından aşağıdaki hello kullanıcı tarafından hello nesnesinde açıklayıcı bir hata olup olmadığını görebilirsiniz.

    a. Merhaba Başlat [Eşitleme Hizmeti Yöneticisi'ni](active-directory-aadconnectsync-service-manager-ui.md).

    b. Tıklatın **Bağlayıcılar**.

    c. Select hello **Active Directory Bağlayıcısı** hello kullanıcının bulunduğu.

    d. Seçin **bağlayıcı alanı arama**.

    e. Merhaba, **kapsam** kutusunda **DN ya da bağlantı**ve sorun gidermeye hello kullanıcının tam DN hello girin.

    ![Bağlayıcı alanı DN'si kullanıcı ara](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Aradığınız ve ardından hello kullanıcı bulun **özellikleri** toosee tüm öznitelikleri hello. Merhaba kullanıcı hello arama sonucunda değilse doğrulayın, [filtreleme kuralları](active-directory-aadconnectsync-configure-filtering.md) ve, çalıştırdığınızdan emin olun [Uygula ve değişiklikleri doğrulamak](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) hello kullanıcı tooappear Bağlan için.

    g. geçen hafta toosee hello parola eşitleme hello hello nesne ayrıntılarını tıklatın **günlük**.  

    ![Nesne günlük ayrıntıları](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Merhaba nesne günlük boşsa, Azure AD Connect oluşturulamıyor tooread hello parola karması Active Directory'den kaldırıldı. Sorunlarını giderme devam [bağlantı hataları](#connectivity-errors). Başka bir değerden görürseniz **başarı**, toohello tabloya başvuruda [Parola Eşitleme günlüğü](#password-sync-log).

    h. Select hello **çizgileri** sekmesinde ve bu en az bir eşitleme kuralı hello emin **PasswordSync** sütunu **True**. Merhaba Varsayılan yapılandırmada hello hello eşitleme kuralının adıdır **içinde AD'den - kullanıcı AccountEnabled**.  

    ![Bir kullanıcı hakkındaki bilgileri çizgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    ı. Tıklatın **meta veri deposu nesne özellikleri** toodisplay kullanıcı özniteliklerinin listesi.  

    ![Meta veri bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Olduğunu doğrulayın hiçbir **cloudFiltered** özniteliği mevcut. Merhaba etki alanı öznitelikler (domainFQDN ve domainNetBios) hello beklenen değerler olduğundan emin olun.

    j. Merhaba tıklatın **Bağlayıcılar** sekmesi. Bağlayıcılar tooboth şirket içi Active Directory gördüğünüzden emin olun ve Azure AD.

    ![Meta veri bilgileri](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Azure AD temsil eden select hello satıra tıklayın **özellikleri**ve ardından hello **Lineage** sekmesini hello bağlayıcı alanı nesne hello bir giden kuralı olmalıdır **PasswordSync** sütun kümesi çok**doğru**. Merhaba Varsayılan yapılandırmada hello hello eşitleme kuralının adıdır **tooAAD - kullanıcı katılma çıkışı**.  

    ![Bağlayıcı alanı nesne özellikleri iletişim kutusu](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Parola Eşitleme günlüğü
Merhaba durum sütun değerleri aşağıdaki hello sahip olabilir:

| Durum | Açıklama |
| --- | --- |
| Başarılı |Parola başarıyla eşitlendi. |
| FilteredByTarget |Parola çok ayarlamak**kullanıcı bir sonraki oturumda parola değiştirmeli**. Parola eşitlenmemiş. |
| NoTargetConnection |Nesne yok hello meta veri deposu veya hello Azure AD Bağlayıcısı alanı. |
| SourceConnectorNotPresent |Nesnesi Hello şirket içi Active Directory Bağlayıcısı alanı bulunamadı. |
| TargetNotExportedToDirectory |hello Azure AD Bağlayıcısı alanı Hello nesnesinde henüz verilemez. |
| MigratedCheckDetailsForMoreInfo |Günlük girişi 1.0.9125.0 Yapı önce oluşturuldu ve eski durumuna gösterilir. |
| Hata |Hizmet bilinmeyen bir hata döndürdü. |
| Bilinmeyen |Tooprocess parola karmaları toplu çalışırken bir hata oluştu.  |
| MissingAttribute |Azure AD etki alanı Hizmetleri tarafından gereken belirli öznitelikleri (örneğin, Kerberos karması) kullanılabilir değil. |
| RetryRequestedByTarget |Azure AD etki alanı Hizmetleri tarafından gereken belirli öznitelikleri (örneğin, Kerberos karması) daha önce kullanılamıyordu. Bir deneme tooresynchronize hello kullanıcının parola karmasını yapılır. |

## <a name="scripts-toohelp-troubleshooting"></a>Betik toohelp sorunlarını giderme

### <a name="get-hello-status-of-password-sync-settings"></a>Parola Eşitleme ayarlarının Hello durumunu Al
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Tüm parolaların tam eşitlemesi
> [!NOTE]
> Bu komut dosyası yalnızca bir kez çalıştırın. Bu birden çok kez toorun ihtiyacınız varsa, başka bir şey hello sorunudur. tootroubleshoot hello sorun, Microsoft desteğe başvurun.

Komut dosyası izleyen hello kullanarak bir tam eşitleme tüm parolaların tetikleyebilirsiniz:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Sonraki adımlar
* [Parola Eşitleme ile Azure AD Connect eşitleme uygulama](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect eşitleme: eşitleme seçeneklerini özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
