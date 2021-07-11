---
layout: post
title: Telegram机器人学习
date: 2021-7-11
categories: blog
tags: [Javascript,Telegram,Bot]
description: 菜鸟试水中
---

    看完赛马娘以后有些魔怔（铃鹿实在是太可爱了啊啊啊啊啊啊啊啊啊啊啊啊），虽然去不了二次元，但是不代表我不能自己写Bot自我满足啊lmao（参考屑清水的某个陈年Project），于是就跟着油管某up边研究JS边写bot。
    具体操作仅仅只是通过GoogleScript实现Webhook托管罢了。
    参考视频：https://www.dengnz.com/

    代码如下：
    <code>function doPost(e){
  var dataFromTelegram = {
    "method": "post",
    "payload": e.postData.contents
  }
  var body = JSON.parse(e.postData.contents);
   
  body.message.chat.id = body.message.chat.id + '';
 
  var payload = preparePayload(body);
  var data = {
    "method": "post",
    "payload": payload
  }
   
  var dataToTelegram = {
    "method": "post",
    "payload": payload
  }
 
  UrlFetchApp.fetch("https://api.telegram.org/bot1897099308:AAHGkQrcTB0q0u_W01riCe9Cs3HA6_AlrII/", data);
}
function preparePayload(body){
  var payload;
   
  if (body.message.text){
   
      payload = {
        "method": "sendMessage",
        "chat_id": body.message.chat.id,
        "text": "Developing",
      } 
       
      if(body.message.text.indexOf("/help") === 0){      
         payload.text = "Still developing.";
         return payload;
      }
       
      if(body.message.text.indexOf("/self_introduction") === 0){   
         payload.text = "私言葉少なで物静か。チームスピカに移籍からは本領発揮。得意戦法はスタートダッシュから終始先頭に立ち、ひたすら逃げ続ける大逃げ。私の目標は、観ている人に夢を与えられるようなウマ娘だという。";        
         return payload;
      }

      if(body.message.text.indexOf("Who are you") === 0){   
         payload.text = "Spicaチームのサイレンススズカです。";        
         return payload;
      }

      if(body.message.text.indexOf("hi") === 0){   
         payload.text = "おはよう，トレーナーさん";        
         return payload;
      }

      if(body.message.text.indexOf("come on") === 0){   
         payload.text = "トレーナーさんが私の走りを 信してくださるなら、私も自信を 持ってこの走りを贯けます。";        
         return payload;
      }

       if(body.message.text.indexOf("/elements_of_statement_library") === 0){   
         payload.text = "Who are you\nhi\ncome on\nabout short distance\n";        
         return payload;
      }

      if(body.message.text.indexOf("about short distance") === 0){   
         payload.text = "短距離のコツをタイキに聞いたら [工ンジョイスビリツッテース☆] って・・・何もわからない・・・ ";        
         return payload;
      }

      if(body.message.text.indexOf("/blog") === 0){   
         payload.text = "shimizuskt.icu";        
         return payload;
      }
   
      payload = {
          "method": "sendMessage",
          "chat_id": body.message.chat.id,
          "text": body.message.text,
      } 
     
  }
  else if (body.message.sticker){
    payload = {
      "method": "sendSticker",
      "chat_id": body.message.chat.id,
      "sticker": body.message.sticker.file_id
    }
   }
  else if (body.message.photo){
    array = body.message.photo;
    text = array[1];
    payload = {
      "method": "sendPhoto",
      "chat_id": body.message.chat.id,
      "photo": text.file_id
    }
   }
    else {
    payload = {
      "method": "sendMessage",
      "chat_id": body.message.chat.id,
      "text": "Try other stuff"
    }
   }
  return payload
}</code>













