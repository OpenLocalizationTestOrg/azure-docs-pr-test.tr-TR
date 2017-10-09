### <a name="create-a-nodejs-application"></a>Node.js uygulaması oluşturma

`listener.js` adlı yeni bir JavaScript dosyası oluşturun.

### <a name="add-hello-relay-npm-package"></a>Merhaba geçiş NPM paket ekleme

Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.

### <a name="write-some-code-tooreceive-messages"></a>Tooreceive iletileri biraz kod yazma

1. Merhaba sabit toohello üstündeki aşağıdaki hello eklemek `listener.js` dosya.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Sabitler toohello aşağıdaki hello eklemek `listener.js` hello karma bağlantı ayrıntılar için. Köşeli ayraçlar Hello yer tutucuları hello karma bağlantıyı oluştururken aldığınız hello değerlerle değiştirin.
   
   1. `const ns`-Geçiş ad alanı hello. Emin toouse hello tam ad alanı adı olmalıdır; Örneğin, `{namespace}.servicebus.windows.net`.
   2. `const path`-hello karma bağlantı hello adı.
   3. `const keyrule`-hello hello SAS anahtarının adı.
   4. `const key`-hello SAS anahtarı değeri.

3. Aşağıdaki kodu toohello hello eklemek `listener.js` dosyası:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Listener.js dosyanız şu şekilde görünmelidir:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

