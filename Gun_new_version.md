from random import randrange as rnd, choice
import tkinter as tk
import math
import time
from tkinter import *
from PIL import Image, ImageTk
# print (dir(math))

root = tk.Tk()
fr = tk.Frame(root)
root.geometry('1300x750')
canv = tk.Canvas(root, bg='white')
canv.pack(fill=tk.BOTH, expand=1)






bacground_obj = PhotoImage(file = "C:\\Users\\NIKITA\\Desktop\\Gun\\Background.png")
canv.create_image(0, 0, anchor = NW, image = bacground_obj)


class ball():

    def __init__(self, x=-40, y=450):
        """ Конструктор класса ball

        Args:
        x - начальное положение мяча по горизонтали
        y - начальное положение мяча по вертикали
        """
        self.x = x
        self.y = y
        self.r = 10
        self.vx = 0
        self.vy = 0

        self.color = choice(['blue', 'green', 'red', 'brown'])
        self.id = canv.create_oval(
                self.x - self.r,
                self.y - self.r,
                self.x + self.r,
                self.y + self.r,
                fill=self.color
        )
        self.live = 1

    def set_coords(self):
        self.bullet_obj = PhotoImage(file = "C:\\Users\\NIKITA\\Desktop\\Gun\\bomb.png")
        self.id = canv.create_image(self.x, self.y, anchor = NW, image = self.bullet_obj)
        
    def delete(self):
        """Delete the object form the canvas.
        Args:
        """
        canv.delete(self.id)

    def move(self):
        """Переместить мяч по прошествии единицы времени.

        Метод описывает перемещение мяча за один кадр перерисовки. То есть, обновляет значения
        self.x и self.y с учетом скоростей self.vx и self.vy, силы гравитации, действующей на мяч,
        и стен по краям окна (размер окна 800х600).
        """
        # FIXME
        g = 4
        self.x += self.vx
        self.y += self.vy + g/2
        self.vy += 0.5*g
        

        if self.x + self.r > 1300:
            self.x = 2 * (1300 - self.r) - self.x
            self.vx *= -0.7
            self.vy *= 0.7
        if self.x - self.r < 0:
            self.x = 2 * self.r - self.x
            self.vx *= -0.7
            self.vy *= 0.7

        if self.y + self.r > 750:
            self.vy -= g * (750 - self.r - self.y) / (self.vy + g / 2)
            self.y = 2 * (750 - self.r) - self.y
            self.vx *= 0.7
            self.vy *= -0.7
        if self.y - self.r < 0:
            self.y = 2*self.r - self.y
            self.vx *= 0.7
            self.vy *= -0.7
        

    def hittest(self, obj):
        """Функция проверяет сталкивалкивается ли данный обьект с целью, описываемой в обьекте obj.

        Args:
            obj: Обьект, с которым проверяется столкновение.
        Returns:
            Возвращает True в случае столкновения мяча и цели. В противном случае возвращает False.
        """
        # FIXME
        if (t1.x - self.x)**2 + (t1.y - self.y)**2 <= (t1.r+self.r)**2:
            return True
        else:
            return False



class Bomb():
    def __init__(self):

        self.points = 0
        self.live = 1
        self.vx = 0
        self.vy = 20

        # FIXME: don't work!!! How to call this functions when object is created?
        self.id = canv.create_oval(5,5,5,5)
        self.id_points = canv.create_text(30,30,text = self.points,font = '28')
        self.new_boomb()
   

    def set_coords(self):
        canv.coords(
                self.id,
                self.x - self.r,
                self.y - self.r,
                self.x + self.r,
                self.y + self.r
        )

    def new_boomb(self):
        """ Инициализация новой цели. """
        x = self.x = g2.x+30
        y = self.y = 100
        r = self.r = rnd(10, 15)
        color = self.color = 'red'
        canv.coords(self.id, x-r, y-r, x+r, y+r)
        canv.itemconfig(self.id, fill=color)

    
    def boomb_move(self):
        """Переместить цель по прошествии единицы времени.

        Метод описывает перемещение цеди за один кадр перерисовки. То есть, обновляет значения
        self.x и self.y с учетом скоростей self.vx и self.vy,
        и стен по краям окна (размер окна 1300х750).
        """
        
        self.y += self.vy
        

    def booom(self, obj):
        """Попадание шарика в цель."""
        global g1
        if obj.x+100> self.x > obj.x and self.y == obj.y:
            return True

        else:

            return False

    


