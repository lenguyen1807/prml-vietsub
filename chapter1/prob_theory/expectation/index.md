---
layout: post
title: Expectations and Covariances
mathjax: true
---

Kì vọng (expectation) là một trong nhất concept quan trọng nhất của xác suất. Giá trị trung bình của một hàm biến ngẫu nhiên $f(x)$ nào đó với $x$ có phân phối xác suất $p(x)$ được gọi là **kì vọng** của $f(x)$ và được kí hiệu là $\mathbb{E}[f]$.

- Nếu $x$ là một biến ngẫu nhiên rời rạc thì:

$$
\mathbb{E}[f] = \sum p(x)f(x)
$$

- Ta có thể thấy kì vọng của $f(x)$ với $x$ là biến sẽ là trung bình có trọng số của các giá trị $f(x)$, trong đó trọng số chính là xác suất của các giá trị $x$ khác nhau ($p(x)$).

- Trung bình có trọng số của $(x_1, \dots, x_n)$ với trọng số $(w_1, \dots, w_n)$ sẽ là:

$$
\dfrac{w_{1}x_{1} + \dots + w_{n}x_{n}}{w_{1} + \dots + w_{n}}
$$

- Ở kì vọng của biến ngẫu nhiên rời rạc $x$, ta có trọng số là các xác suất $p(x)$ mà $\sum_{x}p(x) = 1$ do đó mẫu bị triệt tiêu.

- Nếu $x$ là một biến liên tục (khi này $p(x)$ là mật độ xác suất của $x$), ta có:

$$
\mathbb{E}[f] = \int f(x)p(x)dx
$$

- Khi đó kì vọng của $f(x)$ với $x$ là biến liên tục chính là tích phân của $f(x)p(x)$ trên toàn bộ giá trị của $x$ (hay là từ $-\infty$ đến $\infty$).

Vậy nếu $f(x) = x$ thì ta có:
- Rời rạc:

$$
\mathbb{E}[x] = \sum p(x)x
$$

- Liên tục:

$$
\mathbb{E}[x] = \int p(x)xdx
$$

Đây là công thức mà ta thường gặp hơn.

{% include marginnote.html id="expectation-1" note="Để hiểu tại sao có thể xấp xỉ được kì vọng như vậy, ta nên xem cách xấp xỉ tích phân ví dụ như **Monte Carlo Intergration**" %}

Ngoài ra, nếu lấy $N$ điểm ngẫu nhiên $(x_1, \dots, x_n)$ từ phân phối xác suất (nếu $x$ là rời rạc) hoặc mật độ xác suất (nếu $x$ là liên tục) thì ta có thể xấp xỉ giá trị kì vọng bằng cách sau:

$$
\mathbb{E}[f] \simeq \frac{1}{N} \sum_{n=1}^N f(x_{n})
$$

Đôi lúc, ta cũng quan tâm đến kì vọng của một hàm nhiều biến, ví dụ ta có hàm $f(x, y)$ (2 biến) để kí hiệu kì vọng của 1 biến mà ta quan tâm, ví dụ biến ngẫu nhiên $x$, ta sẽ dùng $\mathbb{E}_{x}[f(x, y)]$ (nghĩa là lấy trung bình trên biến $x$).

- Nếu $x, y$ là các biến rời rạc thì:

$$
\mathbb{E}_{x}[f(x, y)] = \sum_{x} f(x, y)p(x, y)
$$

- Nếu $x, y$ là các biến liên tục thì:

$$
\mathbb{E}_{x}[f(x, y)] = \int f(x, y)p(x, y)dx
$$

- Ta có thể thấy ở cả 2 trường hợp trên, $$\mathbb{E}_{x}[f(x, y)]$$ là một hàm theo $y$, vậy khi lấy trung bình của biến nào, kì vọng sẽ phụ thuộc sẽ là hàm của biến còn lại. Tương tự với $\mathbb{E}_{y}[f(x, y)]$.

Vậy nếu ta không phân biệt kì vọng của $x$ hay $y$ thì khi đó:

- Đối với rời rạc:

$$
\mathbb{E}[f(x, y)] = \mathbb{E}_{x, y}[f(x, y)] = \sum_{y} \sum_{x} f(x,y)p(x,y)
$$

- Đối với liên tục:

$$
\mathbb{E}[f(x, y)] = \mathbb{E}_{x, y}[f(x, y)] = \int \int f(x, y)p(x, y)dx dy
$$

Lưu ý rằng, lúc này kì vọng $\mathbb{E}[f(x, y)]$ là một số thực, trong khi đó $$\mathbb{E}_{x}[f(x, y)]$$ hay $\mathbb{E}_{y}[f(x, y)]$ là một hàm phụ thuộc vào biến còn lại.

Ngoài ra, ta cũng quan tâm đến **kì vọng có điều kiện** (conditional expectation) của một hàm $f(x)$ trong đó $x$ có phân phối điều kiện là $p(x \mid y)$.

