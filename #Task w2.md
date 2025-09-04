---
title: '#Task w2'

---

# Task w2

++1. Chương trình asm: nhân 2 số++

```assembly
include \masm32\include\masm32rt.inc

.data
    ;khai bao bien
    num1 dd 0
    num2 dd 0
    result dd 0

.code
_start:
    ; nhap gia tri
    mov num1, sval(input("So thu nhat: "))
    mov num2, sval(input("So thu hai: "))
    ; gan bien vao thanh ghi de thuc hien phep tinh 
    mov eax, num1
    mov ebx, num2

    ; mul la phep nhan ko dau  
    ; imul la phep nhan co dau 
    imul ebx    ; eax = eax * ebx
    mov result, eax
    ; in ra ket qua bai toan
    print str$(result)

exit
end _start
```

`#include \masm32\include\masm32rt.inc`:
Đây là lệnh tiền xử lý (preprocessor directive) để bao gồm (include) tệp masm32rt.inc. Tệp này chứa các macro và định nghĩa cần thiết cho việc sử dụng các hàm của MASM32 Runtime Library, giúp đơn giản hóa việc nhập/xuất và các thao tác khác.

`.data`:
Đây là phần khai báo dữ liệu. Các biến được khai báo ở đây:

num1 dd 0: Khai báo biến num1 kiểu dd (doubleword - 32 bit), khởi tạo giá trị 0. Biến này sẽ lưu số thứ nhất.
num2 dd 0: Khai báo biến num2 kiểu dd, khởi tạo giá trị 0. Biến này sẽ lưu số thứ hai.
result dd 0: Khai báo biến result kiểu dd, khởi tạo giá trị 0. Biến này sẽ lưu kết quả phép nhân.

`.code`:
Đây là phần chứa mã lệnh của chương trình.

`_start:`: 
Nhãn đánh dấu điểm bắt đầu của chương trình.

*Nhập giá trị*
`input("So thu nhat: ")`: Gọi macro input (được cung cấp bởi masm32rt.inc) để hiển thị thông báo "So thu nhat: " và nhận dữ liệu nhập vào dưới dạng chuỗi.
`sval(...)`: Gọi macro sval (string to value - chuỗi sang giá trị) để chuyển đổi chuỗi nhập vào thành giá trị số nguyên có dấu và lưu vào biến num1.
`mov num2, sval(input("So thu hai: "))`: Tương tự như trên, nhưng nhận và chuyển đổi số thứ hai và lưu vào biến num2.

*Gán biến vào thanh ghi để thực hiện phép tính*
`mov eax, num1`: Chuyển giá trị của num1 vào thanh ghi eax. (eax thường được sử dụng cho các phép toán số học)
`mov ebx, num2`: Chuyển giá trị của num2 vào thanh ghi ebx.
Thực hiện phép nhân:
`imul ebx`: Thực hiện phép nhân có dấu giữa eax và ebx. Kết quả được lưu trong eax (phần thấp 32 bit) và edx (phần cao 32 bit, nếu kết quả vượt quá 32 bit). Trong trường hợp này, vì các số nhập vào là kiểu doubleword (32 bit), nên ta chỉ cần quan tâm đến eax.

*`mul` (phép nhân không dấu):* Nếu bạn muốn thực hiện phép nhân không dấu, bạn có thể sử dụng lệnh mul ebx.
*`imul` (phép nhân có dấu):* Lệnh imul (integer multiply) được sử dụng cho phép nhân có dấu.

`mov result, eax`: Chuyển kết quả từ eax vào biến result.

*In ra kết quả*
`str$(result)`: Gọi macro str$ (value to string - giá trị sang chuỗi) để chuyển đổi giá trị số nguyên trong result thành chuỗi ký tự.
print ...: In chuỗi kết quả ra màn hình.

`exit`: Kết thúc chương trình. Đây là một macro được cung cấp bởi masm32rt.inc để gọi hàm ExitProcess của Windows.

`end _start`: Chỉ thị kết thúc chương trình.

