---
layout: post
title:  "Welcome to Jekyll!"
date:   2020-06-11 10:05:21 +0800
categories: jekyll update
---

> In this series of posts :tent: on "Object Detection for Dummies", we will go through several basic concepts, algorithms, and popular deep learning models for image processing and objection detection. Hopefully, it would be a good read for people with no experience in this field but want to learn more. The Part 1 introduces the concept of Gradient Vectors, the HOG (Histogram of Oriented Gradients) algorithm, and Selective Search for image segmentation.


<!--more-->

{: class="table-of-content"}
* TOC
{:toc}

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/


## Markdown Test
### Test latex

$$
\textit{Hello} = \frac{1}{n}
$$

$$
\begin{align*}
\nabla f
= \begin{bmatrix}
  f(x+1, y) - f(x-1, y)\\
  f(x, y+1) - f(x, y-1)
\end{bmatrix}
= \begin{bmatrix}
  55-105\\
  90-40
\end{bmatrix}
= \begin{bmatrix}
  -50\\
  50
\end{bmatrix}
\end{align*}
$$

### List
- df
- dfdff
- dfsl

### Table List
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

### Code
```python
# Random location [200, 200] as an example.
loc_x = loc_y = 200

ydata = get_magnitude_hist_block(loc_x, loc_y)
ydata = ydata / np.linalg.norm(ydata)

xdata = range(len(ydata))
bucket_names = np.tile(np.arange(N_BUCKETS), BLOCK_SIZE * BLOCK_SIZE)

assert len(ydata) == N_BUCKETS * (BLOCK_SIZE * BLOCK_SIZE)
assert len(bucket_names) == len(ydata)

plt.figure(figsize=(10, 3))
plt.bar(xdata, ydata, align='center', alpha=0.8, width=0.9)
plt.xticks(xdata, bucket_names * 20, rotation=90)
plt.xlabel('Direction buckets')
plt.ylabel('Magnitude')
plt.grid(ls='--', color='k', alpha=0.1)
plt.title("HOG of block at [%d, %d]" % (loc_x, loc_y))
plt.tight_layout()
```

```python
import numpy as np
import scipy
import scipy.signal as sig
# With mode="L", we force the image to be parsed in the grayscale, so it is
# actually unnecessary to convert the photo color beforehand.
img = scipy.misc.imread("manu-2004.jpg", mode="L")

# Define the Sobel operator kernels.
kernel_x = np.array([[-1, 0, 1],[-2, 0, 2],[-1, 0, 1]])
kernel_y = np.array([[1, 2, 1], [0, 0, 0], [-1, -2, -1]])

G_x = sig.convolve2d(img, kernel_x, mode='same')
G_y = sig.convolve2d(img, kernel_y, mode='same')

# Plot them!
fig = plt.figure()
ax1 = fig.add_subplot(121)
ax2 = fig.add_subplot(122)

# Actually plt.imshow() can handle the value scale well even if I don't do
# the transformation (G_x + 255) / 2.
ax1.imshow((G_x + 255) / 2, cmap='gray'); ax1.set_xlabel("Gx")
ax2.imshow((G_y + 255) / 2, cmap='gray'); ax2.set_xlabel("Gy")
plt.show()
```

### Image
![Block histogram]({{ '/assets/images/block_histogram.png' | relative_url }})
{: class="center"}
*Fig. 5. Demonstration of a HOG histogram for one block.*

### Link
[paper](www.google.com)

### Table

{:class="table table-bordered"}
| Tex Space     | Blue Space        | Lambda            |
|-------------- |----------------   |------------------ |
| sXYZ          | sBlue             | sXYZ abcde fghy   |
| Jaobe XTZ     | Blue Game 5.2     | 5.2               |

|            | **Derivative** | **Directional Derivative** | **Gradient** |
| Value type | Scalar | Scalar | Vector |
| Definition | The rate of change of a function $$f(x,y,z,...)$$ at a point $$(x_0,y_0,z_0,...)$$, which is the slope of the tangent line at the point. | The instantaneous rate of change of $$f(x,y,z, ...)$$ in the direction of an unit vector $$\vec{u}$$. | It points in the direction of the greatest rate of increase of the function, containing all the partial derivative information of a multivariable function. |
{:.info}

### Footnote
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.