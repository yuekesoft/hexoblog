---
title: Delphi 字符转义处理
date: 2021-01-20 14:41:37
tags:
categories:	Delphi相关
---

```
function EscapeStr(const SourceStr: ansistring): ansistring;
var
   len,j: integer;
begin
   result:='';
   len:=length(SourceStr);
   j:=1;
   while j<=len do
      begin
         if SourceStr[j]=#13 then
            result:=result+'\r'               {回车}
         else if SourceStr[j]=#10 then
            result:=result+'\n'               {换行}
         else if SourceStr[j]=#9 then
            result:=result+'\t'               {水平制表}
         else if SourceStr[j]=#12 then
            result:=result+'\f'               {换页}
         else if SourceStr[j]=#7 then
            result:=result+'\a'               {响铃}
         else if SourceStr[j]=#8 then
            result:=result+'\b'               {退格}
         else if SourceStr[j]=#11 then
            result:=result+'\v'               {垂直制表}
         else if SourceStr[j]='\' then
            result:=result+'\\'               {斜杠}
         else if SourceStr[j]='"' then
            result:=result+'\"'               {双引号}
         else if SourceStr[j]='''' then
            result:=result+'\'''              {单引号}
         else if SourceStr[j]='?' then
            result:=result+'\?'               {问好}
         else if SourceStr[j]=#0 then
            result:=result+'\0'               {空字符}
         else
            begin
               if SourceStr[j]<' ' then
                  result:=result+'\x'+inttohex(ord(SourceStr[j]),2)
               else
                  result:=result+SourceStr[j];
            end;
         inc(j);
      end;
end;

//
// 字符串反转义处理...
function UnescapeStr(const SourceStr: ansistring): ansistring;
var
   len,j: integer;
begin
   result:='';
   len:=length(SourceStr);
   j:=1;
   while j<len do
      begin
         //
         // 可能转义符...
         if SourceStr[j]='\' then
            begin
               inc(j);
               case SourceStr[j] of
                  'r': result:=result+#13;
                  'n': result:=result+#10;
                  't': result:=result+#9;
                  'f': result:=result+#12;
                  'a': result:=result+#7;
                  'b': result:=result+#8;
                  'v': result:=result+#11;
                  '\': result:=result+'\';
                  '"': result:=result+'"';
                  '''': result:=result+'''';
                  '?': result:=result+'?';
                  '0': result:=result+#0;
                  'x': begin
                          if j<=(len-2) then
                             begin
                                result:=result+chr(strtoint('$'+string(copy(SourceStr,j+1,2))));
                                j:=j+2;
                             end
                          else
                             result:=result+'\'+SourceStr[j];
                       end;
                  else
                     result:=result+'\'+SourceStr[j];
               end;
            end
         //
         // 不是转义符...
         else
            result:=result+SourceStr[j];
         inc(j);
         if j=len then
            result:=result+SourceStr[j];
      end;
end;

```
