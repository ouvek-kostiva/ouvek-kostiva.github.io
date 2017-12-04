---
layout: post
title:  "�Q�� Facebook Graph API �s�@��Ѿ����H Chat Bot"
date:   2017-12-04 17:30:00 +0800
---

# �]�w Facebook Developer �}�o�H���b��

### �ڰ��]�A�w�g���@�� Facebook �b���B�w�n�J

### ���Ӭy�{��g��T

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/1.png)

![FB Dev Register](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/2.png)

### ������ӽЫ�A�I�k�W�� New Apps �A�I Add a New App

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/3.png)

### Display Name �O App ���W�١AEmail �O FB �p���ɥΪ��A�ж�A���o��H���H�c

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/4.png)

### ��o�ӭ������I Messenger �U�誺 Set Up

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/6.png)

### Facebook �� Messenger Chatbot �O��M���j�w���A�ҥH�p�G�٨S���M���N�Ф@��

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/7.png)

### ���|�n�D�\�i�A�]���A���b���� App ���ӷ|�N���A���M���^�H

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/8.png)

### ������|���ͤ@�� Page Access Token�A�o�ӬO FB �Ψӿ�O�O�A�{���Ǫ��N��

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/9.png)

### ���U�誺 Setup Webhook �|�X�{�ܦh�ﶵ�A�p�G�u�n�ǰT���M�Ϋ��áA�� messages, messages_postbacks�A�̤U�����ӬO�p�G�Qĵ�i�ɷ|�ǪF�赹�A���{��

### Callback URL �N�O�A�{���|�����T�������}�AVerify Token �O�I�U�U�� Verify and Save �� Facebook �Ǥ@�h GET �T���� Callback URL �A�{�����ӭn�^��

```python

VERIFY_TOKEN = "�N�O Setup Webhook ���̧A�ۤv�񪺪F��"
PAT = "�N�O Page Access Token �����A���@��"

app = Flask(__name__)

@app.route('/', methods=['GET'])
def verify():
    # Once the endpoint is added as a webhook, it must return back
    # the 'hub.challenge' value it receives in the request arguments
    if (request.args.get('hub.verify_token', '') == VERIFY_TOKEN):
        print("Verified")
        return request.args.get('hub.challenge', '')
    else:
        print('wrong verification token')
        return "Error, Verification Failed"
        
if __name__ == '__main__':
    app.run()
```

### �ثe�]���A����Ѿ����H�b�}�o�Ҧ����A�ҥH���F�A�ۤv�S��k�ΡA�p�G�A�n���O�H�]���o������H���T���n�� Roles ���U Roles ���� Test User ���L�H���b���[�i�h�~��

![FB Dev Homepage](https://raw.githubusercontent.com/ouvek-kostiva/ouvek-kostiva.github.io/master/assets/img/post/facebook-bot-api-img/11.png)

### �U�������O�A�{�������ϥΪ̳z�L FB API �ǰT�����A�A�]��b�P�@���ɮ�

# �`�N�GFB �W�L 20 ��S�q�A�{������ OK 200 �N�|����@�U�A���e�A�ҥH�@�w�n�ɧְe�X OK 200

```python
# FB API �� POST ���e�T��
@app.route('/', methods=['POST'])
@app.route('/webhook', methods=['POST'])
def handle_messages():
    data = request.get_json()
    entry = data['entry'][0]
    if entry.get("messaging"):
        messaging_event = entry['messaging'][0]
        sender_id = messaging_event['sender']['id'] # �ϥΪ̪� ID
        timestamp = entry['time'] # �ɶ�
        if messaging_event.get("message"):
            if messaging_event['message'].get('text'):
                text = messaging_event['message']['text'] #�ϥΪ̶Ǫ��T��
                insret = insertRec() ### �ڦb����T����ߨ�N�T�����s���Ʈw
                return 'ok', 200
            if messaging_event['message'].get('sticker_id'):
                if str(messaging_event['message']['sticker_id']) == str(369239263222822): #�p�g�����s
                    insret = insertRec() ### �ڦb����T����ߨ�N�T�����s���Ʈw
                    return 'ok', 200
                elif str(messaging_event['message']['sticker_id']) == str(369239343222814): #���g�����s
                    insret = insertRec() ### �ڦb����T����ߨ�N�T�����s���Ʈw
                    return 'ok', 200
                elif str(messaging_event['message']['sticker_id']) == str(369239383222810): #�j�g�����s
                    insret = insertRec() ### �ڦb����T����ߨ�N�T�����s���Ʈw
                    return 'ok', 200
                return 'ok', 200
            return 'ok', 200
        elif messaging_event.get("postback"):
            if messaging_event['postback'].get('payload'):
                payload = messaging_event['postback']['payload'] #�A�ۤv�]�w�����ê��T��
                insret = insertRec() ### �ڦb����T����ߨ�N�T�����s���Ʈw
                return 'ok', 200
            return 'ok', 200
        else:
            print(messaging_event)
            return 'ok', 200
    return 'ok', 200
```

### �]�w�ϥΪ̲Ĥ@���I�ǰe�T�����M�����w���r�]�o�Ӧb Linux �W�����K�� Bash ����^

```bash
curl -X POST -H "Content-Type: application/json" -d '{
  "setting_type":"greeting",
  "greeting":{
    "text":"�w���r"
  }
}' "https://graph.facebook.com/v2.6/me/thread_settings?access_token=�o��n��A��PageAccessToken"

```

### �]�w�U��|�@����ܪ��`�Ϋ���

```bash
curl -X POST -H "Content-Type: application/json" -d '{
"persistent_menu":[
    {
    "locale":"default",
    "composer_input_disabled":false,
    "call_to_actions":[
        {
        "title":"Sublist Button Text",
        "type":"nested",
        "call_to_actions":[
            {
            "title":"Button 1 Title",
            "type":"postback",
            "payload":"Payload Reply"
            },
            {
            "title":"Button 2 Title",
            "type":"postback",
            "payload":"Payload Reply"
            },
            {
            "title":"Button 3 Title",
            "type":"postback",
            "payload":"Payload Reply"
            },
            {
            "title":"Button 4 Title",
            "type":"postback",
            "payload":"Payload Reply"
            },
            {
            "title":"Button 5 Title",
            "type":"postback",
            "payload":"Payload Reply"
            }
        ]
        },
        {
        "type":"web_url",
        "title":"Website Button Text",
        "url":"https://www.example.com",
        "webview_height_ratio":"full"
        }
    ]
    },
    {
    "locale":"zh_TW",
    "composer_input_disabled":false,
    "call_to_actions":[
        {
        "title":"��h���s",
        "type":"nested",
        "call_to_actions":[
            {
            "title":"���s��r",
            "type":"postback",
            "payload":"��ڦ��쪺�^��"
            },
            {
            "title":"���s��r",
            "type":"postback",
            "payload":"��ڦ��쪺�^��"
            },
            {
            "title":"���s��r",
            "type":"postback",
            "payload":"��ڦ��쪺�^��"
            },
            {
            "title":"���s��r",
            "type":"postback",
            "payload":"��ڦ��쪺�^��"
            },
            {
            "title":"���s��r",
            "type":"postback",
            "payload":"��ڦ��쪺�^��"
            }
        ]
        },
        {
        "type":"web_url",
        "title":"�������s��r",
        "url":"https://www.example.com",
        "webview_height_ratio":"full"
        }
    ]
    }
]
}' "https://graph.facebook.com/v2.6/me/messenger_profile?access_token=�o��n��A��PageAccessToken"
```