![Screenshot (99)](https://hackmd.io/_uploads/H1Y-mzTDyg.png)

- Vào Command Prompt, đường dẫn đến nơi chứa file và nhập <tên file>.

++2. Chương trình asm: cộng 2 số tự nhiên lớn++

```assembly
include \masm32\include\masm32rt.inc

.data
    ;khai bao bien
    num1 dd 0
    num2 dd 0
    result dd 0

.code
_start:
    ; nhap gia tri
    mov num1, sval(input("So thu nhat: "))
    mov num2, sval(input("So thu hai: "))
    ; gan bien vao thanh ghi de thuc hien phep tinh
    mov eax, num1
    mov ebx, num2
    
    ; add la phep cong
    add eax, ebx    ; eax = eax + ebx
    mov result, eax
    ; in ra ket qua bai toan
    print str$(result)

exit
end _start
```

`.code`

*Gán biến vào thanh ghi và thực hiện phép tính*
`mov eax, num1`: Di chuyển giá trị của num1 vào thanh ghi eax. eax thường được sử dụng cho các phép toán số học.
`mov ebx, num2`: Di chuyển giá trị của num2 vào thanh ghi ebx.
`add eax, ebx`: Thực hiện phép cộng. Giá trị trong ebx được cộng với giá trị trong eax, kết quả được lưu trữ trong eax. 
*eax = eax + ebx*
`mov result, eax`: Chuyển kết quả từ eax vào biến result.

![Select C__Windows_System32_cmd.exe 1_21_2025 7_23_25 PM](https://hackmd.io/_uploads/Skn2fGpwkx.png)

- Vào Command Prompt, đường dẫn đến nơi chứa file và nhập <tên file>.

++3. Chương trình asm: tìm index của substring++

```assembly
include \masm32\include\masm32rt.inc

.data
    msg_a db "Enter stringA: ", 0
    msg_b db "Enter substringB: ", 0
    not_found db "Substring not found", 13, 10, 0
    found_msg db "Substring found at index: ", 0
    index_str db "    ", 0
    buffer_a db 256 dup(0) ; Buffer cho stringA (toi da 255 ky tu)
    buffer_b db 256 dup(0) ; Buffer cho substringB (toi đa 255 ky tu)
    err_len db "String A must be longer than string B", 13, 10, 0

.code
_start:
    ; Nhap chuoi A
    print addr msg_a
    invoke StdIn, addr buffer_a, 255 ; Doc toi da 255 ky tu
    invoke StrLen, addr buffer_a     ; Tinh do dai stringA
    mov esi, eax                     ; lenA

    ; Nhap chuoi con B
    print addr msg_b
    invoke StdIn, addr buffer_b, 255 ; Doc toi da 255 ky tu
    invoke StrLen, addr buffer_b     ; Tinh do dai substringB
    mov edi, eax                     ; lenB

    ; Kiem tra do dai
    cmp esi, edi
    jl length_error     ; Neu lenA < lenB, bao loi

    mov ecx, 0          ; i = 0 (index cua stringA / chi so chuoi A)

; Vong lap duyet chuoi A
lapA:
    cmp ecx, esi
    jge not_found_label 

    mov edx, 0          ; j = 0 (index cua substringB / chi so chuoi B)
    
; Vong lap so sanh tung ki tu cua chuoi con B trong A
lapB:
    cmp edx, edi
    jge found_label     

    mov al, buffer_a[ecx+edx]
    cmp al, buffer_b[edx]
    jne next_i

    inc edx
    jmp lapB

; Tiep tuc duyet chuoi A neu khong tim thay khop o vi tri hien tai
next_i:
    inc ecx
    jmp lapA

; Tim thay chuoi con
found_label:
    ; Chuyen index thanh chuoi
    mov eax, ecx   ; Index
    invoke dwtoa, eax, addr index_str

    ; In thong bao
    print addr found_msg
    print addr index_str
    print chr$(13,10)
    jmp quit

; Khong tim thay chuoi con
not_found_label:
    print addr not_found
    print chr$(13,10)
    jmp quit

; Loi ve do dai
length_error:
    print addr err_len
    jmp quit

; Ket thuc chuong trinh
quit:
    invoke ExitProcess, 0
end _start
```

`.data`:
Phần này định nghĩa các thông báo và vùng đệm (buffer) được sử dụng trong chương trình:

`msg_a, msg_b`: Các thông báo hiển thị để yêu cầu người dùng nhập chuỗi A và chuỗi con B.
`not_found`: Thông báo hiển thị nếu chuỗi con không được tìm thấy.
`found_msg`: Thông báo hiển thị trước chỉ số (index) của vị trí tìm thấy chuỗi con.
`index_str`: Vùng đệm dùng để lưu trữ chỉ số tìm thấy dưới dạng chuỗi ký tự.
`buffer_a, buffer_b`: Các vùng đệm lưu trữ chuỗi A và chuỗi con B được nhập vào. Mỗi buffer có kích thước 256 byte, cho phép lưu trữ tối đa 255 ký tự (byte cuối cùng dành cho ký tự null '\0' kết thúc chuỗi).
`err_len`: Thông báo lỗi hiển thị nếu độ dài chuỗi B lớn hơn độ dài chuỗi A.

`.code`

*Nhập chuỗi A*
`print addr msg_a`: In thông báo yêu cầu nhập chuỗi A.
`invoke StdIn, addr buffer_a, 255`: Đọc tối đa 255 ký tự từ đầu vào chuẩn (bàn phím) và lưu vào buffer_a.
`invoke StrLen, addr buffer_a`: Tính độ dài của chuỗi A và lưu vào thanh ghi eax.
`mov esi, eax`: Sao chép độ dài chuỗi A từ eax vào esi (để tiện sử dụng sau này).

*Nhập chuỗi con B*: Tương tự như nhập chuỗi A, nhưng lưu vào buffer_b và độ dài được lưu vào edi.

*Kiểm tra độ dài*
`cmp esi, edi`: So sánh độ dài chuỗi A (esi) và chuỗi B (edi).
`jl length_error`: Nếu độ dài A nhỏ hơn độ dài B (A < B), nhảy đến nhãn length_error để in thông báo lỗi. Vì chuỗi con không thể dài hơn chuỗi mẹ.

*Vòng lặp tìm kiếm chuỗi con*
`mov ecx, 0`: Khởi tạo biến đếm ecx (tương ứng với chỉ số i của chuỗi A) bằng 0.
`lapA`: Vòng lặp ngoài duyệt qua từng ký tự của chuỗi A.
`cmp ecx, esi`: So sánh ecx với độ dài chuỗi A (esi).
`jge not_found_label`: Nếu ecx >= esi, nghĩa là đã duyệt hết chuỗi A mà không tìm thấy chuỗi con, nhảy đến not_found_label.

`mov edx, 0`: Khởi tạo biến đếm edx (tương ứng với chỉ số j của chuỗi B) bằng 0.
`lapB`: Vòng lặp trong duyệt qua từng ký tự của chuỗi con B.
`cmp edx, edi`: So sánh edx với độ dài chuỗi B (edi).
`jge found_label`: Nếu edx >= edi, nghĩa là đã duyệt hết chuỗi B và tất cả các ký tự đều khớp, nhảy đến found_label.

`mov al, buffer_a[ecx+edx]`: Lấy ký tự thứ ecx + edx của chuỗi A và lưu vào al.
`cmp al, buffer_b[edx]`: So sánh ký tự này với ký tự thứ edx của chuỗi B.

`jne next_i`: Nếu không bằng nhau, nhảy đến next_i để tiếp tục kiểm tra từ vị trí tiếp theo trong chuỗi A.
`inc edx`: Tăng edx để kiểm tra ký tự tiếp theo của chuỗi B.
`jmp lapB`: Quay lại đầu vòng lặp lapB.
`next_i`: Tăng ecx để kiểm tra từ vị trí tiếp theo trong chuỗi A.
`jmp lapA`: Quay lại đầu vòng lặp lapA.

*Đã tìm thấy chuỗi con (found_label)*
`mov eax, ecx`: Sao chép chỉ số ecx (vị trí tìm thấy) vào eax.
`invoke dwtoa, eax, addr index_str`: Chuyển đổi số nguyên trong eax thành chuỗi ký tự và lưu vào index_str.
`print addr found_msg`: In thông báo tìm thấy.
`print addr index_str`: In chỉ số tìm thấy.
`print chr$(13,10)`: In ký tự xuống dòng.
`jmp quit`: Nhảy đến quit để kết thúc chương trình.

*Không tìm thấy chuỗi con (not_found_label)*: In thông báo không tìm thấy.

*Lỗi độ dài (length_error)*: In thông báo lỗi độ dài.

`quit`: Kết thúc chương trình.

![Screenshot 1_23_2025 9_20_45 PM](https://hackmd.io/_uploads/rkztl01_yg.png)

- Vào Command Prompt, đường dẫn đến nơi chứa file và nhập <tên file>.
