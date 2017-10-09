UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < veri aktarımı için kullanılan IP adresi toobe] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parametreler:

* /ServerMode: Zorunlu. Her iki hello yapılandırması ve işlem sunucusu yüklü olup olmadığını veya hello işlemi yalnızca sunucu belirtir. Giriş değerleri: CS, PS.
* InstallLocation: Zorunlu. Merhaba klasör hangi hello bileşenleri yüklenir.
* /MySQLCredsFilePath. Zorunlu. Merhaba dosya yolu hello MySQL sunucusu kimlik bilgileri saklanır. Merhaba dosyası şu biçimde olmalıdır:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Zorunlu. Merhaba kasa kimlik bilgileri dosyası başlangıç konumu
* /EnvType. Zorunlu. yükleme türünü Hello. Değerler: VMware, NonVMware
* /PSIP ve /CSIP. Zorunlu. Merhaba işlem sunucusu ve yapılandırma sunucusu IP adresi Hello.
* /PassphraseFilePath. Zorunlu. Merhaba parola dosyasının başlangıç konumu.
* /BypassProxy. İsteğe bağlı. Bu hello yapılandırma sunucusu Ara sunucu olmadan tooAzure bağlanıp belirtir.
* /ProxySettingsFilePath. İsteğe bağlı. Proxy ayarları (Merhaba varsayılan proxy kimlik doğrulaması ya da özel bir ara sunucu gerektirir). Merhaba dosyası şu biçimde olmalıdır:
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. İsteğe bağlı. Çoğaltma verileri için başlangıç bağlantı noktası numarası.
* SkipSpaceCheck. İsteğe bağlı. Önbellek için alan denetimini atlama.
* AcceptThirdpartyEULA. Zorunlu. Merhaba üçüncü taraf EULA kabul eder.
* ShowThirdpartyEULA. Zorunlu. Üçüncü taraf EULA belgesini görüntüler. Giriş olarak sağlanırsa, diğer tüm parametreler göz ardı edilir.
