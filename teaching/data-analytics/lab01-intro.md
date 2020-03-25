# Thông tin chung

**Mục tiêu buổi học**

- Giới thiệu thư viện Beautiful Soup
- Hướng dẫn cài đặt và sử dụng thư viện Beautiful Soup để thu thập thông tin Web.

**Kiến thức và kỹ năng đạt được**

- Nắm vững và sử dụng được các đối tượng trong thư viện Beautiful Soup.
- Áp dụng cài đặt được các bài tập thực hành.

**Công cụ thực hành**

- Ngôn ngữ lập trình: Python
- Công cụ thực hành: Anaconda, colab

**Thời gian thực hành**: 3 tiết

# Nội dung lý thuyết

**Beautiful Soup**

- Là bộ thư viện thu thập dữ liệu từ các trang HTML, XML.
- Hỗ trợ bộ phân tích cú pháp HTML (html.parser), XML (lxml.parser).
- Đơn giản, dễ sử dụng.

Cài đặt thư viện BeautifulSoup
```python
pip install BeautifulSoup4
```

# Nội dung thực hành

## Đọc dữ liệu từ mã nguồn HTML tĩnh


```python
from bs4 import BeautifulSoup
html_doc = """<!DOCTYPE html><html><body><p><a id="link1" 
href="www.3schools.com">www.3schools.com</a><a id="link2" 
href="https://developer.mozilla.org">
https://developer.mozilla.org</a></p><p>This is a paragraph.</p><p>
This is another paragraph</p></body></html>"""
#
soup = BeautifulSoup(html_doc, "html.parser")
```


```python
print(soup.prettify())
```

    <!DOCTYPE html>
    <html>
     <body>
      <p>
       <a href="www.3schools.com" id="link1">
        www.3schools.com
       </a>
       <a href="https://developer.mozilla.org" id="link2">
        https://developer.mozilla.org
       </a>
      </p>
      <p>
       This is a paragraph.
      </p>
      <p>
       This is another paragraph
      </p>
     </body>
    </html>



```python
print(soup.find(id="link1"))
```

    <a href="www.3schools.com" id="link1">www.3schools.com</a>



```python
print(soup.find_all(name="a"))
```

    [<a href="www.3schools.com" id="link1">www.3schools.com</a>, <a href="https://developer.mozilla.org" id="link2">
    https://developer.mozilla.org</a>]



```python
p_tag = soup.p
print(p_tag)
```

    <p><a href="www.3schools.com" id="link1">www.3schools.com</a><a href="https://developer.mozilla.org" id="link2">
    https://developer.mozilla.org</a></p>



```python
a_tag = p_tag.a
print(a_tag)
```

    <a href="www.3schools.com" id="link1">www.3schools.com</a>



```python
print(a_tag.name, a_tag.attrs, a_tag.string)
```

    a {'id': 'link1', 'href': 'www.3schools.com'} www.3schools.com



```python
name_parents_a_tag = [tag.name for tag in a_tag.parents]
print(name_parents_a_tag)
```

    ['p', 'body', 'html', '[document]']



```python
siblings_p_tag = [tag for tag in p_tag.next_siblings]
# siblings_p_tag = list(p_tag.next_siblings)
print(siblings_p_tag)
```

    [<p>This is a paragraph.</p>, <p>
    This is another paragraph</p>]



```python
list_id = [tag.attrs["id"] for tag in p_tag.children]
print(list_id)
```

    ['link1', 'link2']


## Ứng dụng Beautiful Soup thu thập thông tin trang Web

Ví dụ: Lấy thông tin từ các trang báo trực tuyến:


```python
from urllib.request import urlopen

url = "https://vnexpress.net"
html_doc = urlopen(url).read()
soup = BeautifulSoup(html_doc, "html.parser")
# print(soup.prettify())
```


```python

news = soup.find("section", class_="featured container clearfix").find_all("a")
for new in news:
    title = new.get("title")
    link = new.get("href")
    print(f"- {title}, Link: {link}")
```
