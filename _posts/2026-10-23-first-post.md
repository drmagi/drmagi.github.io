---
tags: [Jekyll]
description: Here is my short description of the first post. It basically tests a view functions such as image, video, code, math and Mermaid. This text shows up in the list of posts.
math: true
mermaid: true
image: /assets/img/avatar.png # preview image should have resolution of 1200 x 630. If the aspect ratio does not meet 1.91 : 1, the image will be scaled and cropped
---

# Hello World!

This is my first blog post. 

## Image

I just created the blog with a wonderfull image:

![AI generated content]( /assets/img/avatar.png){: width="300"}
_This is my AI generated avatar picture_

## Video

Have you seen the Tesla Roadster introduction last week? 

{% include embed/youtube.html id='qt5p-_tE8d0' %}

## Code 

Another cool thing, you can formatted code:

```shell
echo 'With line numbers!'
echo 'Here is the 2nd line!'
```

## Math

$$ a^2+b^2=c^2 $$ 

## Mermaid

```mermaid
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

Let's see if all works...
