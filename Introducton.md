# Introduction to Assembly Language

## Mục tiêu

Làm quen với ngôn ngữ assembly

## Introduction

* Ngôn ngữ máy có thể được tạo ra trực tiếp từ java code bằng trình thông dịch

![h1]()

* Ngôn ngữ C/C++ thực thi hanh hơn java vì nó dịch code sang Assembly trước khi dịch sang mã máy.

![h2]()

* Chuyển code C++ sang mã Assembly bằng Visual Studio 2012

...

* Ngôn ngữ Assembly 

Assembly là một ngôn ngữ lập trình, nó rất giống với ngôn ngữ máy (machine Language) nhưng nó sử dụng các ký tự thay vì các mã nhị phân. Nó được chuyển bởi assembler vào các chương trinh thực thi ngôn ngữ máy.

* Assembly Language Tools

Phần mềm được sử dụng vào việc editing, assembling, linking, and debugging ngôn ngữ assembly. Bạn cần một chương trình assembler, a linker, và debugger và một chương trình editor để gõ code assembly.

1. Assembler

Một assembler là một chương trình để chuyển các source-code của chương trình được viết bằng ngôn ngữ assembly sang object file trong ngôn ngữ máy. Các assembler phổ biến được phát triển dùng cho tiêu chuẩn trong các dòng chip của Intel. Một trong số đó là MASM (Macro Assembler form Microsoft), TASM (Turbo Assembler from Borland), NASM (Netwide Assembler for both Windows and Linux), và GNU assembler distributed by the free software foundation. 

2. Linker

Linker là một chương trình giúp kết hợp các object file của chương trình của bạn được tao ra bằng assembler với các opject file khác, và liên kết các thư viện và tạo thành một chương trình thực thi. Bạn cần một tiện ích linker để tạo ra file thực thi.

* Link.exe tạo một file exe từ .obj file

3. Debugger

Debugger là một chương trình cho phép bạn truy vết các thực thi của chương trình và xác định nội dung của các thanh gi và bọ nhớ.

