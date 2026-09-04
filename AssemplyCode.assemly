.model small
.stack 100h
.data 

menu db 0dh,0ah,0dh,0ah,' BUS RESERVATION SYSTEM ',0dh,0ah,0dh,0ah
db ' 1- Displaying all available Buses and their details ',0dh,0ah
db ' 2- Booking a Bus ',0dh,0ah
db ' 3- Calculating Total Price ',0dh,0ah
db ' 4- Exit the application ' ,0dh,0ah,'$'

msg db 0dh,0ah,0dh,0ah,' Pleace select your option: $',0dh,0ah
 
bus_sch db 0dh,0ah,0dh,0ah,"  Buses schedule ",0dh,0ah
db "  ----------------------------------------------------------------------",0dh,0ah
db "  | Bus Number   | Departure Destination | Departure Time | Ticket Price|",0dh,0ah
db "  ----------------------------------------------------------------------",0dh,0ah
db "  | Bus 101      | Riyadh - Jeddah       | 9:00 AM        | 100 SAR     |",0dh,0ah
db "  ----------------------------------------------------------------------",0dh,0ah
db "  | Bus 102      | Riyadh - Dammam       | 11:00 PM       | 120 SAR     |",0dh,0ah
db "  ----------------------------------------------------------------------",0dh,0ah
db "  | Bus 103      | Jeddah - Riyadh       | 21:00 PM       | 90 SAR      |",0dh,0ah
db "  ----------------------------------------------------------------------",0dh,0ah,'$' 

apo db 0dh,0ah,0dh,0ah, ' Sorry, not Available  :( , press any character to try again $',0dh,0ah
return db 0dh,0ah,0dh,0ah,' Press any character , to return to the menu: $',0dh,0ah 
stu db 0dh,0ah,0dh,0ah, ' Are you a student? if you are Press "S" to get 30% discount, if not press any character $',0dh,0ah
total_msg db 0dh,0ah,0dh,0ah, '  The total price is: $',0dh,0ah
total_msgD db 0dh,0ah,0dh,0ah,' The total price after discount is: $',0dh,0ah
end_msg db 0dh,0ah,0dh,0ah, ' Thank you for using our bus reservation system, have a nice day <3 $'
no_booking db 0dh,0ah,0dh,0ah,' sorry, you dont have any booking yet $',0dh,0ah 
n70 dw 70
n100 dw 100
total dw ?

.code
main proc
mov ax,@data
mov ds,ax 


START:    
mov ah,9
lea dx, menu 
int 21h

mov ah,9 
lea dx, msg 
int 21h

mov ah,1  
int 21h
;----------------
cmp al,"1"
jl out_of_menu 
cmp al,"4"
jg out_of_menu

cmp al,"1" 
je show_sch
  
cmp al,"2"
je reserve
 
cmp al,"3"
je calculate

cmp al,"4"
je exit
;---delete jmp start------------ 
  

OUT_OF_MENU:
mov ah,9
lea dx,apo
int 21h

mov ah,1  
int 21h
jmp start
;--------------

SHOW_SCH:
mov ah,9 
lea dx,bus_sch
int 21h

jmp start
;--------------

RESERVE:
mov ah,9 
lea dx,bus_sch
int 21h

mov ah,9
lea dx,msg
int 21h

call indec 
mov bx,ax
 
cmp bx,101
jl out_of_sch 
cmp bx,103
jg out_of_sch  
jmp start
;-----------------
OUT_OF_SCH: 
mov ah,9
lea dx,apo
int 21h

mov ah,1 
int 21h
jmp reserve
;----------------

CALCULATE: 
cmp bx,101
je price_100

cmp bx,102
je price_120

cmp bx,103
je price_90  

jmp NO__BOOKING:
;--------------------
PRICE_100:
mov total,100
jmp bill

PRICE_120:
mov total,120
jmp bill

PRICE_90:
mov total,90
jmp bill

NO__BOOKING:
mov ah,9 
lea dx,no_booking 
int 21h 

mov ah,1  
int 21h
jmp start
;--------------------------
BILL:
mov ah,9 
lea dx,stu 
int 21h

mov ah,1 
int 21h

cmp al,"S" 
je dis_30
cmp al,"s"
jne no_dis 

;------------------------
DIS_30: 
mov ax,total 
mul n70 
div n100 
mov total,ax 

mov ah,9 
lea dx,total_msgD
int 21h

mov ax,total
call outdec 

jmp start
 ;------------------------
 
NO_DIS: 
mov ah,9 
lea dx,total_msg 
int 21h

mov ax,total
call outdec 

jmp start

 ;----------------------
EXIT:
mov ah,9 
lea dx,end_msg
int 21h

mov ah,4ch 
int 21h

main endp 
include C:\Users\alrub\Desktop\outdec.asm
include C:\Users\alrub\Desktop\indec.asm
end 
