## <a name="create-a-ruby-application"></a><span data-ttu-id="45688-101">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="45688-101">Create a Ruby application</span></span>
<span data-ttu-id="45688-102">Yönergeler için bkz: [Azure üzerinde bir Ruby uygulaması oluşturmak](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="45688-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="45688-103">Uygulama tooUse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="45688-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="45688-104">toouse Service Bus, indirin ve hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir hello Azure Ruby paketini kullanın.</span><span class="sxs-lookup"><span data-stu-id="45688-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="45688-105">RubyGems tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="45688-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="45688-106">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="45688-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="45688-107">"Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.</span><span class="sxs-lookup"><span data-stu-id="45688-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="45688-108">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="45688-108">Import hello package</span></span>
<span data-ttu-id="45688-109">Sık kullandığınız metin düzenleyiciyi kullanarak ekleyin hello Ruby toohello üstündeki aşağıdaki hello toouse depolama düşündüğünüz dosyası:</span><span class="sxs-lookup"><span data-stu-id="45688-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="45688-110">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="45688-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="45688-111">Kullanım hello aşağıdaki kod ad alanı, hello adını tooset hello değerlerini anahtar, anahtar, imzalayan ve ana bilgisayar:</span><span class="sxs-lookup"><span data-stu-id="45688-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="45688-112">Hello tüm URL'yi yerine oluşturulan hello ad alanı değeri toohello değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45688-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="45688-113">Örneğin, **"yourexamplenamespace"**, değil "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="45688-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