class gun():
    def __init__(self, x = 300, y = 640):
        self.f2_power = 10
        self.f2_on = 0
        self.type = 1
        self.an = 0
        self.y = y
        self.x = x
        self.vx = 0
        self.filename = 'ship.png'
        self.vy = 0
        self.live = 1
        image = Image.open(self.filename)
        self.gun_obj = ImageTk.PhotoImage(file = "C:\\Users\\NIKITA\\Desktop\\Gun\\ship.png")
        self.id = canv.create_image(x, y, anchor = NW, image = self.gun_obj)
   
        

    def fire2_start(self, event):
        self.f2_on = 1

    def fire2_end(self, event):
        """Выстрел мячом.

        Происходит при отпускании кнопки мыши.
        Начальные значения компонент скорости мяча vx и vy зависят от положения мыши.
        """
        global balls, bullet
        bullet += 1
        new_ball = ball()
        new_ball.r += 5
        self.an = 3*math.pi/2
        self.an = math.atan((-event.y+self.y) / (event.x-self.x))
        if self.an > 0:
            new_ball.vx = 40*math.cos(self.an)
        if self.an < 0:
            new_ball.vx = -40*math.cos(self.an)
        new_ball.vy = -50
        new_ball.y = self.y
        new_ball.x = self.x+35
        balls += [new_ball]
        self.f2_on = 0
        self.f2_power = 10

    def move_left(self, event):
        self.vx = -10
        
    def move_right(self, event):
        self.vx = 10
    def move_up(self, event):
        self.vy = 10
        
    def move_down(self, event):
        self.vy = -10
    
    def move(self):
        
        self.x += self.vx
        self.y += self.vy
        self.vx = 0
        self.vy = 0
        root.bind('<a>', g1.move_left)
        root.bind('<d>', g1.move_right)
        root.bind('<s>', g1.move_up)
        root.bind('<w>', g1.move_down)
        canv.coords(self.id, self.x, self.y)

    def rotate(self, event):
        global image
        image = self.gun_obj
        
        
        self.an = math.atan((event.y-self.y) / (event.x-self.x))
        
        
        tkimage = image.transpose(PIL.Image.ROTATE_90)
        self.id = canv.create_image(self.x, self.y,anchor=NW, image=tkimage )
        canv.itemconfig(self.id)
    
class gun2():
    def __init__(self, x = 0, y = 0):
        self.an = 0
        self.y = y
        self.x = x
        self.vx = 10
        self.filename = 'ship2.png'
        self.vy = 0
        self.live = 1
        image = Image.open(self.filename)
        self.gun2_obj = ImageTk.PhotoImage(file = "C:\\Users\\NIKITA\\Desktop\\Gun\\ship2.png")
        self.id = canv.create_image(x, y, anchor = NW, image = self.gun2_obj)
   
        

    
    
    def move(self):
        
        self.x += self.vx
        self.y = 0
        if self.x > 1300:
            self.x = 1300
            self.vx = -10
        if self.x < 0:
            self.vx = 10
        
        canv.coords(self.id, self.x, self.y)

    
        



