---
layout: post
title: "[spring]oracle 파일 저장"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-03T23:20:00-04:00
modified: 2021-11-03T23:20:00-04:00
---

# spring oracle에 첨부파일 저장하기
org.springframework.web.multipart.MultipartFile.getBytes()

LONGBLOB

## ORACLE CREATE TABLE
```
CREATE TABLE TEST1(
  ID INT auto_increment primary key,
  FILENAME VARCHAR(100),
  FILE LONGBLOB,
  SIZE INT
);
```

## pom.xml
```
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.4</version>
</dependency>
```

## root-context.xml
```
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```

## .jsp
```
<form ... enctype="multipart/form-data">
  <input type="file" name="uploadFile" multiple="multiple">
</form>
```

## Controller.java
```
import org.springframework.web.multipart.MultipartFile;
@RequestParams("uploadFile") MultipartFile[] files

for(int i=0;i<files.length;i++){
  files[i].getOriginalFilename(); //파일명
  files[i].getBytes(); //파일
  files[i].getSize(); //크기
}
```

## SQL.xml
```
INSERT INTO TABLE(......) VALUES(
   files[i].getOriginalFilename() --VARCHAR2(200)
  ,files[i].getBytes() --BLOB
  ,files[i].getSize() --NUMBER(12)
);
```
- - -
# oracle에 저장했던 파일 다운로드

## SQL.xml
```
SELECT
   filename //String
  ,file //byte[]
  ,filesize //long
FROM TABLE;
```

## Controller.java
```
//쌩 File객체를 byte로 바꾸기
//byte[] file = FileUtils.readFileToByteArray(new File(path+ "/" +fileStrNm));

//IE 버전 별 체크 >> Trident/7.0(IE 11), Trident/6.0(IE 10) , Trident/5.0(IE 9) , Trident/4.0(IE 8)
String userAgent = request.getuserAgent("User-Agent");
if (userAgent.indexOf("MSIE") > -1 || userAgent.indexOf("Trident") > -1 ){//return "MSIE";
  encodedFilename = URLEncoder.encode(filename, "UTF-8").replaceAll("\\+", "%20");
} else if (userAgent.indexOf("Chrome") > -1) {//return "Chrome";
  StringBuffer sb = new StringBuffer();
  for (int i = 0; i < filename.length(); i++) {
    char c = filename.charAt(i);
    if (c > '~') {
      sb.append(URLEncoder.encode("" + c, "UTF-8"));
    } else {
      // ASCII문자(0X00 ~ 0X7E)는 URLEncoder.encode를 적용하지 않는다. 
      sb.append(c);
    }
  }
  encodedFilename = sb.toString();
} else if (userAgent.indexOf("Opera") > -1) {//return "Opera";
  encodedFilename = "\"" + new String(filename.getBytes("UTF-8"), "8859_1") + "\"";
} else if ( userAgent.indexOf("Firefox") > -1 ) {//return "Firefox";
  encodedFilename = "\"" + new String(filename.getBytes("UTF-8"), "8859_1") + "\"";
}else{//return "Safari";

}

res.setContentType("application/octet-stream");
res.setContentLength(file.length);
res.setHeader("Content-Disposition", "attachment; fileName=\"" +encodedFileName +"\";");
res.setHeader("Content-Transfer-Encoding", "binary");
res.getOutputStream().write(file);

res.getOutputStream().flush();
res.getOutputStream().close();
```
