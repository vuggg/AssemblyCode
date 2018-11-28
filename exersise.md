## Bài 1: Viết đoạn mã assembly thực hiện lệnh sau (tính tổng n số tự nhiên đầu tiên)

* Code C++
```
ecx=0;
for(eax=1;eax<n;eax++) ecx+=eax;
```

* Code Assembly

```
xor %ecx, %ecx
mov $1, %eax
while: cmp $n, %eax
jae endwhile
add %eax, %ecx
inc %eax
jmp while

endwhile:
```

