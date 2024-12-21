---
layout: post
title: Exercises (Part 1)
mathjax: true
---

Mục lục:

- [Bài 1.1](#bài-11)
- [Bài 1.2](#bài-12)
- [Bài 1.3](#bài-13)

## Bài 1.1

Phương trình (1.1) như sau:

$$
y(x, \mathbf{w}) = \sum_{j=0}^M x^j w_{j}
$$

Phương trình (1.2) như sau:

$$
E(\mathbf{w}) = \frac{1}{2} \sum_{n=1}^N \left\{ y(x_{n}, \mathbf{w}) - t_{n} \right\}^2
$$

với $(x_1, \dots, x_{n})$ là các dữ liệu, $(t_{1}, \dots, t_{n})$ là các nhãn (hay là target) và $\mathbf{w}$ là bộ tham số. Để cực tiểu được hàm lỗi $E(\mathbf{w})$, ta chỉ cần tìm giá trị $\hat{\mathbf{w}}$, sao cho:

$$
\nabla E(\hat{\mathbf{w}}) = \mathbf{0}
$$

với $\mathbf{0}$ là vector $0$. Do $\nabla E(\mathbf{w})$ là một vector nên để vector bằng $0$ thì từng phần tử bằng $0$, vậy ta cần tìm $\hat{w}_{i}$ sao cho:

$$
\frac{\partial{E(\hat{\mathbf{w}})}}{\partial w_{i}} = 0
$$

Giờ bắt đầu biến đổi để tìm được $\hat{w}_i$ thôi nào. Ta có:

$$
\begin{aligned}
\frac{\partial{E(\hat{\mathbf{w}})}}{\partial w_{i}} &= \frac{1}{2} \sum_{n=1}^N \frac{\partial \{y(x_{n}, \mathbf{w}) - t_{n}\}^2}{\partial w_{i}} \\
&= \frac{1}{2} \sum_{n=1}^N \left[ \frac{\partial y(x_{n}, \mathbf{w})^2}{\partial w_{i}} - 2t_{n} \frac{\partial y(x_{n}, \mathbf{w})}{\partial w_{i}} + \frac{\partial t_{n}^2}{\partial w_{i}} \right] \\
&= \frac{1}{2} \sum_{n=1}^N \left[ 2y(x_{n}, \mathbf{w})\frac{\partial y(x_{n}, \mathbf{w})}{\partial w_{i}} - 2t_{n}x_{n}^i +0 \right] \\
&= \frac{1}{2} \sum_{n=1}^N [2y(x_{n}, \mathbf{w})x_{n}^i -2t_{n}x_{n}^i] \\
&= \sum_{n=1}^N \left[ \sum_{j=0}^M x_{n}^{i+j} w_{j} \right] - \sum_{n=1}^Nt_{n}x_{n}^i
\end{aligned}
$$

Ở phương trình trên, tách phần trước dấu trừ, ta được:

$$
\begin{aligned}
\sum_{n=1}^N \left[ \sum_{j=0}^M x_{n}^{i+j} w_{j} \right] &= \sum_{n=1}^N (x_{n}^{i}w_{0} + \dots x_{n}^{i+M}w_{M}) \\
&= \sum_{n=1}^N x_{n}^iw_{0} + \dots + \sum_{n=1}^N x_{n}^{i+M}w_{M} \\
&= \sum_{j=0}^M \left( \sum_{n=1}^N x_{n}^{i+j} \right) w_{j}
\end{aligned}
$$

Thay vào lại phương trình chỗ ta có:

$$
\begin{aligned}
\frac{\partial{E(\hat{\mathbf{w}})}}{\partial w_{i}} &= \sum_{n=1}^N \left[ \sum_{j=0}^M x_{n}^{i+j} w_{j} \right] - \sum_{n=1}^Nt_{n}x_{n}^i \\
&= \sum_{j=0}^M \left( \sum_{n=1}^N x_{n}^{i+j} \right) w_{j} - \sum_{n=1}^N t_{n}x_{n}^i
\end{aligned}
$$

Đặt $\sum_{n=1}^N x_{n}^{i+j} = A_{ij}$ và $\sum_{n=1}^Nt_{n}x_{n}^i = T_{i}$. Khi đó:

$$
\begin{aligned}
\frac{\partial E(\mathbf{w})}{\partial w_{i}} &= 0 \\
\Leftrightarrow \sum_{j=0}^M A_{ij}w_{j} &= T_{i}
\end{aligned}
$$

Vậy giá trị $\hat{w}_i$ cần tìm chính là nghiệm của phương trình trên.

## Bài 1.2

Phương trình (1.122) là phương trình nghiệm $\hat{w}_i$ ở bài 1.1. Còn phương trình (1.4) như sau:

$$
\tilde{E}(\mathbf{w}) = \frac{1}{2} \sum_{n=1}^N \{y(x_{n}, \mathbf{w}) - t_{n}\}^2 + \frac{\lambda}{2}||\mathbf{w||^2}
$$

trong đó $\|\mathbf{w}\|$ được gọi là **chuẩn** của vector $\mathbf{w}$ và có công thức là:

$$
\|\mathbf{w}\| = \sqrt{ w_{0}^2 + \dots + w_{M}^2 }
$$

Ta có:

$$
\begin{aligned}
\frac{\partial{E(\hat{\mathbf{w}})}}{\partial w_{i}} &= \frac{1}{2} \sum_{n=1}^N \frac{\partial \left( \{y(x_{n}, \mathbf{w}) - t_{n}\}^2 +\frac{\lambda}{2}||\mathbf{w}||^2 \right)}{\partial w_{i}} \\
&= \frac{1}{2} \sum_{n=1}^N \left[ \frac{\partial y(x_{n}, \mathbf{w})^2}{\partial w_{i}} - 2t_{n} \frac{\partial y(x_{n}, \mathbf{w})}{\partial w_{i}} + \frac{\partial t_{n}^2}{\partial w_{i}} + \frac{\lambda}{2} \frac{\partial||\mathbf{w}||^2}{\partial w_{i}} \right] \\
&= \sum_{j=0}^M A_{ij}w_{j} -T_{i} + \sum_{n=1}^N \lambda w_{i} \\
&= \sum_{j=0}^M A_{ij}w_{j} -T_{i} + N\lambda w_{i} \\
\end{aligned}
$$

Vậy giá trị $\hat{w}_i$ chính là nghiệm của phương trình:

$$
\sum_{j=0}^M A_{ij}w_{j} + N\lambda w_{i} = T_{i}
$$

## Bài 1.3

Bài này giải khá tương tự bài trong phần [[Introduction (Prob)]]. Mình đặt biến ngẫu nhiên $B$ đại diện cho các hộp màu, biến ngẫu nhiên $F$ đại diện cho trái cây, $F= a$ là trái táo (apple), $F = o$ là trái cam (orange) và $F = l$ là trái chanh (lime). Ta có:

$$
\begin{aligned}
p(B = r) &= 0.2 \\
p(B = b) &= 0.2 \\
p(B = g) &= 0.6
\end{aligned}
$$

Tiếp theo, ta có xác suất chọn được trái táo khi đã chọn được một hộp màu lần lượt là:

$$
\begin{aligned}
p(F = a \mid B = r) &= \frac{3}{10} = 0.3 \\
p(F = a \mid B = b) &= \frac{1}{2} = 0.5 \\
p(F = a \mid B = g) &= \frac{3}{10} = 0.3
\end{aligned}
$$

Dùng sum rule, ta lại có:

$$
\begin{aligned}
p(F = a) &= \sum_{B} p(F=a, B) \\
&= \sum_{B} p(F=a \mid B)p(B) \\
&= p(F=a \mid B = r)p(B = r) + p(F=a \mid B=b)p(B=b) \\
&+ p(F=a \mid B=g)p(B = g) \\
&= 0.3 \times 0.2 + 0.5 \times 0.2 + 0.3 \times 0.6 \\
&= 0.34
\end{aligned}
$$

Vậy xác suất để chọn được một quả táo là $0.34$. Để tìm xác suất hộp ta chọn là hộp xanh lá $g$ khi đã chọn được quả táo, ta tìm xác suất $p(B = g \mid F = a)$ bằng cách dùng định lý Bayes:

$$
p(B = g \mid F= a) = \frac{p(F=a \mid B=g)p(B =g)}{p(F=a)} = \frac{0.3 \times 0.6}{0.34} \approx 0.52
$$

## Bài 1.4

**WARNING: Bài này khá hardcore 💀**

Giả sử ta có hàm khả vi $f(x)$ với $x$ là số thực (không phải biến ngẫu nhiên), để tìm giá trị lớn nhất của $f(x)$, ta đạo hàm $f'(x)$ sau đó cho $f'(x) = 0$ để tìm được giá trị $x$ thoả mãn, gọi là $\hat{x}$ đi.

Tiếp theo, ta có một biến mới là $y$ với $x = g(y)$. Đổi biến hàm $f(x)$ sang $f(g(y))$ (là một hàm của $y$), ta đặt $\tilde{f}(y) = f(g(y))$ (để biết đây là một hàm của $y$). Để tìm giá trị lớn nhất của $\tilde{f}(y)$, ta đạo hàm và sau đó cho bằng $0$. Đầu tiên đạo hàm:

$$
\begin{aligned}
\frac{d\tilde{f}(y)}{dy} &= \frac{df(g(y))}{g(y)} \frac{dg(y)}{y} \\
\implies  \tilde{f}'(y) &= f'(g(y))g'(y)
\end{aligned}
$$

Sau đó cho bằng $0$ (gọi giá trị làm đạo hàm bằng $0$ là $\hat{y}$):

$$
\tilde{f}'(\hat{y}) = 0 \implies f'(g(\hat{y})) = 0 \hspace{3pt} \text{hoặc} \hspace{3pt} g'(\hat{y}) = 0 \hspace{3pt} \text{hoặc cả 2 $=0$}
$$

{% include marginnote.html id="exercises_1" note="Tuy nhiên ta cần để ý trường hợp chỉ $g'(\hat{y}) = 0$. Trong solution tác giả giả sử luôn $g'(\hat{y}) = 0$ bởi vì ta chỉ quan tâm đến trường hợp $f'(g(\hat{y})) = 0$ thôi, việc $g'(\hat{y}) = 0$ mà $f'(g(\hat{y})) \neq 0$ có thể được giải quyết bằng cách chọn một biến khác, gọi là $t$ đi, lúc này $x = \tilde{g}(t)$ và ta được $f'(\tilde{g}(\hat{t})) = 0$ và ta không cần quan tâm $\tilde{g}'(\hat{t})$ bằng $0$ hay khác $0$ nữa. Do mục đích là tìm giá trị lớn nhất của $f(x)$ thông qua một biến mới nào đó, do đó ta có thể chọn lại biến mới sao cho thoả mãn các giả sử của ta là được. Vậy ở đây, tác giả muốn nói là, với $x$ và $y$ (liên quan với nhau thông qua $x = g(y)$) không là biến ngẫu nhiên thì ta có thể tìm giá trị lớn nhất của $f(x)$ thông qua $y$. Nhưng đối với hai biến ngẫu nhiên $X$ và $Y$ thì việc này không xảy ra (không thể tìm giá trị lớn $f(X)$ thông $Y$) do bị ảnh hưởng bởi jacobian factor." %}

Xét trường hợp $f'(g(\hat{y})) = 0$, ta thấy rằng $f'(\hat{x}) = 0$, do đó $f'(g(\hat{y})) = f'(\hat{x}) \implies g(\hat{y}) = \hat{x}$. Vậy có nghĩa là ta có thể tìm giá trị lớn nhất của $f(x)$ thông qua $y$ với $x = g(y)$. Tương tự với trường hợp $f'(g(\hat{y})) = 0$ và $g'(\hat{y}) = 0$.

Giờ xét $X$ và $Y$ là hai biến ngẫu nhiên với $X = g(Y$) (lưu ý $g$ là hàm khả nghịch). Đặt $p_x$ và $p_y$ lần lượt là hàm mật độ xác suất của $X$ và $Y$. Để tìm được mật độ xác suất của $Y$, ta dùng công thức 1.17 như sau:

$$
p_{y}(y) = p_{x}(g(y)) \hspace{2pt} \left|g'(y)\right|
$$

Giả sử giá trị $\hat{x}$ là giá trị để làm cho $p_x$ lớn nhất, tức là $p_{x}'(\hat{x}) = 0$. Để tìm giá trị lớn nhất của $p_y(y)$ ta đạo hàm và sau đó cho giá trị đạo hàm bằng $0$. Giả sử $g'(y) \neq 0$ (khi đó ta mới có thể đạo hàm $\lvert g'(y)\rvert$) và đặt $\lvert g'(y) \rvert= sg'(y)$ với $s \in \{-1, 1\}$.

Đầu tiên ta lấy đạo hàm:

$$
\begin{aligned}
p_{y}'(y) = \frac{dp_{y}(y)}{dy} &= \frac{dp_{x}(g(y))}{dy} sg'(y) + p_{x}(g(y)) \frac{dsg'(y)}{dy} \\
&= sp_{x}'(g(y))g'(y)\hspace{1pt}|g'(y)| + p_{x}(g(y))\hspace{1pt}sg''(y) \\
&= sp_{x}'(g(y))[g'(y)]^2 + sp_{x}(g(y))\hspace{1pt}g''(y) \\
\end{aligned}
$$

Giả sử giá trị $\hat{y}$ là giá trị để làm cho $p_y$ lớn nhất và **giả sử** $\hat{x} = g(\hat{y})$, tức là $p_x(\hat{x}) = p_x(g(\hat{y})) = 0$ (tương tự như $x$ và $y$ không là biến ngẫu nhiên). Khi đó:

$$
\begin{aligned}
p_{y}'(\hat{y}) &= sp_{x}'(g(\hat{y}))[g'(\hat{y})]^2 + sp_{x}(g(\hat{y}))\hspace{1pt}g''(\hat{y}) \\ 
&= sp_{x}(g(\hat{y}))g''(\hat{y}) \neq 0
\end{aligned}
$$

Vậy rõ ràng nếu $\hat{y}$ là giá trị làm cho $p_y$ lớn nhất và $\hat{x} =g(\hat{y})$ thì điều này lại sai, do đó $\hat{x} \neq g(\hat{y})$. Tức là nếu $X$ và $Y$ là biến ngẫu nhiên thì không có quan hệ nào giữa $\hat{x}$ và $g(\hat{y})$, do đó ta không thể tìm giá trị $X$ làm cho $p_x$ lớn nhất bằng cách tìm giá trị $Y$ làm cho $p_y$ lớn nhất.

Tuy nhiên, nếu ta chọn $g(Y) = X$ sao cho $g$ là một hàm tuyến tính thì mọi chuyện sẽ khác. Giả sử $X = g(Y) = \alpha Y + \beta$. Khi đó:

$$
p'_{y}(\hat{y}) = sp_{x}(g(\hat{y}))g''(\hat{y}) = 0
$$

Do nếu $g(y) = \alpha y + \beta$ thì $g''(y) = 0$ với mọi $y$.

Vậy $p_y'(\hat{y}) = 0 \implies p_x'(g(\hat{y})) = 0 \implies p_x'(\hat{x}) = p_{x}(g(\hat{y})) = 0 \implies  \hat{x} = g(\hat{y})$. Ta có thể thấy bằng việc chọn $g$ là một hàm tuyến tính thì $\hat{x} = g(\hat{y})$, do đó việc chọn hàm $g$ để biến đổi từ $X$ sang $Y$ là rất quan trọng.

**References**:
- [prml-web-sol.dvi (microsoft.com)](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/05/prml-web-sol-2009-09-08.pdf)
- [real analysis - Exercise 1.4 from PRML: Process of Using Transformations to Find Modes of PDFs - Mathematics Stack Exchange](https://math.stackexchange.com/questions/3494289/exercise-1-4-from-prml-process-of-using-transformations-to-find-modes-of-pdfs)
- [real analysis - Linear/non-linear change of variables: $\tilde{f} \ ' (\tilde{y}) = f'(g(\tilde{y})) g'(\tilde{y}) = 0$ and assuming $g'(\tilde{y}) \not= 0$ - Mathematics Stack Exchange](https://math.stackexchange.com/questions/3510938/linear-non-linear-change-of-variables-tildef-tildey-fg-tilde)