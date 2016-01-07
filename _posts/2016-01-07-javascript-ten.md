---
title: ajax 使用模板
description: ajax 使用模板
keywords: ajax 使用模板
category: javascript
---
摘录于 <http://www.w3.org/wiki/JavaScript_best_practices?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io#Don.E2.80.99t_trust_any_data>

    var playercontainer = document.getElementById('easyyoutubeplayer');
    if(playercontainer){
      ajax('template.html');
    }; 
    
    function ajax(url){
      var request;
      try{
        request = new XMLHttpRequest();
      }catch(error){
        try{
          request = new ActiveXObject("Microsoft.XMLHTTP");
        }catch(error){
          return true;
        }
      }
      request.open('get',url,true);
      request.onreadystatechange = function(){
        if(request.readyState == 4){
          if(request.status){ 
            if(request.status === 200 || request.status === 304){
              if(url === 'template.html'){
                setupPlayer(request.responseText);
              }
            }
          }else{
            alert('Error: Could not find template...');
          }
        }
      };
      request.setRequestHeader('If-Modified-Since','Wed, 05 Apr 2006 00:00:00  GMT');
      request.send(null);
    };
