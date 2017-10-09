### <a name="create-a-nodejs-application"></a>Node.js uygulaması oluşturma

`sender.js` adlı yeni bir JavaScript dosyası oluşturun.

### <a name="add-hello-relay-npm-package"></a>Merhaba geçiş NPM paket ekleme

Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.

### <a name="write-some-code-toosend-messages"></a>Toosend iletileri biraz kod yazma

1. Merhaba aşağıdakileri ekleyin `constants` hello toohello üstündeki `sender.js` dosya.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Sabitler toohello aşağıdaki hello eklemek `sender.js` hello karma bağlantı ayrıntılar için. Köşeli ayraçlar Hello yer tutucuları hello karma bağlantıyı oluştururken aldığınız hello değerlerle değiştirin.
   
   1. `const ns`-Geçiş ad alanı hello. Emin toouse hello tam ad alanı adı olmalıdır; Örneğin, `{namespace}.servicebus.windows.net`.
   2. `const path`-hello karma bağlantı hello adı.
   3. `const keyrule`-hello hello SAS anahtarının adı.
   4. `const key`-hello SAS anahtarı değeri.

3. Aşağıdaki kodu toohello hello eklemek `sender.js` dosyası:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Sender.js dosyanız aşağıdaki gibi görünmelidir:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

