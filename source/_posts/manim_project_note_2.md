---
title: Note 2 for Manim Project
date: 2023-09-30
updated:
tags:
- Manim 
- Python
categories:
- lecture notes
keywords:
description:
top_img: 'linear-gradient(to right, #2c3e50, #4ca1af)'
comments:
cover: /img/manim_logo.png
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author: Albert Zhao
copyright_author_href: https://github.com/pengies
copyright_url:  
copyright_info:
mathjax: false
katex: true
aplayer:
highlight_shrink:
aside:
---

# Lesson 2 - Text
## Table of Contents
1. [Recap](#recap)
2. [LaTeX](#LaTeX)
3. [Text in Manim](#text-in-manim)
4. [Modifying Text](#modifying-text)
5. [Examples](#examples)
6. [More Resources](#more-resources)


## Recap
In our previous lesson, we covered how to install and create a basic animation using geometric shapes in Manim.

 However, our animation is missing something *very* important... **text!**
 
In this lesson, we'll answer:
- How do we add text in Manim?
- How can we use LaTeX to make equations?
- How do we *animate* text?
- What are some examples of text being used?
- and much more!

Before starting, make sure you've installed [Manim](https://www.manim.community/) and a [LaTeX distribution](https://miktex.org/).

> Remember, if you're ever confused about anything in Manim or Python, refer to the [Manim documentation](https://docs.manim.community/en/stable/index.html), [Python documentation](https://docs.python.org/3/), or just Google it! 

Now, ***let's get started!***

## LaTeX
Before we start inputting text into Manim, we need to get familiar with the primary way to write digital mathematical statements: $\textbf{\LaTeX}$.

If you're already familar with $\LaTeX$, feel free to skip to [Text in Manim](#text-in-manim). Otherwise, here are the basics:

### The Basics
 $\LaTeX$ is a markup language used for creating mathematical and scientific documents. 

To write equations in $\LaTeX$, you must first enter ***math mode***. This can be done by surrounding the desired area with a `$` on both sides. 
```latex
This is normal text. 
I can't write good equations here :(

$This is text in math mode! 
Hooray!$
```

The above code renders as:
>This is normal text. 
I can't write good equations here :(
>
>$This is text in math mode! 
Hooray!$

As you can see, the resulting snippet inside math mode doesn't look the best. That's because $\LaTeX$'s focus on math extends to regular words too, resulting in every character being interpreted in variable font. 

Let's write some more appropriate text:

```latex
2x + 2y = 2(x+y)

$2x + 2y = 2(x+y)$
```
This is rendered as:
> 2x + 2y = 2(x+y)
> $2x + 2y = 2(x+y)$

### Special Symbols and Functions

That looks so much better! However, it's nothing that special... yet. $\LaTeX$ has the ability to render special characters, such as $\pm$, $\pi$, $\gamma$, $\alef$, $\frac{1}{2}$, $\sqrt{3}$, $\char"263a$, and [*more*](https://tug.ctan.org/info/symbols/comprehensive/symbols-a4.pdf).

To use a symbol, type `\` and then the symbol's name in math mode. To use a function, type `\`, its name, and any inputs it needs. Here are some examples:

---
$\pi = 3.141592\ldots$
```latex
$\pi = 3.141592\ldots$
```
---
$\sqrt{a + b} \neq \sqrt{a} \cdot \sqrt{b}$
```latex
$\sqrt{a + b} \neq \sqrt{a} \cdot \sqrt{b}$
```
---
$(a+b)^n = \sum^n_{i=0} {n\choose{i}}a^ib^{n-i}$
```latex
$(a+b)^n = \sum^n_{i=0} {n\choose{i}}a^ib^{n-i}$
```
---

### Conclusion
That about wraps it up for the basics. If you're interested in learning more about $\LaTeX$, I recommend using [Overleaf](https://www.overleaf.com/) to live render your code and refer to their [online $\LaTeX$ docs](https://www.overleaf.com/learn).

Anyways, let's get into **Manim**...

## Text in Manim
In Manim, Text is writing using the `Text`, `MathText`, and `Tex` objects. 

### `Text`
The `Text` object is used for plain text and cannot use $\LaTeX$ formatting. This is used mainly just to write sentences, such as:
```py
from manim import *  
  
class Text(Scene):        
	def construct(self):  
		text = Text("Can we add apples and oranges together?")
		self.add(text)
```

![Text](/img/manim/lesson_2/text.png)

### `MathTex`
The `MathTex` object is used for mathematical equations and uses  $\LaTeX$. This can be used for inputting equations into an animation.
```py
from manim import *

class Test(Scene):
    def construct(self):
        math_text = MathTex("a^2 + b^2 = \pm \pi")
        self.add(math_text)
```

![MathTex](/img/manim/lesson_2/mathtext.png)

### `Tex`
The `Tex` object is a mix of the `Text` and `MathTex` objects. `Tex` can write both plain text *and* $\LaTeX$.
> By default, `Tex` writes in plain text.
> To use $\LaTeX$, surround the desired region with **`$`**.
```py
from manim import *

class Test(Scene):
    def construct(self):
        tex = Tex("Apples and Oranges: $a^2 + b^2 = \pm \pi$, I think...")
        self.add(tex)
```

![Tex](/img/manim/lesson_2/tex.png)

> **Important:** 
> All Manim text can be written as chunks instead of one singular string. For example, the below snippets perform the same action:
> ```py
> Tex("This is written in chunks ($\LaTeX$ works too!)" )
> ```
>
> ```py
> Tex("This is", "written ", "i", "n", " chunks ($\LaTeX$ works too!)" )
> ```
>
> This is used to modify specific chunks of a Text object.

## Modifying Text
Text in Manim can be modified in a *lot* of ways, but there's two main ways to do so.

### During Initialization
During the creation of a Text object, you can directly pass in arguments for the object's variables. A Text object's variables are its individual traits, which includes (but is not limited to):
 - Font Size (`font_size`)
 - Color (`color`)
 - Fill Opacity (`fill_opacity`)
 - Slant (`slant`)
 - Line Spacing (`line_spacing`)
 - [and many many more...](https://docs.manim.community/en/stable/reference/manim.mobject.text.text_mobject.Text.html)
 
This can be done by passing in more arguments when initializing the object. In other words:

| No Modifications | Modifications |
|---|-------|
|`Tex("orange")`|`Tex("orange", color = ORANGE, font_size = 92, ...)`|
|![normal-orange](/img/manim/lesson_2/orange_normal.png)|![not-normal-orange](/img/manim/lesson_2/orange_special.png) |
 

### After Initialization
The second way to modify text in Manim is by calling **methods** of the text object. A **method** is a function that can only be run with a specific type of object. In this case, we'll be using some special methods of the `Text`, `Tex`, and `MathTex` objects.

Using these methods, you can change any of the variables similar to during initialization, but are also exclusively able to:
- Move Text (`.shift()`)
- Scale Text (`.scale()`)
- Change Colors of Specific Words (`.set_color_by_tex()`)

> Many custom Manim variables and functions take special inputs, such as the vectors `UP` and `RIGHT` in `.scale(UP, RIGHT)` or `YELLOW` in `color = YELLOW`.
> 
> These special inputs may not be common knowledge, and we recommend you look at some examples and projects to get accustomed to them.

Although methods are used for altering objects after their creation, they are also able to be used during initialization.
The following two snippets produce the same result:
```py
from manim import *

class Test(Scene):
    def construct(self):
        text = Text("Hey There!")
        text.shift(UP * 3)
        text.scale(2)
        self.add(text)
```
```py
from manim import *

class Test(Scene):
    def construct(self):
        text = Text("Hey There!").shift(UP * 3).scale(2)
        self.add(text)
```

![hey-there](/img/manim/lesson_2/heythere.png)
## Animations
`Text` objects in Manim can be animated, like any other Manim object. You're able to use any general animation with Text, but also the exclusive `Write` animation, which looks like this:

{% raw %}
<video src="/img/manim/lesson_2/Write.mp4" type='video/mp4' controls='controls' width='100%' height='100%'/></video>
{% endraw%}

> For advanced users, you're able to create your *own* custom animations. If you're interested in doing so, check out [this article](https://docs.manim.community/en/stable/tutorials/building_blocks.html#creating-a-custom-animation).

## Examples
That's about it for the basics of Text in Manim! I hope you've learned a thing or two from this post. 

To end off, Manim, like any other new tool, requires **lots and lots of practice**. So, here's a few examples of Text being used in Manim:

---
### Positioning Text
```py
from manim import *

class Test(Scene):
    def construct(self):
        formula = MathTex("a^2 + b^2 = c^2")    # LaTeX is supported
        text_with_formula = Tex("if $a=3, b=4$, then $c=5$").next_to(formula, DOWN)
                                        # texts can be mixed in with LaTeX
        self.add(formula, text_with_formula)    # Add the formulas to the scene
```
![ex-1](/img/manim/lesson_2/ex1.png)
---
### Set Colors
```py
from manim import *

class Test(Scene):
    def construct(self):
        formula = MathTex("a^2", "+", "b^2", "=", "c^2")
                                # split the equation into 5 parts
        formula[0].set_color(RED) # and you can edit each part separately
        formula[2].set_color(BLUE)
        formula[4].set_color(GREEN)
        self.add(formula)
```
![ex-2](/img/manim/lesson_2/colored_equation.png)
---
### Set Colors + Transform
```py
from manim import *

class Test(Scene):
    def construct(self):
        formula = MathTex("a^2", "+", "b^2", "=", "c^2")
                                 # split the equation into 5 parts
        formula[0].set_color(RED) # and you can edit each part separately
        formula[2].set_color(BLUE)
        formula[4].set_color(GREEN)
        self.add(formula)
        self.play(Transform(formula[0], MathTex("3^2").scale(2).move_to(formula[0])))
        self.wait(1)
        self.play(Transform(formula[2], MathTex("4^2").scale(2).move_to(formula[2])))
        self.wait(1)
        self.play(Transform(formula[4], MathTex("5^2").scale(2).move_to(formula[4])))
        self.wait(1)
```
{% raw %}
<video src="/img/manim/lesson_2/ColorTransform.mp4" type='video/mp4' controls='controls' width='100%' height='100%'/></video>
{% endraw%}

---
### Set Colors Efficiently
```py   
from manim import *

class Test(Scene):
    def construct(self):
        formula = MathTex(
        "a", "^2", "-", "b", "^2", "=(", "a", "-", "b", ")^2"
        ).set_color_by_tex("a", BLUE).set_color_by_tex("b", GREEN).scale(2)
        self.add(formula)
```

![ex-4](/img/manim/lesson_2/color_special.png)


## More Resources

- [Overleaf](https://www.overleaf.com/) - (Online $\LaTeX$ editor)
- [Manim - Text & LaTeX Equations](https://www.youtube.com/watch?v=Ncct3cUqtkE) - (Informative Video)
