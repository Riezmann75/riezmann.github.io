---
title: Chiều nhiều không hiểu nhiều chiều
date: 2025-08-14
math: true
---

**Chú ý: Bài viết mang tính chất kĩ thuật, được viết trong lúc tác giả đang cố gắng học nên rất có thể có sai xót.**

Dạo gần đây tôi đọc được một topic khá vui về một nghịch lý thể tích của vật thể ở không gian đa chiều (như cách tôi chiều người yêu, rất chiều).

Theo tôi hiểu đại khái nó thế này: "Với một vật lồi đẳng hướng (isotrophic convex body), khi số chiều càng tăng, khối lượng của nó sẽ tập trung vào hầu hết ở vỏ". Tưởng tượng một qua cam ở thế giới đa chiều nhiều tép nhưng bóc vỏ ra khối lượng của nó về 0 thật mâu thuẫn. Thế là khi không lại tự đẻ ra vấn đề cho mình tự đi tìm hiểu.

Mọi sự bắt đầu từ một miếng lý thuyết từ một bài báo nghiên cứu có tên *"Whitened CLIP as a Likelihood Surrogate of Images and Captions (Betser et al., 2025)"* từ một đại học ở Israel nói về việc khi thực hiện các phép biến đổi để chuyển các vector trừu tượng (embedding vector) của CLIP thành một bộ vector khác mà trong đó mỗi thành phần của vector đó là gần như vuông góc với nhau, rồi từ đó tiến hành các phép đo để ước tính phân phối xác suất của ảnh đầu vào. Và họ bắt đầu dựa trên một lý thuyết có tên "Thin Shell" (lớp vỏ mỏng). 

Lý thuyết này cho rằng khi một vật lồi đẳng hướng trở thành một vật trong không gian đa chiều, phần lớn khối lượng sẽ tập trung ở vỏ của vật chứ không phải bên trong. Bằng công thức toán thì chúng ta có thể biểu diễn nó như sau:

$$P(\lVert x \rVert \in [r-\epsilon, r+\epsilon]) \approx \frac{C(d)}{\epsilon^d }$$

Mà trong đó $P(.)$ là phép đo xác suất, $    \lVert x \rVert$ là độ dài Euclidean của vector, $r$ là bán kính thông thường và là giá trị trung bình của $    \lVert x \rVert$, $d$ là số chiều, $C(d)$ là một hằng số được tính dựa trên $d$ và $\epsilon$ là một tham số cho biên độ dao động quanh bán kính $r$.

Tuy nhiên, biểu diễn này dựa trên một bài báo của Paouris (2006) với tựa đề:  *Concentration of mass on convex bodies*. Đây là một báo thuần toán, tuy nhiên chúng ta chỉ cần để ý tới kết quả của nó như sau: Với một vật lồi, đẳng hướng $K$ trong không gian $R^d$, tồn tại một hằng số tuyệt đối $c$ thỏa mãn:

$$P(\lVert x \rVert \geq c\sqrt{d}L_Kt)\leq e^{-\sqrt{d}t}$$

Trong đó $L_K$ là hằng số đẳng hướng, $d$ là số chiều, $t\geq1$ là tham số.

Tôi tạm thời diễn giải kết quả này bằng lời như sau: "Nếu $x$ là một vector ngẫu nhiên trong không gian lồi đẳng hướng $K$, thì xác suất để độ dài của vector $x$ lớn hơn $c\sqrt{d}L_Kt$ giảm rất nhanh theo cấp số mũ."

Vậy thì điều này có mối liên hệ gì với bài báo kia? Tôi tự hỏi. Tôi dành thời gian để ngẫm nghĩ, tìm tòi để cố đọc hiểu bài báo của Paouris cho bằng được tuy nhiên vẫn không tìm ra được manh mối nào cho mối tương quan đó. Tuy nhiên tôi nghĩ mình có cách hiểu khác cho dù không viết ra được công thức xấp xỉ như trên. Trong bài báo *The Double-Ellipsoid Geometry of CLIP (Levi and Gilboa, 2025)*, nhóm tác giả Israel đã chứng minh rằng trong không gian đẳng hướng:

$$\mathbb{E}[\lVert x \rVert^2] \approx \mathbb{E}^2[\lVert x \rVert]$$

Và bởi vì là không gian đẳng hướng, chúng ta sẽ có:

$$\mathbb{E}[\lVert x \rVert^2] =\mathbb{E}[\Sigma_{k=1}^dx(k)^2]=C(d)$$

Trong đó $x(k)$ là thành phần thứ $k$ của vector $x$. Vì thế, chúng ta có thể xấp xỉ:

$$\mathbb{E}[\lVert x \rVert]\approx\sqrt{C(d)}$$

và nó là một hằng số.

Bây giờ chúng ta biết độ dài trung bình của vector là một hằng số, bên cạnh đó thì mặc dù độ dài các vector ngẫu nhiên có thể thay đổi, nó khó mà có thể vượt qua được một giới hạn vì xác suất cho việc đó giảm theo cấp số mũ. Chính vì vậy, phần lớn các vector phải nằm gần nhau và nằm xung quanh giá trị trung bình. Nếu không, giá trị trung bình sẽ không cố định, và (hoặc) có giá trị nhỏ hơn giá trị nêu trên. Bên cạnh đó thì Betser (2025) cũng chứng minh rằng nếu $d$ tăng thì giá  trị độ dài trung bình sẽ hội tụ về $\sqrt{d-\frac{1}{2}}$. Điều này càng củng cố thêm lý luận vừa rồi.

Như vậy, các điểm trong không gian đa chiều, nếu thuộc không gian $K$ đa phần sẽ tập trung chủ yếu ở gần một bán kính nhất định khiến cho phần không gian còn lại bị, "rỗng". Kì lạ.

Một ví dụ khác cho cái này đó là nếu bạn nhìn vào phân phối chuẩn (Normal distribution), chúng ta có thể thấy rằng mặc dù điểm ở giữa là điểm có độ đậm đặc (density) cao nhất, nhưng xác suất để ngẫu nhiên ra được điểm đó bằng 0. Còn phần xung quanh thì lại rất dễ ra. Ví dụ này đúng cho cả phân phối chuẩn ở không gian đa chiều, chỉ là lúc này bài toán sẽ trở thành Multi-variate Normal Distribution.

**Reference**

Betser, R., Levi, M. Y., & Gilboa, G. (2025). _Whitened CLIP as a Likelihood Surrogate of Images and Captions_ (No. arXiv:2505.06934). arXiv. [https://doi.org/10.48550/arXiv.2505.06934](https://doi.org/10.48550/arXiv.2505.06934)

Levi, M. Y., & Gilboa, G. (2025). _The Double-Ellipsoid Geometry of CLIP_ (No. arXiv:2411.14517). arXiv. [https://doi.org/10.48550/arXiv.2411.14517](https://doi.org/10.48550/arXiv.2411.14517)

Paouris, G. (2006). Concentration of mass on convex bodies. _GAFA Geometric And Functional Analysis_, _16_(5), 1021–1049. [https://doi.org/10.1007/s00039-006-0584-5](https://doi.org/10.1007/s00039-006-0584-5)
