### <a name="troubleshoot-azure-diagnostics"></a>Azure Tanılama Sorunlarını Giderme

Merhaba aşağıdaki hata iletisini alırsanız, hello Microsoft.ınsights kaynak sağlayıcısı kayıtlı değil:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

tooregister hello kaynak sağlayıcısı hello Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin:

1.  Merhaba Gezinti hello sol taraftaki bölmede *abonelikleri*
2.  Merhaba hata iletisinde belirtilen hello aboneliği seçin
3.  *Kaynak Sağlayıcıları*’ne tıklayın
4.  Hello bulur *Microsoft.ınsights* sağlayıcısı
5.  Merhaba tıklatın *kaydetmek* bağlantı

![Microsoft.insights kaynak sağlayıcısını kaydetme](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Bir kez hello *Microsoft.ınsights* kaynak sağlayıcısı kayıtlı, tanılamaları yapılandırmayı yeniden deneyin.


Merhaba aşağıdaki hata iletisini alırsanız, PowerShell'de tooupdate PowerShell sürümünüz ihtiyacınız:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Kasım 2016 (v2.3.0) PowerShell toohello uygulamanızın sürümünü güncelleştirin veya hello hello yönergeleri kullanarak daha sonra serbest [Azure PowerShell cmdlet'leri kullanmaya başlama](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) makalesi.
