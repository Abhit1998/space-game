# space-game
import pygame
pygame.init()
import time
import random

dwidth=1200
dheight=650

HeroImage=pygame.image.load("Hero.gif")
FireImage=pygame.image.load("HeroFire.png")
Enemy1=pygame.image.load("Enemy2.png")
clock=pygame.time.Clock()

    
surface=pygame.display.set_mode((dwidth,dheight))



def Fire(f1,f2):
    surface.blit(FireImage,(f1,f2))
def Enemy(e1,e2):
    surface.blit(Enemy1,(e1,e2))

def Hero(x,y):
    surface.blit(HeroImage,(x,y))
    #print (x,y)
def main():
    Play="ON"
    x=dwidth*.41
    startF="NO"
    startF2="NO"
    y=dheight*.79
    Hero(x,y)
    x_change=0
    y_change=0
    black=(0,0,0)
    i=y
    j=y
    HeroSize=[195,138]
    lvl1="NO"
    enemyMotion=25
    f1=-140
    f2=-140
    pygame.display.update()
    while Play=="ON":
        for event in pygame.event.get():
            if event.type==pygame.KEYDOWN:
            
                if event.key==pygame.K_LEFT:
                    x_change=-4
                elif event.key==pygame.K_RIGHT:
                    x_change=4
                elif event.key==pygame.K_UP:
                    y_change=-4
                elif event.key==pygame.K_DOWN:
                    y_change=4
                elif event.key==pygame.K_SPACE:
                    if startF2=="YES" and startF=="YES":
                        continue
                        
                    elif startF=="YES":
                        startF2="YES"
                        j=y
                        f2=x+120
                    elif startF=="NO":
                        i=y
                        startF="YES"
                        f1= x+60
                elif event.key==pygame.K_x:
                    if lvl1=="YES":
                        pass
                    lvl1="YES"
                    e1=50
                    e2=50
                    
            elif event.type==pygame.KEYUP:
                if event.key==pygame.K_LEFT or event.key==pygame.K_RIGHT :
                    x_change=0
                elif event.key==pygame.K_DOWN or event.key==pygame.K_UP:
                    y_change=0
                elif event.key==pygame.K_SPACE:
                    pass
                
            elif event.type==pygame.QUIT:
                Play="OFF"
        x=x+x_change
        y=y+y_change
        

        if x<=0:
            x=0
        if y<=0:
            y=0
        if y>=512:
            y=512
        if x>=1000:
            x=1000
       # print (event.type)
        surface.fill((98,45,89))
        Hero(x,y)
        
        if startF=="YES":     #For Bullet Fire1
            Fire(f1,i-40)
            i=i-5
        if startF2=="YES":    #For Bullet Fire2
            Fire(f2,j-40)
            j=j-5
        if i<=0:
            startF="NO"
        if j<=0:
            startF2="NO"

        if lvl1=="YES":
            if enemyMotion==25:
                Edirection=random.randint(1,4)
                enemyMotion=0
            if Edirection==1:
                e1=e1+3
                enemyMotion+=1
            elif Edirection==2:
                e2=e2+3
                enemyMotion+=1
            elif Edirection==3:
                e1=e1-3
                enemyMotion+=1
            elif Edirection==4:
                e2=e2-3
                enemyMotion+=1
            if e1<=0:
                e1=0
                Edirection=random.randint(1,2)
                enemyMotion=0
            if e2<=0:
                e2=0
                Edirection=random.randint(1,3)
                enemyMotion=0
            if e2>=400:
                e2=400
                Edirection=random.randint(3,4)
                enemyMotion=0
            if e1>=1000:
                e1=1000
                Edirection=random.randint(2,4)
                enemyMotion=0
            #print (e1,e2)
            Enemy(200,250)
            pygame.display.update()
            if (250==i or i<250+15) and (200==f1 or f1<200+15) :
               print ("Blast")
               i=y
               startF="NO"
            if(250==j or j<250+15) and (200==f2 or f2<200+15)  :
                print ("Blast from 2")
                startF2="NO"
                j=y
        
        pygame.display.flip()
        clock.tick(90)
        
        
main()
pygame.quit()
