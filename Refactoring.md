import pygame
from pygame.draw import *

pygame.init()

FPS = 30
screen = pygame.display.set_mode((880, 560))

ORANGE = (255, 145, 34)
BROWN = (178, 68, 68)
BLACK = (45, 0, 45)
WATER = (183, 131, 158)

RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
LIGHTBLUE = (0, 255, 255)
YELLOW = (255, 255, 0)

PINK = (243, 0, 191)
LIGHTBLUE_LAS_1 = (111,205,252)
LIGHTBLUE_LAS_2 = (4,138,205)
GREEN_BLACK = (4,138,1)
PINK_LIGHT = (254,169,163)


#background
rect(screen, (255, 213, 170), (0, 0, 880, 560))
rect(screen, (250, 214, 195), (0, 148, 880, 112))

#Top ridge
def draw_top_scar(color):
    '''Function draws top scar
    Attrubutes:
        color : tuple of 3 int
            color of top scar      
    '''
    polygon(screen, color, [(5, 280), (12, 248), (140, 180), (181,138), (216, 146), (228, 163), (339, 234), (396, 226), (429, 237), (470, 200), (510, 210), (529, 192), (598, 150), (658, 130), (698, 165), (733, 157), (791, 184), (819, 169), (882, 197)])

    surface = pygame.Surface([300, 200], pygame.SRCALPHA)
    pygame.draw.ellipse(surface, (250, 214, 195), [-106, -292, 214, 335])
    screen.blit(surface, [534, 148])

    ellipse(screen, color, (610, 117, 60, 96))
    ellipse(screen, color, (607, 121, 65, 90))
    ellipse(screen, color, (603, 128, 71, 68))
    ellipse(screen, color, (704, 156, 57, 44))
    ellipse(screen, color, (698, 159, 72, 42))
    ellipse(screen, color, (716, 164, 62, 32))
    ellipse(screen, color, (715, 167, 71, 34))
    ellipse(screen, color, (728, 172, 67, 34))


    surface = pygame.Surface([300, 200], pygame.SRCALPHA)
    pygame.draw.ellipse(surface, (250, 214, 195), [-280, -485, 489, 556])
    screen.blit(surface, [12, 180])

#Middle ridge
def draw_midlle_scar(color):
    '''Function draws top scar
    Attrubutes:
        color : tuple of 3 int
            color of midlle scar      
    '''
    polygon(screen, color, [(0, 400), (0, 298), (152, 372), (193, 314), (256, 344), (283, 271), (362, 288), (420, 330), (505, 313), (721, 315), (758, 273), (796, 295), (812, 270), (850, 273), (880, 225), (880, 400)])
    circle(screen, color, (656, 413), 178)
    polygon(screen, color, [(729, 345), (721, 315), (758, 273), (796, 295), (812, 270), (850, 273), (880, 225), (880, 400)])
    circle(screen, color, (600, 312), 62)
    ellipse(screen, color, (20, 246, 135, 288))

    ellipse(screen, (255, 213, 170), (640, 220, 170, 80))
    ellipse(screen, (255, 213, 170), (620, 220, 130, 60))
    ellipse(screen, (250, 214, 195), (580, 220, 130, 40))
    rect(screen, (250, 214, 195), (620, 225, 200, 35))

#Water
def draw_water(color):
    '''Function draws top scar
    Attrubutes:
        color : tuple of 3 int
            color down scar      
    '''
    polygon(screen, color, [(0, 392), (880, 373), (880, 569), (0, 560)])

#Down ridge
def draw_down_scar(color1, color2, color3,):
    '''Function draws top scar
    Attrubutes:
        color1 : tuple of 3 int
            color down scar  
        color2 : tuple of 3 int
            color water scar 
        color : tuple of 3 int
            color midlle scar     
    '''
    polygon(screen, color1, [(0, 294), (106, 320), (187, 416), (254, 506), (340, 553), (415, 555), (558, 479), (597, 497), (731, 477), (757, 448), (880, 560), (0, 560)])
    circle(screen, color2, (343, 447), 107)
    circle(screen, color2, (653, 408), 105)
    ellipse(screen, color1, (716, 308, 604, 565))
    polygon(screen, color3, [(242, 386), (329, 290), (469, 382)])
    polygon(screen, color3, [(507, 381), (647, 277), (800, 373)])

#The Sun
def draw_sun(color):
    '''Function draws the sun
    Attrubutes:
        color : tuple of 3 int
            color of the sun      
    '''
    ellipse(screen, color, (368, 93, 100, 91))

#Birds
def draw_bird(x, y, a):
    '''Function draws bird
    Attrubutes:
        x : float
            horizontal coordinate of bird
        y : float
            vertical coordinate of bird
        a : float
            size of bird
    '''
    polygon(screen, (71, 35, 35), [(x, y), (x - round(31/a), y - round(15 / a)), (x - round(36 / a), y - round(18 / a)), (x - round(34/a), y - round(22 / a)), (x - round(22 / a), y - round(20 / a)), (x + round(2 / a), y - round(10 / a)), (x + round(7 / a), y - round(16 / a)), (x + round(12 / a), y - round(19 / a)), (x + round(25 / a), y - round(22 / a)), (x + round(42 / a), y - round(21 / a))])



draw_top_scar(ORANGE)
draw_midlle_scar(BROWN)
draw_water(WATER)
draw_down_scar(BLACK, WATER, BROWN)
draw_sun(YELLOW)

draw_bird(686, 461, 1)
draw_bird(602, 429, 21/13)
draw_bird(553, 391, 1.4)
draw_bird(700, 416, 42/25)
draw_bird(350, 281, 42/29)
draw_bird(419, 257, 1.5)
draw_bird(418, 229, 1.5)
draw_bird(339, 222, 14/9)




pygame.display.update()
clock = pygame.time.Clock()
finished = False

while not finished:
    clock.tick(FPS)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            finished = True

pygame.quit()