- Nếu $x$ là biến rời rạc:

$$
\mathbb{E}_{x}[f(x) \mid y] = \sum_{x} p(x \mid y)f(x)
$$

- Tương tự với $x$ là biến liên tục:

$$
\mathbb{E}_{x}[f(x) \mid y] = \int p(x \mid y) f(x) dx
$$

- Ta có thể thấy, ở hai trường hợp trên kì vọng có điều kiện $\mathbb{E}[f(x) \mid y]$ là một hàm phụ thuộc vào $y$.

{% include marginnote.html note="Một điểm đáng chú ý như ta đã nói ở trên, tại sao sự khác nhau giữa $f(x)$ và trung bình của nó lại lấy bình phương mà sao không lấy cách khác (ví dụ dùng giá trị tuyệt đối), có thể tìm hiểu thêm tại [definition - Why square the difference instead of taking the absolute value in standard deviation? - Cross Validated (stackexchange.com)](https://stats.stackexchange.com/questions/118/why-square-the-difference-instead-of-taking-the-absolute-value-in-standard-devia)."%}

**Phương sai** (variance) của hàm $f(x)$ với $x$ là biến ngẫu nhiên được kí hiệu là $\text{var}[f]$ và được định nghĩa như sau:

$$
\text{var}[f] = \mathbb{E}[(f(x) - \mathbb{E}[f(x)])^2]
$$

Có thể thấy, $\text{var}[f]$ là đại lượng cho thấy độ biến thiên (sự khác nhau) giữa giá trị $f(x)$ và trung bình $\mathbb{E}[f(x)]$ của nó (sự khác nhau $= (f(x) - \mathbb{E}[f(x)])^2$). Ngoài ra ta có thể viết:

{% include marginnote.html note="Công thức này được chứng minh ở bài 1.5 [Exercises](../exercises_1/)" %}

$$
\text{var}[f] = \mathbb{E}[f(x)^2] - \mathbb{E}[f(x)]^2
$$

Xét hai biến ngẫu nhiên $x$ và $y$, ta định nghĩa **hiệp phương sai** (covariance) của $x$ và $y$ là:

{% include marginnote.html note="Công thức này được chứng minh ở bài 1.6 [Exercises](../exercises_1/)" %}

$$
\begin{aligned}
\text{cov}[x, y] &= \mathbb{E}_{x, y} [\{x - \mathbb{E}[x])(y - \mathbb{E}[y]\}] \\
&= \mathbb{E}_{x, y}[xy] - \mathbb{E}[x]\mathbb{E}[y]
\end{aligned}
$$

Giả sử $x$ và $y$ là hai biến ngẫu nhiên liên tục độc lập với nhau (rời rạc ta làm tương tự), tức là $p(x, y) = p(x)p(y)$. Khi đó:

$$
\begin{aligned}
\mathbb{E}_{x, y}[xy] &= \int \int p(x, y) \hspace{3pt} xy \hspace{3pt}  dx dy \\
&= \int \int p(x)p(y) \hspace{3pt} xy \hspace{3pt} dx dy \\
&= \int p(y)y \left[ \int p(x)xdx \right] dy \\
&= \int p(y)y \left[ \mathbb{E}[x] \right]dy \\
&= \mathbb{E}[x] \int p(y)y dy\\
&= \mathbb{E}[x] \mathbb{E}[y]
\end{aligned}
$$

Do đó $\text{cov}[x, y] = 0$. Vậy nếu hai biến ngẫu nhiên $x$ và $y$ độc lập với nhau thì hiệp phương sai của $x$ và $y$ là $0$.

Nếu ta xét hiệp phương sai giữa hai vector ngẫu nhiên $\mathbf{x} = (x_1, x_{2} \dots)$ và $\mathbf{y} = (y_{1}, y_{2}, \dots)$. Ta có:

$$
\begin{aligned}
\text{cov}[\mathbf{x}, \mathbf{y}] &= \mathbb{E}[(\mathbf{x} - \mathbb{E}[\mathbf{x}])(\mathbf{y} - \mathbb{E}[\mathbf{y}])] \\
&= \mathbb{E}_{\mathbf{x}, \mathbf{y}}[\mathbf{x}\mathbf{y}^T] + \mathbb{E}[\mathbf{x}]\mathbb{E}[\mathbf{y}^T]
\end{aligned}
$$

Nếu ta xét hiệp phương sai giữa biến ngẫu nhiên $x$ với chính nó, ta có thể viết $\text{cov}[x]$ thay cho $\text{cov}[x, x]$. Tương tự với vector ngẫu nhiên $\mathbf{x}$, $\text{cov}[\mathbf{x}, \mathbf{x}] \equiv \text{cov}[\mathbf{x}]$.

<br/>

|[Previous](../density/) | [Next]()|