---
title: Task w1

---

# Task w1

++1. Khái niệm cơ bản++
- **Register (Thanh ghi)** là bộ nhớ tốc độ cao  trong CPU để lưu trữ tạm thời (dữ liệu hoặc địa chỉ).

    *AX/EAX/RAX*: Thanh ghi tích lũy, dùng cho các phép toán. 
    *BX/EBX/RBX*: Thanh ghi cơ sở, lưu địa chỉ dữ liệu. 
    *CX/ECX/RCX*: Thanh ghi đếm, dùng trong vòng lặp hoặc lệnh dịch bit. 
    *DX/EDX/RDX*: Thanh ghi dữ liệu, lưu trữ tạm kết quả phép toán. 

- **Instructions (Tập lệnh)** là tập hợp các lệnh máy mà CPU hiểu và thực thi, được viết bằng ngôn ngữ máy hoặc Assembly.

    *Arithmetic*: Thực hiện các phép toán (+, -, *, /). 
    *Data Transfer*: Di chuyển dữ liệu giữa các thanh ghi, bộ nhớ. 
    *Control Flow*: Điều khiển luồng chương trình (jump, call, return).
    *Logical*: Thực hiện các phép toán logic (AND, OR, XOR). 

- **Stack (Ngăn xếp)** là ngăn xếp lưu trữ dữ liệu tạm thời (biến, tham số) theo nguyên tắc LIFO – dữ liệu được đưa vào sau sẽ được lấy ra trước. 

    *Push*: Đưa dữ liệu vào stack. 
    *Pop*: Lấy dữ liệu ra khỏi stack. 

- **Endianness (Thứ tự byte)** là cách sắp xếp byte trong bộ nhớ (Big-Endian, Little-Endian).
  
    *Big-Endian*: Byte có trọng số lớn được lưu ở địa chỉ thấp. 
    *Little-Endian*: Byte có trọng số nhỏ được lưu ở địa chỉ thấp. 

- **Calling Convention (Quy ước gọi hàm)** là quy ước truyền tham số và quản lý stack khi gọi hàm. 

    *cdecl*: Tham số được truyền từ phải sang trái, caller dọn dẹp stack. 
    *stdcall*: Tham số được truyền từ phải sang trái, callee dọn dẹp stack. 
    *fastcall*: Một số tham số đầu tiên được truyền qua thanh ghi để tăng tốc. 
    *thiscall*: Dùng trong lập trình hướng đối tượng, truyền this vào thanh ghi. 

++2. Chương trình asm trên Windows (MASM)++

>Download MASM32: https://www.masm32.com/
>Cài đặt biến môi trường: `C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.42.34433\bin\Hostx86\x86`

