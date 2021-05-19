---
layout: post
title: "ST3에  Markdown  기능 설치"
date: 2017-03-24 15:48:35 +0900
categories: Rasberry Pi
---

참고사이트 :  https://nolboo.kim/blog/2014/04/15/how-to-use-markdown/ 

### MarkdownEditing 설치

### OmniMarkupPreviewer 설치 및 오류 해결
참고사이트 :  https://www.bountysource.com/issues/28732692-404-error-on-preview-buffer_id-29-is-not-valid-closed-or-unsupported-file-format

"Error: 404 Not Found
Sorry, the requested URL 'http://127.0.0.1:51004/view/29' caused an error:

'buffer_id(29) is not valid (closed or unsupported file format)'

---> 해결  : 어떻게 해결 되었는지 모르겠음 ㅋ
>Quick Fix 1: Remove Strikethrough Extension  
>Sublime Text > Preferences > Package Settings > OmniMarkupPreviewer > Settings - User
paste the following to remove the strikeout package.   
>    {
>     "renderer_options-MarkdownRenderer": {
>            "extensions": ["tables", "fenced_code", "codehilite"]
>      }
>  }  
>Quick Fix 2: Fix the Strikethrough Extension (if you need it)  
>Find the python-markdown sublime package.
>On the Mac: subl "/Users/<username>/Library/Application Support/Sublime Text 3/Packages/OmniMarkupPreviewer/OmniMarkupLib/Renderers/libs/mdx_strikeout.py"
>Replace the makeExtension() method with the following:
>def makeExtension(*args, **kwargs):
    return StrikeoutExtension(*args, **kwargs)
>Save, quit and reload Sublime Text.

###  할일
* 웹페이지에서 내용 일부를 붙이기를 할때 출처 URL이 자동으로 붙은 기능이 있는 거 같은데 어찌 하는 지 모르겠다....
* Markdown 문법 배우기 
* 블로그 만들기 github vs Wordpress
