# Intel-based Assembly

[List_of_Intel_microprocessors](https://en.wikipedia.org/wiki/List_of_Intel_microprocessors)

## Môi trường thực thi cơ bản

* General-purpose registers (Thanh gi múc đích chung)
* Index and base registers (Thanh gi chỉ mục và cơ sở)
* Specialized register uses (Thanh gi sử dụng chuyên biệt)
* Status flags (Trạng thái các cờ)
* Floating-point, MMX, XMM registers (Thanh gi cho dữ liệu dấu phẩy động)

### Một vài thanh gi chuyên biệt

* General-Purpose (mục đích chung)

    * RAX/EAX - accumulator (lưu trữ)
    * RCX/RCX - loop counter (biến đếm)
    * RSP/ESP - stack pointer (con trỏ ngăn xếp)
    * RSI/ESI, RDI/EDI - index register (thanh gi chỉ mục)

* RIP/EIP/IP - intruction pointer (con trỏ lệnh)
* Rflags/Eflags 
    * quản lý trạng thái của cờ
    * mỗi cờ là một bit nhị phân (0 huặc 1)

* Trạng thái cờ

    * Carry flags: cờ được bật khi mà một câu lệnh tạo ra kết quả là một số quá lớn (huặc quá nhỏ) cho toán hạng đích (destination).
    * Zero flags: cờ được bật khi mà kết quả của một phéo toán bằng 0.
    * Sign Flags: được bật khi mà toán hạng đích là một số âm, được tắt khi mà toán hạng địch là một số dượng.
    * Overflow flags: được bật khi mà một câu lệnh tạo ra kết quả là một số có dấu không hợp lệ.
    * Parity flags: được bật khi tổng của 1 bit là số chẵn.

## Định nghĩa kiểu dữ liệu

```variableName: .Type value```

vd: ``` VNgoal: .int 2```

### Kiểu toán hạng

* Trực tiệp - Kiểu hằng số nguyên
    * Imm8, imm16, imm32, imm64
* Thanh gi - Tên của một thanh gi
    * r8, r16, r32, r64
* Tham chiếu vị trí trong bộ nhớ
    * m8, m16, m32, m64


__Quy ước:__

![h3](https://i.imgur.com/2XHghxo.png)

## Các câu lệnh

#### Lệnh MOV

* Move từ source đến destionation

    __Cú pháp:__ ```mov source, destination```

    __Quy định:__ Hai toán hạng source và destination phải cùng kích thước, và không có nhiều hơn một biến được sử dụng

    __Ví dụ:__ 
                ```
                    mov $5, %rax
                    mov c, %rbx
                    mov %rbx, %rax
                ```

#### Truy cập giá trị trong mảng

* Truy cập trực tiệp phần tử trong mảng bằng chỉ số
    __Cú pháp:__  ```nameArray(, position, sizeOfTyped)```

    __Ví dụ:__ 

            ```
                myarray: .int 3,6,4,8,4,7,3,6
                xor %ebx, %ebx
                mov myarray(,ebx,4), %eax
            ```
    __int có kích thước là 4 byte, ebx có giá trị là 0. Câu lệnh trên là truy cập phần tử thứ 0 của mảng myarray__

#### Addition and Subtraction

##### Overview
*  Increasing and Decreasing
    * inc
    * dec
* Đổi dấu
    * neg
* Các phép toán số học
* Status flags thay đổi sau khi thực hiện các phép toán số học
    * Zero, Sign, Carry, Overflow

##### Câu lệnh INC and DEC 

* Cộng một và trừ một từ toán hạng địch
    __Toán hạng có thể là một thanh gi huặc một tham chiếu bộ nhớ__
* Cú pháp:

    ``` inc destiantion```
    ``` dec destination```

##### Câu lệnh add và sub

* Cộng/Trừ vào source vào destination
* Cú pháp:

    ``` add source, destination```
    ``` sub source, destination```

* Luật: Các toán hạng source và destination phải cùng kiểu và chỉ có nhiều nhất một biến được sử dụng

* Ví dụ: 

```
var1: .int 5
var2: .int 9

mov var1, %eax
mov var2, %ebx

add %ebx, %eax    # eax += ebx
sub %ebx, %eax    # eax -= ebx
```

##### Câu lệnh NEG

* Đổi dấu của toán hạng, toán hạng có thể là một thanh gi huặc là một tham chiếu bộ nhớ
* Cú pháp: 
    ```neg destination```
* Ví dụ:
```
valB: .BYTE -1
valW .int +32767
…
mov valB,%al    # AL = -1
neg %al         # AL = +1
neg valW        # valW = -32767
```

#### Lệnh nhân và chia

* phép nhân không dấu 

![h4](https://i.imgur.com/svSd0mK.png)


* Phép chia không dấu

| Số bị chia    | số chia   | Thương    | Số dư     |
| ----------    |---------- | ----------|---------- |
| AX            | r8/m8     | AL        | AH        |
| DX:AX         | r16/m16   | AX        | DX        |
| EDX:EAX       | r32/m32   | EAX       | EDX       |
| EDX:RAX       | r64/m64   | RAX       | RDX       |

#### Cờ trạng thái thay đổi sau khi thực thiện các phép số học

* Lệnh __mov__  không làm thay đổi giá trị của các cờ
* Zero flags được set khi mà toán hạng destination bằng 0
* Carry flags được set khi mà một phép toán làm cho giá trị của một số không dấu vượt ra ngoài khoảng giá trị
* Overflow flags được set khi mà một phép toán làm cho giá trị của một số có dấu vượt ra ngoài khoảng giá trị
* Sign flags được bật khi mà toán hạng destination là một số âm


#### Lệnh nhảy JMP

* JMP  là một lệnh không điều kiện, nhảy đến một label.

* Cú pháp: ```jmp label```

#### Lệnh so sánh CMP

* Cú pháp: ```cmp source, destination```
* So sánh toán hạng destination với toán hạng source

* Source có thể là một thanh gi, biến, huặc hằng số

#### Jump conditional instruction

* Jcond Instruction là lệnh nhảy có điều kiện, nhảy được thực thi khi mà  thanh gi chỉ định huặc cờ được thỏa mãn điều kiện.

* 