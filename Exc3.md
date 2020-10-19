import pygame, sys
from pygame.draw import *
from numpy import pi

pygame.init()
white = ((255,255,255))
blue = ((0,0,255))
green = ((0,255,0))
red = ((255,0,0))
black = ((0,0,0))
orange = ((255,100,10))
yellow = ((255,255,0))
blue_green = ((0,255,170))
marroon = ((115,0,0))
lime = ((180,255,100))
pink = ((255,100,180))
purple = ((240,0,255))
gray = ((127,127,127))
magenta = ((255,0,230))
brown = ((100,40,0))
forest_green = ((0,50,0))
navy_blue = ((0,0,100))
rust = ((210,150,75))
dandilion_yellow = ((255,200,0))
highlighter = ((255,255,100))
sky_blue = ((0,255,255))
light_gray = ((200,200,200))
dark_gray = ((50,50,50))
tan = ((230,220,170))
coffee_brown =((200,190,140))
moon_glow = ((235,245,255))

FPS = 30
screen = pygame.display.set_mode((600, 600))
screen.fill(brown)



rect(screen, rust, (0, 250, 600, 450))


#Window
def draw_window(x, y, width, height, pane_color, frame_color):
	''' Function draws a WINDOW
	
	Attrubutes:
	-----------------------------------------------
		x : float
			horizontal coordinate of window center point
		y : float
			vertical coordinate of window top point
		width : float
			horizontal size of the window
		height : float
			vertical size of the window
		frame_color : tuple of 3 int
			color of window frame
		pane_color : tuple of 3 int
			color of window pane
	'''
	rect(screen, pane_color, (x, y, width, height))
	rect(screen, frame_color, (x+0.1*width, y+0.1*height, 0.35*width, 0.35*height))
	rect(screen, frame_color, (x+0.55*width, y+0.1*height, 0.35*width, 0.35*height))
	rect(screen, frame_color, (x+0.1*width, y+0.55*height, 0.35*width, 0.35*height))
	rect(screen, frame_color, (x+0.55*width, y+0.55*height, 0.35*width, 0.35*height))


#Cat's body
def draw_cat(x, y, width, height, hair_color, eyes_color):
	''' Function draws a CAT
	
	Attrubutes:
	-----------------------------------------------
		x : float
			cat horizontal position
		y : float
			cat vertical position
		width : float
			cat's size in horizontal
		height : float
			cat's size in vertical
		hair_color : tuple of 3 int
			color of cat's hair
		eyes_color : tuple of 3 int
			color of cat's eyes
	'''



	ellipse(screen, hair_color, (x+width/3, y-height/6, width/1.5, height/2.5))
	ellipse(screen, black, (x+width/3, y-height/6, width/1.5, height/2.5),1)

	ellipse(screen, hair_color, (x-width/2, y-height/2, width, height))
	ellipse(screen, black, (x-width/2, y-height/2, width, height),1)

	ellipse(screen, hair_color, (x-width/1.75, y-height/8, width/8, height/2))
	ellipse(screen, black, (x-width/1.75, y-height/8, width/8, height/2), 1)

	ellipse(screen, hair_color, (x-4*width/6, y-height/2.5, width/3, height/1.5))
	ellipse(screen, black, (x-4*width/6, y-height/2.5, width/3, height/1.5),1)

	ellipse(screen, hair_color, (x-width/2.3, y+height/4.2, width/4, height/3))
	ellipse(screen, black, (x-width/2.3, y+height/4.2, width/4, height/3),1)

	ellipse(screen, hair_color, (x+width/6, y, width/3, height/1.7))
	ellipse(screen, black, (x+width/6, y, width/3, height/1.7),1)

	ellipse(screen, hair_color, (x+width/2.5, y+height/3, width/7, height/1.7))
	ellipse(screen, black, (x+width/2.5, y+height/3, width/7, height/1.7),1)

#Cat's eyes
	ellipse(screen, green, (x-12*width/24, y-height/4.9, width/10, height/5))
	ellipse(screen, black, (x-12*width/24, y-height/4.9, width/10, height/5), 1)

	ellipse(screen, green, (x-15*width/24, y-height/4.9, width/10, height/5))
	ellipse(screen, black, (x-15*width/24, y-height/4.9, width/10, height/5), 1)

	ellipse(screen, black, (x-11*width/24, y-height/5.3, width/30, height/8))
	ellipse(screen, black, (x-14*width/24, y-height/5.3, width/30, height/8))
