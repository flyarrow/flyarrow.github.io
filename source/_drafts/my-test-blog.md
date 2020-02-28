---
title: my test blog
tags:
description: 这是一篇说明
---
## 常用链接
### [阅读数量](https://www.jianshu.com/p/27b971d84f76)
## 试下代码块

```javascript
function get2SKJson() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var shtSK = ss.getSheetByName("技能json");
  var shtEQ = ss.getSheetByName("装备json");
<!--more-->  
  var lr = shtSK.getRange("a1").getDataRegion(SpreadsheetApp.Dimension.ROWS).getLastRow();
  var acSK = shtSK.getRange("a3:c"+lr).getValues();
  var arSK = acSK[0].map(function(col,i){
    return acSK.map(function(row){
      return row[i];
    });
  });
  
  /*产生所有神器装备的json*/
  
  var jsonEQ = "";
  var catEQ = "2-神器";
  
  for (var i=0;i<arSK[0].length;i++){
    
    if (arSK[0][i] == catEQ) {
      jsonEQ += "{\n\t\"id\": " + arSK[1][i] + ", //技能ID\n" + 
             "\t\"name\": \"" + arSK[2][i] + "\",\n" +
             "\t\"type\": 3,// 1-主,2-必选,3-主要,4次要\n" + 
             "\t\"franction\": 5 //占比\n" + "},";
    }
  
  }
  
  /*去掉最后一个逗号*/
  jsonEQ = jsonEQ.slice(0,-1);
  return jsonEQ;
  
  //shtEQ.getRange("d18").setValue(jsonEQ);
  
}
```

