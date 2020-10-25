import pygame
from pygame.draw import *
from random import randint
from math import cos, pi, sin, radians

pygame.init()

NUM = 12
MIN_R = 20
MAX_R = 100
WIDTH = 1200
HEIGHT = 600
FPS = 60
screen = pygame.display.set_mode((WIDTH, HEIGHT))

RED = (255, 0, 0)
BLUE = (0, 0, 255)
YELLOW = (255, 255, 0)
GREEN = (0, 255, 0)
MAGENTA = (255, 0, 255)
CYAN = (0, 255, 255)
BLACK = (0, 0, 0)
COLORS = [RED, BLUE, YELLOW, GREEN, MAGENTA, CYAN]

TYPE = ['CIRCLE', 'SQUARE', 'TRINGLE']




def new_balls(num):
    """
    Функция рисует num мячиков.
    :param num: количество мячиков
    """
    global x, y, r, v, Vy, Vx, alpha, color, type
    x = []
    y = []
    r = []
    v = []
    alpha = []
    color = []
    type = []
    for i in range(num):
        x.append(randint(MAX_R, WIDTH - MAX_R))
        y.append(randint(MAX_R, HEIGHT - MAX_R))
        r.append(randint(MIN_R, MAX_R))
        v.append(randint(10, 500))
        v[i] = float(v[i])
        alpha.append(randint(0, 360))
        alpha[i] = radians(alpha[i])
        color.append(COLORS[randint(0, 5)])
        type.append(TYPE[randint(0, 2)])
        if type[i] == 'CIRCLE':
            circle(screen, color[i], (x[i], y[i]), r[i])
        if type[i] == 'SQUARE':
            rect(screen, color[i], (x[i], y[i], r[i], r[i]))
        if type[i] == 'TRINGLE':
            polygon(screen, color[i], [[x[i], y[i]-r[i]],  [x[i]+0.866*r[i], y[i]+0.5*r[i]],  [x[i]-0.866*r[i], y[i]+0.5*r[i]]])





def move_balls(num):
    """
    Функция отвечает за передвижение мячиков по экрану.
    :param num: колическтво мячиков
    """
    global x, y, r, v, alpha, color, alpha

    for i in range(num):
        if type[i] == 'CIRCLE':
            circle(screen, BLACK, (x[i], y[i]), r[i])
        if type[i] == 'SQUARE':
            rect(screen, BLACK, (x[i], y[i], r[i], r[i]))
        if type[i] == 'TRINGLE':
            polygon(screen, BLACK, [[x[i], y[i]-r[i]],  [x[i]+0.866*r[i], y[i]+0.5*r[i]],  [x[i]-0.866*r[i], y[i]+0.5*r[i]]])
        
        if type[i] == 'CIRCLE':
            x[i] += round(v[i] / FPS * cos(alpha[i]))
            y[i] -= round(v[i] / FPS * sin(alpha[i]))
            circle(screen, color[i], (x[i], y[i]), r[i])
        if type[i] == 'SQUARE':
            v[i] *= randint(90, 110) / 100
            alpha[i] += radians(randint(0, 10) - 5)
            x[i] += round(v[i] / FPS * cos(alpha[i]))
            y[i] -= round(v[i] / FPS * sin(alpha[i]))
            rect(screen, color[i], (x[i], y[i], r[i], r[i]))
        if type[i] == 'TRINGLE':
            x[i] += round(v[i] / FPS * cos(alpha[i]))
            y[i] -= round(v[i] / FPS * sin(alpha[i]))
            polygon(screen, color[i], [[x[i], y[i]-r[i]],  [x[i]+0.866*r[i], y[i]+0.5*r[i]],  [x[i]-0.866*r[i], y[i]+0.5*r[i]]])
        pygame.display.update()
    check_walls(num)


def check_walls(num):
    """
    Функция проверяет удар мячика о стенку и считает новый угол
    :param num: количество мячиков
    """
    global x, y, r, alpha
    for i in range(num):
        Vy=v[i]*sin(alpha[i])
        if type[i] == 'CIRCLE':
            if x[i] + r[i] > WIDTH:
                alpha[i] = radians(90 + randint(10, 170))
            if x[i] - r[i] < 0:
                alpha[i] = radians(randint(10, 170) - 90)
            if y[i] + r[i] > HEIGHT:
                alpha[i] = radians(randint(10, 170))
            if y[i] - r[i] < 0:
                alpha[i] = radians(randint(10, 170) - 180)
        if type[i] == 'SQUARE':
            if x[i] + r[i] > WIDTH:
                alpha[i] = radians(90 + randint(10, 170))
            if x[i] < 0:
                alpha[i] = radians(randint(10, 170) - 90)
            if y[i] + r[i] > HEIGHT - 10:
                alpha[i] = radians(randint(10, 170))
            if y[i] < 0:
                alpha[i] = radians(randint(10, 170) - 180)
        if type[i] == 'TRINGLE':
            if x[i] + r[i] > WIDTH:
                alpha[i] = radians(90 + randint(10, 170))
            if x[i] - r[i] < 0:
                alpha[i] = radians(randint(10, 170) - 90)
            if y[i] + r[i] > HEIGHT:
                alpha[i] = radians(randint(10, 170))
            if y[i] - r[i] < 0:
                alpha[i] = radians(randint(10, 170) - 180)
        alpha[i] %= 2 * pi