- Sau khi Install, mở file 'qeditor' trong file 'masm32' mới vừa cài đặt và viết chương trình xong lưu file với đuôi `.asm`.
![Untitled 1_15_2025 9_52_49 PM](https://hackmd.io/_uploads/rk2pl8BwJg.png)

- `include \masm32\include\masm32rt.inc`: Dòng này bao gồm (include) *file masm32rt.inc*. File này chứa các định nghĩa và macro cần thiết.
`.data`: Khai báo phần dữ liệu của chương trình. Đây là nơi chứa các biến và hằng số.
`msg db "Hello World!",0`: Khai báo một biến có tên msg kiểu byte (db - define byte) chứa chuỗi "Hello World!". Số 0 ở cuối chuỗi là đánh dấu kết thúc chuỗi.
`.code`: Khai báo phần mã lệnh của chương trình.
`_start:`: Đánh  dấu điểm bắt đầu của chương trình.
`push offset msg`: Lệnh *push* đẩy một giá trị lên stack. *offset msg* lấy địa chỉ của biến msg và đẩy nó lên stack. Hàm StdOut sẽ lấy tham số này từ stack.
`call Stdout`: Lệnh *call* gọi một hàm. Ở đây, hàm được gọi là *StdOut*. Hàm này có nhiệm vụ in chuỗi được trỏ bởi địa chỉ trên stack ra màn hình.
`end _start`: Kết thúc chương trình. 
![C__masm32_thuchanh_h.asm 1_15_2025 9_26_20 PM](https://hackmd.io/_uploads/SyOHU8Sv1g.png)

- Chọn 'Console Assemble & Link' ở mục 'Project' thì thấy có thêm file `.exe` và file `.obj` như hình có nghĩa là đã biên dịch thành công.
![Untitled 1_15_2025 10_11_40 PM](https://hackmd.io/_uploads/SyDteLBvJl.png)

- Sau đó vào Command Prompt (Cmd) và nhập <tên file> xong nhấn Enter.
![Screenshot (91)](https://hackmd.io/_uploads/SykELUrwJl.png)

++3. Chương trình asm trên Linux (NASM)++

>Mở Linux Terminal, nhập 'whereis nasm'. Nếu đã cài đặt, thì một dòng như `nasm: /usr/bin/nasm` sẽ xuất hiện. Nếu không, bạn sẽ chỉ thấy `nasm:`, thì bạn cần cài đặt NASM.

- Vào Teminal, nhập `sudo apt-get install nasm` để cài đặt. Sau đó, nhập `nano <tênfile>.asm`.
![ubuntu [Running] - Oracle VirtualBox 1_16_2025 2_06_04 AM](https://hackmd.io/_uploads/rkARqFBwkg.png)

- Cấu trúc chương trình gồm 3 phần chính: text section, data section, bss section.
`mov eax, 4`: Gán giá trị 4 cho thanh ghi eax. Giá trị này tương ứng với system call sys_write (ghi dữ liệu ra file).
`mov ebx, 1`: Gán giá trị 1 cho thanh ghi ebx. Giá trị này tương ứng với file descriptor 1, là standard output (stdout).
`mov ecx, msg`: Gán địa chỉ của chuỗi msg (đã được định nghĩa trong section .data) cho thanh ghi ecx (ecx chứa địa chỉ của buffer, chứa dữ liệu cần in).
`mov edx, len`: Gán độ dài của chuỗi msg (đã được tính toán và gán cho len) cho thanh ghi edx (edx chứa số byte cần in).
`int 0x80`: Thực hiện lời gọi hệ thống (system call). Lệnh này sẽ chuyển quyền điều khiển cho kernel (nhân hệ điều hành) để thực hiện system call đã được chỉ định trong eax. Trong trường hợp này, kernel sẽ thực hiện việc ghi dữ liệu từ địa chỉ được chỉ định trong ecx với độ dài được chỉ định trong edx ra stdout.
`msg db "Hello World!", 0xa`: Khai báo một chuỗi byte (byte string) có tên msg chứa nội dung "Hello World!". 0xa là mã ASCII của ký tự `\n` (xuống dòng).
`len equ $ - msg`: Tính toán độ dài của chuỗi msg. `$` đại diện cho địa chỉ hiện tại trong bộ nhớ, và `msg` là địa chỉ bắt đầu của chuỗi. Do đó, $ - msg sẽ cho ra số byte từ đầu chuỗi đến vị trí hiện tại, tức là độ dài của chuỗi. `equ` (equates '=') để gán một giá trị.
![ubuntu [Running] - Oracle VirtualBox 1_16_2025 2_04_36 AM](https://hackmd.io/_uploads/BkLJiFBD1x.png)

- Viết chương trình xong thì Ctrl+X để thoát.
`nasm -f elf64 -o <tênfile>.o <tênfile>.asm`
`ld <tênfile>.o -o <tênfile>`
`./<tênfile>`
![ubuntu [Running] - Oracle VirtualBox 1_16_2025 2_16_22 AM](https://hackmd.io/_uploads/SyTJsKHvJg.png)