class target():
    def __init__(self):

        self.points = 0
        self.live = 1
        self.vx = 10
        self.vy = 10

        # FIXME: don't work!!! How to call this functions when object is created?
        self.id = canv.create_oval(5,5,5,5)
        self.id_points = canv.create_text(30,30,text = self.points,font = '28')
        self.new_target()
   

    def set_coords(self):
        canv.coords(
                self.id,
                self.x - self.r,
                self.y - self.r,
                self.x + self.r,
                self.y + self.r
        )

    def new_target(self):
        """ Инициализация новой цели. """
        x = self.x = rnd(600, 780)
        y = self.y = rnd(300, 550)
        r = self.r = rnd(20, 25)
        color = self.color = 'green'
        canv.coords(self.id, x-r, y-r, x+r, y+r)
        canv.itemconfig(self.id, fill=color)



    def target_move(self):
        """Переместить цель по прошествии единицы времени.

        Метод описывает перемещение цеди за один кадр перерисовки. То есть, обновляет значения
        self.x и self.y с учетом скоростей self.vx и self.vy,
        и стен по краям окна (размер окна 800х600).
        """
        self.x += self.vx
        self.y += self.vy
       
        

        if self.x + self.r > 1300:
            self.x = 2 * (1300 - self.r) - self.x
            self.vx *= -1
            self.vy *= 1
        if self.x - self.r < 0:
            self.x = 2 * self.r - self.x
            self.vx *= -1
            self.vy *= 1

        if self.y + self.r > 750:
            self.y = 2 * (750 - self.r) - self.y
            self.vx *= 1
            self.vy *= -1
        if self.y - self.r < 0:
            self.y = 2*self.r - self.y
            self.vx *= 1
            self.vy *= -1

    def hit(self, points=1):
        """Попадание шарика в цель."""
        canv.coords(self.id, -10, -10, -10, -10)
        self.points += points
        canv.delete(self.id)
        canv.itemconfig(self.id_points, text=self.points)

screen1 = canv.create_text(40, 100, text='', font='30')
g1 = gun()
g2 = gun2()
boombs = []

bullet = 0
balls = []


targets= []

def make_bomb(event):
    
        
    b1 = Bomb()
    b1.new_boomb()
    boombs.append(b1)

def make_targets(event):
    t1 = target()
    t1.new_target()
    targets.append(t1)
    for t1 in targets: 
        t1.live = 1

def new_game(event=''):
    global g1, t1, b1, screen1, balls, bullet, targets, boombs

    
    g1.move()
    root.bind('<Button-1>', g1.fire2_end)
    
    root.bind('<Double-Button-1>', make_bomb)
    root.bind('<ButtonRelease-1>', make_targets)
    root.bind('<Motion>', g1.rotate)
    
    
    
    bullet = 0
    balls = []
    boombs = []

    z = 0.03
    

    screen2 = canv.create_text(600, 300, text='', font='70')

    while balls or g1.live or bombs:
        g2.move()
        if g2.x % 300 ==0:
            b1 = Bomb()
            b1.new_boomb()
            boombs.append(b1)
        for b1 in boombs:    
            b1.boomb_move()
            b1.set_coords()
            if b1.booom(g1):

                canv.delete(g1.id)
                canv.itemconfig(screen2, text='Вы проиграли((((((((', font=('Arial',50,'bold italic'), fill = 'blue')
                root.after(3000, canv.destroy)

        



        g1.move()
        g1.live -= 0.01
        for t1 in targets:
            t1.target_move()
            t1.set_coords()
        canv.update()

        


        for b in balls:
            if b.live <= 0:
                b.delete()
            else:
                b.move()
                
                b.live -= 0.01
                b.set_coords()
                for t1 in targets:
                    if b.hittest(t1) and t1.live:
                        t1.live = 0
                        
                        t1.hit()
                        canv.bind('<Button-1>', '')
                        canv.bind('<ButtonRelease-1>', '')

                        canv.itemconfig(screen1, text='Points ' + str(bullet))
            canv.update()
        time.sleep(0.03)
        
        

    canv.itemconfig(screen1, text='')
    canv.delete(gun)
    root.after(750, new_game)


new_game()

root.mainloop()