# cgmt-project
#include<stdio.h>
#include<conio.h>
#include<graphics.h>

/*  ------------------------------------------------------------------------
   This code is a part of the Computer graphics and multimedia lab project
   Aim: To make a scenery including a rainbow

   --> Presented by : Saurav Raj
   --> Branch : CSE

------------------------------------------------------------------------------ */

#define ScreenWidth getmaxx()
#define ScreenHeight getmaxy()
#define GroundY ScreenHeight*0.75

int ldisp=0;


void hut(){
  setcolor(WHITE);
    rectangle(150,180,250,300);
    rectangle(250,180,420,300);
    rectangle(180,250,220,300);
    
    line(200,100,150,180);
    line(200,100,250,180);
    line(200,100,370,100);
    line(370,100,420,180);
    
    setfillstyle(SOLID_FILL, BROWN);
    floodfill(152, 182, WHITE);
    floodfill(252, 182, WHITE);
    setfillstyle(SLASH_FILL, BLUE);
    floodfill(182, 252, WHITE);
    setfillstyle(HATCH_FILL, GREEN);
    floodfill(200, 105, WHITE);
    floodfill(210, 105, WHITE);
}
void DrawManAndUmbrella(int x,int ldisp)
{

circle(x,GroundY-90,10);
line(x,GroundY-80,x,GroundY-30);
line(x,GroundY-70,x+10,GroundY-60);
line(x,GroundY-65,x+10,GroundY-55);
line(x+10,GroundY-60,x+20,GroundY-70);
line(x+10,GroundY-55,x+20,GroundY-70);

line(x,GroundY-30,x+ldisp,GroundY);
line(x,GroundY-30,x-ldisp,GroundY);

pieslice(x+20,GroundY-120,0,180,40);
line(x+20,GroundY-120,x+20,GroundY-70);

}

void Rain(int x)
{
int i,rx,ry;
for(i=0;i<400;i++)
{
 rx=rand() % ScreenWidth;
 ry=rand() % ScreenHeight;
 if(ry<GroundY-4)
 {
  if(ry<GroundY-120 || (ry>GroundY-120 && (rx<x-20 || rx>x+60)))
  line(rx,ry,rx+0.5,ry+4);
 }
}
}
void rainbow() 
{ 
     
    int x, y, i; 
  
    circle(ScreenWidth-100,50,30);
    setfillstyle(SOLID_FILL, YELLOW);
    floodfill(ScreenWidth-100, 50, WHITE);
    
  ldisp=(ldisp+2)%20;
   DrawManAndUmbrella(x,ldisp);
   hut();
    x = getmaxx() / 5;
    y = getmaxy() / 5; 
  
    for (i=30; i<100; i++) 
    { 
        
        delay(50); 
  
   
        setcolor(i/10); 
  
        
        arc(x, y, 0, 180, i-10); 
    }
    getch();
}
void main()
{
  
  int gd=DETECT,gm,x=0;
  
  initgraph(&gd,&gm,"C:\\TurboC3\\BGI");
  while(!kbhit())
  { 
  hut();
  circle(ScreenWidth-100,50,30);
    setfillstyle(SOLID_FILL, YELLOW);
    floodfill(ScreenWidth-100, 50, WHITE);
   line(0,GroundY,ScreenWidth,GroundY);
   Rain(x);
   
   ldisp=(ldisp+2)%20;
   DrawManAndUmbrella(x,ldisp);
   delay(20);
   cleardevice();
   x=(x+2)%ScreenWidth;
}
  ldisp=(ldisp+2)%20;
  DrawManAndUmbrella(x,ldisp);
  rainbow();
  getch();
}