def respawn_figure(i):
    """
    Функция заново создаёт мишень после попадания в цель.
    :param i: номер "возрождаемого" элемента
    """
    x[i] = randint(MAX_R, WIDTH - MAX_R)
    y[i] = randint(MAX_R, HEIGHT - MAX_R)
    r[i] = randint(MIN_R, MAX_R)
    v[i] = randint(10, 500)
    alpha[i] = randint(0, 360)
    alpha[i] = radians(alpha[i])
    color[i] = COLORS[randint(0, 5)]
    type[i] = TYPE[randint(0, 2)]
    if type == 'CIRCLE':
        circle(screen, color[i], (x[i], y[i]), r[i])
    if type == 'SQUARE':
        rect(screen, color[i], (x[i], y[i], r[i], r[i]))
    if type[i] == 'TRINGLE':
            polygon(screen, color[i], [[x[i], y[i]-r[i]],  [x[i]+0.866*r[i], y[i]+0.5*r[i]],  [x[i]-0.866*r[i], y[i]+0.5*r[i]]])
    pygame.display.update()


def check_click(event, num):
    """
    Функция проверяет, попал ли игрок по мячику, подсчитывает очки и рисует новые мячики при необходимости.
    :param event: параметры события
    :param num: колличество мячиков
    """
    global score, x, y, r, v, alpha, color
    coord = event.pos
    for i in range(num):
        if type[i] == 'CIRCLE':
            if (x[i] - coord[0]) ** 2 + (y[i] - coord[1]) ** 2 <= r[i] ** 2:
                score += 1
                circle(screen, BLACK, (x[i], y[i]), r[i])

                respawn_figure(i)
        if type[i] == 'SQUARE':
            if 0 <= coord[0] - x[i] <= r[i] and 0 <= coord[1] - y[i] <= r[i]:
                score += 3
                rect(screen, BLACK, (x[i], y[i], r[i], r[i]))
                respawn_figure(i)
        if type[i] == 'TRINGLE':
            if (x[i] - coord[0]) ** 2 + (y[i] - coord[1]) ** 2 <= (r[i] ** 2)/2:
                score += 2
                polygon(screen, BLACK, [[x[i], y[i]-r[i]],  [x[i]+0.866*r[i], y[i]+0.5*r[i]],  [x[i]-0.866*r[i], y[i]+0.5*r[i]]])
                respawn_figure(i)
                return score

def draw_score(points):
    '''
    Функция отображает на экране число набранных очков
    Points : количество очков
    '''
    rect(screen, CYAN, (0, 0, 300, 40))
    my_font = pygame.font.Font(None, 50)
    string = "Points: " + str(points)
    if points < 0:
        text_color = RED
    else:
        text_color = BLACK
    text = my_font.render(string, 1, text_color)
    screen.blit(text, (3, 3))







pygame.display.update()
clock = pygame.time.Clock()
score = 0
finished = False

save_results = False
file = open('result.txt','a')
name = ''

def print_comment(comment, x, y, size):
    font = pygame.font.Font(None, size)
    text = font.render(comment, True, GREEN)
    screen.blit(text, [x, y])

def save_scores(final_score, name):
    if name == '':
        name = 'Player'
    file.write(name + " : " + str(final_score) + '\n')



while not finished:
    clock.tick(FPS)
    new_balls(NUM)
    pygame.display.update()
    f = True
    while f:
        clock.tick(FPS)
        move_balls(NUM)
        draw_score(score)
        for event in pygame.event.get():

            if event.type == pygame.QUIT:
                finished = True
                f = False

            elif event.type == pygame.KEYDOWN:
                save_results = True
                finished = True
                

            elif event.type == pygame.MOUSEBUTTONDOWN:
                check_click(event, NUM)
    screen.fill(BLACK)
    pygame.display.update()






while save_results:
    screen.fill(BLACK)
    clock.tick(FPS)
    print_comment("Enter your name:", 400, 300, 60)
    print_comment("Use only small letters and numbers, please", 350, 350, 30)
    print_comment("Press 'Enter' to save your result", 400, 500, 30)
    print_comment(name, 400, 400, 72)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            save_results = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_RETURN:
                save_results = False
            elif (event.key < 123 and event.key > 96) or (event.key < 58 and event.key > 47):
                name += chr(event.key)
    pygame.display.update()

save_scores(score, name)
file.close()

pygame.quit()