#Cat's ear
	polygon(screen, pink, [(x-width/1.6,y-height/2.5), (x-width/1.8,y-height/2.9),
		                               (x-width/1.61,y-height/4)])
	polygon(screen, orange, [(x-width/1.6,y-height/2.5), (x-width/1.8,y-height/2.9),
		                               (x-width/1.61,y-height/4)],3)                               
	polygon(screen, black, [(x-width/1.6,y-height/2.5), (x-width/1.8,y-height/2.9),
		                               (x-width/1.61,y-height/4)], 1)

	polygon(screen, pink, [(x-width/1.6+width/4,y-height/2.5), (x-width/1.75+width/8,y-height/2.9),
		                               (x-width/1.61+width/4,y-height/4)])
	polygon(screen, orange, [(x-width/1.6+width/4,y-height/2.5), (x-width/1.75+width/8,y-height/2.9),
		                               (x-width/1.61+width/4,y-height/4)],3)                               
	polygon(screen, black, [(x-width/1.6+width/4,y-height/2.5), (x-width/1.75+width/8,y-height/2.9),
		                               (x-width/1.61+width/4,y-height/4)], 1)
#Cat's nose
	polygon(screen, black, [(x-width/1.89, y+height/30), (x-width/2.04, y+height/30),
	                               (x-width/1.98, y+height/15)])
	pygame.draw.line(screen, black, (x-width/1.98, y+height/15), (x-width/1.98, y+height/10), 1)
	pygame.draw.arc(screen, black, (x-width/1.98, y+height/12, width/20, height/20), pi, pi+pi, 1)
	pygame.draw.arc(screen, black, (x-width/1.98-width/20, y+height/12, width/20, height/20), pi, pi+pi, 1)

	pygame.draw.arc(screen, black, (x-width/2.1, y+height/17, width/6, height/15),0, ((pi+pi+pi+pi+pi)/6), 1)
	pygame.draw.arc(screen, black, (x-width/2.1, y+height/11, width/6, height/15),0, ((pi+pi+pi+pi+pi)/6), 1)
	pygame.draw.arc(screen, black, (x-width/2.1, y+height/7, width/6, height/15),0, ((pi+pi+pi+pi+pi)/6), 1)
	pygame.draw.arc(screen, black, (x-width/1.4, y+height/17, width/6, height/15), pi/6,pi, 1)
	pygame.draw.arc(screen, black, (x-width/1.4, y+height/11, width/6, height/15), pi/6,pi, 1)
	pygame.draw.arc(screen, black, (x-width/1.4, y+height/7, width/6, height/15), pi/6,pi, 1)





#Ball
	''' Function draws a BALL
	
	Attrubutes:
	-----------------------------------------------
		x : float
			ball horizontal position
		y : float
			ball vertical position
		diameter : float
			ball diameter
		ball_color : tuple of 3 int
			color of ball
		fiber_color : tuple of 3 int
			color of ball border and fiber lines
	'''
def draw_ball(x, y, diameter, ball_color, fiber_color):
	circle(screen, ball_color, (x, y), diameter)
	circle(screen, fiber_color, (x, y), diameter, 1)
	pygame.draw.arc(screen, black, (x+diameter/8,y+ diameter/4, diameter/2, diameter/3), pi/6,pi, 1)
	pygame.draw.arc(screen, black, (x+diameter/8,y+ diameter/2.5, diameter/2, diameter/3), pi/6,pi, 1)
	pygame.draw.arc(screen, black, (x+diameter/8,y+ diameter/2, diameter/2, diameter/3), pi/6,pi, 1)

	pygame.draw.arc(screen, black, (x+diameter/4,y+ diameter/3, diameter/2, diameter/3), pi+pi/4,pi+pi, 1)
	pygame.draw.arc(screen, black, (x+diameter/4,y+ diameter/2.5, diameter/2, diameter/3), pi+pi/4,pi+pi, 1)
	pygame.draw.arc(screen, black, (x+diameter/4,y+ diameter/2, diameter/2, diameter/3), pi+pi/4,pi+pi, 1)

	pygame.draw.arc(screen, black, (x-1.5*diameter,y+ 0.84*diameter, 2*diameter, diameter/2), pi/6,pi, 1)



draw_window(60, 20, 120, 150, navy_blue, sky_blue)
draw_window(230, 20, 120, 150, navy_blue, sky_blue)
draw_window(400, 20, 120, 150, navy_blue, sky_blue)

draw_cat(100, 300, 120, 60, orange, green)
draw_cat(430, 300, 150, 75, gray, green)
draw_cat(300, 460, 200, 100, yellow, green)

draw_ball(160, 540, 40, gray, black)	
draw_ball(80, 400, 35, pink, black)	
draw_ball(270, 310, 30, white, black)	
draw_ball(530, 530, 45, coffee_brown, black)

pygame.display.update()
clock = pygame.time.Clock()
finished = False

while not finished:
    clock.tick(FPS)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            finished = True

pygame.quit()

