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

## Bài 7: Viết chương trình tính tổng của một mảng số thực, sau đó in kết quả ra màn hình
```
float a[5]={1.1, 2.2, 3.3, 4.4, 5.5}
unsigned int n=5;
xmm0=0;
for(ecx=0; exc<n; ecx++)
{
    xmm0+=a[ecx];
}
```

```
a: .float 1.1, 2.2, 3.3, 4.4, 5.5
n: .int 5

mov $0, %ecx
xorps %xmm0, %xmm0
while: cmp n, %ecx
jae endwhile
movss a(,%ecx,8), %xmm1
cvtss2sd %xmm1, %xmm1
addsd %xmm1, %xmm0
jmp while

endwhile:
```


## Bài 8: Viết thủ tục sau bằng Assembly
```
void calculate(float *pf, double d, int scale)
{
    *pf=d*(scale+4);
}
```

```

const1: .int 4
mov $pf, %rdi
movsd d, %xmm0
mov scale, %rcx

call calculate // gọi hàm

proc_calculate: 

cvtsi2sd %rcx %xmm1
cvtsi2sd const1, %xmm2

addsd %xmm2, %xmm1
mul %xmm1, %xmm0
movsd %xmm0, 0(%rdi)

```
## Bài 9: Viết hàm sau bằng Assembly

Code C+:

```
double calculate(float pf, double d, int scale)
{
    return pf+d*(scale+4);
}
```


Code Assembly:

```
const1: .int 4

movss %pf, %xmm0
movsd %d, %xmm1
mov scale, %rdi


proc_calculate:

add const1, %rdi
cvtsi2sd %rdi, %xmm2
mulsd %xmm2, %xmm1
svtss2sd %xmm0, %xmm0
add %xmm1, %xmm0
ret
```

## Bài 10: Viết hàm sau bằng Assembly
```
double calculate(long * pf, double d, int scale)
{
    return *pf+d*(scale+4);
}
```

```
const: .int 4
mov $pf, %rdi
movsd d, %xmm0
mov scale, %rsi
call proc_calculate  // gọi hàm

proc_calculate:

add const1, %rsi
cvtsi2sd %rsi, %xmm1
mulsd %xmm1, %xmm0
cvtsi2sdq 0(%rdi), %xmm1
add %xmm1, %xmm0
ret

```

## Bài 11: Viết hàm sau bằng Assembly

```
long calculate(long * pf, double d, int scale)
{
    if (*pf>d) return *pf*scale;
    else return d*scale;
}
```

```
mov $pf, %rdi
movsd d, %xmm0
mov scale, %rsi

proc_calculate:
cvtsi2sdq 0(%rdi), %xmm1
ucomisd %xmm1, %xmm0
jb L1

cvtsi2sd %rsi, %xmm2
mul %xmm2, %xm11
jmp Return

L1:
cvtsi2sd %rsi, %xmm2
mulsq %xmm1, %xmm2
movesd %xmm2, %xmm1
jmp Return


Return:
ret

```

## Bài 12:Viết chương trình tìm ước số chung lớn nhất của hai số nguyên dương a và b.

```
eax=a; ebx=b;

while( eax!=ebx)
{
    if(eax>ebx)eax-=ebx;
    else if (ebx>eax)ebx-=eax;
}
```

mov a, %eax
mov b, %ebx

while: cmp %ebx, %eax
je endwhile
cmp %ebx, %eax
jna L1
cmd %ebx, %eax
jae while
sub %eax, %ebx
jmp while

L1:

sub %ebx, %eax
jmp while

## Bài 12: Viết chương trình tìm bội số chung nhỏ nhất của 2 số nguyên dương a và b.

```
ecx=a; ebx=b;
r8d=ecx*ebx;
while( ecx!=ebx)
{
    if(ecx>ebx) ecx-=ebx;
    else if (ebx>ecx) ebx-=ecx;
}
eax=r8d/ebx;
```

```
mov a, %ecx
mov b, %ebx
mov %ecx, %eax
mul %ebx
mov %eax, %r8d

while: cmp %ebx, %ecx
jne L1
mov %r8d, %eax
mul %ebx

L1:

cmp %ebx, %ecx
ja L2
cmd %ecx, %ebx
ja L3
jmp while

L2: 

sub %ebx, %ecx
jmp while

L3:

sub %ecx, %ebx
```

## Bài 14: Viết chương trình in ra n số đầu tiên của dãy fibonacy

```
r8d=1;
eax=0; 
ebx=1;

for (ecx=n-2; ecx>0; ecx--)
{
    edx=ebx;
    ebx+= eax;
    eax=edx;
    r8d+=ebx;
}
```

```
mov $1, %r8d
mov $0, %eax
mov $a, %ebx

mov n, %ecx
sub $1, %ecx

L1:
mov %ebx, %edx
add %eax, %ebx
mov %eax, %edx
add %ebx, %r8d

loop L1

```

## Bài 15: Viết chương trình tính giai thừa của số nguyên dương n
```
r8d=1;
for(ecx=n; ecx>0; ecx--)r8d*=ecx;
```

```
mov $1, %r8d
mov n, %eax
add $1, %eax
mov %eax, %ecx
mov %r8d, %eax

L1:

mul %ecx

loop L1

mov %eax, %r8d

```



