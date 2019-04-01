# Data Source from web

>It's time to start pulling data from various web sources. The difficulty of collecting data depends a great deal on the permissions and services available for a site or page.

##REST API

**REST** is an acronym for _REpresentational State Transfer_ and is a very handy way to make something trivial sound very complicated. Anytime you see the word REST, just think "webpage that gives me data not HTML." There is a massive industry and giant following behind this term but I don't see anything beyond "fetch data from webpage".

Anyway, we are going to pull data from web servers that intentionally provide nice data spigot URLs. Information you need in order to get data is typically:

- Base URL, including machine name, port number, and "file" path
- The names and values of parameters
- What data comes back and in what format \(XML, JSON, CSV, ...\)

There is a REST data API available at URL template:

```text
URL = "http://openpayments.us/data?query=%s"
```

Data Source from Web

