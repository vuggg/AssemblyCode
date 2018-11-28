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

## Bài 2: Viết đoạn mã assembly thực hiện lệnh sau (tính số thứ n của dãy fibonaci)

* Code C++
```
ecx=1; 
ebx=1;

for(eax=1; eax<n-2; eax++) 
{
    ecx+=eax;
    ebx=ecx;
}
```

* Code Assembly

```
mov $1, %ecx
mov $1, %ebx
move n, %edx
sub $2, %edx

while: cmp  %edx, %eax
jae endwhile
add %eax, %ecx
mov %ecx, %eax
inc %eax
jmp while

endwhile:
```

## Bài 3: Viết đoạn mã assembly thực hiện lệnh sau:

* Code C++:
```
ecx=a; 
eax=0;
while(ecx>0) { eax+=ecx; ecx--;} 
```

* Code Assembly

```
mov a, %ecx
mov $0, eax
while: cmp $0, %ecx
jbe endwhile
add %ecx, %eax
dec %ecx
jmp while

endwhile:
```

## Bài 4: Viết đoạn mã assembly thực hiện lệnh sau

```
int a=5,q=3,n=10;
ecx=a; 
eax=0;
for(edx=1; edx<n; edx++)
{
    eax+=ecx*q;
}
```

```
a: .int 5
q: .int 3
n: .int 10

mov a, %eax
mul q
mov %eax, %ebx
mov a, %ecx
mov $0, %eax
while: cmp n, %edx
jae endwhile
add %ebx, %eax

endwhile:

```

## Bài 5: 57 Viết đoạn mã assembly thực hiện lệnh sau:
```
int a[8], n=8;
eax=0;
ecx=0;
while (ecx < n) eax += a[ecx++] ; 
```

```
a: .int 5,7,2,4,5,7,9,3
n: .int 8

mov $0, %ecx
mov $0, %eax
while: cmp n, %ecx
jae endwhile
add a(,%ecx,4), %eax
inc %ecx
jmp while

endwhile:
```

## Bài 6: Viết chương trình Assembly giải phương trình bậc nhất ax+b=0 trong đó a và b là các số thực kiểu double

```
Xmm1=a; xmm2=b;xmm3=0;
if(Xmm1==xmm3)
{
    if(xmm2!=xmm3) edx=-1;
    else edx=0;
}
else
{
    edx=1;
    xmm0=-xmm2/xmm1;
}
```

```
movsd a, %xmm1
movsd b, %xmm2
xorps %xmm0, %xmm0

ucomisd %xmm1, %xmm3
jne L1
ucomisd %xmm2, %xmm3
je L2
mov $0, %edx
jmp endif

L1:

mov %1, %edx
subsd %xmm2, %xmm0
movsd %xmm0, %xmm2
divsd %xmm1, %xmm2
movsd %xmm2, %xmm1

L2:
mov $1, %edx
neg %edx
```


