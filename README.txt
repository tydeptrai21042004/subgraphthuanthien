Đây là bài tập lớn cấu trúc rời rạc phần 3. write code
ở đây sẽ trình bày về
1.Thuật toán( độ phức tạp về không gian và thời gian, ưu và nhược điểm của từng thuật toán) 
2.triển khai thuật toán bằng ngôn ngữ lập trình python (ghi lại hiệu suất cũng như những khó khăn khi triển khai thuật toán) 
3.Phân tích và đưa ra kết luận để nâng cao hiệu suất làm việc.
Thuật toán.
Bài tập lớn, Subgraph-ismo challenge có hai phần
1. Tam giác, đếm và liệt kê
2. K-truss, find max k-truss
dataset sẽ lấy từ snapdataset, ở đây sẽ sử dụng định dạng .MMIO( matrix markix i/o) để làm việc.
trình biên dịch của python dùng trong trường hợp  là jupyter notebook
python phiên bản 3.11.
các công nghệ sử dụng
xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Về thiết bị
Device name	**********
Processor	Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz   1.80 GHz// bộ vi xử lý intel core i5 thế                                                                   hệ thứ 8, tần số cơ sở xử lý                                                                    là 1.6 GHz 
Installed RAM	12.0 GB (11.9 GB usable)// Ram và số ram khả dụng
Device ID	**********
Product ID	**********
System type	64-bit operating system, x64-based processor// hệ điều hành 64 bit
Pen and touch	No pen or touch input is available for this display
* Trong quá trình làm thì có vẻ bộ xử lý của NVida tương thích hơn để sử dụng, với rất nhiều công cụ hộ trỡ tỏg việc tính toán 
( Bạn nên thay bằng cấu hình thiết bị của bạn để được kết quả đúng hơn)
--------------------------------------------------
I Thuật toán
1. Tam giác 
- thuật toán đầu tiên chúng ta sẽ tìm số tam giác bằng cách cơ bản nhất, một kiểu thuật toán "trâu bò" trong đó nó "duyệt từng cạnh, đếm từng đỉnh" nhầm mục đích xác định các cạnh của một bộ ba đỉnh(nodes) có tạo thành một tập hợp kín( 2 đỉnh bất kì đều có cạnh nối với nhau) không? Thoạt nhìn thì đây có khả năng cao là thuật toán ngốn nhiều thời gian xử lý o(V*(v-1)*(v-2)) với v là số đỉnh  ( do chúng ta phải duyệt qua tất cả bộ tam của đỉnh bằng ba vòng lặp lồng nhau).
- Thuật toán 2: /*(giải thích ngắn gọn: chúng ta sẽ lập phương ma trận kề và đếm số giá trị =3 từ đó tìm số tam giác)*/
    input: ma trận kề(A)
    A*A*A=B
    trace(B)/6 = number of triangles
    Output: number of triangles
Với A là ma trận kề thì một phần 6 trace của A^3 sẽ là số tam giác cần tìm
độ phức tạp của thuật toán là o(n+m+n^2) với n là số đỉnh m là số cạnh. 
o(n+m) là của phép nhân ma trận còn 0(n^2) của phép tính trace
- Thuật toán 3:/* giải thích ngắn gọn: nhân ma trận kề với ma trận liên thuộc, rồi tính giá trị khác 0( bằng 2 ) của kết quả*/ 
    input: ma trận kề (A), ma trận liên thuộc (B)
    A*B=C
    C{0,1,2,0
      1,0,2,3
      .......}
    x= Count the number of value equal 2 in C
    x/3= number of triangles
    output: number of triangles
với v là số đỉnh, n là số cạnh thì độ phức tạp của thuật toán là 0(v^2*n+v*n) 
o(v^2*n) là của phép nhân ma trận còn o(v*n) là của việc tìm số giá trị bằng 2 của ma trận được sinh ra.


2. max k-truss
Để tìm maximal k-truss tôi xin dùng thuật toán sau
mã giả 
find_maximal_k_truss(graph):
    k = 3  // Start with the smallest non-trivial trus

    while Tr// loopue:
        // Compute k-trussomposition, The k-truss decomposition of a graph involves finding all the distinct k-trusses for different values of k.tion
        truss_decomposition = k_truss(grap, k)

        // Check if the set of satisfying edges is non-empty
        satisfying_edges = get_edges(truss_decompsition)

        if satisfying_edges is not empty:
            // Move to the next value of k
            k = k + 1
        else:
            // The previous value of k is the maximal k-truss
            kmax = k - 1
       
or  
Start with an initial value of k (often k = 3).
Identify all the (k-2)-cliques in the graph.
Construct a k-truss by including edges that are part of at least one (k-2)-clique.
Remove the nodes and edges of the identified k-truss from the graph.
Increment the value of k and repeat the process until no more k-trusses can be found.
input chúng ta đưa vào là ma trận kề
output chúng ta nhận được là số k

độ phức tạp của thuật toán là o(số lần lặp lại của vòng lặp *(V+E))    return kmax

II. Thực chạy 
- Các công nghệ được dùng
Networkx:
là một thư viện hộ trở ngôn ngữ Python được ứng dụng rộng rãi trong việc nghiên cứu và phân tích các mạng phức tạp. 
scipy:
là một thư viện mã nguồn mở và miễn  trong ngôn ngữ lập trình Python, chuyên về các chức năng toán học và khoa học và kỹ 
- Các vấn đề khi run code
Trong các lần chạy thì thường gặp lỗi memory errol ( do yêu cầu lưu trữ trong quá trình xử lý quá cao, đôi lúc là lên tới 512 Gib, một con số mà chỉ có siêu máy tính mới giải quyết được ), cách giải quyết thông thường là dùng cách hàm cũng như phương pháp( định dạng) lưu trữ mà NetworkX cung cấp cho ma trận thưa ( không có định nghĩa rõ ràng nhưng có thể hiểu là ma trận có nhiều giá trị bằng 0, nếu chúng ta ứng dụng cách lưu trữ thông thường thì phải lưu toàn bộ giá trị của ma trận cũng như số hàng và số cọt của ma trận, trong khi dữ liệu xử lý đa phần là ma trận thưa, nên chúng ta có thể chỉ cần lưu trữ các giá trị của ma trận lớn hơn không và số giá trị bằng 0, Việc lưu trữ này sẽ có hiểu quả cho việc lưu trữ lần thời gian thực thi của thuật toán) như C00(danh sách tọa độ) , CSR(nén hàng thưa), LIL(danh sách trong danh sách)
Một gợi ý để giảm thời gian thực thi thuật toán là nâng cao phần cứng( tất nhiên rồi) gợi ý là sử dụng card đồ họa của NVIDIA.
------------------------------------------------------------------------------------------------------
Ông chạy code ( với từng bộ dataset khác nhau rồi ghi kết quả( giá trị cần tìm và thời gian để tìm) lên đây, nếu muốn thì tôi làm )

