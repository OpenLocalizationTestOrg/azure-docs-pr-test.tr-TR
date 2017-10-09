## <a name="create-a-ruby-application"></a>Ruby uygulaması oluşturma
Yönergeler için bkz: [Azure üzerinde bir Ruby uygulaması oluşturmak](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama tooUse Service Bus yapılandırın
toouse Service Bus, indirin ve hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir hello Azure Ruby paketini kullanın.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).
2. "Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Sık kullandığınız metin düzenleyiciyi kullanarak ekleyin hello Ruby toohello üstündeki aşağıdaki hello toouse depolama düşündüğünüz dosyası:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Hizmet veri yolu bağlantı kurma
Kullanım hello aşağıdaki kod ad alanı, hello adını tooset hello değerlerini anahtar, anahtar, imzalayan ve ana bilgisayar:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Hello tüm URL'yi yerine oluşturulan hello ad alanı değeri toohello değerini ayarlayın. Örneğin, **"yourexamplenamespace"**, değil "yourexamplenamespace.servicebus.windows.net".
