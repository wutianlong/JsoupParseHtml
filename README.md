# Jsoup
Jsoup解析html,获取数据显示在资讯客户端

### 效果图
<img src="https://github.com/wutianlong/JsoupParseHtml/blob/master/jsoup_parse_html_phone_screencap.png">

### 网页HTML源码
<img  src="https://github.com/wutianlong/JsoupParseHtml/blob/master/html_source_codes.png">

### Android 源码

```
String htmlStr = DataUtil.doGet(url);
        NewsItem item = null;
        Document doc = Jsoup.parse(htmlStr);
        Elements units = doc.getElementsByClass("unit");
        for (int i = 0; i < units.size(); i++) {
            item = new NewsItem();
            item.setNewsType(newsType);

            Element unit = units.get(i);
            Element h1 = unit.getElementsByTag("h1").get(0);
            Element ha = h1.child(0);
            item.setTitle(h1.text());
            item.setLink(ha.attr("href"));

            Element h4 = unit.getElementsByTag("h4").get(0);
            Element ago = h4.getElementsByClass("ago").get(0);
            item.setDate(ago.text());

            Element dl_ele = unit.getElementsByTag("dl").get(0);
            Element dt_ele = dl_ele.child(0);

            try {  // 可能没有图片
                Element img_ele = dt_ele.child(0);
                String imgLink = img_ele.child(0).attr("src");
                item.setImgLink(imgLink);
            } catch (IndexOutOfBoundsException e) {
            }

            Element dd_ele = dl_ele.child(1);
            item.setContent(dd_ele.text());
            newsItems.add(item);
        }
```

### License

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```