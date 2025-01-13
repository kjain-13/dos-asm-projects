0150 : clear screen
0161 : set cursor in the middle of screen
016c : print '*'
0180 : delete '*'
0194 : print '#'
01B0 : input a char 
01B5 : if-else-statement for movement
01ed : print '$'
0200 : read attribute
0207 : "GameOver" display
021A : comparison in enter
// 233 


//100
.clear screen{
    mov ax,0700
    mov bh,07
    mov cx,0
    mov dx,184f
    int 10

    mov dx,0c28
    mov bh,00
    mov ah,02
    int 10
}

.read Screen{
    mov ah,08
    mov bh,00
    int 10
    cmp al,23
    jz movement
    cmp al,24
    jz movement
    call print(*)
}

// 129
.movement{
    mov ah,00
    int 16
    cmp ah,50
    jnz 0138 
    inc dh
    jmp NextPlace
    0138 : cmp ah,48
    jnz 0141
    dec dh
    jmp NextPlace
    0141 : cmp ah,4B
    jnz 014A
    dec dl
    jmp NextPlace
    014A : cmp ah,4D
    jnz 0153
    inc dl
    jmp NextPlace
    0153 : cmp al,71
    jnz 15B
    mov ah,4c
    int 21
    015B : cmp ah,1C
    jnz 012B
    call sub;
    jmp 012B
}

// 170
.print('*'){
   z
    ret
    // works
}

// 182
.print('#'){
    mov ah,02
    mov bh,00
    int 10
    mov ax,0923
    mov bx,7
    mov cx,1
    int 10
    ret
    // works
}
// 194
.print('$'){
    mov ah,02
    mov bh,00
    int 10
    mov ax,0924
    mov bx,7
    mov cx,1
    int 10
    ret
    // works
}

// 240
.remove('*'){
    mov ax,092A
    mov bx,7
    mov cx,1
    int 10
    ret
    // works
}

// 01A6-1B0
wrong code{
    remove(*)
}


// 1b1
.nextplace{
    mov ah,08
    mov bh,00
    int 10
    cmp al,2A
    jnz 1Be
    call 240
    call 1C4
    jmp 118
}

// 1C4
.print('*') if(place != '#' || '$'){
    mov ah,02
    mov bh,00
    int 10
    mov ah,08
    int 10
    cmp al,23
    jz 1d9
    cmp al,24
    jz 1d9
    call 170
    ret
}


// 1e0
.enterKey{
    mov si,200
    mov ax,[si]
    cmp ax,dx
    jnz 01f1
    call 194
    ret
    add si,02
    mov cx,[255]
    dec cx
    mov [225],cx
    jnz 1e4
    ret
}

// 250
.sub{
    call 240
    call 1e0
    ret
}

.horizontalBorder(){
    mov dx,0419
    mov bh,00
    mov ah,02
    int 10
    mov ax,0923
    mov bx,7
    mov cx,20
    int 10

    mov dx,1419
    mov bh,00
    mov ah,02
    int 10
    mov ax,0923
    mov bx,7
    mov cx,20
    int 10


    mov dx,0519
    again :
     mov bh,00
    mov ah,02
    int 10
    cmp dh,14
    jz exit

    mov dl,23
    mov ah,02
    int 21

    inc dh
    mov dl,19

    exit: 

    mov dx,0539
    again : mov bh,00
    mov ah,02
    int 10
    cmp dh,14
    jz exit1

    mov dl,23
    mov ah,02
    int 21

    inc dh
    mov dl,19
    jmp again

    exit1: 
    mov ah,00
    int 16
    mov ah,4c
    int 21


}