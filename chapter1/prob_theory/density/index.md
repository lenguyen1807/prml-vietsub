---
layout: post
title: Probability Densities
mathjax: true
---

{% include marginnote.html id="mn_density_1" note='Nếu ta áp dụng cách tính xác suất cho biến liên tục như ở biến rời rạc thì không khả thi. Ở xác suất của biến rời rạc, ta tính được xác suất tại một điểm $x = 0$ hay $x = 1$, thế nhưng đối với biến liên tục làm sao ta có thể tính được xác suất tại điểm $x = 3.4123545$ hay điểm $x = 234.2535345$ ? Do đó ta xem giá trị của xác suất tại một giá trị của biến liên tục là $0$ (này là informal definition, nếu intuitive hơn một tí thì ta "gần như không thể" chọn được 1 giá trị chính xác trên số thực, how are you gonna pick $x = 2.325424019$).' %}

Xét một biến số thực $x$, nếu xác suất $x$ rơi vào khoảng $(x, x + \delta x)$ được tính bởi $p(x)\delta x$ với $\delta x \to 0$ thì ta gọi $p(x)$ là **mật độ xác suất** (probability density hay viết tắt là pdf) trên $x$.

Xác suất để biến ngẫu nhiên $X$ nằm trong khoảng $(a, b)$ được xác định bằng:

$$
p(x \in (a, b)) = p(a < x < b) = \int_{a}^{b} p(x)dx
$$

<br/>

---

**WARNING 💀**: Đây là intuition của mình nên có thể có sai sót trong đây.

<figure>
    <img src="explain.png">
    <figcaption>Hình 1: Concept của probability density (được mình note thêm một chút) trong sách gốc</figcaption>
</figure>

Các bạn có thể thấy, xác suất để $X$ nằm trong khoảng $(x, x + \delta x)$ được xấp xỉ bởi giá trị $p(x)\delta x$, bởi vì xác suất để $X$ nằm trong khoảng là phần diện tích dưới đồ thị $p(x)$ từ $x \to x + \delta x$, dựa theo tích phân Riemann, ta có thể xấp xỉ:

$$
p(x \in (x , x+ \delta x)) = \int_{x}^{x + \delta x}p(x) dx \approx p(x)\delta x
$$

Tiếp tục dựa theo tích phân riemann, nếu chia đoạn $[a, b]$ thành $n$ điểm, ta có:

$$
p(x \in (a, b)) = \int_{a}^b p(x)dx = \lim_{ \delta x \to 0 } \sum_{k=0}^{n-1} p(a + k \delta x) \delta x
$$

--- 

<br/>

{% include marginnote.html id="mn_density_2" note="Giả sử ta có 2 biến liên tục là $x$ và $y$ với $x = g(y)$, tương tự ta có 2 pdf tương ứng là $p(x)$ và $p(y)$. Việc đổi biến từ $y$ sang $x$ sẽ có 1 hiện tượng cực kì hay (hiểu rõ hơn ở bài tập 1.4 [Exercises](../exercises_1/). Hiện tượng này sẽ được áp dụng rất nhiều ở các mô hình Deep Learning ví dụ như Normalizing Flow.)" %}

Tiếp theo, mật độ xác suất $p(x)$ phải thoả mãn một vài điều kiện:

- Xác suất là không âm:

$$
p(x) \geq 0
$$

- Ta đã biết, $p(x \in (a, b))$ là xác suất $x$ nằm trên khoảng $a, b$, mà $x$ lại là một số thực, do đó $x$ luôn nằm trong $\mathbb{R}$, tức là nằm trong đoạn $(-\infty, \infty)$. Vậy:

$$
p(x \in \mathbb{R}) = \int_{-\infty}^{\infty} p(x)dx = 1
$$

Xác suất mà $x$ nằm trong đoạn $(-\infty, z)$ được gọi là **cummulative distribution function** (hàm phân phối tích luỹ) hay **cdf** của $x$ và được định nghĩa như sau:

{% include marginnote.html id="mn_density_3" note="Việc chứng minh đạo hàm cdf ta được pdf có thể dùng đến Fundamental Theorem of Calculus (Second Part) [^1]"%}

$$
P(z) = \int_{-\infty}^z p(x)dx
$$

và ngoài ra $P'(x) = p(x)$.

{% include marginnote.html id="mn_density_4" note='Khi ở nhiều chiều hơn, một "khoảng" của ta sẽ trở nên khác. Ví dụ ở 1 chiều $\mathbf{x} = (x)$ thì khoảng ở đây sẽ là một khoảng trên đường thẳng từ $(a, b)$ nào đó, nếu ở 2 chiều $\mathbf{x} = (x_1, x_2)$ thì "khoảng" ở đây là một hình chữ nhật, ở 3 chiều là một hình hộp chữ nhật, ở 4 chiều thì chịu 🥲, đùa đấy, ở chiều cao hơn thì sẽ được gọi là **hyper-rectangle**. Ngoài ra chữ *infinitesimal* (vô cùng nhỏ) có nghĩa là một số $x$ nào đó rất gần $0$ và không có số nào gần hơn nó.' %}

Nếu ta có nhiều biến ngẫu nhiên $X_1, \dots, X_D$, được định nghĩa chung bằng vector $\mathbf{x} = (x_1, \dots, x_D)$, khi đó ta định nghĩa hàm **mật độ xác suất đồng thời** $p(\mathbf{x}) = p(x_1, \dots, x_D)$ sao cho xác suất $\mathbf{x}$ thuộc một phần thể tích vô cùng nhỏ (infinitesimal volume) $\delta \mathbf{x}$ (có chứa $\mathbf{x}$) được xác định bởi $p(\mathbf{x})\delta \mathbf{x}$.

Tương tự như mật độ xác suất 1 biến, ta cũng có:

- Xác suất không âm:

$$
p(\mathbf{x}) \geq 0
$$

- Phần tổng diện tích (đúng hơn là thể tích với nhiều chiều) luôn là $1$:

$$
\int p(\mathbf{x}) d\mathbf{x} = 1
$$

Nếu $X$ là biến ngẫu nhiên rời rạc, ta gọi $p(x)$ là **hàm khối xác suất** (probability mass function). Phân biệt một tí với hàm mật độ xác suất, hàm khối xác suất cũng thể được xem là xác suất của biến ngẫu nhiên rời rạc, do đó ta có thể gọi hàm khối xác suất $p(x)$ là phân phối xác suất của $X$, tức là $p(x) = p(X = x)$. Ta định nghĩa cdf của biến rời rạc cũng tương tự:

$$
P(z) = p(X \leq z) = \sum_{x \leq z} p(x)
$$

{% include marginnote.html id="mn_density_5" note="Việc chứng minh sao sum rule, product rule vẫn có thể áp dụng với biến liên tục, ta phải học nâng cao hơn ở môn gọi là **Measure Theory** (lý thuyết độ đo)." %}

Tương tự như biến ngẫu nhiên rời rạc, sum rule, product rule và định lý Bayes vẫn có thể áp dụng với biến ngẫu nhiên liên tục. Đặt $x$ và $y$ là hai biến ngẫu nhiên liên tục, ta có:

$$
\begin{aligned}
p(x) &= \int p(x, y) dy \\
p(x, y) &= p(y \mid x) p(x) \\
\implies p(x,y) &= \int p(y \mid x) p(x) dy \\
&= \int p(x \mid y) p(y) dy
\end{aligned}
$$

<br/>

|[Previous](../../prob_theory/) | [Next](../expectation/)|

<br/>

[^1]: https://en.wikipedia.org/wiki/Fundamental_theorem_of_calculus